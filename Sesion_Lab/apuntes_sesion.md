# Práctica radiactividad PET

## Introducción

Se implanta una fuente $\beta^+$ en un tejido, este decae emitiendo positrones. Estos se dividen en dos fotones de 511 keV que se emiten en direcciones opuestas. Estos fotones se detectan en un detector de PET.

La detección de los fotones (que se emiten en direcciones opuestas) deben detectarse en menos de 1 ns. 

## Fundamento teórico

$$ 
\beta^+: X^A_Z \longrightarrow Y^A_{z-1} + \nu_e + e^+ 
$$

Regla de Oro de Fermi:

Curva de distribución de energía.
La energía cinética máxima coincide con el calor emitido.


## Simulación

Se simula un cerebro [aprox esférica] (se considera que el material es agua), lo rodea una pequeña capa que será considerada como el cráneo (hueso), luego otra capa de agua y por último una capa de aire que se ve rodeada por plomo.


Para ejecutar la simulacion se debe ejecutar el comando:

	PET-W32.exe <PET.inp> PET.out

#### Archivo input

- SEEDS

	Semilla para la generación de números aleatorios

- PARTICLE TYPE

	Tipo de partícula (numero)
	cantidad de materiales 
	(numero )

- MATFILE
	
	Los archivos con los materiales

- ENER: *(si 4 o 5)

	energía, * características del atomo hijo (A y Z), transiciones prohibidas

- NUMBBER OF SURFACES: 
	
	(num)

- RADII:
	
	no tocar

- MATERIALS FOR BODIES:
		
	numeros correspondientes a los archivos de los materiales
	(habrá que cambiar el 3 por un 1 para sustituir creaneo por agua)

- GEO:
	archivo con la geometria 

- RSOURCE:
	posicion de la fuente (en el origen)

- NTOTAL:
	numero de eventos ($>10^5$)

- INITIAL ENERGY FILE: (distribución de energía) [keV]
	nombre archivo
	valor iniciar hist, valor final, numero de bins 

- ANIHILATION: (posiciones [distancia radial] de aniquilacion) [cm]
	nombre archivo
	pos_ini, pos_fin, numero de bins

- DETECTION: (histograma de energía para los fotones que llegan al plomo) [keV]
	nombre archivo
	valor inicial, valor final, numero de bins



Si NTOTAL=1000 entonces se genera POINTS.SAL (contiene las posiciones cartesianas)



Cada simulación en una carpeta diferente.
Copiar .exe, *.mat, PET.f, PET-WBA.geo, PET.inp

## Guión

### Apartado 1

Hacer la simulación para cada radioisótopo.
(NTOTAL $ \approx 10^5 $)

- Representar gráficamente y discutir el archivo _ini-ene.his_. Que se vea bien todo, si no, usar dos grafs. (usar leyenda).
- Calcular la energía media.

$$
\bar{x} = \sum_{i} \frac{x_i \cdot p(x_1)}{p(x_i)} = \sum_{i} \frac{ x_i \cdot p(x_1)}{C}
$$

$$
\sigma^2 (\bar{x}) = \sum_i \left( \frac{\partial \bar{x}}{\partial x_i} \right) ^2 \cdot \sigma^2 (p_i)
$$

$$
\sigma (\bar{x}) = \frac{1}{C} \sqrt{\sum_i \left( x_i \cdot \sigma(p_i) \right) ^2}
$$

### Apartado 2

Ejecutar el programa para otros radioisotopos.

- Representar gráficamente y discutir el archivo _ann-pos.his_.
- Calcular $\bar{r}$ medio y $\sigma(r)$.
- Regresión lineal de $E_m$ (y) vs $r_m$ (x).
- Analizar cambio con fuente monoenergética.
- 6 grafs en la que se representa $\beta^+$ y $e^+$. Tabla con los valores de $E_m$ y $r_m$ para cada isotopo.

### Apartado 3

Fichero: _det-ene.his_ --> Distribución de energía de los **FOTONES** detectados.

- Representar y discutir el archivo _det-ene.his_.

	- Pico grande corresponde a 511keV.

	- Antes - Efecto Compton:

		Pico derecho: a backscattering en el plomo. (~170keV)

		Pico izq: backscaterring de los que han hecho backscattering (~102 keV)

	- Después: Aniquilación con energía cinética no nula.

- Comparar para 1 radioisotopo el cambio de cráneo --> agua. (Representar en graf)

### Apartado 4 (oblig)

Fichero DETECT.SAL: información sobre partículas que llegan al detector (energia, posición, cosenos directores, ...)

E: Cunado 2 fotones de misma historia tienen la misma energía (1-True; 0-False)

D: Cuando 2 fotones de misma historia son colineales (1-True; 0-False)

	Consenos directores: cosenos de los ángulos 
	que forman con los ejes cartesianos.

	Colineas: 
	- $\cos (\alpha) = -\cos (\alpha') $
	- $\cos (\beta) = -\cos (\beta') $
	- $\cos (\gamma) = -\cos (\gamma') $


- Analizar:
	- E=1, D=0 - $\approx 16\%$
	- E=1, D=0
	- E=0, D=1
	- E=0, D=1
- Otras partículas detectadas
- Parejas incompletas