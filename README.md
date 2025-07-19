# Cyclistic-Google_Data_Analytics

Este repositorio documenta el proyecto final del Certificado profesional de Análisis de Datos de Google.  

El objetivo principal es aplicar el proceso completo de análisis para resolver un problema empresarial simulado, siguiendo las seis etapas fundamentales:
**Preguntar, Preparar, Procesar, Analizar, Compartir y Actuar**. Cada paso contribuye a desarrollar habilidades técnicas y estratégicas clave para la toma de decisiones basada en datos.

## 🎬 Escenario
Como analista de datos junior en el equipo de marketing de una empresa de bicicletas compartidas en Chicago, denominada Cyclistic, tu tarea consiste en analizar las diferencias de uso entre los **usuarios ocasionales** y los **miembros anuales**.  

La directora de marketing considera que aumentar el número de suscipciones anuales es clave para el éxito del negocio.  

El objetivo es identificar patrones de comportamiento que sirvan de base para una nueva estrategia de marketing enfocada en convertir usuarios casuales en suscriptores. Las recomensaciones deberán estar respaldadas por datos sólidos y visualizaciones profesionales, ya que serán presentadas ante el equipo ejecutivo para su aprobación.

### 💼 Personajes y equipos

- **Cyclistic**: Empresa con más de 5800 bicicletas y 600 estaciones distribuidas por Chicago. Además de los modelos tradicionales, ofrece opciones asistidas como triciclos de mano, bicicletas reclinadas y de carga, promoviendo un sistema más inclusivo para personas con discapacidad o necesidades específicas. Aunque la mayoría de los usuarios viajan por ocio, cerca del 30% utiliza el servicio para desplazarse al trabajo.
- **Lily Moreno**: Directora de marketing y responsable del desarrollo de campañas para promover el servicio. Supervisa iniciativas en distintos canales como redes sociales, email y otros medios digitales.
- **Equipo de analistas de marketing**: Grupo encargado de recopilar, analizar y reportar datos que orienten la estrategia de marketing. Como analista junior, llevas seis meses dentro del equipo, familiarizándote con los objetivos del negocio y con el papel que puede desempeñar el análisis de datos para alcanzarlos.
- **Equipo ejecutivo**: Orientado a los detalles, decidirán si se aprueba el programa de marketing recomendado.

### 🏙️ Sobre la empresa
Cyclistic es un programa de bicibletas compartidas lanzado en 2016 en la ciudad de Chicago. A lo largo de los años ha crecido hasta contar con más de **5.800 bicicletas geolocalizadas y 692 estaciones**, lo que permite a los usuarios recoger y devolver bicicletas en cualquier punto.  

Su estrategia de marketing se ha centrado en atraer públicos amplios mediante una oferta flexible de tarifas: abonos de un viaje, abonos de día completo y membresías anuales. Los clientes esporádicos (pases únicos o diarios) son considerados usuarios casuales, mientras que quienes adquieren la membresía anual son miembros de Cyclistic.  

Aunque esta flexibilidad ha atraído a muchos clientes, los analistas financieros han concluido que los miembros anuales son significativamente más rentables. Por eso, en lugar de crear una campaña de marketing dirigida a nuevos clientes, Lily Moreno cree que existe una gran oportunidad para **convertir usuarios ocasionales en socios**, aprovechando que estos ya conocen y utilizan el servicio.  

Para lograrlo, es clave entender mejor las diferencias entre ambos perfiles, qué motivaría a un usuario casual a adquirir una membresía y qué papel puede jugar el marketing digital en esa transicción. El análisis de datos histórico de viajes será fundamental para identificar patrones y diseñar estrategias efectivas.

## ❓ Preguntar  
En esta fase se define claramente el problema de negocio que se busca resolver mediante el análisis de datos.  

### Tarea Empresarial  
Cyclistic busca aumentar el número de miembros anuales, ya que estos generan más ingresos que los usuarios ocasionales. El objetivo es entender cómo se comportan ambos grupos de usuarios y en qué se diferencian.  
El análisis permitirá identificar patrones de comportamiento clave que puedan usarse para diseñar campañas de marketing digital mejor segmentadas, aumentando la probabilidad de que usuarios ocasionales se conviertan en miembros anuales.

### Pregunta clave a responder
¿Cómo varía el uso de las bicicletas entre usuarios ocasionales y los miembros anuales?

### Interesados clave  
Este estudio será compartido con:
- La directora de marketing, Lily Moreno  
- El equipo ejecutivo de Cyclistic  
- El equipo de análisis de marketing  

## 🗃️ Preparar  
Descripción de los datos recopilados, su origen, estructura y organización  

