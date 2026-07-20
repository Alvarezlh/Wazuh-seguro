# Wazuh-seguro

Laboratorio práctico de SIEM/XDR con **Wazuh** sobre un entorno virtualizado (Kali Linux como agente atacante/monitorizado + appliance oficial de Wazuh como manager), orientado a construir experiencia real en detección, análisis de logs y respuesta a incidentes de cara a un rol de **SOC Analyst / Blue Team** junior.

## 👤 Sobre este proyecto

Este repositorio forma parte de mi transición profesional hacia ciberseguridad, respaldada por:

- 🎓 **Certificado de Profesionalidad en Seguridad de los Sistemas de Información (Nivel 3)** — Forma-t Escuela de Empleo, subvencionado por el SOC y el Fondo Social Europeo (420 horas, jul. 2025 – may. 2026, Barcelona). Incluye los módulos de Gestión de Servicios (MF0490) y Gestión de Incidentes (MF0488).
- 🎓 **Google Cybersecurity Professional Certificate** (Google / Coursera, 2025–2026) — especialización en Linux y SQL aplicados a la recuperación, gestión y protección de datos.
- 🎓 Formación complementaria: Lógica de Programación y Ciberseguridad Web (Barcelona Activa) y Esquema Nacional de Seguridad — ENS, RD 311/2022.
- 🧪 Este laboratorio con Wazuh, como aplicación práctica de esos conocimientos sobre un SIEM real, complementando la base teórica con hands-on en detección, análisis de logs y respuesta a incidentes.

> 🔗 https://coursera.org/share/dd770e1c2a2a35e468168ee3af5ed2f7

📄 CV completo y contacto: [linkedin.com/in/luis-enrique-alvarez-h](https://linkedin.com/in/luis-enrique-alvarez-h/)

## 🎯 Objetivo del proyecto

Documentar, de forma reproducible, el proceso completo de:

- Desplegar un entorno Wazuh + Kali Linux desde cero.
- Ingerir y analizar logs históricos y en tiempo real.
- Diagnosticar y corregir problemas reales de configuración (campos mal poblados, límites de consulta, permisos).
- Ejecutar ataques controlados y observar/mejorar su detección.
- Producir artefactos propios de un analista SOC: reglas de detección, dashboards, e informes de incidente.

## 🧰 Stack utilizado

| Componente | Detalle |
|---|---|
| SIEM | Wazuh 4.14.6 (manager + indexer + dashboard, OVA oficial) |
| Sistema atacante/agente | Kali Linux |
| Motor de búsqueda | OpenSearch (vía Dashboards / Discover) |
| Virtualización | VirtualBox (red en modo puente) |
| Otros | `logger`/journald, `_update_by_query` (API OpenSearch), Git/GitHub |

## 📁 Estructura del repositorio

```
Wazuh-seguro/
├── 01-guia-configuracion/
│   └── Guia_Configuracion_Wazuh.docx        # Instalación y configuración paso a paso del entorno
├── 02-laboratorios-portfolio/
│   └── Laboratorios_Wazuh_Portfolio.docx    # Propuesta de 7 laboratorios de práctica (ver abajo)
├── 03-reglas-personalizadas/
│   └── local_rules.xml                      # Reglas propias de detección (Laboratorio 1)
├── 04-informes-incidentes/
│   └── (informes de respuesta a incidentes, Laboratorio 6)
└── README.md
```

## 📘 01 — Guía de configuración

Documento con la instalación completa del entorno: memoria de las VMs, red en modo puente, instalación del agente Wazuh en Kali, inyección de logs históricos, activación de `archives` en Filebeat, y una sección adicional de **troubleshooting real** que incluye:

- Corrección masiva de un campo mal poblado (`location: journald` → ruta real del archivo) usando la API `_update_by_query` de OpenSearch.
- Diagnóstico y solución del error `too_many_nested_clauses` en consultas DQL de Discover.

## 🧪 02 — Laboratorios de práctica

Siete laboratorios diseñados para ampliar este proyecto y demostrar competencias de SOC:

1. **Detección de ataques reales y reglas personalizadas** — Hydra, Nmap, `local_rules.xml` propio.
2. **Dashboards personalizados de seguridad** — Top IPs, distribución de eventos por host, eventos por severidad.
3. **Integración con Threat Intelligence (IOCs)** — CDB lists con IPs maliciosas.
4. **Detección de vulnerabilidades** — módulo nativo de Vulnerability Detection de Wazuh.
5. **File Integrity Monitoring (FIM)** — vigilancia de archivos críticos y caso simulado.
6. **Informe de respuesta a incidentes end-to-end** — de la detección al informe final.
7. **Active Response** — bloqueo automático de IPs tras fuerza bruta SSH.

Cada laboratorio se irá documentando en su propia carpeta o subcarpeta a medida que se complete, con capturas de pantalla, comandos utilizados y hallazgos.

## 🔍 Aprendizajes clave documentados

- Cómo Wazuh clasifica un evento según su origen (`journald` vs. lectura directa de archivo vía `<localfile>`), y el impacto de esa diferencia en los metadatos disponibles para análisis forense.
- Cómo corregir datos ya indexados en OpenSearch sin reingerir todo el histórico.
- Buenas prácticas de sintaxis DQL para evitar errores de rendimiento en búsquedas combinadas.
- Diferencia entre analizar una muestra (`Top 5 values`) y una agregación completa (`Visualize`) sobre el total de resultados.

## 🚀 Próximos pasos

- [ ] Completar Laboratorio 1 (ataques reales + reglas propias)
- [ ] Completar Laboratorio 6 (informe de incidente)
- [ ] Añadir capturas de pantalla de cada laboratorio completado
- [ ] Publicar un resumen del proyecto en LinkedIn

---

*Proyecto personal de aprendizaje en ciberseguridad — Blue Team / SOC.*
