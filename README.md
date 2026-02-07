# 🚴‍♂️ Velorace - E-commerce de Ciclismo

Velorace es una plataforma de comercio electrónico completa, moderna y de alto rendimiento diseñada para la venta de bicicletas y accesorios. El proyecto implementa una arquitectura separada (Frontend y Backend) contenerizada, con un fuerte enfoque en la **escalabilidad**, el **rendimiento** y la **experiencia de usuario**.

---

## 🚀 Tecnologías Principales

### Backend (API REST)

* **Framework:** FastAPI (Python) – API rápida y asíncrona.
* **Base de Datos:** PostgreSQL (SQLAlchemy ORM).
* **Migraciones:** Alembic.
* **Caché y Rendimiento:** Redis.
* **Validación de Datos:** Pydantic.
* **Seguridad:** Rate Limiting (middleware propio) y autenticación JWT.
* **Testing:** Pytest.

### Frontend (SPA)

* **Framework:** React (Vite).
* **Estilos:** Tailwind CSS.
* **Gestión de Estado:** Zustand (stores para Auth y Carrito).
* **Gráficos:** Recharts (monitoreo de latencia en admin).
* **Testing:** Jest + React Testing Library.

### Infraestructura y DevOps

* **Contenedores:** Docker y Docker Compose.
* **Servidor Web:** Nginx (Reverse Proxy).

---

## ✨ Características del Sistema

### Para el Cliente

* **Catálogo de Productos:** Exploración de bicicletas y accesorios con filtrado por categorías.
* **Carrito de Compras:** Estado global persistente del carrito.
* **Sistema de Pedidos:** Checkout, generación de órdenes y facturación (Bills).
* **Perfil de Usuario:** Historial de pedidos y gestión de direcciones.
* **Reseñas:** Comentarios y valoraciones de productos.

### Para el Administrador

* **Dashboard Administrativo:** Panel de control protegido.
* **Gestión de Inventario:** CRUD completo de productos y categorías.
* **Monitoreo de Rendimiento:** Gráficos en tiempo real de latencia del sistema (LatencyChart).
* **Gestión de Clientes:** Visualización de usuarios registrados.

---

## 🛠️ Instalación y Despliegue (Docker)

La forma más sencilla de levantar el proyecto es utilizando **Docker Compose**, que orquesta el Backend, Frontend, la Base de Datos y Redis.

### 1️⃣ Clonar el repositorio

```bash
git clone https://github.com/tu-usuario/velorace.git
cd velorace
```

### 2️⃣ Configurar variables de entorno

```bash
cd backend
cp .env.example .env
# Edita el archivo .env con tus credenciales si es necesario
```

### 3️⃣ Levantar los servicios

```bash
docker-compose up --build
```

Esto iniciará:

* **Backend:** [http://localhost:8000](http://localhost:8000)
* **Frontend:** [http://localhost:5173](http://localhost:5173) (o el puerto configurado en Nginx/Docker)
* **PostgreSQL**
* **Redis**

---

## 🔧 Desarrollo Local (Sin Docker)

### Backend

```bash
cd backend
python -m venv venv
source venv/bin/activate  # o venv\\Scripts\\activate en Windows
pip install -r requirements.txt

# Ejecutar migraciones
alembic upgrade head

# Iniciar servidor
uvicorn main:app --reload
```

La documentación de la API (Swagger) estará disponible en:
**[http://localhost:8000/docs](http://localhost:8000/docs)**

### Frontend

```bash
cd frontend
npm install
npm run dev
```

---

## 📂 Estructura del Proyecto

El proyecto sigue una arquitectura limpia y modular:

```plaintext
velorace/
├── backend/
│   ├── app/                # Lógica principal
│   ├── config/             # Configuraciones (DB, Redis, Logs)
│   ├── controllers/        # Endpoints de la API
│   ├── middleware/         # Rate limiter, Request ID
│   ├── migrations/         # Versiones de Alembic
│   ├── models/             # Modelos SQLAlchemy
│   ├── repositories/       # Acceso a datos (DAO)
│   ├── schemas/            # Esquemas Pydantic (DTOs)
│   ├── services/           # Lógica de negocio
│   └── tests/              # Tests unitarios e integración
│
├── frontend/
│   ├── src/
│   │   ├── components/     # Componentes UI
│   │   ├── hooks/          # Custom hooks
│   │   ├── pages/          # Vistas principales
│   │   ├── services/       # Llamadas a la API
│   │   └── store/          # Estado global (Auth, Cart)
│   └── public/             # Assets estáticos
│
└── docker-compose.yml      # Orquestación de contenedores
```

---

## 🧪 Testing

### Backend

```bash
cd backend
pytest
```

Incluye pruebas de controladores, servicios, repositorios y concurrencia.

---

## 🛡️ Seguridad y Rendimiento

Este proyecto no es solo una tienda básica, incluye características avanzadas para entornos de producción:

* **Rate Limiting:** Protección contra abuso de API y ataques DDoS.
* **Caching con Redis:** Optimización de endpoints de lectura frecuente (ej. catálogo).
* **Logging Estructurado:** Logs configurados para trazabilidad y monitoreo.
