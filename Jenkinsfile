/*node {
     stage('Clone repository') {
         checkout scm
     }
     stage('Build image') {
         app = docker.build("onesenal/Innogrid_Project", "--network host -f Dockerfile .")
     }
         echo "image built succeffully" 
     }
stage('Configure') {
    abort = false
    inputConfig = input id: 'InputConfig', message: 'Docker registry and Anchore Engine configuration', \
	parameters: [string(defaultValue: 'https://192.168.160.244', description: 'URL of the Harbor registry for staging images before analysis', name: 'HarborRegistryUrl', trim: true), \
		     string(defaultValue: 'https://192.168.160.244', description: 'Hostname of the Harbor registry', name: 'HarborRegistryHostname', trim: true), \
		     string(defaultValue: 'test/test', description: 'Name of the docker repository', name: 'dockerRepository', trim: true), \
		     credentials(credentialType: 'com.cloudbees.plugins.credentials.impl.UsernamePasswordCredentialsImpl', defaultValue: 'harbor', description: 'Credentials for connecting to the docker registry', name: 'dockerCredentials', required: true), \
		     string(defaultValue: 'http://192.168.160.244:8228/v1', description: 'Anchore Engine API endpoint', name: 'anchoreEngineUrl', trim: true), \
		     credentials(credentialType: 'com.cloudbees.plugins.credentials.impl.UsernamePasswordCredentialsImpl', defaultValue: 'admin', description: 'Credentials for interacting with Anchore Engine', name: 'anchoreEngineCredentials', required: true)], \
		    
    for (config in inputConfig) {
        if (null == config.value || config.value.length() <= 0) {
          echo "${config.key} cannot be left blank"
          abort = true
        }
    }

    if (abort) {
        currentBuild.result = 'ABORTED'
        error('Aborting build due to invalid input')
    }
}*/

node {
  def app
  def dockerfile
  def anchorefile
  def repotag

  try {
    stage('Checkout') {
      // Clone the git repository
      checkout scm
      def path = sh returnStdout: true, script: "pwd"
      path = path.trim()
      dockerfile = path + "/Dockerfile"
      anchorefile = path + "/anchore_images"
    }

    stage('Build') {
      // Build the image and push it to a staging repository
      app = docker.build("test/test", "--network host -f Dockerfile .")
	    docker.withRegistry('https://192.168.160.244', 'harbor') {
/*      repotag = inputConfig['dockerRepository'] + ":${BUILD_NUMBER}"
      docker.withRegistry(inputConfig['HarborRegistryUrl'], inputConfig['dockerCredentials']) {
        app = docker.build(test/test)
        app.push() */
	app.push("$BUILD_NUMBER")
	app.push("latest")
      }
      sh script: "echo Build completed"
    }

    stage('Anchore Image Analyze') {
      parallel Test: {
        app.inside {
            sh 'echo "Dummy - tests passed"'
        }
      },
      Analyze: {
        writeFile file: anchorefile, \
	      /*text: inputConfig['HarborRegistryHostname']*/
	      text: "192.168.160.244" +  "/" + "test/test" + " " + dockerfile
        anchore name: anchorefile, \
	      engineurl: 'http://192.168.160.244:8228/v1', \
	      engineCredentialsId: 'admin', \
	      annotations: [[key: 'added-by', value: 'jenkins']], \
	      forceAnalyze: true
      }
    }
  } finally {
    stage('Cleanup') {
      // Delete the docker image and clean up any allotted resources
      sh script: "echo Clean up"
    }
  }
     stage('OWASP Dependency-Check Vulnerabilities ') {
        dependencyCheck additionalArguments: '''
		-s "." 
		-f "ALL"
		-o "./report/"
		--prettyPrint
		--disableYarnAudit''', odcInstallation: 'OWASP Dependency-check'
		dependencyCheckPublisher pattern: 'report/dependency-check-report.xml'
     }
     stage('SonarQube analysis') {
	    def scannerHome = tool 'sonarqube';
            withSonarQubeEnv('sonarserver'){
                    sh "${scannerHome}/bin/sonar-scanner \
		-Dsonar.projectKey=sonarqube \
		-Dsonar.host.url=http://192.168.160.244:9000 \
		-Dsonar.login=807e0f2bc82e3c377436e2b6292ed7bc73b04e24 \
		-Dsonar.sources=. \
		-Dsonar.report.export.path=sonar-report.json \
		-Dsonar.exclusions=report/* \
		-Dsonar.dependencyCheck.jsonReportPath=./report/dependency-check-report.json \
		-Dsonar.dependencyCheck.xmlReportPath=./report/dependency-check-report.xml \
		-Dsonar.dependencyCheck.htmlReportPath=./report/dependency-check-report.html"
         }
     }
        stage('SonarQube Quality Gate'){
    	 timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
          
          }
     }

     /* stage('Push image') {
         docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
             app.push("$BUILD_NUMBER")
	 app.push("latest")
         }
     } */ 
    stage('OWASP ZAP') {
        sh '''
            pip install archerysec-cli --force
	    rm -rf /tmp/archerysec-scans-report
	    mkdir /tmp/archerysec-scans-report
	    archerysec-cli -h http://192.168.160.244:8000\
	    -t TOHY-2gSbfRjq--f9hjDV-B55ymqMf5cw2u9smywDRePoF2ucpCNxmJg8_cU74of\
	    --cicd_id=3582b517-dca0-4b50-884c-6a27188fc6b4\
	    --project=f03337a6-3498-4512-b078-f9f072036244\
	    --zap-base-line-scan\
	    --report_path=/tmp/archerysec-scans-report'''
              }
}
