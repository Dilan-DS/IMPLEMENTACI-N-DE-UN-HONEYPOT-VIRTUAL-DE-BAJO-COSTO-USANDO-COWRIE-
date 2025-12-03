# Implementacion de un Honeypot Virtual de Bajo Costo usando Cowrie

Proyecto academico que propone la implementacion de un honeypot virtual de bajo costo para registrar, analizar y comprender ataques dirigidos a una red local. El sistema se basa en **Cowrie**, un honeypot de interaccion media para SSH/Telnet desplegado dentro de una maquina virtual.

---

## Integrantes

- Paula Rojas  
- Stephano Dilan Galvez Perez  
- Deyvi Masache  
- Jhosty Soto  

---

## Objetivo General

Implementar un honeypot virtual basado en Cowrie dentro de una maquina virtual para capturar, registrar y analizar patrones de ciberataques dirigidos a una red local, con el fin de validar la importancia de la defensa perimetral activa.

---

## Objetivos Especificos

1. Instalar una plataforma de honeypot basada en Cowrie dentro de una maquina virtual utilizando VirtualBox como entorno de laboratorio de bajo costo.  
2. Configurar Cowrie para simular un entorno SSH/Telnet atractivo para atacantes y exponerlo en modo puente dentro de la red local.  
3. Monitorear intentos de acceso no autorizado, ataques de fuerza bruta y escaneos de puertos detectados durante el periodo de observacion.  
4. Registrar la actividad capturada (metadatos de conexion, credenciales intentadas y comandos ejecutados).  
5. Analizar los registros obtenidos para identificar patrones de ataque predominantes (diccionarios utilizados, IPs de origen, comportamiento recurrente).  
6. Demostrar la viabilidad de una solucion economica y replicable para pequenas instituciones o PyMEs.

---

## Arquitectura del Sistema

- **Host Machine**: equipo fisico con VirtualBox.  
- **VM Honeypot**: Ubuntu Server con Cowrie instalado.  
- **Modo de red**: Bridge (modo puente), para que la VM reciba una IP real de la red local.  
- **Servicios simulados**: SSH y Telnet falsos, controlados por Cowrie.  

La VM aparece ante Internet como un servidor legitimo, permitiendo que bots y atacantes automaticos realicen ataques de diccionario y escaneos.

Un diagrama de red de referencia se incluiria en `Documentacion/diagrama_red.png`.

---

## Requisitos Tecnicos

- VirtualBox u otro hipervisor  
- Maquina virtual con:
  - 1 CPU
  - 2 GB de RAM
  - 20 GB de disco
- Sistema operativo invitado: **Ubuntu Server** o **Kali Linux**
- Python 3 y dependencias de Cowrie

---

## Pasos Basicos de Instalacion (Ubuntu/Kali)

```bash
# Actualizar el sistema
sudo apt update && sudo apt upgrade -y

# Instalar dependencias
sudo apt install git python3 python3-venv python3-dev libffi-dev libssl-dev build-essential -y

# Crear usuario para el honeypot
sudo adduser cowrie
sudo su - cowrie

# Clonar Cowrie
git clone https://github.com/cowrie/cowrie.git
cd cowrie

# Crear entorno virtual
python3 -m venv cowrie-env
source cowrie-env/bin/activate
pip install --upgrade pip
pip install -r requirements.txt

# Copiar configuracion base
cp etc/cowrie.cfg.dist etc/cowrie.cfg
# Proyecto Honeypot Cowrie
