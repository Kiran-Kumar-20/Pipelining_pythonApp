pipeline {
    agent any

    environment {
        VENV = "venv"
    }

    stages {
        stage('Clone GitHub Repo') {
            steps {
                git branch: 'main', credentialsId: 'github-https', url: 'https://github.com/Kiran-Kumar-20/Pipelining_pythonApp.git'
            }
        }

        stage('Set Up Python Virtual Environment') {
            steps {
                // Create virtual environment
                bat '"C:\\Users\\kiran\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" -m venv %VENV%'

                // Upgrade pip, setuptools, wheel
                bat ".\\%VENV%\\Scripts\\python.exe -m pip install --upgrade pip setuptools wheel"

                // Force pip to use prebuilt binaries (avoid compiling pandas)
                bat ".\\%VENV%\\Scripts\\pip.exe install --only-binary :all: pandas"

                // Install the rest of the requirements
                bat ".\\%VENV%\\Scripts\\pip.exe install --prefer-binary -r requirements.txt"
            }
        }

        stage('Run Flask App') {
            steps {
                bat ".\\%VENV%\\Scripts\\python.exe hello.py"
            }
        }
    }
}
