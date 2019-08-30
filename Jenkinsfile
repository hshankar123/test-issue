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
      def build_id = "$BUILD_ID"
      def build_url = "$BUILD_URL"
      def job_name = "$JOB_NAME"
      echo env.GIT_REPO
      def pr_no=env.GITHUB_PR
      def commit_id = env.GITHUB_COMMIT
      wrap([$class: 'BuildUser']) {
      def build_user ="${BUILD_USER}"
      def build_user_id= "${BUILD_USER_ID}"
      def build_user_email="${BUILD_USER_EMAIL}"
      echo "${BUILD_USER_ID}"
      echo "${BUILD_USER_EMAIL}" 
       }
      println "Primary owner ID: ${ownership.job.primaryOwnerId}"
      def primary_owner_id = "${ownership.job.primaryOwnerId}"
      println "Primary owner e-mail: ${ownership.job.primaryOwnerEmail}"
      def primary_owner_email = "${ownership.job.primaryOwnerEmail}" 
      println "Secondary owner IDs: ${ownership.job.secondaryOwnerIds}"
      def secondary_owner_id = "${ownership.job.secondaryOwnerIds}"
      println "Secondary owner e-mails: ${ownership.job.secondaryOwnerEmails}"
      def secondary_owner_email="${ownership.job.secondaryOwnerEmails}"

      
      }
    
          
    }
  }
    
    stage("Build CVE job"){
      steps{
    
      build job: 'dummy-freestyle', parameters: [[$class: 'StringParameterValue', name: 'COMMIT_ID', value:env.GITHUB_COMMIT], [$class: 'StringParameterValue', name: 'GITHUB_REPO', value:"${git_repo}"],[$class: 'StringParameterValue', name: 'GITHUB_PR', value:"${pr_no}"]]
      }
  }
} 
}
