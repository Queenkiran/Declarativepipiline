pipeline
{
    agent any
    stages
    {
        stage('Download')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('Build')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('Deployment')
        {
            steps
            {
               deploy adapters: [tomcat9(credentialsId: 'f8ad942f-8bcb-47ed-b43f-4f6b6a916253', path: '', url: 'http://172.31.38.11:8080')], contextPath: 'testapp1', war: '**/*.war'
            }
        }
        stage('Testing')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                
                sh 'java -jar /home/ubuntu/.jenkins/workspace/Declarativepipeline/testing.jar'
            }
        }
        stage('Delivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'f8ad942f-8bcb-47ed-b43f-4f6b6a916253', path: '', url: 'http://172.31.44.14:8080')], contextPath: 'prodapp1', war: '**/*.war'
            }
        }
    }
}
