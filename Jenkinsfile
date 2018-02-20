#!/usr/bin/env groovy

pipeline {
    agent any

    tools {
        maven 'M3'
    }

    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }

        stage ('Build') {
            steps {
                sh 'mvn -Dmaven.test.failure.ignore clean package' 
            }
            post {
                success {
                    junit 'target/surefire-reports/**/*.xml' 
                }
            }
        }
    }
    catch (exc) {
		echo "Caught: ${exc}"

		String recipient = 'infra@lists.jenkins-ci.org'

		mail subject: "${env.JOB_NAME} (${env.BUILD_NUMBER}) failed",
				body: "It appears that ${env.BUILD_URL} is failing, somebody should do something about that",
				to: recipient,
				replyTo: recipient,
				from: 'noreply@ci.jenkins.io'

		/* Rethrow to fail the Pipeline properly */
		throw exc
	}
}
