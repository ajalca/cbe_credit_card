# CREDIT CARD

## INTRODUCCIÓN
### El problema: 
aquí se plantea el problema y se lo contextualiza. Para esto pueden basarse en información que encuentren en internet. Pueden tratar de encontrar oportunidades de negocio en base a los datos que tienen disponibles, tal como pasa en su diario vivir.

### La solución: 
aquí se plantea la solución, que aunque es altamente técnica, en este punto de la presentación no se debe profundizar aún en ese tipo de detalles. Mencionen la solución técnica (segmentación de clientes) y cuál es su objetivo. Aquí también pueden mencionar soluciones existentes similares (machine learning-like) que hayan sido usadas en problemas similares.

## METODOLOGÍA
### Análisis exploratorio:
<blockquote>
Utilicen este espacio para explicar a su audiencia el dataset con el que cuentan y los descubrimientos relevantes que realizaron sobre él durante la exploración. Dar preferencias a la descripción de columnas/descubrimientos que luego serán relevantes como sustentación de decisiones técnicas (limpieza de datos, feature engineering, etc).
</blockquote>

El dataset contiene 8k de registros aproximadamente, de las que contiene dos tipos de variables numéricas y categóricas, de la cuál CUST_ID no aporta información para el análisis.
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
En MINIMUM_PAYMENTS y CREDIT_LIMIT hay valores faltantes, con un valor de 0.01% (313 registros) y 3.50% (1 registro) respectivamente.

![Grafico de dispersion](https://github.com/ajalca/cbe_credit_card/tree/main/images/readme/10222024_dispersion_balance_y_credit_limit.png)
A medida que aumenta el saldo en la tarjeta de crédito también aumente el límite de crédito, se ve un comportamiento de crecimiento ascendente.
Entre un saldo menor a 5000 y una línea de crédito menor a 10000 hay mayor concentración por lo que se aprecia que la mayoría de clientes tienen un saldo y crédito bajo.
En la parte superior derecha hay unos puntos outliers, que representa a unos pocos clientes con alto balance y crédito.
Hay otra dispersión de puntos con valores superiores a 20000 en la línea de créditos pero con un balance bajo, puede representar clientes con alta límite de crédito disponible pero no lo usan.

![Grafico de dispersion con categoría](https://github.com/ajalca/cbe_credit_card/tree/main/images/readme/10222024_dispersion_balance_y_credit_limit_por_tenure.png)
Se agregó la antigüedad de los usuarios en meses, se aprecia para 6 meses en azul y para 12 meses en rojo. Los clientes con más antigüedad están más dispersos lo que indica gran variedad de saldos y líneas de crédito.

![Grafico de cajas](https://github.com/ajalca/cbe_credit_card/tree/main/images/readme/10222024_plot_balance_y_tenure.png)
La distribución entre el saldo y la antigüedad.
Conforme la antigüedad aumenta es más variable el incremento en el saldo, y outliers en niveles superiores de saldo.
Desde el 9° mes los outliers son más frecuentes lo que sugiere que los clientes van acumulando su saldo como avanza el tiempo.
En cada uno de los niveles de antigüedad se aprecia a la mediana algo constante pero con un aumento en la dispersión por lo que no todos los clientes ahorran de la misma manera.

![Histograma de conjuntos](https://github.com/ajalca/cbe_credit_card/tree/main/images/readme/10222024_plot_balance_y_tenure.png)
La mayoría de los clientes tienen pagos relativamente bajos menor a 10000 por la concentración en la esquina inferior izquierda de la gráfica.
Se ve una correlación positiva entre los pagos y las compras, a medida que aumentan los pagos también aumentan las compras; pero también hay una alta dispersión en está tendencia lo que nos indica que no es un comportamiento lineal para todos.
Hay unos outliers en pagos y compras superando los 30000. Pero la mayoría de usuarios tienden hacer pagos y compras pequeñas como se visualiza en los histogramas.

### Procesamiento de datos
Expliquen aquí todo el procesamiento que le realizaron a sus datos y justifíquenlo.

### Entrenamiento y tuneo de hiperparámetros: 
Expliquen aquí la metodología que siguieron para el entrenamiento y tuneo. Expliquen y sustenten sus decisiones.

### Interpretación de los clusters:
Expliquen la relación de las variables del modelo con los clusters (al menos 4) en el sentido del negocio, utilicen visualizaciones para poder ver el comportamiento de las variables en cada uno de los clusters.

### IMPLEMENTACIÓN EN EL NEGOCIO
Expliquen cómo implementarían el modelo en el negocio y justifíquenlo. La justificación puede ser basada en cómo otras empresas implementan soluciones similares o puede ser basada en su humilde entendimiento del negocio.

### LIMITACIONES
Este es un espacio de autocrítica en donde describen las limitaciones que tiene su solución, es decir, factores que pudieron haber hecho que su solución no sea mejor de lo que es. Las limitaciones pueden ir desde el poder computacional, hasta la ausencia de alguna variable que consideren muy discriminante

### CONCLUSIONES Y RECOMENDACIONES
Las conclusiones pueden ir dirigidas a si pudieron resolver el problema exitosamente.
Las recomendaciones pueden ir dirigidas a otros científicos de datos o analistas de negocio que quieran construir una solución similar. En ese caso, estas recomendaciones pueden ser basadas en los problemas que ustedes enfrentaron durante el desarrollo. Las recomendaciones también pueden ir dirigidas al negocio, por ejemplo, recomendando el registro de cierta información que creen que pudiera ser bastante discriminativa pero que ustedes no tenían disponible en su dataset.

### FUTURE WORK
En esta sección ustedes suponen que seguirían trabajando en este proyecto o que alguién más lo hará y entonces mencionan qué cosas adicionarían o probarían para mejorar el proyecto.
