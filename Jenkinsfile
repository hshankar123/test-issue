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
      
      echo "$BUILD_ID"
      echo "$BUILD_URL"
      echo "$JOB_NAME"
      echo env.GIT_REPO
      echo env.GITHUB_PR
      echo env.GITHUB_COMMIT
      println "Primary owner ID: ${ownership.job.primaryOwnerId}"
      println "Primary owner e-mail: ${ownership.job.primaryOwnerEmail}"
      println "Secondary owner IDs: ${ownership.job.secondaryOwnerIds}"
      println "Secondary owner e-mails: ${ownership.job.secondaryOwnerEmails}"
      wrap([$class: 'BuildUser']) {
      echo "${BUILD_USER}"
      echo "${BUILD_USER_ID}"
      echo "${BUILD_USER_EMAIL}"
      
    }
          
    }
  }
    
    stage("Build CVE job"){
      steps{
    
      build job: 'dummy-freestyle', parameters: [[$class: 'StringParameterValue', name: 'COMMIT_ID', value:env.GITHUB_COMMIT], [$class: 'StringParameterValue', name: 'GITHUB_REPO', value:env.GIT_REPO],[$class: 'StringParameterValue', name: 'GITHUB_PR', value:env.GITHUB_PR]]
      }
  }
} 
}
