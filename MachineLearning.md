
# Clase 1
## Usos de machine learning
- Texto natural
- Imagenes
- Recomendaciones
- Clasificación: spam, fraude, copyright, incumplimiento de normas de conducta

## Paradigma general

Machine learning es un programa que **aprende** a partir de **Experiencia(E)** con respecto a una **tarea T** y una medida de **rendimiento P**.

Optimizamos P para mejorar nuestro rendimiento sobre los datos que tenemos.

## Aspectos a tener cuidado
- Encontrar los features correctos para caracterizar el problema

## Códificación de features

| Provincia    | número | binario | one-hot |
| ------------ | ------ | ------- | ------- |
| Córdoba      | 0      | 0       | 10000   |
| Catamarca    | 1      | 01      | 010000  |
| ....         | -      | -       | -       |
| Buenos Aires | 5      | 0001    | 000001  |

Codificamos variables con vectores para evitar que se pueda relacionar el tamaño de los datos con los encodings con la variable a predecir de forma erronea. *Mi intuición me dice que se hacen así porque son ortogonales*

Otras variables pueden llegar a ser numéricas y de cuantificación, por lo que si es importante que el modelo pueda entrenarse con la posibilidad de relacionar el valor numérico con la función objetivo.

## Métrica de rendimiento
Hay métricas standard para cada tipo de problema que nos va a decir que tan buenas son las predicciones / resultados de nuestro modelo.

un ejemplo es la **raiz del error cuadrático medio**:

$$RMSE = \sqrt{\sum^{n}_{i=1} \frac{(\hat y_i - y_i)^2}{n}}$$
## Función de pérdida
Una métrica de rendimiento que nos permite ver si estamos mejorando o no en la tarea dada. No entiendo mucho la diferencia con lo anterior. En el caso visto en clase(predecir salarios) usaremos el **error cuadrático medio**

$$MSE = \sum^{n}_{i=1} \frac{(\hat y_i - y_i)^2}{n}$$

## Overfitting vs undefitting

### Overfitting
Usar un modelo muy complejo que se acerca demasiado a los datos de entrenamiento y termina teniendo mal desempeño.

### Underfitting
Usar un modelo demasido simple que no pueda acercarse lo suficiente a los datos de entrenamiento.

### Detección

Se compara la performance en el **conjunto de entrenamiento** y en el **conjunto de evaluación**.

| Conjunto      | Mal Rendimiento | Buen Rendimiento |
| ------------- | --------------- | ---------------- |
| Entrenamiento | underfitting    | overfitting      |
| Evaluación    | overfitting     | ok               |

### Evitar undefitting
Complejizar el modelo agregando features o usar un modelo más complejo(un modelo no lineal, una red neuronal, etc.)
## Evitar overfitting: 
### Eliminar features
Si eliminamos features, hacemos que el modelo se simimplifique y tenga una curva más regular.
### Regularización
Agregar una penalización adicional a la funció nde pérdida para limitar la complejidad del modelo y evitar el overfitting.
#### Regularización L1
Esta penaliza por el valor absoluto de los coeficientes, usando norma $l1$ del vector $\theta$
$$loss(\theta) = \sum^{n}_{i=1} \frac{(f_\theta(x_i) - y_i)^2}{n} + \lambda \sum^k_{i=0}|\theta_i|$$
#### Regularización L2

Esta trabaja en forma similar a la de arriba, pero esta usa la norma $l2$
$$loss(\theta) = \sum^{n}_{i=1} \frac{(f_\theta(x_i) - y_i)^2}{n} + \lambda \sum_{i=0}^k\theta_i^2$$
## Tipos de modelos
- Red neuronal
- Árbol de decisión
- Regresión logística
## Cosas random
- Los modelos que vemos son **modelos probabilístico**
- regresores != clasificadores
- Ley de Sif: siempre nos queda algo afuera cuando hacemos reglas lógicas

## Referencias
- Scikit-learn

# Clase 2

## Stochastic Gradient Descent

Lo que hacemos es calcular el gradiente de la función de pérdida con los parámetros actuales y luego **restar ese gradiente**. 

**Recordatorio:** El gradiente es el vector de derivadas parciales correspondientes a la misma coordenada en el vector de variables de la función:

$$\Delta f(x,y) = (\frac{\partial f}{\partial x}, \frac{\partial f}{\partial y})$$
- **El gradiente nos indica a donde ir si queremos que la función aumente**
- **Tenemos que ir en el sentido opuesto**

