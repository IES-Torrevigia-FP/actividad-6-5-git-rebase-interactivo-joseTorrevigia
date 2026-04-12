## git rebase -i: ventajas frente a dejar el historial de commits tal cual se creó

Sirve para reescribir, limpiar y organizar el historial de commits localmente antes de compartir ese historial de commits con otros compañeros.

## Describe con un ejemplo cuándo usarías:

- reword: 
- squash:
- drop:

Imagina que estás trabajando en una rama local llamada feature-login y tienes los siguientes 4 commits antes de enviarlos a revisión:

8a1b2c3 - "añado login"
4d5e6f7 - "corrijo typo en el login"
9g8h7i6 - "borro archivo de prueba que no sirve"
2j3k4l5 - "agrego validacion de contraseña"

Para limpiar esto, ejecutas git rebase -i HEAD~4 y usas los comandos así:

1. reword: Cuando el mensaje es vago o tiene errores
Ejemplo: El primer commit dice "añado login". Quieres que sea más profesional para el historial del proyecto.
Acción: Cambias pick por reword.
Resultado: Git se detendrá y te pedirá un nuevo mensaje. Lo cambias a: "Implementación inicial del módulo de autenticación".

2. squash: Cuando tienes micro-commits que deben ser uno solo
Ejemplo: El segundo commit "corrijo typo..." es un cambio mínimo que no debería existir por separado; es parte de la creación del login.
Acción: Cambias pick por squash en ese commit.
Resultado: Git fusionará ese cambio dentro del anterior. El historial se verá más limpio porque el "error" desaparece y se integra en la "implementación".

3. drop: Cuando un commit fue un error o ya no es necesario
Ejemplo: El tercer commit "borro archivo de prueba..." simplemente deshace algo que hiciste mal antes. En lugar de tener un commit que "crea basura" y otro que la "borra", es mejor que el historial ni sepa que existió.
Acción: Cambias pick por drop (o simplemente borras esa línea en el editor).
Resultado: Ese commit desaparece por completo. El archivo de prueba nunca llegará al servidor.

Tu lista final en el editor se vería así:

text
reword 8a1b2c3 añado login
squash 4d5e6f7 corrijo typo en el login
drop   9g8h7i6 borro archivo de prueba que no sirve
pick   2j3k4l5 agrego validacion de contraseña

## ¿Qué riesgos tiene usar mal git rebase -i (especialmente en ramas compartidas)?

Es conveniente no usar rebase en ramas compartidas por que genera demasiados problemas por que al reescribir los historiales de commits Git se descontrola, tambien, se puede perder trabajo ya realizado, alteracion del codigo, dificultad para auditar el proyecto, rotura de la integracion continua. En resumen, mejor ejecuta solamente rebase en ramas locales, y nunca hacer rebase en ramas ya compartidas.
