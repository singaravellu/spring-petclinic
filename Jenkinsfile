pipeline{
    agent { label 'redhat' }
    stages{
        stage('scm'){
            steps {
                    git 'https://github.com/dummyrepos/spring-petclinic.git'
            }
        }
        stage('Package'){
            steps {
                sh 'mvn package'
            }
        }

    }
}
