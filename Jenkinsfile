
pipeline{
	agent any
	stages{
		stage('Pull Latest Image'){
			steps{
				bat "docker pull avadooty/selenium-docker"
			}
		}
		stage('Start Grid'){
			steps{
				bat "docker-compose up -d hub chrome firefox"
			}
		}
		stage('Run Test'){
			steps{
				bat "docker-compose up search-module book-flight-module"
			}
		}
	}
	post{
		always{
			archiveArtifacts artifacts:'output/**'

			publishHTML target: [
            allowMissing: false,
            alwaysLinkToLastBuild: false,
            keepAll: true,
            reportDir: 'coverage',
            reportFiles: 'index.html',
            reportName: 'RCov Report'
            ]

			bat "docker-compose down"
		}
	}
}