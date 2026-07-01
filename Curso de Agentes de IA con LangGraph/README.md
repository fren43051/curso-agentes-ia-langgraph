# 🤖 Curso de Agentes de IA con LangGraph

Notebook introductorio para el diseño e implementación de **Agentes de Inteligencia Artificial** usando **LangChain**, **LangGraph** y los modelos **Gemini** de Google a través de **Google Cloud Vertex AI**.

---

## 📋 Contenido del Notebook

| Paso | Descripción |
|------|-------------|
| **Paso 1** | Instalación de dependencias |
| **Paso 2** | Autenticación con Google Cloud (ADC) |
| **Paso 3** | Configuración del entorno e importaciones |
| **Paso 4** | Inicialización del modelo, herramientas y prueba de conexión |
| **Paso 5** | Prueba de herramientas (`busca_web` y `multiplicar`) |

---

## 🛠️ Tecnologías

- [LangChain](https://www.langchain.com/) — framework principal para construir aplicaciones con LLMs
- [LangGraph](https://langchain-ai.github.io/langgraph/) — motor para flujos de trabajo basados en grafos con estados y ciclos
- [Gemini 2.5 Flash](https://deepmind.google/technologies/gemini/) — modelo de lenguaje de Google vía `langchain-google-genai`
- [Tavily Search](https://tavily.com/) — herramienta de búsqueda web en tiempo real
- [Google Cloud ADC](https://cloud.google.com/docs/authentication/application-default-credentials) — autenticación sin API key mediante credenciales de aplicación

---

## ⚙️ Requisitos previos

- Python 3.10+
- [Google Cloud SDK](https://cloud.google.com/sdk/docs/install) instalado y configurado
- Proyecto de Google Cloud con **Vertex AI** habilitado
- Cuenta de [Tavily](https://tavily.com/) para obtener una API key

---

## 🚀 Instalación

```bash
pip install -q -U langchain langchain-community langgraph langchain-google-genai \
    langchain-tavily google-auth python-dotenv arxiv tavily-python
```

---

## 🔐 Configuración de credenciales

### 1. Autenticación con Google Cloud (ADC)

Ejecuta estos comandos **una sola vez** en tu terminal:

```bash
gcloud auth login
gcloud auth application-default login
gcloud config set project TU_PROJECT_ID
```

### 2. Variables de entorno

Crea un archivo `.env` en la raíz del proyecto:

```env
GOOGLE_CLOUD_PROJECT=tu-project-id
TAVILY_API_KEY=tu-tavily-api-key
```

> ⚠️ El archivo `.env` está incluido en `.gitignore` para proteger tus credenciales.

---

## 🧩 Herramientas del agente

| Herramienta | Descripción |
|-------------|-------------|
| `busca_web` | Realiza búsquedas en la web en tiempo real usando Tavily Search |
| `multiplicar` | Multiplica dos números enteros |

Las herramientas se vinculan al modelo con `llm.bind_tools(tools)`, permitiendo que el agente las invoque de forma autónoma según el contexto.

---

## 📁 Estructura del proyecto

```
📦 Curso de Agentes de IA con LangGraph
├── 📓 Curso de Agentes de IA con LangGraph.ipynb
├── 📄 .env                  # Variables de entorno (no versionado)
├── 🚫 .gitignore
└── 📖 README.md
```

---

## 🎯 Objetivos de aprendizaje

- Conectar modelos de lenguaje con herramientas externas
- Crear flujos de trabajo cíclicos basados en grafos
- Dotar a los sistemas de capacidades de razonamiento
- Diseñar agentes con toma de decisiones autónoma
