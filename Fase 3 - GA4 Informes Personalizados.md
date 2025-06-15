# GA4 - Informes Personalizados para E-commerce

## Configuración de informes avanzados

Este documento constituye la tercera fase de nuestra implementación de analytics para e-commerce. Habiendo configurado el tracking completo en GTM (view_item, select_item, add_to_cart, view_cart, purchase), ahora crearemos informes personalizados en GA4 que transformen estos datos en insights accionables para la toma de decisiones de negocio.

Los informes que configuraremos permitirán analizar el rendimiento de productos desde múltiples perspectivas, identificar patrones de comportamiento del usuario, medir la efectividad del funnel de conversión, y calcular métricas clave de revenue. Esta información es fundamental para optimizar la experiencia de usuario, mejorar las tasas de conversión, y maximizar el valor promedio de pedido.

## Acceso a GA4 y navegación

### Verificación de datos disponibles

Antes de crear informes, es fundamental verificar que los eventos implementados en GTM están llegando correctamente a GA4.

#### Verificación en tiempo real
1. Acceder a GA4 → **Informes** → **Tiempo real**
2. En la sección "Eventos en los últimos 30 minutos", verificar la presencia de:
   - `view_item`
   - `select_item` 
   - `add_to_cart`
   - `view_cart`
   - `purchase`

#### Verificación de parámetros
Para cada evento, hacer clic en el nombre del evento y verificar que los parámetros personalizados aparecen correctamente:
- `item_name`
- `interaction_source` (solo para select_item)
- `currency`
- `value`
- `transaction_id` (solo para purchase)

### Navegación a informes de exploración

Los informes de exploración ofrecen la máxima flexibilidad para análisis personalizados:

1. **Menú lateral**: Explorar → **Exploración**
2. **Crear nuevo informe**: Botón "+" o "Exploración en blanco"
3. **Plantillas disponibles**: Exploración libre, Embudo, Análisis de cohortes, Análisis de rutas

## Informe: Ranking de Visualizaciones por Productos

Este informe identifica qué productos generan mayor interés inicial, proporcionando insights sobre la efectividad del catálogo y las preferencias de los usuarios.

### Configuración del informe de exploración

**Tipo de informe**: Formato libre

**Pasos de configuración:**
1. Acceder a **Explorar** > **Formato libre**
2. Agregar dimensiones: clic en "+" junto a Dimensiones → seleccionar `Nombre del evento` y `Ruta de página`
3. Agregar métrica: clic en "+" junto a Métricas → seleccionar `Número de eventos`
4. Configurar visualización: arrastrar `Ruta de página` a Filas y `Número de eventos` a Valores
5. Aplicar filtro: clic en "+" en Filtros → `Nombre del evento` exactamente igual a `view_item`
6. Configurar formato: seleccionar visualización Tabla y tipo de celda "gráfico de barras" para la métrica
7. Ordenar: clic en encabezado `Número de eventos` para orden descendente

**Configuración de variables:**
- **Dimensiones**:
  - `Nombre del evento` 
  - `Ruta de página`
- **Métricas**:
  - `Número de eventos`

**Configuración de visualización:**
- **Filas**: `Ruta de página`
- **Valores**: `Número de eventos` (tipo de celda: gráfico de barras)
- **Filtros**: 
  - `Nombre del evento` exactamente igual a `view_item`

**Configuración adicional:**
- **Ordenar por**: `Número de eventos` (descendente)
- **Visualización**: Tabla

Este informe mostrará una tabla ordenada con los productos más visualizados, permitiendo identificar qué items del catálogo generan mayor atención.


## Análisis de Comportamiento de Interacción

### Informe: Imagen vs Botón "View Product"

Este análisis específico mide la efectividad de diferentes elementos de interfaz para generar interacciones con productos.

#### Configuración del informe de exploración

**Tipo de informe**: Exploración libre

**Configuración de variables:**
- **Dimensiones**:
  - `Origen de interacción` (parámetro personalizado)
  - `Nombre del elemento`
- **Métricas**:
  - `Recuento de eventos`

**Configuración de visualización:**
- **Filas**: `Origen de interacción`
- **Columnas**: `Nombre del elemento`
- **Valores**: `Recuento de eventos`
- **Filtros**:
  - `Nombre del evento` exactamente igual a `select_item`

**Análisis adicional - Gráfico de barras:**
- **Dimensión**: `Origen de interacción`
- **Métrica**: `Recuento de eventos`
- **Tipo de gráfico**: Gráfico de barras

Este informe revelará si los usuarios prefieren hacer clic en las imágenes de productos o en los botones "View Product", información crucial para optimizar la experiencia de usuario.

### Informe: Análisis de Comportamiento de Interacción

