# Practica Despliegue de Servidores  

**Parte 1** - Accediendo por DNS:   
- App Node Avanzado: http://ec2-54-191-102-249.us-west-2.compute.amazonaws.com/  
- Estático: http://ec2-54-191-102-249.us-west-2.compute.amazonaws.com/images/langs/en.png   
- *Cabecera X-Owner: edudev4
- *Con Supervisor y mongoDB configurado para levantarse al iniciar la máquina.  
- *Recibiendo por el puerto 80 y redirigiendo con Nginx a Node por el :3000

**Parte 2** - Default Server:   
- App React: http://54.191.102.249/  
- *Sin backend  

**Pasos adicionales:**
- Eliminada la opción de mostrar versión de Nginx
- Cambiado el puerto SSH a uno diferente al 22
- Creados 2 usuarios. Uno para cada aplicación.
- Deshabilitados los accesos por contraseña de los usuarios de aplicación

---
---
---

## Practica Node Avanzado:       
     
## NodePop Avanzado

[Demo](/anuncios) of the methods (this link works only if you run the project)

Api for the iOS/Android apps.

## Deploy

### Install dependencies  
    
    npm install

### Configure  

Review lib/connectMongoose.js to set database configuration

### Init database

    npm run installDB

## Start

To start a single instance:
    
    npm start

To start in development mode:

    npm run dev (including nodemon & debug log)

## Test

    npm test (pending to create, the client specified not to do now)

## ESLint

    npm run hints

## API v1 info


### Base Path

The API can be used with the path: 
[API V1](/apiv1/anuncios)

### Language

All requests that return error messages are localized to english, if you want to 
change language make the request with the header accept-language set to other language, 
i.e. Accept-Language: es 

### Error example

    {
      "ok": false,
      "error": {
        "code": 401,
        "message": "Authentication failed. Wrong password."
      }
    }

### GET /anuncios

**Input Query**: 

start: {int} skip records  
limit: {int} limit to records  
sort: {string} field name to sort by  
includeTotal: {bool} whether to include the count of total records without filters  
tag: {string} tag name to filter  
venta: {bool} filter by venta or not  
precio: {range} filter by price range, examples 10-90, -90, 10-   
nombre: {string} filter names beginning with the string  

Input query example: ?start=0&limit=2&sort=precio&includeTotal=true&tag=mobile&venta=true&precio=-90&nombre=bi

**Result:** 

    {
      "ok": true,
      "result": {
        "rows": [
          {
            "_id": "55fd9abda8cd1d9a240c8230",
            "nombre": "iPhone 3GS",
            "venta": false,
            "precio": 50,
            "foto": "/images/anuncios/iphone.png",
            "__v": 0,
            "tags": [
              "lifestyle",
              "mobile"
            ]
          }
        ],
        "total": 1
      }
    }


### GET /anuncios/tags

Return the list of available tags for the resource anuncios.

**Result:** 

    {
      "ok": true,
      "allowed_tags": [
        "work",
        "lifestyle",
        "motor",
        "mobile"
      ]
    }
