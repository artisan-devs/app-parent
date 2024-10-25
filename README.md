En el fichero `settings.xml` de la carpeta `.m2`, incluir el servidor de github:

> ⚠️ GitHub Packages sólo admite la autenticación mediante un **token de acceso personal (clásico)**

```xml
<servers>
    <server>
        <id>github</id>
        <username>USERNAME</username>
        <password>CLASSIC ACCESS TOKEN</password> <!-- Ver https://github.com/settings/tokens / Tokens (classic) -->
    </server>
</servers>
```



Después, en el `pom.xml` del proyecto, indicamos en primer lugar el repositorio de GitHub:

> ⚠️ En la URL, el OWNER debe coincidir con el propietario del repositorio, y el REPOSITORY debe coincidir con el nombre de este. Ej:
>
> - Repo: https://github.com/artisan-devs/app-parent
> - URL: https://maven.pkg.github.com/artisan-devs/app-parent

```xml
<repositories>
    <repository>
        <id>github</id>
        <name>GitHub Maven registry for Artisan Devs packages</name>
        <url>https://maven.pkg.github.com/artisan-devs/app-parent</url>
        <snapshots>
            <enabled>true</enabled>
        </snapshots>
    </repository>
</repositories>
```

Y después le indicamos a maven que utilice este servidor para los despliegues del paquete:

```xml
<distributionManagement>
    <repository>
        <id>github</id>
        <url>https://maven.pkg.github.com/artisan-devs/app-parent</url>
    </repository>
</distributionManagement>
```

Una vez tengamos todo configurado, para desplegar una versión del paquete, utilizamos el comando:

```bash
mvn clean deploy
```
