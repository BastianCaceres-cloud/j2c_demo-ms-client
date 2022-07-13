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
      }
    }
    stage ("Checkjava"){
        //verificar si java está instalado
      steps{
      }
    }
    stage ("Clean"){
        //limpiar los archivos compilados de ejecuciones anteriores del pipeline
      steps{
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
      }
    }
    stage ("SonarQube"){
        //verificar calidad de código con SonarQube
      steps{
      }
    }
    stage ("Build"){
        //construcción de ejecutable (jar)
      steps{
          echo 'building the applications...'
          bash "mvn install
      }
    }
    stage ("Package"){
        //registro en nexus del ejecutable versionado
      steps{
      }
    }
  }
    post{
        always{
        }
        failure{
            //notificación de falla
        }
    }
    
    
