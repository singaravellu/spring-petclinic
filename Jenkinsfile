#!/usr/bin/env groovy
env.GIT_COMMIT
echo "${env.GIT_COMMIT}"
def approvalList=['venkatesh','vijay']
def recepients = 'venkateshsingaravelu95335@gmail.com'
def subject = ''
def body = ''
node {
    // def branches=[]
      properties([parameters([
                choice(choices: ['master', 'wavefront'], description: 'please select branch', name: 'branch'),
                choice(choices: ['dev', 'qat','testing'], description: 'please select environments', name: 'environments'),
                gitParameter(name:'branches',type:'Branch',description: 'listing ',branchFilter: 'origin/(.*)')
                ])])
    // parameters{
    //     string(name:'Branch',defaultValue:'master',description:'please select the branch you want')
    // }
    //  echo "${env.GIT_COMMIT} and 'env.GIT_COMMIT' {env.GIT_COMMIT} "
    //  GIT_COMMIT
    stage('checkout'){
                echo "${params.branch}"
                 if (params.branch == 'master' || params.environments =='dev'){
                    input message: "are you sure you want to build ${params.branch} in ${params.environments}", ok: 'yes ', submitter: 'approvalList[]' , submitterParameter: 'approver'
                     cleanWs()
                    checkout([$class: 'GitSCM', branches: [[name: "${params.branch}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/singaravellu/spring-petclinic.git']]])
                 }
                 else{
                     echo 'please select master branch'
                 }
              // echo "${params.branch}"
              shortCommit = sh(returnStdout: true, script: "git log -n 1 --pretty=format:'%h'").trim()
              echo "${shortCommit}"
            //   for (element in branches){
            //        echo "${element} "
            //    }
        //    echo "${env.GIT_COMMIT}"
        //    echo "${env.BRANCH_NAME}"
        //     checkout([$class: 'GitSCM', branches: [[name: 'commitId' ]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/singaravellu/spring-petclinic.git']]])
            
        }
        if(currentBuild.result=='SUCCESS'){
            sendemail()
                     echo "Job '${JOB_NAME}' (${BUILD_NUMBER}) is waiting for input"
                 }
                 else{
                     //echo "Job '${JOB_NAME}' (${BUILD_NUMBER}) is waiting for input"
                     echo  "Please go to ${BUILD_URL} and  verify the build"
                 }
}
            def sendemail(){
             if(currentBuild.result=='FAILURE' ){
        echo 'Sending a failure email'
        subject = "build failed #${BUILD_NUMBER}"
        body = "The build Failed while \"${message}\"...\n\nPlease goto ${env.BUILD_URL} for more information..."
        /* groovylint-disable-next-line SpaceAroundMapEntryColon */
        mail to: recepients, subject: subject, body: body
    }else if(currentBuild.result=='SUCCESS'){    
        subject = "completed for Build #${BUILD_NUMBER}"
        /* groovylint-disable-next-line LineLength */
        body = "Abuild #${BUILD_NUMBER} completed on branch ${BUILD_STREAM}.\n\nPlease goto ${env.BUILD_URL} for more information..."
        /* groovylint-disable-next-line SpaceAroundMapEntryColon */
        mail to: recepients, subject: subject, body: body
    }
}