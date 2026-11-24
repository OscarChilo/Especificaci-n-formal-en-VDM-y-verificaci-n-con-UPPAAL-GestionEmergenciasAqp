# Sistema de Alerta y Gestión de Emergencias — Fenómeno El Niño (Arequipa)

## Especificación formal en VDM++ y verificación con UPPAAL

**Curso:** Aspectos Formales de Especificación y Verificación  
**Universidad:** Universidad Nacional de San Agustín (UNSA)  
**Escuela:** Ingeniería de Sistemas  

### Integrantes
- Chilo Huillca, Oscar Raul — ochilo@unsa.edu.pe
- Suasaca Pacompia, Alvaro Gustavo — asuasaca@unsa.edu.pe
- Huarca Pallani, Jael Emerson — jhuarcap@unsa.edu.pe

---

## Descripción del Proyecto

Sistema crítico de alerta y gestión de emergencias ante el Fenómeno El Niño en Arequipa. El modelo integra cinco clases principales especificadas formalmente en **VDM++** y verificadas mediante **UPPAAL**.

### Componentes del sistema
| Clase | Descripción |
|---|---|
| `SistemaEmergencias` | Coordinador central del modelo |
| `ZonaAfectada` | Gestión de niveles de alerta (VERDE, AMARILLO, NARANJA, ROJO) |
| `UnidadRescate` | Control de estados (DISPONIBLE, ASIGNADA, OPERANDO) |
| `EstacionMonitoreo` | Registro de mediciones de precipitación y caudal |
| `AlbergueSeguro` | Gestión de capacidad y ocupación |

---

## Estructura del Repositorio

```
├── SistemaEmergencias/
│   ├── AlbergueSeguro.vpp          # Clase AlbergueSeguro
│   ├── EstacionMonitoreo.vpp       # Clase EstacionMonitoreo
│   ├── ZonaAfectada.vpp            # Clase ZonaAfectada
│   ├── UnidadRescate.vpp           # Clase UnidadRescate
│   ├── SistemaEmergencias.vpp      # Clase coordinadora
│   ├── PruebasAlbergue.vpp         # Casos de prueba CP-01 a CP-03
│   ├── PruebasUnidad.vpp           # Casos de prueba CP-04 a CP-07
│   ├── PruebasZona.vpp             # Caso de prueba CP-08
│   ├── PruebasEstacion.vpp         # Casos de prueba PE-01 a PE-04
│   ├── PruebasSistema.vpp          # Casos de prueba PS-01 a PS-04
│   ├── UnidadRescate_UPPAAL.xml    # Modelo UPPAAL del autómata
│   ├── SistemaEmergencias.prj      # Proyecto VDM++ Toolbox
│   └── SistemaEmergencias.opt      # Configuración del proyecto
├── Capturas/
│   ├── diagrama.JPG                # Autómata en UPPAAL (Editor)
│   └── verifier.JPG                # Verificación en UPPAAL (Verifier)
└── README.md
```

---

## Inicio Rápido

### Parte 1: Especificación formal en VDM++

1. Descargar e instalar [VDM++ Toolbox](https://github.com/vdmtools/vdmtools)
2. Abrir el proyecto `SistemaEmergencias/SistemaEmergencias.prj`
3. Ejecutar los casos de prueba desde las clases `Pruebas*.vpp`
4. Se espera que los 16 casos de prueba produzcan los resultados documentados

### Parte 2: Verificación con UPPAAL (Model Checking)

1. Descargar e instalar [UPPAAL 5.0.0](https://uppaal.org/downloads/)
2. Requiere **Java 11 a 21** instalado
3. Abrir `SistemaEmergencias/UnidadRescate_UPPAAL.xml` en UPPAAL
4. En la pestaña **Editor**: visualizar el autómata de estados
5. En la pestaña **Verifier**: ejecutar las 5 propiedades CTL

### Propiedades verificadas en UPPAAL

| # | Propiedad CTL | Descripción | Resultado |
|---|---|---|---|
| P1 | `A[] (unidad.DISPONIBLE imply unidad.tieneZona == false)` | Disponibilidad sin asignación | ✅ Satisfecha |
| P2 | `A[] (unidad.OPERANDO imply unidad.tieneZona == true)` | Operación con asignación | ✅ Satisfecha |
| P3 | `E<> unidad.ASIGNADA` | Alcanzabilidad de ASIGNADA | ✅ Satisfecha |
| P4 | `E<> unidad.OPERANDO` | Alcanzabilidad de OPERANDO | ✅ Satisfecha |
| P5 | `A[] not deadlock` | Ausencia de bloqueos | ✅ Satisfecha |

---

## Herramientas Utilizadas

- **VDM++ Toolbox** — Especificación y validación formal
- **UPPAAL 5.0.0** — Model checking con autómatas temporizados
- **Java 21** — Requerido por UPPAAL

---

## Referencias

- Fitzgerald et al. (2005). *Validated Designs for Object-oriented Systems*. Springer.
- CENEPRED (2024). Informe de vulnerabilidad ante El Niño — Arequipa.
- Gobierno Regional de Arequipa (2023). Plan de Contingencia ante Lluvias Intensas.
