Data_BD: base de datos fuente (ficticia)

Estas cuatro tablas simulan la base de datos de origen de un sistema de tickets de soporte de una fintech, el mismo tipo de sistema del que salen las tres consultas de la carpeta sql/. Todos los datos son 100% ficticios (generados con Python y Faker), pensados para que las consultas SQL de este proyecto se puedan correr contra ellas tal cual y devuelvan resultados coherentes.

Contexto: es una fintech de pagos y remesas con presencia en varios paises de Latinoamerica y Espana. El equipo de soporte atiende consultas de cuentas, verificacion de identidad (KYC), retiros, cargas de saldo, tarjetas y reclamos por cobros, repartidas en seis areas.

Data_BD_Tickets.csv (5800 filas)

Tabla de hechos. Cada fila es un ticket de soporte. Incluye la poblacion normal de casos (variados, en distintas areas) mas un lote de 800 tickets generados por un proceso automatico de deteccion de cuentas duplicadas (subject = 'POSSIBLE DUPLICATED USER'), que se resuelven solos en segundos y siempre los cierra el mismo agente.

Columnas: id_ext (identificador del ticket), createdAt/created_at (fecha de creacion), date_closed (fecha de cierre), date_resolve (fecha de resolucion), updated_at (ultima actualizacion), first_status_change (fecha de la primera respuesta, vacio en un 38% de los casos), status (2 Abierto, 3 Pendiente, 4 Resuelto, 5 Cerrado, 8 En Espera), type (categoria del ticket), priority (1 Baja a 4 Urgente), requester_id (quien pidio ayuda, referencia a Agentes), responder_id (quien lo atendio, referencia a Agentes), group_id (area responsable, referencia a Grupos), source (canal de entrada, referencia a Fuentes), subject (asunto del ticket).

Data_BD_Agentes.csv (915 filas)

Tabla de identidades. Guarda tanto a los clientes que abren tickets (role = Cliente, sin area asignada) como al staff de soporte que los resuelve (role en Agente Soporte, Agente Senior o Team Lead, con group_id asignado). Es la misma logica que la tabla Agents real: tanto requester_id como responder_id en Tickets apuntan aca.

Columnas: id_ext, name, email, role, group_id (solo para staff).

Data_BD_Grupos.csv (6 filas)

Las areas de soporte: Cuentas (Nivel Uno), Cuentas (Nivel Dos), Pagos y Transferencias, KYC y Verificacion, Tarjetas, Soporte Tecnico.

Columnas: id_ext, name.

Data_BD_Fuentes.csv (6 filas)

Los canales por los que entra un ticket: Email, Chat en Vivo, WhatsApp, Portal Cliente, Telefono, Facebook. Notar que la clave de union con Tickets es de texto (source), no un id numerico, igual que en el sistema real.

Columnas: source (clave de texto), name (nombre visible del canal).

Como se relacionan
Data_BD_Tickets.requester_id  --> Data_BD_Agentes.id_ext   (role = Cliente)
Data_BD_Tickets.responder_id  --> Data_BD_Agentes.id_ext   (role = staff de soporte)
Data_BD_Tickets.group_id      --> Data_BD_Grupos.id_ext
Data_BD_Tickets.source        --> Data_BD_Fuentes.source
Data_BD_Agentes.group_id      --> Data_BD_Grupos.id_ext    (solo agentes de staff)
Como usarlas

Cargalas en tu motor de base de datos con los nombres Tickets, Agents, Groups y Sources (sin el prefijo Data_BD_) para correr las consultas de la carpeta sql/ sin modificarlas. Si preferis mantener el prefijo en los nombres de tabla, solo tenes que ajustar el FROM de cada consulta.
