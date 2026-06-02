pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/cybe44oot/Mega-Project-CD.git'
            }
        }
        
        stage('Kubernetes Deployment') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'https://A385AC9BFF829E9144AA7129151C1092.gr7.eu-north-1.eks.amazonaws.com', contextName: '', credentialsId: 'k8s-token', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://A385AC9BFF829E9144AA7129151C1092.gr7.eu-north-1.eks.amazonaws.com') {
                    sh "kubectl apply -f Manifest/manifest.yaml -n webapps"
                    sh "kubectl apply -f Manifest/HPA.yaml"
                    sleep 30
                    sh "kubectl get pods -n webapps"
                    sh "kubectl get service -n webapps"
                }
            }
        }
    }
}
