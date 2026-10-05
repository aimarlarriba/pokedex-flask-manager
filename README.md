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

## 📌 Executive Summary

**Pokédex Ecosystem** is a modular, resilient full-stack web platform built with **Python and Flask**, designed around **Clean Architecture**, **Separation of Concerns**, and **Automated Data Synchronization**.

Unlike traditional static web catalogs, the platform implements an **Auto-Healing Architecture** that continuously monitors local persistence integrity against the external public **PokeAPI**. It automatically hydrates relational schemas upon detecting missing entities or inconsistent database states. Additionally, it features an interactive battle team builder, recursive evolution tree exploration, dynamic elemental type compatibility analytics, a conversational chatbot assistant, and an automated test suite.

---

## 🛠️ Key Engineering Highlights

### 1. 🔄 Self-Healing Persistence Architecture
* **Startup Integrity Verification:** During the `create_app()` bootstrap lifecycle, the `GestorBD` engine audits key database integrity indicators (1,025 Pokémon species and 484 evolution graph relations).
* **Hot-Hydration Worker:** If the local SQLite database is missing or incomplete, a background synchronization worker consumes the external PokeAPI to structure, index, and persist the entity graph without requiring manual seed scripts or external migrations.

### 2. 🧩 Modular Decoupling via Blueprints & Application Factory
The application eliminates monolithic controllers by organizing functional domains into isolated **Flask Blueprints** registered onto the Application Factory pattern:
* **`IU_LPokemon`:** High-performance catalog search and dynamic filtering engine (name, generation, type, base stats) powered by asynchronous JavaScript.
* **`IU_Equipos`:** Custom Pokémon team builder with relational user persistence and aggregated combat stat analytics.
* **`IU_CadenaEvolutiva`:** Recursive graph traversal algorithm for complex branching evolution trees.
* **`IU_CompatibilidadTipos`:** Dynamic damage multiplier matrix calculating dual-type elemental resistances and weaknesses.
* **`IU_Chatbot`:** Integrated conversational assistant handling domain-specific inquiries.
* **`IU_Admin` & `IU_Amigos`:** Role-based access control (RBAC), request auditing, user moderation, and social networking features (friend requests, team sharing).

### 3. 🧪 Automated Testing & Reliability
The codebase includes an automated unit and integration testing suite in `tests/`:
* `test_gestion_usuarios.py`: Authentication lifecycle, session security, role authorization, and password validation.
* `test_gestion_equipos.py`: Team creation, relational updates, capacity validation, and team persistence.
* `test_chatbot.py`: Natural language query matching and intent resolution.
* `test_lpokemon.py`: Catalog query filters and attribute validation.
* `test_changelog.py`: Audit trails and user activity tracking.

---

## 🏗️ Project Architecture

```text
pokedex-flask-manager/
├── app/
│   ├── controller/
│   │   ├── model/             # Domain models (Catalogo, GestorEquipos, PokeEspecie...)
│   │   └── ui/                # Blueprint UI controllers (Admin, Chatbot, Teams, Catalog...)
│   ├── database/
│   │   ├── GestorBD.py        # Data Access Layer & automated synchronization worker
│   │   ├── ResultadoSQL.py    # Strongly-typed SQL cursor wrapper
│   │   └── schema.sql         # Relational DDL schema (Tables, foreign keys, indexes)
│   ├── static/                # Frontend assets (CSS3 custom properties, modular JS)
│   └── templates/             # Decoupled Jinja2 views organized by Blueprint domain
├── tests/                     # Automated unit and integration test suite
├── config.py                  # Environment runtime configuration
├── crear_admins.py            # CLI administrative provisioning tool
├── requirements.txt           # Strict production dependencies manifest
└── run.py                     # Application entry point
```

---

## ⚙️ Installation & Setup

### 1. Clone the repository and set up a virtual environment:
```bash
git clone https://github.com/aimarlarriba/pokedex-flask-manager.git
cd pokedex-flask-manager

# Create virtual environment
python -m venv venv

# Activate on Windows:
venv\Scripts\activate

# Activate on Linux/macOS:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### 2. Run the Application:
```bash
python run.py
```
> [!NOTE]
> On the first launch, the application automatically provisions `identifier.sqlite` using `schema.sql` and hydrates catalog data from PokeAPI transparently. Access the web interface at:
> `http://localhost:1111`

### 3. Run the Automated Test Suite:
```bash
pytest
# or alternatively via standard unittest:
python -m unittest discover tests
```

---

## 👥 Academic Context & Authorship

Originally conceptualized as a collaborative university project for the **Information Systems Analysis & Design (ADSI)** course at the **University of the Basque Country (UPV/EHU)**.

Original student contributors: *Eneko Rodríguez, Urko Horas, Aimar Larriba, Iván Salazar, and Aitor Cotano*.

This repository represents the **individual architectural refactoring, expansion, and ongoing maintenance** by **[Aimar Larriba](https://github.com/aimarlarriba)**, engineered to satisfy modern clean architecture, modular decoupling, and industry production standards.

---

## ⚖️ License

Distributed under the **MIT** License. See [LICENSE](LICENSE) for more details.
