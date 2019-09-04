pipeline {
  agent {
    label 'master'
  }
  stages {
    stage("First") {
      steps {
       script{
        def url="$GIT_URL"
        final git_repo = url.substring(url.lastIndexOf('/') + 1, url.length()-4)
        env.GIT_REPO =git_repo
        }
      } 
    }
    stage("Build cve job"){
        when { triggeredBy 'SCMTrigger' } 
       steps{
      wrap([$class: 'BuildUser']) {   
      build job: 'dummy-freestyle', parameters: [[$class: 'StringParameterValue', name: 'COMMIT_ID', value:env.GIT_COMMIT],[$class: 'StringParameterValue', name: 'GITHUB_PR', value:env.CHANGE_ID], [$class: 'StringParameterValue', name: 'GITHUB_REPO', value:env.GIT_REPO],[$class: 'StringParameterValue', name: 'BUILD_ID', value:env.BUILD_ID],[$class: 'StringParameterValue', name: 'BUILD_URL', value:env.BUILD_URL],[$class: 'StringParameterValue', name: 'BUILD_USER', value:env.BUILD_USER],[$class: 'StringParameterValue', name: 'BUILD_USER_ID', value:env.BUILD_USER_ID],[$class: 'StringParameterValue', name: 'BUILD_USER_EMAIL', value:env.BUILD_USER_EMAIL],[$class: 'StringParameterValue', name: 'JOB_NAME', value:env.JOB_NAME],[$class: 'StringParameterValue', name: 'PRIMARY_JOB_OWNER_ID', value:"${ownership.job.primaryOwnerId}"],[$class: 'StringParameterValue', name: 'PRIMARY_JOB_OWNER_EMAIL', value:"${ownership.job.primaryOwnerEmail}" ],[$class: 'StringParameterValue', name: 'SECONDARY_JOB_OWNER_EMAIL', value:"${ownership.job.secondaryOwnerEmails}"],[$class: 'StringParameterValue', name: 'SECONDARY_JOB_OWNER_ID', value:"${ownership.job.secondaryOwnerIds}"]]
      }
      
   }  
  }
  }
/*post{
      success{
       /*script{
      if(env.CHANGE_ID ==null)
        {
          env.CHANGE_ID=""
        }
       }*/
      /* when { triggeredBy 'SCMTrigger' } 
       steps{
      wrap([$class: 'BuildUser']) {   
      build job: 'dummy-freestyle', parameters: [[$class: 'StringParameterValue', name: 'COMMIT_ID', value:env.GIT_COMMIT],[$class: 'StringParameterValue', name: 'GITHUB_PR', value:env.CHANGE_ID], [$class: 'StringParameterValue', name: 'GITHUB_REPO', value:env.GIT_REPO],[$class: 'StringParameterValue', name: 'BUILD_ID', value:env.BUILD_ID],[$class: 'StringParameterValue', name: 'BUILD_URL', value:env.BUILD_URL],[$class: 'StringParameterValue', name: 'BUILD_USER', value:env.BUILD_USER],[$class: 'StringParameterValue', name: 'BUILD_USER_ID', value:env.BUILD_USER_ID],[$class: 'StringParameterValue', name: 'BUILD_USER_EMAIL', value:env.BUILD_USER_EMAIL],[$class: 'StringParameterValue', name: 'JOB_NAME', value:env.JOB_NAME],[$class: 'StringParameterValue', name: 'PRIMARY_JOB_OWNER_ID', value:"${ownership.job.primaryOwnerId}"],[$class: 'StringParameterValue', name: 'PRIMARY_JOB_OWNER_EMAIL', value:"${ownership.job.primaryOwnerEmail}" ],[$class: 'StringParameterValue', name: 'SECONDARY_JOB_OWNER_EMAIL', value:"${ownership.job.secondaryOwnerEmails}"],[$class: 'StringParameterValue', name: 'SECONDARY_JOB_OWNER_ID', value:"${ownership.job.secondaryOwnerIds}"]]
      }
      
   }  
} 
} */

}
