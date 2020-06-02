node {
    def branches=[];
      properties([parameters([
                choice(choices: ['master', 'wavefront'], description: 'please select', name: 'branch'),
                gitParameter(name:'branches',type:'Branch',description: 'listing all the branches in repos',branchFilter: 'origin/(.*)')
                ])])         
    // parameters{ 
    //     string(name:'Branch',defaultValue:'master',description:'please select the branch you want') 
    // }
    //  echo "${env.GIT_COMMIT} and 'env.GIT_COMMIT' {env.GIT_COMMIT} "
    //  GIT_COMMIT
    stage('checkout'){
                 echo "${params.branch}"
                 if(params.branch == 'master'){
               checkout([$class: 'GitSCM', branches: [[name: "${params.branch}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/singaravellu/spring-petclinic.git']]]) 
                 }
                 else{
                     echo "please select master branch"
                 }

              // echo "${params.branch}"
              
               for (element in branches) 
               {
                   echo "${element} " 
               }
           
            // checkout([$class: 'GitSCM', branches: [[name: 'commitId']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/singaravellu/spring-petclinic.git']]])
            //  echo "${env.GIT_COMMIT}"   
        }
}