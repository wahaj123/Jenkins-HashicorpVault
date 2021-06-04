import groovy.json.JsonSlurper
node {
    // Add the path to your secrets
    def kv_path = 'kv/secret'
    withCredentials([[$class: 'VaultTokenCredentialBinding', 
                      addrVariable: 'VAULT_ADDR', // no need to change
                      credentialsId: 'vault-token', // Add your credential id 
                      tokenVariable: 'VAULT_TOKEN', // no need to change
                      vaultAddr: 'http://127.0.0.0:8200']]) { // Add your vault URL
        script{
            secret_key = sh (
                        script: "vault kv get -format json -field=data $kv_path", 
                        returnStdout: true
                        ) // This will list the secrets in the defined path and store it in secret_key
            // Parse the response
            def list = new JsonSlurper().parseText( secret_key )
            // Print them out to make sure
            list.each { println it }
        }
    }
}