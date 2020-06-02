node {
            properties([parameters([string(defaultValue: 'master', description: 'select branch you need', name: 'branch', trim: false)])])
    // parameters{ 
    //     string(name:'Branch',defaultValue:'master',description:'please select the branch you want') 
    // }
    stage('checkout'){
               checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/singaravellu/spring-petclinic.git']]]) 
        }