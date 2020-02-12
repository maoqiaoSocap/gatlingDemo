timestamps {

node () {

    stage ('Performance-Testing - Checkout') {
     checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git-login', url: 'https://github.com/maoqiaoSocap/gatlingDemo.git']]]) 
    }
    stage ('Performance-Testing - Build Maven') {
            // Maven build step
    withMaven(maven: 'maven') { 
            if(isUnix()) {
                sh "mvn -B clean package" 
            } else { 
                bat "mvn -B clean package" 
            } 
        } 
    }
    stage ('Performance-Testing - Run Gatling') {
    withMaven(maven: 'maven') { 
            if(isUnix()) {
                sh "mvn gatling:test" 
            } else { 
                bat "mvn gatling:test" 
            } 
        } 
    gatlingArchive()
    }
  }
}
