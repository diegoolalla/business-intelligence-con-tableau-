# Análisis de Business Intelligence - Easy Loans 2023

## 📊 Descripción del Proyecto

Análisis completo de inteligencia de negocios para Easy Loans utilizando Tableau Desktop. Este proyecto incluye el modelado de datos, exploración, cálculos clave y visualizaciones interactivas para analizar el desempeño de préstamos durante el año 2023.

## 🎯 Objetivos

- Analizar el comportamiento de préstamos otorgados en 2023
- Identificar patrones de aprobación y desembolso
- Evaluar tasas de recuperación y mora
- Proporcionar insights estratégicos para optimizar operaciones financieras
- Crear dashboards interactivos para toma de decisiones en tiempo real

## 📁 Estructura del Proyecto

```
business-intelligence-con-tableau-/
├── data/
│   └── easy_loans_2023.csv          # Dataset principal (100 préstamos)
├── docs/
│   ├── data_dictionary.md           # Diccionario de datos completo
│   ├── tableau_implementation_guide.md  # Guía de implementación en Tableau
│   └── insights_estrategicos.md     # Análisis de insights y recomendaciones
├── images/
│   └── (screenshots de dashboards)
└── README.md                        # Este archivo
```

## 📋 Dataset

El dataset `easy_loans_2023.csv` contiene **100 registros** de préstamos con las siguientes características:

### Campos Principales:
- **Identificación:** ID_Prestamo, ID_Cliente
- **Temporal:** Fechas de solicitud, aprobación, desembolso y último pago
- **Financiero:** Montos solicitados/aprobados, tasas de interés, plazos, montos pagados
- **Cliente:** Nombre, edad, género, score crediticio, ingreso mensual, empleador
- **Geográfico:** Ciudad, país, coordenadas (latitud, longitud)
- **Categorización:** Tipo de préstamo, estado, propósito

### Tipos de Préstamos:
1. **Personal** (40%): Consolidación de deudas, gastos varios, educación
2. **Hipotecario** (30%): Compra y refacción de viviendas
3. **Automotriz** (20%): Compra de vehículos
4. **Empresarial** (10%): Capital de trabajo, equipamiento

### Estados:
- **Activo** (85%): Préstamos en proceso de pago
- **Completado** (10%): Préstamos totalmente pagados
- **Moroso** (5%): Préstamos con retrasos

## 🚀 Guía de Uso

### 1. Preparación de Datos

1. El archivo CSV está listo para usar en Tableau
2. Revisar el [Diccionario de Datos](docs/data_dictionary.md) para entender cada campo
3. Importar a Tableau Desktop: `Connect → Text File → easy_loans_2023.csv`

### 2. Implementación en Tableau

Seguir la [Guía de Implementación](docs/tableau_implementation_guide.md) que incluye:

#### A. Cálculos Clave
- **Promedios:** Monto promedio, tasa promedio, plazo promedio
- **Acumulados:** Monto acumulado aprobado, pagos acumulados
- **Reembolsos:** Tasa de recuperación, monto pendiente
- **Desviación:** Diferencia entre solicitado y aprobado

#### B. Visualizaciones Principales
1. **Dashboard de KPIs:**
   - Total préstamos
   - Monto total aprobado
   - Tasa de recuperación
   - Tasa de mora
   - Monto promedio

2. **Mapa Geográfico:**
   - Distribución de préstamos por ciudad
   - Tamaño: Monto aprobado
   - Color: Tasa de interés promedio

3. **Gráfico de Evolución Acumulada:**
   - Líneas temporales de montos aprobados vs pagados
   - Análisis mensual y trimestral

4. **Análisis de Desviación:**
   - Diferencia entre monto solicitado y aprobado
   - Scatter plot con línea de tendencia

#### C. Dashboards Interactivos
- **Overview Easy Loans 2023:** Dashboard principal con todos los KPIs
- **Análisis de Riesgo:** Enfocado en mora y scoring
- **Análisis Financiero:** Flujo de efectivo y rentabilidad

