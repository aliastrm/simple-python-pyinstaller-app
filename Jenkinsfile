// node {
//     stage('Build') {
//         docker.image('python:2-alpine').inside {
//             sh 'python -m py_compile sources/add2vals.py sources/calc.py'
//             sh 'mkdir -p dist'
//             sh 'mv sources/add2vals.pyc dist/'
//         }
//     }
//     stage('Test') {
//         docker.image('qnib/pytest').inside {
//             sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
//         }
//     }
//     stage('Manual Approval') {
//         input message: 'Lanjutkan ke tahap deploy? '
//     }
//     stage('Deploy') {
//         docker.image('python:2-alpine').inside {
//             archiveArtifacts artifacts: 'dist/*', allowEmptyArchive: false
//             sh 'sleep 60'
//         }
//     }


    
// }

node {
    stage('Build') {
        docker.image('python:2-alpine').inside {
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'
            sh 'mkdir -p dist'
            sh 'mv sources/add2vals.pyc dist/'
        }
    }

    stage('Test') {
        docker.image('qnib/pytest').inside {
            sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
//            junit 'test-reports/results.xml'
        }
    }

    stage('Manual Approval') {
        input message: 'Lanjutkan ke tahap deploy? '
    }

    stage('Deploy') {
        docker.image('python:2-alpine').inside {
            archiveArtifacts artifacts: 'dist/*', allowEmptyArchive: false
            sh 'sleep 60'
        }
    }
}
