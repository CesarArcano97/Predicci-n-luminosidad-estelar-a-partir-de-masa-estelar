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

![image](https://github.com/user-attachments/assets/2534ae4a-1d4b-4e5b-bbe1-0050e649232d)

Incluimos la validación de nuestro proyecto utilizando datos distintos al conjunto de entrenamiento para evaluar métricas de ajuste como el coeficiente de determinación $R^2$, y el error cuadrático medio $MSE$.

Adicionalmente, el análisis revela que las distribuciones de masa estelar y luminosidad no son normales en el espacio original, presentando un sesgo hacia la derecha y alta varianza. Estas características justificaron el uso de la transformación Box-Cox, que permitió obtener distribuciones más simétricas y mejor adaptadas al modelo lineal. 

# Resultados

Las distribuciones de la masa estelar y la luminosidad presentan sesgo hacia la derecha. Este sesgo indica que ambas distribuciones están concentradas en valores bajos, pero con una cola extendida hacia valores mayores, lo que deja entrever que no son normales. Esto es un comportamiento bastante esperado pues, en astronomía y astrofísica, la mayoría de las estrellas tienen masas y luminosidades relativamente bajas (como enanas rojas), mientras que pocas poseen valores significativamente mayores, como las supermasivas. 

Para abordar estas características y cumplir con los supuestos necesarios para aplicar regresión lineal, como la normalidad de los residuos o la homocedasticidad, se utilizó la transformación Box-Cox. Las lambdas óptimas fueron:

* Lambda óptimo para masa estelar: $\lambda_{ME} = -0.8$
* Lambda óptimo para luminosidad: $\lambda_{\ell} = -0.2$

Asimismo, en la siguiente figura, podemos ver cómo esta transformación logra reducir el sesgo a la derecha y aproximar la simetría en cada distribución. 

![image](https://github.com/user-attachments/assets/8fb7e815-e2e4-492d-84cd-56d096c11814)

De color azul podemos apreciar la distribución de la masa estelar tal como viene en los datos reales, mientras que la roja representa la distribución al realizar Box-Cox. Por otra parte, la distribución de luminosidad verde representa a la original de nuestros datos, mientras que la morada representa a la transformada.

En cuanto a la regresión lineal, Box-Cox devolvió una regresión claramente lineal, demostrando así cómo la transformada realizar el ajuste necesario para la linealidad. 

![image](https://github.com/user-attachments/assets/a842f4a9-5c3f-406c-970e-510385771623)

Además, encontramos un $R^2$ de 0.99701 puntos y un $MSE$ de 0.06319 puntos. En comparación con lo obtenido previo a la transformación Box-Cox, se trata de una mejora significativa, pues regresando a la figura 4.2, antes de Box-Cox encontramos un $R^2 = 0.85865$ y un $MSE = 4.25942$. 

Recordemos que el $R^2$ (Coeficiente de determinación), es una métrica que mide qué tan bien el modelo explica la variabilidad de los datos observados. Valores cercanos al 1 indicaría que el modelo explica bien los datos, mientras que valores cercanos a 0 indicarían que el modelo no los puede explicar. La ecuación que la describe es:

$$
R^2 = 1 - \frac{Suma de Residuos al Cuadrado}{Suma Total al Cuadrado}
$$

Finalmente, para validar nuestro modelo de regresión lineal ajustado con Box-Cox, utilizamos un conjunto de datos nuevo para predecir sus luminosidades. El resultado gráfico demuestra una alta concordancia entre las luminosidades calculadas con las ecuaciones y las predichas, especialmente para valores bajos y medios. Esto se observa al seguir la línea de predicción con los puntos calculados. 

![image](https://github.com/user-attachments/assets/3fad77f2-ab7e-4a59-b736-e953601721ad)

Sin embargo, en valores de luminosidad altos, por encima de los 60 puntos, se puede observar subestimación en las predicciones, ya que los puntos se desvían por debajo de la línea. Esto puede tener dos razones: la primera es que las estrellas con alta luminosidad suelen ser menos frecuentes y podrían estar siendo poco representadas por el modelo. Asimismo, aunque Box-Cox linealiza la relación en buena medida, no se está capturando a la perfección todas las características de estrellas más masivas. 

Haciendo la recapitulación de todo, podemos decir que nuestra transformación Box-Cox fue suficientemente efectiva. 





