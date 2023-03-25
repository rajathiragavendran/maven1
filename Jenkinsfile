pipeline
{
    agent any
    stages
    {
        stage('continuousdownload')
        {
            steps
            {
                git 'https://github.com/rajathiragavendran/maven1.git' 
            }
        }
        stage('continuousbuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('continuousdeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '18419657-abc7-4eef-8139-22e47b3605fb', path: '', url: 'http://172.31.0.69:8080')], contextPath: 'testing', war: '**/*.war'
            }
        }
       stage('continuoustesting')
        {
            steps
            {
                git 'https://github.com/rajathiragavendran/functionaltesting.git'
                sh '''java -jar /var/lib/jenkins/workspace/declarativepipeline/testing.jar'''
            }
        } 
        stage('continuousdelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '18419657-abc7-4eef-8139-22e47b3605fb', path: '', url: 'http://172.31.2.171:8080')], contextPath: 'delivery', war: '**/*.war'
            }
        } 
    }    
}
