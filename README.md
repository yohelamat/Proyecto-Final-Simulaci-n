# Simulación del Flujo de Pasajeros en la Estación Villa Zaita – Metro de Panamá

## 1. Descripción del proyecto

Este proyecto consiste en el desarrollo de una simulación interactiva del flujo de pasajeros en la estación Villa Zaita del Metro de Panamá, durante el horario de mayor demanda, comprendido entre las 6:30 a. m. y las 8:30 a. m.

La simulación representa el ingreso de pasajeros a través de los torniquetes, el desplazamiento hacia el andén, la llegada de los trenes y el proceso de abordaje. También permite observar el comportamiento de las filas, la capacidad de los torniquetes y la cantidad de pasajeros que logran abordar o permanecen pendientes al finalizar la simulación.

## 2. Integrantes del grupo

**Universidad:** Universidad Interamericana de Panamá

**Proyecto:** Simulación del Flujo de Pasajeros y Tiempos de Espera en Villa Zaita, Metro de Panamá.

**Integrantes:**

- Yohel Amat
- Keytlen Mata
- Michael Zhang
- Rances Hernandez

## 3. Objetivo general

Simular el comportamiento del flujo de pasajeros en la estación Villa Zaita mediante un modelo de eventos discretos, con el propósito de analizar los tiempos de espera, la capacidad de atención de los torniquetes y el abordaje de pasajeros en los trenes durante las horas de mayor demanda.

## 4. Tecnologías utilizadas

- **HTML5:** estructura principal de la aplicación.
- **CSS3 y Tailwind CSS:** diseño y presentación de la interfaz.
- **JavaScript:** lógica de simulación y procesamiento de eventos.
- **Three.js:** representación visual en 3D de la estación.
- **Chart.js:** generación de gráficos estadísticos.

## 5. Funcionamiento de la simulación

El modelo representa las siguientes etapas:

1. **Ingreso de pasajeros:** los pasajeros llegan a la estación de manera aleatoria.
2. **Acceso por torniquetes:** los usuarios ingresan mediante los torniquetes disponibles, donde se simula el tiempo de validación.
3. **Desplazamiento al andén:** después de pasar por los torniquetes, los pasajeros se dirigen hacia el área de espera.
4. **Llegada del tren:** los trenes llegan de acuerdo con el intervalo de tiempo configurado.
5. **Abordaje:** los pasajeros ingresan al tren mientras exista tiempo disponible durante la parada y capacidad para recibirlos.
6. **Pasajeros pendientes:** quienes no logran abordar permanecen en la estación esperando una próxima oportunidad.

La representación visual permite observar el movimiento de los pasajeros, las filas de acceso, la separación entre los torniquetes de entrada y salida, el área del andén y los trenes.

## 6. Parámetros configurables

La aplicación permite modificar diferentes parámetros para evaluar el comportamiento del sistema.

| Parámetro | Descripción | Valor inicial |
|---|---|---:|
| Tiempo medio entre llegadas | Intervalo promedio entre la llegada de pasajeros | 1.2 segundos |
| Tiempo medio de validación | Tiempo promedio que tarda un torniquete en atender a un pasajero | 3 segundos |
| Torniquetes activos | Cantidad de torniquetes habilitados para la entrada | 9 |
| Capacidad por tren | Cantidad máxima de pasajeros que puede abordar cada tren en la simulación | 40 pasajeros |
| Intervalo entre trenes | Tiempo entre la llegada de un tren y el siguiente | 90 segundos |
| Tiempo de parada | Tiempo que permanece el tren en la estación para permitir el abordaje | 22 segundos |

**Nota:** La capacidad por tren es un supuesto configurable del modelo y no representa necesariamente la capacidad oficial de los trenes del Metro de Panamá.

## 7. Modelo matemático

### 7.1. Llegada de pasajeros

Las llegadas se modelan mediante una distribución exponencial, utilizada para representar intervalos aleatorios entre pasajeros.

La tasa promedio de llegada se calcula mediante:

$$
\lambda = \frac{60}{T_a}
$$

Donde:

- **λ:** tasa promedio de llegada de pasajeros por minuto.
- **Tₐ:** tiempo medio entre llegadas, expresado en segundos.

### 7.2. Atención en los torniquetes

El tiempo de validación se genera mediante una distribución lognormal, permitiendo representar variaciones en el tiempo de atención de cada pasajero.

La tasa de servicio por torniquete se calcula mediante:

$$
\mu = \frac{60}{T_v}
$$

La capacidad teórica total de atención se obtiene con:

$$
C = \mu \times N
$$

Donde:

- **μ:** capacidad de atención por torniquete.
- **Tᵥ:** tiempo medio de validación en segundos.
- **N:** cantidad de torniquetes activos.
- **C:** capacidad teórica total de atención por minuto.

