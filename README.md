# 🍽️ Restaurante App — Fundamentos de Manejo de Eventos con Tkinter

🌟 **Estudiante:** Ramiro Alcoser A.

## 📚 Tema

**Semana 15:** Conceptos fundamentales de manejo de eventos en la aplicación **restaurante_app**, construida con **Tkinter**.

## 🎯 Objetivo de aprendizaje

Evolucionar el proyecto **restaurante_app** de la Semana 14 **sin reconstruirlo desde cero**. La aplicación conserva el inicio de sesión, la arquitectura por capas, la persistencia en JSON, la consulta de usuarios y el CRUD de productos. En esta semana se agrega una operación sencilla de **venta** para observar el flujo completo entre una acción del usuario, un botón con `command=`, un callback, el servicio y la respuesta visual. 🧑‍🍳💰

## 🔄 Continuidad desde la Semana 14

La interfaz mantiene los mismos colores, estilos, iconos, menú lateral, barra de estado y organización general construidos previamente. La nueva sección **Ventas** se integra como una capacidad adicional de la misma aplicación, sin romper nada de lo ya funcional. ✅

## 🆕 Nueva funcionalidad: Ventas

La venta relaciona:

```text
Usuario + Producto + Fecha -> Venta
```

La sección **Ventas** permite:

- 👤 seleccionar un usuario registrado con `ttk.Combobox`;
- 🍔 seleccionar un producto registrado con `ttk.Combobox`;
- 🖱️ pulsar el botón **Registrar venta**;
- ⚙️ ejecutar el callback `registrar_venta()` mediante `command=`;
- 💾 guardar la venta en `datos/ventas.json`;
- 📊 mostrar las ventas registradas en un `ttk.Treeview`.

Flujo educativo del evento:

```text
Accion del usuario -> Boton -> command= -> callback -> servicio -> JSON -> Treeview actualizado
```

## 🗂️ Estructura del proyecto

```text
restaurante_app/
├── assets/
│   ├── icons/
│   │   ├── home.png
│   │   ├── users.png
│   │   ├── products.png
│   │   ├── sales.png        # icono de la nueva seccion Ventas
│   │   ├── logout.png
│   │   ├── add.png
│   │   ├── edit.png
│   │   ├── delete.png
│   │   ├── search.png
│   │   └── clean.png
│   └── logo/
│       ├── logo.png
│       └── icono.png
├── datos/
│   ├── productos.json
│   ├── usuarios.json
│   └── ventas.json
├── modelos/
│   ├── __init__.py
│   ├── usuario.py
│   ├── producto.py
│   └── venta.py
├── servicios/
│   ├── __init__.py
│   ├── archivo_servicio.py
│   └── restaurante_servicio.py
├── ui/
│   ├── __init__.py
│   ├── login_view.py
│   └── main_view.py
├── main.py
└── README.md
```

## 🧱 Capas del proyecto

- 🧩 `modelos/`: define las clases `Usuario`, `Producto` y `Venta`, con validaciones básicas mediante `property` para evitar campos vacíos o precios inválidos.
- ⚙️ `servicios/`: contiene la lógica de consulta, registro, actualización, eliminación y persistencia. `RestauranteServicio` también registra y valida las ventas.
- 💾 `datos/`: guarda la información persistente en archivos JSON (`usuarios.json`, `productos.json` y `ventas.json`).
- 🖼️ `ui/`: contiene las vistas creadas con Tkinter (`LoginView` y `MainView`).
- 🎨 `assets/icons/`: iconos PNG usados por los botones. Si falta un icono, la aplicación sigue funcionando solo con texto.
- 🏷️ `assets/logo/`: identidad visual del sistema, usada en el login y en el icono de la ventana.

## 🔔 Icono opcional de Ventas

Para el nuevo botón del menú lateral se espera opcionalmente este archivo:

```text
restaurante_app/assets/icons/sales.png
```

No es obligatorio incluirlo. La función `cargar_icono()` devuelve `None` si no lo encuentra y el botón se muestra solo con texto. 🙂

## 🖥️ Pantallas principales

