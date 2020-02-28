pipeline{
    agent any
    stages{
        
         stage('Getting Code From GitHub')
      {
        steps {
              git 'https://github.com/adil1806/INGFavBank.git'
              } 
      }
        stage('Build'){
            steps{
             sh '/opt/maven/bin/mvn clean package'
            }
        }
        stage('Release'){
            steps{
                sh 'export JENKINS_NODE_COOKIE=dontkillme ; nohop java -jar $WORKSPACE/target/*.jar &'
            }
        }
        stage('Copy jar and application.property file to Ansible Server'){
            steps{
             sshPublisher(publishers: [sshPublisherDesc(configName: 'Ansible', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//home//ansadm//demo', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '**/*.properties')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
        stage('Copy Application.property file to Ansible Server'){
            steps{
            sshPublisher(publishers: [sshPublisherDesc(configName: 'Ansible', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//home//ansadm//demo', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '**/*.jar')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
        stage('Running Playbook'){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'Ansible', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'ansible-playbook back.yml', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}
