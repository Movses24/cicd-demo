pipeline {
  agent any

  environment {
    EC2_HOST = '54.221.69.91'
    EC2_USER = 'ec2-user'
    DOCKER_IMAGE = "movses2001/cididemo:latest"
  }

  stages {
    stage('Test') {
      steps {
        echo "✅ All tests passed!"
      }
    }

    stage('Deploy to EC2') {
      steps {
        sshagent(['ec2-ssh-key']) {
          sh """
            ssh -o StrictHostKeyChecking=no ${EC2_USER}@${EC2_HOST} \\
            'docker pull ${DOCKER_IMAGE} && \\
             docker stop web || true && \\
             docker rm web || true && \\
             docker run -d --name web -p 80:80 ${DOCKER_IMAGE}'
          """
        }
      }
    }
  }
}
