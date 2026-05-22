
# Informe de configuración de DMZ con Cisco Packet Tracer


### 1. Objetivo del laboratorio

> Explica brevemente qué se buscaba lograr con este laboratorio.

Configurar una DMZ segura usando un router Cisco ISR, aplicando NAT y ACLs para controlar el tráfico entre LAN, DMZ y red externa.

---

### 2. Topología implementada

> <img width="935" height="510" alt="red" src="https://github.com/user-attachments/assets/aa41400f-7402-4de8-bd97-3d0dc9e3c592" />


- Cantidad de redes: 3
- Dispositivos usados: se utilizo 3 switches Cisco 2960 (o 2960 IOS15), 3 dispositivos finales y un Router cisco ISR 2911
- El router cisco actua como el corazón de seguridad, los switches para separar cada segmento de red. El PC_Internal representa un usuario en la red interna. Servidor web que se encuentra en la DMZ y un PC externo que simula un cliente en internet que intenta acceder a los servicios.



### 3. Plan de direccionamiento IP

Completa la tabla con las IPs asignadas 

| Dispositivo             | IP               | Máscara           | Gateway          |
|-------------------------|------------------|-------------------|-------------------|
| PC_Internal             | 192.168.1.10     |     24            | 192.168.1.1       |
| Server_DMZ              | 192.168.2.10     |     24            | 192.168.2.1       |
| PC_External             | 192.168.3.10     |     24            | 192.168.3.1       |
| Router_FW Gi0/0 (LAN)   | 192.168.1.1      |     24            |                   |
| Router_FW Gi0/1 (DMZ)   | 192.168.2.1      |     24            |                   |
| Router_FW Gi0/2 (Ext)   | 192.168.3.1      |     24            |                   |


### 4. Configuración aplicada (resumen)

> Resume los comandos o pasos más relevantes que ejecutaste. Usa texto + fragmentos de código cuando sea necesario.

- Interfaces configuradas con `ip address`
- <img width="615" height="254" alt="config int" src="https://github.com/user-attachments/assets/a4003852-5719-4ea3-b900-4f766af84c8b" />
```bash
ip nat inside source static 192.168.2.10 192.168.3.1

```
- ACLs: configuración de las ACL que permite conexiones TCP desde cualquier origen hacia la IP del servidor DMZ únicamente al puerto 80. La cual aplica la ACL en la interfaz WAN (GigabitEthernet0/2) en sentido de entrada (inbound).
- <img width="572" height="261" alt="nat" src="https://github.com/user-attachments/assets/8b0d654b-8ec0-4506-8392-dfb187bacd98" />

- ACLs:Con esta ACL se bloquea cualquier protocolo IP (TCP, UDP, ICMP, etc.) desde la DMZ hacia la LAN. Permitiendo el resto del tráfico que no coincida con la regla anterior (por ejemplo, DMZ → Internet). 
- <img width="572" height="109" alt="acl 2" src="https://github.com/user-attachments/assets/fa46c8c8-7fa4-4158-950d-10d714fb06f2" />

```bash

```

### 5. Verificaciones realizadas

> Describe las pruebas y su resultado. Incluye capturas o salidas de comandos si se puede.

- `ping` desde PC_Internal al router: ✅
- Acceso web desde PC_External: ✅
- Bloqueo de acceso desde DMZ a LAN: ✅


### 6. Conclusiones y recomendaciones

> ¿Qué aprendiste con este ejercicio? ¿Qué mejorarías?


Aprendí a aplicar NAT y ACLs en un entorno simulado. Recomiendo verificar conectividad básica antes de aplicar reglas de firewall, ya que un error en la IP puede bloquear todo.


