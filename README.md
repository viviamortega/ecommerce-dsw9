# ecommerce-dsw9

**Sitio de e-commerce completo con Node.js, Express y MySQL**

Aplicación de comercio electrónico construida con tecnologías modernas, integración con PayPal y base de datos relacional.

---

## 📋 Características

- 🛒 **Carrito de compras** con sesiones persistentes
- 💳 **Integración PayPal** para pagos seguros
- 🗄️ **Base de datos MySQL** con ORM Sequelize
- 🎨 **Plantillas EJS** con sistema de layouts
- 🔐 **Gestión de sesiones** segura
- 📱 **Interfaz responsiva** con Bootstrap/CSS personalizado
- 🚀 **Deployment** en Render.com

---

## 🛠️ Tech Stack

| Tecnología | Versión | Uso |
|-----------|---------|-----|
| **Node.js** | >=18.0.0 | Runtime |
| **Express.js** | ^5.2.1 | Framework web |
| **Sequelize** | ^6.37.8 | ORM para MySQL |
| **MySQL2** | ^3.22.3 | Driver MySQL |
| **EJS** | ^5.0.2 | Motor de plantillas |
| **Express-session** | ^1.19.0 | Gestión de sesiones |
| **dotenv** | ^17.4.2 | Variables de entorno |

---

## 📦 Instalación

### Requisitos previos
- Node.js >= 18.0.0
- MySQL 8.0+
- npm o yarn

### Pasos de instalación

```bash
# 1. Clonar el repositorio
git clone <url-repositorio>
cd ecommerce-dsw9

# 2. Instalar dependencias
npm install

# 3. Configurar variables de entorno (ver sección siguiente)
cp .env.example .env

# 4. Ejecutar la aplicación
npm start

# 5. Para desarrollo con auto-reload (recomendado)
npm run dev
```

---

## ⚙️ Configuración

### Variables de Entorno

Crea un archivo `.env` en la raíz del proyecto con las siguientes variables:

```env
# Base de datos MySQL
DB_NAME=ecommerce_db
DB_USER=usuario_mysql
DB_PASSWORD=tu_contraseña
DB_HOST=localhost
DB_PORT=3306

# Sesiones
SESSION_SECRET=tu_secret_key_de_sesion_aleatorio

# PayPal
PAYPAL_CLIENT_ID=tu_client_id
PAYPAL_CLIENT_SECRET=tu_client_secret
PAYPAL_MODE=sandbox  # o 'live' en producción

# Servidor
PORT=3000
NODE_ENV=development
```

### Obtener credenciales PayPal

