# Checklist de seguridad práctica para AI Agents (Español)

> Alineado con las categorías reales del OWASP Top 10 for LLM Applications (2025). Cada punto es una acción concreta: márcalos todos antes de lanzar.
> Herramienta complementaria: [Web-Vuln-Scanner](https://github.com/Ezra-Zhao/Web-Vuln-Scanner) (escáner de vulnerabilidades web: encuentra las fallas de verdad)

## 1. Protección contra la inyección de prompts (OWASP LLM01 / LLM05 / LLM07)

- [ ] Coloca el system prompt en un nivel que el usuario no pueda sobrescribir (rol de sistema separado o jerarquía explícita de instrucciones).
- [ ] Envuelve las entradas no confiables con delimitadores (``` o etiquetas `<user_input>`) y deja claro que son datos, no instrucciones por ejecutar.
- [ ] Regla inquebrantable: ninguna instrucción del usuario puede anular las del sistema; los trucos tipo "ignora todo lo anterior" no funcionan.
- [ ] Valida la salida del modelo antes de ejecutarla (esquema JSON o lista permitida); si no cumple el formato, se rechaza sin adivinar.
- [ ] Antes de llamar una herramienta, verifica que los parámetros estén dentro de lo esperado (límites numéricos, valores permitidos, rutas permitidas).
- [ ] Marca el contenido de páginas web, documentos y correos externos como fuente no confiable: no puede disparar llamadas a herramientas por sí solo.
- [ ] Trata el contenido recuperado por RAG como entrada no confiable y cita siempre la fuente.
- [ ] Haz pruebas de regresión periódicas con casos de inyección de prompts (directa, indirecta y progresiva en varias rondas).
- [ ] Registra y alerta los intentos de inyección; no los descartes en silencio.

## 2. Permisos mínimos para herramientas (OWASP LLM06 / LLM10)

- [ ] Dale a cada agente solo las herramientas necesarias para su tarea (principio de mínimo privilegio).
- [ ] Todo denegado por defecto, lista blanca para permitir: lo que no esté explícitamente autorizado no se puede llamar.
- [ ] Las operaciones peligrosas (borrar bases de datos, enviar correos, pagos, cambiar la configuración de producción) requieren confirmación humana.
- [ ] Doble confirmación o flujo de aprobación para operaciones de alto riesgo; en producción crítica, revisión por varias personas.
- [ ] Ejecuta las herramientas en un sandbox o entorno aislado, con red y sistema de archivos restringidos.
- [ ] Pon límites de tiempo de espera y de reintentos para evitar bucles infinitos que quemen tu cuota de tokens (OWASP LLM10: consumo sin límites).
- [ ] Limita el número de llamadas a herramientas y el presupuesto de tokens por tarea; si se supera, detén todo y alerta.
- [ ] Limpia los mensajes de error de las herramientas antes de pasarlos al modelo: nada de rutas internas, detalles de pila ni fragmentos de secretos.

## 3. Manejo de datos sensibles (OWASP LLM02)

- [ ] Nunca pongas API keys, contraseñas ni tokens en prompts, comentarios de código, ejemplos o documentación.
- [ ] Inyecta los secretos con variables de entorno o un gestor de secretos; en el código solo se referencian, nunca se escriben.
- [ ] Anonimiza o convierte en tokens los datos personales (nombre, teléfono, documento de identidad, dirección) antes de enviarlos al modelo.
- [ ] Enmascara secretos y datos personales en logs, trazas y stack traces.
- [ ] Define un plazo claro de retención para los datos de usuario, bórralos al vencer e informa la política al usuario.
- [ ] Filtra la información sensible antes de guardarla en la memoria entre sesiones; el usuario debe poder ver, exportar y borrar su memoria.
- [ ] Elimina las muestras sensibles de los datos de entrenamiento y ajuste; revisa también los conjuntos de evaluación.

## 4. Auditoría y monitoreo

- [ ] Registra todo el flujo: prompt de entrada, parámetros de las herramientas, salida del modelo y confirmaciones humanas, todo con marca de tiempo e ID de solicitud.
- [ ] Guarda los logs de auditoría en un almacenamiento independiente e inmutable (solo anexar), separado físicamente de los logs de negocio.
- [ ] Alerta ante comportamientos anómalos: muchas llamadas a herramientas en poco tiempo, intentos de escalada de privilegios, palabras clave de inyección, picos de consumo de tokens.
- [ ] Revisa los logs de auditoría cada semana, con foco en lo rechazado y lo interceptado por humanos.
- [ ] Ten un plan de respuesta a incidentes: contener → investigar → corregir → aprender, con responsables claros en cada paso.
- [ ] Asigna a cada agente o servicio una identidad y permisos propios: así puedes localizar el problema y revocar el acceso rápido.
- [ ] Monitorea que la salida del modelo no filtre información sensible (fragmentos del system prompt, formatos típicos de claves); bloquéalo al detectarlo.

## 5. Cadena de suministro y despliegue (OWASP LLM03 / LLM04)

- [ ] Revisa las dependencias de terceros (librerías, modelos, skills, plugins) antes de usarlas: estado de mantenimiento, CVEs conocidos, reputación del autor.
- [ ] Fija todas las versiones de dependencias (lockfile) y valida cada actualización primero en un entorno de pruebas.
- [ ] Instala skills y plugins solo de fuentes confiables, verificando firma o hash; lo de origen desconocido no se activa.
- [ ] Versiona el modelo y el system prompt como código; los cambios pasan por revisión.
- [ ] Rota los secretos periódicamente (cada 90 días o menos); si sospechas una filtración, rótalos de inmediato.
- [ ] Separa estrictamente los secretos de producción y de pruebas; en pruebas usa solo datos falsos.
- [ ] Antes de desplegar, pasa una línea base de seguridad: al menos un caso de prueba de inyección, uno de escalada y uno de filtración.
- [ ] Usa imágenes mínimas de contenedor o máquina virtual, aplica los parches de seguridad a tiempo y no ejecutes como root.

---

*39 puntos en total. Úsalo como lista de verificación de lanzamiento: sin los 39 marcados, no hay despliegue.*
