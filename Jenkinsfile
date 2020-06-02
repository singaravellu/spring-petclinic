node {
            properties([parameters([choice(choices: ['master', 'wavefront'], description: 'please select', name: 'branch')])])
    // parameters{ 
    //     string(name:'Branch',defaultValue:'master',description:'please select the branch you want') 
    // }
    stage('checkout'){
                 echo "${params.branch}"
               checkout([$class: 'GitSCM', branches: [[name: "${params.branch}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/singaravellu/spring-petclinic.git']]]) 

               echo "${params.branch}"
        }
}