#!/usr/bin/groovy

properties([
    parameters([
        choice (name:'branches',choices:['master','something'],description:'select your branch')
    ])
])

node {
    stage('checkout')
    {
               git branch:"${params.branches}" ,url:'https://github.com/singaravellu/spring-petclinic.git'

               echo "$params.branches"
        }
   
}