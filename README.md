# anthea — Entrega React 2026

Tienda reducida de servicios IT construida con React, TanStack Start, Context API y Firebase.

## Funcionalidades

- Carrito global para agregar, quitar y vaciar servicios.
- Registro e inicio de sesión con Firebase Authentication.
- Perfiles con nombre y roles separados (`user` y `admin`).
- Rutas protegidas para perfil y gestión.
- Catálogo público de Firestore con creación, edición y eliminación para administradores.
- Validación de formularios, confirmación al eliminar, estados de carga y errores.
- Búsqueda en tiempo real y paginación de cuatro servicios por página.
- Catálogo local de respaldo mientras Firebase no esté configurado.

## Configuración local

1. Instalá dependencias con `bun install` (o `npm install`).
2. Creá un proyecto en [Firebase](https://console.firebase.google.com/) y agregá una aplicación web.
3. En Authentication → Sign-in method, habilitá **Correo electrónico/Contraseña**.
4. Creá una base de datos de Cloud Firestore.
5. Copiá `.env.example` como `.env.local` y completá los valores de configuración de la aplicación web.
6. Publicá las reglas incluidas en `firestore.rules` desde Firestore → Reglas.
7. Ejecutá `bun run dev` (o `npm run dev`).

Las claves `VITE_FIREBASE_*` identifican la aplicación web; las reglas de Firestore son las que protegen los datos.

## Primer administrador

Los registros nuevos reciben siempre el rol `user` y no pueden cambiarlo desde la aplicación. Para crear el primer administrador:

1. Registrate desde la pantalla **Ingresar**.
2. En Firestore, abrí la colección `roles` y el documento cuyo ID sea el UID de tu usuario.
3. Cambiá el valor de `role` de `user` a `admin` desde la consola de Firebase.
4. Cerrá sesión y volvé a ingresar.

Después aparecerá la sección **Gestión**. Si el catálogo está vacío, el botón **Cargar catálogo inicial** incorpora los seis servicios originales.

También podés publicar las reglas con Firebase CLI desde una terminal autenticada:

```sh
npx firebase-tools login
npx firebase-tools use TU_PROJECT_ID
npx firebase-tools deploy --only firestore:rules
```

## Pruebas

```sh
bun run test
```

## Repositorio y despliegue

Creá un repositorio público llamado `entrega react 2026` en GitHub y subí el código, sin incluir `.env.local`. Desde Lovable, la conexión con GitHub se realiza en **Configuración del proyecto → Git**. Para dejar una copia pública en internet usá **Publish** en Lovable o conectá ese repositorio a Vercel o Netlify siguiendo su configuración para TanStack Start.
