#!/usr/bin/env groovy

pipeline {
    agent any
	
	//Option One for Environments
	environment {
        ENV_NAME = 'PIL'
		ABP_HOST = '10.252.3.21'
		ABP_PORT = '80'
		ABP_WEB_SYSADMIN_USERNAME = 'sysadmin'
		ABP_WEB_SYSADMIN_PASSWORD = 'password'
    }
	
	//Option 2 fror environment insertion
	//load "$JENKINS_HOME/.envvars/stacktest-staging.groovy"


    //Example :
	//node {
	//	load "$JENKINS_HOME/.envvars/stacktest-staging.groovy"
	//	echo "${env.DB_URL}"
	//	echo "${env.DB_URL2}"
	//}
	
	
	
	// Triggers build everyday at 11 PM
	triggers { pollSCM('H 23 * * *') }
	

	
	// Check out the source code at this stage from the existing repository
	stage('Checkout source') {
		checkout scm
	}	
	
	
	// Clean workspace before doing anything
	stage('Clean workspace') {
		deleteDir()
	}
	
	// Job will about after build stuck for 60 minutes
	options {
        timeout(time: 1, unit: '1') 
    }
	
	// Enables timestamp to add on the console
	options { timestamps() }
