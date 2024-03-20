pipeline {
    
agent {
label 'jenkins-ansible'
}

environment{
AWS_EC2_PRIVATEKEY=credentials('EC2-Instance-Private-Key-File')
}

options {
  buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')
  timestamps()
}

    
parameters {
  choice choices: ['development', 'staging', 'master'], description: 'Select the Branch Name', name: 'BranchName'
}
    
stages{
stage('Checkoutcode'){
steps{
git branch: "${params.BranchName}", credentialsId: 'c1af1c61-a689-4e7b-8b47-e2b438a11ea6', url: 'https://github.com/tajroshith/jenkins-with-ansible.git'
}
}

stage('ExecutePlaybook'){
steps{
sh "ansible-playbook -i inventory/star.hosts playbooks/installTomcat.yaml --private-key=$AWS_EC2_PRIVATEKEY --ssh-common-args='-o StrictHostKeyChecking=no'"
}
}

}// Stages Closing
}// Pipeline Closing
