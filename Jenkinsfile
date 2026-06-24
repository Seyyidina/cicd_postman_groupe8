pipeline {
    agent {
        docker
        { 
            image 'postman/newman:latest'
            args '-u=root --entrypoint='
        }  
    }
    parameters {
        choice(name: 'collection_choisie', choices: ['collection', 'Collection_1', 'Collection_2'], description: 'Collection à lancer')
        choice(name: 'Environnements', choices: ['Env_1', 'Env2'], description: 'Choix des environnements')
        booleanParam(name: 'select_tout', defaultValue: true, description: 'Lancer tout')
        booleanParam(name: 'selection', defaultValue: true, description: 'Lancer selon le choix')
    }

    stages {
        stage('lancer le test') {
            steps {
                script {
                    if (params.select_tout) {
                        sh 'newman run collection.json'
                        sh 'newman run collection_1.json -e Env_1.json'
                        sh 'newman run collection_2.json -e Env2.json'
                    }
                    else {
                        if (params.selection) {
                            sh 'newman run collection.json'
                        }
                        else {
                            switch (params.Environnements) {
                                case 'Env_1':
                                    sh 'newman run Collection_1.json -e Env_1.json'
                                    break;
                                case 'Env2':
                                    sh 'newman run Collection_2.json -e Env2.json'
                                    break;
                                default:
                                    sh 'newman run collection.json'
                                    break;                                                                   
                            }
                        }
                    }
                        

                }
               
            }
        }
    }
}
