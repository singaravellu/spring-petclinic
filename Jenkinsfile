node {
    parameters{ 
        string(name:'Branch',defaultValue:'master',description:'please select the branch you want') 
    }
    stage('checkout'){
               git branch:${parameters.Branch} url:'https://github.com/singaravellu/spring-petclinic.git'       
        }
   
    }
}