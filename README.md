# Sistema de Alerta Temprana de Riesgo Socioeconómico Provincial

> Trabajo Fin de Grado · Business Analytics · Universidad Francisco de Vitoria · Curso 2025–2026

Dashboard interactivo de prevención social proactiva basado en modelos predictivos y análisis de datos de panel para la criminalidad patrimonial en las 52 provincias de España.

**Autor:** Eduardo López López
**Tutor:** Alfonso Vegara

## Demo

🌐 **[Ver dashboard en vivo](https://eduloopezzz.github.io/sistema-alerta-temprana-tfg/)**

## ¿Qué es esto?

Este sistema es el **Pilar 3 (Análisis de Negocio)** del TFG. Traduce los hallazgos de los pilares analíticos previos en una herramienta visual que un gestor público podría usar para:

1. **Identificar provincias en alerta** mediante un mapa coroplético con la predicción de delitos patrimoniales para 2025.
2. **Comprender qué variables explican la criminalidad** mediante los coeficientes within del Modelo A' con efectos fijos provinciales.
3. **Recibir recomendaciones accionables** específicas para cada provincia, priorizadas según su perfil socioeconómico.

## Estructura del repositorio

```
.
├── index.html                  # Dashboard principal (HTML + D3.js)
├── data/
│   ├── dashboard_data.json     # Datos del modelo (predicciones, coeficientes, etc.)
│   └── provincias.topo.json    # Geometría TopoJSON de las provincias (IGN)
├── README.md
└── LICENSE
```

## Tecnología

- **Frontend:** HTML5 + CSS3 + JavaScript vanilla
- **Visualización:** [D3.js v7](https://d3js.org) + [TopoJSON Client v3](https://github.com/topojson/topojson-client)
- **Geometría provincial:** [es-atlas](https://www.npmjs.com/package/es-atlas) (Instituto Geográfico Nacional)
- **Tipografía:** Fraunces + Inter (Google Fonts)

## Modelos analíticos subyacentes

El dashboard se alimenta de dos modelos desarrollados en el Pilar 2 del TFG:

| Modelo | Tipo | Propósito | R² test |
|--------|------|-----------|---------|
| **Modelo B** | Regresión lineal con lag temporal | Predictivo (mapa pestaña 1) | 0,876 |
| **Modelo A'** | OLS con efectos fijos provinciales | Explicativo (coeficientes pestaña 2) | 0,719 |

Los coeficientes within del Modelo A' son los que sostienen las recomendaciones de política pública, ya que ofrecen una interpretación causal más limpia que un OLS agrupado (test F de poolability: F(51, 516) = 119,07; p < 0,001).

## Fuentes de datos

- **Ministerio del Interior:** estadísticas trimestrales de delitos por provincia (2010–2024)
- **Instituto Nacional de Estadística (INE):** tasa de paro provincial trimestral, renta neta media por persona, población provincial
- **Instituto Geográfico Nacional (IGN):** geometría administrativa provincial vía es-atlas

## Cómo ejecutar localmente

Clona el repositorio y sirve los archivos con cualquier servidor HTTP estático. Por ejemplo, con Python:

```bash
git clone https://github.com/eduloopezzz/sistema-alerta-temprana-tfg.git
cd sistema-alerta-temprana-tfg
python3 -m http.server 8000
```

Después abre `http://localhost:8000` en tu navegador.

> Nota: abrir `index.html` directamente con doble clic no funciona porque el navegador bloquea las peticiones `fetch` a archivos locales por motivos de seguridad (política CORS).

## Cómo desplegar en GitHub Pages

1. Sube todo el contenido de este repositorio a un repositorio público de GitHub.
2. Ve a **Settings → Pages**.
3. En **Source**, selecciona la rama `main` y la carpeta `/ (root)`.
4. Pulsa **Save**. La URL del dashboard estará disponible en unos segundos en `https://TU-USUARIO.github.io/NOMBRE-DEL-REPO/`.

## Limitaciones y advertencias

- Los datos socioeconómicos de 2025 no estaban disponibles en el momento de la construcción del dashboard. Las predicciones del Modelo B utilizan los valores de 2024 como proxy bajo la hipótesis de continuidad y `Delta_Paro = 0`.
- Las predicciones son estimaciones probabilísticas con incertidumbre asociada (RMSE = 217,7 delitos/100k en test). No deben interpretarse como cifras exactas.
- Las recomendaciones de política pública son ejemplos académicos elaborados a partir de la literatura citada, no propuestas oficiales de ninguna administración.
- El sistema es un prototipo académico orientado a la defensa del TFG, no una herramienta operativa.

## Citación

Si reutilizas este código o sus análisis, cita como:

> López López, E. (2026). *Sistema de Alerta Temprana de Riesgo Socioeconómico Provincial: análisis predictivo de la criminalidad patrimonial en España* [Trabajo Fin de Grado]. Universidad Francisco de Vitoria.

## Licencia

Código distribuido bajo licencia MIT (ver [LICENSE](LICENSE)).
La geometría provincial proviene de [es-atlas](https://github.com/martgnz/es-atlas) y mantiene su licencia original.
Los datos socioeconómicos son de dominio público (INE, Ministerio del Interior).

---

*Construido con D3.js · Datos generados el 30 de abril de 2026*
