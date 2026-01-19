# Diccionario de Datos - Easy Loans 2023

## Descripción General
Este conjunto de datos contiene información detallada sobre 100 préstamos procesados por Easy Loans durante el año 2023 en Argentina. Los datos incluyen información del cliente, detalles del préstamo, ubicación geográfica y estado de reembolso.

## Campos del Dataset

### Identificadores
| Campo | Tipo | Descripción |
|-------|------|-------------|
| ID_Prestamo | Numérico | Identificador único del préstamo |
| ID_Cliente | Texto | Identificador único del cliente (formato: C001, C002, etc.) |

### Información Temporal
| Campo | Tipo | Descripción |
|-------|------|-------------|
| Fecha_Solicitud | Fecha | Fecha en que el cliente solicitó el préstamo |
| Fecha_Aprobacion | Fecha | Fecha en que se aprobó el préstamo |
| Fecha_Desembolso | Fecha | Fecha en que se entregó el dinero al cliente |
| Fecha_Ultimo_Pago | Fecha | Fecha del último pago realizado por el cliente |

### Información Financiera del Préstamo
| Campo | Tipo | Descripción | Rango |
|-------|------|-------------|-------|
| Monto_Solicitado | Numérico | Monto que el cliente solicitó (ARS) | 7,500 - 52,000 |
| Monto_Aprobado | Numérico | Monto que fue aprobado por Easy Loans (ARS) | 7,500 - 48,000 |
| Tasa_Interes | Decimal | Tasa de interés anual del préstamo (%) | 9.5% - 14.5% |
| Plazo_Meses | Numérico | Duración del préstamo en meses | 12, 15, 18, 24, 30, 36, 48, 60 |
| Monto_Pagado | Numérico | Monto total pagado hasta la fecha (ARS) | Variable |

### Información del Cliente
| Campo | Tipo | Descripción |
|-------|------|-------------|
| Nombre_Cliente | Texto | Nombre completo del cliente |
| Edad | Numérico | Edad del cliente en años (26-52) |
| Genero | Texto | Género del cliente (M/F) |
| Score_Credito | Numérico | Puntaje de crédito del cliente (635-760) |
| Ingreso_Mensual | Numérico | Ingreso mensual declarado del cliente (ARS) |
| Empleador | Texto | Nombre del empleador actual |

### Información Geográfica
| Campo | Tipo | Descripción |
|-------|------|-------------|
| Ciudad | Texto | Ciudad de residencia del cliente |
| Pais | Texto | País (todos los registros: Argentina) |
| Latitud | Decimal | Coordenada de latitud de la ciudad |
| Longitud | Decimal | Coordenada de longitud de la ciudad |

### Categorización del Préstamo
| Campo | Tipo | Descripción | Valores Posibles |
|-------|------|-------------|------------------|
| Tipo_Prestamo | Texto | Categoría del préstamo | Personal, Hipotecario, Automotriz, Empresarial |
| Estado_Prestamo | Texto | Estado actual del préstamo | Activo, Completado, Moroso |
| Proposito | Texto | Propósito declarado del préstamo | Consolidación de deudas, Compra de vivienda, Educación, Capital de trabajo, Compra de vehículo, Gastos médicos, Viaje, etc. |

## Estadísticas Clave del Dataset

### Distribución por Tipo de Préstamo
- **Personal**: ~40% de los préstamos
- **Hipotecario**: ~30% de los préstamos
- **Automotriz**: ~20% de los préstamos
- **Empresarial**: ~10% de los préstamos

### Distribución por Estado
- **Activo**: ~85% de los préstamos
- **Completado**: ~10% de los préstamos
- **Moroso**: ~5% de los préstamos

### Rangos Financieros
- **Monto promedio solicitado**: ~25,000 ARS
- **Monto promedio aprobado**: ~23,000 ARS
- **Tasa de interés promedio**: ~11.8%
- **Plazo promedio**: ~33 meses

### Distribución Geográfica
Los préstamos están distribuidos en 24 ciudades argentinas, con mayor concentración en:
- Buenos Aires
- Córdoba
- Rosario
- Mendoza

## Notas Importantes

1. **Calidad de Datos**: Todos los registros están completos sin valores nulos
2. **Período**: Todos los préstamos fueron procesados durante el año 2023
3. **Moneda**: Todos los montos están expresados en Pesos Argentinos (ARS)
4. **Coordenadas**: Las coordenadas geográficas son aproximadas al centro de cada ciudad
5. **Score de Crédito**: Utiliza un sistema de puntuación de 300-850 (estándar internacional)

## Casos de Uso para Análisis

### KPIs Sugeridos
1. Tasa de aprobación: (Monto_Aprobado / Monto_Solicitado) * 100
2. Porcentaje de mora: Préstamos Morosos / Total Préstamos
3. Tasa de completitud: Préstamos Completados / Total Préstamos
4. Monto promedio por tipo de préstamo
5. Porcentaje de reembolso: (Monto_Pagado / Monto_Aprobado) * 100

### Análisis Recomendados
1. **Análisis Temporal**: Evolución de préstamos aprobados por mes
2. **Análisis Geográfico**: Distribución de préstamos por ciudad/región
3. **Análisis de Riesgo**: Correlación entre Score_Credito y Estado_Prestamo
4. **Análisis de Desviación**: Diferencia entre Monto_Solicitado y Monto_Aprobado
5. **Análisis de Reembolso**: Progreso de pagos vs. monto aprobado
