
properties([
    parameters([
        gitParameter(branch: '',
                     branchFilter: 'origin/(.*)',
                     defaultValue: 'master',
                     description: 'please select which branch you want to build',
                     name: 'BRANCH',
                     quickFilterEnabled: false,
                     selectedValue: 'NONE',
                     sortMode: 'NONE',
                     tagFilter: '*',
                     type: 'PT_BRANCH')
    ])
])

node {
    stage('checkout')
    {
               git branch:"${params.BRANCH}" ,url:'https://github.com/singaravellu/spring-petclinic.git'

               echo "$params.BRANCH"
        }
   
}