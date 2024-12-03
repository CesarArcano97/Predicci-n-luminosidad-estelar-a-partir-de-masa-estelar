# Predicción-luminosidad-estelar-a-partir-de-masa-estelar
Aplicación de transformación Box-Cox para la predicción de Luminosidad Estelar a partir de la Masa Estelar

Implementación de la Transformación Box-Cox
La Transformación Box-Cox es una técnica utilizada para abordar problemas de heterocedasticidad y desviación de la normalidad en los datos. Este README describe los pasos clave para implementarla correctamente.

Propósito de la Transformación Box-Cox
El objetivo principal de la Transformación Box-Cox es:

Reducir la heterocedasticidad: Garantizar que la varianza de los errores sea constante en todas las observaciones.
Ajustar los datos a la normalidad: Cumplir con los supuestos fundamentales de métodos estadísticos como regresión lineal y análisis de varianza.
Preparación de los Datos
Antes de aplicar la transformación:

Asegúrate de que los datos sean positivos:
La transformación solo es aplicable a valores mayores que cero.
Si hay ceros o valores negativos, suma una constante positiva a los datos.
Identifica la variable objetivo:
Generalmente, se aplica a la variable dependiente o respuesta ($y$).
Divide los datos por subpoblaciones (si es necesario):
Aplica la transformación por separado a cada subgrupo.
