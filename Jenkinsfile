pipeline {

  agent any
  environment {
        PLATFORM_CRED = credentials('platform-cred')
        
      }
  stages {
    stage('Build') {
      steps {
          \\assuming mvn-settings.xml is at root/current folder, otherwise provide absolute or relative path
          sh 'mvn -s settings.xml clean install'
      }
    }

    stage('Test') {
      steps {
          echo  'hello world Munit test case'
      }
    }

     stage('Deployment dev')      {
         
         environment {
        CLIENT_ID = credentials('dev-client-d')
        CLIENT_SECRET = credentials('dev-client-secret')
      }
         steps {
            bat 'mvn -U -V -e -B -DskipTests deploy -Pdev -DmuleDeploy -Dusername=%PLATFORM_CRED_USR% -Dpassword=%PLATFORM_CRED_PSW% -Danypoint.platform.client_id=%CLIENT_ID% -Danypoint.platform.client_secret=%CLIENT_SECRET%'
      }
    }
	 stage('Deployment qa')      {
         
         environment {
        CLIENT_ID = credentials('qa-client-id')
        CLIENT_SECRET = credentials('qa-client-secret')
      }
         steps {
            bat 'mvn -U -V -e -B -DskipTests deploy -Pqa -DmuleDeploy -Dusername=%PLATFORM_CRED_USR% -Dpassword=%PLATFORM_CRED_PSW% -Danypoint.platform.client_id=%CLIENT_ID% -Danypoint.platform.client_secret=%CLIENT_SECRET%'
      }
    }
    
  }
}