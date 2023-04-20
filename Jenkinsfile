pipeline {

  agent any
  environment {
        PLATFORM_CRED = credentials('platform-cred')
		MAVEN_CRED = credentials('maven-settings')
      }
  stages {
  stage('mvn test settings') {
            steps {
                sh 'mvn -s $MAVEN_CRED help:effective-settings'
            }
        }
    stage('Build') {
      steps {
            bat 'mvn -B -U -e -V clean -DskipTests package'
      }
    }

    stage('Test') {
      steps {
          echo  'hello world Munit test case'
      }
    }

     stage('Deployment develop')      {
         
         environment {
        CLIENT_ID = credentials('dev-client-d')
        CLIENT_SECRET = credentials('dev-client-secret')
      }
         steps {
            bat 'mvn -U -V -e -B -DskipTests deploy -Pdev -DmuleDeploy -Duser=%PLATFORM_CRED_USR% -Dpswd=%PLATFORM_CRED_PSW% -Danypoint.platform.client_id=%CLIENT_ID% -Danypoint.platform.client_secret=%CLIENT_SECRET%'
      }
    }
	 stage('Deployment qa')      {
         
         environment {
        CLIENT_ID = credentials('qa-client-id')
        CLIENT_SECRET = credentials('qa-client-secret')
      }
         steps {
            bat 'mvn -U -V -e -B -DskipTests deploy -Pqa -DmuleDeploy -Duser=%PLATFORM_CRED_USR% -Dpswd=%PLATFORM_CRED_PSW% -Danypoint.platform.client_id=%CLIENT_ID% -Danypoint.platform.client_secret=%CLIENT_SECRET%'
      }
    }
    
  }
}