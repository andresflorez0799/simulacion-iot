## Demostracion

<a href="https://andresflorez0799.github.io/simulacion-iot/" target="_blank" rel="noopener noreferrer">Click aqui para visitar Demostración:</a>

### Resumen general de la simulación IoT (finca)

La simulación representa un flujo IoT típico en una finca mixta (cultivo + ganadería):

1. **Sensores** capturan telemetría (humedad de suelo, temperatura, lluvia, tanque, pH, batería).
2. Un **gateway** recibe/normaliza y “envía” (simulado) a la nube.
3. Un **motor de reglas** decide acciones (actuadores) en modo **Automático**.
4. **Actuadores** ejecutan acciones: riego, ventilación, bomba, dosificador.
5. Se generan **eventos**: telemetría, alertas y comandos.

En modo **Manual**, los actuadores se pueden encender/apagar, pero con **bloqueos mínimos** de seguridad (p. ej. no activar riego si llueve, y no activar cargas con batería crítica).

---

## Qué pasa si manipulas los rangos (umbrales) y cómo cambian los actuadores

En la práctica, al mover umbrales “mueves la sensibilidad” del sistema. Eso afecta **frecuencia de activaciones**, **duración de ON**, **consumo de agua/energía**, y **cantidad de alertas**.

### 1) Riego (controlado por umbral de humedad y lluvia)

**Regla base (AUTO):**

* Si **llueve** ⇒ riego **OFF**.
* Si **humedad < umbral** y **tanque > 10%** y **batería > 10%** ⇒ riego **ON**.
* Si humedad sube a **umbral + 6** ⇒ riego **OFF** (histéresis).

**Si subes el umbral de humedad (ej. de 28% a 45%)**

* El sistema considera “seco” más pronto ⇒ **riego ON con más frecuencia**.
* Resultado típico: **más consumo de agua**, tanque baja más rápido, **bomba puede activarse más**.
* Beneficio: cultivos más “seguros” contra sequía.
* Riesgo: si te pasas, terminas en “ciclo de riego” (riego/bomba más constante).

**Si bajas el umbral (ej. 28% a 15%)**

* Riego se activa tarde ⇒ **menos consumo de agua**.
* Riesgo: el cultivo puede pasar más tiempo en estrés hídrico (humedad baja) antes de que el sistema reaccione.

**Conclusión práctica:**

* Umbral alto = “protección” (pero más gasto).
* Umbral bajo = “ahorro” (pero más riesgo para el cultivo).

---

### 2) Ventilación (temperatura corral/invernadero)

**Regla base (AUTO):**

* Si **temp > umbral** y **batería > 10%** ⇒ ventilación **ON**.
* Si temp baja a **umbral - 2** ⇒ ventilación **OFF** (histéresis).

**Si bajas el umbral (ej. 33°C a 26°C)**

* Ventilación entra rápido ⇒ **más confort animal**, menos estrés térmico.
* Coste: **más consumo de batería/energía**, y sube la probabilidad de entrar en modo ahorro.

**Si subes el umbral (ej. 33°C a 40°C)**

* Ventilación casi nunca se activa ⇒ **ahorras energía**.
* Riesgo: temperaturas elevadas sostenidas ⇒ **mayor estrés y menor bienestar/producción** (ganado más afectado).

**Conclusión práctica:**

* Umbral bajo = bienestar ↑ / energía ↓
* Umbral alto = energía ↑ / bienestar ↓

---

### 3) Bomba (nivel de tanque)

**Regla base (AUTO):**

* Si **tanque < umbral** y **batería > 12%** ⇒ bomba **ON**
* Si tanque sube a **umbral + 18** ⇒ bomba **OFF** (histéresis)

**Si subes el umbral (ej. 25% a 50%)**

* La bomba se activa con más frecuencia y por más tiempo ⇒ tanque se mantiene alto.
* Pero consumes más energía y “ciclas” más el sistema.

**Si bajas el umbral (25% a 10%)**

* La bomba se prende tarde ⇒ **menos consumo**, pero el tanque pasa más tiempo bajo.
* Riesgo: quedarte “corto” de agua justo cuando riego o bebederos lo necesitan (además, riego requiere tanque > 10% para encender).

**Conclusión práctica:**

* Umbral alto = continuidad de agua ↑ / energía ↓
* Umbral bajo = energía ↑ / riesgo de desabastecimiento ↑

---

### 4) Dosificador de fertilizante (por pH fuera de rango)

**Regla base (AUTO):**

* Si pH fuera de [min, max] ⇒ alerta + **dosificación ON por 3 ticks**, luego OFF.

**Si estrechas el rango (ej. 6.0–6.5)**

* pH “fuera de rango” más a menudo ⇒ más alertas y dosificaciones.
* Riesgo: sobreactuar (demasiadas correcciones).

**Si amplías el rango (ej. 5.5–7.2)**

* Menos alertas y menos dosificación.
* Riesgo: el suelo puede desviarse más sin corrección.

**Conclusión práctica:**

* Rango estrecho = control fino (pero más intervención)
* Rango amplio = estabilidad operativa (pero menos precisión agronómica)

---

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


## Conclusiones generales al manipular rangos

1. **Los umbrales definen la “sensibilidad” del sistema.**
   Umbrales más exigentes (más altos o rangos más estrechos) hacen que el sistema **actúe más**, con más eventos, consumo y ciclos.
2. **Histéresis evita el “parpadeo” ON/OFF**, pero igual puedes generar ciclos si el umbral queda muy agresivo.
   * Riego usa **umbral + 6** para apagar.
   * Ventilación usa **umbral - 2** para apagar.
   * Bomba usa **umbral + 18** para apagar.
3. **Riego y bomba están acoplados**: si subes el umbral de humedad, el riego se usa más ⇒ el tanque cae ⇒ la bomba se usa más.
   Un ajuste “inocente” en humedad puede disparar el consumo de energía por la bomba.
4. **La batería es el “freno de seguridad”.**
   Con batería baja, el sistema apaga actuadores (y en manual bloquea ON), lo que puede dejarte sin riego/ventilación/bombeo aunque los umbrales lo pidan.
5. **Mejor práctica:** ajustar umbrales en parejas (humedad ↔ tanque ↔ batería), no aislados.
   * Subes humedad ⇒ revisa tanque mínimo y batería.
   * Bajas temperatura ⇒ revisa batería/energía disponible.

