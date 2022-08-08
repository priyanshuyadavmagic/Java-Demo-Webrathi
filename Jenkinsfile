pipeline {
  agent any
  tools {
    maven "Maven"
    jdk "JDK"
  }
  environment {
    JAVA_HOME = '/usr/lib/jvm/java-1.8.0-openjdk-amd64'      
  }
  stages {
    stage('Initialize'){
      steps{
        echo "${JAVA_HOME} "
        echo "PATH = ${M2_HOME}/bin:${PATH}"
        echo "M2_HOME = /opt/maven"
      }
    }
    stage('build') {
      steps {
        echo "Build"
       // sh 'pwd' 
        dir("/var/lib/jenkins/workspace/java") {
       // sh 'mvn -B -DskipTests clean install'
        }
        sh ' zip -r /var/lib/jenkins/workspace/java/app.zip /var/lib/jenkins/workspace/java/demo-0.0.1-SNAPSHOT.jar /var/lib/jenkins/workspace/java/java.sh '
      }
    }
    stage('deploy') {
      steps {
//          sh 'echo "Uploading content with AWS creds"'
//          sh 'pwd'
//          sh 'ls'
//          sh 'cd target'
//          sh 'ls target'
        withAWS(region:'ap-south-1',credentials:'a1cefe13-c0e3-416f-bf3f-6a6cd652fdb6') {
          s3Upload(file:'/var/lib/jenkins/workspace/java/app.zip', bucket:'jenkinsdeploy1')
//           sh '
//           aws s3 cp ./target/demo-0.0.1-SNAPSHOT.jar s3://jenkinsdeploy1/demo-0.0.1-SNAPSHOT.jar '
        }
      }
    }
  }
}
