# 📊 E‑Commerce Analytics Demo: GTM + GA4 Tracking & Reporting

**Proyecto:** Implementación y explotación de un funnel de e‑commerce completo
**Rol:** Data Analyst & Marketing Analytics
**Objetivo:** Diseñar, configurar y validar un seguimiento avanzado de eventos en Google Tag Manager y Google Analytics 4, y construir informes accionables para optimizar la experiencia de usuario y la conversión.

---

## 🎯 Descripción

Este proyecto documenta la implementación completa de GTM y GA4 en una tienda ecommerce basada en el GTM Boilerplate de Google.

🔗 **Repositorio Demo:** [https://github.com/google-marketing-solutions/gtm-boilerplate](https://github.com/google-marketing-solutions/gtm-boilerplate)

La demo incluye 3 productos con variantes de talla y color, carrito de compras, sistema de login y proceso de checkout completo.

🛍️ **Funcionalidades Implementadas**

* Tienda Demo
* Catálogo con 3 productos
* Selección de tallas y colores
* Carrito de compras funcional
* Sistema de login/registro
* Proceso de checkout

---

## 🗂️ Estructura del Repositorio

```plaintext
gtm-ga4-ecommerce-implementation/
│
├── README.md
├── Fase 1  - GTM Select Item View Item.md
├── Fase 2  - GTM Funnel Completo de Compras.md
├── Fase 3  - GA4 Informes Personalizados.md
├── screenshots/
│   └── gtm/ …
├── reports/
│   └── …
└── .gitignoreplaintext

```

---

## 🚀 Fase 1 – GTM: Select Item & View Item

**Objetivo:** Capturar interacciones de usuario y visualizaciones de producto.

* **Eventos configurados:**

  * `select_item` (clic en imágenes/botón “View Product”)
  * `view_item` (carga de página de detalle)

| Evento        | Trigger                                  | Parámetros clave                                       |
| ------------- | ---------------------------------------- | ------------------------------------------------------ |
| `select_item` | Clic en `product-image` / `View Product` | `interaction_source`, `currency`, `value`, `item_name` |
| `view_item`   | Evento personalizado `view_item`         | `currency`, `value`, `items`, `item_name`              |

* **Variables GTM:**

  * Data Layer v2: `ecommerce.currency`, `ecommerce.value`, `ecommerce.items.0.item_name`
  * Custom JS “Click Source” para distinguir imagen vs botón

* **Validación:**

  * GTM Preview: etiquetas “GA4 – Select Item” y “GA4 – View Item” disparadas
  * Revisión de dataLayer y valores de variables

---

## 🔄 Fase 2 – GTM Funnel Completo de Compras

**Objetivo:** Implementar eventos clave del funnel: selección, carrito y compra.

* **Eventos adicionales configurados:**

  * `add_to_cart`
  * `view_cart`
  * `purchase`

* **Embudo de conversión:**

  1. `view_item` (visualización de producto)
  2. `select_item` (selección desde listado)
  3. `add_to_cart` (añadir al carrito)
  4. `view_cart` (visualización del carrito)
  5. `purchase` (compra finalizada)

* **Triggers:**

  * Custom Events para todos los eventos del dataLayer
  * Fallback de Page View en `/thank-you`

* **Validación en GTM Preview:**

  * Secuencia de firing en orden correcto
  * Verificación de `transaction_id` en `purchase`

---

## 📈 Fase 3 – GA4: Informes Personalizados

**Objetivo:** Transformar los eventos del funnel en insights accionables.

1. **Ranking de Visualizaciones (**\`\`**)**

   * Exploración Libre, filtro `view_item`
   * Dimensión: Ruta de página
   * Métrica: Número de eventos

2. **Análisis de Interacción (**\`\`**)**

   * Dimensión: `interaction_source`
   * Métrica: Recuento de eventos
   * Visualización: Tabla + Gráfico de barras

3. **Embudo de Conversión Completo**

   * Pasos definidos en Fase 2
   * Ventana: 30 min, embudo cerrado

4. **Dashboard de Revenue & AOV**

   * Métricas: Ingresos, Compras, Usuarios únicos
   * AOV = Valor del evento ÷ Recuento de compras
   * Tasa de Conversión = purchases ÷ view\_item × 100%

---

## 🔧 Habilidades y Tecnologías

* Google Tag Manager: dataLayer v2, triggers, tags, JS personalizado
* Google Analytics 4: Exploraciones, embudos, dimensiones y métricas personalizadas
* Data Analysis: Funnel analysis, cohortes, segmentación, KPIs
* Marketing Digital: Tracking de interacciones, optimización UX, métricas de revenue
* Reporting & BI: Dashboards y próximos pasos hacia Looker

---

## ⭐ Resultados Clave

* Implementación robusta de eventos en todo el funnel
* Visualización clara de secuencia de compra y puntos de abandono
* Informes GA4 para:

  * Productos más vistos vs más comprados
  * Elementos de interfaz con mayor engagement
  * Conversion Rate y AOV detallados
* Base lista para escalar análisis con BigQuery y Looker

---

## 📬 Contacto

**LinkedIn:** [https://www.linkedin.com/in/barbara-m-gamarra/](https://www.linkedin.com/in/barbara-m-gamarra/)
