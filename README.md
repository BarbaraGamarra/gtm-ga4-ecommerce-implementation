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
