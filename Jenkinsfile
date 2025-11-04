pipeline {
    agent any

    environment {
        ANSIBLE_CONFIG = "${WORKSPACE}/ansible.cfg"
        INVENTORY = "${WORKSPACE}/inventory"
        PLAYBOOK = "${WORKSPACE}/site.yaml"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/OhseungKeun/jenkins.git'
            }
        }

        stage('Syntax Check') {
            steps {
                sh 'ansible-playbook -i ${INVENTORY} ${PLAYBOOK} --syntax-check'
            }
        }

        stage('Dry Run') {
            steps {
                sh 'ansible-playbook -i ${INVENTORY} ${PLAYBOOK} --check'
            }
        }

        stage('Deploy') {
            steps {
                sh 'ansible-playbook -i ${INVENTORY} ${PLAYBOOK}'
            }
        }
    }

    post {
        failure {
            echo "❌ 배포 실패 — 로그를 확인하세요."
        }
        success {
            echo "✅ 배포 완료 — 모든 단계 성공!"
        }
    }
}
