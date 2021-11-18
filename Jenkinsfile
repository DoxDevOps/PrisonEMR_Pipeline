pipeline {
  agent any
  stages {
    stage('Initializing') {
      steps {
        echo 'Initializing ...'
        sh 'echo "Working from $WORKSPACE"'
        sh '''echo "Your build number is: \\${BUILD_NUMBER} -> ${BUILD_NUMBER}"
echo "Your build number is: \\${REQUEST_ID} -> ${REQUEST_ID}"'''
      }
    }

    stage('Fetching Repos') {
      parallel {
        stage('Fetching backend') {
          steps {
            echo 'Starting to fetch API from GitHub'
            echo 'Checking if folder exists.'
            sh '[ -d "prisonemr_backend" ] && echo "folder already cloned." || git clone https://zio-git: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@github.com/EGPAFMalawiHIS/prisonemr_backend.git'
            echo 'Giving access to all users'
            sh 'cd $WORKSPACE && chmod 777 prisonemr_backend'
            echo 'Fetching Tags'
            sh 'cd $WORKSPACE/prisonemr_backend && git fetch --tags -f'
          }
        }

        stage('Fetching frontend') {
          steps {
            echo 'checking if folder exist'
            sh '[ -d "prisoner" ] && echo "Core already cloned." || git clone https://zio-git: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@github.com/EGPAFMalawiHIS/prisonemr.git'
            echo 'Giving access to users'
            sh 'cd $WORKSPACE && chmod 777 prisonemr'
            echo 'Fetching New Tags'
            sh 'cd $WORKSPACE/prisonemr && git fetch --tags -f'
          }
        }

      }
    }

    stage('Shipping & Configurations') {
      parallel {
        stage('API') {
          steps {
            echo 'shipping & Configuring API'
            sh '''#python3 api_shippingx.py



'''
          }
        }

        stage('Core & ART') {
          steps {
            echo 'Shipping & configuring Core & ART'
            sh '''#python3 core_shippingx.py
#python3 art_shippingx.py'''
          }
        }

      }
    }

  }
  environment {
    REQUEST_ID = 'true'
    CLUSTER_ID = '12345'
  }
}