Este análisis mide la efectividad de diferentes elementos de la interfaz para generar interacciones con productos, usando la dimensión personalizada `interaction_source` que indica si la interacción fue en imagen, botón de producto o botón variante.

#### Cómo crear la dimensión personalizada `interaction_source` en GA4

1. Entra en tu cuenta de GA4.
2. En el menú de la izquierda, ve a **Configuración > Definiciones personalizadas**.
3. Haz clic en **Crear dimensión personalizada**.
4. Rellena los campos:
   - **Nombre**: interaction_source
   - **Ámbito**: Evento
   - **Descripción**: Tipo de interacción del usuario con el producto (imagen, botón, variante)
   - **Nombre del parámetro del evento**: interaction_source
5. Guarda la dimensión personalizada.

> Nota: Para que la dimensión aparezca en los informes puede tardar hasta 24 horas después de su creación y de que los datos empiecen a llegar con ese parámetro.

#### Configuración del informe de exploración en GA4

##### Tipo de informe
- Exploración libre

##### Variables a configurar

###### Dimensiones
- `interaction_source` (dimensión personalizada basada en el parámetro del evento `select_item`)
- `Nombre del evento`

###### Métricas
- `Recuento de eventos`

##### Configuración de filas y valores

- **Filas**: `interaction_source`
- **Valores**: `Recuento de eventos`

##### Filtros

- `Nombre del evento` exactamente igual a `select_item`

#### Visualización recomendada

- Tabla o gráfico de barras para comparar el número de interacciones por tipo (imagen, botón, botón variante)

#### Interpretación

Este informe muestra qué tipo de interacción prefieren los usuarios al seleccionar productos, ayudando a optimizar los elementos de interfaz para mejorar la experiencia y conversión.


## Funnel de Conversión

### Informe: Embudo de E-commerce Completo

El análisis de embudo es fundamental para identificar puntos de fricción en el customer journey y oportunidades de optimización.

#### Configuración del informe de embudo

**Tipo de informe**: Análisis de embudo

**Configuración de pasos:**

**Paso 1 - Visualización de producto:**
- **Nombre**: "View Item"
- **Condición**: `Nombre del evento` exactamente igual a `view_item`

**Paso 2 - Selección desde lista:**
- **Nombre**: "Select Item"  
- **Condición**: `Nombre del evento` exactamente igual a `select_item`

**Paso 3 - Añadir al carrito:**
- **Nombre**: "Add to Cart"
- **Condición**: `Nombre del evento` exactamente igual a `add_to_cart`

**Paso 4 - Compra:**
- **Nombre**: "Purchase"
- **Condición**: `Nombre del evento` exactamente igual a `purchase`

**Configuración del embudo:**
- **Ventana de tiempo**: 30 minutos (tiempo razonable para completar una compra)
- **Tipo de embudo**: Embudo cerrado (los usuarios deben completar pasos en orden)

### Análisis de Abandono por Paso

Este informe complementa al embudo principal y permite identificar cuellos de botella o fricciones en cada paso del journey del usuario dentro del proceso de compra.

#### Informe: Exploración de abandono por paso

**Tipo de informe**: Exploración libre

---

#### Configuración de variables

- **Dimensiones**:
  - `Nombre del evento` (`event_name`)

- **Métricas**:
  - `Recuento de eventos`
  - `Total de usuarios`

---

#### Configuración de visualización

- **Filas**:
  - `Nombre del evento`

- **Valores**:
  - `Recuento de eventos`
  - `Total de usuarios`

- **Filtro**:
  - `Nombre del evento` **coincide con expresión regular**:
    ```
    view_item|select_item|add_to_cart|view_cart|purchase
    ```

---

#### Métricas calculadas externas (puedes calcularlas fuera de GA4 con los datos exportados)

- **Tasa de conversión global**:  
  `(purchase / view_item) * 100`

- **Tasa de abandono de carrito**:  
  `((view_cart - purchase) / view_cart) * 100`

- **Eficiencia de selección**:  
  `(add_to_cart / select_item) * 100`

---

> 💡 Este informe ofrece una visión rápida de cuántos usuarios avanzan por cada paso clave del proceso de compra y en qué punto abandonan. Puedes usarlo como punto de partida para aplicar mejoras en la UX o el contenido de producto.

## Análisis de Volumen y Revenue

### Informe Personalizado: Dashboard de Revenue

Este será nuestro informe personalizado que aparecerá en el menú lateral de GA4, proporcionando acceso rápido a métricas clave de ingresos.

#### Creación del informe personalizado

**Navegación**: Informes → **Biblioteca** → **Crear informe personalizado**

**Configuración básica:**
- **Nombre del informe**: "E-commerce Revenue Dashboard"
- **Tipo**: Informe detallado

