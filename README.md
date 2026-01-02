# Phishing-Evilginx-tool
🕵 Evilginx: UTILIZADA EN PHISHING AVANZADO (roba cookies de sesión y evade la MFA)
⭕ Hoy en día no se roban contraseñas… se roban sesiones enteras

En un artículo reciente de Malwarebytes (enlace en el comentario), se alerta sobre un aumento de ataques donde los actores utilizan técnicas de sesión hashtag#hijacking, para robar hashtag#cookies válidas, hacerse pasar por el usuario y evitar completamente la autenticación multifactor (hashtag#MFA).
Estos ataques ya han afectado a instituciones educativas y otros entornos sensibles‼️

La idea principal es preocupante 😱 :
si un atacante roba tu cookie de sesión, puede acceder igual que tú, sin contraseña y sin MFA‼️ 

En este laboratorio, he analizado Evilginx en modo hashtag#developer, lo que permite explorarlo de forma segura.

Evilginx funciona mediante hashtag#phishlets: plantillas que definen cómo cómo interceptar su flujo de autenticación para capturar las cookies de sesión. Tras configurar mi dominio local en /etc/hosts, cargué el phishlet correspondiente en la herramienta.

Lo interesante: mi navegador bloqueó la conexión mostrando el error
PR_END_OF_FILE_ERROR(Evilginx requiere dominio con SSL para funcionar 😏)
⭕ Esta exploración, mostró exactamente la barrera que los atacantes ya están superando usando certificados válidos para engañar al navegador.

¿Qué ocurre cuando Evilginx se configura con un dominio real con un certificado hashtag#SSL (por ejemplo, de Let’s Encrypt-->uso muy común entre los atacantes)?
Evilginx funciona como un hashtag#proxy inverso:
1- La víctima accede a una página aparentemente legítima
2- Evilginx actúa como INTERMEDIARIO‼️
La herramienta retransmite todo el tráfico entre la víctima y el servicio verdadero (Microsoft, Google, Meta, etc.)-->escucha en el puerto cifrado HTTPS 443
3- La víctima introduce sus credenciales...
Evilginx la envía al servicio real.
4- El servicio real valida la autenticación (incluyendo el MFA)
5- El servidor real devuelve una sesión válida
‼️Aquí es donde ocurre lo crítico:
Evilginx CAPTURA la session cookie y se la entrega al atacante.
6- El atacante reutiliza esa cookie para entrar como el usuario: sin contraseña, sin MFA.

💭 Si controlas la sesión, controlas al usuario 😏

☘️Recomendaciones para protegerse contra ataques de sesión (Evilginx y similares):
 1- Usar MFA de tipo “hardware”.
 2-Cerrar sesión y borrar cookies al usar equipos compartidos o públicos.
 3-Vigilar actividad de sesión
 4- No confiar solo en el candado HTTPS.
 5-Usar navegadores con aislamiento de sitios y extensiones de seguridad que alerten sobre phishlets o proxies sospechosos.
