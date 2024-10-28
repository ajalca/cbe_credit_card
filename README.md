# CREDIT CARD

## INTRODUCCIÓN
### El problema: 
En las instituciones financieras, la falta de una segmentación limita la capacidad de ofrecer servicios adaptados a las necesidades y hábitos específicos de cada usuario, lo que resulta en una menor satisfacción y en la pérdida de oportunidades de fidelización y optimización de ingresos. Identificar y caracterizar a distintos grupos de clientes con base en sus patrones de consumo y pago es esencial para desarrollar productos financieros efectivos que maximicen el valor y la lealtad del cliente.

### La solución: 
La solución a este problema se basa en la segmentación de clientes mediante técnicas de análisis de datos que permitirán identificar patrones comunes y crear perfiles específicos según el comportamiento de consumo y pago. Esta estrategia, ampliamente utilizada en la industria financiera a través de métodos de machine learning, facilita el desarrollo de productos personalizados al agrupar a los clientes en segmentos con características y necesidades similares. Nofal, S. (2024) utilizó la segmentación de clientes para identificar aquellos altamente valorados en un banco en Jordania, basándose en la frecuencia y el monto de sus transacciones, demostrando que la segmentación basada en comportamiento transaccional ayuda a los bancos a mejorar la personalización y efectividad de sus estrategias. El objetivo es optimizar la oferta de servicios financieros y mejorar la satisfacción del cliente, aplicando un enfoque de segmentación avanzado que se ha demostrado efectivo en problemas similares de personalización de productos y fidelización en otras áreas comerciales. 

Referencia:                                                                                                                                                        
Nofal, S. (2024). Identifying highly-valued bank customers with current accounts based on the frequency and amount of transactions. Heliyon, 10(13).

## METODOLOGÍA
### Análisis exploratorio:

El dataset contiene **8k de registros** aproximadamente, de las que contiene dos tipos de ***variables numéricas*** y ***variables categóricas***, de la cuál *CUST_ID* no aporta información para el análisis.
<ul>
  <li>Variables numéricas
    <ol>
      <li>Balance</li>
        <ul>
            <li>BALANCE</li>
            <li>PURCHASES</li>
            <li>ONEOFF_PURCHASES</li>
            <li>INSTALLMENTS_PURCHASES</li>
            <li>CASH_ADVANCE</li>
            <li>CREDIT_LIMIT</li>
        </ul>
      <li>Frecuencia</li>
        <ul>
            <li>BALANCE_FREQUENCY</li>
            <li>PURCHASES_FREQUENCY</li>
            <li>ONEOFF_PURCHASES_FREQUENCY</li>
            <li>PURCHASES_INSTALLMENTS_FREQUENCY</li>
            <li>CASH_ADVANCE_FREQUENCY</li>
            <li>CASH_ADVANCE_TRX</li>
            <li>PURCHASES_TRX</li>
        </ul>
      <li>Pagos</li>
        <ul>
            <li>PAYMENTS</li>
            <li>MINIMUM_PAYMENTS</li>
            <li>PRC_FULL_PAYMENT</li>
        </ul>
      <li>Otros</li>
        <ul>
            <li>TENURE</li>
        </ul>
    </ol>
  </li>
  <li>Variable categórica</li>
    <ol>
      <li>CUST_ID</li>
    </ol>
</ul>

En *MINIMUM_PAYMENTS* y *CREDIT_LIMIT* hay valores faltantes, con un valor de **0.01%** (313 registros) y **3.50%** (1 registro) respectivamente.

