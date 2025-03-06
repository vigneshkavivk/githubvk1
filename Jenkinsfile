podTemplate(
    label: 'trivy-agent',
    containers: [
        containerTemplate(
            name: 'trivy', 
            image: 'aquasec/trivy:latest', 
            command: 'cat', 
            ttyEnabled: true
        )
    ]
) {
    node('trivy-agent') {
        stage('Trivy Scan') {
            container('trivy') {
                sh '''
                trivy image nginx:latest
                '''
            }
        }
    }
}
