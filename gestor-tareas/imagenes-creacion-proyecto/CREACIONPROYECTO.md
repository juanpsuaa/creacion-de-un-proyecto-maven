# Creación de un proyecto con Maven

## 1. Descripción de la tarea y del sistema operativo

La tarea propone el reto de crear un proyecto de Java utilizando Maven desde cero.

El sistema operativo que utilizaré para el desarrollo de la tarea será **CachyOS**, una distribución basada en Arch Linux.

## 2. Preparación del entorno

El primer paso consiste en instalar todas las herramientas necesarias para trabajar con el proyecto. Para ello, utilizamos los siguientes comandos:

```bash
sudo pacman -S jdk21-openjdk
sudo pacman -S maven
sudo pacman -S intellij-idea-community-edition
```

Una vez instaladas las herramientas, procedemos a crear el proyecto de Maven.

## 3. Creación y configuración inicial del proyecto

Después de crear el proyecto, modificamos el archivo `pom.xml` con la información proporcionada en la práctica.

A continuación, ejecutamos:

```bash
mvn validate
```

Como se puede observar en la **imagen 1**, el proyecto funciona correctamente.

Después realizamos el cambio solicitado en el proyecto y volvemos a ejecutar:

```bash
mvn validate
```

En este caso, el resultado se muestra en la **imagen 2**, donde podemos observar que el nombre cambia de `gestor-tareas` a `gestor_tareas`.

## 4. Compilación y limpieza del proyecto

El siguiente paso consiste en comprobar la compilación de los archivos del proyecto. Para ello, ejecutamos:

```bash
mvn compile
```

Como se muestra en la **imagen 3**, la compilación no se realiza correctamente debido a unos errores relacionados con la versión de los plugins.

Además, durante este proceso se crea la carpeta `target`.

Posteriormente, ejecutamos:

```bash
mvn clean
```

Con este comando comprobamos que la carpeta `target` desaparece, realizando así la limpieza de los archivos generados durante la compilación.

## 5. Comprobación y cambio de la versión de Java

A continuación, comprobamos las versiones de Java instaladas en el sistema mediante:

```bash
archlinux-java status
```

El resultado se muestra en la **imagen 4**. Podemos observar que la versión utilizada por defecto es **JDK 26**.

Para cambiar la versión utilizada por el sistema, empleamos:

```bash
sudo archlinux-java set <nombre_de_la_version>
```

Primero cambiamos la versión a **Java 17**, como se muestra en la **imagen 5**. Después comprobamos que el cambio se ha realizado correctamente.

Posteriormente, repetimos el mismo proceso para utilizar **JDK 21**, cuyo resultado se muestra en la **imagen 6**.

## 6. Añadir y utilizar dependencias

Una vez configurada la versión de Java, añadimos nuevas dependencias al proyecto y procedemos a utilizarlas.

En mi caso, las dependencias funcionan correctamente.

Después ejecutamos:

```bash
mvn install
```

Este comando guarda el artefacto generado en el **repositorio local de Maven**, es decir, en el repositorio que se encuentra en nuestro propio ordenador. Por este motivo, otras personas no pueden acceder directamente a dicho artefacto.

## 7. Configuración del repositorio público

A continuación, creamos una nueva carpeta llamada `config`.

Dentro de esta carpeta creamos el archivo:

```text
settings-publico.xml
```

y lo rellenamos con la información necesaria.

Una vez creado el archivo, utilizamos los siguientes comandos:

```bash
mvn -s config/settings-publico.xml -Prepositorio-publico help:active-profiles
```

```bash
mvn -s config/settings-publico.xml -Prepositorio-publico compile
```

Con estos comandos comprobamos la configuración del repositorio público y la compilación del proyecto.

El comando continúa mostrando **SUCCESS** incluso cuando eliminamos `Repositorio-publico`.

## 8. Configuración del repositorio de empresa

A continuación, intentamos crear el archivo:

```text
settings-empresa.xml
```

Sin embargo, durante este proceso se produce un error. Por este motivo, dejamos este problema pendiente y continuamos con el siguiente apartado de la práctica.

## 9. Configuración de los perfiles de Maven

El siguiente paso consiste en actualizar el archivo `pom.xml` del proyecto, añadiendo los diferentes **profiles** después de la sección `build`.

Una vez realizada esta modificación, ejecutamos los siguientes comandos para comprobar el funcionamiento de los perfiles:

```bash
mvn clean package
```

```bash
mvn -Pdistribucion clean package
```

```bash
java -jar target/gestor-tareas-1.0.0-SNAPSHOT-all.jar
```

```bash
mvn -Pdistribucion,informe clean verify
```

```bash
mvn -Pdistribucion help:active-profiles
```

```bash
mvn -Pdistribucion help:effective-pom
```

Los resultados obtenidos durante estas comprobaciones se pueden observar en la **imagen 7**.

## 10. Activación de perfiles

Finalmente, añadimos una nueva configuración de **activation** al proyecto.

En mi caso, esta configuración produce un error. Por lo tanto, este será uno de los problemas que habrá que revisar y solucionar posteriormente antes de continuar con la práctica.

---

## Imágenes

* **Imagen 1:** Resultado de `mvn validate`.
* **Imagen 2:** Cambio del nombre del proyecto.
* **Imagen 3:** Error durante `mvn compile`.
* **Imagen 4:** Versiones de Java instaladas.
* **Imagen 5:** Cambio a Java 17.
* **Imagen 6:** Cambio a JDK 21.
* **Imagen 7:** Resultado de la configuración de los perfiles.
