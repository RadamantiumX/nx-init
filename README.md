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


## DATA FETCHING

Podríamos usar HOOKS para poder obtener data de alguna API, o servidor, pero no es la forma mas eficiente de 
hacerlo.
En NEXTJS tenemos una propiedad que esta disponible para utilizar cuando realizamos algún FETCHING, se llama
**serverComponentsHmrCache** *(HMR: Hot Module Replacement)*, esto quiere decir que, tendremos mas rápidas 
respuestas y reduciremos las las llamadas a la API, lo cual puede tener un costo adicional.

El DATA FETCHING en el SSR, es muy beneficioso, ya que reduce todo los parametros de carga y costo adicional, y,
sobre todo, es amigable con el SEO. Se evita la duplicación del FETCHING DATA, solo se pide una sola vez. Y, obviamente, la seguridad también es un factor importante en el FETCHING, lo cual en el SSR se le da mas importancia
y respalda las llamadas a la API, protegiendolas de ataques externos.


## STATIC SIDE GENERATION (SSG)

Es una técnica que genera las páginas HTML al momento de hacer la BUILD, es decir, cuando se hace el despligue y no
cuando el usuario lo solicita.

**Podemos ver otros tipo de RENDERING con NEXTJS en la documentación oficial, uno de los recientes en el PPR (Partial PreRendering).**

## PARTIAL PRERENDERING

Combina STATIC y DYNAMIC RENDERING. NEXTJS genera una carcaza estatica del despligue, que son, el diseño y cualquier parte estatica de la página, en forma de componentes, en estos componentes hay marcadores para el contenido dinámico, lo que hacemos en envolver todo ese contenido dinámico en el tag **Suspenese**, mientras que el contenido STATIC se carga automáticamente, el DYNAMIC espera a ser requerido.


## API ROUTES

En NEXTJS es muy sencillo la utilización de un servidor, ya que, no debemos crear uno de forma separada del proyecto, lo podemos incluir aquí mismo. Este FRAMEWORK utiliza el renderizado del servidor, es por ello, que realizar llamadas a la API, y la base de datos, es totalmente recomendable. De la misma forma que organizamos los directorio y archivos, para UI, lo podemos hacer en una API.