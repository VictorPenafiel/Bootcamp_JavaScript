npm run dev
http://localhost:3000/

1.- Trabajar las rutas del backened 
2.- Importamos nuestras rutas desde la clase servidor
3.- trabajamos en la carpeta routes
4.- Trabajamos en la carpeta controller



SELECT t.id AS transferencia_id, 
	emisor.nombre AS nombre_emisor
	receptor.nombre AS nombre_receptor,
	t.monto, 
	t.fecha 
FROM 
	tranferencias t 
JOIN
	usuarios emisor ON t.emisor = emisor.id
JOIN
	usuarios receptor ON t.receptor = receptor.id


1. Empezamos a ocupar el boilerplate que poseemos

2.- Instalamos dependencias preconfiguradas de nuestro boilerplate
    npm install

3.- Definimos el modelo del objeto, a traves de una Clase
    Server.js 

Trabajamos en rutas de dependencias instaladas como tambien a carpetas de FrondEnd
Trabajamos en rutas desde el modelo hasta las vistas donde queremos visualizar la informacion




$ npm init -y

npm i express nodemon express-handlebars bootstrap uuid jimp
npm run dev



# Inicio de un proyecto con NPM

### Iniciar un proyecto con NPM
1. npm init ( Te pregunta la configuración )
1. npm init -y ( No te pregunta la configuración )

### Instalar una dependencia con NPM
1. npm install `nombre_del_paquete` ( Se instala en el proyecto )
1. npm install -g `nombre_del_paquete` ( Se instala en la maquina )

### Desintalar una dependencia
1. npm uninstall `nombre_del_paquete`

### Versionamiento y actualización
1. npm install `nombre_del_paquete>`@`numero_version`

### Update 
1. npm update `nombre_del_paquete`
1. npm update ( Actualiza todos los paquetes )
1. npm update -g ( Actualiza todos los paquetes a nivel global )

Ahora, ¿Qué sucede si deseo actualizar una dependencia para solo aplicar parches o quizá solo actualizar a una versión menor? Para esto, podemos modificar el registro de la dependencia en el archivo package.json, anteponiendo un carácter especial que NPM lo interpretará para saber a qué nivel deseamos actualizar. Por ejemplo:

1. ~3.5.1: El carácter “tilde” nos asegurará que solo se corregirán errores, es decir, se aplicará el parche más reciente disponible.

1. ^3.5.1: El carácter intercalación nos garantizará que se corregirán errores y se agregarán funcionalidades nuevas, es decir, se cambiará a la versión menor más reciente disponible.

1. *3.5.1: El carácter asterisco nos asegurará que se actualizará a la versión mayor más reciente disponible. Aplicar este tipo de configuración suele ser de alto impacto, por lo que se requiere cuidado al proceder.

### Lista las dependencias
1. npm list






En Node.js, las variables `__filename` y `__dirname` son muy útiles para obtener la ruta del archivo actual y el directorio del archivo actual, respectivamente. Estas variables están disponibles por defecto en módulos creados utilizando `require()` (CommonJS), pero no están directamente disponibles en módulos ES (cuando se usa `import` en lugar de `require`).Desde Node.js 12 en adelante, especialmente en entornos que utilizan ES Modules (con la sintaxis `import/export`), necesitas una forma alternativa de obtener estas variables porque `__filename` y `__dirname` no existen por defecto. A continuación, te muestro cómo puedes simular estas variables en un entorno que utiliza ES Modules.### Paso 1: Crear `__filename` y `__dirname` con `import.meta.url`En módulos ES, puedes utilizar `import.meta.url` para obtener la URL del archivo actual. Aquí te muestro cómo puedes derivar `__filename` y `__dirname` de `import.meta.url`:```javascript
import { fileURLToPath } from 'url';
import { dirname } from 'path';// Obtén la ruta del archivo actual mediante import.meta.url
const __filename = fileURLToPath(import.meta.url);// Obtén el directorio del archivo actual basado en __filename
const __dirname = dirname(__filename);console.log('Filename:', __filename);
console.log('Dirname:', __dirname);
```### Explicación del Código1. **Importar Módulos Necesarios**:
    - `fileURLToPath`: Convierte una URL de archivo (`file://`) a una ruta de archivo tradicional.
    - `dirname`: Extrae el directorio de una ruta de archivo completa.2. **Convertir URL a Ruta de Archivo**:
    - `import.meta.url` devuelve la URL del módulo actual. Por ejemplo, `file:///path/to/your/module.js`.
    - `fileURLToPath(import.meta.url)` convierte esta URL en una ruta de archivo normal.3. **Obtener el Directorio**:
    - `dirname(__filename)` extrae el directorio de la ruta del archivo, proporcionando un análogo directo para `__dirname`.### ¿Por Qué es Necesario?En módulos ES, `import.meta.url` proporciona la ubicación del script actual similar a `__filename` en CommonJS. No hay una variable global en módulos ES que directamente equivalga a `__filename` o `__dirname`, por lo que usar `import.meta.url` es una solución estándar y moderna.### Uso en Diferentes EntornosEsta solución funciona tanto en aplicaciones Node.js que corren directamente en tu servidor o máquina local, como en entornos de compilación que procesan módulos ES (por ejemplo, usando bundlers como Webpack o Rollup que comprenden `import.meta.url`).### Ejemplo PrácticoSi estás desarrollando una aplicación y necesitas acceder a archivos relativos al script actual, puedes usar `__dirname` para construir rutas seguras y confiables, como en el siguiente ejemplo:```javascript
import { readFileSync } from 'fs';// Leer un archivo que está en el mismo directorio que este script
const data = readFileSync(`${__dirname}/data.txt`, 'utf8');
console.log(data);
```Este enfoque garantiza que tus rutas de archivos sean correctas independientemente del directorio de trabajo actual, evitando errores comunes que ocurren cuando se asume una ruta de trabajo relativa.Con estos pasos, `__filename` y `__dirname` pueden ser fácilmente utilizados en aplicaciones Node.js que emplean la sintaxis moderna de módulos ES. Esta es la forma recomendada de manejar rutas de archivos y directorios en nuevos proyectos Node.js que utilizan `import` en lugar de `require()`.