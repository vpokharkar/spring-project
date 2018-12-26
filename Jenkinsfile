node {    
    checkout scm    
    stage('Application_Compile') {                
        bat 'mvn clean compile'
    }
    stage('Application_Unit_Test') {        
        bat 'mvn compiler:testCompile surefire:test'
        step([$class: 'Publisher'])
    }
    stage('Application_Code_Analysis') {
        withSonarQubeEnv {
            bat 'mvn sonar:sonar'
        }
    }
    stage('Application_Packaging') {        
        bat 'mvn war:war'
    }
    stage('Application_Deploy') {
       build job: 'Application_Deploy', propagate: false 
    }
}
