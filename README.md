# Proyecto Integrador · Red de tres edificios

Diseño, implementación, pruebas y documentación en **Cisco Packet Tracer** de una red jerárquica (acceso → IDF → MDF/Core) que conecta **360 nodos** en **3 edificios**, con VLSM, 8 VLAN, trunks 802.1Q, enrutamiento inter-VLAN en el Core, STP y SSH.

**Materia:** Conmutación de Redes · Unidad 2 (VLAN y Trunk) · TecNM Campus Colima · Ingeniería en Sistemas Computacionales
**Equipo:** 4 integrantes (3 técnicos + 1 de documentación y vigilancia) · **Fuente de los requisitos:** `proyecto_redes_U2.pdf`

## Equipo

| Rol | Integrante | Es dueño de | Suplente |
|---|---|---|---|
| R1 · Documentación y vigilancia | `<NOMBRE R1>` | Fases 0, 1 y 9, **todo el expediente PDF**, bitácora, registro de evidencias, calendario, puerta documental.| R2 |
| R2 · Maqueta, VLSM y pruebas | `<NOMBRE R2>` | Fases 2, 3 y 8, **llave del `.pkt`**, banco de pruebas | R3 |
| R3 · VLAN, trunks e inter-VLAN | `<NOMBRE R3>` | Fases 4 y 5, IP de las 85 PCs, Extra VTP | R4 |
| R4 · STP y seguridad | `<NOMBRE R4>` | Fases 6 y 7, credenciales y SSH | R2 |

**Dos controles por fase, y ninguno lo hace el dueño:**
1. **Revisión técnica** (en rueda): lo de R2 lo revisa R3, lo de R3 lo revisa R4 y lo de R4 lo revisa R2.
2. **Puerta documental** (R1, vigila): comprueba que hay evidencias legibles con nombre estándar, notas al día, bitácora y registro completos y ninguna clave. En las fases de R1 (0, 1 y 9) lo comprueba el revisor técnico.

## La red en una tabla

| Concepto | Cantidad |
|---|---|
| Edificios · plantas por edificio | 3 · 3 |
| Nodos (por planta · por edificio · total) | 40 · 120 · **360** |
| Switches (Core · IDF · acceso) | 1 · 3 · 18 = **22** |
| Enlaces entre switches | **39** (36 cobre + 3 fibra monomodo de 250, 450 y 650 m) |
| PCs mínimas en la maqueta | **85** |
| Bloque de direcciones | `10.80.0.0/16` (VLSM) |

## Estado de las fases

