pipeline {
    agent {
        label 'master'
    }

    environment {
        PATH="/usr/local/bin:$PATH"
        VAULT_ADDR="http://127.0.0.1:8200"
    }

    stages {
        stage('AppRole Auth and Azure Login') {
            steps {
                withCredentials([[$class: 'VaultTokenCredentialBinding', \
                    addrVariable: 'VAULT_ADDR', \
                    credentialsId: 'vault-approle', \
                    tokenVariable: 'VAULT_TOKEN', \
                    vaultAddr: "$VAULT_ADDR"]]) {
                sh '''
                set +x
                export $(curl -s --header "X-Vault-Token: $VAULT_TOKEN" "$VAULT_ADDR/v1/azure/creds/jenkins" | \
                    jq -r '.data | to_entries | .[] | .key + "=" + .value')
                az login --service-principal -u $client_id -p $client_secret --tenant $tenant_id
                '''
                }
            }
        }
        
        stage('List Resource Groups') {
            steps {
                sh 'az group list'
            }
        }
    
        stage('Azure Logout') {
            steps {
                sh 'az logout'
            }
        }
    }
}
