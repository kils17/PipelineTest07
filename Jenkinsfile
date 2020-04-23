pipeline {
    // 다수의 agent를 사용하기 위해선 pipeline 후 선언하는 agent를 none으로 선언합니다.
    agent none
    stages {
        stage('Run Tests') {
            // stage를 병렬로 실행
            // Jenkins 문서 에서는 steps를 병렬처리하는 것 보다, stage를 병렬처리하는 것을 추천하고 있습니다.  
            parallel {
                // parallel의 안에서 다시 stage를 정의 합니다.
                stage('Test On Windows') {
                    // 이 스테이지에서 사용할 agent의 값을 label을 통해 지정합니다.
                    agent {
                        label "${Windows}"
                    }
                    // steps의 세부처리로 bat을 통해 windows 명령어를 실행합니다. 
                    steps {
                      bat "whoami"
                      bat "ipconfig"
                    }
                }
                // Linux(docker container == jenkins master server) 에서 실행 
                stage('Test On Linux') {
                    // agent는 기본값인 master가 설정 됩니다.
                    agent any
                    // sh를 통해 shell명령어를 실행합니다.
                    steps {
                        sh 'pwd'
                    }
                }
            }
        }
    }
}
