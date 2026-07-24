pipeline {
    agent any

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

                // ДОБАВЛЕНО: Проверяем, что создалось в папке
                echo '=== Проверяем содержимое папки dist ==='
                sh 'ls -la'
                sh 'ls -la dist || echo "Папка dist не найдена или пуста!"'
            }
        }
    }

    post {
        success {
            echo '✅ Сборка прошла успешно!'
            archiveArtifacts artifacts: 'dist/**', allowEmptyArchive: true
        }
        failure {
            echo '❌ Ошибка сборки.'
        }
    }
}
