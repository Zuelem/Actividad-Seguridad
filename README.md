# Actividad-Seguridad
Trabajo en equipo desarrollado con Zuelem Chanillao, Cristían Díaz, Natalia Medel, Sary Viafara y Alexander Hass

# 🛡️ ACTIVIDAD 3: SEGURIDAD

---

## 
📚 Tabla de Contenido
- [1. Conceptos base](#1-conceptos-base)
- [2. Permissions (accesos en sistemas)](#2-permissions-accesos-en-sistemas)
- [3. A Good Password](#3-a-good-password)
- [4. Vulnerabilidades](#4-vulnerabilidades)
- [5. Intrusion Ataques](#5-intrusion-ataques)
- [6. Seguridad de red](#6-seguridad-de-red)
- [7. Conexion directa con desarrollo CLAVE](#7-conexion-directa-con-desarrollo-clave)
- [8. Caso practico real](#8-caso-practico-real)
- [9. Analogias](#9-analogias)
- [BONUS](#bonus)
---

##  1. Conceptos base

| 🧠 Concepto        | 📘 Definición simple                                      | ⚙️ Nivel técnico breve                                           | 💡 Ejemplo real                                              |
|------------------|----------------------------------------------------------|------------------------------------------------------------------|-------------------------------------------------------------|
| Permissions      | Son reglas que dicen qué puede o no hacer un usuario      | Control de acceso a recursos (archivos, APIs, sistema)           | Un usuario puede “leer” datos pero no “eliminarlos”          |
| Password segura  | Contraseña difícil de adivinar                           | Debe tener longitud, complejidad y no ser reutilizada            | G7!k9@pL2# en vez de 123456                                 |
| Vulnerabilidad   | Debilidad en un sistema                                  | Falla que puede ser explotada por un atacante                    | Un endpoint sin protección que expone datos                 |
| Intrusión        | Acceso no autorizado a un sistema                        | Uso de vulnerabilidades para entrar sin permiso                  | Un hacker accede a una base de datos                       |
| Seguridad de red | Protección de la comunicación y sistemas conectados      | Uso de firewalls, cifrado, control de acceso                     | Bloquear acceso externo a una base de datos                |

---

**Endpoint:**  
Un endpoint es una “dirección específica” dentro de una API. Es el lugar al que haces una petición para obtener o enviar datos. Es una URL que representa un recurso o acción. Ejemplo: http://localhost:3000/api/users  

👉 Este es un endpoint  
/api/users → recurso (usuarios)

---

##  2. Permissions (accesos en sistemas)

### ¿Qué es autenticación?
👉 Es verificar quién eres  
El sistema valida tu identidad  
Normalmente con usuario + contraseña  

📌 Ejemplo:  
Ingresas email y password para entrar  

---

### ¿Qué es autorización?
👉 Es verificar qué puedes hacer  
Ocurre después de autenticarte  
Define permisos dentro del sistema  

📌 Ejemplo:  
Puedes ver datos, pero no eliminarlos  

---

### ⚖️ Diferencia clave

Autenticación → identidad (quién eres)  
Autorización → permisos (qué puedes hacer)  

👉 Orden correcto:  
Te identificas  
El sistema decide tus permisos  

---

### 👨‍💻 Ejemplo developer

🔐 Login → ¿qué es?  
👉 Es el proceso de autenticación  

Envías credenciales (usuario/password)  
El servidor valida  
Si es correcto → te deja entrar  

---

👥 Roles (admin / user) → ¿qué es?  
👉 Es un sistema de autorización  

Define niveles de acceso  

Ejemplo:  
Admin → crear, editar, eliminar  
User → solo ver información  

---

### 🔗 Relación con APIs

Cuando trabajas con APIs:

🔑 Autenticación  
Envías un token (ej: JWT)  
El servidor valida quién eres  

**Token:** Un token es una “llave digital” que demuestra que ya iniciaste sesión. Es lo que usas para decirle al servidor: “soy yo, ya estoy autenticado”.

---

Autorización  
El servidor revisa tu rol o permisos  
Decide si puedes acceder al endpoint  

---

💡 Ejemplo completo

1. Login → obtienes token  
2. Llamas a API (/users)  
3. Servidor valida:  
  - Quién eres (autenticación)  
  - Qué puedes hacer (autorización)  

---

## 3. A Good Password

- Qué hace que sea segura: larga, con mayúsculas, minúsculas, números y símbolos.  
No guardar en texto plano: cualquiera que robe la base podría ver todas las contraseñas.  

- Hashing: transformar la contraseña en un código irreversible que se guarda. O sea es  una "huella digital" ilegible e irreversible (Seguro). El servidor nunca sabe cuál es tu contraseña real; sólo sabe cómo se ve su huella.  

Ejemplo desarrollador ¿Cómo se manejan contraseñas en backend?:  

- Usuario ingresa contraseña → backend la convierte en hash  
- Se guarda el hash en la base de datos  
- En login: se hace hash otra vez y se compara con el guardado  

---

## 4. Vulnerabilidades

Qué es: fallo en la app que permite ataques.  

Tipos comunes:  

- Exposición de datos sensibles : Contraseñas guardadas en texto plano, que es cuando las contraseñas no están encriptadas. Se ven a simple vista

- Configuración insegura (Misconfiguration): Es cuando un sistema o red está mal configurado y deja puertas abiertas sin querer. 

- Control de acceso roto: Cuando el sistema te deja entrar a una parte que no te corresponde (ej. entrar al panel de administrador siendo un usuario común).  

- Desbordamiento de búfer (Buffer Overflow): Se le envía más información de la que la memoria puede manejar, haciendo que el sistema colapse o ejecute órdenes extrañas.  

Ejemplo real:  
Formulario sin validar permite que alguien escriba DROP TABLE usuarios; y borre la base. ( ejemplo de SQL injection)  

---

## 5.-Intrusion-Ataques

- ¿Qué es una intrusión o un ataque?  
Es cuando una persona accede a un sistema sin permiso, aprovechando errores o debilidades para entrar.  

- ¿Qué busca un atacante?  
Robar información, modificar datos, obtener acceso total o usar el sistema para otros ataques.  

- ¿Qué pasa si una app es comprometida?  
Se pueden filtrar datos, perder información, dañar el sistema o afectar a los usuarios (ej: robo de cuentas).  

- Ejemplos:  
Robo de datos → contraseñas, correos o datos personales filtrados.  
Acceso no autorizado → un usuario normal entra al panel de administrador.  
Control del sistema → el atacante puede borrar o cambiar información.  

- En resumen, una intrusión es la consecuencia de una vulnerabilidad mal protegida.  

Qué es: cuando alguien entra sin permiso al sistema.  
Qué busca: robar datos, modificar información, o controlar el sistema.  
Consecuencia: datos comprometidos, pérdida de confianza, problemas legales.  

Ejemplos:  

- SQL Injection  
El atacante escribe código en formularios para manipular la base de datos.  
Puede acceder, modificar o borrar información.  

- Phishing  
Engaña al usuario para que entregue sus datos (correo, contraseña).  
Usa mensajes o páginas falsas que parecen reales.  

- Fuerza bruta (Brute Force)  
Prueba muchas contraseñas hasta adivinar la correcta.  
Funciona mejor si la contraseña es débil.  

---

## 6. Seguridad de red

- ¿Qué protege la seguridad de red?  
Protege los datos mientras viajan entre el usuario y el servidor, evitando que sean interceptados o manipulados.  

- ¿Qué es un firewall?  
Es un filtro que decide qué conexiones entran o salen de un sistema, bloqueando tráfico sospechoso.  

- ¿Qué es HTTPS y por qué es importante?  
Es una versión segura de HTTP que cifra la información, evitando que terceros puedan leerla o robarla.  

Ejemplo desarrollador:  

-¿Por qué usar HTTPS en APIs?  
Porque protege datos sensibles como tokens, contraseñas y datos de usuarios.  

Sin HTTPS, cualquiera en la red podría ver o robar esa información.  

Ejemplo simple:  

- Sin HTTPS → enviar contraseña es como escribirla en una postal (todos la ven).  
- Con HTTPS → es como enviarla en un sobre cerrado (nadie puede leerla).  

---

## 7. Conexion directa con desarrollo (CLAVE)

- ¿Qué errores comunes cometen los developers en seguridad?  

Confiar en el frontend: Creer que porque un botón está oculto o un formulario tiene validaciones en HTML/JavaScript, el usuario no puede enviar datos maliciosos. (Todo debe validarse en el backend).  

- Hardcodear secretos: Dejar contraseñas, tokens o claves de API directamente en el código fuente en lugar de usar variables de entorno (ofuscación)  

- Mensajes de error muy descriptivos: Mostrar al usuario el stack trace completo o el error exacto de la base de datos (esto le da pistas valiosas a un agente malicioso).  

- Usar librerías desactualizadas: Ignorar las alertas de seguridad de las dependencias (como paquetes de npm o dependencias de Python) que tienen vulnerabilidades conocidas.  

---

- ¿Qué pasaría si:  

- ¿No validas inputs?  
Abres la puerta a ataques como Inyección SQL (donde un atacante manipula tu base de datos) o Cross-Site Scripting (XSS) (donde inyectan código malicioso que se ejecuta en los navegadores de otros usuarios). Básicamente, dejas que el usuario dicte qué hace tu servidor.  

- ¿No proteges rutas?  
Ocurre lo que se llama Broken Access Control. Cualquiera que adivine o encuentre la URL (ej. tusitio.com/admin/borrar-usuarios) podría ejecutar acciones críticas sin estar autenticado o sin tener el rol necesario.  

- ¿No usas HTTPS?  
Todo el tráfico entre el navegador del usuario y tu servidor viaja en texto plano. Si alguien está en la misma red pública puede hacer un ataque Man-in-the-Middle y leer contraseñas, tarjetas de crédito y tokens de sesión como si fuera un libro abierto.  

---

## 8. Caso practico real

Escenario: “Un usuario logra acceder a información que no le corresponde.”  

- ¿Qué falló?  
Falló la Autorización (Authorization). El sistema supo quién era el usuario (Autenticación), pero falló en verificar si ese usuario tenía derecho a ver ese recurso en particular. Un ejemplo clásico es el IDOR (Insecure Direct Object Reference), donde un usuario cambia la URL de tusitio.com/factura/10 a tusitio.com/factura/11 y el servidor le muestra la factura de otra persona.  

- ¿Es problema de permisos, vulnerabilidad o intrusión?  
Es principalmente un problema de permisos debido a una vulnerabilidad lógica en el código. No necesariamente hubo una intrusión compleja (como hackear el servidor); el atacante simplemente le pidió la información al sistema, y el sistema, al estar mal programado, se la entregó.  

¿Cómo lo evitarías como developer?  

- Validación en el backend (Siempre): Antes de devolver un registro de la base de datos, verificar si el ID del usuario que hace la petición coincide con el ID del propietario del registro.  

- Control de Acceso Basado en Roles (RBAC): Implementar un sistema de roles estricto y verificar los permisos en cada endpoint de tu API, no solo ocultar elementos en la interfaz gráfica.  

- Usar UUIDs en lugar de IDs secuenciales: En vez de usar usuario/1, usuario/2, usar identificadores únicos universales (ej. usuario/550e8400-e29b-41d4-a716-446655440000). Esto no reemplaza la validación de permisos, pero evita que los atacantes puedan adivinar fácilmente las URLs de otros recursos.  

---

## 9. Analogias

| Concepto | Analogía |
|----------|---------|
| Permissions | El Gafete/Credencial (determina si puedes entrar a la oficina o solo al lobby). |
| Password | El Código PIN del ascensor (lo que tú sabes para demostrar quién eres). |
| Vulnerabilidad | Una Ventana mal cerrada o un sensor de movimiento que no funciona. |
| Intrusión | Un Colado (polizón) que logró entrar al área de servidores sin invitación. |
| Seguridad de red | El Equipo de Seguridad y Murallas que protegen todo el perímetro del terreno. |

---

## BONUS

🔐¿Qué es JWT? (JSON Web Token)  

Es un token seguro que el servidor genera cuando haces login.  
Contiene información (como el id del usuario) y una firma que evita que sea modificado.  

La forma de usarlo es:  

- El usuario inicia sesión  
- El backend genera el JWT  
- El cliente lo guarda y lo envía en cada petición  

Sirve para no pedir login repetidamente.  

---

🔑 ¿Qué es Autenticación con tokens?  

Es una forma de autenticación donde no se usan sesiones tradicionales, sino tokens. Su flujo de procesos es:  

- Haces login → servidor te da un token  
- Guardas ese token (en tu app o navegador)  
- Cada vez que haces algo (ver perfil, comprar, etc.), envías el token  
- El servidor lo revisa y dice: “ok, eres tú”  

Muy usado en APIs y apps modernas  

---

Ejemplo token en palabras simples. “Entrada a un concierto”:  

1. Llegas al concierto y muestras tu entrada (login con usuario/contraseña)  
2. Te ponen una pulsera (ese es el token)  
3. Ahora, cada vez que quieres entrar a una zona, solo muestras la pulsera  
4. No necesitas mostrar tu entrada otra vez  

La pulsera = token  

---

¿Qué es Rate limiting?  

Es una técnica para controlar cuántas solicitudes puede hacer un usuario en un tiempo determinado. Ejemplo:  

Máximo 100 requests por minuto  
Si supera el límite → se bloquea temporalmente  

Protege contra:  

Ataques de fuerza bruta  
Spam  
Sobrecarga del servidor  

---

## ✅ En resumen

JWT → tu “credencial digital”  
Tokens → forma moderna de autenticarse  
Rate limiting → límite de uso para seguridad 
