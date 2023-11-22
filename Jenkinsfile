pipeline {
    agent any

    stages {
        stage('Récupération de l\'applicatif') {
            steps {
                git url: 'https://AuceaneH:token@github.com/AuceaneH/HelloWorld.git'
                script {
                    // Copiez le fichier HelloWorld.java dans /tmp
                    sh 'rm -f /tmp/*.java'
                    sh 'cp HelloWorld.java /tmp'
                }
            }
        }
        
        stage('Build de l\'applicatif') {
            steps {
                dir('/tmp') {
                    sh 'javac HelloWorld.java'
                    sh 'java HelloWorld'
                }
            }
        }
        
        stage("Tag Version. Release") {
            environment { 
                GIT_TAG = "Version-2.$BUILD_NUMBER"
            }
            steps {
                script {
                    // Création et poussée du tag Git
                    sh "git tag -a \$GIT_TAG -m \"[Jenkins CI] New Tag\""
                    sh "git push origin \$GIT_TAG"
                }
            }
        }
    }
}
