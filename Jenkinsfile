pipeline {
    agent any

    stages {
        stage('Get the Code !') {
            steps {
                git branch: 'main', url: 'https://github.com/corentin-godefroy/OSDetector'
            }
        }

        stage('Setting permissions and running the script') {
            steps {
                sh 'chmod +x OSDetector.py'
                sh 'python3 OSDetector.py'
            }
        }
    }

    post {
        success {
            echo 'It worked, you Geniuuuus !'
        }
        failure {
            echo 'Ohh god, we are in troubles'
            script {
                def emailBody = "Bonjour,\n\nLa construction et l'exécution du script ont échoué. Veuillez vérifier les journaux de construction Jenkins pour plus de détails.\n\nCordialement,\nL'équipe DevOps"
                emailext (
                    subject: 'Échec de la construction Jenkins',
                    body: emailBody,
                    recipientProviders: [[$class: 'CulpritsRecipientProvider']],
                    to: 'coco241200@gmail.com'
                )
            }
        }
    }
}