1. Accede a [PayPal Developer](https://developer.paypal.com/)
2. Crea una aplicación de prueba
3. Copia `Client ID` y `Client Secret`
4. Usa modo `sandbox` para pruebas

---

## 📁 Estructura del Proyecto

```
ecommerce-dsw9/
├── app.js                    # Punto de entrada principal
├── package.json              # Dependencias del proyecto
├── .env                      # Variables de entorno (no subir a Git)
├── .gitignore               # Archivos ignorados en Git
│
├── config/
│   └── database.js          # Configuración de conexión MySQL
│
├── models/                  # Modelos de datos (Sequelize)
│   ├── Product.js           # Modelo de productos
│   ├── Order.js             # Modelo de órdenes
│   ├── OrderItem.js         # Modelo de items en órdenes
│   └── index.js             # Exportación y relaciones
│
├── routes/                  # Rutas de la API
│   ├── products.js          # Rutas de productos
│   ├── cart.js              # Rutas del carrito
│   └── checkout.js          # Rutas de checkout/pago
│
├── controllers/             # Controladores (lógica de negocio)
│   └── [controllers aquí]
│
├── views/                   # Plantillas EJS
│   ├── layout.ejs           # Plantilla base
│   ├── index.ejs            # Página principal
│   ├── cart.ejs             # Página del carrito
│   ├── checkout.ejs         # Página de checkout
│   └── 404.ejs              # Página de error
│
├── public/                  # Archivos estáticos
│   ├── css/
│   ├── js/
│   └── images/
│
└── seeders/                 # Scripts de población de BD (opcional)
```

---

## 🚀 Uso

### Ejecutar localmente

```bash
npm start
```

La aplicación estará disponible en `http://localhost:3000`

### Rutas principales

| Ruta | Método | Descripción |
|------|--------|-------------|
| `/` | GET | Página principal |
| `/products` | GET | Listado de productos |
| `/cart` | GET | Ver carrito |
| `/cart/add` | POST | Agregar producto al carrito |
| `/checkout` | GET | Página de checkout |
| `/checkout/process` | POST | Procesar pago con PayPal |

---

## 🗄️ Base de Datos

### Modelos y relaciones

**Product** (Productos)
```
- id (PK)
- name
- description
- price
- stock
- createdAt
- updatedAt
```

**Order** (Órdenes)
```
- id (PK)
- totalAmount
- status (pending, paid, cancelled)
- paypalTransactionId
- createdAt
- updatedAt
```

**OrderItem** (Items de órdenes)
```
- id (PK)
- OrderId (FK)
- ProductId (FK)
- quantity
- price
```

### Relaciones
- Order **hasMany** OrderItem
- Product **hasMany** OrderItem

---

## 💳 Integración PayPal

### Flujo de pago

1. Usuario agrega productos al carrito (sesión local)
2. Accede a checkout
3. Se redirige a PayPal
4. Pago aprobado/rechazado
5. Se registra la orden en BD
6. Confirmación al usuario

### Usar en sandbox

```env
PAYPAL_MODE=sandbox
PAYPAL_CLIENT_ID=ARZFQn7ltwi1xDgrmgn9eHHb08...
PAYPAL_CLIENT_SECRET=EF7dpDC1nKTO8v_BwBAO...
```

---

## 🔐 Seguridad

- Variables sensibles en `.env` (nunca en Git)
- Sesiones con secret seguro
- Cookie-parser para cookies seguras
- HTTPS recomendado en producción
- Certificado SSL incluido (`ca.pem`)

---

## 🚢 Deployment en Render

### Pasos para desplegar

1. **Crear repositorio Git**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git push
   ```

2. **Conectar con Render**
   - Accede a [render.com](https://render.com)
   - New > Web Service
   - Conecta tu repositorio GitHub

3. **Configurar variables de entorno**
   - En Render dashboard > Environment
   - Agrega todas las variables de `.env`

4. **Configurar base de datos**
   - Aiven.io o similar para MySQL
   - Actualizar `DB_HOST`, `DB_USER`, `DB_PASSWORD`

5. **Deploy automático**
   - Cada push a main dispara un deployment

---

## 📝 Scripts disponibles

```bash
npm start       # Inicia el servidor
npm run dev     # Desarrollo (si está configurado)
```

---

## 🐛 Troubleshooting

### Error: Cannot find module 'dotenv'
```bash
npm install
```

### Error de conexión a BD
- Verifica credenciales en `.env`
- Comprueba que MySQL está corriendo
- Valida el host y puerto

### Variables de entorno no se cargan
```bash
# Asegúrate de ejecutar desde la raíz del proyecto
pwd  # Debe mostrar: /ruta/a/ecommerce-dsw9
npm start
```

---

## 👨‍💻 Autor

**Vivivam Ortega**

---

## 📄 Licencia

Este proyecto está bajo licencia MIT.

---

## 🤝 Contribuciones

Las contribuciones son bienvenidas. Por favor:

1. Fork el proyecto
2. Crea una rama (`git checkout -b feature/AmazingFeature`)
3. Commit cambios (`git commit -m 'Add AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

---

## 📞 Soporte

Para soporte, contacta a: [tu-email@example.com]

---

## 📚 Recursos útiles

- [Express.js Docs](https://expressjs.com/)
- [Sequelize Docs](https://sequelize.org/)
- [EJS Docs](https://ejs.co/)
- [PayPal Developer](https://developer.paypal.com/)
- [MySQL Docs](https://dev.mysql.com/doc/)