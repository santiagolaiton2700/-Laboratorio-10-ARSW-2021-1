### Escuela Colombiana de Ingeniería
### Arquitecturas de Software - ARSW

## Escalamiento en Azure con Maquinas Virtuales, Sacale Sets y Service Plans

### Dependencias
* Cree una cuenta gratuita dentro de Azure. Para hacerlo puede guiarse de esta [documentación](https://azure.microsoft.com/en-us/free/search/?&ef_id=Cj0KCQiA2ITuBRDkARIsAMK9Q7MuvuTqIfK15LWfaM7bLL_QsBbC5XhJJezUbcfx-qAnfPjH568chTMaAkAsEALw_wcB:G:s&OCID=AID2000068_SEM_alOkB9ZE&MarinID=alOkB9ZE_368060503322_%2Bazure_b_c__79187603991_kwd-23159435208&lnkd=Google_Azure_Brand&dclid=CjgKEAiA2ITuBRDchty8lqPlzS4SJAC3x4k1mAxU7XNhWdOSESfffUnMNjLWcAIuikQnj3C4U8xRG_D_BwE). Al hacerlo usted contará con $200 USD para gastar durante 1 mes.

### Parte 0 - Entendiendo el escenario de calidad

Adjunto a este laboratorio usted podrá encontrar una aplicación totalmente desarrollada que tiene como objetivo calcular el enésimo valor de la secuencia de Fibonnaci.

**Escalabilidad**
Cuando un conjunto de usuarios consulta un enésimo número (superior a 1000000) de la secuencia de Fibonacci de forma concurrente y el sistema se encuentra bajo condiciones normales de operación, todas las peticiones deben ser respondidas y el consumo de CPU del sistema no puede superar el 70%.

### Escalabilidad Serverless (Functions)

1. Cree una Function App tal cual como se muestra en las  imagenes.

![](images/part3/part3-function-config.png)

![](images/part3/part3-function-configii.png)

2. Instale la extensión de **Azure Functions** para Visual Studio Code.

![](images/part3/part3-install-extension.png)

3. Despliegue la Function de Fibonacci a Azure usando Visual Studio Code. La primera vez que lo haga se le va a pedir autenticarse, siga las instrucciones.

![](images/part3/part3-deploy-function-1.png)

![](images/part3/part3-deploy-function-2.png)

4. Dirijase al portal de Azure y pruebe la function.

![](images/part3/part3-test-function.png)

5. Modifique la coleción de POSTMAN con NEWMAN de tal forma que pueda enviar 10 peticiones concurrentes. Verifique los resultados y presente un informe.

6. Cree una nueva Function que resuleva el problema de Fibonacci pero esta vez utilice un enfoque recursivo con memoization. Pruebe la función varias veces, después no haga nada por al menos 5 minutos. Pruebe la función de nuevo con los valores anteriores. ¿Cuál es el comportamiento?.

**Preguntas**

* ¿Qué es un Azure Function?
  - Es una solución la cual permite ejecutar de forma sencilla pequeños codigos lo cual facilita tener una aplicación en la nube sin preocuparse de la infrastructura. Una de las mejores caracteristicas de esto es que podemos codificar en el portal de Azure esto nos ayuda a que si no tenemos buenos dispositivos (HARDWARE) podemos desarrollar aplicaciones sin ninguna limitación. Estas peticiones se pagan de acuerdo por el consumo, esto quiere decir que se factura por el numero de peticiones ejecutadas.  
* ¿Qué es serverless?
  - Este es el tipo de arquitectura que no utiliza servidores físicos, pero la responsabilidad de implementar el código recae en el proveedor de la nube que es responsable de distribuir los recursos. Esto generalmente funciona con contenedores de baja densidad, que pueden ser una función http u otra función.
* ¿Qué es el runtime y que implica seleccionarlo al momento de crear el Function App?
  - Es un intervalo de tiempo de ejecución en la cual el programa se ejecuta. En Azure esta relacionado con la versión del .NET, Nodejs, Python o java, en la que se basa el tiempo de ejecución. En este caso la versión de runtime es de 12 lo cual implica que el timeout sería de 5 minutos y además nuestra memoria se limpiara en este intervalo de tiempo.
* ¿Por qué es necesario crear un Storage Account de la mano de un Function App?
  - Para que algunas apliaciones pueden implementar cache y mejorar el rendimiento de nuestras aplicaciones.
* ¿Cuáles son los tipos de planes para un Function App?, ¿En qué se diferencias?, mencione ventajas y desventajas de cada uno de ellos.
  - Consumption plan Ofrece escalabilidad dinámica y factura solo cuando la aplicación es ejecutada, tiene un timeout es de 5 minutos y brinda una memoria máxima de 1.5 GB por instancia, un almacenamiento de 1 GB y un máximo número de instancias de 200.
* ¿Por qué la memoization falla o no funciona de forma correcta?
  - Debido a que el plan que utilizamos nos ofrece 1.5G las cuales en algunos casos esta memoria pude llegar a quedar corto con peticiones en las cuales tengamos que realizar muchos cálculos.
* ¿Cómo funciona el sistema de facturación de las Function App?
  - El consumo de recursos se calcula multiplicando la magnitud medio de memoria en GB por la era en milisegundos que tiesa la ejecución de la funcionalidad. La memoria que una funcionalidad usa se mide redondeando a los 128 MB más cercanos hasta un tamaño de memoria mayor de 1.536 MB, y la época de ejecución se redondea a los 1 ms más cercanos. Para la ejecución de una exclusiva funcionalidad, la era de ejecución mínimo es de 100 ms y la memoria mínima es de 128 MB, respectivamente.


### AUTORES

- WEISNNER RODRIGUEZ JAMES ALLAN
- LAITON CUBIDES SANTIAGO AGUSTIN