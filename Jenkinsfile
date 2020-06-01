#!/usr/bin/groovy


    

node {
    parameters{
        choice ( name: 'CHOICE' , choices: [ 'master' , 'something' ], description:'select your branch')
    }

    stage('checkout')
    {
               git branch:"${params.BRANCH}" ,url:'https://github.com/singaravellu/spring-petclinic.git'

               echo "$params.branches"
        }
   
}