
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
		stage('Publishing TestNG Result'){
		    steps([$class: 'Publisher', reportFilenamePattern: '**/custom/testng-results.xml'])
		}
	}
	post{
		always{
			archiveArtifacts artifacts:'output/**'

			publishHTML target: [
            allowMissing: false,
            alwaysLinkToLastBuild: false,
            keepAll: true,
            reportDir: 'output/',
            reportFiles: 'index.html',
            reportName: 'RCov Report'
            ]

			bat "docker-compose down"
		}
	}
}