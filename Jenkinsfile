#!/usr/bin/groovy


    parameters{
        choice ( name: 'BRANCH' , choices: ['master','something'], description:'select your branch')
    }


node {
    stage('checkout')
    {
               git branch:"${params.BRANCH}" ,url:'https://github.com/singaravellu/spring-petclinic.git'

               echo "$params.branches"
        }
   
}