pipeline {
  agent any
    tools{
        maven 'Maven'
    }
    parameters{
        booleanParam(name: 'executeTests', defaultValue: true, desription:'')
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
        echo 'checkjava'
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
        echo 'test'
      }
    }
    stage ("SonarQube"){
        //verificar calidad de código con SonarQube
      steps{
        echo 'sonar'
      }
    }
    stage ("Build"){
        //construcción de ejecutable (jar)
      steps{
          echo 'building the applications...'
          bash "mvn install"
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
    
