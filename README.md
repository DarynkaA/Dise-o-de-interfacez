# 📱 MyApp Android

**MyApp** es una aplicación Android desarrollada en Kotlin que implementa una estructura de autenticación básica con navegación entre pantallas mediante el componente Navigation. Esta aplicación fue creada como proyecto educativo para comprender cómo se estructura una app con múltiples pantallas, cómo se navega entre ellas, y cómo se aplican buenas prácticas de diseño de interfaces de usuario en Android.

---

## 🚧 Propósito del Proyecto

Este proyecto tiene como objetivo enseñar y demostrar:

* Cómo utilizar `Fragments` con navegación declarativa.
* Cómo crear interfaces intuitivas y modernas usando `Material Design`.
* Cómo integrar animaciones `Lottie` para mejorar la experiencia del usuario.
* Cómo construir un flujo completo de autenticación (inicio, login, registro).

---

## 🛠️ Tecnologías y librerías utilizadas

* **Kotlin**: lenguaje moderno, seguro y expresivo para Android.
* **Android Jetpack**:

  * `Navigation Component`: para manejar flujos de navegación entre pantallas.
  * `Fragments`: pantallas modulares y reutilizables.
* **Material Components**: campos de texto, botones, layouts estilizados.
* **Lottie**: animaciones SVG en tiempo real mediante archivos `.json`.

---

## 🧭 Flujo de navegación

La navegación está definida en un archivo `navigation.xml` y sigue este orden:

```text
StartFragment (splash screen)
   └──▶ LoginFragment (login de usuario)
               └──▶ SignUpFragment (registro de usuario)
```

La clase `MainActivity` contiene el `NavHostFragment` encargado de alojar los fragmentos y dirigir la navegación.

---

## 🔎 Detalle por componente

### 📌 MainActivity

Clase principal que sirve como contenedor para los fragmentos. Tiene las siguientes responsabilidades:

* Aplica `enableEdgeToEdge()` para gestionar áreas del sistema como la barra de estado.
* Define el layout principal que contiene el `FragmentContainerView`.
* Aplica márgenes dinámicos usando `WindowInsetsCompat` para un diseño que respete notch y status bar.
* Inicializa el `NavController` en el método `onStart()` para habilitar la navegación entre fragmentos.

**Recomendación:** Usa `MainActivity` como única actividad en apps modernas, evitando múltiples activities.

---

### 🚀 StartFragment

Este fragmento funciona como una **pantalla de bienvenida o splash**. Su propósito es mostrar una animación durante 3 segundos y redirigir automáticamente al login.

**Características:**

* Muestra una animación Lottie (developer.json).
* Utiliza `Handler().postDelayed` para controlar la duración.
* Navega automáticamente al `LoginFragment`.

**Código clave:**

```kotlin
Handler().postDelayed({
  findNavController().navigate(R.id.action_startFragment_to_loginFragment)
}, 3000)
```

**Consejo:** Se puede usar `CoroutineScope` + `delay` como alternativa moderna.

---

### 🔐 LoginFragment

Pantalla principal de autenticación. Aquí el usuario puede iniciar sesión o acceder a la opción de crear cuenta.

**Elementos:**

* Campo de entrada para correo electrónico (`TextInputLayout`).
* Campo de contraseña con opción de mostrar u ocultar (`passwordToggleEnabled`).
* Botón para iniciar sesión.
* Botón con fondo personalizado para iniciar con Google.
* Texto clickeable para navegar a `SignUpFragment`.

**Lógica:**

* Utiliza `findNavController()` para navegar entre fragmentos.

**Mejoras sugeridas:**

* Validar entradas (email, contraseña) antes de permitir avanzar.
* Integrar lógica real de autenticación (Firebase, SQLite, etc.).

---

### 📝 SignUpFragment

Pantalla de registro de nuevos usuarios. Contiene múltiples campos de entrada para completar la creación de cuenta.

**Campos esperados:**

* Nombre completo
* Correo electrónico
* Contraseña
* Confirmación de contraseña

*(En el XML original los hints están repetidos, se recomienda diferenciarlos para claridad.)*

**Botón de acción:**

* `btnCalcular` que debería renombrarse a algo más descriptivo como `btnRegistrarse`.

**Recomendaciones:**

* Implementar validaciones de formulario.
* Usar ViewModel para manejar el estado de los datos.

---

### ☰ Menú (menu.xml)

Archivo XML con definición de dos ítems:

* `main`
* `cart`

Cada uno tiene un ícono asociado. Aunque los títulos están duplicados, se pueden personalizar.

**Sugerencia de uso:**

* Puede integrarse en un `BottomNavigationView` o `Toolbar`.

---

### 🧭 Navegación (navigation.xml)

Archivo central para la navegación con tres fragmentos:

* `startFragment` → pantalla inicial (splash).
* `loginFragment` → autenticación.
* `signUpFragment` → registro.

**Ejemplo de acción:**

```xml
<action
    android:id="@+id/action_loginFragment_to_signUpFragment"
    app:destination="@id/signUpFragment" />
```

**Consejo:** mantener nombres consistentes entre IDs y destinos para facilitar la lectura.

---

## 🎨 Diseño y estética

* **Tipografía**: fuente condensada y moderna (`notosans_condensed_bold`).
* **Animaciones**: `Lottie` para dar dinamismo sin afectar rendimiento.
* **Colores**: contraste fuerte para botones (`#D51A1A` sobre blanco).
* **Diseño responsive**: uso de `match_parent`, márgenes proporcionales y `gravity` para centrar elementos.

---

## 🧪 Cómo ejecutar el proyecto

1. Abre Android Studio.
2. Clona o importa el proyecto.
3. Verifica que las dependencias estén sincronizadas.
4. Conecta un emulador o dispositivo físico.
5. Ejecuta con `Run ▶` o `Shift + F10`.

**Compatibilidad:** Android 5.0 (API 21) en adelante.

---

## 🧠 Conclusiones y recomendaciones

* Separar la lógica de UI de la lógica de negocio usando `ViewModel` + `LiveData`.
* Validar todas las entradas de usuario antes de permitir navegación.
* Renombrar IDs y botones para mayor claridad y mantenimiento.
* Agregar `SafeArgs` para navegación segura con paso de parámetros.
* Expandir funcionalidades: recuperación de contraseña, integración con backend real, manejo de estados de carga.

Este proyecto es una base excelente para quien desea aprender la arquitectura moderna en Android. Desde navegación, diseño, fragmentos y estructura limpia, ofrece todos los componentes esenciales para evolucionar a una app robusta y escalable.
