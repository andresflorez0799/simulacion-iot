La **configuración balanceada** para una **finca mixta (cultivos + ganadería)**, pensada para **estabilidad operativa**, **consumo moderado** y **buen bienestar/productividad**, sin que el sistema “reaccione de más”.

---

## 🎯 Objetivo de la configuración balanceada

* Evitar ciclos frecuentes ON/OFF (desgaste y consumo).
* Mantener cultivos fuera de estrés hídrico.
* Proteger al ganado de calor excesivo.
* No agotar tanque ni batería.
* Generar **pocas alertas**, pero **relevantes**.

---

## ⚙️ Configuración recomendada (balanceada)

### 🌱 1. Humedad de suelo (Riego)

| Parámetro              | Valor           |
| ---------------------- | --------------- |
| **Umbral de riego**    | **30 %**        |
| Apagado por histéresis | 36 % (30 % + 6) |

**Por qué funciona bien**

* No espera a sequía crítica.
* No riega “por cualquier cosa”.
* Compatible con climas normales y transiciones a sequía.

✔️ Buen equilibrio entre **salud del cultivo** y **consumo de agua**.

---

### 🌡️ 2. Temperatura (Ventilación – ganadería)

| Parámetro              | Valor     |
| ---------------------- | --------- |
| **Umbral ventilación** | **32 °C** |
| Apagado                | 30 °C     |

**Por qué funciona bien**

* Actúa antes de estrés térmico severo.
* No mantiene ventilación constante.
* Evita consumo innecesario en horas templadas.

✔️ Balance entre **bienestar animal** y **energía**.

---

### 🚰 3. Nivel de tanque (Bomba)

| Parámetro        | Valor            |
| ---------------- | ---------------- |
| **Nivel mínimo** | **25 %**         |
| Apagado          | 43 % (25 % + 18) |

**Por qué funciona bien**

* Garantiza agua para riego y bebederos.
* Evita que el tanque caiga a niveles críticos.
* Reduce arranques excesivos de la bomba.

✔️ Balance entre **continuidad de servicio** y **vida útil del sistema**.

---

### 🧪 4. pH del suelo (Dosificación)

| Parámetro     | Valor   |
| ------------- | ------- |
| **pH mínimo** | **5.8** |
| **pH máximo** | **6.8** |

**Por qué funciona bien**

* Rango estándar para muchos cultivos.
* Evita correcciones constantes.
* Solo actúa cuando hay desviaciones reales.

✔️ Control agronómico **estable**, no agresivo.

---

### 🔋 5. Batería (seguridad energética)

| Regla         | Valor      |
| ------------- | ---------- |
| Modo ahorro   | < **20 %** |
| Corte crítico | < **10 %** |

**Efecto**

* Prioriza supervivencia del sistema.
* Evita quedar sin energía por automatizaciones “optimistas”.

✔️ Protege la **operación continua**.

---

## 🧠 Comportamiento esperado con esta configuración

### Escenario normal

* Riego: **1–2 ciclos cortos** al día.
* Ventilación: activa solo en picos de calor.
* Bomba: ciclos espaciados, tanque estable.
* Alertas: **bajas**, solo cuando algo realmente se sale de rango.

### Escenario seco

* Riego aumenta gradualmente.
* Tanque baja → bomba entra oportunamente.
* Sistema sigue estable sin entrar en “espiral”.

### Escenario lluvioso

* Riego se bloquea automáticamente.
* Humedad sube de forma natural.
* Consumo energético disminuye.

---

## 🧩 Conclusión final

Esta configuración es **balanceada** porque:

* 🔄 **Evita sobre-automatización**
* 🌾 **Protege cultivos**
* 🐄 **Cuida el ganado**
* 💧 **No desperdicia agua**
* 🔋 **Respeta la energía disponible**

Es ideal como **configuración base productiva**, y desde aquí puedes:

* Subir umbrales → enfoque más **conservador/protector**
* Bajarlos → enfoque más **ahorrador**
