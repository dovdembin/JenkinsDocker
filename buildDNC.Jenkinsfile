def dockerImage;

node('dockers'){
	stage('SCM'){
		checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/dovdembin/JenkinsDocker']]]);
	}
	stage('build'){
		dockerImage = docker.build('chrisbbehrens/agent-dnc:v$BUILD_NUMBER', './dotnetcore');
	}
	stage('push'){
		docker.withRegistry('https://index.docker.io/v1/', 'dockerhubcreds'){
			dockerImage.push();
		}
	}
}