# Predicción de Luminosidad Estelar

Este proyecto realiza una predicción de la luminosidad estelar a partir de la masa estelar.

Haz clic aquí para ver la [visualización interactiva](https://rpubs.com/Arcano97/Box-Cox-Luminosidad-Masa-Estelar).

# Teoría

El estudio de la luminosidad estelar es fundamental para la Astrofísica y Cosmología en general. Se trata de un parámetro que en primera instancia está relacionado con la clasificación y evolución estelar, presente dentro del diagrama de Hertzprung-Russell (HR), gráfico ampliamente popular para visualizar de manera sencilla la distribución espectral y fase evolutiva de las estrellas, el cual podemos ver a continuación.

![image](https://github.com/user-attachments/assets/ed06224b-8cde-4bcd-9b6c-798b682cdf22)

Este gráfico organiza a las estrellas según dos de sus propiedades principales:

* Luminosidad: qué tan brillante es una estrella (eje vertical)
* Temperatura superficial: qué tan caliente es una estrella (eje horizontal)

Sobre el eje horizontal, podemos ver a las estrellas más calientes del lado izquierdo del gráfico, y a las más frías en el extremo derecho. Sobre el eje verticual, arriba tenemos a las estrellas más brillantes, y debajo a las menos brillantes. 

La seucencia prinicipal, una banda señalada con el mismo nombre, atraviesa el gráfico desde la esquina superior izquierda (estrellas calientes y muy brillantes) hasta la esquina inferior derecha (estrellas frías y menos brillantes). Sobre esta secuencia están la mayoría de las estrellas, incluyendo al Sol.

Las estrellas de la secuencia principal están, en principio, quemando hidrógeno en sus núcleos. Las gigantes y supergigantes están en la parte superior del gráfico, y son estrellas frías, pero extremadamente brillantes por su tamaño. Por otro lado, las enanas blancas están en la parte inferior izquierda. Se trata de estrellas pequeñas, pero muy calientes y poco luminosas por su tamaño. 

Es a través de la luminosidad que podemos asociar ciertas propiedades físicas interesantes, como calcular el radio y la temperatura efectiva de las estrellas mediante las relación $L \approx R^2 T^{4}_{eff}$, expresión derivada de la ley de Stefan-Bolztmann. De igual forma, la luminosidad puede complementar estudios espectroscópicos para interpretar la composición química de las estrellas y su lugar dentro de las poblaciones estelares.

En este trabajo, se estudia la relación de dependencia entre la luminosidad y la masa estelar. Para ello, implementamos un modelo predictivo que utiliza la temperatura efectiva, denominada como $T_{eff}$, para estimar la masa estelar. Posteriormente, se predice la luminosidad basándonos en la relación masa-luminosidad, que es fundamental para estrellas de la secuencia principal. 

En la secuencia principal, las estrellas mantienen una relación que aproxima sus luminosidades y masas al compararlas con las del Sol, i.e. la masa solar $M_{\odot}$ y la luminosidad solar $L_{\odot}$. De ese modo, se pueden normalizar las relaciones estudiadas, para validar que las estrellas analizada pertenecen a la secuencia principal. Es importante mencionar que esta relación no se mantiene para estrellas fuera de la secuencia principal, como gigantes rojas o enanas blancas. Sin mencionar que factores como la metalicidad y la edad de la estrella pueden modificar la luminosidad relativa para una masa dada.

Antes de continuar, es importante destacar qué datos utilizamos. Para la descarga de nuestro dataset, recurrimos al Sloan Digital Sky Survey (SDSS). Esta base de datos tiene como objetivo principal mapear una amplia proción del cielo, y estudiar los objetos astronómicos contenidos en el mismo. El proyecto inició en el año 2000, y desde entonces el SDSS ha contribuido al avance del conocimiento en diversas áreas de la astronomía y astrofísica. Entre los datos que podemos encontrar dentro están imágenes, espectros y datos tabulados respecto a la temperatura de estrellas, filtros de observación, coordenadas estelares, etc. 

Para los fines de este proyecto, nos quedamos con la temperatura de estrellas contenidas en la secuencia principal definida, como antes mencionamos, como $T_{eff}$. Con ello, pudimos acceder a cálculos para obtener masa estelar y luminosidad. 

Ahora bien, dado que la relación entre masa estelar y luminosidad no es lineal en el espacio original, se aplicó una transformación Box-Cox para mejorar la linealidad y garantizar la homogeneidad de varianza (corrección de heterocedasticidad). Esto permitió cumplir con lo necesario para ajustar un modelo de regresión lineal robusto. 

Incluimos la validación de nuestro proyecto utilizando datos distintos al conjunto de entrenamiento para evaluar métricas de ajuste como el coeficiente de determinación $R^2$, y el error cuadrático medio $MSE$.



