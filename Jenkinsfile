pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh """
                R=$(od -An -N1 -i /dev/random)
                echo $R > result
                """
            }
        }

        stage('Test') {
            steps {
                sh """
                R=$(cat result)
                if [ $((R < 0.5)) ]
                then
                   echo test failed
                   exit 1
                fi
                """
            }
        }

        stage('Deploy - Staging') {
            steps {
                echo 'Cool! all ok'
            }
        }

        stage('Sanity check') {
            steps {
                input "Does the staging environment look ok?"
            }
        }

        stage('Deploy - Production') {
            steps {
                sh './deploy production'
            }
        }
    }
}
