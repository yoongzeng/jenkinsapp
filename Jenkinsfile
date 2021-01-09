pipeline
{
    agent none
    stages
    {
        stage('Non-parallel stage ')
        {
            agent {label "master"}
            steps { git 'https://github.com/yoongzeng/jenkinsapp.git'}
        }
        stage('Build')
        {
            agent {label "master"}
            steps {bat 'Building.bat' }
        }
        stage('Run in parallel')
        {
            parallel
            {
                stage('Test1 on master')
                {
                    agent {label "master"}
                    steps {bat'Testing.bat' }
                }
                stage('Test2 on slave machine')
                {
                    agent {label "master"}
                    steps {echo "tested on slave machine" }
                }
            }
        }
        stage('Deploy')
        {
            agent {label "master"}
            steps {bat 'Deployment.bat' }
        }
    }
    
    post
    {
        always{ echo "this will always run"}
        success{ echo "this will run if all steps run successfully"}
        failure{echo "this will run only when one step fail"}
        unstable{echo "this will run only if the run marked as unstable"}
        changed{echo "this will run only if the state of the pipeline changed , example the pipeline was previously failure and now is success"}
    }
}
