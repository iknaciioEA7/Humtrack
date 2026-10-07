HumTrack12X - Documentación Resumida
1. Resumen del Proyecto
HumTrack12X es una aplicación móvil de monitoreo IoT desarrollada en Android Studio con Kotlin, conectada a una pasarela local en Raspberry Pi (Python/Flask) y respaldada por una base de datos centralizada en la nube de AWS RDS MySQL.
2. Arquitectura de Comunicación
[ Dispositivo Android (App) ] 
       │ (Wi-Fi / Red Local)
       ▼
[ Raspberry Pi / Debian (API Flask en Puerto 5000) ]
       │ (Conexión Segura PyMySQL)
       ▼
[ AWS RDS MySQL (Tabla 'usuarios' y 'sesiones') ]
3. Características Principales de Seguridad
•
Hashing de Contraseñas: Las credenciales nunca se almacenan en texto plano; se utiliza un algoritmo seguro con hashlib.pbkdf2_hmac y salt aleatorio.
•
Tokens de Sesión: Los inicios de sesión generan tokens de sesión seguros almacenados en la base de datos y protegidos en la app móvil mediante EncryptedSharedPreferences (Android Keystore).
•
Protección contra Inyección SQL: Todas las consultas ejecutadas por la API utilizan sentencias preparadas y parametrizadas (%s).
4. Instrucciones Rápidas de Ejecución
1.
Base de Datos: Ejecutar el script  database/schema.sql en MySQL Workbench conectado a AWS RDS.
2.
Servidor (Raspberry Pi): Ubicarse en la carpeta backend/, verificar que la librería pymysql y flask estén presentes, y ejecutar:
Shell Script
python3 main.py
3.
Aplicación Android: Configurar la IP del servidor en ApiConfig.BASE_URL (dentro de  ApiClient.kt), compilar el APK e instalarlo en los dispositivos móviles conectados a la misma red Wi-Fi.
