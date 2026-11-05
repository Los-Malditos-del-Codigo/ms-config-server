# ms-config-server

Servidor de configuración centralizada de Servillantas RV con backend nativo versionado en `src/main/resources/config`.

- Puerto por defecto: `8888`
- Health: `/actuator/health`
- Ejemplo: `/ms-api-gateway/default`

Este es el primer componente que debe arrancar. Su configuración de bootstrap permanece local para evitar una dependencia circular; toda la configuración operativa de Eureka, Gateway y los microservicios reside en `src/main/resources/config`.

Las credenciales no se almacenan en Git: los perfiles centrales conservan referencias a variables de entorno como `SPRING_DATASOURCE_URL`, `DB_USER`, `DB_PASSWORD` y `JWT_SECRET`.

Orden de arranque: Config Server, Eureka Server, microservicios y API Gateway.
