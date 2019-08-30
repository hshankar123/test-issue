pipeline {
  agent {
    label 'master'
  }
  
  environment {
    GOPATH = "$WORKSPACE"
    GITHUB_COMMIT="$GIT_COMMIT"
    GITHUB_PR="$CHANGE_ID"
  }
  

  stages {
    stage("First") {
      steps {
       script{
        def url="$GIT_URL"
        final git_repo = url.substring(url.lastIndexOf('/') + 1, url.length())
        env.GIT_REPO =git_repo
       
        }
        
      }
       
    }
    stage("printing other variables"){
    steps{
      
      script{
        
       env.BUILD_ID="$BUILD_ID"
       env.BUILD_URL="$BUILD_URL"
       wrap([$class: 'BuildUser']) {
        env.BUILD_USER=="${BUILD_USER}"
        env.BUILD_USER_ID= "${BUILD_USER_ID}"
        env.BUILD_USER_EMAIL="${BUILD_USER_EMAIL}"
        echo "${BUILD_USER_ID}"
        echo "${BUILD_USER_EMAIL}" 
       }
       env.JOB_NAME="$JOB_NAME"
       env.PRIMARY_JOB_OWNER_ID="${ownership.job.primaryOwnerId}"
       env.PRIMARY_JOB_OWNER_EMAIL="${ownership.job.primaryOwnerEmail}" 
       env.SECONDARY_JOB_OWNER_EMAIL="${ownership.job.secondaryOwnerIds}"
       env.SECONDARY_JOB_OWNER_ID="${ownership.job.secondaryOwnerEmails}"
       


        
        
        
      
     
      echo env.GIT_REPO
      
     
     
      println "Primary owner ID: ${ownership.job.primaryOwnerId}"
     
      println "Primary owner e-mail: ${ownership.job.primaryOwnerEmail}"
      
      println "Secondary owner IDs: ${ownership.job.secondaryOwnerIds}"
      
      println "Secondary owner e-mails: ${ownership.job.secondaryOwnerEmails}"
      

      
      }
    
          
    }
  }
    
    stage("Build CVE job"){
      steps{
    
      build job: 'dummy-freestyle', parameters: [[$class: 'StringParameterValue', name: 'COMMIT_ID', value:env.GITHUB_COMMIT], [$class: 'StringParameterValue', name: 'GITHUB_REPO', value:"env.GITHUB_REPO"],[$class: 'StringParameterValue', name: 'GITHUB_PR', value:"env.GITHUB_PR"]]
      }
  }
} 
}
