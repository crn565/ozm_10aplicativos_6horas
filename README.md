# ozm_10aplicativos_6horas  con transitorios

Medidas con 3 ozm  trifasicos conformando en total  10 aplicativos  mas el agregado, todo estos dureate 6 horas (2+2+2) 

Se realiza  en los cuadernos adjuntos a este repositorio el analisis de las medidas de 10 aplicativos incluyendo transitorios  hasta el orden 150 de tension, corriente y potencia. Las Medidas  se realizan con 3  OpenZMeter  Trifásicos  (cada uno con 4 canales de medida)  conformando asi en total  11 canales de medida  que se distribuyen en los 10 aplicativos, mas el agregado. Las medidas corresponden a W, VAR, VA,f, VLN,PF y A, mas los transititoros  hasta el orden 150 de W, V y A,   todas con un marca de tiempo (Timestamp) de 13 dígitos tipo UNIX Epox.

Las medidas se realizaron el 10 de Marzo de 2033  en el Laboratorio de Electrotecnia de la  Escuela de Ingenieria Industrial de la Universidad de Almeria.Las medidas reales fueron tomadas entre las 11:10 y las 13:12 lo que conforma 5818000 milisegundos ( ver cálculo mas abajo). Para conformar 6 horas se agrego un doble offset de  unas 2h para  crear un nuevo DS  compuesto por las medidas reales, las medidas reales +2h y las medidas reales +4h.

Para la adicion de dos offset a los ficheros de medida  se considero el siguinte cálculo:¶

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


## RESULTADOS


Para el algoritmo combinatorio se obtienen estos resultados


![image](https://user-images.githubusercontent.com/75988158/231506370-213a3780-0ef2-41eb-9542-5520cdeaa02a.png)

Para el algoritmo FHMM se obtienen estos resultados

![image](https://user-images.githubusercontent.com/75988158/231506191-cecb7ca8-4f8d-4410-8355-af264ff09280.png)





En resumen  estos son los resultados de las metricas para el algoritmo CO, tiempo de muestreo 60"  y metodo  first:

![image](https://user-images.githubusercontent.com/75988158/231506558-cf2e440a-b937-4b5b-8372-25a59be04fb7.png)


Las conclusiones obtenidas  son que resumidamente al repicar las medidas NO mejoran las metricas de NILMTK  con los algoritmos CO y FHMM , asi como tampoco mejoran las predicciones. Ademas, computacionalemente para ejecutar el algoritmo FHMM  se requiere mas de 32GB de RAM para procesar las medidas.  
