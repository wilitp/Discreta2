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