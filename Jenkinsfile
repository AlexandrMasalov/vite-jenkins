pipeline {
    agent any

    // Используем Node.js, который мы настроили ранее
    tools {
        nodejs 'NodeJS'
    }

    stages {
        stage('Установка зависимостей') {
            steps {
                echo 'Устанавливаем пакеты...'
                sh 'npm ci'
            }
        }

        stage('Сборка проекта') {
            steps {
                echo 'Собираем Vite проект...'
                sh 'npm run build'
            }
        }
    }

    post {
        success {
            echo '✅ Сборка прошла успешно!'
            // Сохраняем папку dist как артефакт сборки
            archiveArtifacts artifacts: 'dist/**', allowEmptyArchive: true
        }
        failure {
            echo '❌ Ошибка сборки. Проверь код или зависимости.'
        }
    }
}