**Configuración de métricas:**
- **Métricas principales**:
  - `Ingresos por compras` (revenue from purchases)
  - `Compras` (purchases)
  - `Usuarios que compraron`

**Configuración de dimensiones:**
- **Dimensión primaria**: `Nombre del elemento`
- **Dimensión secundaria**: `Fecha`

**Filtros del informe:**
- `Nombre del evento` exactamente igual a `purchase`

**Configuración de visualización:**
- **Tabla principal**: Datos por producto
- **Gráfico temporal**: Tendencia de ingresos por día
- **Métricas resumidas**: Totales en tarjetas superiores

### Informe: Análisis de Average Order Value (AOV)

Análisis detallado del valor promedio de pedido y patrones de compra.

#### Configuración del informe de exploración

**Tipo de informe**: Exploración libre

**Configuración de variables:**
- **Dimensiones**:
  - `Nombre del elemento`
  - `ID de transacción`  
- **Métricas**:
  - `Valor del evento`
  - `Recuento de eventos`

**Configuración de visualización:**
- **Filas**: `Nombre del elemento`
- **Valores**: `Valor del evento`, `Recuento de eventos`
- **Filtros**:
  - `Nombre del evento` exactamente igual a `purchase`

**Métricas calculadas:**
- **AOV por producto**: `Valor del evento / Recuento de eventos`
- **Contribución al revenue total**: `(Valor del evento del producto / Valor total) * 100`

### Informe: Volumen de Compras por Producto

Análisis de popularidad de productos basado en volumen de ventas.

#### Configuración del informe de exploración

**Tipo de informe**: Exploración libre

**Configuración de variables:**
- **Dimensiones**:
  - `Nombre del elemento`
  - `Cantidad` (parámetro personalizado)
- **Métricas**:
  - `Recuento de eventos`
  - `Valor del evento`

**Configuración de visualización:**
- **Filas**: `Nombre del elemento`
- **Valores**: `Recuento de eventos`, `Valor del evento`
- **Filtros**:
  - `Nombre del evento` exactamente igual a `purchase`

**Ordenación**: Por `Recuento de eventos` descendente

**Visualización adicional - Gráfico de dispersión:**
- **Eje X**: `Recuento de eventos` (volumen)
- **Eje Y**: `Valor del evento` (revenue)
- **Puntos**: `Nombre del elemento`

Este gráfico identificará productos con alto volumen/bajo valor vs productos premium con menor volumen pero mayor valor.

## Configuración de métricas calculadas

### Creación de métricas personalizadas

GA4 permite crear métricas calculadas para obtener insights más específicos. Acceder a través de: Administrar → **Definiciones personalizadas** → **Métricas calculadas**.

#### Métrica: Tasa de Conversión Global
- **Nombre**: `Tasa de Conversión Global`
- **Nombre para informes**: `Global Conversion Rate`
- **Fórmula**: `count_distinct_events(purchase) / count_distinct_events(view_item) * 100`
- **Unidad de medida**: Porcentaje

#### Métrica: Tasa de Abandono de Carrito
- **Nombre**: `Tasa de Abandono de Carrito`
- **Nombre para informes**: `Cart Abandonment Rate`
- **Fórmula**: `(count_distinct_events(view_cart) - count_distinct_events(purchase)) / count_distinct_events(view_cart) * 100`
- **Unidad de medida**: Porcentaje

#### Métrica: Eficiencia de Interacción
- **Nombre**: `Eficiencia de Interacción`
- **Nombre para informes**: `Interaction Efficiency`
- **Fórmula**: `count_distinct_events(add_to_cart) / count_distinct_events(select_item) * 100`
- **Unidad de medida**: Porcentaje

#### Métrica: Revenue por Usuario
- **Nombre**: `Revenue por Usuario`
- **Nombre para informes**: `Revenue per User`
- **Fórmula**: `sum(event_value) / count_distinct_users`
- **Unidad de medida**: Moneda

### Aplicación de métricas calculadas

Una vez creadas, estas métricas estarán disponibles en todos los informes de exploración y pueden utilizarse para:

- **Benchmarking**: Comparar rendimiento entre períodos
- **Segmentación**: Identificar usuarios o productos de alto/bajo rendimiento  
- **Alertas**: Configurar notificaciones cuando las métricas cambien significativamente
- **Reporting automatizado**: Incluir en dashboards para stakeholders

## Configuración de alertas y automatización

### Alertas inteligentes

Para monitorear cambios significativos en el rendimiento:

**Navegación**: Administrar → **Alertas inteligentes**

#### Alerta: Caída en Conversiones
- **Nombre**: "Caída significativa en compras"
- **Condición**: `purchase events` disminuye más del 20% comparado con período anterior
- **Frecuencia**: Diaria
- **Destinatarios**: Equipo de e-commerce

