node {
    stage('Build') {
        echo 'checkout code...'
        checkout scm
    }
    stage('Test') {
        sh 'node --version'
    }
    stage('Deploy') {
        echo 'Deploying....'
        sh 'npm install'
        sh 'npm start'
    }
     stage('Archive') {
		steps {
			sh "cd dist && zip -r ../${DIST_ARCHIVE}.zip . && cd .."
			archiveArtifacts artifacts: "${DIST_ARCHIVE}.zip", fingerprint: true
		}
	}
	stage('Deploy') {
		steps {
			sh "aws s3 cp ${DIST_ARCHIVE}.zip s3://sampleapp-teja/${DIST_ARCHIVE}.zip --profile=default"
    }
}