El algoritmo entonces hace:

$$\theta^{(t+1)} = \theta^{(t)} - \alpha \Delta loss(\theta^{(t)})$$
donde $\alpha$ es el *learning rate*.
$loss$ es una sumatoria en este caso(MSE) y cuando hacemos la derivada parcial en cada coordenada nos queda:

$$\theta^{(t+1)} = \theta^{(t)} - \alpha \sum^n_{i=0}(f_{\theta^{(t)}}(x_i)-y_i)x_i$$
**Nota:** hay un $2$ que debería queda dando vuelta si hacemos el gradiente, pasa que queda multiplicado por $\alpha$ y entonces no nos calienta, pero técnicamente estamos usando el $gradiente / 2$ multiplicado por $\alpha$.

### Learning rate

El learning rate dicta que tan grandes son los saltos que hacemos en cada iteración. Este parámetro deberá ser optimizado para mejorar la convergencia.
![[Pasted image 20230701123035.png]]

### Estandarización del input

Estandarizar cada feature a modo de variable normal estandar. De estar forma acercamos los valores a 0 y hacemos que su desviación estandar sea de 1.

**Problema: Vanishing Gradient** - al estar los datos muy pegados al 0, el gradiente tiende a 0 y nos movemos muy lento.

**Solución:** estandarizar alrededor del número 1, así la media es 1.

### Batching
Calcular el gradiente usando solo una porción aleatoria de los datos de entrenamiento. 
**Ventajas**:
- Eficiencia computacional
- Estabilidad del gradiente
- Mejora el impacto de la regularización
**Desventaja**: no es perfecto teóricamente y podríamos usar una porción no representativa del dataset en algún paso.

**Como implementar Batching:** tomamos un orden aleatorio del dataset y tomamos batches en ese orden.
**Tamaño del batch**: me tengo que asegurar de que entre en memoria, pero también me tengo que asegurar de que tenga un tamaño importante, para que los datos outliers sean promediados con otros más normales(esto es más bien específico a la función de pérdida que estamos usando, que tiene una media metida).

# Clase 3: Modelos no lineales

## MLP: Multi-Layer-Perceptron

tira el título y no menciona más nada xd

## Regresión logística
Este modelo es para predecir probabilidades, vamos a ver que usando este modelo basado en un modelo de regresión lineal(el que vimos la clase anterior), no vamos a poder predecir un XOR. Usando esta limitación como pie para hablar de modelos más complejos.

El modelo es:

$$h_{\theta}(x) = g(\theta^T x)$$
$$g(z) = \frac{1}{1+e^{-z}}$$

- Notar que estamos metiendo lo que antes era nuestro modelo de regresión lineal($\theta ^T x$) dentro de $g$, que se llama Sigmoide.
- Este modelo nos da resultados de 0 a 1, y la idea es que prediga la probabilidad de algún evento dados los features del input.
- Por ejemplo podríamos estimar la probabilidad de que un paciente padezca de una enfermedad usando datos como la edad, peso, algún estudio de sangre, sexo, etc.

### Limitaciones en modelos lineales:
Si quisieramos representar un XOR:

![[Pasted image 20230701131204.png]]

Vemos que el modelo lineal con regresión logística no nos sirve, ya que es demasido complejo para nuestro modelo.

## Redes neuronales

Una red neuronal es básicamente una función gigante de varias "capas".

![[Pasted image 20230701131755.png]]
### Como funca
No entendí mucho desde las filminas, pero la idea muy a lo bruto es que se computa el error en la salida, y luego se "propaga hacia atras"(back-propagation) y se van "haciendo cargo" los nodos, actualizando sus pesos.

### No linealidad
La no linealidad se basa en funciones de activación, es decir, una función que le aplico a la función lineal que me dan los pesos(por lo que entiendo, en cada "flecha" o conexión se aplica una de estas funciones). Entre estas están el **Sigmoide**, la **Tangente Hiperbólica** y **ReLU**(esta última es 0 si x es negativo e id si x es positivo).

### Normalización, o algo que cumple esa función
Para evitar **overfitting**, podemos "apagar" conexiones al azar.

### Cantidad de neuronas, cantidad de capas

- Más neuronas -> más probable el overfitting
- Mientras más capas -> más costoso entrenar


