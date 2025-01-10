pipeline
{
    agent any
    stages
    {
        stage('Continuous Download')
        {
            steps
            {
               git 'https://github.com/IntelliqDevops/maven.git' 
            }
        }
        stage('Continuous Build')
        {
            steps
            {
              sh 'mvn package'  
            }
        }
        stage('Continuous Deployment')
        {
            steps
            {deploy adapters: [tomcat9(credentialsId: '3fc91db5-bad6-498b-8a31-3c19b30e6cbd', path: '', url: 'http://172.31.83.236:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('Continuous Testing')
        {
            steps
            {
                git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/ScriptedPipeline1/testing.jar'
            }
        }
        stage('Continuous Delivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '3fc91db5-bad6-498b-8a31-3c19b30e6cbd', path: '', url: 'http://172.31.91.82:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
