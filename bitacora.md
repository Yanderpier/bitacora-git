# BITÁCORA TÉCNICA DE GIT Y GITHUB

# 1. Fundamentos de Git

## 1.1. Control de versiones

Es un sistema que registra los cambios realizados en los archivos de un proyecto. Permite consultar versiones anteriores, recuperar información y conocer la evolución del trabajo.

**¿Para qué sirve?**
- Mantener un historial de cambios.
- Recuperar versiones anteriores.
- Identificar modificaciones.
- Trabajar en paralelo.
- Facilitar la colaboración entre desarrolladores.

## 1.2. Tipos de control de versiones

| Tipo | Descripción |
|---|---|
| Centralizado (CVCS) | Utiliza un servidor central que almacena el historial del proyecto. |
| Distribuido (DVCS) | Cada usuario dispone de una copia del repositorio y su historial. |

Git pertenece al modelo distribuido.

## 1.3. ¿Qué es Git?

Git es un sistema de control de versiones distribuido y de código abierto. Permite registrar modificaciones, administrar ramas y mantener un historial de los proyectos.

Su funcionamiento no depende permanentemente de internet, ya que gran parte de las operaciones se realizan localmente.

## 1.4. ¿Qué es GitHub?

GitHub es una plataforma que permite alojar repositorios Git en internet y facilita el desarrollo colaborativo.

Incluye herramientas para administrar proyectos, revisar código, registrar problemas y coordinar equipos.

## 1.5. Diferencias entre Git y GitHub

| Git | GitHub |
|---|---|
| Es un sistema de control de versiones. | Es una plataforma de alojamiento y colaboración. |
| Funciona en el equipo local. | Funciona principalmente mediante internet. |
| Administra commits y ramas. | Permite compartir y gestionar repositorios. |
| Puede trabajar sin conexión. | Necesita conexión para acceder a sus servicios remotos. |

## 1.6. Conceptos fundamentales

- **Repositorio:** espacio que contiene los archivos y el historial del proyecto.
- **Commit:** confirmación que registra un conjunto de cambios.
- **Branch:** línea independiente de desarrollo.
- **Merge:** integración de los cambios de diferentes ramas.
- **Remote:** conexión con otro repositorio.
- **Working Directory:** directorio donde se modifican los archivos.
- **Staging Area:** área donde se preparan los cambios antes del commit.

---

# 2. Instalación y configuración

## 2.1. Instalación de Git

Git puede instalarse en diferentes sistemas operativos:

- Windows: instalador oficial de Git for Windows.
- Linux: administrador de paquetes de la distribución.
- macOS: instalador oficial o herramientas de desarrollo de Apple.

Documentación: https://git-scm.com/downloads

## 2.2. Comprobar la instalación

```bash
git --version
```

Muestra la versión instalada de Git. Permite comprobar que el programa está disponible desde la terminal.

## 2.3. Configurar la identidad

Git utiliza un nombre y un correo electrónico para identificar al autor de los commits.

```bash
git config --global user.name "Nombre Apellido"
git config --global user.email "correo@example.com"
```

La opción `--global` aplica la configuración a todos los repositorios del usuario.

## 2.4. Niveles de configuración

| Nivel | Alcance |
|---|---|
| `--system` | Todo el sistema. |
| `--global` | Todos los repositorios del usuario. |
| `--local` | Solamente el repositorio actual. |

La configuración local tiene prioridad sobre la global, y esta sobre la del sistema.

## 2.5. Consultar la configuración

```bash
git config --list
```

Muestra las configuraciones activas.

```bash
git config user.name
```

Consulta un valor específico.

```bash
git config --global --edit
```

Abre el archivo de configuración global para modificarlo.

## 2.6. Archivo `.gitconfig`

Es el archivo donde Git guarda preferencias de configuración.

Ubicaciones habituales:

