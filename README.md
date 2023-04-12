# ozm_10aplicativos_6horas  con transitorios

En este respositorio se analizaran medidas con 3 ozm  trifasicos conformando en total  10 aplicativos  mas el agregado, todo estos durante 6 horas (2+2+2) . Este repositorio por tanto se apoya en el repositorio https://github.com/crn565/ozm10_appliances_transitorios

En efecto, se realiza  en los cuadernos adjuntos a este repositorio el analisis de las medidas de 10 aplicativos incluyendo transitorios  hasta el orden 150 de tension, corriente y potencia. Las Medidas  se realizan con 3  OpenZMeter  Trifásicos  (cada uno con 4 canales de medida)  conformando asi en total  11 canales de medida  que se distribuyen en los 10 aplicativos, mas el agregado. Las medidas corresponden a W, VAR, VA,f, VLN,PF y A, mas los transititoros  hasta el orden 150 de W, V y A,   todas con un marca de tiempo (Timestamp) de 13 dígitos tipo UNIX Epox.


Las medidas se realizaron el 10 de Marzo de 2033  en el Laboratorio de Electrotecnia de la  Escuela de Ingenieria Industrial de la Universidad de Almeria.Las medidas reales fueron tomadas entre las 11:10 y las 13:12 lo que conforma 5818000 milisegundos ( ver cálculo mas abajo). Para conformar 6 horas se agrego un doble offset de  unas 2h para  crear un nuevo DS  compuesto por las medidas reales, las medidas reales +2h y las medidas reales +4h.



Para la adicion de dos offset a los ficheros de medida  se considero el siguinte cálculo:

- Para 12:47:36, hay 12 horas * 60 minutos/hora * 60 segundos/minuto * 1000 milisegundos/segundo + 47 minutos * 60 segundos/minuto * 1000 milisegundos/segundo + 36 segundos * 1000 milisegundos/segundo = 46056000 milisegundos.

- Para 11:10:38, hay 11 horas * 60 minutos/hora * 60 segundos/minuto * 1000 milisegundos/segundo + 10 minutos * 60 segundos/minuto * 1000 milisegundos/segundo + 38 segundos * 1000 milisegundos/segundo = 40238000 milisegundos.

Es decir, para calcular la diferencia entre ambas horas, simplemente restamos el número de milisegundos del segundo tiempo al número de milisegundos del primer tiempo:
46056000 milisegundos - 40238000 milisegundos = 5818000 milisegundos.  Por tanto para ampliar el tiempo de muestras y demostrar  que las medidas deben ser diferentes, a los ficheros csv originales de las medidas, se le añaden nuevos ficheros csv identicos,  pero  con  dos desplazamientos en el campo timestamp ( es decir en un caso sumamamos 58180000 ms y otro sumamos 2 x 5818000 ms).


  
  
Para el  entrenamiento se  han definido tres periodos:

 - TRAIN: 11:10 a 14:58:34 

 - VAL: 14:58:35 a 15:42:22
 
 - TEST: 15:42:23 a 16:26:11
 

Estos datos se entrenaron, tanto con el algoritmo CO, como el algoritmo FHMM.


Los aplicativos  usados en el experimento son los siguintes:

 1 -Main
 
2 - Electric Furnace ( Horno)

3- Microwave (Microonda)

4 - Television

5 - Kettle ( hervidor de agua)

6 - Vacuum Cleaner ( Aspiradora)

7- Electric Space Heater ( Radiador de aceite)

8 - Electric Shower Heater  (Calentador de agua)

9 - Fan  ( Ventilador)

10 - Fridge  ( refrigerador)

11 -  Freezer (congelador)


## Eficiencia  computacional

Para el algoritmo combinatorio se obtienen los siguintes resultados:


![image](https://user-images.githubusercontent.com/75988158/231506370-213a3780-0ef2-41eb-9542-5520cdeaa02a.png)

Para el algoritmo FHMM se obtienen estos resultados limitados por la falta de memoria para ejecutar el algoritmo en tiempos de muestreo inferiores a 5 minutos:

![image](https://user-images.githubusercontent.com/75988158/231506191-cecb7ca8-4f8d-4410-8355-af264ff09280.png)


## RESULTADOS FINALES
La rápida expansión de NILM y el desarrollo de diferentes algoritmos, han hecho que sea esencial proporcionar una evaluación de rendimiento mediante el uso de métricas de desempeño. Las métricas de evaluación, comparan los resultados de la desagregaciónn (predicciones) de los modelos entrenados con los datos del set de validación (mediciones reales de cada proceso). NILMTK cuenta con el cálculo de métricas de evaluación mediante el uso del MeterGroup para la validación de los resultados mediante el set de validación Vamos ahora analizar en nuestro dataset diferentes metricas como son FEAC,F1, EAE ,MNEAP y RMSE que resumimos a continuacion en el siguinte cuadro

![image](https://user-images.githubusercontent.com/75988158/231511728-d7aea751-23a0-48f6-95bf-61a0007d7055.png)



Para que sirva de referencia, se muestran  los resultados de aplicar las metricas para los ficheros originales sin el offset de 2+2  y que presentamos en el respositorio https://github.com/crn565/ozm10_appliances_transitorios
![image](https://user-images.githubusercontent.com/75988158/231507441-839c8421-3e21-40b2-b0ba-8ff544f40600.png)

Y  estos son los resultados de las metricas para el algoritmo CO, tiempo de muestreo 60"  y metodo  first para los nuevos datos:
![image](https://user-images.githubusercontent.com/75988158/231506558-cf2e440a-b937-4b5b-8372-25a59be04fb7.png)

Como se puede apreciar,  a pesar de que el tiempo de las muestras se ha multiplicado por tres, los resultados de las metricas lejos de mejorar empeoran en casi todos los casos ( sobre todo con F1) , lo que demuestra que en realidad para mejorar un modelo no sólo se necesitan mas medidas, sino que tambien estas sean diferentes y lo mas variadas posibles . 

## RESUMEN

Las conclusiones obtenidas pues con este experimento es que resumidamente al repicar las medidas NO mejoran las metricas de NILMTK  con los algoritmos CO y FHMM , asi como tampoco mejoran las predicciones. 

- La precisión de los modelos en identificar los patrones de consumo de energía de los electrodomésticos individuales es baja, lo que se refleja en un bajo valor de F1.

- Los modelos son buenos para estimar la cantidad total de energía consumida en el hogar, como lo indican los buenos valores de EAE y MNEAP.

- A pesar de que los modelos son capaces de identificar diferentes patrones de consumo de energía en el hogar,sus capacidades para predecir la cantidad exacta de energía consumida por los electrodomésticos individuales es baja, lo que se refleja en un alto valor de RMSE.


Ademas, computacionalemente para ejecutar el algoritmo FHMM  se requiere mas de 32GB de RAM para procesar las medidas.  