#### Alerta: Aumento en Abandono de Carrito
- **Nombre**: "Incremento en abandono de carrito"
- **Condición**: `Tasa de Abandono de Carrito` aumenta más del 15%
- **Frecuencia**: Semanal
- **Destinatarios**: Equipo de UX

### Programación de informes

**Navegación**: Desde cualquier informe → **Compartir** → **Programar envío por correo electrónico**

#### Informe Semanal de Revenue
- **Frecuencia**: Semanal (lunes por la mañana)
- **Formato**: PDF
- **Destinatarios**: Equipo directivo
- **Contenido**: Dashboard de Revenue personalizado

## Interpretación de resultados y insights

### Análisis de Productos

**Insights clave a identificar:**
- **Productos con alta visualización, baja conversión**: Oportunidades de optimización de página de producto
- **Productos con baja visualización, alta conversión**: Candidatos para mayor promoción
- **Productos consistentes**: Base estable del catálogo

**Acciones recomendadas:**
- Optimizar descripciones y imágenes de productos con baja conversión
- Aumentar visibilidad de productos con alta conversión
- Analizar patrones estacionales o tendencias

### Análisis de Comportamiento

**Insights clave a identificar:**
- **Preferencia imagen vs botón**: Optimización de diseño de interfaz
- **Patrones por producto**: Algunos productos pueden funcionar mejor con interacciones visuales
- **Tasas de conversión diferenciadas**: Diferentes tipos de interacción pueden tener diferentes intenciones de compra

**Acciones recomendadas:**
- Priorizar el elemento de interacción más efectivo en el diseño
- A/B testing de diferentes layouts basado en los datos
- Personalización de interfaz por tipo de producto

### Análisis de Funnel

**Insights clave a identificar:**
- **Mayor punto de abandono**: Dónde se pierde más usuarios en el proceso
- **Patrones de comportamiento**: Usuarios que saltan pasos vs usuarios lineales
- **Tiempo de conversión**: Cuánto tardan los usuarios en completar el funnel

**Acciones recomendadas:**
- Optimizar el paso con mayor abandono
- Simplificar el proceso de checkout
- Implementar remarketing para usuarios que abandonan en pasos específicos

### Análisis de Revenue

**Insights clave a identificar:**
- **Productos estrella**: Alto volumen y alto valor
- **Productos de entrada**: Alto volumen, bajo valor (pueden ser loss leaders)
- **Productos premium**: Bajo volumen, alto valor
- **Tendencias temporales**: Patrones estacionales o semanales

**Acciones recomendadas:**
- Estrategias de pricing diferenciadas
- Promociones cruzadas entre productos complementarios
- Optimización de inventory basada en patrones de venta
- Campaigns específicas para aumentar AOV

## Exportación y compartición de datos

### Exportación para análisis adicional

Todos los informes de exploración permiten exportación en múltiples formatos:

**Opciones de exportación:**
- **CSV**: Para análisis en Excel o hojas de cálculo
- **Google Sheets**: Integración directa con Google Workspace  
- **PDF**: Para presentaciones y reportes ejecutivos

**Procedimiento de exportación:**
1. Desde cualquier informe → **Compartir**
2. Seleccionar **Descargar archivo**
3. Elegir formato deseado
4. Configurar opciones de exportación (rango de fechas, filtros, etc.)

### Compartición de informes

**Opciones de compartición:**
- **Enlace directo**: URL que mantiene configuración del informe
- **Acceso colaborativo**: Permisos de visualización o edición
- **Integración en sitios web**: Embed de gráficos específicos

**Consideraciones de privacidad:**
- Verificar permisos de acceso a la propiedad GA4
- Configurar filtros de datos sensibles si es necesario
- Documentar quién tiene acceso a qué información

## Próximos pasos hacia Looker

### Preparación de datos para Looker

Los informes configurados en GA4 servirán como base para el análisis avanzado en Looker. Para preparar la transición:

**Documentación de métricas:**
- Crear diccionario de métricas calculadas
- Documentar fórmulas y definiciones
- Establecer nomenclatura consistente

**Identificación de KPIs clave:**
- Seleccionar métricas más importantes para dashboards ejecutivos
- Definir targets y benchmarks para cada KPI
- Establecer frecuencia de reporte para cada métrica

**Estructura de datos:**
- Identificar dimensiones principales para segmentación
- Planificar jerarquías de productos/categorías
- Definir períodos de comparación estándar

Con esta base sólida de informes en GA4, la siguiente fase del proyecto se enfocará en crear dashboards ejecutivos y KPIs avanzados en Looker, proporcionando una vista integral del rendimiento del e-commerce para la toma de decisiones estratégicas.