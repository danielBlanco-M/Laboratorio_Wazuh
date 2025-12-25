# Introducción

Este documento describe el **laboratorio de Wazuh integrado con Suricata como IDS**, diseñado con fines educativos y prácticos para **fortalecer mis habilidades como analista SOC (Security Operations Center)**. A través de este laboratorio se simularán distintos escenarios de ataque para comprender cómo funcionan la detección, correlación y respuesta ante incidentes de seguridad en un entorno controlado.

## Objetivo del laboratorio

El objetivo principal de este laboratorio es:

* Comprender la arquitectura y funcionamiento de **Wazuh** como plataforma SIEM/XDR.
* Integrar **Suricata** como sistema de detección de intrusiones (IDS).
* Analizar alertas de seguridad generadas por ataques simulados.
* Mejorar habilidades prácticas en **monitorización, detección y análisis de incidentes**, propias de un entorno SOC.

Este laboratorio está enfocado en el aprendizaje práctico, replicando situaciones reales que un analista de seguridad podría encontrar en un entorno empresarial.

## ¿Qué es Wazuh?

**Wazuh** es una plataforma de seguridad de código abierto que combina funcionalidades de **SIEM (Security Information and Event Management)** y **XDR (Extended Detection and Response)**. Permite:

* Recolección y análisis de logs.
* Detección de amenazas y comportamientos anómalos.
* Monitorización de integridad de archivos (FIM).
* Detección de vulnerabilidades.
* Cumplimiento normativo (PCI DSS, GDPR, ISO 27001, entre otros).

Wazuh se compone principalmente de:

* **Wazuh Server**: procesa, analiza y correlaciona los eventos.
* **Wazuh Agents**: instalados en los endpoints para recolectar información.
* **Wazuh Dashboard**: interfaz gráfica para visualización y análisis.

## ¿Para qué sirven los agentes de Wazuh?

Los **agentes de Wazuh** se instalan en los sistemas que se desean monitorizar y cumplen funciones clave como:

* Envío de logs del sistema y aplicaciones.
* Detección de cambios en archivos críticos.
* Monitorización de procesos y actividad del sistema.
* Reporte de vulnerabilidades y eventos de seguridad.

En este laboratorio, el agente permitirá observar cómo un endpoint Linux es monitorizado en tiempo real y cómo se detectan actividades maliciosas.

## ¿Qué es Suricata?

**Suricata** es un **sistema de detección y prevención de intrusiones (IDS/IPS)** de código abierto. Analiza el tráfico de red y detecta:

* Escaneos de puertos.
* Ataques conocidos basados en firmas.
* Comportamientos anómalos en la red.

En este laboratorio, Suricata funcionará como **IDS**, generando alertas que serán enviadas y correlacionadas por Wazuh para su análisis centralizado.

## Topología del laboratorio

La topología del laboratorio es sencilla pero representativa de un entorno real:

* **192.168.1.10** → Servidor **Wazuh** (Manager + Dashboard + Integración con Suricata)
* **192.168.1.13** → **Agente Wazuh** sobre Ubuntu
* **Kali Linux** → Máquina atacante utilizada para simular ataques

```
[Kali Linux]  --->  [Agente Ubuntu - 192.168.1.13]  --->  [Wazuh Server - 192.168.1.10]
```

## Simulación de ataques

Desde la máquina **Kali Linux** se llevarán a cabo diferentes ataques controlados, como:

* Escaneos de puertos (Nmap).
* Ataques de fuerza bruta.
* Tráfico malicioso simulado.

El objetivo es observar:

* Cómo Suricata detecta el tráfico malicioso.
* Cómo Wazuh correlaciona los eventos.
* Cómo se generan alertas y se visualizan en el dashboard.

## Alcance educativo

Este laboratorio no tiene fines maliciosos. Todo el contenido está orientado a:

* Aprendizaje en ciberseguridad defensiva.
* Práctica de análisis SOC.
* Comprensión de herramientas ampliamente usadas en entornos profesionales.

---

Este documento servirá como base para el resto del laboratorio, donde se detallarán la instalación, configuración y pruebas prácticas de Wazuh y Suricata.
