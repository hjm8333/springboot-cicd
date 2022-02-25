pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo '빌드 끗'
        sh './gradlew clean build'
      }
    }

    stage('upload') {
      steps {
        echo '업로드 끗'
        sh 'aws s3 cp build/libs/application.war s3://springboot-cicd-uhmjunsik/application.war --region us-west-1' 
      }
    }

    stage('deploy') {
      steps {
        echo '디플로이 끗'
        sh 'aws elasticbeanstalk create-application-version --region us-west-1 --application-name springboot-uhmjunsik --version-label ${BUILD_TAG} --source-bundle S3Bucket="springboot-cicd-uhmjunsik",S3Key="application.war"' 
        sh 'aws elasticbeanstalk update-environment --region us-west-1 --environment-name Springbootuhmjunsik-env --version-label ${BUILD_TAG}' 
      }
    }

  }
}