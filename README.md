# Jenkins DevOps on IBM Cloud Schematics :cloud:

En esta guía encontrará una descripción detallada sobre automatización del despliegue de Infraestructura con IBM Cloud Schematics usando Jenkins como herramienta de DevOps .

<img width="700" alt="workspace" src="Assets/architecture1.jpeg"> 


## 1. Configuración del proyecto en Jenkins :computer:

Jenkins es un servidor de automatización de código abierto autónomo que se puede utilizar para automatizar todo tipo de tareas relacionadas con la creación, prueba y entrega o implementación de software. Jenkins se puede instalar a través de paquetes del sistema nativo, Docker, o incluso ejecutarse de forma independiente en cualquier máquina que tenga instalado un Java Runtime Environment (JRE). 

La configuración en de la tarea DevOps requiere de la creación de un proyecto **Multibranch Pipeline** para la configuración de un repositorio GitHub el cual contendrá el archivo Jenkinsfile para ejecutar la tarea.

<img width="545" alt="item" src="Assets/create-item.JPG">

Una vez creado el proyecto se debe vincular al respositorio de GitHub donde se encuentra el Jenkinsfile a utilizar, en la siguiente imagen encontrará la configuración de ejemplo:

<img width="545" alt="cred" src="Assets/set-credentials.JPG"> 

Como se puede ver se deben añadir las credenciales del usuario en GitHub y luego de ello ingresar la dirección del repositorio. Para añadir las credenciales de la cuenta de GitHub se debe especificar la información de **Username** y **Password** como se muestra en la siguiente imagen:

<img width="545" alt="github credentials" src="Assets/github-credentials.JPG">

Una vez creado el proyecto se puede observar un _DASHBOARD_ como aparece en la siguiente imagen:

<img width="545" alt="dash_jenkins" src="Assets/dash-jenkins.JPG">

En donde se selecciona el **commit** master que contiene el archivo Jenkinsfile para la ejecución de tareas.
Una vez alli se observa el _DASHBOARD_ del **master**:

<img width="545" alt="dash_workspace" src="Assets/dash-master.JPG">

Para ejecutar el PIPELINE se selecciona **Build with Paramenters**, luego de ello aparecerán los parametros requeridos como se muestra a continuación:

<img width="545" alt="dash_workspace" src="Assets/select_os.JPG">

Se debe selecciónar el sistema operativo sobre el cual la herramienta Jenkins esta instalado. También se debe ingresar el IAM Token el cual se obtiene dentro de su CLI con el siguiente comando:
```
ibmcloud iam oauth-tokens
```

## 2. Jenkisfile :page_with_curl:	

La estructura de código del archivo Jenkinsfile consta de 
```
pipeline {
    agent any

    stages {
        stage('DevOps Schematics') {
            steps {
                
            }
        }
        
    }
}
```
El Jenkinsfile cuenta con un pipeline con diferentes directivas. La directiva **agent** determina el motor de ejecución. En este caso se acepta cualquiera. La directiva **stages** establece un conjunto de etapas. Y por ultimo se tiene la directiva **steps** donde se determinan los pasos de ejecución de la tarea.

La conexión de Jenkins con Schematics se hizo mediante la API de Schematics. Las peticiones y el código correspondiente se encuentran en el archivo **Jenkinsfile** del presente repositorio; estas peticiones responden a los pasos necesarios para aprovisonar un recurso dentro de Schematics (que se encuentran referenciados en la [Documentación](https://cloud.ibm.com/docs/schematics?topic=schematics-getting-started)) de Schematics y los cuales son:

1). Crear un workspace

2). Crear un plan

3). Aplicar un plan

La estructura general de las peticiones a la API de Schematics se encuentra a continuación:

Linux:
```
curl --request _(POST, PUT, GET)_ --url _URL_ -H _Token de Autorización_ -d _Datos de petición_
```
Windows:
```
Invoke-RestMethod -Uri _URL_ -Method _(GET-POST-PUT)_ -Headers __Token de Autorización__ -Body _Datos de petición_
```

## 3. Resultados

Al ejecutar un nuevo Pipeline puede encontrar la descripción del proceso al ingresar a la información de los logs. También puede corroborar que el proceso fue exitoso al ingresar a la lista de workspaces, donde se creará el workspace "jenkins".

<img width="745" alt="dash_workspace" src="Assets/workspaces.png">

También puede ingresar a la interfaz de Skytap donde ecnontrará las dos máquinas aprovisionadas, con las características especificadas dentro de la [plantilla de Terraform](https://github.com/emeloibmco/Skytap-DevOps-Terraform) usada en la guía.

<img width="745" alt="dash_workspace" src="Assets/skytap.png">

## Referencias
Encuentre información sobre Jenkins en: [Jenkins documentation](https://www.jenkins.io/doc/)
<br>
Encuentre información sobre IBM Cloud Schematics API en: [IBM Cloud Schematics API](https://cloud.ibm.com/apidocs/schematics)
<br>

## Autores :black_nib:
IBM Cloud Tech Sales
