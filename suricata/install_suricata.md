# Integración de Suricata como NIDS en agente Ubuntu

Este documento describe **cómo instalar y configurar Suricata en un agente Ubuntu**, siguiendo **la documentación oficial de Wazuh** para la integración como **Network IDS (NIDS)**.

---

## 1. Infraestructura

* **Sistema**: Ubuntu 22.04 (endpoint)
* **Rol**: Agente Wazuh
* **Interfaz monitorizada**: `enp0s3`
* **Logs de Suricata**: `/var/log/suricata/eve.json`

---

## 2. Instalar Suricata

Añadir el repositorio oficial de Suricata:

```bash
sudo add-apt-repository ppa:oisf/suricata-stable
sudo apt-get update
```

Instalar Suricata:

```bash
sudo apt-get install suricata -y
```

---

## 3. Descargar reglas Emerging Threats

Descargar y extraer el ruleset:

```bash
cd /tmp/ && curl -LO https://rules.emergingthreats.net/open/suricata-6.0.8/emerging.rules.tar.gz
sudo tar -xvzf emerging.rules.tar.gz
sudo mkdir /etc/suricata/rules
sudo mv rules/*.rules /etc/suricata/rules/
sudo chmod 777 /etc/suricata/rules/*.rules
```

---

## 4. Configurar Suricata

Editar el archivo de configuración:

```bash
sudo nano /etc/suricata/suricata.yaml
```

Configurar las siguientes variables:

```yaml
HOME_NET: "192.168.1.10"
EXTERNAL_NET: "any"

default-rule-path: /etc/suricata/rules
rule-files:
  - "*.rules"

stats:
  enabled: yes

af-packet:
  - interface: enp0s3
```

Guardar los cambios.

---

## 5. Reiniciar Suricata

Reiniciar el servicio:

```bash
sudo systemctl restart suricata
```

---

## 6. Configurar el agente Wazuh

Editar el archivo de configuración del agente:

```bash
sudo nano /var/ossec/etc/ossec.conf
```

Añadir el siguiente bloque:

```xml
<ossec_config>
  <localfile>
    <log_format>json</log_format>
    <location>/var/log/suricata/eve.json</location>
  </localfile>
</ossec_config>
```

---

## 7. Reiniciar el agente Wazuh

Reiniciar el servicio:

```bash
sudo systemctl restart wazuh-agent
```

---

✔️ **Suricata integrado correctamente como NIDS en el agente Ubuntu y monitorizado por Wazuh.**