![Grafico de dispersion](https://github.com/ajalca/cbe_credit_card/blob/main/images/readme/10222024_dispersion_balance_y_credit_limit.png)

A medida que aumenta el saldo en la tarjeta de crédito también aumente el límite de crédito, se ve un comportamiento de crecimiento ascendente.
Entre un saldo menor a **5k** y una línea de crédito menor a **10k** hay mayor concentración por lo que se aprecia que la mayoría de clientes tienen un saldo y crédito bajo.
En la parte superior derecha hay unos puntos outliers, que representa a unos pocos clientes con alto balance y crédito.
Hay otra dispersión de puntos con valores superiores a **20k** en la línea de créditos pero con un balance bajo, puede representar clientes con alta límite de crédito disponible pero no lo usan.

![Grafico de dispersion con categoría](https://github.com/ajalca/cbe_credit_card/blob/main/images/readme/10222024_dispersion_balance_y_credit_limit_por_tenure.png)

Se agregó la antigüedad de los usuarios en meses, se aprecia para ***6 meses en azul*** y para ***12 meses en rojo***. Los clientes con más antigüedad están más dispersos lo que indica gran variedad de saldos y líneas de crédito.

![Grafico de cajas](https://github.com/ajalca/cbe_credit_card/blob/main/images/readme/10222024_plot_balance_y_tenure.png)

La distribución entre el saldo y la antigüedad.
Conforme la antigüedad aumenta es más variable el incremento en el saldo, y outliers en niveles superiores de saldo.
Desde el ***9° mes*** los outliers son más frecuentes lo que sugiere que los clientes van acumulando su saldo como avanza el tiempo.
En cada uno de los niveles de antigüedad se aprecia a la mediana algo constante pero con un aumento en la dispersión por lo que no todos los clientes ahorran de la misma manera.

![Histograma de conjuntos](https://github.com/ajalca/cbe_credit_card/blob/main/images/readme/10222024_histograma_payments_purchases.png)

La mayoría de los clientes tienen pagos relativamente bajos menor a **10k** por la concentración en la esquina inferior izquierda de la gráfica.
Se ve una correlación positiva entre los pagos y las compras, a medida que aumentan los pagos también aumentan las compras; pero también hay una alta dispersión en está tendencia lo que nos indica que no es un comportamiento lineal para todos.
Hay unos outliers en pagos y compras superando los **30k**. Pero la mayoría de usuarios tienden hacer pagos y compras pequeñas como se visualiza en los histogramas.

![Correlacion](https://github.com/ajalca/cbe_credit_card/blob/main/images/readme/10222024_correlacion.png)

*ONEOFF_PURCHASES* y *PURCHASES* tienen una correlación positiva muy fuerte **~0.92**, cuanto más gasta alguien en compras de pago único más aumentan sus compras totales.
*INSTALLMENTS_PURCHASES*  y *PURCHASES* presentan una correlación fuerte **~0.68**, lo que indica que las compras a plazos frecuentes tienen un impacto significativo en las compras totales.
*CASH_ADVANCE_FREQUENCY* y *BALANCE* tienen una correlación negativa fuerte **~-0.45**, lo que indica que los adelantos en efectivo frecuentes se asocian con saldos más bajos.

### Procesamiento de datos

![Nulos](https://github.com/ajalca/cbe_credit_card/blob/main/images/readme/10222024_distribucion_missing.png)

Se reemplazaron los valores faltantes con la mediana de cada columna numérica. Cómo se apreciaron varios outliers y está técnica no afecta a los valores extremos, ya que usa los valores centrales.
*MINIMUM_PAYMENTS* o *CREDIT_LIMIT*, algunos clientes pueden tener límites o pagos extremadamente altos o bajos, lo que afectaría el promedio, pero no la mediana.

Se inicio el dataset con **17 variables**, sólo se a eliminado una columna porque el *CUST_ID* que no aporta para el análisis; se tienen finalmente **16 variables** para el análisis.

![1Variable](https://github.com/ajalca/cbe_credit_card/blob/main/images/readme/10242024_distribucion_purchases_to_credit_limit.png)

Mide qué tan cerca está un cliente de su límite de crédito con respecto a las compras realizadas. Un valor alto puede indicar que el cliente está alcanzado el límite de su crédito disponible.

![2.1Variable](https://github.com/ajalca/cbe_credit_card/blob/main/images/readme/10242024_stripplot_payments_to_balance.png)

Pero se tuvieron problemas con la computadora al querer graficar esta nueva variable, se hizo una transformación logarítmica.
Existen algunos outliers en el lado derecho (valores **mayores a 0.8**), hay algunos clientes que realizan pagos muy altos en proporción a su saldo.

![2.2Variable](https://github.com/ajalca/cbe_credit_card/blob/main/images/readme/10242024_distribucion_log_payments_to_balance.png)

Mide la proporción de pagos realizados en comparación con el saldo. Un valor alto indica que el cliente paga gran parte de su saldo, mientras que un valor bajo puede indicar que no paga lo suficiente.

La mayoría de los datos están concentrados en la parte baja de la escala logarítmica (**entre 0 y 2**), lo que indica que la mayoría de los clientes realizan pagos relativamente bajos en comparación con su balance.

### Entrenamiento y tuneo de hiperparámetros: 

![MetodoCodo](https://github.com/ajalca/cbe_credit_card/blob/main/images/readme/10252024_metodo_codo_n1.png)

Se ve la variación de la "Suma de los Errores al Cuadrado" (SSE) en función de la cantidad de clusters K. Mientras los clusters están aumentando los SSE disminuyen porque están más cercanos  a su centro.
El codo está *alrededor de 4* aproximadamente lo que representa los cluster para nuestros datos.

![Silhouette](https://github.com/ajalca/cbe_credit_card/blob/main/images/readme/10252024_sihouette_n1.png)
Se visualiza la separación entre los clusters. El score más alto se encuentre en el cluster 2, antes de que disminuya significativamente el score , el *cluster 3 y 4* son valores alto. Pero el score 4 se alinea con el gráfico del codo.

Un óptimo cluster es **4** hay un cohesión entre dentro de los cluster y la separación entre ellos.

![Cluster jerarquico](https://github.com/ajalca/cbe_credit_card/blob/main/images/readme/10272024_clustering_jerarquico.png)
Se refleja tres grupo de colores, lo que representa los clusters. Hay una mayor similitud en los grupos de la parte baja que los que están más arriba.

![Cluster jerarquico Frecuencia](https://github.com/ajalca/cbe_credit_card/blob/main/images/readme/10272024_clustering_jerarquico_freq.png)
El cluster de color púrpura (**0**) se agrupa hacia valores más altos de *BALANCE*, los clusters de otros colores están distribuidos en distintos niveles de *BALANCE_FREQUENCY*.  Para los puntos con el mismo color, tienen similitudes en sus valores de *BALANCE* y *BALANCE_FREQUENCY*.  Nos permitirá identificar patrones en la frecuencia de balance y los montos de balance entre los distintos grupos.


### Interpretación de los clusters:
<blockquote>
Expliquen la relación de las variables del modelo con los clusters (al menos 4) en el sentido del negocio, utilicen visualizaciones para poder ver el comportamiento de las variables en cada uno de los clusters.
</blockquote>

### IMPLEMENTACIÓN EN EL NEGOCIO
De acuerdo a los clusters determinados, podemos segmentar a los clientes por su saldo y uso de crédito, con frecuencia de adelantos, y con pagos completos y frecuentes. Para así poder desarrollar diferentes estrategias de fidelización, de acuerdo a la necesidad de cada segmento, ya sean ofertas de inversión, líneas de crédito extendidas, programas de educación financiera. También se podría implementar programas de recompensas o fidelización a clientes que pagan sus préstamos antes del tiempo pactado, e incluso ofrecer productos financieros con bajas tasas de interés en adelantos en efectivo.
  
Los resultados obtenidos del modelo deberían ser cargados en alguna plataforma CRM, asignando a cada cliente su cluster correspondiente. Para que así los equipos de ventas y marketing tomen en cuenta la información y puedan segmentar de manera óptima las estrategias, promociones, y la comunicación.

### LIMITACIONES
Para poder segmentar aún mejor a la base de clientes, la falta de algunos datos financieros y de comportamiento podría limitar la precisión de nuestro modelo en la clasificación de los perfiles. Esto puede ser mitigado en futuras versiones del modelo si se recopilan datos más específicos, como información sobre ingresos y empleo.
En cuanto a los modelos, aunque K-medoids es menos sensible que K-means, la presencia de outliers en ciertas variables puede afectar los clusters. En futuras mejoras, se pueden considerar métodos de detección y remoción de outliers o transformar variables que presenten alta variabilidad.
En recursos computacionales, la actualización periódica del modelo requiere recursos computacionales, lo que puede ser una limitación si los datos crecen significativamente. Para reducir este costo, puede implementarse un enfoque de entrenamiento incremental.

### CONCLUSIONES Y RECOMENDACIONES
<blockquote>
Las conclusiones pueden ir dirigidas a si pudieron resolver el problema exitosamente.
Las recomendaciones pueden ir dirigidas a otros científicos de datos o analistas de negocio que quieran construir una solución similar. En ese caso, estas recomendaciones pueden ser basadas en los problemas que ustedes enfrentaron durante el desarrollo. Las recomendaciones también pueden ir dirigidas al negocio, por ejemplo, recomendando el registro de cierta información que creen que pudiera ser bastante discriminativa pero que ustedes no tenían disponible en su dataset.
</blockquote>

### FUTURE WORK
<blockquote>
En esta sección ustedes suponen que seguirían trabajando en este proyecto o que alguién más lo hará y entonces mencionan qué cosas adicionarían o probarían para mejorar el proyecto.
</blockquote>
