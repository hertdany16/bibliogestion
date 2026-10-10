# BiblioGestión

## Objetivo

BiblioGestión es un sistema de gestión de biblioteca pensado para digitalizar el control de libros, préstamos, devoluciones y reservas, reemplazando los registros manuales que suelen generar errores y pérdida de información.

## Problema que resuelve

Actualmente llevar el control de préstamos y devoluciones de forma manual (o en hojas sueltas) hace difícil saber qué libros están disponibles, quién los tiene prestados y cuándo vencen. BiblioGestión centraliza esa información en un solo sistema para que el bibliotecario y los usuarios puedan consultarla en tiempo real.

## Funcionalidades principales

- Consultar disponibilidad de libros en el catálogo, con búsqueda y filtros.
- Registrar préstamos y devoluciones desde un sistema centralizado.
- Reservar un libro que esté prestado.
- Notificar al usuario antes de que venza su préstamo.
- Generar reportes del inventario.
- Registro y autenticación de usuarios (estudiante / bibliotecario).

## Arquitectura seleccionada

El sistema está diseñado bajo una **arquitectura en capas sobre un modelo cliente-servidor**, separando la interfaz, la lógica de negocio y los datos para que cada parte se pueda mantener de forma independiente:

1. **Cliente** (navegador/dispositivo) → se comunica por HTTPS con la interfaz.
2. **Interfaz de usuario** (catálogo, préstamos, reservas, panel del bibliotecario).
3. **Módulo de autenticación** (login, roles: estudiante / bibliotecario).
4. **Servicios de lógica de negocio** (préstamos, reservas, reportes).
5. **Servicio de notificaciones** (avisos de vencimiento).
6. **Capa de acceso a datos** (repositorios / ORM).
7. **Base de datos** (libros, ejemplares, usuarios, préstamos, reservas).

Diagrama completo: ver `docs/arquitectura.png` y el diagrama en Visual Paradigm Online enlazado en la tarjeta "Definición de arquitectura inicial" del tablero.

## Organización frontend / backend

**Frontend (interfaz de usuario)**
Responsable de mostrar el catálogo, los formularios de préstamo/devolución/reserva y el panel del bibliotecario. No contiene lógica de negocio: solo arma las peticiones y muestra lo que el backend responde.

**Backend (servicios)**
Responsable de toda la lógica: autenticación y manejo de sesión, reglas de préstamos y devoluciones, reservas, generación de reportes, envío de notificaciones y acceso a la base de datos.

**Comunicación entre ambos**
El frontend se comunica con el backend mediante peticiones **REST sobre HTTPS, con datos en formato JSON**. Cada petición del frontend pasa primero por el módulo de autenticación (que valida la sesión) antes de llegar a los servicios de lógica de negocio; estos, a su vez, usan la capa de acceso a datos para leer o escribir en la base de datos, y el servicio de notificaciones se activa de forma independiente cuando un préstamo está por vencer.

## Herramientas utilizadas

- **GitHub** — control de versiones del proyecto y la documentación.
- **GitHub Projects** — tablero para organizar y dar seguimiento a las tareas.
- **GitHub Issues** — registro de historias de usuario, incidencias y tareas pendientes.
- **Visual Paradigm Online** — modelado UML y diagrama de arquitectura.
- **Word / PDF** — documentación de las entregas semanales del curso.

## Estado actual del proyecto

- Consulta de disponibilidad de libros (catálogo): **finalizado**.
- Arquitectura inicial del sistema: **finalizada y documentada**.
- Catálogo de libros (búsqueda y filtros): **en revisión**.
- Registro de préstamos en sistema centralizado: **en progreso**.
- Gestión de préstamos y devoluciones / registro y autenticación de usuarios: **en progreso**.
- Notificación antes de vencer el préstamo, reservar un libro prestado, reportes de inventario: **pendientes**.
