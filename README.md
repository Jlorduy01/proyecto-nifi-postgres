# Proyecto de Sistemas Distribuidos
Flujo de datos con Apache NiFi y PostgreSQL en Docker.
- Flujo: flujo_nifi_fhir.json (procesamiento de pacientes)
- Base de datos: PostgreSQL (tabla pacientes)
- Tolerancia a fallos: NiFi retiene los datos en cola si PostgreSQL se cae.
