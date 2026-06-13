<div align="center">

# 📊 Cost Center Tracker
### Power BI · Excel · PGC España

[![Power BI](https://img.shields.io/badge/Power%20BI-Desktop-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![Excel](https://img.shields.io/badge/Excel-Fuente%20de%20datos-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)](https://www.microsoft.com/excel)
[![PGC](https://img.shields.io/badge/Plan%20General%20Contable-España-c0392b?style=for-the-badge)]()
[![Demo](https://img.shields.io/badge/Datos-Sintéticos-8e44ad?style=for-the-badge)]()

**Dashboard interactivo de seguimiento de centros de coste, cuentas contables y empleados.**  
Selecciona un centro o un nombre y el informe se filtra solo — cuentas, personas y notas en tiempo real.

</div>

---

<!-- (CAPTURA 1 — tabla principal del informe con columnas CENTRO DE COSTE · CUENTA · CONCEPTO · Notas cuenta. Pega aquí: ![Vista principal](assets/screenshots/01_main_table.png)) -->

<!-- (CAPTURA 2 — slicer con un centro seleccionado, ej. RESORTS, mostrando cuentas y empleados filtrados en paralelo. Pega aquí: ![Filtro activo](assets/screenshots/02_slicer_filtered.png)) -->

<!-- (CAPTURA 3 — visual de empleados con centro asignado y columna de comentarios de split. Pega aquí: ![Empleados](assets/screenshots/03_employees_view.png)) -->

<!-- (CAPTURA 4 — vista Modelo de Power BI Desktop con tablas COMBI, T_worker, t_ccoste y T_DADES y sus relaciones. Menú Vista → Modelo. Pega aquí: ![Modelo de datos](assets/screenshots/04_data_model.png)) -->

---

## 📁 Estructura del repositorio

```
📦 cost-center-tracker/
│
├── 📄 README.md
├── 📈 PBI_TABLAS_COSTES.pbix        ← Informe Power BI
├── 📊 XLS_TABLAS_COSTES.xlsx        ← Fuente de datos (datos sintéticos)
│
└── 📁 assets/
    └── 📁 screenshots/
        ├── 01_main_table.png
        ├── 02_slicer_filtered.png
        ├── 03_employees_view.png
        └── 04_data_model.png
```

---

## ⚡ Inicio rápido

```
1. Descarga PBI_TABLAS_COSTES.pbix y XLS_TABLAS_COSTES.xlsx
2. Abre el .pbix en Power BI Desktop
3. Inicio → Transformar datos → Configuración de origen de datos
4. Cambia el origen al archivo XLS_TABLAS_COSTES.xlsx descargado
5. Cerrar y aplicar → listo
```

> ⚠️ No renombres columnas ni tablas o las relaciones dejarán de funcionar.

---

## 🗂️ Modelo de datos

El informe pivota sobre una tabla central **`COMBI`**, resultado del cruce entre cuentas contables y empleados a través del centro de coste.

```
T_DADES  ──────┐
                ├── LEFT JOIN (CENTRO DE COSTE) ──► COMBI  ◄──  visuales del informe
T_worker ──────┘

t_ccoste ──► dimensión maestra de centros de coste
```

### Tablas del modelo

| Tabla | Rol | Filas |
|---|---|:---:|
| `COMBI` | Tabla de hechos principal · cruce cuenta × empleado | ~148 |
| `T_DADES` | Catálogo de cuentas contables con centro asignado | 50 |
| `T_worker` | Empleados, centros y comentarios de split | 18 |
| `t_ccoste` | Maestro de centros de coste con ID y descripción | 8 |
| `Hoja3` | Auxiliar · fórmulas `LEFT`/`RIGHT` para parsear cuentas | 50 |

### Columnas de `COMBI`

| Columna | Tipo | Descripción |
|---|---|---|
| `CENTRO DE COSTE` | Texto | Departamento o área funcional |
| `CUENTA` | Texto | Código contable (8 dígitos · PGC España) |
| `CONCEPTO` | Texto | Descripción literal de la cuenta |
| `NUMERO` | Entero | ID numérico del centro (1–7) |
| `T_WORKER.Empleado` | Texto | Nombre del empleado asignado |
| `T_WORKER.Coments` | Texto | Split de imputación si aplica (ej. 50/50) |
| `Notas cuenta` | Texto | Descripción del subgrupo PGC |
| `Notas worker` | Texto | Descripción funcional del centro |

---

## ⚙️ Cuentas contables — Subgrupos PGC

| Subgrupo | Naturaleza | Tipo |
|---|---|:---:|
| `629` | Otros gastos de gestión corriente · G&A · viajes | Gasto |
| `623` | Servicios de profesionales · contratación externa | Gasto |
| `642` | Seguridad Social a cargo de la empresa | Gasto |
| `649` | Otros gastos sociales · formación · seguros | Gasto |
| `755` | Ingresos por servicios al personal | Ingreso |
| `705` | Prestaciones de servicios · ingresos operativos | Ingreso |

---

## 🏗️ Qué puedes hacer con el informe

<table>
<tr>
<td width="50%">

**🔍 Buscar por empleado**

Selecciona un nombre en la visual de la izquierda y el canvas muestra al instante:
- Cuentas de su centro de coste
- Notas de cada cuenta
- Si tiene imputación compartida entre centros

</td>
<td width="50%">

**🏷️ Filtrar por centro de coste**

Usa el slicer y el informe muestra en paralelo:
- Todas las cuentas del departamento
- Los empleados asignados a ese centro
- Notas funcionales del área

</td>
</tr>
</table>

---

## 🧩 Centros de coste del modelo demo

| # | Centro | Descripción |
|:---:|---|---|
| 1 | **RESORTS** | Operaciones hoteleras · recepción · housekeeping · F&B |
| 2 | **SPA CENTERS** | Bienestar y terapias · coordinación wellness |
| 3 | **PEOPLE & TALENT** | RRHH · selección · formación · desarrollo organizativo |
| 4 | **DIGITAL & TECH** | Infraestructura tecnológica · sistemas · soporte digital |
| 5 | **BRAND & MARKETING** | Estrategia de marca global · campañas · comunicación |
| 6 | **EXPANSION** | Nuevas aperturas · desarrollo de activos |
| 7 | **FINANCE & CONTROL** | Control financiero · tesorería · reporting · auditoría |
| 1–7 | **ESPECIAL** | Transversal · imputaciones con split entre centros |

---

## 📋 Sobre los datos

- **100% datos sintéticos.** Empleados, cuentas y centros son ficticios y no corresponden a ninguna empresa real.
- Los códigos de cuenta respetan la estructura del PGC pero con numeración final modificada.
- El campo `Coments` representa imputaciones con split (ej. *"50% RESORTS - 50% FINANCE & CONTROL"*), útil para análisis de personal compartido entre departamentos.

---

## 🛠️ Requisitos

| Herramienta | Versión mínima |
|---|---|
| Power BI Desktop | 2024 o superior |
| Microsoft Excel | 2016 o superior |

---

<div align="center">

📄 Proyecto de demostración · uso libre · sin datos reales ni información confidencial

</div>
