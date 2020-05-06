stage 'CI'
node {
    
    checkout scm
    //git branch: 'jenkins2-course', 
        url: 'https://github.com/thatPranav/angular-ci'

    // pull dependencies from npm
    // on windows use: bat 'npm install'
    sh 'npm install'

    // stash code & dependencies to expedite subsequent testing
    // and ensure same code & dependencies are used throughout the pipeline
    // stash is a temporary archive
    // stash name: 'everything', 
    //     //   excludes: 'test-results/**', 
    //       includes: '**'
    
    // test with PhantomJS for "fast" "generic" results
    // on windows use: bat 'npm run test-single-run -- --browsers PhantomJS'
    // sh 'ng test'
    
    // archive karma test results (karma is configured to export junit xml files)
    // step([$class: 'JUnitResultArchiver', 
    //       testResults: 'coverage/angular-ci/src/index.html'])

    script {
        COVERAGE_SUMM = sh(
            returnStdout: true, 
            script: 'ng test --code-coverage'
        ).trim()
    }

    def result = (COVERAGE_SUMM =~ /[0-9.]+%/).findAll()

    echo result[0]

       
}

// node('linux') {
//     sh 'ls'
//     sh 'rm -rf *'
//     unstash 'everything'
//     sh 'ls'
// }

// //parallel
// stage 'Browser Testing'
// parallel chrome: {
//     runTests("Chrome")
// }, firefox: {
//     runTests("Firefox")
// }

// def runTests(browser) {
//     node {
//         sh 'rm -rf *'
//         unstash 'everything'
//         sh "npm run test-single-run -- --browsers ${browser}"
//         step([$class: 'JUnitResultArchiver', 
//               testResults: 'test-results/**/test-results.xml'])
//     }
// }

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
