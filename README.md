# SIAPEM - Sistema Electrónico de Avisos y Permisos de Establecimientos Mercantiles

> https://codigofuente.git


**Sistema de administración de establecimientos mercantiles para la Ciudad de México**  
Aplicación en Java EE desarrollada para la gestión integral de trámites y servicios mercantiles.

## Índice

- [Descripción](#descripción)
- [Tecnologías](#tecnologías)
- [Variables de entorno](#variables-de-entorno)
- [Requisitos del Sistema](#requisitos-del-sistema)
- [Instalación para DESPLIEGUE](#instalación-para-despliegue)
- [Instalación para DESARROLLO](#instalación-para-desarrollo)

---

## Descripción

SIAPEM es el sistema oficial mediante el cual se gestionan los establecimientos mercantiles en la Ciudad de México. Proporciona una plataforma integral para:

- Gestión de trámites y licencias mercantiles
- Administración de establecimientos comerciales
- Control de usuarios por dependencias
- Reportes y estadísticas de actividad comercial
- Integración con sistemas legacy

## Tecnologías

### Stack Principal:
- **Java**: 8 (Runtime) / 24+ (IDE) solo para el equipo de desarrollo
- **Java EE**: Plataforma empresarial
- **WildFly**: 17.0.1 - Servidor de aplicaciones
- **PostgreSQL**: 14+ - Base de datos principal
- **SQL Server**: 11.2.0+ - Base de datos legacy
- **Maven**: 3.8.7 - Gestión de dependencias

### Herramientas de Desarrollo:
- **Eclipse IDE**: 2025+ (Enterprise Java and Web Developers)
- **JBoss Tools**: Plugin para desarrollo
- **Maven**: Automatización de builds

### Dependencias Principales:
- `javax.annotation-api`: 1.3.2
- `sia-commons`: Utilidades comunes
- `hibernate-core`: ORM
- `jersey-*`: 1.19 - Servicios REST
- `mandrillClient`: 1.1 - Servicio de emails
- `itext`: 2.1.7 - Generación de PDFs

## Variables de Entorno
### Variables de Base de Datos:
```bash
export DB_HOST=localhost
export DB_PORT=00000
export DB_USER=tu_usuario
export DB_PASS=tu_password

export SQLSERVER_HOST=localhost
export SQLSERVER_PORT=00
export SQLSERVER_USER=sa
export SQLSERVER_PASS=password_legacy
```

### Variables de Servidor:
```bash
export WILDFLY_HOME=/opt/wildfly/wildfly
export JBOSS_HOME=$WILDFLY_HOME

```

## Requisitos del Sistema
- **OS**: Linux (Debian/Ubuntu/Fedora/CentOS/Arch)
- **Java**: JDK 8 (runtime) + JDK 24+ (IDE)
- **RAM**: 8GB mínimo (16GB recomendado)
- **Espacio**: 10GB disponible
- **IDE**: Eclipse IDE 2025+ Enterprise

### Preparación del Sistema - General

#### Sistemas Debian/Ubuntu:
```bash
# Actualizar sistema
sudo apt update && sudo apt upgrade -y

# Dependencias base
sudo apt install -y wget curl git maven build-essential
```

----

# Instalación para DESPLIEGUE 

## 1. Instalación de Git

```bash 
# Actulización de paquetes
sudo apt update

# Instalación Git
sudo apt install git

# Seleccionar carpeta para el repositorio
sudo mkdir git

# Asignar propietario a la carpeta

sudo chown -r tu_usuario:tu_usuario

# Clonar el repositorio
git clone https://codigofuente.git

```

### 2. Instalación de Maven
```bash
# Descargar Maven 3.8.7
sudo apt update
sudo apt install maven -y

# Verificar la instalación
mvn -version
```

## 3. Instalación de Java

### Java 8 (Runtime del proyecto):

**Ubuntu:**
```bash
sudo apt install openjdk-8-jdk
```
**Debian:**
```bash
# Instalar bajo comando
sudo wget https://cdn.azul.com/zulu/bin/zulu8.86.0.25-ca-fx-jdk8.0.452-linux_x64.tar.gz

# Alternativa de instalación (link para descarga directa)
https://aur.archlinux.org/packages/openjdk-zulu8-ca-fx-bin

# Crea la carpeta para el JDK si no existe
sudo mkdir -p /usr/lib/jvm

# Descomprimir el archivo en esta carpeta
sudo tar -xzf zulu8.86.0.25-ca-fx-jdk8.0.452-linux_x64.tar.gz -C /usr/lib/jvm

(esto creará una carpeta como: "/usr/lib/jvm/zulu8.86.0.25-ca-fx-jdk8.0.452-linux_x64")

# Registrar este JDK en el sistema Debian
sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/zulu8.86.0.25-ca-fx-jdk8.0.452-linux_x64/bin/java 1080
##Ese comando no funciona, no cambia la version de java
```

**Verificar instalación de Java 8**

```bash
# Seleccionar versión para Eclipse
sudo update-alternatives --config java
sudo update-alternatives --config javac
```

### Configurar Variables de Entorno:

```bash
## la version en este comando debe ser la 1.8 (ejemplo si se instaló en Debian)
# Agregar al final de ~/.bashrc
echo 'export JAVA_HOME=/usr/lib/jvm/zulu8.86.0.25-ca-fx-jdk8.0.452-linux_x64' >> ~/.bashrc
echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.bashrc

# Aplicar cambios
source ~/.bashrc
```

### Verificar Instalación:
```bash
java -version
javac -version
echo $JAVA_HOME
```
## 4. Configuración de Base de Datos

#### Instalar PostgreSQL:

**Debian/Ubuntu:**
```bash
sudo apt install postgresql postgresql-contrib
```

#### Configurar Usuario y Base de Datos:
```bash
# Acceder como usuario postgres
sudo -u postgres psql

# Dentro de PostgreSQL:
ALTER USER postgres WITH PASSWORD 'tu_password_seguro';
CREATE DATABASE "sssiiapem";
GRANT ALL PRIVILEGES ON DATABASE "sssiiape" TO postgres;
\q
```

#### Restaurar Backup:
```bash
# Copiar backup a directorio temporal
sudo cp ruta/al/backup/siap /tmp/

# Cambiar a usuario postgres
sudo -i -u postg8

# Restaurar base de datos
```

## 5. Instalación de WildFly

#### Descargar y Configurar:
```bash
# Crear directorio para WildFly
sudo mkdir -p /opt/wildfly
cd /opt/wildfly

# Descargar WildFly 17.0.1
sudo wget https://download.jboss.org/wildfly/17.0.1.Final/wildfly-17.0.1.Final.tar.gz

# Extraer
sudo tar -xvzf wildfly-17.0.1.Final.tar.gz
sudo mv wildfly-17.0.1.Final wildfly

# Configurar permisos
sudo chown -R $USER:$USER /opt/wildfly/wildfly
```
## Comandos de Gestión para correr el proyecto

### Maven:
```bash
# Limpia
mvn clean 

# Compilar
mvn install
```

### WildFly:
```bash
# Iniciar servidor
sudo systemctl start wildfly

# Ingresar a la ruta wildfly
cd /opt/wildfl17.0.1.Final/bin/

# Revisar que tenga perfil de ejecución (debe tener una x)
ls -l ./standalone.sh

# Si no tiene perfil de ejecución darle el permiso
chmod +x ./standalone.sh

# Ejecutar servidor:
sudo ./standalone.sh -b 0.0.0.0 &
```

#### Verificar Despliegue:
```bash
# Acceder a la aplicación
curl http://localhost:8080/siapem
```

---

# Instalación para DESARROLLO

## 1. Instalación de Java

### Java 8 (Runtime del proyecto):

**Ubuntu:**
```bash
sudo apt install openjdk-8-jdk
```

**Debian:**
```bash
# Instalar bajo comando
sudo wget https://cdn.azul.com/zulu/bin/zulu8.86.0.25-ca-fx-jdk8.0.452-linux_x64.tar.gz

# Alternativa de instalación (link para descarga directa)
https://aur.archlinux.org/packages/openjdk-zulu8-ca-fx-bin

# Crea la carpeta para el JDK si no existe
sudo mkdir -p /usr/lib/jvm

# Descomprimir el archivo en esta carpeta
sudo tar -xzf zulu8.86.0.25-ca-fx-jdk8.0.452-linux_x64.tar.gz -C /usr/lib/jvm

(esto creará una carpeta como: "/usr/lib/jvm/zulu8.86.0.25-ca-fx-jdk8.0.452-linux_x64")

```

### Java 24+ (Para Eclipse IDE):

```bash
# Descargar Java 24
wget https://download.java.net/java/GA/jdk24.0.1/2/GPL/openjdk-24.0.1_linux-x64_bin.tar.gz

# Crear directorio e instalar
sudo mkdir -p /usr/lib/jvm
sudo tar -xvzf openjdk-24.0.1_linux-x64_bin.tar.gz -C /usr/lib/jvm/

# Configurar alternativas
sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk-24.0.1/bin/java 1
sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk-24.0.1/bin/javac 1

# Seleccionar versión para Eclipse
sudo update-alternatives --config java
sudo update-alternatives --config javac
```

#### Configurar Variables de Entorno:

```bash
## la version en este comando debe ser la 1.8
# Agregar al final de ~/.bashrc
echo 'export JAVA_HOME=/usr/lib/jvm/jdk-24.0.1' >> ~/.bashrc
echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.bashrc

# Aplicar cambios
source ~/.bashrc
```

#### Verificar Instalación:
```bash
java -version
javac -version
echo $JAVA_HOME
```

### 2. Configuración de Base de Datos

#### Instalar PostgreSQL:

**Debian/Ubuntu:**
```bash
sudo apt install postgresql postgresql-contrib
```

#### Configurar Usuario y Base de Datos:
```bash
# Acceder como usuario postgres
sudo -u postgres psql

# Dentro de PostgreSQL:
ALTER USER postgres WITH PASSWORD 'tu_password_seguro';
CREATE DATABASE "siapemDS";
GRANT ALL PRIVILEGES ON DATABASE "siap" TO postgres;
\q
```

#### Restaurar Backup:
```bash
# Copiar backup a directorio temporal
sudo cp ruta/al/backup/siap/tmp/

# Cambiar a usuario postgres
sudo -i -u postgres

# Restaurar base de datos
pg_restore -d siap /tmp/siap

# Verificar restauración
psql -d siap -c "\dt"
```
### 3. Instalación de Maven
```bash
# Descargar Maven 3.8.7
sudo apt update
sudo apt install maven -y

# Verificar la instalación
mvn -version
```

### 4. Instalación de WildFly

#### Descargar y Configurar:
```bash
# Crear directorio para WildFly
sudo mkdir -p /opt/wildfly
cd /opt/wildfly

# Descargar WildFly 17.0.1
sudo wget https://download.jboss.org/wildfly/17.0.1.Final/wildfly-17.0.1.Final.tar.gz

# Extraer
sudo tar -xvzf wildfly-17.0.1.Final.tar.gz
sudo mv wildfly-17.0.1.Final wildfly

# Configurar permisos
sudo chown -R $USER:$USER /opt/wildfly/wildfly
```
#### Configurar Drivers de Base de Datos:

```bash
# Copiar archivos de la parte "manual_archivos" (desde manual_de_instalacion.zip del repositorio)

# Crear los directorios postgresql y main dentro de postgres,también sqlserver

# Se debe estar en la carpeta /siapem/manual_de_instalacion

sudo cp -r material_archivos/postgresql/* /opt/wildfly/wildfly/

sudo cp -r material_archivos/sqlserver/* /opt/wildfly/wildfly/

# Sustituir el standalone.xml predeterminado que da wildfly por el que se encuentra en la carpeta "manual_archivos"

cp material_archivos/standalone.xml /opt/wildfly/wildfly/standalone/configuration/
```
### 5. Configuración del IDE

#### Instalar Eclipse IDE:

**Opción 1 - Desde sitio oficial:**
```bash
# Descargar Eclipse IDE for Enterprise Java and Web Developers
sudo wget https://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/2025-03/R/eclipse-jee-2025-03-R-linux-gtk-x86_64.tar.gz

# Extraer e instalar
tar -xvzf eclipse-jee-2025-03-R-linux-gtk-x86_64.tar.gz
sudo mv eclipse /opt/
sudo ln -s /opt/eclipse/eclipse /usr/local/bin/eclipse
```

#### Configurar Eclipse:

1. **Instalar JBoss Tools:**
   - `Help` → `Marketplace`
   - Buscar "JBoss Tools"
   - Instalar y reiniciar

2. **Configurar Perspectiva Git:**
   - `Window` → `Perspective` → `Open Perspective` → `Git`

3. **Clonar Repositorio:**
   - Hacer clic en "Clone a Git repository"
   - Ingresar URL y credenciales
   - Importar proyectos

### 7. Compilación y Despliegue

#### Configurar Proyecto Maven:
```bash
# Desde terminal del proyecto
cd ruta/al/proyecto/siapem

# Limpiar y compilar
mvn clean install
```

#### Configurar Servidor en Eclipse:

1. **Crear Servidor WildFly:**
   - `Window` → `Show View` → `Servers`
   - Crear nuevo servidor → `WildFly 17`
   - Home Directory: `/opt/wildfly/wildfly`
   - Runtime JRE: Java 8

2. **Desplegar Aplicación:**
   - Agregar `siapem-ear` al servidor
   - Full publish
   - Start server

---

## Estado del Proyecto

- **Estable**: Sistema en producción
- **Mantenimiento activo**: Actualizaciones regulares
- **Autores**: Célula SEDECO


---