pipeline {
  agent any
  stages {
    stage('Build') {
      parallel {
        stage('Server') {
          agent {
            docker {
              image 'maven:3.5-jdk-8-slim'
            }

          }
          steps {
            sh 'echo "Building the server code..."'
            sh 'mvn -version'
            sh 'mkdir -p target'
            sh 'touch "target/server.war"'
            stash(name: 'server', includes: '**/*.war')
          }
        }

        stage('Client') {
          agent {
            docker {
              image 'node:6'
              args '-u 0:0'
            }

          }
          steps {
            sh 'echo "Building the client node..."'
            sh 'npm install --save react'
            sh 'mkdir -p dist'
            sh '''cat > dist/index.html <<EOF
hello!
EOF'''
            sh 'touch "dist/client.js"'
          }
        }

      }
    }

  }
}