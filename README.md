# Petróleos Mexicanos
Data analysis project exploring insights and trends in Mexico's petroleum industry

<img src="assets/img/project4-oil.png" width="400" height="400"/>

Image from [freepik](https://www.freepik.com/free-vector/offshore-oil-rig-raw-materials-fossil-extraction-equipment-heavy-machinery-smoking-chimneys-ocean-platform_25273103.htm#fromView=keyword&page=1&position=7&uuid=9c068652-659d-4c80-8b6e-91e9d7a183e2&query=Oil+Rig+Cartoon)

## Table Of Contents
- [Executive Summary](#executive-summary)
  - [Primary Goal](#primary-goal)
  - [Solution](#solution)
  - [Key Findings](#key-findings)
  - [Recommendations](#recommendations)
- [Introduction](#introduction)
  - [Business Problem](#business-problem)
  - [Goals](#goals)
- [Methodology](#methodology)
  - [Data Source](#data-source)
  - [Tools](#tools)
  - [Data Cleaning and Transformation](#data-cleaning-and-transformation)
  - [Data Analysis](#data-analysis)
  - [Data Visualisation](#data-visualisation)
- [Insights](#insights)
- [Action Plan](#action-plan)	 
- [Report](#report)	


## Executive Summary
### Primary Goal

### Solution

### Key Findings

### Recommendations

## Introduction
### Business Problem

### Goals

## Methodology
### Data source
For this project, the datasets were downloaded from the [Plataforma Nacional de Datos Abiertos](https://www.datos.gob.mx/), Mexico’s National Open Data Platform. As of May 2025, this website has been modified, and an [historic data archive](https://historico.datos.gob.mx/) is now available, allowing users to search additional databases from Mexican government institutions. 

To gather relevant data, I searched for the term "petróleo", which returned over 90 results, including datasets and official documents published by **PEMEX (Petróleos Mexicanos), SENER (Secretaría de Energía), INEGI (INstituto Nacional de Estadística y Geografía)** other Mexican government institutions.

For this project’s scope, I selected **14 datasets**, all related to Mexico’s petroleum, gas, and oil industry. You can access the original datasets through [this Github repository](https://github.com/alejandralopezgalan/petroleos-mexicanos/tree/main/assets/datasets/raw) and [this Google Drive Folder](https://drive.google.com/drive/folders/1Ht727_UwEuUORxWzpP4smzny2tHzYurv?usp=sharing).

A brief description of each dataset is provided below. Most of the data was recorded monthly from January 2010 to February 2023.
| File | Description | 
| :--- | :--- |
| `SENER_05_ComercioExteriorGasNaturalImportacionExportacion-PMXE1C12_data.csv` | External trade of natural gas, measured by volume (in millions of cubic feet per day) and value (in millions of US dollars). | 
| `SENER_05_ElaboracionProductosPetroliferos-PMXD1C01_data.csv` | Production of petroleum products by category, measured in thousands of barrels per day | 
| `SENER_05_ElaboracionProductosPetroquimicosDerivadosMetano-PMXD2C01_data.csv` | Production of petroleum products by category, measured in thousands of tons per day.  | 
| `SENER_05_ImportacionesGasLicuadoPropanoButanoPuntoInternacion-PMXE2C12_data` | Import volume of liquefied gas, propane, and butane by entry point, measured in thousands of barrels per day. | 
| `SENER_05_PerforacionPozosPorRegion-PMXAC02_data.csv` | Count of oil well drillings. | 
| `SENER_05_ProduccionPetroleoCrudoPorActivosRegion-PMXB1C05_data.csv` | Crude oil production by region, measured in thousands of barrels per day. | 
| `SENER_05_ProduccionPetroleoCrudoPorEntidadFederativa-PMXB1C02_data.csv` |  Crude oil production by state, measured in thousands of barrels per day. | 
| `SENER_05_ValorComercioIntTipoDeHidrocarburosSusDerivados-PMXF4C02_data.csv` | Monetary value of petroleum product imports and exports, measured in millions of US dollars. | 
| `SENER_05_ValorExportacionesPetroleoCrudoPorDestinoGeografico-PMXF1C02_data.csv` | Value of petroleum product exports by geographical destination, measured in millions of US dollars.  | 
| `SENER_05_VolumenImportacionPorTipoPetroliferos-PMXE2C15_data.csv` | Import volume of certain petroleum products, measured in thousands of barrels per day..  | 
| `SENER_05_VolumenVentasPorTipoPetroliferos-PMXE2C01_data.csv` | Sales volume of certain petroleum products, measured in thousands of barrels per day. | 
| `Historico_Precios_Expendios_2023.csv` | Daily retail price of petroleum products by authorised sellers in 2023. | 
| `Historico_Precios_Expendios_2024.csv` | Daily retail price of petroleum products by authorised sellers in 2024. | 
| `Historico_Precios_Expendios_2025.csv` | Daily retail price of petroleum products by authorised sellers in 2025. | 



### Tools
- Excel: Used for initial exploring, cleaning, and formatting the data.
- Microsoft SQL Server: used for data analysis.
- Power BI: To built a dashboard.


### Data Cleaning and Transformation
#### Standarising Dates in Excel
In the initial data exploration, I found that in all the datasets there was a Date column with values like ene-05, Feb-05, Mar-05, abr-05. When converting them to a Date format in Excel, some cells were recognised correctly, but others were not. After reviewing the data, I realised that these values were monthly dates. To ensure consistency and prevent errors, I turned to the EDATE function in Excel.

Here’s how it works:
`EDATE(start_date, months)` shifts a date forward or backwards by a specified number of months. Since I needed all dates to follow a consistent format, such as 01/01/2010, 01/02/2010, 01/03/2010, I applied the formula:
`=EDATE(A2, 1)`

This helped standardise the datasets while adding one month to each value. I applied this transformation to the following datasets: `SENER_05_ComercioExteriorGasNaturalImportacionExportacion-PMXE1C12_data.csv`, `SENER_05_ElaboracionProductosPetroliferos-PMXD1C01_data.csv`, `SENER_05_ElaboracionProductosPetroquimicosDerivadosMetano-PMXD2C01.csv`, `SENER_05_ImportacionesGasLicuadoPropanoButanoPuntoInternacion-PMXE2C12`, `SENER_05_PerforacionPozosPorRegion-PMXAC02.csv`, `SENER_05_ProduccionPetroleoCrudoPorActivosRegion-PMXB1C05.csv`, `SENER_05_ProduccionPetroleoCrudoPorEntidadFederativa-PMXB1C02`, `SENER_05_ValorComercioIntTipoDeHidrocarburosSusDerivados-PMXF4C02.csv`, `SENER_05_ValorExportacionesPetroleoCrudoPorDestinoGeografico-PMXF1C02.csv`, `SENER_05_VolumenImportacionPorTipoPetroliferos-PMXE2C15.csv`, `SENER_05_VolumenVentasPorTipoPetroliferos-PMXE2C01.csv`. 

#### SQL
In Microsoft SQL Server Management Studio I created the database `pemex_db`

### Data Analysis




### Data Visualisation



## Insights


## Action plan



## Report
To review the analysis in detail, you can download the Report here.