Cambia la casilla **solo cuando el revisor técnico** marcó `terminado` y R1 dio la puerta documental (ver [Definición de terminado](#cuándo-una-fase-está-terminada)).

| Fase | Qué se obtiene | Dueño → Revisor técnico | Puerta documental (R1) | Estado |
|---|---|---|---|---|
| [0 · Planeación](Fases/Fase%200%20-%20Planeacion%20y%20reparto%20del%20equipo.md) | Roles, calendario, reglas, banco de pruebas | R1 → R3 | — | ☐ |
| [1 · Investigación técnica](Fases/Fase%201%20-%20Investigacion%20tecnica.md) | Base técnica con fuentes | R1 redacta · A→R2 · B→R3 · C→R4 · D→R2 | — | ☐ |
| [2 · Diseño físico y maqueta](Fases/Fase%202%20-%20Diseno%20fisico%20y%20maqueta.md) | 22 switches, 39 enlaces, 85 PCs | R2 → R3 | ☐ | ☐ |
| [3 · Diseño lógico y VLSM](Fases/Fase%203%20-%20Diseno%20logico%20y%20VLSM.md) | Subredes, gateways, IP de administración | R2 → R3 | ☐ | ☐ |
| [4 · VLAN y trunks](Fases/Fase%204%20-%20VLAN%20y%20trunks.md) | 8 VLAN y trunks podados (capas 1–3) | R3 → R4 | ☐ | ☐ |
| [5 · Inter-VLAN](Fases/Fase%205%20-%20Enrutamiento%20inter-VLAN%20en%20el%20Core.md) | Core Capa 3 con 8 SVI (capa 4) | R3 → R4 | ☐ | ☐ |
| [6 · STP y prueba de falla](Fases/Fase%206%20-%20STP%20y%20prueba%20de%20falla.md) | Core = Root 4096 y falla recuperada (capa 5) | R4 → R2 | ☐ | ☐ |
| [7 · SSH y seguridad](Fases/Fase%207%20-%20SSH%20y%20seguridad.md) | SSH solo desde TI (capas 6–8) | R4 → R2 | ☐ | ☐ |
| [8 · Pruebas de aceptación](Fases/Fase%208%20-%20Pruebas%20de%20aceptacion.md) | 12 pruebas y matriz de conectividad | R2 → R3 | ☐ | ☐ |
| [9 · Expediente y demostración](Fases/Fase%209%20-%20Expediente%20y%20demostracion.md) | PDF final y ensayos | R1 → R4 (auditoría) y R2 (PDF) | — | ☐ |
| [Extra · VTP](Fases/Extra%20-%20VTP%20opcional.md) | +5 pts, solo si hay margen | R3 → R4 | ☐ | ☐ |

## Estructura del repositorio

```text
.
├── README.md
├── Proyecto Integrador - Red de tres edificios.md   ← nota principal (hub)
├── Fases/        ← una nota por fase: ficha, plan paso a paso, revisión y pendientes
├── Referencia/   ← inventario, mapeo de 360 nodos (+ CSV), configuraciones por capas, Bitácora del equipo
└── Anexos/       ← evidencias (EV-*.png), imágenes del PDF y el Registro de evidencias
```

- Las notas son **Markdown para Obsidian** (enlaces `[[...]]`, callouts, Dataview). En GitHub se leen bien, pero los `[[enlaces]]` solo navegan dentro de Obsidian.
- Por dónde empezar: [`Fase 0`](Fases/Fase%200%20-%20Planeacion%20y%20reparto%20del%20equipo.md) (quién es quién, calendario y reglas) y la [Bitácora del equipo](Referencia/Bitacora%20del%20equipo.md).

## Cómo se sube una fase (flujo de trabajo)

Cada fase se sube **en su propia rama** y entra a `main` mediante un **Pull Request que aprueba su revisor**. Así queda en Git quién hizo, quién revisó y con qué evidencias.

```text
main ──────────────────────────────●─────────────●──────────►
        \                          ↑ merge       ↑ merge
         fase-4-vlan-trunks ──●──●─┘             │
                                  PR + revisión   │
                              fase-5-inter-vlan ──┘
```

1. **Actualiza y crea la rama** de tu fase (nombre `fase-N-tema`, por ejemplo `fase-4-vlan-trunks`):
   ```bash
   git switch main && git pull
   git switch -c fase-4-vlan-trunks
   ```
2. **Trabaja y sube evidencias mientras avanzas** (no al final). Commits pequeños:
   ```bash
   git add Anexos/EV-F04-SW-A-PB-01-show-vlan-brief.png Fases/
   git commit -m "F4: capas 1-3 verificadas en edificio A"
   git push -u origin fase-4-vlan-trunks
   ```
3. **Abre el Pull Request** hacia `main` y pide revisión a **tu revisor técnico** y a **R1** (puerta documental). Usa la lista de abajo como descripción.
4. **El revisor técnico** hace la *Revisión cruzada* de la nota de la fase (incluida la prueba oral). **R1** revisa la lista documental y aprueba. Solo después el revisor técnico corrige `estado:` a `terminado` **dentro del PR** y lo aprueba. **No se hace merge sin las dos aprobaciones.**
5. **Merge a `main`.** Después actualiza la tabla de estado de este README y la [Bitácora](Referencia/Bitacora%20del%20equipo.md) (versión del `.pkt`, firma de revisión).

### Convención de commits
`F{fase}: qué se hizo` · `docs:` para documentación suelta · `evid:` si solo se agregan capturas.
Ejemplos: `F6: prueba de falla en SW-A-PB-02 con evidencias` · `evid: F7 rechazo de Telnet desde Finanzas`.

### Plantilla de descripción del Pull Request
```markdown
## Fase
F__ · dueño: R_ · revisor técnico: R_ · puerta documental: R1

## Qué incluye
- [ ] Pasos del plan de ejecución completados (F__-01 … F__-__)
- [ ] Evidencias en `Anexos/` con nombre `EV-F__-{equipo}-{qué}.png`
- [ ] Notas corregidas con lo que realmente se hizo
- [ ] Versión del `.pkt` registrada en la Bitácora (si aplica)

## Para el revisor técnico
- [ ] Revisión cruzada de la nota de la fase hecha
- [ ] Repetí al menos una verificación yo mismo en el `.pkt`
- [ ] Prueba oral superada
- [ ] Sin contraseñas ni claves en archivos o capturas

## Para R1 (puerta documental)
- [ ] Evidencias en `Anexos/` con nombre estándar, nombre del equipo visible y legibles al 100 %
- [ ] Notas, bitácora y [Registro de evidencias](Anexos/Registro%20de%20evidencias.md) al día
- [ ] Tablero de despliegue y tabla de estado del README actualizados
```

## Cuándo una fase está terminada

Solo si se cumplen las **siete** condiciones (detalle en la Fase 0, sección B.3):

1. Todos los pasos del plan de ejecución hechos con el resultado esperado.
2. Evidencias subidas a `Anexos/`, legibles al 100 % y **mostrando el nombre del equipo**.
3. Las notas dicen lo que **realmente** se implementó (documentación = implementado).
4. Versión nueva del `.pkt` registrada, si se tocó la maqueta.
5. Limitaciones de Packet Tracer anotadas en el apartado D de la Fase 1.
6. El **revisor técnico** comprobó los criterios y superó la prueba oral.
7. **R1 dio la puerta documental** (evidencias, notas y bitácora al día; en las fases de R1 la comprueba el revisor).

## Evidencias

- Nombre: `EV-F{fase}-{equipo}-{qué muestra}.png` (ejemplo: `EV-F06-SW-CORE-show-spanning-tree-summary.png`).
- **La captura la toma quien hace la prueba; R1 la verifica** (nombre del equipo visible, legible, sin claves) y mantiene el registro.
- Van en `Anexos/`. La lista completa de lo que hay que capturar, con responsable y estado, está en el [Registro de evidencias](Anexos/Registro%20de%20evidencias.md).
- Una captura vale solo si: tiene el nombre estándar, **se ve el prompt o la ventana del equipo**, se lee al 100 % de zoom y **no muestra ninguna clave**.

## Reglas del repositorio

| Regla | Por qué |
|---|---|
| **Nunca** subir contraseñas ni claves reales (`enable`, cuentas SSH, VTP). Se usan marcadores `<CLAVE_...>`; las reales viven en el archivo de `Credenciales/` de la carpeta compartida | El repositorio es compartido y el historial de Git no se olvida |
| El **`.pkt` maestro no se versiona aquí**: vive en la carpeta compartida (`PKT/`) con la regla de la llave del `.pkt`. En el repo solo se anota la versión y, al final, la huella SHA-256 del archivo entregado | Es un binario que no se puede fusionar; dos personas editándolo lo sobrescriben |
| Nada de `git push --force` y nadie hace commit directo a `main` | Protege el trabajo de los demás |
| `git pull --rebase` antes de editar la **Bitácora** o este README | Son archivos que tocan varias personas; una fila por persona evita conflictos |
| Si cambias la maqueta, corrige la nota **el mismo día** y anótalo en la bitácora de cambios | El PDF exige que la documentación corresponda con lo implementado |

### `.gitignore` sugerido
```gitignore
# Credenciales: jamás al repo
Credenciales/
*.secret
*claves*

# Packet Tracer: el .pkt vive en la carpeta compartida
*.pkt
*.pka

# Obsidian: estado personal de cada quien
.obsidian/workspace*.json
.obsidian/cache

# Sistema
.DS_Store
Thumbs.db
```

## Documentación clave

| Qué | Dónde |
|---|---|
| Visión general, reglas del PDF y rúbrica | [Nota principal](Proyecto%20Integrador%20-%20Red%20de%20tres%20edificios.md) |
| Inventario de 22 switches y tabla de 39 enlaces | [Inventario y conexiones físicas](Referencia/Inventario%20y%20conexiones%20fisicas.md) |
| 360 nodos con switch, puerto, VLAN e IP · hoja de control de las 85 PCs | [Mapeo de los 360 nodos](Referencia/Mapeo%20de%20los%20360%20nodos.md) · [CSV](Referencia/Proyecto-Nodos-360.csv) |
| Configuración por capas (se pega y verifica una capa a la vez) | [Core e IDF](Referencia/Config%20-%20Core%20e%20IDF.md) · [Switches de acceso](Referencia/Config%20-%20Switches%20de%20acceso.md) |
| Versiones del `.pkt`, cambios, respuestas del profesor, tablero de los 22 switches | [Bitácora del equipo](Referencia/Bitacora%20del%20equipo.md) |
| Capturas requeridas por el expediente | [Registro de evidencias](Anexos/Registro%20de%20evidencias.md) |

## Entregables del proyecto

1. **Maqueta funcional:** archivo `.pkt` con las configuraciones **guardadas**.
2. **Expediente técnico:** PDF con calidad de informe profesional.
3. **Demostración técnica:** presentación en vivo; el profesor puede preguntar a cualquiera sobre cualquier parte.

## Estructura del repo

```text
equipo/
  R1_brisa/ · R2_gonzalo/ · R3_maki/ · R4_estrella/
    configs/      ← running-config y comandos
    evidencias/   ← capturas y pruebas (ping, show, etc.)
    partes/       ← tu parte del .pkt antes de integrarla al MASTER
    TAREAS.md     ← asignadas / en progreso / terminadas
expediente/       ← documento final y entregables
maqueta/
  MASTER/         ← versión integrada del .pkt
  respaldos/      ← copias de versiones anteriores
```

Dónde sube cada quién sus archivos:

- **Cada integrante solo trabaja dentro de su carpeta en `equipo/`** (R1 Brisa, R2 Gonzalo, R3 Maki, R4 Estrella).
- **`maqueta/MASTER/`** guarda la versión integrada del `.pkt` (`Proyecto_Red_vXX.pkt`); solo se toca al integrar.
- **`maqueta/respaldos/`** guarda copias de versiones anteriores.
- **`expediente/`** guarda el documento final y los entregables.
