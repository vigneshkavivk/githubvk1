podTemplate(
    label: 'jenkins-agent',
    containers: [
        containerTemplate(
            name: 'jnlp',  // Jenkins default agent container
            image: 'jenkins/inbound-agent',
            args: '${computer.jnlpmac} ${computer.name}'
        ),
        containerTemplate(
            name: 'ubuntu',  // Ubuntu container where we will install Trivy
            image: 'ubuntu:latest',
            command: 'sleep',
            args: '999999'
        )
    ]
) {
    node('jenkins-agent') {
        stage('Install Trivy') {
            container('ubuntu') {
                sh '''
                apt-get update -y
                apt-get install -y wget
                wget https://github.com/aquasecurity/trivy/releases/latest/download/trivy_0.50.2_Linux-64bit.deb
                dpkg -i trivy_0.50.2_Linux-64bit.deb
                trivy --version
                '''
            }
        }

        stage('Trivy Scan') {
            container('ubuntu') {
                sh '''
                trivy fs --format table -o trivy-fs-report.html .
                '''
            }
        }
    }
}
