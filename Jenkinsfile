pipeline {
    agent {
        docker
        { 
            image 'postman/newman:latest'
            args '-u=root --entrypoint='
        }  
    }
    parameters {
        choice(name: 'Environnements', choices: ['Env_1', 'Env2', 'Env3'], description: 'Choix des environnements')
        booleanParam(name: 'select_tout', defaultValue: true, description: 'Lancer tout')
        booleanParam(name: 'selection', defaultValue: true, description: 'Lancer selon le choix')
    }

    stages {
        stage('lancer le test') {
            steps {
                script {
                    if (params.select_tout) {
                        sh 'newman run collection.json'
                        sh 'newman run Collection_1.json -e ./Environment/Env_1.json'
                        sh 'newman run Collection_1.json -e ./Environment/Env2.json'
                        sh 'newman run Collection_2.json -e ./Environment/Env3.json'
                    }
                    else {
                        if (params.selection) {
                            sh 'newman run collection.json'
                        }
                        else {
                            switch (params.Environnements) {
                                case 'Env3':
                                    sh 'newman run Collection_2.json -e ./Environment/' + params.Environnements + '.json'
                                    break;
                                // Env1 et Env2
                                default:
                                    sh 'newman run Collection_1.json -e ./Environment/' + params.Environnements + '.json'
                                    break;                                                                   
                            }
                        }
                    }
                        

                }
               
            }
        }
    }
}
