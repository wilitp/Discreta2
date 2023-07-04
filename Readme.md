# Resumen Matemática Discreta 2 2023
## Cómo usar el repo:
**No leer desde Github**, re renderizan mal los `.md` por la sintáxis de Latex que uso. Leerlo clonando el repo, y abriéndolo como una vault de [Obsidian](https://obsidian.md/). Ya hay en el repo archivos de configuración específicos de Obsidian para que funcionen los diagramas de Excalidraw.

## Teórico Daniel
1. [Edmonds-karp](./Demostraciones/comp-ek.md)
2. [Propiedad de las distancias](./Demostraciones/Propiedad-de-las-distancias.md)
3. [Complejidad Dinic](./Demostraciones/complejidad-de-dinic.md)
4.  [Complejidad Wave](./Demostraciones/comp-wave.md)
5. [Networks auxiliares sucesivos aumentan en longitud](./Demostraciones/Networks-auxiliares-aumentan.md)
6.  [Max flow min cut o teorema de Ford-Fulkerson](./Demostraciones/max-flow-min-cut.md)
7. [2-COLOR es polinomial.](./Demostraciones/2color-polinomial.md)
8. [Probar el Teorema de Hall.](./Demostraciones/teorema-hall.md)
9. [Teorema del matrimonio](./Demostraciones/teorema-matrimonio.md).
10. [Si G es bipartito entonces índice cromático es Delta.](./Demostraciones/teorema-indice-cromatico.md)
11. [Húngaro](./Demostraciones/comp-hungaro.md)
12. [Cota de Hamming y probarlo](./Demostraciones/cota-hamming.md)
13. [Delta del codigo es cardinal de minimo conjunto de columnas LD de H](./Demostraciones/delta-columnas-h.md)
14. [Teorema fundamental de códigos cíclicos](./Demostraciones/teorema-ciclicos.md)
15. [3SAT es NP-completo](./Demostraciones/3SAT-np-completo.md)
16. [3-COLOR es NP-completo.](./Demostraciones/3color-np-completo.md)

## Teórico Mili

**¿En qué tipo de problemas es adecuado utilizar aprendizaje automático?**
En problemas donde es difícil definir reglas - como relaciones lógicas o funciones matemáticas - de forma manual y necesitamos automatizar este proceso de relacionar variables independientes(input) de variables dependientes(output).

**¿Cuál es la diferencia entre la función de costo o pérdida, y las métricas de rendimiento del modelo?**

La función de costo es la que a intenar minimizar el optimizador que usemos, mientras que las métricas de rendimiento son para que un humano pueda evaluar el desempeño del modelo.

**¿Cómo se puede entrenar un modelo utilizando features o características no numéricas?**
Para esto, deben codificarse estos features de forma tal que sean transformados en una o varias entradas numéricas. Un ejemplo es el one-hot encoding:

| Provincia    | número | binario | one-hot |
| ------------ | ------ | ------- | ------- |
| Córdoba      | 0      | 0       | 10000   |
| Catamarca    | 1      | 01      | 010000  |
| ....         | -      | -       | -       |
| Buenos Aires | 5      | 0001    | 000001  |

Acá generamos n entradas, donde en es la cantidad de opciones para ese feature.

**Explique por qué se intenta minimizar la función de costo utilizando un método iterativo (numérico) y no un método analítico minimizando la derivada de la función?**
Minimizar de manera analítica es muy dificil para funciones más complejas. Al usar un método numérico mitigamos el costo y obtenemos resultados suficientemente buenos.

**¿Por qué el algoritmo SGD se llama “estocástico”?**
Esto viene de que el gradiente que calculamos es solo una aproximación estocástica del "valor real" del gradiente, dado que no es posible calcular la función de pérdida usando todos los datos presentes en el universo y solo usamos una porción de ellos.

Nota: estocástico es ser caracterizado por una distribución de variable aleatoria. Es similar a aleatorio y muchas veces se usa de forma indistinta. Pero siendo finos, aleatoriedad es un fenómeno concreto y lo estocástico tiene más que ver con como se modela.

**¿Qué impacto tiene el learning rate en la optimización de la función?**
El optimizador va a usar el learning rate para determinar cuánto hacer variar los pesos en cada iteración. Un **learning rate demasiado grande puede causar divergencia**. Mientras que un **learning rate demasido pequeño puede hacer muy largo el tiempo necesario** para que el método llegue a converger.

**Si una red tiene muy buen rendimiento durante el entrenamiento, pero muy bajo rendimiento en un conjunto de datos de evaluación, ¿qué acciones tomaría para mejorar el modelo?**
Este es un ejemplo de **overfitting**. En este caso podríamos reducir la **cantidad de features**, la **cantidad de neuronas / capas** o aplicar **dropout**.

**¿Por qué inicializamos los pesos de un modelo en valores aleatorios? ¿Qué pasaría si los inicializamos todos en cero? ¿Y todos en uno?**
Inicializamos en valores aleatorios para evitar problemas como el **vanishing gradient** y el **exploding gradient**, producto de inicializar los pesos en valores fijos particulares como 0 y 1.

**¿Por qué el dropout puede ser considerado una técnica de regularización?**
La regularización se usa para mitigar el overfitting. Este se da cuando el modelo tiene la capacidad de acercarse demasido(a modo de memorización) a los datos de entrenamiento.

El redes neuronales, el dropout consiste en "apagar" o "quitar" conexiones entre neuronas y así evitar que se aprendan relaciones que consistan en "memorizar" los datos de entrenamiento.

**¿Por qué está recomendada la estandarización de los valores de entrada de un modelo de machine learning?**
El optimizador puede llegar a ser sensible a la variabilidad en la escala en la que puede variar cada feature, y por ende darle más peso a un feature que a otro. Por eso, tener todas las entradas con desviación estandar de 1 es útil.