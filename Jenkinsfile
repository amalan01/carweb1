node('ubuntu-Appserver-2140')
{
    def app
    stage('Cloning Git')
    {
        /* Let's make sure we have the repository cloned to our workspace */
        checkout scm

    }

    stage('Build-and-Tag')
    {
        app = docker.build('amalan06/carweb1')
        

    }

    stage('Post-to-dockerhub')
    {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials')
        {
          app.push("latest")  
        }
        

    }
    stage('Pull-image and Deploy')
    {
        sh "docker-compose down"
        sh "docker-compose up -d"         
    }

}
