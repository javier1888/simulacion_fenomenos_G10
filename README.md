# Descripcion del Proyecto
Este proyecto busca modelar numericamente el secado por medio de un horno convectivo de la macroalga Ulva Stenophylloides, siendo esta la principal responsable de las mareas verdes que ocurren en la bahia de Algarrobo, Chile. Para ellos se realiza un modelo 1-D no estacionario de difusión de humedad mediante el uso de la segunda ley de Difusion de Fick.

La problematica principal que afronta este proyecto es el exceso de biomasa del alga Ulva Stenophylloides que es la responsable de las mareas verdes que ocurren en la bahia de Algarrobo, Chile. Esta acumulación en las playas genera un gran impacto ambiental pudiendo causar hipoxia como tambien limitar el paso de la luz solar, provocando la muerte de animales y plantas del ecosistema marino local. Ademas esta situación genera impactos socioeconomicos relevantes, la presencia en abundancia de esta alga a provocado malos olores y problemas de higiene en las costas logrando el cierre de las playas, perjudicando el turismo local y a los comericiantes.

En el contexto chileno, este tipo de mareas verdes se ha identificado como un desafío para la gestión costera y la economía local. Estudiar el secado convectivo del alga permitiría avanzar hacia su valorización como materia prima para alimentos, bioproductos o bioenergía. Todo esto se relaciona con los desafíos de sustentabilidad y economía circular del país, al transformar una biomasa que genera problemas en un recurso aprovechable. Por lo tanto el proyecto contribuiría en la disminución del impacto ambiental en Algarrobo, como tambien se estaría buscando un aprovechamiento sustentable de la Ulva Stenophylloides

# Explicacion Modelo
El sistema modela una cama de algas Ulva stenophylloides que se encuentran sobre una bandeja dentro de un horno convectivo a una temperatura constante de 50°C y 120° C. Para el modelado la cama se le asumirá una geometría con forma de placa horizontal con un espesor de 2mm. El contenido de humedad solo variará con respecto al grosor (eje z) y el tiempo. Se considerará como z=0 el centro del alga, y la transferencia será unidireccional, solo hacia el eje z positivo, ya que se asume que la bandeja es impermeable. 

<img width="702" height="169" alt="image" src="https://github.com/user-attachments/assets/143af2f6-d902-4917-9629-9a54074f3eab" />


Como se menciona anteriormente el fenomeno de transporte utilizado es el de transferencia de masa, en concreto la difusión de húmedad y descrita por la segunda ley de Fick. Los supuestos principales son un dominio 1D con forma de placa horizontal con simetría en el plano medio, proceso isotérmico (la temperatura del alga es uniforme e igual a la del aire de secado), propiedades del aire constantes y flujo homogéneo, como tambein la difusividad de humedad se considera independiente del contenido de agua, osea constante y la densidad del alga seca constante tambien.

<img width="573" height="325" alt="image" src="https://github.com/user-attachments/assets/49fc9702-f728-4fb2-9305-af48aa59f2d7" />

Se considera una condicion incial que sería la humedad incial que posee el alga X(z,t=0) = Xo. La primera condicion de borde es del tipo Neumann en z=0, en donde no hay humedad en el plano central debido a simetria del secado, dX/dz|z=0 = 0. La segunda condicion de borde es del tipo Robin (convectiva) en z= L/2, en donde en la interface el flujo difusivo interno es igual al flujo convectivo de la sueprficie, Deff = dX/dz|z=L/2 = -km(C_aire-C_L/2).

# Descripción metodo númerico

La implementación numérica del modelo se basa en el método de diferencias finitas (FTCS) aplicado a la ecuación de difusión de Fick en 1D. El dominio espacial corresponde al espesor efectivo de la cama de algas, que se discretiza en N+1 nodos igualmente espaciados con paso ∆z, desde el plano de simetria en z=0 hasta la superficie que está en contacto con el aire en z=L/2. Para el dominio del tiempo se utiliza un paso ∆t, y dado que el metodo de Euler explicito (FTCS) no es completamente estable, se ocupó la condicion de estabilidad de Von Neumann para garantizar que la solución numerica no diverja r=Deff*Δt/(Δz)^2, y se utiliza un Δt que haga que el valor de r (numero de Fourier) sea menor o igual a 0.5.

