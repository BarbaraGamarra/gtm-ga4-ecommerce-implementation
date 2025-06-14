# GTM & GA4 Ecommerce Implementation

> **Implementación práctica de Google Tag Manager y Google Analytics 4 en tienda ecommerce demo**

## 🎯 Descripción

Este proyecto documenta la implementación completa de GTM y GA4 en una tienda ecommerce basada en el [GTM Boilerplate de Google](https://github.com/google-marketing-solutions/gtm-boilerplate). 

La demo incluye 3 productos con variantes de talla y color, carrito de compras, sistema de login y proceso de checkout completo.

## 🛍️ Funcionalidades Implementadas

### Tienda Demo
- Catálogo con 3 productos
- Selección de tallas y colores
- Carrito de compras funcional
- Sistema de login/registro
- Proceso de checkout

### Tracking Implementado
- **Eventos básicos:** `page_view`, `view_item_list`, `view_item`, `add_to_cart`, `purchase`
- **Eventos personalizados:** `variant_change`, `user_login`
- **Enhanced Ecommerce** completo en GA4
- **Custom dimensions** para variantes de producto

## 📊 Google Tag Manager - Implementación de Eventos E-commerce

### Eventos Implementados

#### 🔍 View Item
Rastrea automáticamente cuando un usuario visualiza una página de producto individual (`/product/*`), proporcionando métricas de engagement por producto.

#### 👆 Select Item  
Captura las interacciones deliberadas del usuario con productos desde la página de listado (`/products`), diferenciando entre:
- **Clics en imagen del producto** (`interaction_source: product_image`)
- **Clics en botón "View Product"** (`interaction_source: view_button`)

### 🔧 Elementos HTML Trackeados

#### Elementos en la página `/products`:

**🖼️ Imagen del producto:**
```html
<img class="product-image" alt="product-image-T-Shirt" src="assets/images/t-shirt.jpg">
```

**🔘 Botón "View Product":**
```html
<a class="btn" href="/product/tshirt">View Product</a>
```

#### Selectores utilizados:
- **Clase CSS**: `product-image` (para clics en imagen)
- **Clase CSS**: `btn` (para clics en botón)
- **Texto**: "View Product" (identificación de botón)

> 💡 **Flujo**: Clic en `/products` → Evento `select_item` → Navegación a `/product/*` → Evento `view_item`

### Configuración Técnica

#### Variables de Capa de Datos
- `ecommerce.currency` - Moneda del producto (GBP)
- `ecommerce.value` - Valor/precio del producto  
- `ecommerce.items.0.item_name` - Nombre del producto
- `Click Source` - Variable personalizada que identifica el origen del clic

#### Activadores Configurados
- **Custom Event - View Item**: Se dispara con evento `view_item` del dataLayer
- **Click - Product Image**: Detecta clics en elementos con clase `product-image`
- **Click - View Product Button**: Detecta clics en botones con texto "View Product"

#### Estructura de Datos
```javascript
{
  event: 'view_item',
  ecommerce: {
    currency: 'GBP',
    value: 150,
    items: [{
      item_id: 'blazer_red_m',
      item_name: 'Blazer',
      price: 150,
      quantity: 1,
      item_variant: 'blazer#red#m'
    }]
  }
}
```

### Métricas y Análisis Disponibles

✅ **Productos más visualizados** - Frecuencia de eventos `view_item`  
✅ **Productos que generan mayor interés** - Frecuencia de eventos `select_item`  
✅ **Método de acceso preferido** - Análisis del parámetro `interaction_source`  
✅ **Tasa de conversión lista → visualización** - Ratio `select_item` vs `view_item`  
✅ **Patrones de navegación** - Secuencia de eventos por sesión de usuario

### Verificación

Los eventos pueden verificarse en:
- **GTM Preview Mode**: Para depuración en tiempo real
- **GA4 Informes en Tiempo Real**: Para validar llegada de datos
- **Console del navegador**: Inspección directa del `dataLayer`

## 🛒 Fase 2: Implementación de Funnel de E-commerce Completo

Esta segunda fase completa el tracking del funnel de conversión e-commerce implementando los eventos críticos del proceso de compra: **Add to Cart**, **View Cart** y **Purchase**.

### Configuración Implementada

**Variables de DataLayer:**
- `ecommerce.transaction_id` - ID único de transacción
- `ecommerce.items.0.item_id` - Identificador de producto
- `ecommerce.items.0.item_variant` - Variante del producto
- `ecommerce.items.0.quantity` - Cantidad de productos

**Activadores:**
- `Custom Event - Add to Cart` - Se dispara al añadir productos al carrito
- `Custom Event - View Cart` - Se activa al visualizar el carrito
- `Custom Event - Purchase` - Se ejecuta al completar una compra
- `Page View - Thank You Page` - Activador de respaldo para compras

**Etiquetas GA4:**
- `GA4 - Add to Cart` - Rastrea productos añadidos al carrito
- `GA4 - View Cart` - Mide engagement con el contenido del carrito
- `GA4 - Purchase` - Registra conversiones con transaction_id único

### Flujo de Testing

1. **Add to Cart**: Navegar a página de producto → Clic "Add to Basket" → Verificar evento en GTM Preview
2. **View Cart**: Añadir producto → Ir a `/basket` → Confirmar disparo automático del evento
3. **Purchase**: Completar compra (directa o desde carrito) → Validar transaction_id único en `/thank-you`

### Métricas Disponibles

- Funnel de conversión completo (view_item → add_to_cart → view_cart → purchase)
- Tasa de abandono del carrito
- Average Order Value (AOV)
- Revenue tracking con IDs únicos
- Análisis de comportamiento de compra (directa vs carrito)

> **Ventaja clave**: Los eventos de e-commerce están pre-implementados en el dataLayer, permitiendo una configuración robusta sin depender de tracking de clics complejos.

## 🚀 Tecnologías

- **Frontend:** Angular
- **Backend:** Flask
- **Analytics:** Google Analytics 4
- **Tag Management:** Google Tag Manager
- **Reporting:** GA4 + Looker Studio

## 📁 Estructura del Proyecto

```
├── docs/                    # Documentación paso a paso
│   ├── plan-proyecto.md     # Objetivos y cronograma
│   ├── setup-gtm-ga4.md     # Configuración inicial
│   ├── implementacion.md    # Etiquetado completo
│   └── testing-reports.md   # Testing e informes
├── gtm-config/              # Configuraciones exportadas
├── screenshots/             # Capturas del proceso
│   ├── gtm/                 # Screenshots de GTM
│   └── ga4/                 # Screenshots de GA4
└── reports/                 # Templates de informes
```

## 📊 Informes Creados

1. **Dashboard GA4:** Métricas clave de ecommerce
2. **Análisis de Productos:** Performance por producto y variante
3. **Dashboard Looker Studio:** Visualización ejecutiva

## 🛠️ Quick Start

1. **Clonar repositorio base:**
   ```bash
   git clone https://github.com/google-marketing-solutions/gtm-boilerplate.git
   ```

2. **Configurar GTM:**
   - Crear container en GTM
   - Configurar GTM ID en `environment.prod.ts`

3. **Configurar GA4:**
   - Crear property GA4
   - Configurar Measurement ID
   - Habilitar Enhanced Ecommerce

## 📈 Progreso

- [ ] Setup inicial GTM y GA4
- [ ] Implementación eventos básicos
- [ ] Eventos personalizados
- [ ] Testing y validación
- [ ] Informes y dashboards
- [ ] Documentación completa

## 📚 Documentación

Sigue la documentación paso a paso en la carpeta `/docs/`:

1. [Plan del Proyecto](docs/plan-proyecto.md)
2. [Setup GTM y GA4](docs/setup-gtm-ga4.md)
3. [Implementación](docs/implementacion.md)
4. [Testing y Reports](docs/testing-reports.md)

## 🎯 Objetivos de Aprendizaje

- ✅ Configuración avanzada de GTM
- ✅ Enhanced Ecommerce en GA4
- ✅ Custom events y dimensions
- ✅ Testing y debugging
- ✅ Reporting personalizado

---

**Desarrollado por:** [Barbara Gamarra](https://github.com/BarbaraGamarra)  
**Proyecto:** Certificación Google Analytics & Tag Manager  
**Fecha:** Junio 2025

> 💡 **Nota**: La implementación utiliza Enhanced Ecommerce de GA4 y sigue las mejores prácticas de medición de comercio electrónico.