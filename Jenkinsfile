pipeline {
  agent any
  tools { 
        maven 'Maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=p_devsecops_webapp -Dsonar.organization=p-devsecops -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=519bdd08b9fe98854a40dd64effd0b0f9cdfba1d'
			}
    }

	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }

	// stage('Build') { 
 //            steps { 
 //               withDockerRegistry([credentialsId: "dockerlogin", url: ""]) {
 //                 script{
 //                 app =  docker.build("p_devsecops_ecr")
 //                 }
 //               }
 //            }
 //    }

	// stage('Push') {
 //            steps {
 //                script{
 //                    docker.withRegistry('https://239312700453.dkr.ecr.us-west-2.amazonaws.com', 'ecr:us-west-2:aws-credentials') {
 //                    app.push("latest")
 //                    }
 //                }
 //            }
 //    	}
	    
  }
}
