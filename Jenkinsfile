pipeline {
    agent any
    stages {
        stage('CMS'){
            steps {
                echo 'Gathering code from version control...'
                git branch:'${branch}' , url: 'https://github.com/agustinmerino/hello-world.git'
            }
        }
        stage('Build Application') {
            steps {
                sh '/opt/maven/bin/mvn -f pom.xml clean install package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Deploy Application') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'tomcat_user', path: '', url: 'http://34.205.33.125:8080')], contextPath: 'webapp/target', war: '**/*.war'
            }            
        }       

    }
}
