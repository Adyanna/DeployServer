# DeployServer

Configuraciones realizadas para la práctica de despliegue en servidor de KeepCoding.

El proyecto contiene configuraciones de Docker y Nginx para desplegar dos aplicaciones:

- **Wallapop React**: aplicación frontend desplegada mediante Docker.
- **BookShop API**: backend desarrollado con Node.js, Express, TypeScript y Prisma, desplegado mediante Docker.
- **Nginx**: configuración como reverse proxy y servidor de archivos estáticos.

## Estructura

```text
DeployServer/
│
├── config bookshop nodejs/
│   ├── Dockerfile
│   ├── docker-compose.yml
│   └── .dockerignore
│
├── config wallapop react/
│   ├── Dockerfile
│   ├── compose.yaml
│   └── .dockerignore
│
└── configuracion nginx/
    ├── bookshop_node
    └── wallapop_react
```

## Tecnologías

- Docker
- Docker Compose
- Nginx
- Node.js
- TypeScript
- Express
- Prisma
- PostgreSQL
- Redis
- Next.js / React

## Acceso a las aplicaciones

Las aplicaciones son accesibles a través de Nginx utilizando los siguientes dominios y direcciones configurados localmente.

### BookShop API

```text
http://bookshop.local
```

Nginx recibe la petición y la redirige hacia la aplicación BookShop API que se ejecuta mediante Docker.

```text
Cliente
   │
   ▼
http://bookshop.local
   │
   ▼
Nginx
   │
   ▼
BookShop API
   │
   ├── PostgreSQL
   ├── Redis
   └── MailDev
```

### Wallapop React

La aplicación Wallapop React se consume mediante la IP del servidor:

```text
http://172.18.72.195
```

Nginx recibe la petición y la redirige hacia el contenedor de Wallapop.

```text
Cliente
   │
   ▼
http://172.18.72.195
   │
   ▼
Nginx
   │
   ▼
Wallapop React
```

## Despliegue

### BookShop API

La API se ejecuta mediante Docker Compose y utiliza los siguientes servicios:

- Node.js / Express
- PostgreSQL
- Redis
- MailDev
- pgAdmin

El contenedor de la aplicación utiliza el puerto `3001` del host.

### Wallapop React

La aplicación se ejecuta mediante Docker y está disponible en el puerto `3000`.

Nginx funciona como reverse proxy para ambas aplicaciones.

## Archivos estáticos

Los archivos estáticos del proyecto BookShop se sirven directamente mediante Nginx.

La configuración utiliza la ruta:

```text
/public/
```

y añade el encabezado requerido:

```text
X-Owner
```

El objetivo es que los archivos estáticos no sean servidos por Node.js, sino directamente por Nginx.

## Nginx

Nginx se utiliza como reverse proxy para las aplicaciones y como servidor de archivos estáticos.

Configuraciones incluidas:

- `bookshop_node`
- `wallapop_react`

## Práctica

Este repositorio contiene las configuraciones utilizadas durante la práctica de despliegue en servidor de KeepCoding.
