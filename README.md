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
```
2. Verificar que los nodos están activos:
bash
```bash
docker ps
```
3. Visualizar el archivo original (JSON crudo):
bash
```bash
cat pacientes.ndjson | head -n 1
```
4. Verificar los datos insertados en PostgreSQL:
bash
```bash
docker exec -i postgres_fhir psql -U postgres -d fhir_db -c "SELECT * FROM pacientes;"
```
5. Ver el esquema relacional de la tabla:
bash
```bash
docker exec -i postgres_fhir psql -U postgres -d fhir_db -c "\d pacientes"
```
🛡️ Prueba de Tolerancia a Fallos

El sistema está diseñado para ser resiliente. Si la base de datos falla, el flujo de datos no se pierde.

1. Apagar la base de datos:
bash
```bash
docker stop postgres_fhir
```
2. Comprobar que NiFi sigue en ejecución:
bash
```bash
docker ps
docker logs nifi_fhir --tail 5
```
(Se observa que NiFi registra el error de conexión pero se mantiene activo y retiene los datos en cola).

3. Volver a encender la base de datos:
bash
```bash
docker start postgres_fhir
```
4. Verificar que los datos en cola se insertaron:
bash
```bash
docker exec -i postgres_fhir psql -U postgres -d fhir_db -c "SELECT * FROM pacientes;"
```
