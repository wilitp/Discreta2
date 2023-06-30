Probar que si H es matriz de chequeo de C, entonces;

$$\delta(C) = Min\{j : \exists \text{ un conjunto de j columnas LD de H}\}$$

Sea H matriz de chequeo, entonces C = Nu(H), y por lo tanto si $H \cdot w^t = 0 => w \ in C$

Sea M un conjunto de columnas de H de cardinal mínimo tal que M es LD.

Observemos primero que al ser de tamaño mínimo, hay una única combinación lineal no trivial de las columnas en M que es 0: donde todos los coeficientes son 1. Si suponemos que existe una combinación lineal con algún coeficiente nulo, digamos el i-ésimo, entonces tenemos que $M - H^{(i)}$ también es LD, lo que es absurdo pues es de cardinal más chico que M.

Sea w la palabra con un uno en cada entrada i-ésima sólo si $H^{(i)} \in M$, tenemos por lo observación de arriba que  $H \cdot w^t = \sum M = 0$

Tenemos que $|M| = |w|$ y $w \in C$. Sabemos que $\delta(C) \le |w|$Asumamos que $\delta < |w|$. Si este fuera el caso, existiría una palabra w' en C con menor cantidad de 1s, y tendríamos entonces que existe un subconjunto M' de columnas de H tal que $H \cdot w^t = \sum M' = 0$ y $|M'| = |w'|$. Tendríamos entonces que existe un subcojunto de columnas LD de cardinal menor a M. 

Concluyo por contradicción que 
$$\delta = |w| = |M| = Min\{j : \exists \text{ un conjunto de j columnas LD de H}\}$$