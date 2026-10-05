[🇬🇧 English](README.md) | [🇪🇸 Español](README.es.md)

# Pokédex Ecosystem & Resilient Data Sync Platform

<p align="center">
  [![CI Test Suite](https://github.com/aimarlarriba/pokedex-flask-manager/actions/workflows/ci.yml/badge.svg)](https://github.com/aimarlarriba/pokedex-flask-manager/actions/workflows/ci.yml)
  <img src="https://img.shields.io/badge/Python-3.10%20%7C%203.11%20%7C%203.12-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python Version"/>
  <img src="https://img.shields.io/badge/Framework-Flask-000000?style=for-the-badge&logo=flask&logoColor=white" alt="Flask Framework"/>
  <img src="https://img.shields.io/badge/Architecture-Factory%20%26%20Blueprints-007ACC?style=for-the-badge" alt="Architecture Pattern"/>
  <img src="https://img.shields.io/badge/Storage-SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white" alt="SQLite"/>
  <img src="https://img.shields.io/badge/Tests-Pytest%20Passing-success?style=for-the-badge&logo=pytest&logoColor=white" alt="Tests"/>
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge" alt="MIT License"/>
</p>

---

## 📌 Resumen Ejecutivo

**Pokédex Ecosystem** es una plataforma web modular y resiliente desarrollada con **Python y Flask**, diseñada bajo estrictos principios de **Arquitectura Limpia**, **Separación de Responsabilidades** y **Sincronización Automatizada de Datos**.

A diferencia de catálogos estáticos convencionales, la plataforma implementa una **arquitectura auto-reparable (*Auto-Healing Architecture*)** que monitoriza la integridad de la persistencia local contra la API externa de **PokeAPI**, hidratando automáticamente el esquema relacional en caso de detectar inconsistencias o registros faltantes. Además, integra un constructor de equipos interactivo, visualización de cadenas evolutivas dinámicas, matriz de efectividad de tipos, asistente conversacional y una suite completa de pruebas automatizadas.

---

## 🛠️ Aspectos Destacados de Ingeniería

### 1. 🔄 Arquitectura de Persistencia Auto-Reparable (Self-Healing)
* **Verificación de Integridad en Arranque:** Durante el ciclo de inicialización del `create_app()`, el motor del `GestorBD` evalúa métricas clave de integridad del catálogo (1.025 especies de Pokémon y 484 relaciones evolutivas).
* **Worker de Hidratación en Caliente:** Si la base de datos local SQLite se encuentra vacía o incompleta, se activa automáticamente un proceso de sincronización con la API pública para descargar, estructurar y persistir el grafo de entidades sin requerir intervención manual ni migraciones externas.

### 2. 🧩 Desacoplamiento Modular mediante Blueprints & Factory Pattern
La aplicación prescinde por completo de controladores monolíticos, organizando sus dominios en módulos independientes registrados sobre el patrón **Application Factory**:
* **`IU_LPokemon`:** Motor de búsqueda y filtrado dinámico (nombre, generación, tipo, estadísticas base) optimizado con JavaScript asíncrono.
* **`IU_Equipos`:** Constructor de equipos Pokémon con persistencia relacional por usuario y cálculo agregado de estadísticas de combate.
* **`IU_CadenaEvolutiva`:** Algoritmo de resolución de árboles y ramificaciones evolutivas complejas.
* **`IU_CompatibilidadTipos`:** Matriz dinámica de resistencias, debilidades y multiplicadores de daño según el tipo elemental.
* **`IU_Chatbot`:** Asistente interactivo integrado para consultas rápidas sobre el universo Pokémon.
* **`IU_Admin` & `IU_Amigos`:** Sistema de roles, auditoría de peticiones, moderación y funcionalidades sociales (solicitudes de amistad, inspección de equipos ajenos).

### 3. 🧪 Testing Automatizado & Fiabilidad
El repositorio incluye una suite de pruebas unitarias y de integración organizadas en el directorio `tests/`:
* `test_gestion_usuarios.py`: Flujos de autenticación, control de sesiones, roles y validación de contraseñas.
* `test_gestion_equipos.py`: Creación, actualización, límites de integrantes y persistencia de equipos.
* `test_chatbot.py`: Validación de respuestas e intenciones del asistente conversacional.
* `test_lpokemon.py`: Filtrado de catálogo y validación de atributos.
* `test_changelog.py`: Trazabilidad y registro de actividad de los usuarios.

---

## 🏗️ Arquitectura del Proyecto

```text
pokedex-flask-manager/
├── app/
│   ├── controller/
│   │   ├── model/             # Modelos de dominio (Catalogo, GestorEquipos, PokeEspecie...)
│   │   └── ui/                # Controladores Blueprints (Admin, Chatbot, Equipos, Pokemon...)
│   ├── database/
│   │   ├── GestorBD.py        # Capa de abstracción de datos y worker de sincronización
│   │   ├── ResultadoSQL.py    # Envoltorio tipado de cursores SQL
│   │   └── schema.sql         # Esquema DDL relacional (Tablas, llaves foráneas, índices)
│   ├── static/                # Assets frontend (CSS3 custom properties, JavaScript modular)
│   └── templates/             # Vistas Jinja2 desacopladas por vistas de Blueprint
├── tests/                     # Suite de pruebas automatizadas
├── config.py                  # Parámetros de entorno y configuración de runtime
├── crear_admins.py            # Utilidad CLI para provisionar superusuarios
├── requirements.txt           # Manifiesto estricto de dependencias de producción
└── run.py                     # Punto de entrada de la aplicación
```

---

## ⚙️ Instalación y Puesta en Marcha

### 1. Clonar el repositorio y preparar el entorno virtual:
```bash
git clone https://github.com/aimarlarriba/pokedex-flask-manager.git
cd pokedex-flask-manager

# Crear entorno virtual
python -m venv venv

# Activar en Windows:
venv\Scripts\activate

# Activar en Linux/macOS:
source venv/bin/activate

# Instalar dependencias
pip install -r requirements.txt
```

### 2. Ejecutar la Aplicación:
```bash
python run.py
```
> [!NOTE]
> Al arrancar por primera vez, la aplicación creará automáticamente `identifier.sqlite` a partir de `schema.sql` y sincronizará los registros de PokeAPI de forma transparente. La interfaz estará disponible en:
> `http://localhost:1111`

### 3. Ejecutar la Suite de Pruebas:
Para validar la integridad de todos los módulos y controladores:
```bash
pytest
# o alternativamente con unittest:
python -m unittest discover tests
```

---

## 👥 Contexto Académico y Autoría

Este proyecto fue concebido y desarrollado originalmente como una práctica colaborativa para la asignatura de **Análisis y Diseño de Sistemas de Información (ADSI)** en la **Universidad del País Vasco (UPV/EHU)**. 

Equipo de desarrollo original: *Eneko Rodríguez, Urko Horas, Aimar Larriba, Iván Salazar y Aitor Cotano*.

El presente repositorio constituye la **evolución y refactorización técnica individual** mantenida por **[Aimar Larriba](https://github.com/aimarlarriba)**, orientada a cumplir con estándares de arquitectura limpia, desacoplamiento modular y preparación para entornos profesionales.

---

## ⚖️ Licencia

Distribuido bajo la Licencia **MIT**. Consulta el archivo [LICENSE](LICENSE) para más información.
