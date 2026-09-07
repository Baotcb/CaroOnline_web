pipeline {
    agent any
    
   
    tools {
        nodejs 'NodeJS' 
    }
    
    environment {
        NETLIFY_SITE_ID = credentials('netlify-site-id')
        NETLIFY_AUTH_TOKEN = credentials('netlify-auth-token')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
            }
        }
        
        stage('Build Angular') {
            steps {
                sh 'npm run build -- --configuration production'
            }
        }
        
        stage('Deploy to Netlify') {
            steps {

                sh 'npx netlify-cli deploy --dir=dist/caro-online/browser --site $NETLIFY_SITE_ID --auth $NETLIFY_AUTH_TOKEN --prod'
            }
        }
    }
}
