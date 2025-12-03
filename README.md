# Fiexpress
## Sistema Integral de Control de Asistencia y Fichajes
FiExpress es una solución completa de gestión de asistencia laboral que combina hardware IoT y software empresarial. Permite el control de entradas y salidas mediante tarjetas RFID y una plataforma web administrativa, ofreciendo estadísticas en tiempo real, gestión de incidencias y notificaciones de seguridad vía Telegram.

## Características Principales

### Panel Web (Frontend)

    Diseño Moderno: Interfaz con estética Glassmorphism Dark responsiva.

    Gestión de Personal: CRUD completo de empleados, departamentos, roles y horarios.

    Dashboard Interactivo: Gráficos en tiempo real (Chart.js) sobre puntualidad, horas extra y ausencias.

    Reportes: Tablas dinámicas con filtros avanzados y exportación de datos.

    Seguridad: Login con autenticación JWT/Cookies y roles (Admin, Supervisor, Empleado).

### Backend API

    Lógica de Negocio: Procesamiento automático de estados de asistencia (Normal, Retraso, Falta).

    Integración Telegram: Alertas inmediatas a administradores sobre intentos de fichaje no autorizados o tarjetas desconocidas.

    Modo Captura: Funcionalidad para registrar nuevas tarjetas RFID remotamente desde la web.

### Hardware IoT

    Fichaje Rápido: Lectura de tarjetas RFID Mifare (RC522).

    Feedback Inmediato: Pantalla OLED para mostrar hora, estado de conexión y resultado del fichaje.

    Indicadores: Sistema de LEDs y Buzzer para feedback visual y sonoro.

    Conectividad: Sincronización automática de hora (NTP) y comunicación HTTP segura con la API.

## Arquitectura del Sistema

### El sistema sigue una arquitectura cliente-servidor con integración IoT:

    Dispositivo ESP32: Lee la tarjeta RFID y envía una petición POST al servidor.

    API (.NET 8): Recibe la petición, valida la tarjeta contra la base de datos SQL Server, registra el fichaje y devuelve el estado.

    Telegram Bot: Si la tarjeta es inválida o hay un error de seguridad, el backend notifica inmediatamente al chat de administradores.

    Cliente Web: Consume la API para visualizar los datos actualizados en tiempo real.

### Stack Tecnológico
´´´Plaintext
+---------------+-----------------------+------------------------------------------------------------------+
|     AREA      |      TECNOLOGIA       |                             DETALLES                             |
+---------------+-----------------------+------------------------------------------------------------------+
| Backend       | .NET 8.0 (C#)         | ASP.NET Core Web API, Entity Framework Core 9                    |
+---------------+-----------------------+------------------------------------------------------------------+
| Base de Datos | SQL Server            | Relacional, Code-First (o Database-First adaptable)              |
+---------------+-----------------------+------------------------------------------------------------------+
| Frontend      | HTML5 / JS / CSS3     | Bootstrap 5.3, TailwindCSS (Login), Chart.js, SweetAlert2        |
+---------------+-----------------------+------------------------------------------------------------------+
| Firmware      | C++ (Arduino IDE)     | Librerias: MFRC522, Adafruit GFX/SSD1306, ArduinoJson            |
+---------------+-----------------------+------------------------------------------------------------------+
| Hardware      | ESP32 DevKit V1       | Modulo RFID RC522, OLED 0.96" I2C                                |
+---------------+-----------------------+------------------------------------------------------------------+
´´´
