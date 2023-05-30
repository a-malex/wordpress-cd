pipeline {
    stage any
    stages {
        stage('Execute Ansible Adhoc Command') {
            steps {
                dir("ansible-docker/") {
                    sh '''
                        ansible all -i hosts.ini -b -m raw -a "apt install python3 /" 
                    '''
                }
            }
        }
        stege('Infrastructure Configuration') {
            steps {
                dir("ansible/") {
                    ansiblePlaybook(
                        playbook: "playbook.yml",
                        become: true,
                        credentialsId: "ansible_ssh_key",
                        hostKeyChecking: false,
                        disableHostKeyCheccking: true,
                        inventory: "hosts.ini"
                    )
                }
            }
        }
        stege('Deploy App using Docker Compose') {
            steps {
                dir("ansible-deploy/") {
                    ansiblePlaybook(
                        playbook: "playbook.yml",
                        become: true,
                        credentialsId: "ansible_ssh_key",
                        hostKeyChecking: false,
                        disableHostKeyCheccking: true,
                        inventory: "hosts.ini"
                    )
                }
            }
        }
    }
}
