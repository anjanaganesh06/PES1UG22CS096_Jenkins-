pipeline {
    agent any

    environment {
        SRN = "PES1UG22CS096"  // Replace with your actual SRN
        CPP_FILE = "program.cpp"
        BUILD_OUTPUT = "program.out"
        REPO_URL = "https://github.com/YOUR_USERNAME/YOUR_REPO.git"
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    sh "git clone ${REPO_URL} repo"
                    sh "cd repo && touch ${CPP_FILE} && echo '#include <iostream>\nint main() { std::cout << \"Hello, Jenkins!\" << std::endl; return 0; }' > ${CPP_FILE}"
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    sh """
                    g++ -o ${BUILD_OUTPUT} repo/${CPP_FILE}
                    echo "Build completed: ${BUILD_OUTPUT}"
                    """
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    sh """
                    ./repo/${BUILD_OUTPUT}
                    """
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh """
                    cd repo
                    git config --global user.email "you@example.com"
                    git config --global user.name "Your Name"
                    git add ${CPP_FILE}
                    git commit -m "Added working C++ file"
                    git push origin main
                    echo "Code pushed to repository"
                    """
                }
            }
        }
    }

    post {
        failure {
            echo "🚨 Pipeline failed! Please check the logs."
        }
        success {
            echo "✅ Pipeline completed successfully!"
        }
    }
}
