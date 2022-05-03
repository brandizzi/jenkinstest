pipeline {
    agent {
        label '!windows'
    }

    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'sqlite'
        DB_USER_PASSWD = credentials('DBCREDENTIALS')
    }

    stages {
        stage('Build') {
            steps {
                echo "Database engine is ${DB_ENGINE}"
                echo "DISABLE_AUTH is ${DISABLE_AUTH}"
                sh 'echo "connect -u $DB_USER_PASSWD Localhost"'
                sh """
                    echo "notthisway -u $DB_USER_PASSWD Localhost"
                """
                sh 'printenv'
            }
        }
    }
}
