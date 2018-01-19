#!groovy

node('Server_Group_1') {

    currentBuild.result = "SUCCESS"

    try {

            stage('Checkout'){

            env.NODE_ENV = "Checkout"

	    print "Environment will be : ${env.NODE_ENV}"

            sh "echo                                                   > Jenkin_Pipeline_Example_01.log"
            sh "echo [Stage: ${env.NODE_ENV}]                         >> Jenkin_Pipeline_Example_01.log" 
            sh "echo ------------------------                         >> Jenkin_Pipeline_Example_01.log"
	    sh "echo                                                  >> Jenkin_Pipeline_Example_01.log"
	    sh "echo 'Checking out the code from SCM...'              >> Jenkin_Pipeline_Example_01.log"
            sh "echo Hostname: hostname                               >> Jenkin_Pipeline_Example_01.log"
            sh "echo                                                  >> Jenkin_Pipeline_Example_01.log"
            sh "echo PATH: ${env.PATH}                                >> Jenkin_Pipeline_Example_01.log"

       }

       stage('Test'){

            env.NODE_ENV = "Test"

            print "Environment will be : ${env.NODE_ENV}"

	    sh "echo                                                  >> Jenkin_Pipeline_Example_01.log"
            sh "echo [Stage: ${env.NODE_ENV}]                         >> Jenkin_Pipeline_Example_01.log" 
            sh "echo ------------------------                         >> Jenkin_Pipeline_Example_01.log"
	    sh "echo                                                  >> Jenkin_Pipeline_Example_01.log"
            sh "echo ls ${WORKSPACE}/target                           >> Jenkin_Pipeline_Example_01.log"

       }

       stage('Build'){

            env.NODE_ENV = "Build"

            print "Environment will be : ${env.NODE_ENV}"

	    sh "echo                                                  >> Jenkin_Pipeline_Example_01.log"
            sh "echo [Stage: ${env.NODE_ENV}]                         >> Jenkin_Pipeline_Example_01.log" 
            sh "echo ------------------------                         >> Jenkin_Pipeline_Example_01.log"
	    sh "echo Building the code..                              >> Jenkin_Pipeline_Example_01.log"

            sh 'export MAVEN_HOME=/opt/maven'
            sh 'cd ${WORKSPACE}'
	    sh '${MAVEN_HOME}/bin/mvn clean install'
       }

       stage('Deploy'){

            env.NODE_ENV = "Deploy"

            print "Environment will be : ${env.NODE_ENV}"

	    sh "echo                                                  >> Jenkin_Pipeline_Example_01.log"
            sh "echo [Stage: ${env.NODE_ENV}]                         >> Jenkin_Pipeline_Example_01.log" 
            sh "echo ------------------------                         >> Jenkin_Pipeline_Example_01.log"
	    sh "echo                                                  >> Jenkin_Pipeline_Example_01.log"
	    sh "Copy the Jenkinsfile to Deployment server....         >> Jenkin_Pipeline_Example_01.log"

	    sh 'rsync ${env.WORKARERA}/Jenkinsfile root@15.213.52.106:/tmp'

       }

       stage('Cleanup'){

            env.NODE_ENV = "Deploy"

            print "Environment will be : ${env.NODE_ENV}"

	    sh "echo                                                  >> Jenkin_Pipeline_Example_01.log"
            sh "echo [Stage: ${env.NODE_ENV}]                         >> Jenkin_Pipeline_Example_01.log" 
            sh "echo ------------------------                         >> Jenkin_Pipeline_Example_01.log"
	    sh "echo                                                  >> Jenkin_Pipeline_Example_01.log"
	    sh "Cleaning up the files....                             >> Jenkin_Pipeline_Example_01.log"

	    mail    from: 'rsbisht@hpe.com',
                 replyTo: 'rsbisht@hpe.com',
                      to: 'rsbisht@hpe.com',
                 subject: 'Project Build Successful',
	            body: 'Project Build Successful' 
       }

    }
    catch (err) {

        currentBuild.result = "FAILURE"

            mail    from: 'rsbisht@hpe.com',
                 replyTo: 'rsbisht@hpe.com',
                      to: 'rsbisht@hpe.com',
                 subject: 'Project Build Failed !',
	            body: "Project Build Failed. You can find the error is here: ${env.BUILD_URL}" 

        throw err
    }

}
