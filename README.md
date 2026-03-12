# ClarIA: From Claims to Clarity

> Transformando quejas del sistema financiero en soluciones estratégicas.

**Deep Learning Project — Especialización en Ciencia de Datos e IA (UTEC – MIT)**  
Martina Ibarra · Elena Salomón · Florencia Nebot · 2026

---

## Descripción

ClarIA es un agente de IA para el sector financiero que analiza reclamos bancarios en lenguaje natural, identifica causas raíz y genera respuestas fundamentadas en datos reales — sin alucinaciones.

Las instituciones financieras reciben miles de reclamos diarios pero carecen de herramientas para identificar automáticamente sus causas raíz. ClarIA transforma ese caos de datos no estructurados en una base de conocimiento accionable, y detecta tendencias emergentes antes de que se conviertan en problemas sistémicos.

---

## Dataset

- **Fuente:** [CFPB — Consumer Financial Protection Bureau (Kaggle)](https://www.kaggle.com/datasets/cfpb/us-consumer-finance-complaints)
- **Tamaño original:** 1.28 millones de reclamos
- **Con narrativa semántica:** 383.000 registros
- **Subconjunto utilizado:** Banca tradicional (excluye fintechs)
- **Datos descartados como ruido:** 2.47% (filtro con Llama 3.2)

---

## Arquitectura

El sistema implementa un pipeline RAG (Retrieval-Augmented Generation) en seis pasos:

1. El usuario consulta al agente en lenguaje natural
2. La consulta se vectoriza con `all-MiniLM-L6-v2`
3. Se buscan fragmentos relevantes en el índice FAISS
4. Se clasifican los fragmentos por cercanía semántica
5. Ollama genera una respuesta con Llama 3.2 1B
6. El sistema entrega información en tiempo y forma

**Chunking:** 300 caracteres con solapamiento de 20, preservando el hilo narrativo.  
**Filtro anti-alucinaciones:** si el score de distancia semántica supera 1.0, el sistema limita la respuesta en lugar de inventar contenido.

---

## Benchmark de Modelos

| Modelo | Tiempo (seg) | Estabilidad | Calidad |
|--------|-------------|-------------|---------|
| **Llama 3.2 1B** ✓ | 2.06 – 2.08 | Alta (±0.01s) | Objetivo y profesional |
| Phi-3 Mini | 15.49 – 51.95 | Muy baja (±36s) | Capta frustración |
| Mistral 7B | 30.47 – 45.18 | Baja (±14s) | Exhaustivo y técnico |
| Solar 10.7B | 36.01 – 38.98 | Media (±2s) | Directo a los dolores |

---

## Stack Técnico

```
Python · FAISS · Ollama · all-MiniLM-L6-v2 · Llama 3.2 1B · NetworkX
```

---

## Caso de Uso: Hipotecas

**Consulta:** *"What issues are reported regarding mortgage interest rate calculations?"*

**Respuesta de ClarIA:**
1. The mortgage payments for an existing loan were not applied properly to the mortgage issued.
2. The mortgage and communication about aggregating monthly payments into a payment request was not done as promised.
3. The interest calculation costs more money due to incorrect numbers, which also affect the amortization schedule.

---

## Próximos Pasos

- Pipeline en tiempo real para incorporación continua de reclamos
- Dashboard visual para auditores
- Expansión multi-sector (fintechs y otras instituciones)
- Agente de resolución con políticas bancarias integradas
- Benchmark con FinGPT

---

## Estructura del Repositorio

```
ClarIA/
├── ClarIA_notebook.ipynb
└── README.md
```

> **Dataset:** Por su tamaño (varios GB), el dataset CFPB no está incluido en este repositorio. Puede descargarse desde [Kaggle](https://www.kaggle.com/datasets/cfpb/us-consumer-finance-complaints).
