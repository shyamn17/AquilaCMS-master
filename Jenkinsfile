pipeline {
    agent any

    environment {
        NODE_VERSION = '14'  // Set your Node.js version
        DEPLOY_DIR = '/var/www/html'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Prepare Server') {
            steps {
                sh "mkdir -p $DEPLOY_DIR"
                sh "apt-get update"
                sh "apt-get install -y nginx"
            }
        }

        stage('Deploy') {
            steps {
                sh "cd $DEPLOY_DIR"
                sh "git pull"  // Fetch the latest code from your Git repository

                // Build the React front-end (if applicable)
                sh "npm install"  // Install Node.js dependencies
                sh "npm run build"  // Build the React app

                // Start or restart the Node.js server (replace 'your-app-name' and 'path-to-your-app.js')
                sh "pm2 stop your-app-name || true"  // Stop the existing Node.js server
                sh "pm2 start path-to-your-app.js --name your-app-name"  // Start the Node.js server

                // Update Nginx configuration (replace 'mern' and '3000' with your actual values)
                sh "sed -i 's/mern/your-app-name/g' /etc/nginx/sites-available/mern"
                sh "sed -i 's/3000/your-app-port/g' /etc/nginx/sites-available/mern"
                sh "ln -sf /etc/nginx/sites-available/mern /etc/nginx/sites-enabled/"

                // Test Nginx configuration and reload
                sh "nginx -t"
                sh "systemctl reload nginx"
            }
        }

        stage('Testing') {
            steps {
                // Run tests (if applicable)
                // Add testing commands here
            }
        }
    }

    post {
        success {
            echo 'Deployment successful'
        }
        failure {
            echo 'Deployment failed'
        }
    }
}
