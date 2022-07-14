pipeline {
  agent any
    tools{
        maven 'Maven'
    }
    parameters{
        booleanParam(name: 'executeTests', defaultValue: true, description:'')
    }
    
  stages {
    stage ("Checkout"){
        //se obtienen los fuentes a pasar por el pipeline
      steps{
        echo 'checkout'
      }
    }
    stage ("Checkjava"){
        //verificar si java está instalado
      steps{
        bat 'java -version'
      }
    }
    stage ("Clean"){
        //limpiar los archivos compilados de ejecuciones anteriores del pipeline
      steps{
        echo 'clean'
      }
    }
    stage ("Test"){
        //ejecución y validación de test
        when { 
            expression {
                params.executeTests
            }
        }
            
      steps{
        bat 'mvn verify'
      }
    }
    stage ("SonarQube"){
        //verificar calidad de código con SonarQube   
       
      steps {
        script {
           def sonarParams=" -Dsonar.projectName=clientms-0.0.1-SNAPSHOT -Dsonar.projectKey=clientms-0.0.1-SNAPSHOT \
          -Dsonar.projectVersion=clientms-main -Dsonar.analysis.version=0.0.1-SNAPSHOT \
          -Dsonar.sources=src/main -Dsonar.sourceEncoding=UTF-8 -Dsonar.java.binaries=target/classes \
         -Dsonar.test.inclusions=src/test -Dsonar.junit.reportsPath=target/surefire-reports \
         -Dsonar.surefire.reportsPath=target/surefire-reports -Dsonar.binaries=target/classes \
         -Dsonar.java.coveragePlugin=jacoco -Dsonar.coverage.jacoco.xmlReportPaths=target/site/jacoco-ut/jacoco.xml \
         -Dsonar.analysis.projectName=clientms \
         -Dsonar.analysis.branch=main -Dsonar.qualitygate.wait=true"     

        }
        withSonarQubeEnv('sonar'){
          bat "mvn -U -Pprod sonar:sonar ${sonarParams}"
        }

      }
    }
    stage ("Build"){
        //construcción de ejecutable (jar)
      steps{
          echo 'building the applications...'
          bat "mvn install"
      }
    }
    stage ("Package"){
        //registro en nexus del ejecutable versionado
      steps{
        echo 'package'
      }
    }
  }
    post{
        always{
          echo 'ok'
        }
        failure{
          echo 'falla'
            //notificación de falla
        }
    }
}


    
