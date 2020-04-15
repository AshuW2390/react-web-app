pipeline
{
  agent any
  
  tools
  {
    nodejs 'node'
  }
  
  stages
  {
    stage('Build')
    {
      steps
      {
       cleanWs()
          checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '${RepoBranch}']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github_credentials', url: 'https://github.com/AshuW2390/react-web-app.git']]]
       sh '''
       ls -ltr
       npm install
       npm run build
       ls -ltr
       cd build/
       ls -ltr
       tar -cvf frontend-${BUILD_NUMBER}.tar *
       cp frontend-${BUILD_NUMBER}.tar ${WORKSPACE}/
       ls -ltr
       ''' 
      }
    }
    
  stage('Deploy')
  {
    steps
    {
      sh '''
      rm -rf deploy
      mkdir deploy
      cp -r frontend-${BUILD_NUMBER}.tar deploy/
      cd deploy
      tar -xvf frontend-${BUILD_NUMBER}.tar
      ls -ltr
      gsutil acl ch -u AllUsers:R gs://ashwini-walunj
      gsutil defacl set public-read gs://ashwini-walunj
      gsutil web set -m index.html -e index.html gs://ashwini-walunj
      gsutil cp -r * gs://ashwini-walunj
      gsutil setmeta -h "content-type: image/svg+xml" gs://ashwini-walunj/static/media/*.svg
      '''
    }
  }
 }
}
