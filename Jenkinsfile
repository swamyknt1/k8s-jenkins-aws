node {

    stage("Git Clone"){

        git credentialsId: 'GIT_HUB_CRED', url: 'https://github.com/swamyknt1/k8s-jenkins-aws'
    }

     stage('Gradle Build') {

       sh './gradlew build'

    }

    stage("Docker build"){
        sh 'docker version'
        sh 'docker build -t jhooq-docker-demo1 .'
        sh 'docker image list'
        sh 'docker tag jhooq-docker-demo1 498381/jhooq-docker-demo1:jhooq-docker-demo1'
    }

    withCredentials([string(credentialsId: 'DOCKER_HUB_PASS', variable: 'PASSWORD')]) {
        sh 'docker login -u 498381 -p $PASSWORD'
    }

    stage("Push Image to Docker Hub"){
        sh 'docker push  498381/jhooq-docker-demo1:jhooq-docker-demo1'
    }
    
    stage("kubernetes deployment"){
        sh 'kubectl apply -f k8s-spring-boot-deployment.yml'
    }
} 