- Sistema: `/etc/gitconfig`.
- Usuario: `~/.gitconfig`.
- Repositorio: `.git/config`.

También permite configurar el editor predeterminado, alias y otras preferencias.

## 2.7. Configurar el editor

Por ejemplo, para utilizar Visual Studio Code:

```bash
git config --global core.editor "code --wait"
```

Establece VS Code como editor para operaciones que requieren escribir mensajes o modificar archivos de texto.

## 2.8. Crear alias

Los alias permiten asignar nombres cortos a comandos utilizados frecuentemente.

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm "commit -m"
```

Ejemplo:

```bash
git st
```

Ejecuta el comando `git status`.

---

# 3. Repositorios y funcionamiento interno

## 3.1. ¿Qué es un repositorio?

Es el espacio donde Git administra los archivos y almacena el historial de cambios de un proyecto.

**Tipos:**

- **Local:** almacenado en el equipo del desarrollador.
- **Remoto:** alojado en un servidor o plataforma como GitHub.

## 3.2. Inicializar un repositorio

```bash
git init
```

Convierte el directorio actual en un repositorio Git mediante la creación de la carpeta interna `.git`.

Para establecer el nombre de la rama principal:

```bash
git init -b main
```

## 3.3. Clonar un repositorio

```bash
git clone URL
```

Descarga un repositorio remoto, incluyendo sus archivos e historial, y crea una copia local.

Ejemplo:

```bash
git clone https://github.com/usuario/proyecto.git
```

## 3.4. Directorio `.git`

Es una carpeta oculta que contiene la información interna del repositorio.

Almacena el historial, las referencias, la configuración y los objetos que Git necesita para administrar el proyecto.

No debe eliminarse si se desea conservar el historial local.

## 3.5. Objetos internos de Git

Git utiliza cuatro tipos principales de objetos:

| Objeto | Función |
|---|---|
| Blob | Almacena el contenido de un archivo. |
| Tree | Representa directorios y organiza archivos. |
| Commit | Registra una instantánea del proyecto. |
| Tag | Identifica una versión o punto importante del historial. |

## 3.6. Hash

Es un identificador generado a partir del contenido de un objeto Git. Permite identificarlo de manera única dentro del repositorio.

Git utiliza identificadores basados en SHA-1 tradicionalmente, aunque también admite repositorios con SHA-256.

## 3.7. HEAD

Es una referencia que indica la posición actual del repositorio, normalmente asociada a la rama activa.

Permite saber desde qué punto del historial se están realizando las operaciones.

## 3.8. Referencias

Son nombres que apuntan a commits específicos.

Ejemplos:

- `main`: referencia de la rama principal.
- `feature-login`: referencia de una rama de funcionalidad.
- `v1.0.0`: etiqueta de una versión.

---

# 4. Gestión de archivos y cambios

## 4.1. Estados de los archivos

| Estado | Descripción |
|---|---|
| Untracked | Archivo que Git todavía no sigue. |
| Modified | Archivo seguido que ha sido modificado. |
| Staged | Cambio preparado para el próximo commit. |
| Committed | Cambio registrado en el historial. |

## 4.2. Áreas principales de Git

Git organiza el trabajo en tres espacios:

1. **Working Directory:** lugar donde se crean y modifican los archivos.
2. **Staging Area:** área donde se seleccionan los cambios que se registrarán.
3. **Repository:** almacena las confirmaciones del historial.

Flujo general:

`Working Directory → Staging Area → Repository`

## 4.3. Consultar el estado

```bash
git status
```

Muestra la rama actual y los archivos nuevos, modificados o preparados.

```bash
git status -s
```

Muestra una versión resumida del estado.

## 4.4. Preparar archivos

```bash
git add archivo.txt
```

Prepara un archivo específico.

```bash
git add .
```

Prepara los cambios detectados dentro del directorio actual y sus subdirectorios.

## 4.5. Registrar cambios

```bash
git commit -m "Descripción del cambio"
```

Crea una confirmación con los cambios preparados.

Un mensaje debe ser breve, claro y describir el propósito de la modificación.

Ejemplos:

```bash
git commit -m "Agregar documentación inicial"
git commit -m "Corregir validación de datos"
git commit -m "Actualizar configuración del proyecto"
```

## 4.6. Eliminar archivos

```bash
git rm archivo.txt
```

Elimina el archivo del directorio de trabajo y prepara su eliminación para el siguiente commit.

```bash
git rm --cached archivo.txt
```

Deja de seguir el archivo sin eliminarlo del disco.

## 4.7. Mover o renombrar archivos

```bash
git mv archivo.txt documentos/archivo.txt
```

Mueve o renombra un archivo y prepara el cambio para registrarlo.

---

# 5. Historial y recuperación de cambios

## 5.1. Consultar el historial

```bash
git log
```

Muestra las confirmaciones con sus datos principales.

```bash
git log --oneline
```

Presenta el historial de forma resumida.

```bash
git log --graph --oneline --all --decorate
```

Muestra gráficamente las relaciones entre commits y ramas.

## 5.2. Consultar un commit

```bash
git show ID
```

Muestra información y modificaciones correspondientes a un commit específico.

Si no se proporciona un identificador, muestra el commit actual.

## 5.3. Comparar cambios

| Comando | Qué compara |
|---|---|
| `git diff` | Directorio de trabajo frente al staging. |
| `git diff --staged` | Staging frente al último commit. |
| `git diff HEAD` | Directorio de trabajo frente al último commit. |

Permite revisar exactamente qué líneas fueron modificadas.

## 5.4. Consultar autoría

```bash
git blame archivo.txt
```

Muestra quién modificó cada línea y a qué commit pertenece la modificación.

Es útil para investigar cuándo y por quién se introdujo un cambio.

## 5.5. Restaurar archivos

```bash
git restore archivo.txt
```

Descarta modificaciones no preparadas y restaura el contenido del archivo desde el índice.

```bash
git restore --staged archivo.txt
```

Retira un archivo del staging, pero conserva sus modificaciones en el directorio de trabajo.

## 5.6. Reset

Permite mover la referencia de la rama a otra confirmación y, según la opción utilizada, modificar el staging y el directorio de trabajo.

| Opción | Resultado |
|---|---|
| `--soft` | Conserva los cambios preparados. |
| `--mixed` | Conserva los cambios, pero los retira del staging. |
| `--hard` | Restablece también el directorio de trabajo. |

Ejemplos:

```bash
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
```

`HEAD~1` representa el commit anterior al actual.

**Precaución:** `--hard` puede eliminar modificaciones que no estén guardadas en commits.

## 5.7. Revert

```bash
git revert ID
```

Crea un nuevo commit que revierte los cambios introducidos por una confirmación anterior.

Es recomendable cuando se necesita deshacer un cambio sin reescribir el historial compartido.

## 5.8. Reflog

```bash
git reflog
```

Muestra los movimientos recientes de HEAD y otras referencias locales.

Puede ayudar a recuperar commits que dejaron de estar referenciados después de determinadas operaciones.

---

# 6. Ramas e integración

## 6.1. ¿Qué es una rama?

Una rama es una línea independiente de desarrollo que permite trabajar en funcionalidades, mejoras o correcciones sin modificar inmediatamente la línea principal.

La rama principal suele llamarse `main`.

## 6.2. Consultar ramas

```bash
git branch
```

Muestra las ramas locales.

```bash
git branch -a
```

Muestra las ramas locales y las referencias de ramas remotas.

## 6.3. Crear ramas

```bash
git branch nueva-rama
```

Crea una rama sin cambiar a ella.

```bash
git switch -c nueva-rama
```

Crea una rama y cambia a ella.

## 6.4. Cambiar de rama

```bash
git switch main
```

Cambia a la rama `main`.

También existe el comando tradicional:

```bash
git checkout main
```

`git switch` está especializado en cambiar de rama, mientras que `checkout` también permite realizar otras operaciones.

## 6.5. Eliminar ramas

```bash
git branch -d nueva-rama
```

Elimina una rama local que Git considera integrada.

```bash
git branch -D nueva-rama
```

Fuerza su eliminación, incluso si contiene cambios no integrados.

## 6.6. Merge

Integra los cambios de una rama en otra.

```bash
git switch main
git merge nueva-rama
```

**Tipos principales:**

- **Fast-forward:** la rama destino avanza directamente hasta la nueva confirmación.
- **Merge commit:** se crea un commit que une dos líneas de desarrollo.

## 6.7. Conflictos de merge

Se producen cuando Git no puede combinar automáticamente modificaciones incompatibles.

Marcadores habituales:

```text
<<<<<<< HEAD
Contenido actual
=======
Contenido de la otra rama
>>>>>>> otra-rama
```

**Resolución:**

1. Abrir el archivo afectado.
2. Revisar los cambios.
3. Elegir o combinar el contenido.
4. Eliminar los marcadores.
5. Ejecutar `git add`.
6. Finalizar la integración.

## 6.8. Rebase

```bash
git rebase main
```

Reaplica los commits de la rama actual sobre otra base.

Permite obtener un historial más lineal, pero cambia los identificadores de los commits reaplicados.

Debe utilizarse con precaución en ramas compartidas.

## 6.9. Cherry-pick

```bash
git cherry-pick ID
```

Incorpora un commit específico a la rama actual sin integrar necesariamente toda la rama de origen.

---

# 7. GitHub y administración de proyectos

## 7.1. ¿Qué es GitHub?

Es una plataforma que permite alojar repositorios Git y gestionar proyectos de software.

Sus funcionalidades principales incluyen repositorios, Issues, Pull Requests, revisión de código, permisos y automatización.

## 7.2. Repositorios públicos y privados

| Tipo | Característica |
|---|---|
| Público | Cualquier persona puede consultar el contenido. |
| Privado | El acceso está limitado a usuarios autorizados. |

La visibilidad determina quién puede consultar el proyecto. Un repositorio público nunca debe contener información confidencial.

## 7.3. Elementos de un repositorio

| Elemento | Función |
|---|---|
| `README.md` | Explica el proyecto y cómo utilizarlo. |
| `.gitignore` | Define archivos que Git debe ignorar. |
| `LICENSE` | Establece las condiciones de uso y distribución. |
| `CONTRIBUTING.md` | Explica cómo contribuir al proyecto. |
| `CHANGELOG.md` | Registra los cambios entre versiones. |
| `docs/` | Puede almacenar documentación adicional. |
| `.github/` | Contiene configuraciones de GitHub. |

## 7.4. README

Es el documento principal de presentación de un proyecto.

Normalmente contiene:

- Nombre y descripción.
- Objetivo.
- Características.
- Requisitos.
- Instalación.
- Uso.
- Estructura de archivos.
- Licencia y contribuciones.

## 7.5. Markdown

Es un lenguaje ligero de marcado utilizado para escribir documentación.

Ejemplos:

```markdown
# Título principal
## Subtítulo

