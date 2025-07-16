# BalanceApp
Herramienta BalanceApp

**Para el ejemplo con Kikuyo (3.6% grasa):**
```
Factor Energía = 0.64 Mcal/L
Factor Proteína = 78 g/L

Aporte ENl Concentrado = 11.23 × 1.7 = 19.09 Mcal
Aporte PB Concentrado = 11.23 × 16 × 10 = 1796.8 g

Energía Disponible = (17.02 + 19.09) - 9.94 = 26.17 Mcal
Proteína# BalanceApp - Guía de Usuario
## Aplicación para balanceamiento de ración de vacas lecheras en producción

**Desarrollado por:** GrICA, Facultad de Ciencias Agrarias, Universidad de Antioquia  
**Versión Web:** 2025

---

## 1. Entrada de Datos del Animal

### Datos requeridos:
- **Peso de la vaca (kg):** Peso corporal actual del animal
- **Producción de leche (litros/día):** Producción diaria promedio
- **Grasa (%):** Porcentaje de grasa en la leche
- **Días en leche (DEL):** Días transcurridos desde el parto
- **Proporción Forraje (%):** Porcentaje de forraje en la dieta total
- **Fórmula CMS:** Selección de fórmula para calcular consumo de materia seca

### Cálculos iniciales:
```
Semana de lactancia = DEL ÷ 7
FCM = (0.4 × Producción de leche) + (15 × (Producción de leche × (Grasa ÷ 100)))
Proporción concentrado = 100 - Proporción forraje
```

**Ejemplo:**
- Peso: 620 kg
- Producción: 37 litros
- Grasa: 3.6%
- DEL: 180 días
- Forraje: 60%

```
Semana lactancia = 180 ÷ 7 = 25.7 semanas
FCM = (0.4 × 37) + (15 × (37 × (3.6 ÷ 100))) = 14.8 + 19.98 = 34.78 kg
Concentrado = 100 - 60 = 40%
```

---

## 2. Requerimientos de Mantenimiento

Los requerimientos se calculan mediante interpolación lineal según rangos de peso:

### Fórmulas por rango de peso:

**400-450 kg:**
```
EMant = 7.16 - ((450 - Peso) × (7.82 - 7.16)) ÷ (450 - 400)
ProtMant = 318 - ((450 - Peso) × (341 - 318)) ÷ (450 - 400)
CaMant = 16 - ((450 - Peso) × (18 - 16)) ÷ (450 - 400)
PMant = 11 - ((450 - Peso) × (13 - 11)) ÷ (450 - 400)
```

**450-500 kg:**
```
EMant = 8.46 - ((500 - Peso) × (8.46 - 7.82)) ÷ (500 - 450)
ProtMant = 341 - ((500 - Peso) × (364 - 341)) ÷ (500 - 450)
CaMant = 18 - ((500 - Peso) × (20 - 18)) ÷ (500 - 450)
PMant = 13 - ((500 - Peso) × (14 - 13)) ÷ (500 - 450)
```

**500-550 kg:**
```
EMant = 9.09 - ((550 - Peso) × (9.09 - 8.46)) ÷ (550 - 500)
ProtMant = 364 - ((550 - Peso) × (386 - 364)) ÷ (550 - 500)
CaMant = 20 - ((550 - Peso) × (22 - 20)) ÷ (550 - 500)
PMant = 14 - ((550 - Peso) × (16 - 14)) ÷ (550 - 500)
```

**550-600 kg:**
```
EMant = 9.7 - ((600 - Peso) × (9.7 - 9.09)) ÷ (600 - 550)
ProtMant = 386 - ((600 - Peso) × (406 - 386)) ÷ (600 - 550)
CaMant = 22 - ((600 - Peso) × (24 - 22)) ÷ (600 - 550)
PMant = 16 - ((600 - Peso) × (17 - 16)) ÷ (600 - 550)
```

**600-650 kg:**
```
EMant = 10.3 - ((650 - Peso) × (10.3 - 9.7)) ÷ (650 - 600)
ProtMant = 406 - ((650 - Peso) × (428 - 406)) ÷ (650 - 600)
CaMant = 24 - ((650 - Peso) × (26 - 24)) ÷ (650 - 600)
PMant = 17 - ((650 - Peso) × (19 - 17)) ÷ (650 - 600)
```

**650-700 kg:**
```
EMant = 10.89 - ((700 - Peso) × (10.89 - 10.3)) ÷ (700 - 650)
ProtMant = 428 - ((700 - Peso) × (449 - 428)) ÷ (700 - 650)
CaMant = 26 - ((700 - Peso) × (28 - 26)) ÷ (700 - 650)
PMant = 19 - ((700 - Peso) × (20 - 19)) ÷ (700 - 650)
```

**700 kg:**
```
EMant = 10.89
ProtMant = 449
CaMant = 28
PMant = 20
```

**Para el ejemplo (620 kg):**
```
EMant = 10.3 - ((650 - 620) × (10.3 - 9.7)) ÷ (650 - 600) = 9.94 Mcal
ProtMant = 406 - ((650 - 620) × (428 - 406)) ÷ (650 - 600) = 392.8 g
CaMant = 24 - ((650 - 620) × (26 - 24)) ÷ (650 - 600) = 22.8 g
PMant = 17 - ((650 - 620) × (19 - 17)) ÷ (650 - 600) = 15.8 g
```

---

## 3. Requerimientos de Producción

Los requerimientos se calculan según el porcentaje de grasa en la leche:

### Fórmulas por rango de grasa:

**3.0-3.5%:**
```
EPdn = (0.69 - ((3.5 - Grasa) × (0.69 - 0.64)) ÷ (3.5 - 3)) × Producción
ProtPdn = (84 - ((3.5 - Grasa) × (84 - 78)) ÷ (3.5 - 3)) × Producción
CaPdn = (2.97 - ((3.5 - Grasa) × (2.97 - 2.73)) ÷ (3.5 - 3)) × Producción
PPdn = (1.83 - ((3.5 - Grasa) × (1.83 - 1.68)) ÷ (3.5 - 3)) × Producción
```

**3.5-4.0%:**
```
EPdn = (0.74 - ((4 - Grasa) × (0.74 - 0.69)) ÷ (4 - 3.5)) × Producción
ProtPdn = (90 - ((4 - Grasa) × (90 - 84)) ÷ (4 - 3.5)) × Producción
CaPdn = (3.21 - ((4 - Grasa) × (3.21 - 2.97)) ÷ (4 - 3.5)) × Producción
PPdn = (1.96 - ((4 - Grasa) × (1.96 - 1.83)) ÷ (4 - 3.5)) × Producción
```

**4.0-4.5%:**
```
EPdn = (0.78 - ((4.5 - Grasa) × (0.78 - 0.74)) ÷ (4.5 - 4)) × Producción
ProtPdn = (96 - ((4.5 - Grasa) × (96 - 90)) ÷ (4.5 - 4)) × Producción
CaPdn = (3.45 - ((4.5 - Grasa) × (3.45 - 3.21)) ÷ (4.5 - 4)) × Producción
PPdn = (2.13 - ((4.5 - Grasa) × (2.13 - 1.96)) ÷ (4.5 - 4)) × Producción
```

**4.5-5.0%:**
```
EPdn = (0.83 - ((5 - Grasa) × (0.83 - 0.78)) ÷ (5 - 4.5)) × Producción
ProtPdn = (101 - ((5 - Grasa) × (101 - 96)) ÷ (5 - 4.5)) × Producción
CaPdn = (3.69 - ((5 - Grasa) × (3.69 - 3.45)) ÷ (5 - 4.5)) × Producción
PPdn = (2.28 - ((5 - Grasa) × (2.28 - 2.13)) ÷ (5 - 4.5)) × Producción
```

**5.0-5.5%:**
```
EPdn = (0.88 - ((5.5 - Grasa) × (0.88 - 0.83)) ÷ (5.5 - 5)) × Producción
ProtPdn = (107 - ((5.5 - Grasa) × (107 - 101)) ÷ (5.5 - 5)) × Producción
CaPdn = (3.93 - ((5.5 - Grasa) × (3.93 - 3.69)) ÷ (5.5 - 5)) × Producción
PPdn = (2.43 - ((5.5 - Grasa) × (2.43 - 2.28)) ÷ (5.5 - 5)) × Producción
```

**5.5%:**
```
EPdn = 0.88 × Producción
ProtPdn = 107 × Producción
CaPdn = 3.93 × Producción
PPdn = 2.43 × Producción
```

**Para el ejemplo (3.6% grasa, 37 L):**
```
EPdn = (0.74 - ((4 - 3.6) × (0.74 - 0.69)) ÷ (4 - 3.5)) × 37 = 23.68 Mcal
ProtPdn = (90 - ((4 - 3.6) × (90 - 84)) ÷ (4 - 3.5)) × 37 = 2886 g
CaPdn = (3.21 - ((4 - 3.6) × (3.21 - 2.97)) ÷ (4 - 3.5)) × 37 = 101.01 g
PPdn = (1.96 - ((4 - 3.6) × (1.96 - 1.83)) ÷ (4 - 3.5)) × 37 = 62.16 g
```

---

## 4. Requerimientos Totales

```
Req ENl Total = EPdn + EMant
Req Proteína Total = ProtPdn + ProtMant
Req Calcio Total = CaPdn + CaMant
Req Fósforo Total = PPdn + PMant
```

**Para el ejemplo:**
```
Req ENl = 23.68 + 9.94 = 33.62 Mcal
Req Proteína = 2886 + 392.8 = 3278.8 g
Req Calcio = 101.01 + 22.8 = 123.81 g
Req Fósforo = 62.16 + 15.8 = 77.96 g
```

---

## 5. Consumo de Materia Seca (CMS)

La aplicación ofrece 5 fórmulas diferentes:

### Fórmula 0 - NRC 2001:
```
CMS = ((Peso^0.75 × 0.0968) + (0.372 × FCM) - 0.293) × (1^(-0.192 × (Semana lactancia + 3.67)))
```

### Fórmula 1 - NRC Modificada:
```
CMS = (0.372 × FCM + (0.0968 × Peso^0.75)) × (1^(-0.192 × (Semana lactancia + 3.67)))
```

### Fórmula 2 - NRC2:
```
CMS = 0.29 + (0.372 × FCM) + (0.0968 × Peso^0.75)
```

### Fórmula 3 - NRC3:
```
CMS = (0.025 × Peso) + (0.1 × Producción) + 0.88 - (0.4 × 0.88)
```

### Fórmula 4 - Israel:
```
CMS = (0.025 × Peso) + (0.1 × Producción)
```

**Para el ejemplo (Fórmula 0):**
```
CMS = ((620^0.75 × 0.0968) + (0.372 × 34.78) - 0.293) × (1^(-0.192 × (25.7 + 3.67)))
CMS = 24.7 kg/día
```

---

## 6. Selección de Tipo de Pasto

### Tipos de pasto disponibles para Colombia:

#### **Kikuyo (Cenchrus clandestinus):**
| Nutriente | % | Cd (%) |
|-----------|---|--------|
| PC        | 20.5 | 45 |
| FDN       | 58.1 | 55 |
| FDA       | 30.3 | 38 |
| LDA       | 11.0 | 1 |
| EE        | 3.63 | 35 |
| Cenizas   | 10.6 | 36 |
| CNE       | 13.4 | 80 |
| Ca        | 0.35 | 68 |
| P         | 0.38 | 77 |
| MS        | 14.0 | - |
| ENl       | 1.15 | - |

#### **Ryegrass (Lolium perenne):**
| Nutriente | % | Cd (%) |
|-----------|---|--------|
| PC        | 24.21 | 70 |
| FDN       | 49.6 | 60 |
| FDA       | 25.57 | 60 |
| LDA       | 3.29 | 1 |
| EE        | 3.63 | 35 |
| Cenizas   | 10.6 | 36 |
| CNE       | 15.4 | 80 |
| Ca        | 0.35 | 68 |
| P         | 0.38 | 77 |
| MS        | 16.0 | - |
| ENl       | 1.35 | - |

#### **Mezcla Kikuyo-Ryegrass:**
La aplicación permite configurar proporciones variables de la mezcla. Los valores se calculan mediante promedio ponderado:

```
Valor Mezcla = (Valor Kikuyo × % Kikuyo) + (Valor Ryegrass × % Ryegrass)
```

**Ejemplo mezcla 60% Kikuyo - 40% Ryegrass:**
```
PC Mezcla = (20.5 × 0.6) + (24.21 × 0.4) = 21.984%
Cd PC Mezcla = (0.45 × 0.6) + (0.7 × 0.4) = 0.55 (55%)
```

### Cálculo de aportes con coeficientes de digestibilidad:

```
Aporte Proteína Digestible = CMS × (PC pasto × Cd PC ÷ 100) × 1000
Aporte Ca Digestible = CMS × (Ca pasto × Cd Ca ÷ 100) × 1000
Aporte P Digestible = CMS × (P pasto × Cd P ÷ 100) × 1000
```

**Diferencias importantes entre pastos:**
- **Ryegrass:** Mayor digestibilidad proteica (70% vs 45%), mayor MS, mayor ENl
- **Kikuyo:** Menor calidad pero más resistente a condiciones adversas
- **Mezcla:** Permite optimizar según disponibilidad y condiciones del predio

---

## 7. Composición Nutricional de Alimentos

### Pasto:
Los valores dependen del tipo seleccionado (ver sección anterior). La aplicación usa automáticamente la composición correspondiente y aplica los coeficientes de digestibilidad.

### Concentrado:
- **Materia Seca:** 88%
- **Proteína Bruta:** 16%
- **Energía Neta:** 1.7 Mcal/kg MS
- **FDN:** 18.8%
- **Calcio:** 1.78%
- **Fósforo:** 0.34%

---

## 8. Aportes del Pasto

```
Aporte ENl Pasto = CMS × (% Forraje ÷ 100) × ENl pasto
Aporte PB Pasto = CMS × (PC pasto × Cd PC ÷ 100) × 1000
Aporte Ca Pasto = CMS × (Ca pasto × Cd Ca ÷ 100) × 1000
Aporte P Pasto = CMS × (P pasto × Cd P ÷ 100) × 1000
```

**Para el ejemplo con Kikuyo:**
```
Aporte ENl = 24.7 × (60 ÷ 100) × 1.15 = 17.02 Mcal
Aporte PB = 24.7 × (20.5 × 0.45 ÷ 100) × 1000 = 2279.3 g
Aporte Ca = 24.7 × (0.35 × 0.68 ÷ 100) × 1000 = 58.8 g
Aporte P = 24.7 × (0.38 × 0.77 ÷ 100) × 1000 = 72.3 g
```

**Comparación con Ryegrass:**
```
Aporte PB = 24.7 × (24.21 × 0.7 ÷ 100) × 1000 = 4192.5 g
```
*Nota la diferencia significativa en aporte proteico debido a mayor PC y digestibilidad*

---

## 9. Balance Nutricional

```
Balance ENl = Aporte ENl Pasto - Req ENl Total
Balance PB = Aporte PB Pasto - Req Proteína Total
Balance Ca = Aporte Ca Pasto - Req Calcio Total
Balance P = Aporte P Pasto - Req Fósforo Total
```

**Para el ejemplo con Kikuyo:**
```
Balance ENl = 17.02 - 33.62 = -16.60 Mcal (DÉFICIT)
Balance PB = 2279.3 - 3278.8 = -999.5 g (DÉFICIT)
Balance Ca = 58.8 - 123.81 = -65.01 g (DÉFICIT)
Balance P = 72.3 - 77.96 = -5.66 g (DÉFICIT)
```

---

## 10. Suplementación con Concentrado

### Cantidad total de concentrado:
```
Kg Concentrado = CMS × (% Concentrado ÷ 100) × (1 ÷ MS concentrado)
```

### Concentrado requerido por nutriente (solo si hay déficit):
```
Kg por ENl = |Balance ENl| ÷ ENl concentrado
Kg por PB = |Balance PB| ÷ (PB concentrado × 10)
Kg por Ca = |Balance Ca| ÷ (Ca concentrado × 10)
Kg por P = |Balance P| ÷ (P concentrado × 10)
```

**Para el ejemplo con Kikuyo:**
```
Kg Concentrado Total = 24.7 × (40 ÷ 100) × (1 ÷ 0.88) = 11.23 kg