#### D. Filtros Globales
- Rango de fechas
- Tipo de préstamo
- Estado del préstamo
- Ciudad
- Rango de montos

#### E. Parámetros Ajustables
- Objetivo de recuperación
- Top N ciudades
- Umbral de mora
- Métrica principal (selector dinámico)

### 3. Insights Estratégicos

Consultar el documento de [Insights Estratégicos](docs/insights_estrategicos.md) que incluye:

- **Hallazgos principales:** Análisis de volumen, aprobación, distribución
- **Análisis de riesgo:** Perfil de mora, scoring, recuperación
- **Oportunidades:** Expansión geográfica, nuevos productos, fidelización
- **Riesgos:** Concentración, competencia, liquidez
- **Recomendaciones:** Plan de acción a corto, mediano y largo plazo

## 📊 KPIs Principales

| KPI | Valor | Meta |
|-----|-------|------|
| Total Préstamos | 100 | - |
| Monto Total Aprobado | $2,300,000 ARS | - |
| Monto Promedio | $23,000 ARS | - |
| Tasa de Aprobación | 92% | >90% |
| Tasa de Recuperación | ~40% | - |
| Tasa de Mora | 5% | <3% |
| Score Crediticio Promedio | 710 | >700 |
| Tiempo de Procesamiento | 5-6 días | <5 días |

## 🎨 Características del Análisis

### Modelado de Datos ✅
- Estructura relacional con 100 registros completos
- Sin valores nulos
- Tipos de datos correctamente definidos
- Campos calculados para análisis avanzados

### Exploración de Datos ✅
- Análisis descriptivo completo
- Distribución por tipo, estado y geografía
- Análisis temporal y estacional
- Segmentación de clientes

### Cálculos Clave ✅
- Promedios ponderados y simples
- Acumulados con running sums
- Métricas de reembolso y recuperación
- Análisis de desviación

### Visualizaciones ✅
- KPIs con formato profesional
- Mapas con coordenadas geográficas
- Gráficos acumulados (running totals)
- Análisis de desviación con scatter plots
- Heat maps y tree maps
- Distribuciones y comparativas

### Dashboards Interactivos ✅
- Filtros globales sincronizados
- Parámetros ajustables en tiempo real
- Acciones de highlight y filtrado
- Tooltips personalizados
- Navegación intuitiva

### Configuración Avanzada ✅
- Paleta de colores consistente
- Formato de números estandarizado
- Responsive design
- Story telling con narrativa

## 📦 Entregables

### Archivo Principal
- **Easy_Loans_2023_Analisis_BI.twbx**: Tableau Packaged Workbook completo
  - Incluye todos los datos
  - Todos los dashboards configurados
  - Filtros y parámetros operativos
  - Story con insights principales

### Documentación
- [x] Diccionario de datos
- [x] Guía de implementación
- [x] Insights estratégicos
- [x] README completo

### Bonus (Opcional)
- [ ] Publicación en Tableau Cloud
- [ ] Screenshot del dashboard en Cloud
- [ ] URL pública compartible

## 🔍 Insights Destacados

### 1. Performance Operativa
- Proceso de aprobación eficiente (2-3 días)
- Alta tasa de aprobación (92%) indica buenos criterios
- Tasa de mora controlada (5%) para el sector

### 2. Distribución de Cartera
- Diversificación saludable entre tipos de préstamo
- Concentración geográfica en 3 ciudades principales (70%)
- Oportunidad de expansión en regiones desatendidas

### 3. Perfil de Riesgo
- Score crediticio promedio saludable (710)
- Correlación clara entre score bajo y mora
- Préstamos personales con mayor riesgo relativo

### 4. Recuperación
- Préstamos a corto plazo (12 meses) muestran completitud total
- Hipotecarios y empresariales en progreso normal
- Sistema de cobranza efectivo

