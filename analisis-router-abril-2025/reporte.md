# 🛡️ Reporte Técnico de Seguridad en Red Doméstica

## 🟢 1. Datos Generales del Análisis

- **Nombre del Analista:** Antonio Fernandez
- **Fecha del Análisis:** 25 de abril de 2025
- **Tipo de Análisis:** Reconocimiento y evaluación de la seguridad de red doméstica
- **Objetivo:** Identificar posibles vulnerabilidades en el router y dispositivos de la red local, como ejercicio formativo.

---

## 🟠 2. Herramientas y Metodología

**Herramientas utilizadas:**
- Kali Linux (máquina virtual)
- nmap (escaneo de hosts y puertos)
- Comandos Linux: `ip a`, `ip route`

**Metodología:**
1. Configuración de red en modo "Bridged Adapter" para interactuar con la red local real.
2. Descubrimiento de dispositivos activos con `nmap -sn 192.168.***.*/24` (ping scan).
3. Escaneo de puertos TCP del router (192.168.***.*) con `nmap -sS -p 1-1000 192.168.***.*`.
4. Análisis de los servicios detectados y evaluación de riesgos.

> ⚠️ **Nota importante:** Este análisis se realizó únicamente sobre direcciones IP privadas (red local). No se expuso ni utilizó ninguna dirección IP pública durante este ejercicio.

---

## 🟥 3. Hallazgos

| Dispositivo                | IP                        | MAC Address             | Fabricante           | Servicios detectados                            |
|----------------------------|--------------------------|-------------------------|----------------------|-------------------------------------------------|
| Router principal           | [IP privada de red local] | [censurado por seguridad] | Huawei Technologies   | 23/tcp (Telnet), 53/tcp (DNS), 80/tcp (HTTP), 22/tcp (SSH filtered) |

### **Detalles:**
- **Puerto 23 (Telnet) abierto:** Protocolo inseguro, permite acceso remoto sin cifrado.
- **Puerto 80 (HTTP sin HTTPS):** Consola de administración accesible por HTTP, sin protección de cifrado.
- **SSH filtrado:** Puerto detectado, pero con firewall bloqueando el acceso externo.
- **DNS activo:** Común en routers que ofrecen resolución de nombres a los dispositivos de la red.

---

## 🛠️ 4. Riesgos Identificados

| Servicio | Nivel de Riesgo     | Descripción del riesgo                                   |
|----------|---------------------|----------------------------------------------------------|
| Telnet   | Alto                | Transmite credenciales en texto plano, fácil de interceptar o explotar si las contraseñas son débiles o de fábrica. |
| HTTP     | Medio               | Sin cifrado (HTTPS), expone credenciales y configuración a sniffing si alguien está en la red Wi-Fi. |
| SSH      | Bajo (monitorizado) | Filtrado, pero recomendable revisar configuración interna para confirmar que solo acepte conexiones necesarias. |

---

## 🟡 5. Recomendaciones

- Desactivar **Telnet** y habilitar solo **SSH** (con autenticación por llave o passwords fuertes).
- Activar **HTTPS** en la administración web del router (si es posible).
- Cambiar todas las contraseñas de fábrica del router.
- Limitar el acceso a la consola de administración únicamente desde dispositivos autorizados o vía cable.
- Verificar si el router permite actualizar el firmware y hacerlo si hay una versión más segura.

---

## 🟦 6. Conclusión

> El análisis permitió identificar configuraciones inseguras en el router principal. Estas configuraciones son comunes en entornos domésticos, pero representan una superficie de ataque considerable. Se recomienda aplicar las medidas correctivas sugeridas para fortalecer la seguridad de la red local y evitar accesos no autorizados.

---

## ⚠️ Nota
Este ejercicio fue realizado en un entorno doméstico con fines de aprendizaje y formación profesional en ciberseguridad. No se han realizado pruebas de explotación ni ataque activo sobre los servicios detectados, únicamente reconocimiento pasivo y escaneo de puertos.

> 🚩 **Aclaración:** Todas las IPs utilizadas en este análisis corresponden a direcciones privadas (ej. 192.168.x.x) que no son accesibles desde internet público.

