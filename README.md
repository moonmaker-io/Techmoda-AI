# TechModa AI — Serverless Intelligent E-Commerce Platform

Plataforma de comercio electrónico basada en arquitectura serverless desacoplada e integración integral de servicios de Inteligencia Artificial preentrenada y Generativa en Amazon Web Services (AWS).

---

## 📺 Demostración en Video del Proyecto (Respaldo)
* 🔗 **[Ver Video de Demostración en Google Drive](https://drive.google.com/file/d/1wCIPq_gHvKKYD4NR05y-skQ9BIgFa7iF/view?usp=sharing)**

Demostración en video del catálogo inteligente, síntesis de voz con Amazon Polly, checkout y el asistente de compras con Amazon Bedrock (RAG).

---

## 🏗️ Arquitectura del Sistema
* **Frontend**: SPA estática alojada en **Amazon S3** con distribución CloudFront.
* **Cómputo & Microservicios**: **AWS Lambda** con Function URLs y Router desacoplado.
* **Persistencia**: **Amazon DynamoDB** con esquema NoSQL flexible para catálogo, metadatos y vectores.
* **Almacenamiento Multimedia**: **Amazon S3** con políticas privadas para audio neuronal generado.
* **Orquestación & IaC**: **AWS SAM (Serverless Application Model)**.

---

## 🧠 Matriz de Servicios de Inteligencia Artificial (Rúbrica S00-S11)

| Módulo | Servicio AWS | Función y Capacidad Implementada | Dominio AIF-C01 |
| :--- | :--- | :--- | :--- |
| **S01** | **Amazon Rekognition** | Detección automática de etiquetas (`aiLabels`) con umbral `MinConfidence >= 80`. | D1: Fundamentos de IA/ML |
| **S02** | **Amazon Rekognition** | Moderación de imágenes (`APPROVED` / `FLAGGED`) y generación de `altText` accesible. | D4: IA Responsable / Accesibilidad |
| **S03** | **Amazon Comprehend** | Análisis de sentimiento en reseñas (`POSITIVE`/`NEGATIVE`/`NEUTRAL`) en ES y EN. | D1: Fundamentos de IA/ML |
| **S04** | **Amazon Translate** | Traducción bidireccional dinámica (`POST /products/{id}/translate`) persistida en tabla. | D1: Fundamentos de IA/ML |
| **S05** | **Amazon Polly** | Síntesis de voz neuronal (Lupe en ES / Joanna en EN) con audio MP3 persistido en S3. | D1: Capacidades de IA / Accesibilidad |
| **S06** | **Amazon Bedrock** | Generación de descripciones de producto contextuales con control de tono y tokens. | D2 & D3: GenAI y LLMs |
| **S07** | **Amazon Bedrock** | Búsqueda semántica vectorial con embeddings densos (**Titan Embeddings V2**, 1024 dims). | D2 & D3: Embeddings y RAG |
| **S08** | **Amazon Bedrock** | Shopping Assistant conversacional con RAG anclado a catálogo real e historial. | D3: Aplicaciones de Modelos Fundacionales |
| **S09** | **Bedrock Guardrails** | Enmascaramiento de PII, bloqueo de temas fuera de dominio y mitigación de sesgos. | D4: Pautas para uso responsable |
| **S10** | **AWS IAM & Governance** | Principio de menor privilegio, Bedrock Model Invocation Logging y control de costos. | D5: Seguridad y Gobernanza |

---

## 🛠️ Retos Técnicos Resueltos (Troubleshooting)
1. **Colisión de CORS en Function URLs**: Conflicto de origen múltiple por duplicidad entre headers devueltos por el código Lambda y la metadata de AWS. Resuelto centralizando el control en la capa de aplicación y limpiando la configuración en Function URL.
2. **Estandarización REST & Handlers SAM**: Mapeo estricto de parámetros de ruta (`rawPath`) y payloads JSON para llamadas a microservicios (`POST /products/{id}/translate` y `POST /products/{id}/voice`).
3. **Optimización RAG y Ventana de Contexto**: Paginación y filtrado de embeddings para equilibrar precisión de búsqueda y consumo de tokens de entrada en modelos fundacionales.
