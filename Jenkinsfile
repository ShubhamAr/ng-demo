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
            bat 'npm install'
            echo "Module Installed"
        }
     }
    
     stage('Build') 
     {
        nodejs('nodejs')
        {
            bat 'npm run build --prod'
            echo "Build Complete"
        }
     }   
     
}
