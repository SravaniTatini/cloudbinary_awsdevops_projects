pipeline {
    agent any 
    
    triggers {
        githubPush()
    }
    
    stages {
        stage('Stage-0 : Clone') { 
            steps {
                echo 'This stage clones SC from GITHUB'
                git branch: 'main', url: 'https://github.com/SravaniTatini/cloudbinary_awsdevops_projects.git'
            }
        }
         stage('Stage-1 : Clean') { 
            steps {
                echo 'This stage cleans the project by removeing old builds.'
                sh 'mvn clean'
            }
        }
        
         stage('Stage-2 : Validate') { 
            steps {
                echo 'This stage Checks if the project is correct.'
                sh 'mvn validate'
            }
        }
        
         stage('Stage-3 : Compile') { 
            steps {
                echo 'This stage Compiles source code into .class files.'
                sh 'mvn compile'
            }
        }

          stage('Stage-4 : Install') { 
            steps {
                echo 'This stage .'
                sh 'mvn install'
            }
        }

        stage('Stage-5 : Package') { 
            steps {
                echo 'This stage Packages compiled code into a .war.'
                sh 'mvn package'
            }
        }
          stage('Stage-6 : Verify') { 
            steps {
                echo 'This stage Runs additional checks to ensure quality.'
                sh 'mvn verify'
            }
        }
        
          stage('Stage-7 : Deploy') { 
            steps {
                echo 'This stage Deploys artifact to Nexus.'
                sh 'mvn deploy'
            }
        }
          
          stage('Stage-7 : Deployment') { 
            steps {
                echo 'This stage Deploys an Artifact .war file to Tomcat Server.'
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'vahin', path: '', url: 'http://54.83.111.46:8080/')], contextPath: 'MY-WEBAPP', war: '**/*.war'
            }
        } 
  
          
    }
}
