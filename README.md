# Tarea: Clasificación con Redes Neuronales Convolucionales (CNN) — MNIST

**Inteligencia Artificial & Mini Robots** · Prof. Flavio Prieto
Ingeniería Mecatrónica — Universidad Nacional de Colombia, Sede Bogotá

Este repositorio contiene la solución completa de la tarea: diseño, entrenamiento,
optimización y evaluación de una **CNN** y un **MLP** para clasificar los dígitos
manuscritos del dataset **MNIST** (10 clases, imágenes 28×28 en escala de grises).

---

## 📁 Contenido

| Archivo | Descripción |
|---------|-------------|
| `CNN_MNIST_IA_MiniRobots.ipynb` | Notebook principal (informe técnico reproducible con celdas markdown). |
| `README.md` | Este archivo: instrucciones de ejecución y guion para el video. |

---

## ▶️ Cómo ejecutar (Google Colab — recomendado)

No necesitas instalar nada: **TensorFlow y el dataset MNIST ya vienen incluidos en Colab**.

1. Entra a <https://colab.research.google.com>.
2. `Archivo → Subir cuaderno` (File → Upload notebook) y selecciona `CNN_MNIST_IA_MiniRobots.ipynb`.
   - *Alternativa:* si el notebook está en GitHub, usa `Archivo → Abrir cuaderno → GitHub` y pega la URL del repo.
3. (Recomendado) Activa la GPU: `Entorno de ejecución → Cambiar tipo de entorno → Acelerador por hardware → GPU (T4)`.
4. Ejecuta todo: `Entorno de ejecución → Ejecutar todo` (Runtime → Run all).

Tiempo aproximado de ejecución completa:
- **Con GPU (T4):** ~3–6 minutos.
- **Solo CPU:** ~15–30 minutos (funciona igual, solo más lento).

### Ejecución local (opcional)
Si prefieres correrlo en tu máquina:
```bash
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install tensorflow scikit-learn matplotlib seaborn pandas jupyter
jupyter notebook CNN_MNIST_IA_MiniRobots.ipynb
```

---

## 🗂️ Estructura del notebook (mapeo con el enunciado)

| Sección del notebook | Parte del enunciado | Qué hace |
|---|---|---|
| 0. Configuración | — | Semillas fijas (reproducibilidad), imports, chequeo de GPU. |
| **Parte 1 — Preprocesamiento** | Parte 1 | Carga MNIST · split **train/validación/test** (estratificado) · normaliza a `[0,1]` · reshape (4D para CNN, 784 para MLP) · **distribución de clases**. |
| **Parte 2 — Diseño de la CNN** | Parte 2 | Arquitectura Conv2D+ReLU+MaxPooling+Dense+Softmax · **tabla de justificaciones** (filtros, kernel, profundidad, pooling, pérdida, optimizador) · **variantes** (16-32, 32-64, 64-128, +Dropout) · comparación **Adam vs SGD**. |
| **Parte 3 — Diseño de la MLP** | Parte 3 | MLP sobre el vector de 784 píxeles, sin convoluciones · curvas de entrenamiento. |
| **Parte 4 — Evaluación** | Parte 4 | Para ambos modelos: **accuracy, matriz de confusión, precision/recall/F1, F1 macro y micro, tiempo de entrenamiento** · **análisis de errores comunes** (dígitos similares). |
| **Parte 5 — Discusión** | Parte 5 | Aporte de las convoluciones vs MLP · efecto del nº de filtros · diagnóstico de **sobreajuste** (brecha train-test). |
| Conclusiones | Entregables | Tablas comparativas, gráficas y conclusiones argumentadas. |

---

## 📊 Decisiones de diseño (resumen)

- **Filtros crecientes 32→64:** patrones de bajo nivel en las primeras capas, combinaciones de alto nivel al reducir resolución.
- **Kernel 3×3:** campo receptivo eficiente con pocos parámetros.
- **MaxPooling 2×2:** invarianza a traslaciones, menos cómputo, control de sobreajuste.
- **ReLU + Softmax de salida:** convergencia estable y salida como probabilidades sobre 10 clases.
- **Pérdida:** `sparse_categorical_crossentropy` (Cross-Entropy, etiquetas enteras).
- **Optimizador:** Adam (lr=1e-3); se justifica comparándolo con SGD+momentum.
- **Regularización:** EarlyStopping, Dropout (variante CNN y MLP).

---

## 🎥 Guion sugerido para el video (máx. 15 min)

1. **(1 min) Introducción:** objetivo, dataset MNIST, por qué CNN vs MLP.
2. **(2 min) Parte 1 — Preprocesamiento:** carga, split train/val/test, normalización, distribución de clases.
3. **(3 min) Parte 2 — CNN:** explica la arquitectura y **justifica** cada hiperparámetro con la tabla; muestra las variantes de filtros y Adam vs SGD.
4. **(2 min) Parte 3 — MLP:** por qué se aplana a 784 y qué se pierde al no usar convoluciones.
5. **(3 min) Parte 4 — Evaluación:** compara accuracy/F1 macro-micro, muestra las matrices de confusión y los errores comunes (4↔9, 3↔5).
6. **(3 min) Parte 5 — Discusión:** responde las 3 preguntas (aporte de convoluciones, efecto de filtros, sobreajuste) usando las tablas y curvas.
7. **(1 min) Conclusiones** y cierre.

> Consejo: ejecuta el notebook **antes** de grabar para tener las gráficas y los números reales a la vista.

---

## ✅ Checklist de entregables

- [x] Código reproducible y comentado (tipo informe técnico, celdas markdown).
- [x] Tablas comparativas.
- [x] Gráficas de entrenamiento.
- [x] Conclusiones argumentadas.
- [ ] Video explicativo de máximo 15 minutos *(a cargo del estudiante)*.
