# Descripcion del Proyecto
Este proyecto busca modelar numericamente el secado por medio de un horno convectivo de la macroalga Ulva Stenophylloides, siendo esta la principal responsable de las mareas verdes que ocurren en la bahia de Algarrobo, Chile. Para ellos se realiza un modelo 1-D no estacionario de difusión de humedad mediante el uso de la segunda ley de Difusion de Fick.

La problematica principal que afronta este proyecto es el exceso de biomasa del alga Ulva Stenophylloides que es la responsable de las mareas verdes que ocurren en la bahia de Algarrobo, Chile. Esta acumulación en las playas genera un gran impacto ambiental pudiendo causar hipoxia como tambien limitar el paso de la luz solar, provocando la muerte de animales y plantas del ecosistema marino local. Ademas esta situación genera impactos socioeconomicos relevantes, la presencia en abundancia de esta alga a provocado malos olores y problemas de higiene en las costas logrando el cierre de las playas, perjudicando el turismo local y a los comericiantes.

En el contexto chileno, este tipo de mareas verdes se ha identificado como un desafío para la gestión costera y la economía local. Estudiar el secado convectivo del alga permitiría avanzar hacia su valorización como materia prima para alimentos, bioproductos o bioenergía. Todo esto se relaciona con los desafíos de sustentabilidad y economía circular del país, al transformar una biomasa que genera problemas en un recurso aprovechable. Por lo tanto el proyecto contribuiría en la disminución del impacto ambiental en Algarrobo, como tambien se estaría buscando un aprovechamiento sustentable de la Ulva Stenophylloides

# Explicacion Modelo
El sistema modela una cama de algas Ulva stenophylloides que se encuentran sobre una bandeja dentro de un horno convectivo a una temperatura constante de 50°C y 120° C. Para el modelado la cama se le asumirá una geometría con forma de placa horizontal con un espesor de 2mm. El contenido de humedad solo variará con respecto al grosor (eje z) y el tiempo. Se considerará como z=0 el centro del alga, y la transferencia será unidireccional, solo hacia el eje z positivo, ya que se asume que la bandeja es impermeable. 

<img width="702" height="169" alt="image" src="https://github.com/user-attachments/assets/143af2f6-d902-4917-9629-9a54074f3eab" />



Como se menciona anteriormente el fenomeno de transporte utilizado es el de transfernecia de masa, en concreto la difusion de humedad y descrita por la segunda ley de Fick