- 🔐 **LoginView:** pantalla de inicio de sesión.
- 🏠 **Inicio:** panel de resumen con tarjetas de usuarios, productos y ventas.
- 👤 **Usuarios:** pantalla de consulta de usuarios registrados.
- 🍔 **Productos:** pantalla de gestión con formulario, botones y tabla para el CRUD básico.
- 🧾 **Ventas:** pantalla nueva para seleccionar un usuario, seleccionar un producto y registrar una venta simple.

## 🧩 Componentes Tkinter utilizados

- 🏷️ `Label`: textos y títulos.
- ⌨️ `Entry`: campos de entrada para login y formulario de productos.
- 🔽 `ttk.Combobox`: selectores de usuario y producto en la vista de ventas.
- 🔘 `ttk.Button`: botones de navegación y acciones con `command=`.
- 📊 `ttk.Treeview`: tablas de usuarios, productos y ventas.
- 🧭 `ttk.Scrollbar`: barra de desplazamiento para las tablas.
- 💬 `messagebox`: mensajes simples de confirmación o error.
- 🎨 `ttk.Style`: estilos reutilizables para botones y encabezados.

## ⚡ Concepto de evento

```text
Usuario hace clic -> Boton genera una accion -> command ejecuta un callback
-> el callback consulta/solicita al servicio -> la interfaz refresca el resultado
```

En **Ventas**, el botón usa `command=self.registrar_venta`. Ese callback obtiene el usuario y el producto seleccionados en los `Combobox`, delega la validación y el registro a `RestauranteServicio.registrar_venta()`, y luego actualiza la tabla y muestra un mensaje de confirmación o error. 🔁

## 💾 Persistencia

Los usuarios, productos y ventas se cargan desde JSON al iniciar la aplicación, a través de `ArchivoServicio`.

```text
restaurante_app/datos/usuarios.json
restaurante_app/datos/productos.json
restaurante_app/datos/ventas.json
```

Al registrar una venta, `RestauranteServicio` agrega el objeto a la colección en memoria, convierte las ventas a datos serializables y escribe `ventas.json`. La interfaz **nunca** lee ni escribe los archivos JSON directamente. 🔒

## 🚫 Qué NO se trabaja todavía

En la Semana 15 no se utilizan eventos avanzados. No se implementa:

- `bind()`;
- doble clic;
- eventos de teclado;
- eventos de mouse;
- `<<TreeviewSelect>>`;
- carga automática desde tablas;
- selección reactiva de filas;
- facturación, carrito de compras o inventario avanzado.

Estos conceptos quedan para una siguiente semana sobre manejo de eventos. ⏭️

## 🛠️ Requisitos

- 🐍 Python 3.x
- 🪟 Tkinter disponible en la instalación de Python

No se requieren dependencias externas.

## ▶️ Cómo ejecutar

Desde la carpeta del proyecto:

```bash
python main.py
```

En Windows, si el comando `python` no está disponible en la terminal, puede usarse:

```bash
py main.py
```

## 🔑 Credenciales de demostración

Usuario: `admin`
Contraseña: `1234`

También puede usarse:


Usuario: `caja1`
Contraseña: `abcd`

Usuario: `caja2`
Contraseña: `abcd`

## ⚠️ Nota educativa

El proyecto mantiene una implementación sencilla para que el estudiante pueda seguir el crecimiento progresivo de la aplicación:

```text
Semana 14: componentes y contenedores
Semana 15: accion -> command= -> callback -> servicio -> persistencia -> respuesta visual
```

La venta no representa todavía un sistema comercial completo. Solo muestra una relación clara entre un usuario y un producto para estudiar los fundamentos del manejo de eventos mediante botones. 🎓

La autenticación de este proyecto es local y simulada; las contraseñas se guardan en JSON solo con fines pedagógicos y no representan una práctica segura para producción. 🔐

## 🚀 Próxima evolución

En las siguientes prácticas se incorporarán progresivamente eventos más avanzados (`bind()`, selección reactiva, `<<TreeviewSelect>>`) sobre esta misma base de modelos, servicios, ui y main.py. 🌱
