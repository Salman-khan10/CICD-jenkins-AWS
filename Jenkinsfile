node {
    def appDir = '/var/ww/nextjs-app'

    stage('Clean Workspace'){
        echo 'Cleaning Jenkins Woorkspace'
        deleteDir()
    }

    stage('Clone Repo '){
        echo 'Cloning Repo'
        git(
            branch: 'main' ,
            url: 'https://github.com/Salman-khan10/CICD-jenkins-AWS'
        )
    }

    stage('Deploy to EC2'){
        ecjo 'Deploying to EC2'
        sh """
            sudo mkdir -p ${appDir}
            sudo chown -R jenkins:jenkins ${appDir}

            rsync -av --delete --exclude='.git' --exclude='node_modules' ./ ${appDir}

            cd ${appDir}
            sudo npm install
            sudo npm run build
            sudo fuser -k 3000/tcp || true
            npm run start

        """
    }
}
