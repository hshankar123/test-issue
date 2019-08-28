pipeline {
  agent {
    label 'master'
  }
  environment {
    GOPATH = "$WORKSPACE"
    GITHUB_COMMIT="$GIT_COMMIT"
    GITHUB_PR="$GIT_CHANGE_ID"
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
      echo env.GITHUB_COMMIT
      sh'''
      BUILD_CAUSE_JSON=$(curl --silent ${BUILD_URL}/api/json | tr "{}" "\n" | grep "Started by")
      BUILD_USER_ID=$(echo $BUILD_CAUSE_JSON | tr "," "\n" | grep "userId" | awk -F\" '{print $4}')
      BUILD_USER_NAME=$(echo $BUILD_CAUSE_JSON | tr "," "\n" | grep "userName" | awk -F\" '{print $4}')
      echo ${BUILD_USER_NAME}
      '''
          
    }
  }
    
    stage("Build CVE job"){
      steps{
    
      build job: 'run_ngp_cve_scan_image', parameters: [[$class: 'StringParameterValue', name: 'COMMIT_ID', value:env.GITHUB_COMMIT], [$class: 'StringParameterValue', name: 'GITHUB_REPO', value:env.GIT_REPO],[$class: 'StringParameterValue', name: 'GITHUB_PR', value:env.GITHUB_PR]]
      }
  }
} 
}
