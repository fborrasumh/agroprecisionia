# AgroPrecisiónIA

Laboratorio autónomo de agricultura de precisión: índices espectrales, calibración y zonas de manejo. Aplicación web de un solo fichero.

**Usar la app:** https://fborrasumh.github.io/agroprecisionia/

**Idiomas:** español (por defecto), inglés, portugués; selector en la barra superior (o `?lang=en` / `?lang=pt` en la URL).

## Qué hace

- **Práctica autónoma con corrección por código** de 11 habilidades vinculadas a cinco resultados de aprendizaje (RA1–RA5): área de una parcela por coordenadas UTM, píxeles y resolución, NDVI, interpretación del NDVI, SAVI, EVI, calibración del LAI por mínimos cuadrados, estimación del LAI, RMSE de validación, zonas de manejo y prescripción de dosis variable.
- **Ejercicios únicos y reproducibles**: cada ejercicio se genera con una semilla (seudónimo + habilidad + número). Quien tenga la app puede regenerar el mismo ejercicio sin guardar nada.
- **Diagnóstico de errores típicos por recálculo**: el código recalcula el ejercicio con los errores más frecuentes (signo cambiado, m² en lugar de ha, MSE en lugar de RMSE, regresión invertida…) y, si la respuesta coincide con uno, dice cuál es.
- **Ruta adaptativa explicable**: el dominio de cada habilidad se estima con los intentos recientes y decae con el tiempo. La siguiente actividad sigue reglas deterministas: repaso espaciado, refuerzo, contenido nuevo en el orden del curso e intercalado de habilidades. Siempre se muestra por qué toca cada actividad. Tras dos intentos fallidos se puede ver la solución resuelta paso a paso.
- **Datos de campo**: se pega o se sube un CSV del proyecto de dron. La app ajusta una regresión y calcula el R², el RMSE y el RMSE de validación cruzada dejando uno fuera, con avisos de muestra pequeña, valores atípicos y filas no válidas.
- **Plan de acción (RA5)**: la IA (opcional) lo comenta con cinco criterios y cita el plan literalmente. El código comprueba cada cita y avisa de las cifras que no están en el plan. No pone nota.
- **Evidencia**: un JSON con una huella SHA-256 para el profesor, un informe en Word y un CSV de intentos, todo generado sin conexión.
- **Profesorado**: carga las evidencias del grupo, detecta los ficheros editados y muestra la analítica por habilidad (acierto a la primera, error más frecuente y dominio medio). También propone mejoras que el profesor decide si aplica.
- Funciona **sin clave de IA y sin red**: toda la corrección es local. Incluye un ejemplo completo con una estudiante ficticia y un grupo de ejemplo para el profesorado.

## Cómo se usa la IA

La IA es **opcional** y nunca calcula ni pone nota. Se usa con la clave propia de OpenAI, Google Gemini o Anthropic Claude, que se guarda solo en el navegador; no hace falta servidor. Tiene dos usos:
1. **Explicar un error** sin dar el resultado. La IA no recibe la solución, y el código elimina cualquier frase de su respuesta que contenga una cifra igual a la solución.
2. **Comentar el plan de acción** con cinco criterios. Cada cita de la IA se comprueba contra el plan.

## Privacidad

Los ejercicios, el progreso, los datos de campo y el plan se guardan solo en el navegador (IndexedDB). Hacia el proveedor de IA solo sale lo que se pide comentar: el enunciado y la respuesta, o el plan con los correos y teléfonos enmascarados. Antes del primer envío se muestra lo que sale. Se recomienda un seudónimo en lugar del nombre. El fichero de evidencia lo entrega el propio estudiante; en el modo profesorado, los ficheros se leen en el navegador y no se guardan.

## Límites

- El dominio es una **estimación** para orientar el estudio, no una nota.
- El sílabo declara un único resultado de aprendizaje («Optimiza los sistemas de producción agropecuaria con el uso de la agricultura de precisión»). Los RA1–RA5 son una **propuesta de desglose**, pendiente de validación por el profesorado de la asignatura.
- Los ejercicios usan **datos simulados**. Las clases de NDVI son orientativas (dependen del cultivo, la fenología y el sensor). La prescripción del ejercicio de dosis es didáctica, no una recomendación agronómica.
- La huella SHA-256 detecta ediciones del fichero de evidencia, pero no es una prueba infalible: quien sepa puede recalcularla.
- No lee imágenes multiespectrales (GeoTIFF): trabaja con valores ya extraídos.
- **Sin evidencia de eficacia todavía**: medir su efecto en el aprendizaje exige un estudio con aprobación ética, consentimiento informado y, idealmente, un grupo de comparación.
- Antes de publicar conviene revisar el inglés y el portugués con hablantes nativos.

## Pruebas

```bash
node tests/nucleo_test.js           # lógica pura: fórmulas, 3 300 variantes por habilidad, errores típicos, modelo de dominio, CSV
python3 tests/flujo_test.py         # flujo completo con IA simulada que miente, exportaciones, profesorado, cobertura de traducciones
python3 tests/calidad_test.py       # WCAG 2.2 AA medible (contraste, nombres, etiquetas, objetivos, encabezados, teclado), sin red, CPU ×4, móvil
```

## Adaptar a otra asignatura

Los resultados de aprendizaje, las habilidades, las clases de NDVI, la prescripción y los parámetros del modelo de dominio están en `src/curriculum.js`. Los generadores de ejercicios están en `src/nucleo.js`.

## Autoría

Fernando Borrás Rocher (Universidad Miguel Hernández de Elche) y Paúl Santiago Ortiz Tirado (Universidad Politécnica Estatal del Carchi (UPEC), Ecuador).

## Origen de la idea

A partir del sílabo de Agricultura de Precisión (Carrera de Agropecuaria, nivel 9, UPEC, PAO 2026 B) del profesor Paúl Santiago Ortiz Tirado.

ORCID: Fernando Borrás Rocher [0000-0002-5519-4573](https://orcid.org/0000-0002-5519-4573) · Paúl Santiago Ortiz Tirado [0000-0001-5004-1466](https://orcid.org/0000-0001-5004-1466)

## Cómo citar

Borrás Rocher, F. y Ortiz Tirado, P. (2026). *AgroPrecisiónIA* (v1.0.0) [Software]. (DOI en trámite)

## Licencia

MIT. Véase [LICENSE](LICENSE).
