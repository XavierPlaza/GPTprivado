# Creación de un GPT Privado con OpenAI

Este proyecto explica como crear un Chatbot privado que responda preguntas sobre nuestros documentos. 

![Alt text](<docs/Preguntas y respuestas.png>)

Para la construcción del chatbot utilizaremos [GPT-3.5-Turbo](https://platform.openai.com/docs/models/gpt-3-5) de OpenAI y [LangChain](https://langchain.com/).

Puedes encontrar la explicación completa del código la puedes encontrar en el artículo [Cómo crear tu ChatGPT privado](https://www.pgconocimiento.com/como-crear-tu-chatgpt-privado/).


# Configuración del entorno
## Requerimientos del sistema
Para la ejecución del proyecto se requiere la versión 3.10 de python y la instalación de los paquetes indicados en requirements.txt

Se aconseja crear un entorno conda
```shell
conda create -n gptprivado python=3.10
conda activate gptprivado
```
Antes de instalar los requerimientos es necesario instalar el paquete ```hnswlib```. En caso de no hacerlo, al instalar ChromaDB se produce el siguiente error:

```
ERROR: Failed building wheel for chroma-hnswlib
Failed to build hnswlib chroma-hnswlib
ERROR: Could not build wheels for hnswlib, chroma-hnswlib, which is required to install pyproject.toml-based projects
```
La solución al problema se describe [aquí](https://github.com/imartinez/privateGPT/issues/302#issuecomment-1646731000). Otra alternativa es instalar entornos de desarrollo para compilar el proyecto antes de instalar ChromaDB como se [explica en este hilo](https://stackoverflow.com/questions/73969269/).

Para instalar el paquete hnswlib y evitar la compilación del código ejecutaremos:
```shell
conda install -c conda-forge hnswlib
export HNSWLIB_NO_NATIVE=1
```
Finalmente ya podremos instalar los requerimientos utilizando la instrucción 
```shell
pip intall -r requirements.txt
```

## Archivo de entorno
Se debe cambiar el nombre del archivo ```ejemplo.env``` a ```.env``` y editarlo para copiar tu clave API de Open AI.

``` shell
PERSIST_DIRECTORY=db/docsdb
CHUNK=1000
OVERLAP=100
DOCUMENT=docs/Creacion-de-chatbots-con-IA.pdf
OPENAI_API_KEY=<pega tu key de OpenAI aquí (sin espacios finales)>
```

Si deseas realizar las pruebas con otro archivo pdf, simplemente tienes que subirlo y cambiar la entrada ```DOCUMENT``` del archivo .env con el nombre y la ubicación correctos.


# Descargo de responsabilidad
Este es un proyecto de pruebas para ilustrar la creación de una solución de chatbot utilizando modelos de lenguaje GPT mediante la técnica de embeddings. 

No es un proyeto listo para su puesta en producción ni está deseñado para usarse en producción. 

Tampoco es un modelo totalmente privado puesto que utiliza APIs de terceros y envía información de los documentos a esas APIs