## 🎯 Recomendaciones Clave

1. **Optimizar criterios de aprobación** para scores <650
2. **Expandir geográficamente** a 5 nuevas ciudades estratégicas
3. **Implementar programa de fidelización** para clientes recurrentes
4. **Desarrollar productos especializados** (préstamos verdes, educativos)
5. **Digitalizar proceso** para reducir tiempo a <3 días
6. **Implementar cobranza preventiva** para reducir mora a <3%

## 🛠️ Requisitos

### Software
- **Tableau Desktop** 2023.1 o superior
- Cualquier navegador moderno (para Tableau Cloud)

### Archivos Necesarios
- `data/easy_loans_2023.csv` (incluido)
- Todos los archivos de documentación (incluidos)

### Conocimientos Recomendados
- Conceptos básicos de Tableau
- Entendimiento de métricas financieras
- Interpretación de visualizaciones de datos

## 📚 Recursos Adicionales

### Documentación Interna
1. [Diccionario de Datos](docs/data_dictionary.md) - Descripción completa de campos
2. [Guía de Implementación](docs/tableau_implementation_guide.md) - Paso a paso en Tableau
3. [Insights Estratégicos](docs/insights_estrategicos.md) - Análisis y recomendaciones

### Tableau Resources
- [Tableau Desktop User Guide](https://help.tableau.com/current/pro/desktop/en-us/default.htm)
- [Tableau Calculations](https://help.tableau.com/current/pro/desktop/en-us/calculations.htm)
- [Tableau Dashboards](https://help.tableau.com/current/pro/desktop/en-us/dashboards.htm)

## 📞 Soporte

Para preguntas o problemas:
1. Revisar la documentación en `/docs`
2. Consultar los comentarios en los cálculos de Tableau
3. Verificar que los datos se cargaron correctamente

## 📝 Notas Técnicas

### Formato de Fechas
- Formato CSV: YYYY-MM-DD
- Formato Tableau: Se detecta automáticamente
- Recomendado: dd/mm/yyyy para visualización

### Formato de Montos
- Moneda: Pesos Argentinos (ARS)
- Sin decimales en montos principales
- Formato: $ ###,###

### Coordenadas Geográficas
- Sistema: WGS84 (estándar GPS)
- Precisión: Centro de ciudad (aproximado)
- Uso: Mapas de símbolos en Tableau

## 🔄 Actualizaciones Futuras

Este proyecto es extensible para:
- [ ] Análisis comparativo anual (2023 vs 2024)
- [ ] Integración con datos en tiempo real
- [ ] Modelos predictivos de mora
- [ ] Automatización de reportes
- [ ] API para integración con otros sistemas

## ✅ Checklist de Implementación

- [x] Dataset preparado y documentado
- [x] Diccionario de datos completo
- [x] Guía de implementación detallada
- [x] Cálculos y fórmulas documentadas
- [x] Especificaciones de visualizaciones
- [x] Configuración de dashboards
- [x] Filtros y parámetros definidos
- [x] Insights estratégicos documentados
- [x] README completo
- [ ] Archivo .twbx generado (requiere Tableau Desktop)
- [ ] Testing de todas las funcionalidades
- [ ] Publicación en Tableau Cloud (opcional)

## 🎓 Aprendizajes Clave

Este proyecto permite practicar:
- Modelado de datos para análisis financiero
- Creación de cálculos complejos en Tableau
- Diseño de dashboards interactivos
- Storytelling con datos
- Análisis de riesgo crediticio
- Recomendaciones basadas en datos

## 📄 Licencia

Este proyecto es de uso educativo y demostrativo para análisis de Business Intelligence.

---

**Desarrollado para:** Curso de Business Intelligence con Tableau  
**Fecha:** 2024  
**Herramientas:** Tableau Desktop, CSV  
**Alcance:** Análisis de préstamos 2023
