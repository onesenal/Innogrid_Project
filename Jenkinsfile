node {
     stage('Clone repository') {
         checkout scm
     }
     /* stage('Build image') {
         app = docker.build("onesenal/Innogrid_Project", "--network host -f Dockerfile .")
     } */
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
            withSonarQubeEnv('sonarserver'){
                    sh "mvn sonar:sonar \
		-Dsonar.projectKey=sonarqube \
		-Dsonar.host.url=http://192.168.160.234:9000 \
		-Dsonar.login=1089bf1c1f3fd28c831ce744752e9f0a1124a5d6 \
		-Dsonar.sources=. \
        -Dsonar.exclusions=./dist/ **/*,./reports/*,./coverage/** /* \
        -Dsonar.dependencyCheck.severity.blocker=9.0 \
        -Dsonar.dependencyCheck.severity.critical=7.0 \
        -Dsonar.dependencyCheck.severity.major=4.0 \
        -Dsonar.dependencyCheck.severity.minor=0.0 \
		-Dsonar.dependencyCheck.jsonReportPath=reports/dependency-check-report.json \
        -Dsonar.dependencyCheck.htmlReportPath=reports/dependency-check-report.html \
         }
     }
        stage('SonarQube Quality Gate'){
    	 timeout(time: 1, unit: 'HOURS') {
              waitForQualityGate abortPipeline: true
              }
          
          }
     }

     /* stage('Push image') {
         docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
             app.push("$BUILD_NUMBER")
	 app.push("latest")
         }
     } */