Se parte de la ecuación de difusión en 1D con Deff constante y se aproxima la derivada temporal con un esquema hacia adelante en el tiempo y la derivada espacial de segundo orden con diferencias centrales para un nodo interior cualquiera i, con 2 ≤ i ≤ N, obteniendo la siguiente ecuación discretizada

<img width="244" height="58" alt="image" src="https://github.com/user-attachments/assets/dec74e54-472f-4b0e-afa7-7a0d80e56543" />

Las condiciones de borde se discretizan considerando una malla de N + 1 nodos. Para la condicion de borde 1, en el plano de simetría se impone una condición de flujo nulo, es decir, ∂X∂z∣z=0 = 0, la cual se aproxima numéricamente imponiendo la relación Xt0 = Xt2.

<img width="360" height="63" alt="image" src="https://github.com/user-attachments/assets/b19bdb04-a518-41d2-9ecd-28ab73a5c575" />

Para la condicion de borde 2, la interfaz se impone la condición de flujo convectivo y se utiliza el balance de flujo para obtener la ecuación discretizada. Sustituyendo el flujo de borde (FN +1/2 = −km(Caire − Ce)) y el flujo interno (FN −1/2 ≈ D XtN +1−XtN∆z ) en el lado derecho, se obtiene la siguiente ecuacion discretizada:

<img width="361" height="56" alt="image" src="https://github.com/user-attachments/assets/01338745-ce63-4f6e-b529-aa0ab063ec6a" />

Finalmente para la condición inicial del problema se establece considerando una distribución uniforme de humedad en todo el dominio al tiempo inicial t = 0:

<img width="258" height="42" alt="image" src="https://github.com/user-attachments/assets/5bf50888-46d3-42a7-a310-716bd0dbd530" />

Este metodo numerico es adecuado para nuestro fenomeno estudiado porque se modela con una EDP lineal unidimensional , usando coeficientes constante en la ecuacion como lo son Deff y ρ, y la geometria es una placa horizontal relativamente, lo que nos ayuda a poder representar el dominio del sistema como una grilla con una cantidad de nodos finitos, en donde se pueden obtener grillas uniformes y la distancia entre cada nodo se mantiene constante en toda la grilla. Ademas facilita la idea de que en los extremos de la grilla se plantean las condiciones de borde. Tambien las condiciones de borde utilizadas en el modelo cumplen con las condiciones de borde que funcionan en el metodo de diferencias finitas como lo son las de Neumann, Dirichlet y Robin. Ademas este esquema explícito es computacionalmente es sencillo de implementar, siendo mas adecuado para el tipo de análisis presentado en el proyecto.


#Instrucciones para ejecutar el código 

Se importan los módulos necesarios para el cálculo númerico y la visualización.

import numpy as np
import matplotlib.pyplot as plt
from matplotlib import cm
from scipy.special import erf, erfc

Definir los parámetros materiales, convectivos y las condiciones de operación del horno:
- Párametros Materiales: Deff (Difusividad Efectiva), ρs (Densidad del sólido seco), X0 (Humedad
inicial).
- Parámetros Convectivos: km (Coeficiente de transferencia de masa), Caire (Concentración de humedad en el aire).
- Dimensiones: L/2 (Mitad del espesor del alga, para el dominio de simetría).

Se calcula la concentración de humedad de equilibrio (Ce) en la interfase alga-aire, esencial para
la Condición de Borde de Robin. Esto requiere el cálculo de la presi´on de vapor saturada (Pvs) a la
temperatura de secado T:
Ce = awPvs(TL/2)/(RvTL/2)

Se establece la malla y el paso temporal ∆t, garantizando la estabilidad del esquema explícito.
a) Malla Espacial (∆z): Definir el n´umero de nodos (N) y el espaciamiento: ∆z = (L/2)/(N − 1).

