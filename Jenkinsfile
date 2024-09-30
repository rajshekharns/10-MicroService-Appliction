pipeline {
    agent any

    environment{
        SCANNER_HOME = tool 'sonar-scanner'
    }
    
    stages {
        stage('Git Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/latest']], extensions: [], userRemoteConfigs: [[credentialsId: 'github_token', url: 'https://github.com/rajshekharns/10-MicroService-Appliction.git/']])
            }
        }
        
        stage('sonarQube') {
            steps {
                withSonarQubeEnv("sonar")
                sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=Ecom-microsvc-project -Dsonar.projectName=Ecom-microsvc-project -Dsonar.java.binaries=. '''
                
            }
        }
        
        stage('adservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker'){
                        dir('var/lib/jenkins/workspace/Ecom-microsvc-project/src/adservice')
                            sh "docker build -t rajns/adservice:latest ."
                            sh "docker push rajns/adservice:latest"
                            sh "docker rmi rajns/adservice:latest"
                    }
                }
            }
        }
        
        stage('cartservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker'){
                        dir('var/lib/jenkins/workspace/Ecom-microsvc-project/src/cartservice/src/')
                            sh "docker build -t rajns/cartservice:latest ."
                            sh "docker push rajns/cartservice:latest"
                            sh "docker rmi rajns/cartservice:latest"
                    }
                }
            }
        }
        
        stage('productcatalogservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker'){
                        dir('var/lib/jenkins/workspace/Ecom-microsvc-project/src/productcatalogservice')
                            sh "docker build -t rajns/productcatalogservice:latest ."
                            sh "docker push rajns/productcatalogservice:latest"
                            sh "docker rmi rajns/productcatalogservice:latest"
                    }
                }
            }
        }
        
        stage('currencyservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker'){
                        dir('var/lib/jenkins/workspace/Ecom-microsvc-project/src/currencyservice')
                            sh "docker build -t rajns/currencyservice:latest ."
                            sh "docker push rajns/currencyservice:latest"
                            sh "docker rmi rajns/currencyservice:latest"
                    }
                }
            }
        }
        
        stage('paymentservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker'){
                        dir('var/lib/jenkins/workspace/Ecom-microsvc-project/src/paymentservice')
                            sh "docker build -t rajns/paymentservice:latest ."
                            sh "docker push rajns/paymentservice:latest"
                            sh "docker rmi rajns/paymentservice:latest"
                    }
                }
            }
        }
        
        stage('emailservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker'){
                        dir('var/lib/jenkins/workspace/Ecom-microsvc-project/src/emailservice')
                            sh "docker build -t rajns/emailservice:latest ."
                            sh "docker push rajns/emailservice:latest"
                            sh "docker rmi rajns/emailservice:latest"
                    }
                }
            }
        }
        
        stage('loadgenerator') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker'){
                        dir('var/lib/jenkins/workspace/Ecom-microsvc-project/src/loadgenerator')
                            sh "docker build -t rajns/loadgenerator:latest ."
                            sh "docker push rajns/loadgenerator:latest"
                            sh "docker rmi rajns/loadgenerator:latest"
                    }
                }
            }
        } 
        
        stage('frontend') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker'){
                        dir('var/lib/jenkins/workspace/Ecom-microsvc-project/src/frontend')
                            sh "docker build -t rajns/frontend:latest ."
                            sh "docker push rajns/frontend:latest"
                            sh "docker rmi rajns/frontend:latest"
                    }
                }
            }
        } 
        
        stage('shippingservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker'){
                        dir('var/lib/jenkins/workspace/Ecom-microsvc-project/src/shippingservice')
                            sh "docker build -t rajns/shippingservice:latest ."
                            sh "docker push rajns/shippingservice:latest"
                            sh "docker rmi rajns/shippingservice:latest"
                    }
                }
            }
        }
        
        stage('checkoutservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker'){
                        dir('var/lib/jenkins/workspace/Ecom-microsvc-project/src/checkoutservice')
                            sh "docker build -t rajns/checkoutservice:latest ."
                            sh "docker push rajns/checkoutservice:latest"
                            sh "docker rmi rajns/checkoutservice:latest"
                    }
                }
            }
        }
        
        stage('recommendationservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker'){
                        dir('var/lib/jenkins/workspace/Ecom-microsvc-project/src/recommendationservice')
                            sh "docker build -t rajns/recommendationservice:latest ."
                            sh "docker push rajns/recommendationservice:latest"
                            sh "docker rmi rajns/recommendationservice:latest"
                    }
                }
            }
        }
        
        stage('k8s-Deploy') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'my-eks', contextName: '', credentialsId: 'k8s-sa-token', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://846861BF7A1719C545B5455687AECA42.gr7.us-east-1.eks.amazonaws.com') {
                    
                    sh 'kubectl apply -f deployment-service.yml'
                    sh 'kubectl get pods'
                    sh 'kubectl get svc'
                    
                    
                }
            }
        }
        
        
        
        
    }
    
}