Concentrado por déficit:
- ENl: 16.60 ÷ 1.7 = 9.76 kg
- PB: 999.5 ÷ (16 × 10) = 6.25 kg
- Ca: 65.01 ÷ (1.78 × 10) = 3.65 kg
- P: 5.66 ÷ (0.34 × 10) = 1.66 kg
```

---

## 11. Índices de Producción Potencial

### Energy Allowed Milk (EAM) - Leche Permitida por Energía:
```
Energía Disponible Producción = (Aporte ENl Pasto + Aporte ENl Concentrado) - EMant
Energy Allowed Milk = Energía Disponible Producción ÷ Factor Energía por Litro
```

### Protein Allowed Milk (PAM) - Leche Permitida por Proteína:
```
Proteína Disponible Producción = (Aporte PB Pasto + Aporte PB Concentrado) - ProtMant
Protein Allowed Milk = Proteína Disponible Producción ÷ Factor Proteína por Litro
```

### Factores de Conversión por % de Grasa:
Los factores se calculan con las mismas fórmulas de interpolación usadas en requerimientos de producción.

**Para el ejemplo (3.6% grasa):**
```
Factor Energía = 0.64 Mcal/L
Factor Proteína = 78 g/L

Aporte ENl Concentrado = 11.23 × 1.7 = 19.09 Mcal
Aporte PB Concentrado = 11.23 × 16 × 10 = 1796.8 g

