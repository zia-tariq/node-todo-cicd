pipeline {
	agent {label 'dev-agent' }
    
	stages {
    	stage ('Code') {
        	steps {
            	git url: 'https://github.com/zia-tariq/node-todo-cicd.git', branch: 'master'
        	}
    	}
    	stage ('Build and Test') {
        	steps {
            	sh 'docker build . -t ziatariq2023/node-todo-app-cicd:latest'
        	}
    	}
    	stage ('Login and Push Image') {
        	steps {
            	echo 'Login into docker hub and push image'
            	withCredentials([usernamePassword(credentialsId:'Dockerhub',passwordVariable:'DockerhubPassword', usernameVariable: 'DockerhubUsername' )]) {
                	sh "docker login -u ${env.DockerhubUsername} -p ${env.Dockerhubpassword}"
                	sh "docker push ziatariq2023/node-todo-app-cicd:latest"
            	}
        	}
    	}
    	stage ('Deploy') {
        	steps {
            	sh 'docker-compose down && docker-compose up -d'
        	}
    	}
	}
}