### Fuente de datos  
Se utilizaron datos históricos de viajes en bicicleta del sistema [Divvy](https://divvy-tripdata.s3.amazonaws.com/index.html), originalmente recopilados por Motivate International Inc. y actualmente gestionados por Lyft Bikes and Scooters, LLC.  
Los datos corresponden al periodo entre **julio de 2024 y junio de 2025**. Esta información es pública, anónima y de libre uso, con restricciones relacionadas a la privacidad de los usuarios.  
### Estructura de los datos  
Los datos están organizados en archivos mensuales en formato .csv, cada uno de los cuales contiene registros individuales de cada viaje: id del viaje, tipo de bicicleta (clasica, docked o eléctrica), fecha y hora de inicio y fin, nombre, identificador y coordenadas de la estación de partida y de llegada, y tipo de usuario (casual o miembro).  
### Consideraciones sobre privacidad y licencia  
Los datos son públicos y anónimos, proporcionados bajo una licencia que permite su uso y análisis para fines legítimos. Está prohibido identificar usuarios o vender los datos como conjunto independiente. Para más detalles, consultar la [licencia](https://divvybikes.com/data-license-agreement).  
### Verificación e integridad
Se realizó una revisión preliminar para asegurar que todos los archivos estuvieran completos, sin columnas faltantes ni datos corruptos evidentes. También se verificó que las categorias y formatos de campos clave (fechas, duración, tipo de usuario) fueran consistentes y adecuados para continuar el análisis.
### Utilidad para el análisis  
Estos datos provienen de una fuente oficial, son confiables y permiten identificar patrones de uso entre usuarios ocasionales y miembros anuales, lo cual es esencial para responder a la pregunta de negocio planteda en la fase anterior.

## 🛠️ Procesar  
Descripción del tratamiento y limpieza de los datos para prepararlos para el análisis.  
La herramienta usada para manipular los datos es RStudio.  

### Bibliotecas  
Durante esta fase se utilizaron varias bibliotecas:
```r
# colección de paquetes para importar, manipular y visualizar datos
install.packages("tidyverse")
library("tidyverse")
# facilita el trabajo con fechas y horas
install.packages("lubridate")
library("lubridate")
# janitor: útil para limpiar nombres de columnas y detectar inconsistencias
install.packages("janitor")
library("janitor")
# dplyr: parte de tidyverse, permite filtrar, seleccionar y transformar datos fácilmente
install.packages("dplyr")
library("dplyr")
```
### Lectura  
Se importaron los 12 archivos mensuales en formato .csv y se unieron en un único dataframe para facilitar el análisis global.  
```r
trips_202407 <- read.csv("202407-divvy-tripdata.csv")
trips_202408 <- read.csv("202408-divvy-tripdata.csv")
trips_202409 <- read.csv("202409-divvy-tripdata.csv")
trips_202410 <- read.csv("202410-divvy-tripdata.csv")
trips_202411 <- read.csv("202411-divvy-tripdata.csv")
trips_202412 <- read.csv("202412-divvy-tripdata.csv")
trips_202501 <- read.csv("202501-divvy-tripdata.csv")
trips_202502 <- read.csv("202502-divvy-tripdata.csv")
trips_202503 <- read.csv("202503-divvy-tripdata.csv")
trips_202504 <- read.csv("202504-divvy-tripdata.csv")
trips_202505 <- read.csv("202505-divvy-tripdata.csv")
trips_202506 <- read.csv("202506-divvy-tripdata.csv")
```
```r
column_names <- list(
    df1 = names(trips_202407), df2 = names(trips_202408), df3 = names(trips_202409), df4 = names(trips_202410),
    df5 = names(trips_202411), df6 = names(trips_202412), df7 = names(trips_202501), df8 = names(trips_202502),
    df9 = names(trips_202503), df10 = names(trips_202504), df11 = names(trips_202505), df12 = names(trips_202506)
)

all_same <- all(sapply(column_names, function(x) identical(x, column_names[[1]])))

print(all_same)

```
```r
column_types <- list(
    df1 = sapply(trips_202407, class), df2 = sapply(trips_202408, class), df3 = sapply(trips_202409, class),
    df4 = sapply(trips_202410, class), df5 = sapply(trips_202411, class), df6 = sapply(trips_202412, class),
    df7 = sapply(trips_202501, class), df8 = sapply(trips_202502, class), df9 = sapply(trips_202503, class),
    df10 = sapply(trips_202504, class), df11 = sapply(trips_202505, class), df12 = sapply(trips_202506, class)
)

all_types_same <- all(sapply(column_types, function(x) identical(x, column_types$df1)))

print(all_types_same)
```
```r
trips_202407_202506 <- bind_rows(
    trips_202407,trips_202408,trips_202409,trips_202410,trips_202411,trips_202412,
    trips_202501,trips_202502,trips_202503,trips_202504,trips_202505,trips_202506
)
```
```r
trips_202407_202506 <- trips_202407_202506 %>% select(-c(start_lat, start_lng, end_lat, end_lng))
```
```r
library(skimr)
skim(trips_202407_202506)
```
```r

```
```r

```
