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

CO_mean	CO_median	CO_first
1s	4.06	3.75	3.75
10s	2.45	2.98	2.25
30s	2.10	2.07	2.11
60s	2.05	3.31	2.30
5min	2.02	1.84	1.85
10min	1.90	1.78	1.80
15min	1.83	1.87	2.04
30min	2.09	2.14	2.38

Para el algoritmo FHMM se obtienen estos resultados



      FHMM_mean	  FHMM_median	FHMM_first
5min	25.83	  2.78	        2.18
10min	2.37	  2.12	        2.10
15min	2.06	  2.07	        2.07


En resumen  estos son los resultados de las metricas para el algoritmo CO, tiempo de muestreo 60"  y metodo  first:

	  Electric furnace	Microwave	Television	Kettle	Vacuum cleaner	Electric space heater	Electric shower heater	Fan	Fridge	Freezer
F1	0.129	            0.400	     0.519	     0.061	0.424	          0.222	                0.333	                 0.574	0.455	  0.400
EAE	0.003	            0.077	     0.003	     0.050	0.025         	0.192                	0.005	                 0.002	0.061	  0.089
MNEAP	1.808         	1.487	     0.847	     2.292	1.309	          1.059	                1.400	                 0.680	2.987	  5.608
RMSE	877.262	        514.697	   23.137	    615.359	342.614       	994.239	             734.337	            19.083	153.247	 281.465


Las conclusiones obtenidas  son que resumidamente al repicar las medidas NO mejoran las metricas de NILMTK  con los algoritmos CO y FHMM , asi como tampoco mejoran las predicciones. Ademas, computacionalemente para ejecutar el algoritmo FHMM  se requiere mas de 32GB de RAM para procesar las medidas.  
