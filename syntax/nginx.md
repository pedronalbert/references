# Nginx
## Directives

### Rewrite
```
rewrite REGEX REPLACEMENT [flag];
```

#### Flags
**last**: This flag will stop the processing of the rewrite directives in the current set, and will start at the new location that matches the changed URL.

**break**: This flag will stop the processing of the rewrite directives in the current set.

**redirect**: This flag will do a temporary redirection using 302 HTTP code. This is mainly used when the replacement string is not http, or https, or $scheme

**permanent**: This flag will do a permanent redirection using 301 HTTP code

#### Logging
By default, anytime Nginx does successful rewrite, it doesn’t log it in the error.log.

```
rewrite_log on;
```

### Location
```
location [MODIFIER] MATCH {
  ...
}

location /images/ {
  # This representes /images/**
}


```

#### Modifiers
- **=** Equality
- **~** Case Sensitive Regex
- **~\*** Case Insensitive Regex


#### Named Locations
You can also use @ (at symbol) in the location directive as shown in the example below.

```
location / {
  try_files $uri $uri/ @foo;
}

location @foo {
  #...
}
```

## FAQ

### Root vs Alias
Cuando se usa alias el path especificado en el location es eliminado de la busqueda del archivo, ejemplo

```
server {
    location /assets/images {
        alias /var/html;
        try_files $uri $uri/ =404;
    }
}

http://site.com/assets/images/logo.png -> /var/html/logo.png
http://site.com/assets/images/others/logo.png -> /var/html/others/logo.png
```