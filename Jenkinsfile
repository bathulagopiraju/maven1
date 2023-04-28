pipeline
{
    agent any
    stages
    {
        stage('ContDownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '1fdf3df7-3a81-4b74-a6bd-98d4f5483d4e', path: '', url: 'http://172.31.13.245:8080')], contextPath: 'test1', war: '**/*.war'
            }
        }
        stage('ContTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh '''java -jar /var/lib/jenkins/workspace/DeclarativePipeline/testing.jar'''
            }
        }
        stage('ContDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '82fb6ea0-6b5b-43f2-a971-34abf401dde6', path: '', url: 'http://172.31.6.239:8080')], contextPath: 'prod1', war: '**/*.war'
            }
        }
    }
}
