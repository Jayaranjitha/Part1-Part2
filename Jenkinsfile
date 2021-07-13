node {
    // Get Artifactory server instance, defined in the Artifactory Plugin administration page.
    def server = Artifactory.server "SERVER_ID"
    // Create an Artifactory Maven instance.
    def rtMaven = Artifactory.newMavenBuild()
    def buildInfo

    stage('Clone sources') {
        git url: 'https://github.com/Jayaranjitha/Part1-Part2.git'
    }

 
    stage('Artifactory configuration') {
       
        steps {
        
        sh '''
            npm config set registry https://repo.lab.pl.alcatel-lucent.com/gsc-pspp-mvn-dependencies/
            npm config set cafile /etc/pki/ca-trust/extracted/pem/tls-ca-bundle.pem
        '''
        
      }
    }

    stage('Maven build') {
        buildInfo = rtMaven.run pom: 'pom.xml', goals: 'clean install'
    }

    stage('Publish build info') {
        server.publishBuildInfo buildInfo
    }
}
