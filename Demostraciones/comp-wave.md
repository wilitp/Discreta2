¿Cual es la complejidad del algoritmo de Wave? Probarla. (no hace falta probar que la distancia en networks auxiliares sucesivos aumenta).
## Estructura
- Dar pseudocódigo(IMPORTANTE SE BORRAN VERTICES DESPUES DE ENVAR/DEVOLVER EN CIERTOS CASOS)
- Acotar cantidad de olas: **siempre bloqueamos a alguien en la ida**
- Separar en casos de envío y devolución (vértice a vértice)
- Acotar ocurrencias de cada caso
- Concluir la complejidad
## Prueba
Primero doy el pseudocódigo:

```python
g = 0

# Inicializacion
for x in E:
	D(x) = 0 # D(x) es in(x) - out(x) "Desbalanceo hacia adelante"
	B(x) = 0 # B(x) = "esta bloqueado?"
for x in R+(s):
	g(sx) = c(sx)
	D(x) = c(sx)
	D(s) = -c(sx)
	M(x) = {s} # Registramos a s como alguien que me envia

# Bucle principal

while (D(t) + D(s) != 0)
	# Forward wave
	for x in range(s+1, t-1)
		if(D(x) > 0): FB(x)
			
	# Backward wave
	for x in range(s+1, t-1)
		if(D(x) > 0 and B(x)): BB(x)
			

# Forward Balance "Enviar flujo"
def FB(x):
	while(D(x) > 0) and (R+(x).notEmpty())
		y = R+(x).get()
		if(B(y)): R+(x) -= y # Si esta bloqueado ya no le mandamos
		else:
			A = min(D(x),  c(xy) - g(xy)) # Cantidad a enviar, toda la que pueda dentro de mi desbalanceo
			# Actualizar flujo y desbalanceo
			g(xy) += A
			D(x) -= A
			D(y) += A
			M(y) = M(y) + x
			# Quitar de vecinos si esta lleno el lado
			if(g(xy) == c(xy)): R+(x) -= y
	if(D(x) > 0): B(x) = 1 # si no pudimos balancear, estamos bloqueados	
			
		
# Backward Balance "Devolver flujo"
def BB(x):
	while(D(x) > 0)
		y = M(x).get()
		A = min(D(x),  g(yx)) # Cantidad a devolver, toda la que pueda dentro de mi desbalanceo
		g(xy) -= A
		D(x) -= A
		D(y) += A
		if(g(yx) == 0): M(x) -= y # Si le devolvi todo, ya no me manda


```

La complejidad va a estar dada por:
$$S + P + V + Q$$
donde
$S = \text{cantidad de veces que enviamos de un x a un y y lo saturamos}$
$P = \text{cantidad de veces que enviamos de un x a un y y no lo saturamos}$
$V = \text{cantidad de veces que devolvemos de un x a un y y lo vaciamos}$
$Q = \text{cantidad de veces que devolvemos de un x a un y y no lo vaciamos}$

### Cantidad de olas
- Cuando vamos hacia adelante, siempre bloqueamos a un vértice. De no ser el caso, sería la última ola(pues si quedan todos balanceados, terminamos). Por lo tanto hay $O(n)$ olas.
- Solo podemos ir hacia atras luego de ir hacia adelante, así que también hay $O(n)$ olas hacia atrás

### S
Para S, sabemos que FB elimina a $y$ luego de enviarle flujo si lo hemos saturado. Esto es correcto ya que no volvemos a envar flujo por ahí(está lleno el lado). Si en algún momento se vaciara por un BB desde $y$, entonces $y$ estaría bloqueado y tampoco habría que enviarle nada por ese lado. **Por lo tanto $S \le m$**

### V
Al igual que para S, cuando devolvemos por un lado y este lado se vacía, entonces borramos a $y$ de $M(x)$. En principio podríamos ver a $y$ devuelta en $M(x)$ si este le volviera a envar; pero esto no es posible ya que $y$ no le enviaría nada a un vértice bloqueado como. **Por lo tanto $V \le m$**

### P
Cuando hacemos FB, solo el último lado que vemos es capaz de no ser saturado y terminar de balancear D(x), **ocurre a lo sumo una vez por Forward Balance**. Por lo tanto $P \le FB$. Cuál es la cantidad de FB? A lo sumo $(n-2)$ **por ola**. P es entonces $n-2 * O(n) = O(n^2)$

### Q
Cuando hacemos BB, solo un lado de los que miramos es capaz de no ser vaciado y por lo tanto hay uno solo(a lo sumo) por ola hacia atras por vértice. Q es entonces $(n-2= * O(n) = O(n^2)$

Complejidad total CFB:
$$S + V + P + Q = O(2m + 2n^2) = O(n^2)$$
Complejidad total Wave:
$$O(n) * O(n^2) = O(n^3)$$

