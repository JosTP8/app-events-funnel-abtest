# Embudo de Eventos y A/A/B Test en App Móvil

Proyecto de analítica de producto para una app de pedidos: se estudia el embudo
(Main → Offers → Cart → Payment) y se evalúa un experimento **A/A/B** que cambia la tipografía.

## 🎯 Objetivos
- Medir el embudo de conversión y detectar cuellos de botella.
- Verificar que los dos grupos de control (A/A) se comportan igual.
- Comparar el grupo experimental (B) frente a controles mediante pruebas de proporciones (Z-test).

## 📂 Datos
- Archivo: `logs_exp_us.csv` (del curso TripleTen).
- Columnas: `EventName`, `DeviceIDHash`, `EventTimestamp`, `ExpId`.
- **No se sube el CSV** por licencia/tamaño. Ver `data/README.md` para obtención local.

## 🛠️ Metodología
1. Limpieza y enriquecimiento:
   - Renombrado de columnas (`event`, `user_id`, `timestamp`, `group`).
   - Conversión de `timestamp` a `datetime` y `date`.
   - Corte de fechas iniciales con bajo volumen (desde **2019‑07‑31**).
2. Embudo:
   - Conteo de usuarios únicos por evento y tasas de paso entre etapas.
3. A/A/B:
   - Z-test de proporciones entre 246 vs 247 (controles).
   - Z-test de 248 vs controles combinados (246+247) por evento.
   - Discusión de significancia y riesgo de falsos positivos.

## 📈 Hallazgos (resumen)
- Conversión total Main → Payment ~ **47.7%**.
- Mayor caída: **Main → Offers (~62%)**.
- Controles 246 vs 247: **sin diferencias** significativas.
- 248 vs (246+247): **sin diferencias** significativas en eventos clave → el cambio de fuente **no impacta** el comportamiento.

## ▶️ Reproducibilidad
```bash
pip install -r requirements.txt
jupyter notebook notebook.ipynb