**Texto importante**

*Texto en cursiva*

- Elemento 1
- Elemento 2

`comando`

[Enlace](https://example.com)
```

## 7.6. Issues

Son registros utilizados para organizar tareas, errores, mejoras y preguntas de un proyecto.

## 7.7. Pull Requests

Son propuestas para integrar cambios de una rama o repositorio en otro.

Permiten revisar código, comentar modificaciones y solicitar correcciones antes de integrar los cambios.

## 7.8. Releases

Permiten publicar versiones identificables de un proyecto, generalmente asociadas a etiquetas y notas de cambios.

## 7.9. Colaboradores y permisos

GitHub permite conceder permisos según las responsabilidades de cada usuario.

Esto permite controlar quién puede consultar, modificar o administrar un repositorio.

## 7.10. Organizaciones y equipos

Las organizaciones permiten administrar proyectos y colaboradores de manera centralizada.

Los equipos agrupan usuarios y facilitan la asignación de permisos sobre los repositorios.

---

# 8. Repositorios remotos

## 8.1. ¿Qué es un remoto?

Es una conexión con otro repositorio, normalmente alojado en GitHub.

Permite intercambiar commits entre el repositorio local y el remoto.

## 8.2. Origin y upstream

- **origin:** nombre convencional del remoto principal.
- **upstream:** nombre utilizado frecuentemente para identificar el repositorio original cuando se trabaja mediante forks.

Son nombres convencionales que pueden cambiarse.

## 8.3. Consultar remotos

```bash
git remote
```

Lista los remotos configurados.

```bash
git remote -v
```

Muestra las direcciones utilizadas para descargar y enviar cambios.

## 8.4. Agregar un remoto

```bash
git remote add origin URL
```

Asocia el repositorio local con una dirección remota.

Ejemplo:

```bash
git remote add origin https://github.com/usuario/proyecto.git
```

## 8.5. Consultar información del remoto

```bash
git remote show origin
```

Muestra información del remoto, incluyendo las ramas y sus relaciones de seguimiento.

## 8.6. Cambiar la dirección

```bash
git remote set-url origin URL
```

Modifica la dirección asociada al remoto.

## 8.7. Eliminar un remoto

```bash
git remote remove origin
```

Elimina la conexión configurada localmente. No elimina el repositorio alojado en GitHub.

## 8.8. Ramas de seguimiento remoto

Son referencias locales que representan el estado conocido de las ramas alojadas en el remoto.

Ejemplo:

- `main`: rama local.
- `origin/main`: referencia de seguimiento de la rama remota.

Se actualizan mediante operaciones como `git fetch`.

## 8.9. Consultar seguimiento de ramas

```bash
git branch -vv
```

Muestra las ramas locales, sus commits y las ramas remotas que siguen.

---

# 9. Sincronización entre Git y GitHub

## 9.1. Push

Envía commits locales al repositorio remoto.

```bash
git push origin main
```

Publica los commits de la rama local `main` en la rama remota correspondiente.

## 9.2. Configurar seguimiento con `-u`

```bash
git push -u origin main
```

Establece la relación de seguimiento entre la rama local y la remota.

Después de configurarla, normalmente se puede utilizar:

```bash
git push
```

## 9.3. Fetch

Obtiene información y commits del repositorio remoto, actualizando las referencias remotas de seguimiento.

```bash
git fetch origin
```

No integra automáticamente los cambios en la rama local ni modifica directamente los archivos de trabajo.

## 9.4. Pull

Obtiene cambios del remoto y los integra en la rama local actual.

```bash
git pull origin main
```

Normalmente realiza un `fetch` seguido de un `merge`. Según la configuración, también puede utilizar `rebase`.

## 9.5. Pull sin abrir el editor

```bash
git pull --no-edit
```

Permite realizar una integración mediante merge utilizando el mensaje predeterminado sin abrir el editor para modificarlo.

## 9.6. Diferencias entre push, fetch y pull

| Comando | Función |
|---|---|
| `git push` | Envía commits locales al remoto. |
| `git fetch` | Obtiene cambios sin integrarlos automáticamente. |
| `git pull` | Obtiene e integra cambios en la rama actual. |

## 9.7. Repositorios adelantados y atrasados

Después de un `fetch`, la rama local y su referencia remota pueden encontrarse en diferentes posiciones.

- **Adelantada:** la rama local tiene commits que el remoto todavía no tiene.
- **Atrasada:** el remoto tiene commits que todavía no están integrados localmente.
- **Divergente:** ambas ramas tienen commits diferentes.

Para consultar el estado:

```bash
git status -sb
```

Para visualizar las relaciones:

```bash
git log --oneline --graph --decorate --all
```

## 9.8. Mantener repositorios sincronizados

Un flujo habitual consiste en:

```bash
git fetch origin
git status
git pull
```

Después de integrar los cambios, se pueden publicar nuevas confirmaciones locales mediante `git push`.

La sincronización requiere que las operaciones se realicen correctamente y que no existan conflictos pendientes.

---

# 10. Organización y seguridad

## 10.1. Archivo `.gitignore`

Es un archivo que contiene reglas para excluir archivos y directorios del seguimiento de Git cuando todavía no están versionados.

Ejemplo:

```gitignore
.env
*.log
node_modules/
dist/
```

- `.env`: excluye archivos con ese nombre.
- `*.log`: excluye archivos con extensión `.log`.
- `node_modules/`: excluye el directorio indicado.
- `dist/`: excluye archivos generados dentro de ese directorio.

## 10.2. Archivos ignorados y versionados

Un archivo ignorado no se elimina del disco.

Además, agregar un archivo a `.gitignore` no hace que Git deje de seguirlo si ya fue incorporado al historial.

Para dejar de seguirlo sin eliminarlo del equipo:

```bash
git rm --cached archivo
```

## 10.3. Consultar archivos ignorados

```bash
git status --short --ignored
```

Muestra los cambios y también los archivos ignorados.

## 10.4. Archivo `.gitattributes`

Permite definir atributos para archivos específicos, como el tratamiento de saltos de línea y archivos binarios.

Ejemplo:

```gitattributes
*.txt text
*.png binary
```

## 10.5. Protección de información sensible

Los archivos `.env` suelen contener configuraciones y credenciales del entorno.

Buenas prácticas:

- No publicar contraseñas ni tokens.
- Excluir archivos sensibles mediante `.gitignore`.
- Utilizar variables de entorno.
- No compartir claves privadas.
- Revocar inmediatamente las credenciales expuestas.
- Revisar los archivos antes de realizar un `push`.

**Importante:** eliminar una credencial de un archivo no significa que haya desaparecido de los commits anteriores. Si se expone, primero debe revocarse o reemplazarse.

---

# 11. Autenticación y conexión

## 11.1. HTTPS

Es un método de conexión que utiliza una dirección que comienza con `https://`.

Ejemplo:

```text
https://github.com/usuario/repositorio.git
```

Para operaciones que requieren autenticación, GitHub utiliza mecanismos compatibles como gestores de credenciales o tokens de acceso.

## 11.2. SSH

Es un método de autenticación mediante un par de claves criptográficas.

- **Clave pública:** se registra en GitHub.
- **Clave privada:** permanece protegida en el equipo del usuario.

Ejemplo de dirección:

```text
git@github.com:usuario/repositorio.git
```

## 11.3. Diferencias entre HTTPS y SSH

| HTTPS | SSH |
|---|---|
| Utiliza una URL HTTPS. | Utiliza una dirección SSH. |
| Puede utilizar gestores de credenciales. | Utiliza claves públicas y privadas. |
| Puede requerir autenticación mediante token. | Requiere configurar las claves. |

## 11.4. Personal Access Token (PAT)

Es un mecanismo de autenticación que permite autorizar determinadas operaciones mediante un token.

Debe protegerse como una contraseña y no debe publicarse en repositorios ni compartirse con otras personas.

## 11.5. Claves SSH

Generar un par de claves:

```bash
ssh-keygen -t ed25519 -C "correo@example.com"
```

Mostrar la clave pública:

```bash
cat ~/.ssh/id_ed25519.pub
```

Comprobar la conexión con GitHub:

```bash
ssh -T git@github.com
```

La clave privada nunca debe compartirse ni publicarse.

---

# 12. Trabajo colaborativo

## 12.1. Fork

Es una copia de un repositorio en otra cuenta de GitHub.

Permite desarrollar cambios sin necesitar permisos de escritura sobre el repositorio original.

## 12.2. Pull Request

Es una propuesta para integrar cambios en otra rama o repositorio.

Permite revisar código, discutir modificaciones y solicitar mejoras antes de aceptar la integración.

## 12.3. Flujo de colaboración

Un proceso habitual es:

1. Obtener una copia del proyecto.
2. Crear una rama.
3. Realizar modificaciones.
4. Registrar los cambios mediante commits.
5. Publicar la rama.
6. Abrir un Pull Request.
7. Revisar y corregir el código.
8. Integrar los cambios.

## 12.4. Revisión de código

Consiste en examinar las modificaciones realizadas por otros desarrolladores.

Su finalidad es detectar errores, mejorar la calidad del código y mantener criterios comunes dentro del proyecto.

## 12.5. GitHub Flow

Es un flujo de trabajo sencillo basado en ramas.

1. Crear una rama.
2. Realizar cambios.
3. Publicar la rama.
4. Abrir un Pull Request.
5. Revisar los cambios.
6. Integrar en `main`.

## 12.6. Git Flow

Es un modelo de trabajo que utiliza diferentes ramas según su función:

| Rama | Función |
|---|---|
| `main` | Versiones estables. |
| `develop` | Integración del desarrollo. |
| `feature` | Nuevas funcionalidades. |
| `release` | Preparación de versiones. |
| `hotfix` | Correcciones urgentes. |

Es un modelo más estructurado que GitHub Flow.

---

# 13. Versionado y automatización

## 13.1. Tags

Permiten identificar commits específicos, normalmente asociados con versiones del proyecto.

Crear una etiqueta:

```bash
git tag v1.0.0
```

Consultar etiquetas:

```bash
git tag
```

Publicar una etiqueta:

```bash
git push origin v1.0.0
```

## 13.2. Versionado semántico (SemVer)

Es un sistema para identificar versiones mediante tres números:

`MAYOR.MENOR.PARCHE`

- **Mayor:** cambios incompatibles.
- **Menor:** nuevas funcionalidades compatibles.
- **Parche:** correcciones compatibles.

Ejemplo: `v1.2.3`.

## 13.3. Releases

Son publicaciones de versiones de un proyecto en GitHub.

Pueden incluir etiquetas, descripción de novedades y archivos distribuidos.

## 13.4. GitHub Actions

Es una herramienta de automatización integrada en GitHub.

Permite ejecutar tareas automáticamente, como:

- Ejecutar pruebas.
- Compilar aplicaciones.
- Analizar código.
- Publicar versiones.
- Desplegar aplicaciones.

Los flujos de trabajo se definen mediante archivos YAML dentro de:

```text
.github/workflows/
```

## 13.5. CI/CD

- **CI (Integración continua):** automatiza la integración y comprobación de cambios.
- **CD (Entrega o despliegue continuo):** automatiza la preparación o publicación del software.

GitHub Actions puede utilizarse para implementar procesos CI/CD.

---

# 14. Errores frecuentes y soluciones

| Problema | Qué revisar |
|---|---|
| `not a git repository` | Verificar que se está dentro de un repositorio. |
| `nothing to commit` | Comprobar si existen cambios y si fueron preparados. |
| `remote origin already exists` | Consultar `git remote -v` antes de agregar otro remoto. |
| `src refspec main does not match any` | Verificar que exista la rama y que tenga commits. |
| `rejected` al hacer push | Revisar si el remoto contiene commits que no están integrados localmente. |
| `Permission denied (publickey)` | Revisar la configuración de SSH. |
| Conflicto de merge | Resolver los archivos afectados y finalizar la integración. |
| `detached HEAD` | Comprobar la posición actual y cambiar a una rama cuando corresponda. |

## 14.1. Comandos de diagnóstico

```bash
git status
```

Consulta el estado del repositorio.

```bash
git remote -v
```

Comprueba las conexiones remotas.

```bash
git branch -vv
```

Consulta las ramas y su seguimiento.

```bash
git log --oneline --graph --decorate --all
```

Inspecciona el historial.

```bash
git reflog
```

Consulta movimientos anteriores de HEAD.

---

# 15. Buenas prácticas y referencia rápida

## 15.1. Buenas prácticas

1. Utilizar nombres claros para archivos y ramas.
2. Realizar commits pequeños y relacionados.
3. Escribir mensajes descriptivos.
4. Revisar `git status` antes de confirmar cambios.
5. Consultar `git diff` antes de preparar archivos.
6. Utilizar ramas para nuevas funcionalidades.
7. Sincronizar periódicamente con el remoto.
8. Mantener actualizado el README.
9. Utilizar `.gitignore` correctamente.
10. No publicar credenciales ni información confidencial.
11. Revisar los Pull Requests antes de integrar cambios.
12. Proteger las ramas importantes.

## 15.2. Flujo básico de trabajo

```bash
git status
git add .
git commit -m "Descripción del cambio"
git push
```

Este flujo permite revisar el estado, preparar los cambios, registrarlos y enviarlos al repositorio remoto. Presupone que el repositorio remoto y el seguimiento de la rama ya están configurados.

## 15.3. Tabla de comandos esenciales

| Comando | Función |
|---|---|
| `git init` | Crear un repositorio. |
| `git clone URL` | Clonar un repositorio. |
| `git status` | Consultar el estado. |
| `git add` | Preparar cambios. |
| `git commit` | Registrar cambios. |
| `git log` | Consultar historial. |
| `git diff` | Comparar modificaciones. |
| `git restore` | Restaurar archivos. |
| `git reset` | Mover referencias y modificar estados. |
| `git revert` | Revertir mediante un nuevo commit. |
| `git branch` | Administrar ramas. |
| `git switch` | Cambiar de rama. |
| `git merge` | Integrar ramas. |
| `git rebase` | Reaplicar commits sobre otra base. |
| `git remote` | Administrar remotos. |
| `git push` | Enviar commits. |
| `git fetch` | Obtener cambios remotos. |
| `git pull` | Obtener e integrar cambios. |
| `git tag` | Administrar etiquetas. |
| `git reflog` | Consultar movimientos de HEAD. |

---

# 16. Glosario técnico

| Término | Significado |
|---|---|
| Version Control | Control de versiones. |
| Repository | Repositorio. |
| Commit | Confirmación de cambios. |
| Branch | Rama de desarrollo. |
| Merge | Integración de ramas. |
| Rebase | Reaplicación de commits sobre otra base. |
| Remote | Repositorio remoto. |
| Origin | Nombre convencional del remoto principal. |
| Upstream | Repositorio original o rama de seguimiento, según el contexto. |
| HEAD | Referencia a la posición actual. |
| Staging Area | Área de preparación. |
| Working Directory | Directorio de trabajo. |
| Push | Envío de commits al remoto. |
| Fetch | Obtención de información remota. |
| Pull | Obtención e integración de cambios. |
| Fork | Copia de un repositorio en otra cuenta. |
| Pull Request | Propuesta de integración. |
| Conflict | Modificaciones que Git no puede combinar automáticamente. |
| Tag | Referencia a una versión o punto del historial. |
| Hash | Identificador de un objeto. |
| CI/CD | Integración y entrega o despliegue continuo. |

---

# 17. Recursos y documentación oficial

- **Git:** https://git-scm.com/
- **Documentación de Git:** https://git-scm.com/docs
- **Libro Pro Git en español:** https://git-scm.com/book/es/v2
- **Documentación de GitHub:** https://docs.github.com/es
- **GitHub Skills:** https://skills.github.com/
- **Guía de Markdown:** https://www.markdownguide.org/