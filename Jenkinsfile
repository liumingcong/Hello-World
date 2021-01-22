pipeline{
    agent any
    parameters{
        gitParameter branch: '', 
                     branchFilter: '.*', 
                     defaultValue: 'master', 
                     description: 'git_tig', 
                     name: 'GIT_TAG', 
                     quickFilterEnabled: true, 
                     selectedValue: 'TOP', 
                     sortMode: 'DESCENDING_SMART', 
                     tagFilter: '*', 
                     type: 'PT_TAG'
		choice(name: 'HOST_IP', choices: ['10.67.78.61','10.67.78.60'], description: '')
        choice(name: 'ENV', choices: ['dev','test'], description: '')                        
    }
    stages{
        stage('git'){
            steps{
               checkout([$class: 'GitSCM', 
                          branches: [[name: "${params.GIT_TAG}"]], 
                          doGenerateSubmoduleConfigurations: false, 
                          extensions: [], 
                          gitTool: 'Default', 
                          submoduleCfg: [], 
                          userRemoteConfigs: [[credentialsId: '1c37c2e6-110d-402a-a270-dc75aa1173bf', url: 'git@10.67.78.66:gudongxiao/bailing-service-simulation.git']]
                        ])
            }
        }
        stage('build'){
            steps{
                sh 'sh /usr/local/bailing/deploy-service/informal/one_module_pre_build_framework.sh'  
                sh 'sh /usr/local/bailing/deploy-service/informal/one_module_pre_build.sh ${JOB_NAME}'
                sh 'sh /usr/local/bailing/deploy-service/informal/one_module_deploy.sh ${JOB_NAME} ${params.GIT_TAG} ${params.HOST_IP} ${params.ENV}'
            }
        }
    }    
}
