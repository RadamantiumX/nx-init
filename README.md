# NEXT JS FULL STACK

Para empezar, lo primero será ejecutar el comando de NEXTJS para instalar toda la paqueria necesaria para
nuestro proyecto.

```bash
npx create-next-app@latest
```
Luego nos preguntará si queremos instalar:

Typescript ✅
ESLint ✅
Tailwind CSS ✅

Si queremos crear un directorio **src**, en este caso le decimos que **NO**, luego nos recomienda utilizar
**APP ROUTER**, lo cual decimos que si, **TURBOPACK** (para agilizar el funcionamiento de la aplicación) y por ultimo dejamos el **CUSTOM ALIAS** por defecto, es decir, le decimos **NO** a la customización.


## SERVER SIDE RENDERING

NEXTJS se ejecuta en el lado del servido, por ello, si intentamos ver un **console.log()**, va a aparecer en el 
navegador, pero con una señalizacion de que es SERVER SIDE COMPONENT.

Estos **Componentes de Servidor** son muy útiles cuando necesitamos acceso directo los recursos del SERVIDOR, pero no todo puede ser un componente de servidor, algunas funcionalidades tendrían que ser CLIENTE SIDE COMPONENTS. Estos últimos, sin **PRE-RENDERIZADOS** del lado del servidor primero, en una **CARCAZA ESTATICA**,para luego **HIDRATARLA** en LADO DEL CLIENT, a esto se llama, **SERVER SIDE PRE-RENDERING**.

## PARAMS ON DYNAMIC ROUTES

Podemos obtener el parametro que nos otorgan las RUTAS DINÁICAS de esta forma:

```tsx
import React from 'react'

const Page = ({ params }: { params: { id: string } }) => {
    const { id } = params
    return (
        <div>
          User {id} details 
        </div>
    )
}
```

Obtenemos el ID del usuario que viene en los parámetros. No tiene que ser solo el ID, puede ser el NAME u otro 
parámetro que veamos conveniente en nuestro desarrollo.
Estos parametros, si bien lo podemos utilizar dentro de esta ruta, también lo podemos utilizar fuera de ella.
En este caso utilizamos el HOOK **useParams()**.


## LAYOUT

Este componentes, vendría a ser el padre de todos los elementos del proyecto UI (elementos renderizables), pero también, podemos crear los nuestro propios para alguna ruta específica, lo único que tenemos que hacer es, nombrarlo propiamente **layout.tsx/jsx**, de otra forma NEXTJS no lo reconocerá como tal.

```tsx
import React from 'react'

export default function Layout({ children }: {children: React.ReactNode}) {
  return (
    <div>
        <h2>Dashboard Layout</h2>
      {children}
    </div>
  )
}
```


## ROUTE GROUPS

Nos permite estructurar rutas y segmentos, sin que estos tenga impacto en la URL, creamos nuevos directorios,
pero estos no van a aparecer en la URL, todo esto lo logramos envolviendo al nombre de estos directorio para agrupar, entre paréntesis **()**.

Dado este caso, podemos crear LAYOUTS diferentes para cada RUTA AGRUPADA. Todo esto, sin dejar que el LAYOUT principal siga siendo el TOP DE LA JERARQUÍA.
**Con todo esto obtenemos un codigo mas ordenado, con LAYOUTS mas independientes, diferentes UI's y, sobre todo, sin la necesidad de modificar la URL.**


## ERROR HANDLING

En NEXTJS, existe una forma muy organizada y eficiente para manejar los posibles errores que puedan tener las 
aplicaciones. Estos ERRORES, no pueden ser vistos por el USUARIO. 
En la documentación, podremos copiar una base del codigo de ERROR que nos proveé NEXTJS, lo podemos establecer en 
cada RUTA AGRUPADA. Asimismo, tenemos la opción de crear una manejo de ERRORES GLOBALES, solo tenemos que crear una archivo en la RAIZ de la APP, llamado **global-error.tsx""**.


## LOADING

Al igual que el manejo de ERRORES, tambien tenemos la posibilidad de manejar las cargas de paginas con LOADING, ubicando un archivo llamado **loading.tsx** en la ROOT del proyecto.