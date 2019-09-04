pipeline {
  agent {
    label 'master'
  }
  
  environment {
   
    
    GITHUB_PR="$CHANGE_ID"
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
    stage("printing other variables"){
    steps{
      script{ 
       //env.BUILD_ID="$BUILD_ID"
       //env.BUILD_URL="$BUILD_URL"
       wrap([$class: 'BuildUser']) {
       env.BUILD_USER="${BUILD_USER}"
       env.BUILD_USER_ID= "${BUILD_USER_ID}"
       env.BUILD_USER_EMAIL="${BUILD_USER_EMAIL}"
       echo "${BUILD_USER_ID}"
       echo "${BUILD_USER_EMAIL}" 
       
       env.JOB_NAME="$JOB_NAME"
       env.PRIMARY_JOB_OWNER_ID="${ownership.job.primaryOwnerId}"
       env.PRIMARY_JOB_OWNER_EMAIL="${ownership.job.primaryOwnerEmail}" 
       env.SECONDARY_JOB_OWNER_EMAIL="${ownership.job.secondaryOwnerIds}"
       env.SECONDARY_JOB_OWNER_ID="${ownership.job.secondaryOwnerEmails}"
       //echo env.GOPATH
      //echo env.GIT_REPO
      //println "Primary owner ID: ${ownership.job.primaryOwnerId}"
      //println "Primary owner e-mail: ${ownership.job.primaryOwnerEmail}"
      //println "Secondary owner IDs: ${ownership.job.secondaryOwnerIds}"
      //println "Secondary owner e-mails: ${ownership.job.secondaryOwnerEmails}"
       }
      }  
    }
  }
    
    stage("Build CVE job"){
      steps{
        when{
          not{
            changeRequest()
          }
        }
      wrap([$class: 'BuildUser']) {   
      build job: 'dummy-freestyle', parameters: [[$class: 'StringParameterValue', name: 'COMMIT_ID', value:env.GIT_COMMIT], [$class: 'StringParameterValue', name: 'GITHUB_REPO', value:env.GIT_REPO],[$class: 'StringParameterValue', name: 'repo', value:env.image_repo],[$class: 'StringParameterValue', name: 'tag', value:env.image_tag],[$class: 'StringParameterValue', name: 'BUILD_ID', value:env.BUILD_ID],[$class: 'StringParameterValue', name: 'BUILD_URL', value:env.BUILD_URL],[$class: 'StringParameterValue', name: 'BUILD_USER', value:env.BUILD_USER],[$class: 'StringParameterValue', name: 'BUILD_USER_ID', value:env.BUILD_USER_ID],[$class: 'StringParameterValue', name: 'BUILD_USER_EMAIL', value:env.BUILD_USER_EMAIL],[$class: 'StringParameterValue', name: 'JOB_NAME', value:env.JOB_NAME],[$class: 'StringParameterValue', name: 'PRIMARY_JOB_OWNER_ID', value:"${ownership.job.primaryOwnerId}"],[$class: 'StringParameterValue', name: 'PRIMARY_JOB_OWNER_EMAIL', value:"${ownership.job.primaryOwnerEmail}" ],[$class: 'StringParameterValue', name: 'SECONDARY_JOB_OWNER_EMAIL', value:"${ownership.job.secondaryOwnerEmails}"],[$class: 'StringParameterValue', name: 'SECONDARY_JOB_OWNER_ID', value:"${ownership.job.secondaryOwnerIds}"]]
      }
   }  
} 
} 
}
