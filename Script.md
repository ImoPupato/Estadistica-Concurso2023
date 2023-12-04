## Ciclo PPDAC

<p align = "center">
<img src="https://github.com/ImoPupato/Estadistica-Concurso2023/blob/main/Ciclo%20ppdac.PNG">
</p>

Cuando los datos provienen de un censo o estudio poblacional, luego de aplicar herramientas del análisis descriptivo _(Etapa A)_ podemos avanzar directamente hacia las conclusiones _(Etapa C)_.  

En el caso de contar con una **muestra**, como los datos están incompletos en el sentido que no se cuenta con información de toda la población, debemos considerar como **preliminares** a los resultados de nuestro análisis. En próximas unidades, trabajaremos con herramientas inferenciales para generalizar las conclusiones a la población de referencia _(Etapa C)_. Estas herramientas, que también se asocian al análisis de los datos _(Etapa A)_.  
  
En esta clase, a través de un ejemplo, aplicaremos las principales herramientas de análisis descriptivo univariado que hemos abordado en la teoría.

## Situación problema
Para certificar normas de calidad, una empresa controla periódicamente ciertas componentes electrónicas que fabrica. Una de las características que se requiere evaluar es su longitud (medida en mm).  
Interesa tener información sobre la **proporción** de esas componentes cuya longitud es menor a 80 mm.  
Para ello, se toma una **muestra aleatoria simple** de **100 componentes**, se le mide la **longitud** a cada una de ellas y se lleva a cabo un análisis estadístico.  
_En negrita se encuentran indicadas las palabras claves necesarias para completar la descripción del problema._  
_Para realizar una descripción completa, debemos detallar **Variable en estudio**, **Unidad experimental**, **Muestra**, **Población**, **Población estadística**, **Objetivo** del estudio, **Parámetro** de interés y **Estimador** de dicho parámetro.  

### Descripción del problema
- Variable:  longitud de las componentes (cuantitativa, continua)  
- Unidad: componente electrónica fabricados por dicha empresa  
- Muestra: 100 componentes  
- Población: todas las componentes electrónicas fabricadas por dicha empresa  
- Población estadística: todas las longitudes de las componentes  
- Objetivo: conocer la proporción de componentes cuya longitud es menor a 80 mm  
- Parámetro de interés: proporción de componentes con longitud menor a 80 mm, $\pi$  
- Estimador: $f_0$, frecuencia relativa de componentes con longitud menor a 80 mm en la muestra
  
### ¡Vamos a R!
## Asignar el directorio de trabajo  
Recordar que en la función _'setwd'_, debemos indicar la ruta de la carpeta donde queremos guardar el espacio de trabajo y desde dónde leeremos las bases de datos.
```R
setwd("C:/Users/Aylen/Desktop/Estadistica-2023") #las barras deben ser las indicadas
```
### Cargar los datos
```R
library(readxl) # llamamos a la librería necesaria para leer el archivo de extensión .xlsx
datos <- read_excel("datos problema.xlsx") # asignamos los datos al objeto "datos"
```
### Explorar la tabla
```R
class(datos)
class(datos$longitud)
```
### Proporción de componentes con longitud menor a 80 mm
La frecuencia relativa ($f_0$) es el cociente entre el número de unidades que satisfacen el criterio y el total.  
```R
sum(datos$longitud>80)/length(datos$longitud)
```
_Entre las componentes analizadas, un 97% cumplen la pretensión de tener una longitud menor a 80 mm._  
### Estadísticas descriptivas
```R
summary(datos) #posición
IQR(datos) # rango intercuartil
var(datos) # variancia
sd(datos$longitud) # desvío estándar
sd(datos$longitud)/mean(datos) # coeficiente de variación
```
Resumimos los resultados en una tabla que nos permita describir el conjunto de datos:
<table>
    <thead>
        <tr>
            <th> Tipo de estadístico </th>
            <th> Estadístico </th>
            <th> Valor (mm) </th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=7 align="center"> Posición </td>
            <td rowspan=1 align="center"> Mínimo ($y_{min}$)</td>
            <td align="center"> 78.50 </td>
        <tr>
            <td rowspan=1 align="center"> Primer cuartil ($Q_1$) </td>
            <td align="center"> 86.25 </td>
        <tr>
            <td rowspan=1 align="center"> Segundo cuartil o mediana ($Q_2$) </td>
            <td align="center"> 89.30 </td>
        <tr>
            <td rowspan=1 align="center"> Tercer cuartil ($Q_3$) </td>
            <td align="center"> 92.42 </td>
        <tr>
            <td rowspan=1 align="center"> Media ($\overline{y}$) </td>
            <td align="center"> 89.27 </td>
        <tr>
            <td rowspan=1 align="center"> Máximo ($y_{max}$) </td>
            <td align="center"> 101.00 </td>
       </tbody>
       <tbody>
        <tr>   
            <td rowspan=7 align="center"> Dispersión </td>
            <td rowspan=1 align="center"> Variancia ($s^2$)</td>
            <td align="center"> 23.88 </td>
        <tr>
            <td rowspan=1 align="center"> Desvío estándar ($s$) </td>
            <td align="center"> 4.89 </td>
        <tr>
            <td rowspan=1 align="center"> Rango ($r$) </td>
            <td align="center"> 22.5 </td>
        <tr>
            <td rowspan=1 align="center"> Rango intercuartil ($ric$ = $Q_3$ - $Q_1$) </td>
            <td align="center"> 6.17 </td>
        <tr>
            <td rowspan=1 align="center"> Coeficiente de vazriación ($cv$ = $s$ / $\overline{y}$) </td>
            <td align="center"> 0.055 </td>
    </tbody>
</table>

### Análisis gráfico
Diagrama de caja y bigotes (boxplot)
```R
boxplot(datos$longitud, # datos
        horizontal = TRUE, # boxplot horizontal
        xlab="Longitud de componente (mm)",# etiqueta del eje x
        col = "lightgreen") # color
title(main = "Diagrama de caja y bigotes correspondiente a la longitud de los componentes", # título
      cex.main = 1) # tamaño de la letra
```
<div>
<p style = 'text-align:center;'>
<img src="https://github.com/ImoPupato/Estadistica-Concurso2023/blob/main/Boxplot.png">
</p>
</div>
    
Histograma de frecuencias
```R
hist(datos$longitud, # datos
     breaks=6, #cantidad de intervalos
     ylim = c(0,40), # límites del eje y
     col="lightblue", # color
     ylab="Frecuencia", # etiqueta del eje y
     xlab= "Longitod de componente (mm)", etiqueta del eje x
     main= "Histograma correspondiente a la longitud de los componentes" # título
     )
```
<div>
<p style = 'text-align:center;'>
<img src="https://github.com/ImoPupato/Estadistica-Concurso2023/blob/main/Histograma.png">
</p>
</div>
