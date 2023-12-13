pipeline
{
    agent any
    stages
    {
        stage('ContinuosDownload')
        {
            steps
            {
                git 'https://github.com/bharathkumar080/maven.git'
            }
        }
        stage('ContinuosBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContinuosDeployment')
        {
            steps
            {
               deploy adapters: [tomcat9(credentialsId: '203cdae9-fd6d-43ba-bbaf-32167f14b10a', path: '', url: 'http://172.31.40.25:8080')], contextPath: 'testingapp', war: '**/*.war'
            }
        }
        stage('ContinuosTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                
                sh 'java -jar /var/lib/jenkins/workspace/DeclerativePipeline/testing.jar'
            }
        }
        stage('ContinuosDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '203cdae9-fd6d-43ba-bbaf-32167f14b10a', path: '', url: 'http://172.31.32.135:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
