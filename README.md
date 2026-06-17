# Lab Active Directory — estudiolegal.local

Laboratorio doméstico de Active Directory sobre VirtualBox que simula la infraestructura informática de un estudio jurídico. Lo uso para practicar administración de Windows Server, diseño de GPOs y operaciones cotidianas de soporte IT.

## Arquitectura

| Rol | Nombre | SO | RAM | Notas |
|-----|--------|-----|-----|-------|
| Domain Controller | SRV-LEGAL-01 | Windows Server 2022 | 4 GB | DNS + DHCP + AD DS |
| Cliente 1 | WS-LEGAL-01 | Windows 10 Pro | 2 GB | Perfil abogado |
| Cliente 2 | WS-LEGAL-02 | Windows 11 Pro | 2 GB | Perfil secretaria |

**Dominio:** `estudiolegal.local`

## Estructura de Active Directory

Organización lógica replicando un estudio jurídico chico:

    estudiolegal.local
    ├── _Usuarios
    │   ├── Socios
    │   ├── Abogados
    │   ├── Secretaria
    │   └── Externos
    ├── _Grupos
    │   ├── G_Socios
    │   ├── G_Abogados
    │   ├── G_Administrativos
    │   └── G_TI
    ├── _Equipos
    │   ├── Estaciones
    │   └── Servidores
    └── _Servicios

## GPOs aplicadas

| GPO | Aplicada a | Función |
|-----|------------|---------|
| Block-USB-Storage | _Equipos/Estaciones | Bloqueo de almacenamiento USB excepto para G_TI |
| Password-Policy | Dominio raíz | Mínimo 12 caracteres, complejidad obligatoria, expiración 90 días |
| Logon-Banner | Dominio raíz | Aviso legal de uso corporativo al iniciar sesión |
| Map-Drives | _Usuarios | Unidad H: perfil personal, unidad S: compartida del grupo |
| Restrict-Control-Panel | _Usuarios/Externos | Acceso restringido al panel de control |

## En curso

- [ ] Integrar pfSense / OPNsense como firewall perimetral
- [ ] Segmentar la red en VLAN de usuarios y VLAN de servidores
- [ ] Implementar monitoreo con Sysmon y revisión de Event Viewer
- [ ] Documentar baja y alta masiva de usuarios con PowerShell

## Stack técnico

- **Virtualización:** Oracle VirtualBox 7.x
- **SO servidor:** Windows Server 2022 Standard (evaluación 180 días)
- **SO clientes:** Windows 10 Pro / Windows 11 Pro
- **Análisis de red:** Wireshark
- **Scripts:** PowerShell y Bash

## Aprendizajes destacados

- Cómo se construye una OU bien estructurada y por qué importa para GPOs y delegación.
- Diagnóstico de problemas comunes: replicación de DNS, política no aplicada, GPO heredada vs bloqueada.
- Diferencia operativa entre `gpupdate /force` y reinicio para refrescar políticas.
- Filtrado WMI para aplicar GPOs según el tipo de equipo.

## Capturas

Ver carpeta `/screenshots` *(se agregan a medida que avanza el lab).*

---

> **Sobre este lab:** lo armé y lo mantengo como parte de mi formación práctica mientras curso la Tecnicatura en Seguridad Informática y proyecto mi primer rol formal en IT. Lo documento públicamente porque creo que mostrar *el cómo* es más valioso que enumerar tecnologías sin contexto.
