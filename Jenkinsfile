node {
    
            properties([parameters([
                choice(choices: ['master', 'wavefront'], description: 'please select', name: 'branch'),
                gitParameter(name:'branches',type:'Branch',description: 'listing all the branches in repos',branchFilter: 'origin/(.*)')
                ])])
    // parameters{ 
    //     string(name:'Branch',defaultValue:'master',description:'please select the branch you want') 
    // }
    stage('checkout'){
                 echo "${params.branch}"
                 if(params.branch == 'master'){
               checkout([$class: 'GitSCM', branches: [[name: "${params.branch}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/singaravellu/spring-petclinic.git']]]) 
                 }
                 else{
                     echo "please select master branch"
                 }

              // echo "${params.branch}"
              def list = [1,2,3,4];
               for (element in list) 
               {
                  echo "${element} and ${list.size}" 
               }
               
        }
}