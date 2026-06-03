# 🐳 MySQL Containerizado con Docker y HeidiSQL

> Despliegue de MySQL 8.0 en contenedor Docker sobre Ubuntu Server con generación de datos con Mockaroo y gestión con HeidiSQL.

---

## 📋 Descripción

Laboratorio de infraestructura de bases de datos donde se desplegó **MySQL 8.0** usando un **Dockerfile personalizado** en Ubuntu Server.  
Se generaron datos de prueba con **Mockaroo** y se gestionaron 3 tablas de datos desde **HeidiSQL** como cliente.

---

## 🛠️ Stack y Herramientas

| Tecnología | Uso |
|-----------|-----|
| Ubuntu Server (KVM) | Servidor de base de datos |
| Docker | Contenedor de MySQL |
| MySQL 8.0 | Motor de base de datos |
| HeidiSQL 12.15 | Cliente GUI de base de datos |
| Mockaroo | Generación de datos de prueba |
| SSH | Acceso al servidor |

---

## 📁 Dockerfile

```dockerfile
# Imagen oficial de MySQL
FROM mysql:8.0

# Configurar contraseña root
ENV MYSQL_ROOT_PASSWORD=mi_clave_segura

# Crear base de datos inicial
ENV MYSQL_DATABASE=parcial_db

# Exponer puerto estándar
EXPOSE 3306
```

---

## 🔧 Despliegue

```bash
# Conectar al servidor Ubuntu via SSH
ssh moises@192.168.122.9

# Instalar Docker y Docker Compose
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker $USER

# Crear directorio del proyecto
mkdir proyecto-parcial && cd proyecto-parcial

# Construir imagen
docker build -t mi-mysql-parcial .

# Levantar contenedor
docker run -d --name mysql-contenedor   -p 0.0.0.0:3306:3306   mi-mysql-parcial

# Verificar
docker ps
# CONTAINER ID: af2d6412ed55
# STATUS: Up 15 seconds
# PORTS: 0.0.0.0:3306->3306/tcp
```

---

## 📊 Base de Datos y Tablas

### Tablas creadas en `parcial_db`

#### 1. `automoviles` — 114 registros
| Campo | Tipo |
|-------|------|
| id | INT (PK) |
| car_make | VARCHAR |
| car_model | VARCHAR |
| car_model_year | YEAR |
| car_vin | VARCHAR |
| car_color | VARCHAR |
| car_price | DECIMAL |
| car_mileage | INT |
| car_condition | VARCHAR |
| car_owner_name | VARCHAR |

#### 2. `social` — 130 registros
| Campo | Tipo |
|-------|------|
| id | INT (PK) |
| username | VARCHAR |
| bio | TEXT |
| followers_count | INT |
| following_count | INT |
| profile_pic | VARCHAR (URL) |
| status | ENUM |
| location | VARCHAR |

#### 3. `videojuegos` — 90 registros
| Campo | Tipo |
|-------|------|
| id | INT (PK) |
| titulo | VARCHAR |
| genero | VARCHAR |
| plataforma | VARCHAR |
| fecha_lanzamiento | DATE |
| precio | DECIMAL |
| stock | INT |
| calificacion | DECIMAL |
| desarrollador | VARCHAR |
| es_multiusuario | TINYINT |

---

## 🔌 Conexión con HeidiSQL

```
Host/IP:     192.168.122.9
Puerto:      3306
Usuario:     root
Network:     MySQL on RDS
```

---

## 🧠 Aprendizajes

- Creación de imágenes Docker personalizadas con Dockerfile
- Variables de entorno en contenedores (`ENV`)
- Exposición de puertos entre host y contenedor
- Gestión visual de bases de datos con HeidiSQL
- Generación masiva de datos de prueba con Mockaroo