Energía Disponible = (17.02 + 19.09) - 9.94 = 26.17 Mcal
Proteína Disponible = (2445.3 + 1796.8) - 392.8 = 3849.3 g

Energy Allowed Milk = 26.17 ÷ 0.64 = 40.9 L
Protein Allowed Milk = 3849.3 ÷ 78 = 49.4 L
```

### Factores Limitantes:
```
Factor Limitante Energía = (EAM ÷ Producción Actual) × 100
Factor Limitante Proteína = (PAM ÷ Producción Actual) × 100
```

**Para el ejemplo:**
```
Factor Energía = (40.9 ÷ 37) × 100 = 110.5%
Factor Proteína = (49.4 ÷ 37) × 100 = 133.5%
```

### Interpretación:
- **Factor > 100%:** El nutriente NO es limitante para la producción
- **Factor < 100%:** El nutriente SÍ es limitante para la producción
- **Factor más bajo:** Indica el nutriente más limitante en la dieta

---

## 11. Consumo de Forraje Verde

```
Consumo FV = CMS × (% Forraje ÷ 100) ÷ MS pasto
```

**Para el ejemplo:**
```
Consumo FV = 24.7 × (60 ÷ 100) ÷ 0.14 = 105.86 kg/día
```

---

## 12. Interpretación de Resultados

### Códigos de color en la aplicación:
- **Verde:** Exceso o balance positivo
- **Rojo:** Déficit o balance negativo

### Recomendaciones generales:
1. **Si hay déficit energético:** Aumentar concentrado o mejorar calidad del forraje
2. **Si hay déficit proteico:** Usar concentrados con mayor PB o suplementos proteicos
3. **Si hay déficit mineral:** Considerar suplementación mineral específica
4. **Consumo FV excesivo:** Puede indicar baja MS del pasto o sobreestimación
5. **Factor limitante energía <100%:** Incrementar energía de la dieta (más concentrado/mejor forraje)
6. **Factor limitante proteína <100%:** Incrementar proteína de la dieta (concentrados proteicos)
7. **Ambos factores >100%:** La dieta permite mayor producción, evaluar otros factores limitantes

### Limitaciones del modelo:
- Asume composición promedio de alimentos
- No considera variaciones individuales del animal
- No incluye factores ambientales (estrés térmico, etc.)
- Digestibilidad del pasto asumida como constante

### Recomendaciones para uso en campo:
- Realizar análisis bromatológicos del forraje disponible
- Ajustar composición del concentrado según disponibilidad local
- Monitorear condición corporal y producción real
- Considerar suplementación mineral independiente
