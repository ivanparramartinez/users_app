# users_app

## Introduccion

Esta aplicación permite obtener usuarios de un API por defecto.

Consta de una tabla donde se muestran dichos usuarios y de un formulario para agregar usuarios nuevos
y así mismo mostrarlos también en dicha tabla.

El arreglo de usuarios se mantiene en el localStorage.

El sitio es responsive. 

## Funcionamiento al agregar usuarios

El formulario tiene cuatro campos:

1. Email
2. Nombre(s)
3. Apellido(s)
4. Fecha de Nacimiento

Al oprimir el botón de Agregar Usuario se valida que los campos estén diligenciados. En caso positivo, se agrega al usuario y se muestra una alerta informando que el usuario fue agregado. En caso negativo, no se agrega al usuario y se muetra una alerta informando el inconveniente.

## Project setup

```
yarn install
```

### Compiles and hot-reloads for development

```
yarn serve
```

### Compiles and minifies for production

```
yarn build
```

### Lints and fixes files

```
yarn lint
```

### Customize configuration

See [Configuration Reference](https://cli.vuejs.org/config/).
