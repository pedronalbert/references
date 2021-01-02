# Docker

## Volumes

> En docker-compose si se quiere evitar que se toque uno de los volumenes (pisar volumenes) se indica solo la url de la direccion

```yml
services:
  testing:
    volumes:
      - /usr/src/node_module # Esta url no será pisada por ningun volumen
```

## MultiStage Builds
```Dockerfile
FROM node as builder

RUN npm install

# Second Stage
...

COPY --from=builder ["/app/data", "/app"]
```

## Caveats

> Cuando se crea una network se debe indicar --atachable para poder conectar containers luego
> Cuando se hace exposicion o montaje de volumenes el formato es {host}:{container}

## To Remember

> ¿Diferencia entre ENTRYPOINT y CMD en docker-compose?

ENTRYPOINT es el comando por defecto que se va a ejecutar en el contenedor y el CMD son los argumentos que se le anidarán a dicho ENTRYPOINT

```Dockerfile
FROM ubuntu

ENTRYPOINT ["/bin/ping", "-c", "3"]
CMD ["localhost"]
```