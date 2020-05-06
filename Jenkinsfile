node {
    stage('clone repo') {
        checkout scm
        url: 'https://github.com/thatPranav/angular-ci'
    }
    
    stage('npm install') {
        sh 'npm install'
    }

    stage('get code coverage') {
        script {
            COVERAGE_SUMM = sh(
                returnStdout: true, 
                script: 'ng test --code-coverage'
            ).trim()
        }
    }

    stage('check code coverage') {
        def result = (COVERAGE_SUMM =~ /[0-9.]+%/).findAll()
        echo result[1]
    }
    

}




// def notify(status){
//     emailext (
//       to: "jawajipranav@gmail.com",
//       subject: "${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
//       body: """<p>${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
//         <p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
//     )
// }

// node {
//     notify("Deploy to staging?")
// }

// input "Deploy to staging?"

// stage name: 'Deploy to staging', concurrency: 1
// node {
//     sh "echo '<h1>${env.BUILD_DISPLAY_NAME}</h1>' >> app/index.html"
    
//     sh 'docker-compose up -d --build'
    
//     notify('Solitaire Deployed!')
// }
