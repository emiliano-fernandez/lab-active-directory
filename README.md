# Lab Active Directory — estudiolegal.local

Laboratorio doméstico de Active Directory sobre VirtualBox que simula la infraestructura informática de un estudio jurídico chico. Lo uso para practicar administración de Windows Server, diseño de OUs y GPOs, y operaciones cotidianas de soporte IT.

> **Estado actual (junio 2026):** infraestructura base operativa. Domain Controller promovido, dominio funcional, servicios AD DS y DNS instalados. Próxima fase: construcción de OUs personalizadas y GPOs. Ver roadmap más abajo.

## Arquitectura actual

| Rol | Nombre de máquina | SO | Estado |
|-----|-------------------|-----|--------|
| Domain Controller | SRV-LEGAL-01 | Windows Server 2022 | Operativo, roles AD DS + DNS instalados |
| Cliente 1 | PC-ABOGADO-01 | Windows 11 | Configurado, pendiente unión al dominio |

**Dominio:** `estudiolegal.local` 
**Plataforma de virtualización:** Oracle VirtualBox

## Lo que está hecho hasta ahora

- [x] Promoción del servidor a Domain Controller (AD DS)
- [x] Configuración de DNS interno del dominio
- [x] Configuración de DHCP para asignación dinámica
- [x] Servidor local operativo y monitoreado desde Server Manager
- [x] Cliente Windows 11 instalado y configurado en la red

## Roadmap — próximas etapas

### Fase 2: Estructura organizacional (próxima)

- [ ] Crear OUs personalizadas: `_Usuarios`, `_Grupos`, `_Equipos`, `_Servicios`
- [ ] Sub-OUs por rol: Socios, Abogados, Secretaria, Externos
- [ ] Crear grupos de seguridad: G_Socios, G_Abogados, G_Administrativos, G_TI
- [ ] Crear usuarios de prueba con asignación por rol
- [ ] Unir cliente PC-ABOGADO-01 al dominio

### Fase 3: Políticas de grupo (GPOs)

- [ ] Password-Policy: complejidad de contraseñas y expiración
- [ ] Block-USB-Storage: bloqueo de almacenamiento USB en estaciones
- [ ] Map-Drives: mapeo automático de unidades de red por grupo
- [ ] Logon-Banner: aviso legal corporativo al iniciar sesión
- [ ] Restrict-Control-Panel: restricciones para usuarios externos

### Fase 4: Documentación y auditoría

- [ ] Scripts PowerShell para alta y baja masiva de usuarios
- [ ] Implementación de Sysmon para registro detallado
- [ ] Procedimientos documentados para tareas comunes de soporte

## Stack técnico

- **Virtualización:** Oracle VirtualBox 7.x
- **SO servidor:** Windows Server 2022 Standard (evaluación 180 días)
- **SO cliente:** Windows 11 Pro
- **Análisis de red:** Wireshark
- **Scripts:** PowerShell, Bash

## Capturas del estado actual

Ver carpeta `/screenshots`:

- `01-server-manager.png` — Server Manager con los roles AD DS, DNS y Servicios de archivos instalados
- `02-usuarios-equipos-ad.png` — Consola Usuarios y equipos de Active Directory con el dominio estudiolegal.local
- `03-ad-users-container.png` — Contenedor Users por defecto con cuentas y grupos del sistema
- `04-gpmc-default-policies.png` — Administración de directivas de grupo mostrando las GPOs por defecto del dominio

## Conceptos clave que estoy trabajando

- **Diferencia entre contenedores por defecto y OUs personalizadas:** los contenedores (Users, Computers, Builtin) vienen con el dominio y no permiten enlazar GPOs. Las OUs personalizadas sí, por eso son la base de cualquier diseño serio.
- **Estructura plana vs jerárquica:** una OU plana es más simple pero limita la granularidad de las políticas. Una jerárquica permite herencia de GPOs y delegación de administración por sub-equipo.
- **Default Domain Policy vs GPOs personalizadas:** la política por defecto aplica a todo el dominio. Para reglas específicas por grupo o equipo se crean GPOs nuevas y se enlazan a OUs.

## Parte de un homelab más amplio

Este repo documenta solo el lab de Active Directory. Forma parte de un homelab de ciberseguridad que también incluye, en distintas etapas de configuración:

- **SOC con Wazuh** (SIEM/XDR open source) — repo en preparación
- **pfSense** como firewall perimetral y segmentación de red — repo en preparación
- **Tsurugi Linux** para forensia digital — repo en preparación

Cada componente tendrá su propio repo a medida que avance la documentación.

---

> **Sobre este lab:** lo armé y lo mantengo como parte de mi formación práctica mientras curso la Tecnicatura en Seguridad Informática y proyecto mi primer rol formal en IT. Lo documento públicamente porque creo que mostrar *el cómo* es más valioso que enumerar tecnologías sin contexto.