b) Cálculo de ∆t (Condición de Estabilidad): El paso de tiempo debe cumplir la condición de
von Neumann (Número de Fourier λ ≤ 0,5):
∆t ≤ 0,5 · ∆z2 Deff, max
Se utiliza el Deff, max para asegurar la estabilidad durante toda la simulación.

c) Inicialización: Crear el vector de humedad inicial X (tamaño N), con todos los nodos inicializados
a X0.

El modelo se implementa en notación matricial.
a) Matriz de Difusión (A): Construir la matriz tridiagonal que incorpora los coeficientes de difusi´on.
Se ajustan las filas para implementar la condici´on de simetría en el nodo inicial (z = 0) y la parte
difusiva de la condición de Robin en el nodo final (z = L/2).
b) Vector Convectivo (b): El vector b maneja la parte no homogénea de la convección superficial,
siendo distinto de cero únicamente en el último nodo (N), utilizando el t´ermino km(Caire − Ce).

Se realiza la iteración para la evolución del perfil de humedad utilizando la relación explícita de Euler:
- Iniciar el bucle de tiempo hasta alcanzar la duración deseada o la humedad final.
- Aplicar la ecuaci´on de evolución en cada paso: Xnew = Xold + (AXold + b) · ∆t
- Almacenar el perfil Xnew en la matriz histórica (Xnum).

Los resultados se presentan mediante gráficos de línea y mapas de calor.
- Perfiles de Concentración: Graficar X vs. z para distintos instantes de tiempo t.
- Mapa de Calor: Utilizar matplotlib.pyplot.pcolormesh con la matriz de resultados transpuesta (X⊤
num) para visualizar la evolución del contenido de humedad en funci´on del tiempo y la posición.



#Graficos

En los cuatro siguientes graficos se muestra como va disminuyendo la cantida de humedad a lo largo del espesor del alga (2mm), midiendose a distintos periodos de tiempo hasta un tiempo  maximo de 8 horas

<img width="530" height="402" alt="image" src="https://github.com/user-attachments/assets/a092d898-8a64-493a-8c5f-3bde4568f569" /> 

Figura 1.  
Este gráfico se encuentra en la carpeta de Resultados Graficos con el nombre de "Secado Convectivo 50°C Grafico 1"

<img width="777" height="589" alt="image" src="https://github.com/user-attachments/assets/151ead74-d93f-4693-bc9c-48273eedb767" />

Figura 2.  
Este gráfico se encuentra en la carpeta de Resultados Graficos con el nombre de "Secado Convectivo 50°C Grafico 2"

El perfil de cantidad de humedad para este caso se puede apreciar que al pasar las 8 horas no se logra una variacion significativa de la humedad dentro de alga, se visualiza una disminucion maxima de 0.92 a 0.86 viendose limitada y no muy funcional el modelo. Se ve que mantiene cantidad de humedad cercanos a la inicial durante gran parte del tiempo y existe una leve disminucion cerca de la superficie. 


<img width="534" height="406" alt="image" src="https://github.com/user-attachments/assets/4162de71-8754-4e0d-bd48-e2fd77d3c75c" />

Figura 3.  
Este gráfico se encuentra en la carpeta de Resultados Graficos con el nombre de "Secado Convectivo 120°C Gráfico 1"

<img width="761" height="587" alt="image" src="https://github.com/user-attachments/assets/f18171bd-e985-4060-9bf8-0b81a538e19c" />

Figura 4. 
Este gráfico se encuentra en la carpeta de Resultados Graficos con el nombre de "Secado Convectivo 120°C Gráfico 2"


Al observar ambos graficos ya muestran una mejora en el secado del alga, en donde se observa que la cantidad de humedad al pasar las 8 horas disminuye significativamente, quedando menos de un 0.1 kg agua/kg solido seco, estando practicamente seco. La humedad desciende gradualmente a medida que nos acercamos a la superficie, lo cual ocurre a una tasa muy baja. Por lo tanto el modelo nos indica que al aumentar la temperatura a la que se trabaja con el horno convectivo el alga logra deshidratarse de mejor manera. 










