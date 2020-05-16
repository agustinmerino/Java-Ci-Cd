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
                sh '/opt/maven/bin/mvn -f pom.xml clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }       

    }
}
