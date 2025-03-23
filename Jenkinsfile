pipeline {
    agent any
    
    tools {
        nodejs 'NodeJS 23' // Substitua 'NodeJS 16' pelo nome que você configurou
    }

    environment {
        NODE_ENV = 'development'
    }

    stages {
        stage('Checkout') {
            steps {
                // Fazer checkout do código no repositório
                git branch: 'master', url: 'https://github.com/ruan-cardozo/task-track-api.git'
            }
        }
        
        stage('Install Dependencies') {
            steps {
                // Instalar dependências do projeto usando npm
                sh 'npm install'
            }
        }
        
        stage('Run Linter') {
            steps {
                // Verificar qualidade do código com ESLint
                sh 'npm run lint'
            }
        }

        stage('Run Tests') {
            steps {
                // Rodar testes unitários com Jest
                sh 'npm run test'
            }
        }

        stage('Build') {
            steps {
                // Construir o projeto NestJS (compilar TypeScript)
                sh 'npm run build'
            }
        }
    }

    post {
        success {
            // Notificar sucesso
            echo 'Build and tests completed successfully!'
        }
        failure {
            // Notificar falha
            echo 'Build or tests failed.'
        }
    }
}
