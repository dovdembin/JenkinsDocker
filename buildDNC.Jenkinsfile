def dockerImage;

node('docker'){
	stage('SCM'){
		checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/dovdembin/JenkinsDocker']]]);
	}
	stage('build'){
		dockerImage = docker.build('dovdembin/agent-dnc:v2', './dotnetcore');
	}
	stage('push'){
		docker.withRegistry('', 'dockerhubcreds'){
			dockerImage.push();
		}
	}
}