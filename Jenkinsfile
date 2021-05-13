pipeline 
        {
            agent any
            stages
                {
                    stage ("Git Checkout")
                            {
                                steps 
                                        {
                                            git branch: 'master', url: 'https://github.com/prashanth-konakala-bluepal/Sonarqube-Project.git'
                                        }
                            }
                    stage ("Build")
                            {
                                steps
                                        {
                                            sh 'mvn clean install -f MyWebApp/pom.xml'
                                            sh 'mvn clean package -f MyWebApp/pom.xml'
                                        }
                            }
                    stage ("Sonar Analysis")
                            {
                                steps
                                        {
                                            script 
                                                    {
                                                        def scannerHome = tool 'sonarqube';
                                                        withSonarQubeEnv("Sonarqube_Pipeline_OhioRegion")
                                                        {
                                                         sh " mvn -f MyWebApp/pom.xml sonar:sonar \
                                                              -Dsonar.projectName=Sonarqube_Jenkinsfile_Pipeline \
                                                              -Dsonar.projectKey=Sonarqube_Jenkinsfile_Pipeline \
                                                              -Dsonar.login=b86e54949ae3cb448a47fbd9aca44dfc24fc214d "
                                                        }
                                                    }
                                        }
                            }
                    stage ("Code Coverage")
                            {
                               steps 
                                    {
                                      jacoco()       
                                    }
                            }
                }
        }
