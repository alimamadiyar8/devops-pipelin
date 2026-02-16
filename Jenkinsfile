pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building application...'
                echo 'Компиляция кода'
                echo 'Сборка артефактов'
            }
        }
        
        stage('Test') {
            steps {
                echo 'Testing application...'
                echo 'Запуск модульных тестов'
                echo 'Проверка качества кода'
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                echo 'Копирование файлов на сервер'
                echo 'Перезапуск сервиса'
            }
        }
    }
    
    post {
        success {
            echo '✅ Поздравляю! Pipeline выполнен успешно!'
        }
        failure {
            echo '❌ Что-то пошло не так. Проверьте логи.'
        }
    }
}
