pipeline{
    agent any
    tools { 
        maven 'maven3'
    }
    stages
       {
            stage("clean")
            {
                steps{
                    sh "mvn clean"
                }
            }
            stage("Build")
            {
                steps{
                    sh "mvn compile"
                }
                
            }
            stage("TEST")
            {
                steps{
                    sh "mvn test"
                }
            }
            stage("package")
            {
                steps{
                    sh "mvn package"
                }
            }
        stage("Deploy")
            {
                steps{
                    sshagent(['balraj_deploy']) {
                    sh "scp -o StrictHostKeyChecking=no  /var/lib/jenkins/workspace/Final_project_prod/target/*.jar ubuntu@54.167.173.50:/home/ubuntu/"
                               
                 }
              }
           }
       }

   post {
        always{
            mail to: 'balraj.sabharwal@knoldus.com',
			subject: "Pipeline: ${currentBuild.fullDisplayName} is ${currentBuild.currentResult}",
			body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}"
           }

        }

}
