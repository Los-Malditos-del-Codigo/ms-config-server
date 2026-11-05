# MS Config Server

Servidor central de configuración de Servillantas, basado en Spring Cloud Config con repositorio nativo incluido en `src/main/resources/config`.

## Responsabilidades

- Entrega una configuración común (`application.yml`) y una específica por servicio.
- Centraliza puertos, Eureka, pools de conexión, JPA, rutas del gateway, JWT e integraciones.
- Mantiene secretos fuera del repositorio mediante variables de entorno.
- Falla al arrancar un servicio si faltan variables obligatorias como credenciales de base de datos o `JWT_SECRET`.

## Uso

Arranca en el puerto `8888`. Ejemplos de consulta:

```text
GET http://localhost:8888/ms-ventas/default
GET http://localhost:8888/msvc-inventario/default
```

Debe iniciarse antes que Eureka, gateway y servicios de negocio.

Para Supabase, `SPRING_DATASOURCE_URL` debe usar el pool transaccional en el
puerto `6543`. La configuración central desactiva los prepared statements del
driver (`DB_PREPARE_THRESHOLD=0`) y limita cada servicio a una conexión para
evitar agotar el pool compartido.

```bash
./mvnw test
./mvnw spring-boot:run
```
