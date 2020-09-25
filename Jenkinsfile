node()
{
     stage('Cloning git') 
     {
        checkout scm
     }
        
     stage('Installing dependencies')
     {
         nodejs('nodejs')
        {
            sh 'npm install'
            echo "Module Installed"
        }
     }
    
     stage('Build') 
     {
        nodejs('nodejs')
        {
            sh 'npm run build --prod'
            echo "Build Complete"
        }
     }   
     
     stage('Package Build')
     {
        sh "tar -zcvf bundle.tar dist/my-app/"
     }
        
     stage('Artifcts creation')
     {
        fingerprint 'bundle.tar.gz'
        archiveArtifacts 'bundle.tar.gz'
        echo "Artifcts created"
     }
         
     stage('Stash Changes')
     {
        stash allowEmpty: true, includes: 'bundle.tar.gz' , name: 'buildArtifacts'
     }
   
}

node('ngnodeserver')
{
    echo 'Unstash'
    unstash 'buildArtifacts'
    echo 'Artifcts copied'
    
    echo 'Copy'
    sh "yes | sudo cp -R bundle.tar.gz /var/www/html && cd /var/www/html && sudo tar -xvf bundle.tar.gz"
    echo 'Copy Completed'
}