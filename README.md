# 🛡️ Jec0d3r SIEM & SOC L2 Analyzer

![Status](https://img.shields.io/badge/Status-Active-16a34a?style=flat-square)
![Role](https://img.shields.io/badge/SOC-Nivel%202%20%7C%20DFIR-ea580c?style=flat-square)
![Framework](https://img.shields.io/badge/MITRE-ATT%26CK-1f2937?style=flat-square)
![Stack](https://img.shields.io/badge/Stack-HTML5%20%7C%20TailwindCSS%20%7C%20JS-374151?style=flat-square)
![Powered By](https://img.shields.io/badge/Powered%20by-Jec0d3r-ea580c?style=flat-square)

Plataforma web interactiva (*Single-Page Application*) de análisis de logs SIEM, correlación de incidentes, extracción de Indicadores de Compromiso (IoCs) y generación de informes técnicos en PDF, diseñada para **Analistas SOC Nivel 2** bajo una estética formal y corporativa.

> **Origen del Proyecto:** Desarrollado inicialmente como laboratorio práctico final del **Bootcamp Analista SOC Nivel 2** (*De los fundamentos a la operación y respuesta*) impartido por **Comunidad DOJO** y **WoSEC Panamá**, y posteriormente evolucionado a una herramienta multi-caso reutilizable para laboratorios de ciberdefensa y *Threat Hunting*.

---

## 🚀 Funcionalidades Principales

La herramienta cubre el flujo completo de investigación de incidentes desde la ingesta hasta el veredicto ejecutivo:

* **00. Toma de Datos de la Misión (Multi-Caso):** Configuración dinámica de Cliente/Organización, Analista asignado, ID de Ticket/Caso y contexto del incidente. Incluye función **Limpiar Aplicación** para reiniciar el entorno y analizar nuevos casos de estudio.
* **01. Carga de Archivos (`.xlsx` / `.csv`):** Importación directa en el navegador (sin necesidad de backend) de exportaciones de SIEM mediante *SheetJS*, con tabla interactiva y filtros avanzados.
* **02. Análisis de Seguridad y Correlación:** Motor heurístico que clasifica eventos sospechosos, agrupa ráfagas de ataque por IP/usuario para identificar múltiples incidentes independientes, extrae IoCs y construye la línea de tiempo forense.
* **03. Dashboard Ejecutivo:** Métricas KPI y gráficos interactivos (*Chart.js*) por nivel de criticidad, tácticas detectadas y activos comprometidos.
* **04. Clasificación de Riesgos:** Matriz interactiva para evaluar cada hallazgo (**Crítico, Alto, Medio o Bajo**) con justificación técnica editable en tiempo real.
* **05 & 06. Informe Técnico y Exportación a PDF:** Generación automática de un documento corporativo listo para imprimir o descargar en **PDF**.

---

## 🎯 Motor de Detección y Mapeo MITRE ATT&CK

El analizador evalúa los registros del SIEM (Windows Event Logs, Syslog, VPN, Firewall, etc.) en **6 categorías clave**:

| Categoría de Detección | MITRE ATT&CK | Patrones / Artefactos Evaluados |
| :--- | :---: | :--- |
| **Fuerza bruta** | `T1110` | Múltiples fallos de autenticación (`Event ID 4625`, SSH/RDP/VPN failed logins). |
| **Inicios sospechosos** | `T1078` | Accesos exitosos (`Event ID 4624`) tras fuerza bruta previa, horarios anómalos, nodos TOR o *impossible travel*. |
| **Escalamiento** | `T1548` / `T1098` | Asignación de privilegios especiales (`4672`), agregación a *Domain Admins* (`4728`), abuso de `sudo` o creación de cuentas privilegiadas. |
| **Comandos y procesos** | `T1059` / `T1003` | PowerShell codificado (`-enc`, `-nop -w hidden`), volcado de `lsass.exe`, `mimikatz`, `procdump` (`4688`, `7045`). |
| **Movimiento lateral** | `T1021` | Saltos internos mediante SMB (`ADMIN$`, `5140`), `PsExec`, WinRM, WMI o RDP lateral. |
| **Otras anomalías** | `T1041` / `T1053` | Exfiltración de datos (`rclone`, transferencias salientes anómalas), persistencia (`schtasks`), criptominería (`xmrig`) y tráfico C2. |

---

## 📄 Estructura del Informe Técnico (PDF)

El módulo de reportes compila automáticamente la evidencia y la estructura en 8 secciones estándar de respuesta a incidentes:

1. **Resumen ejecutivo** (sincronizado con los datos de la misión).
2. **Hallazgos identificados** por táctica.
3. **Explicación técnica** de cada hallazgo.
4. **Evidencias encontradas en los logs** (tabla forense e IoCs).
5. **Criticidad y justificación** de riesgos.
6. **Posible impacto en la organización**.
7. **Plan de acción:** Investigar, contener y remediar.
8. **Recomendaciones generales de seguridad**.

---

## 🛠️ Stack Tecnológico

* **Frontend:** HTML5 + JavaScript (ES6+) puro — 100% *client-side* (los logs nunca salen de tu equipo).
* **Estilos:** [Tailwind CSS](https://tailwindcss.com/) (paleta corporativa en grises, naranja para alertas/acciones críticas y verde para validaciones/PDF).
* **Procesamiento Excel/CSV:** [SheetJS (xlsx)](https://sheetjs.com/).
* **Visualización de Datos:** [Chart.js](https://www.chartjs.org/).
* **Iconografía:** [Lucide Icons](https://lucide.dev/).

---

## ⚡ Instalación y Uso Rápido

Al ser una aplicación autocontenida (*client-side*), no requiere servidores, bases de datos ni instalación de dependencias locales:

1. Clona el repositorio:
   ```bash
   git clone https://github.com/JEc0d3r/Analizador-SIEM-e-Informes-SOC.git

### Autor y Créditos
Autor: (Jec0d3r)

Desarrollo Asistido por IA: Estructurado y refinado con el apoyo del modelo Gemini como asistente de ingeniería de software.

Agradecimientos: Comunidad DOJO y WoSEC Panamá por la formación técnica impartida en el Bootcamp Analista SOC Nivel 2.