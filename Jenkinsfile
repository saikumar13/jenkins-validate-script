pipeline {
    agent any

    stages {
        stage('Trigger Jobs') {
            steps {
                script {
                    // Define the list of jobs to trigger
                    def jobs = ['demo', 'demo']

                    // Trigger each job and store the build numbers in a map
                    def buildNumbers = [:]
                    jobs.each { job ->
                        def build = build job: job, wait: true
                        println "Hello =================> ${build}"
                        buildNumbers[job] = build.getNumber()
                    }

                    // Write the build results to a file
                    def outputFile = new File('build_results.txt')
                    jobs.each { job ->
                        def build = buildNumbers[job]
                        def result = currentBuild.rawBuild.getExecution().getRuns()[build].getResult()
                        def outputLine = "${job}: Build #${build} - ${result}"
                        outputFile.append(outputLine + '\n')
                        echo outputLine
                    }
                }
            }
        }
    }
}
