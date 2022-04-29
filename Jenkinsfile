pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
                retry(3) {
                    sh '''
                      R=$(od -An -N1 -i /dev/random)
                      echo retry R=$R
                      echo trying flakey... ; [ "$R" % 2 -eq 0 ] && exit 1
                    '''
                }
                timeout(time: 5, unit: 'SECONDS') {
                  R=$(od -An -N1 -i /dev/random)
                  echo timeout R=$R
                  sh 'echo trying slow... ; [ "$R" % 2 -eq 0 ] && sleep 10
                }
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
