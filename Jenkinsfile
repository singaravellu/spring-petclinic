#!/usr/bin/env groovy
/* groovylint-disable DuplicateStringLiteral */
/* groovylint-disable-next-line CompileStatic */
env.GIT_COMMIT
echo "${env.GIT_COMMIT}"
/* groovylint-disable-next-line NoDef, UnusedVariable, VariableTypeRequired */
def approvalList = ['venkatesh', 'vijay']
// def recepients = 'venkateshsingaravelu95335@gmail.com'
// def subject = ''
// def body = ''
node {
    // def branches=[]
    properties([parameters([
                choice(choices: ['master', 'wavefront'], description: 'please select branch', name: 'branch'),
                                /* groovylint-disable-next-line LineLength */
                                choice(choices: ['dev', 'qat', 'testing'], description: 'please select environments', name: 'environments'),
                                /* groovylint-disable-next-line LineLength, SpaceAroundMapEntryColon */
                                gitParameter(name:'branches', type:'Branch', description: 'listing ', branchFilter: 'origin/(.*)')
                ])])
    // parameters{
    //     string(name:'Branch',defaultValue:'master',description:'please select the branch you want')
    // }
    //  echo "${env.GIT_COMMIT} and 'env.GIT_COMMIT' {env.GIT_COMMIT} "
    //  GIT_COMMIT
    stage('checkout') {
        echo "${params.branch}"
        /* groovylint-disable-next-line DuplicateStringLiteral, SpaceAfterClosingBrace */
        if (params.branch == 'master' || params.environments == 'dev') {
            /* groovylint-disable-next-line LineLength, SpaceAroundMapEntryColon */
         input message: "are you sure you want to build ${params.branch} in ${params.environments}", ok: 'yes', submitter: 'approvalList[]' , submitterParameter: 'approver'
            cleanWs()
            /* groovylint-disable-next-line LineLength */
            checkout([$class: 'GitSCM', branches: [[name: "${params.branch}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/singaravellu/spring-petclinic.git']]])
        }else {
            echo 'please select master branch'
        }
        // echo "${params.branch}"
        shortCommit = sh(returnStdout: true, script: "git log -n 1 --pretty=format:'%h'").trim()
        echo "${shortCommit}"
        echo "RESULT: ${currentBuild.currentResult}"
    //   for (element in branches){
    //        echo "${element} "
    //    }
    //    echo "${env.GIT_COMMIT}"
    //    echo "${env.BRANCH_NAME}"
    /* groovylint-disable-next-line LineLength */
    //     checkout([$class: 'GitSCM', branches: [[name: 'commitId' ]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/singaravellu/spring-petclinic.git']]])
    }

    /* groovylint-disable-next-line SpaceAfterClosingBrace */
    if (currentBuild.currentResult == 'SUCCESS') {
       //sendEmail()
        echo 'Sending a failure email'
        subject = "build failed #${BUILD_NUMBER}"
        body = "The build Failed while \"${message}\"...\n\nPlease goto ${env.BUILD_URL} for more information..."
        /* groovylint-disable-next-line SpaceAroundMapEntryColon */
        mail to: recepients, subject: subject, body: body
        echo "Job '${JOB_NAME}' (${BUILD_NUMBER}) is waiting for input"
        }else {
        echo "RESULT: ${currentBuild.currentResult}"
        //echo "Job '${JOB_NAME}' (${BUILD_NUMBER}) is waiting for input"
        echo  "Please go to ${BUILD_URL} and  verify the build"
    }

}
/* groovylint-disable-next-line NoDef */
def sendEmail() {
    /* groovylint-disable-next-line SpaceAfterClosingBrace */
    if (currentBuild.result == 'FAILURE' ) {
        echo 'Sending a failure email'
        subject = "build failed #${BUILD_NUMBER}"
        body = "The build Failed while \"${message}\"...\n\nPlease goto ${env.BUILD_URL} for more information..."
        /* groovylint-disable-next-line SpaceAroundMapEntryColon */
        mail to: recepients, subject: subject, body: body
    }
    else (currentBuild.result == 'SUCCESS') {
        subject = "completed for Build #${BUILD_NUMBER}"
        /* groovylint-disable-next-line LineLength */
        body = "Abuild #${BUILD_NUMBER} completed on branch ${BUILD_STREAM}.\n\nPlease goto ${env.BUILD_URL} for more information..."
        /* groovylint-disable-next-line SpaceAroundMapEntryColon */
        mail to: recepients, subject: subject, body: body
    }
}
