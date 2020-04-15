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
        script
        {
          checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '{$RepoBranch}']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github_credentials', url: 'https://github.com/AshuW2390/react-web-app.git']]]
        }        
      }
    }
  }
}
