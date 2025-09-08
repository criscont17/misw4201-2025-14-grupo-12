# Sistema de Microservicios con RabbitMQ

Este sistema implementa un validador que distribuye solicitudes a múltiples microservicios de inventario usando Ngnix como enrutador de peticiones y RabbitMQ como mensajería asíncrona.

## Estructura

- **Validador**: Recibe solicitudes HTTP y las envía a los microservicios apropiados
- **Inventario (3 instancias)**: Procesan solicitudes y devuelven respuestas JSON
- **RabbitMQ**: Servidor de mensajería que coordina la comunicación
- **Nginx**: API Gateway para enrutamiento de solitudes entre clinte-servidor.

## Instalación y ejecución

1. Clona o descarga este repositorio
2. Ejecuta: `docker-compose up --build`
3. Revisa las **Instrucciones de instalación**.

## Instrucciones de instalación

1. **Descarga todos los archivos** en una carpeta llamada `misw4201-2025-14-grupo-12`

2. **Ejecuta el sistema:**

```bash
   cd microservices-system
   docker-compose up --build

Dar de baja:
docker-compose down
```

## Uso - AWS

Envía una solicitud POST al validador pasando por el API Gateway:

`````bash
curl -X POST http://3.15.179.192:8080/consulta-inventario \
  -H "Content-Type: application/json" \
  -d '{"product_id": "P002", "action": "check_inventory"}'

Validador: GET http://3.15.179.192:8080/api-health ````
`````

## Uso - Docker - Utilizando API Gateway

Envía una solicitud POST al validador pasando por el API Gateway:

`````bash
curl -X POST http://localhost:8080/consulta-inventario \
  -H "Content-Type: application/json" \
  -d '{"product_id": "P002", "action": "check_inventory"}'

Validador: GET http://localhost:8080/api-health ````
`````

## Uso - Docker - Omitiendo API Gateway

Envía una solicitud POST al validador sin pasar por el API Gateway:

```bash
curl -X POST http://localhost:5001/process \
  -H "Content-Type: application/json" \
  -d '{"product_id": "P002", "action": "check_inventory"}'

Validador: GET http://localhost:5001/health
```
