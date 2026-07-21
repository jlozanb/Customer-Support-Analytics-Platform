SQL: consultas de analisis de soporte

Estas son las tres consultas reales de un sistema de tickets de soporte, adaptadas unicamente para usar datos ficticios (nombres de agentes y volumen de tickets), sin cambiar la logica de negocio. Corren contra las tablas de la carpeta data_bd/ (cargadas como Tickets, Agents, Groups y Sources, sin el prefijo Data_BD_).

01_Extraccion_Detalle_Tickets.sql

Que hace: devuelve un ticket por fila, con fecha de creacion, fecha de cierre, mes de resolucion, estado, agente que lo levanto (requester_id), area (Groups) y tipo de ticket.

Para que sirve: es la base de cualquier reporte de detalle o auditoria. Tambien es el punto de partida para armar el extracto plano con columnas calculadas (hora, dia de la semana, mes actual, etc), que se arma despues en Power Query o en un paso adicional de transformacion.

Tablas que usa: Tickets (tabla principal), Agents (por requester_id), Groups (por group_id).

02_Rendimiento_Equipo.sql

Que hace: cuenta tickets por agente, clasificandolos en tres categorias (Abiertos, Atendidos, Resueltos) y en tres ventanas de tiempo moviles (ultimas 24 horas, ultimos 7 dias, ultimos 30 dias). Un ticket se cuenta como Abierto si esta en estado 2 y fue creado en las ultimas 24 horas; como Atendido si esta en estado 3, 4, 5 u 8 y se actualizo en las ultimas 24 horas; y como Resuelto en cualquier otro caso.

Para que sirve: es la consulta detras de un dashboard de carga de trabajo por agente, para ver quien esta resolviendo mas casos y en que ventana de tiempo.

Tablas que usa: Agents (agente responsable), Tickets (por responder_id).

03_Rendimiento_SLA.sql

Que hace: calcula dos metricas mensuales de los ultimos 60 dias, tiempo medio de primera respuesta (desde created_at hasta first_status_change) y tiempo medio de resolucion (desde created_at hasta updated_at, solo para tickets en estado 4 o 5). Excluye tickets de tipo Llamadas y los que llegaron por Telefono o Facebook, porque esos canales no tienen un tiempo de primera respuesta comparable (la interaccion es en vivo).

Para que sirve: es la consulta detras del dashboard de SLA, para ver si el equipo esta respondiendo y resolviendo dentro de los tiempos objetivo, y como evoluciona mes a mes.

Tablas que usa: Tickets (fechas y estado), Sources (para filtrar por canal).

Orden de lectura sugerido

Si estas armando el portfolio y queres mostrar el flujo completo, el orden logico es 01 (para entender la estructura del dato caso a caso), despues 02 y 03 (las dos consultas de KPI que se arman a partir de esa misma tabla de tickets).
