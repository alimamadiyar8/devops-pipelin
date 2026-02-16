pipeline {
    agent any
    
    stages {
        stage('Checkout Code') {
            steps {
                echo 'Забираем код из GitHub...'
                checkout scm
            }
        }
        
        stage('Check Files') {
            steps {
                echo 'Проверяем созданные файлы...'
                bat '''
                    @echo off
                    echo === ФАЙЛЫ В РЕПОЗИТОРИИ ===
                    dir
                    echo.
                    
                    echo === ПРОВЕРКА НАШИХ ФАЙЛОВ ===
                    
                    if exist Dockerfile (
                        echo ✅ Dockerfile найден
                    ) else (
                        echo ❌ Dockerfile не найден
                    )
                    
                    if exist requirements.txt (
                        echo ✅ requirements.txt найден
                    ) else (
                        echo ❌ requirements.txt не найден
                    )
                    
                    if exist src (
                        echo ✅ Папка src найдена
                        if exist src\\app.py (
                            echo ✅ Файл src/app.py найден
                        ) else (
                            echo ❌ Файл src/app.py не найден
                        )
                    ) else (
                        echo ❌ Папка src не найдена
                    )
                    
                    if exist .dockerignore (
                        echo ✅ .dockerignore найден
                    ) else (
                        echo ❌ .dockerignore не найден
                    )
                '''
            }
        }
        
        stage('Docker Theory') {
            steps {
                echo 'ТЕОРИЯ DOCKER'
                echo 'Если бы Jenkins не был в Docker, мы бы выполнили:'
                echo '1. docker build -t my-app .'
                echo '2. docker run -d -p 8081:5000 my-app'
                echo '3. curl http://localhost:8081/health'
                echo ''
                echo 'Но так как Jenkins в Docker, эти команды могут не работать.'
                echo 'Это нормально! Главное - понять процесс.'
            }
        }
        
        stage('Try Docker Commands') {
            steps {
                echo 'Пробуем Docker команды...'
                script {
                    try {
                        bat 'docker --version || echo Docker не доступен'
                        bat '''
                            echo Пробуем собрать Docker образ...
                            docker build -t test-image . 2>nul || echo Не удалось собрать образ
                        '''
                    } catch (Exception e) {
                        echo "Docker команды не работают. Это ожидаемо!"
                        echo "Причина: Jenkins запущен на Windows"
                    }
                }
            }
        }
    }
    
    post {
        always {
            echo '=== ИТОГ РАБОТЫ ==='
            bat '''
                @echo off
                echo Дата: %date% %time%
                echo Процесс CI/CD понятен?
                echo 1. Код РЄ GitHub
                echo 2. GitHub РЄ Jenkins
                echo 3. Jenkins проверяет файлы
                echo 4. Docker теория изучена
            '''
        }
        success {
            echo 'ОТЛИЧНО! Вы поняли процесс CI/CD!'
            echo 'Даже если Docker не работал - вы молодец!'
        }
        failure {
            echo 'Были ошибки, но это часть обучения!'
            echo 'Главное - файлы созданы и процесс понят.'
        }
    }
}
