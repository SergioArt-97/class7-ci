pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // This checks out the code from the repository.
                git(url: 'https://github.com/EduardUsatchev/class7-ci.git', branch: 'main')
            }
        }
        stage('Run Script') {
    steps {
        script {
            def branch = sh(script: "git rev-parse --abbrev-ref HEAD", returnStdout: true).trim()
            echo "Detected branch: ${branch}"

            if (branch == 'main') {
                echo "Running myapp.py on main branch..."
                sh 'python myapp.py'
            } else if (branch.startsWith("feature")) {
                echo "Running myapp.py on a feature branch..."
                sh 'python myapp.py'
                error("Intentional failure for feature branch")
            } else {
                echo "Branch ${branch} does not trigger any specific action."
            }
        }
    }
}
