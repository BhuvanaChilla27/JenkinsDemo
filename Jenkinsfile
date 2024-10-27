pipeline {
    agent any
    stages {
        stage('Build') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
               sh '''
                   ls -la
                   node --version
                   npm --version
                   npm ci
                   npm run build
                   ls -la
               '''
            }
        }
        stage('Test') {
              steps{
                echo "Test stage... "
               if [ -f build/index.html ]; then
                  echo "index.html exists in the build directory."
               else
                  echo "index.html does not exist in the build directory."
                  exit 1  # Exit with non-zero status to indicate failure
               fi
            }
        }
    }
}
