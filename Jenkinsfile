pipeline {
 agent any
 parameters {
     password(name: 'PASSWD', defaultValue: '', description: 'Please Enter your Gitlab password')
     string(name: 'IMAGETAG', defaultValue: '1', description: 'Please Enter the Image Tag to Deploy?')
     choice(name:'environment', choices: ['dev', 'qa', 'prod' ] ,description: 'select where need to deploy')
 }
 stages {
  stage('Deploy')
  {
    steps { 
        git branch: 'springboot', credentialsId: 'GitlabCred', url: 'https://github.com/kirtan8/spingboot-cd-pipeline-main.git'
      dir ("./${params.environment}") {
              sh "sed -i 's/image: cary01.*/image: cary01\\/democicd:$IMAGETAG/g' deployment.yml" 
	    }
	    sh 'git commit -a -m "New deployment for Build $IMAGETAG"'
	    sh "git push https://kirtan8:$PASSWD@github.com/kirtan8/spingboot-cd-pipeline-main.git"
    }
  }
 }
}
