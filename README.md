
# AIOT2025

## Descripción

El estudiante manipulará sensores y actuadores conectados a hardware abierto para procesar y almacenar datos, desarrollando habilidades teóricas, prácticas y de integración de sistemas IoT.

---

## Contenido del Curso

### Parte Teórica

- Basado en **NetAcad Python Fundamentals 2**\
Capítulo 1
![image](https://github.com/user-attachments/assets/034afded-84a2-4912-b2e6-4f6971f1f130)
Capítulo 2\
![image](https://github.com/user-attachments/assets/916d5ec7-b405-45d1-8078-2585e2da3f52)
Capítulo 3\
![image](https://github.com/user-attachments/assets/aad7a913-9b64-484a-abdb-d7b2f5e342b2)
Capítulo 4\
![image](https://github.com/user-attachments/assets/a7836531-9a34-486c-bf66-a91cd210f93d)
Prueba Final del curso Fundamentos de Python 2 (PE2)\
![image](https://github.com/user-attachments/assets/b84129a4-ee14-4ebe-8f98-17dbb58c949c)

### Parte Práctica

#### Ejercicios Evaluados

- **Almacenamiento de Datos** (15 puntos)
- **Control de Actuadores** (15 puntos)
- **Soldadura - Circuito funcional en placa fenólica**
- **Soldadura - Figura 2D o 3D**

#### Actividades en Clase

- **Videos demostrativos**
- **CRUD en PostgreSQL**
- **Instalaciones y configuraciones básicas**
- **LED y botón con Raspberry Pi**
- **Conexión MQTT en Node-RED**

---

## Requisitos

- **Raspberry Pi con Raspbian instalado**
- **PostgreSQL configurado**
- **Node-RED instalado y configurado**
- **Materiales de soldadura (placa fenólica, estaño, cautín)**
- **Sensores y actuadores según las prácticas definidas**

---

# Instalaciones y Configuraciones  
### Instalar Raspberry Pi con Raspbian instalado
## Requisitos  

- **Tarjeta SD**: Mínimo **32 GB**, máximo **64 GB**.  
- **Software**: [Raspberry Pi Imager](https://www.raspberrypi.com/software/).  

## Instalación del Sistema Operativo  

1. Descargar e instalar **Raspberry Pi Imager**.  
2. Insertar la **tarjeta SD** en el PC.  
3. Ejecutar **Raspberry Pi Imager** y seguir estos pasos:  
   - Seleccionar el sistema operativo deseado.  
   - Elegir la tarjeta SD como destino.  
   - Configurar las opciones avanzadas:  
     - **Nombre de host**.  
     - **Usuario y contraseña**.  
     - **Red Wi-Fi** (si aplica).  
     - **Zona horaria y región**.  
4.  Grabar el sistema operativo en la tarjeta SD y esperar a que finalice.  
5. Insertar la tarjeta SD en la **Raspberry Pi** y encender el dispositivo.
![image](https://github.com/user-attachments/assets/13b5588c-1340-4e27-b5f5-99823194cee3)

### Instalación y Configuración de PostgreSQL en Raspberry Pi  
## Requisitos Previos  
- Raspberry Pi con **Raspberry Pi OS** instalado.  
- Conexión a internet.  
- Permisos de administrador (**sudo**).

## Instalación de PostgreSQL  
```sh
  1. Instalación de PostgreSQL:
    sudo apt install postgresql -y
  
  3. Verificar la instalación:
  
    psql --version
  
  4. Iniciar el servicio PostgreSQL
    sudo systemctl start postgresql
  
  5. Habilitar PostgreSQL para que inicie automáticamente
    sudo systemctl enable postgresql
  
  6. Cambiar al usuario PostgreSQL
    sudo -i -u postgres
  
  7. Acceder a la terminal interactiva de PostgreSQL
    psql
  8. Crear un nuevo usuario de bases de datos
    CREATE USER utng WITH PASSWORD '1234';
  9. Conceder privilegios
    GRANT ALL PRIVILEGES ON DATABASE aiot UTNG
  10. Salir de la terminal
    \q
```

  ## Creación de Tablas en PostgreSQL
  ```sh
  CREATE TABLE sensors (
      id SERIAL PRIMARY KEY,
      name VARCHAR(100),
      type VARCHAR(50),
      record_at TIMESTAMP DEFAULT now()
  );
  
  CREATE TABLE sensor_details (
      id SERIAL PRIMARY KEY,
      sensor_id INTEGER,
      user_id INTEGER,
      value VARCHAR(100),
      record_at TIMESTAMP DEFAULT now(),
      FOREIGN KEY (sensor_id) REFERENCES sensors(id),
      FOREIGN KEY (user_id) REFERENCES users(id)
  );
  
  CREATE TABLE actuators (
      id SERIAL PRIMARY KEY,
      name VARCHAR(100),
      type VARCHAR(50),
      record_at TIMESTAMP DEFAULT now()
  );
  
  CREATE TABLE actuator_details (
      id SERIAL PRIMARY KEY,
      actuator_id INTEGER,
      user_id INTEGER,
      state VARCHAR(100),
      record_at TIMESTAMP DEFAULT now(),
      FOREIGN KEY (actuator_id) REFERENCES actuators(id),
      FOREIGN KEY (user_id) REFERENCES users(id)
  );
```







