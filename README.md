# Descripcion del Proyecto
Este proyecto busca modelar numericamente el secado por medio de un horno convectivo de la macroalga Ulva Stenophylloides, siendo esta la principal responsable de las mareas verdes que ocurren en la bahia de Algarrobo, Chile. Para ellos se realiza un modelo 1-D no estacionario de difusión de humedad mediante el uso de la segunda ley de Difusion de Fick.

La problematica principal que afronta este proyecto es el exceso de biomasa del alga Ulva Stenophylloides que es la responsable de las mareas verdes que ocurren en la bahia de Algarrobo, Chile. Esta acumulación en las playas genera un gran impacto ambiental pudiendo causar hipoxia como tambien limitar el paso de la luz solar, provocando la muerte de animales y plantas del ecosistema marino local. Ademas esta situación genera impactos socioeconomicos relevantes, la presencia en abundancia de esta alga a provocado malos olores y problemas de higiene en las costas logrando el cierre de las playas, perjudicando el turismo local y a los comericiantes.

En el contexto chileno, este tipo de mareas verdes se ha identificado como un desafío para la gestión costera y la economía local. Estudiar el secado convectivo del alga permitiría avanzar hacia su valorización como materia prima para alimentos, bioproductos o bioenergía. Todo esto se relaciona con los desafíos de sustentabilidad y economía circular del país, al transformar una biomasa que genera problemas en un recurso aprovechable. Por lo tanto el proyecto contribuiría en la disminución del impacto ambiental en Algarrobo, como tambien se estaría buscando un aprovechamiento sustentable de la Ulva Stenophylloides

# Explicacion Modelo
El sistema modela una cama de algas Ulva stenophylloides que se encuentran sobre una bandeja dentro de un horno convectivo a una temperatura constante de 50°C y 120° C. Para el modelado la cama se le asumirá una geometría con forma de placa horizontal con un espesor de 2mm. El contenido de humedad solo variará con respecto al grosor (eje z) y el tiempo. Se considerará como z=0 el centro del alga, y la transferencia será unidireccional, solo hacia el eje z positivo, ya que se asume que la bandeja es impermeable. 

<img width="702" height="169" alt="image" src="https://github.com/user-attachments/assets/143af2f6-d902-4917-9629-9a54074f3eab" />



Como se menciona anteriormente el fenomeno de transporte utilizado es el de transfernecia de masa, en concreto la difusion de humedad y descrita por la segunda ley de Fick. Se considera una condicion incial que sería la humedad incial que posee el alga X(z,t=0) = Xo. La primera condicion de borde es del tipo Neumann en z=0, en donde no hay humedad en el plano central debido a simetria del secado, dX/dz|z=0 = 0. La segunda condicion de borde es del tipo Robin (convectiva) en z= L/2, en donde en la interface el flujo difusivo interno es igual al flujo convectivo de la sueprficie, Deff = dX/dz|z=L/2 = -km(C_aire-C_L/2).

Los supuestos principales son un dominio 1D con forma de placa placa con simetría en el plano medio, proceso isotérmico (la temperatura del alga es uniforme e igual a la del aire de secado), propiedades del aire constantes y flujo homogéneo, como tambein la difusividad de humedad se considera independiente del contenido de agua, osea constante y la densidad del alga seca constante tambien.
<img width="573" height="325" alt="image" src="https://github.com/user-attachments/assets/49fc9702-f728-4fb2-9305-af48aa59f2d7" />




