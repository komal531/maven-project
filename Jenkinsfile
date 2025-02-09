
pipeline
{
    agent any
    stages
    {
        // CI part
        stage ('scm checkout')
        {
            steps {
                git 'https://github.com/komal531/maven-project.git'
            }
        }
        stage ('validate the code')
        {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn validate'
                }
            }
        }
        stage ('compile the code')
        {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn compile'
                }
            }
        }
        stage ('package the code')
        {
            steps {
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
                    sh 'mvn package'
                }
            }
        }
        // CD part
        stage ('deploy the code on tomcat')
        {
            steps {
                sshagent(['DEFCICD']) {
                    sh 'scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@172.31.0.193:/usr/share/tomcat/webapps'
                }
            }
        }
    }
}



//sh 'scp -o StrictHostKeyChecking=no  '

//sh 'scp -o StrictHostKeyChecking=no  <source file> <user name>@<ip of tomcat server>:<destination file>'

//sh 'scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@172.31.15.52:/usr/share/tomcat/webapps'

//To copy a file from one server to another using the scp command, use the syntax: 
//scp [source_username@source_host:source_file] [destination_username@destination_host:destination_path]; 
//where "source_username" is the username on the source server, "source_host" 
//is the source server's IP address, "source_file" is the file you want to copy, 
//"destination_username" is the username on the destination server, and "destination_path" 
//is the location where you want to copy the file on the destination server. 


//cp src_file tgt_file
//scp user_name/ path    IP address/user_name/path
