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
                        buildNumbers[job] = build.number
                    }

                    // Write the build results to a file
                    def outputFile = new File('build_results.txt')

                    jobs.each { job ->
                        def build = buildNumbers[job]
                        def result = build.getResult()
                        def outputLine = "${job}: Build #${build} - ${result}\n"
                        outputFile.append(outputLine)
                        echo outputLine
                    }
                }
            }
        }
    }
}