### 7.3. Capacidad de los trenes

Cada tren tiene una capacidad máxima configurable. El sistema controla la cantidad de pasajeros que aborda cada tren y evita que se supere el límite establecido.

Cuando el tren alcanza su capacidad máxima o finaliza su tiempo de parada, deja de recibir pasajeros y continúa su recorrido.

## 8. Indicadores de resultados

Al finalizar la simulación, el sistema presenta indicadores que permiten analizar el comportamiento del flujo de pasajeros.

| Indicador | Descripción |
|---|---|
| Ingresos | Cantidad total de pasajeros que ingresaron a la estación. |
| Abordajes | Cantidad total de pasajeros que lograron abordar los trenes. |
| Pendientes al finalizar | Pasajeros que ingresaron, pero no habían abordado ningún tren al finalizar la simulación. |
| Personas únicas que perdieron un tren | Cantidad de pasajeros que no lograron abordar al menos un tren. Cada pasajero se cuenta una sola vez en este indicador. |
| Eventos de tren perdido | Cantidad total de ocasiones en que los pasajeros no lograron abordar un tren. Un mismo pasajero puede generar más de un evento. |
| Porcentaje de personas retrasadas | Porcentaje de pasajeros que perdieron al menos un tren. |
| Espera promedio en andén | Tiempo promedio que los pasajeros permanecen esperando en el andén. |

### 8.1. Balance de pasajeros

Para garantizar la consistencia de los resultados, se utiliza la siguiente relación:

$$
\text{Ingresos} = \text{Abordados} + \text{Pendientes al finalizar}
$$

Por lo tanto, la cantidad de pasajeros pendientes se calcula mediante:

$$
\text{Pendientes al finalizar} = \text{Ingresos} - \text{Abordados}
$$

**Ejemplo:**

Si durante la simulación ingresaron 5,298 pasajeros y abordaron 5,258 pasajeros, se realiza la siguiente operación:

$$
5,298 - 5,258 = 40
$$

El resultado correcto es de **40 pasajeros pendientes al finalizar la simulación**.

Es importante diferenciar este indicador de las personas que perdieron un tren. Estas últimas representan a los pasajeros que no lograron abordar una salida específica, aunque pueden permanecer en la estación y abordar un tren posterior. Por esta razón, ambos indicadores no deben confundirse ni utilizarse como si fueran equivalentes.

## 9. Comparación de escenarios

La aplicación permite registrar dos escenarios diferentes, identificados como **Escenario A** y **Escenario B**.

Esta funcionalidad facilita la comparación de los resultados obtenidos al modificar los parámetros de la simulación, por ejemplo:

- Aumentar o disminuir la cantidad de torniquetes activos.
- Modificar el tiempo de validación.
- Cambiar el intervalo entre trenes.
- Ajustar el tiempo de parada.
- Modificar la capacidad de pasajeros por tren.
- Variar el tiempo promedio entre llegadas.

La comparación presenta los resultados de ambos escenarios y la diferencia entre sus indicadores, permitiendo identificar cómo los cambios en los parámetros afectan el funcionamiento del sistema.

## 10. Alcance y limitaciones

La simulación permite analizar de manera visual y cuantitativa el comportamiento del flujo de pasajeros en una estación de metro.

Sin embargo, los resultados dependen de los parámetros configurados, las distribuciones probabilísticas utilizadas y la variabilidad propia del modelo.

La capacidad por tren y los demás valores iniciales son parámetros de simulación. Para utilizar los resultados como base de decisiones operativas reales, sería necesario contrastarlos con datos oficiales de operación y demanda del Metro de Panamá.

## 11. Ejecución del proyecto

Para ejecutar la simulación:

1. Descargar o clonar este repositorio.
2. Abrir la carpeta del proyecto.
3. Localizar el archivo HTML principal.
4. Abrirlo en un navegador web actualizado.
5. Configurar los parámetros deseados.
6. Iniciar la simulación y observar los resultados.

**Recomendación:** Se requiere conexión a internet para cargar las bibliotecas externas utilizadas por la aplicación.

## 12. Conclusión

El desarrollo de esta simulación permite representar y analizar el flujo de pasajeros en la estación Villa Zaita, considerando los procesos de ingreso, atención en torniquetes, espera en el andén y abordaje de trenes.

Mediante la modificación de los parámetros y la comparación de escenarios, es posible observar cómo la capacidad de atención y la frecuencia de los trenes influyen en los tiempos de espera y en la acumulación de pasajeros pendientes.

Asimismo, el balance entre ingresos, abordajes y pasajeros pendientes permite mantener la coherencia de los resultados y distinguir correctamente a quienes aún no han abordado de quienes han perdido una o varias oportunidades de abordar un tren.
