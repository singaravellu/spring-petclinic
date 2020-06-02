#!/usr/bin/env groovy
env.GIT_COMMIT
echo "${env.GIT_COMMIT}"
def approvalList=['venkatesh','vijay']
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
                 if (params.branch == 'master' && params.environments =='dev'){
                    input message: "are you sure you want to build ${params.branch} in ${params.environments}", ok: 'yes ', submitter: approvalList , submitterParameter: 'approver'
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
                     echo "Job '${JOB_NAME}' (${BUILD_NUMBER}) is waiting for input"
                 }
                 else{
                     echo "Job '${JOB_NAME}' (${BUILD_NUMBER}) is waiting for input"
                     echo  "Please go to ${BUILD_URL} and  verify the build"
                 }
}