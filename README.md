# ozm_10aplicativos_6horas  con transitorios

Medidas con 3 ozm  trifasicos confromando en total  10 aplicativos  mas el agregado  , todo estos dureate 6 horas (2+2+2) 

Se realiza  en los cuadernos el analisis de las medidas de 10 aplicativos incluyendo transitorios  hasta el orden 150 de tension, corriente y potencia. Las Medidas  se realizan con 3  OpenZMeter  Trifásicos  (cada uno con 4 canales de medida)  conformando asi en total  11 canales de medida  que se distribuyen en 10 aplicativos, mas el agregado.

Las medidas corresponden a W, VAR, VA,f, VLN,PF y A, mas los transitioros  hasta el orden 150 de W, V y A,   todas con un marca de tiempo ( Timestamp) de 13 dígitos.

Las medidas se realizaron el 10 de Marzo de 2033  en el Laboratorio de Electrotecnia de la  Escuela de Ingenieria Industrial de la Universidad de Almeria.

Las medidas reales fueron tomadas entre las 11:10 y las 13:12. Se agrego un doble offset de  unas 2h para  crear un nuevo DS  compuesto por las medidas reales, las medidas reales +2h y las medidas reales +4h.

Las conclusiones obtenidas  son que resumidamente al repicar las medidas no mejoran las metricas de NILMTK  con los algoritmos CO y FHMM , asi como tampoco mejoran las predicciones. Ademas, computacionalemente para ejecutar el algoritmo FHMM  se requiere mas de 32GB de RAM para procesar las medidas.  
  
  
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

