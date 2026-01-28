# Check Cashing Garantizado - Maxi

Este repositorio contiene la documentación del proyecto de **Check Cashing Garantizado** (Cambio de Cheques Garantizados) para Maxi.

## Contenido del Repositorio

### 📄 Documentos Principales

- **`BRD_Check_Cashing_Garantizado.md`** - Business Requirements Document completo en inglés con todos los requerimientos funcionales y no funcionales del proyecto
- **`RESUMEN_ANALISIS.md`** - Resumen ejecutivo en español del análisis realizado y los documentos revisados

### 📁 Documentos de Origen (`/DocInicial`)

#### Transcripciones de Llamadas (SRT)
- `Entendimiento del alcance de Check Cashing - 2025_06_30 11_28 CST - Recording.srt`
- `Entendimiento del alcance de Check Cashing parte 2 - 2025_07_02 14_55 CST - Recording 1.srt`
- `Entendimiento del alcance de Check Cashing parte 3 - 2025_07_07 11_58 CST - Recording.srt`
- `Entendimiento del alcance de Check Cashing parte 4 - 2025_07_08 15_56 CST - Recording.srt`

#### Diagramas y Procesos (PDF)
- `Proceso General por departamento.pdf` - Flujos de proceso de Front-End y Back-Office
- `Flujos por Departamento.pdf` - Procesos de compliance, cobranza y finanzas
- `Diagrama de pantallas.pdf` - Wireframes y mockups de las pantallas del sistema

## Resumen del Proyecto

El proyecto **Check Cashing Garantizado** implementa un sistema donde Maxi asume el 100% de la responsabilidad de los cheques cambiados, a diferencia del proceso tradicional donde el agente asume el riesgo.

### Componentes Principales

**Front-End (Hermes 2.0):**
- Escaneo de cheques con OCR
- Gestión de clientes con KYC completo
- Verificación telefónica por SMS
- Validación automática con Valid Systems
- Generación de recibos

**Back-Office (Cronos):**
- Gestión de retenciones (OFAC, KYC, Edit, Duplicate, Validation)
- Sistema de cobranza para cheques rebotados
- Compliance y prevención de fraude
- Dashboard de KPIs

### Integraciones Clave

- Valid Systems (validación de cheques)
- Nemesis (screening OFAC/AML)
- Bancos (formato X9)
- SMS/Email gateways

## Cómo Usar Este Repositorio

1. **Para entender el proyecto completo**: Lee el `BRD_Check_Cashing_Garantizado.md`
2. **Para un resumen rápido en español**: Consulta `RESUMEN_ANALISIS.md`
3. **Para revisar documentos originales**: Navega a la carpeta `/DocInicial`

## Estado del Proyecto

✅ BRD inicial completado  
⏳ Pendiente de revisión por stakeholders  
⏳ Resolución de ítems pendientes de decisión

---

*Última actualización: 28 de Enero de 2026*