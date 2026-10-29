# Proyecto de Sistemas Distribuidos: NiFi + PostgreSQL

## 📌 Descripción
Este proyecto implementa un flujo de datos distribuido para la automatización de historiales clínicos. Utiliza **Apache NiFi** para consumir, procesar y transformar un archivo NDJSON, y **PostgreSQL** para el almacenamiento final de los datos. Todo el ecosistema está orquestado con **Docker**.

## 🏗️ Arquitectura
- **Nodo 1 (NiFi):** Se encarga del procesamiento del flujo (GetFile -> SplitText -> EvaluateJsonPath -> ReplaceText -> PutSQL).
- **Nodo 2 (PostgreSQL):** Base de datos relacional donde se almacenan los registros procesados.
- **Docker:** Aísla ambos servicios, garantizando la independencia y el desacoplamiento de los nodos.

## 🚀 Comandos Utilizados

**1. Levantar el ecosistema:**
```bash
docker start postgres_fhir nifi_fhir
