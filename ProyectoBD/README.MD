# Tabla "pacientes":

id (int, primary key, auto increment)
historia_clinica (int, unique)
nombre (varchar)
numero_seguridad_social (varchar)
direccion (varchar)
telefono (varchar)
fecha_nacimiento (date)

# Tabla "servicios":

id (int, primary key, auto increment)
nombre (varchar)

# Tabla "ingresos":

id (int, primary key, auto increment)
paciente_id (int, foreign key references pacientes.id)
servicio_id (int, foreign key references servicios.id)
fecha_ingreso (date)
fecha_alta (date)
diagnostico (varchar)

# Tabla "consumos":

id (int, primary key, auto increment)
paciente_id (int, foreign key references pacientes.id)
servicio_id (int, foreign key references servicios.id)
fecha_consumo (date)
unidades (int)
medicamento_id (int, foreign key references medicamentos.id)

# Tabla "medicamentos":

id (int, primary key, auto increment)
registro_id (int)
nombre_comercial (varchar)
nombre_clinico (varchar)
compuesto_quimico (varchar)
ubicacion (varchar)
codigo_proveedor (varchar)
unidades_por_envase (int)
precio_por_unidad (decimal)
precio_total_por_envase (decimal)

# Tabla "facultativos":

id (int, primary key, auto increment)
colegiado_id (int, unique)
nombre (varchar)
direccion (varchar)
telefono (varchar)
servicio_id (int, foreign key references servicios.id)

# Tabla "recetas":

id (int, primary key, auto increment)
facultativo_id (int, foreign key references facultativos.id)
paciente_id (int, foreign key references pacientes.id)
ingreso_id (int, foreign key references ingresos.id)
medicamento_id (int, foreign key references medicamentos.id)

# Tabla "revisiones":

id (int, primary key, auto increment)
facultativo_id (int, foreign key references facultativos.id)
paciente_id (int, foreign key references pacientes.id)
ingreso_id (int, foreign key references ingresos.id)
fecha (date)
hora (time)
informe (text)

[Diagrama ER]
# Diagrama de entidad-relación:

Pacientes (1,N) --- (0,N) Ingresos: Un paciente puede tener cero o más ingresos, y cada ingreso pertenece a un paciente.

Pacientes (1,N) --- (0,N) Consumos: Un paciente puede tener cero o más consumos, y cada consumo pertenece a un paciente.

Pacientes (1,N) --- (0,N) Recetas: Un paciente puede tener cero o más recetas, y cada receta pertenece a un paciente.

Pacientes (1,N) --- (0,N) Revisiones: Un paciente puede tener cero o más revisiones, y cada revisión pertenece a un paciente.

Servicios (1,N) --- (0,N) Ingresos: Un servicio puede estar asociado a cero o más ingresos, y cada ingreso pertenece a un servicio.

Servicios (1,N) --- (0,N) Consumos: Un servicio puede estar asociado a cero o más consumos, y cada consumo pertenece a un servicio.

Servicios (1,N) --- (0,N) Facultativos: Un servicio puede tener cero o más facultativos, y cada facultativo pertenece a un servicio.

Ingresos (1,1) --- (0,N) Recetas: Cada ingreso debe tener cero o más recetas, y cada receta pertenece a un ingreso.

Ingresos (1,1) --- (0,N) Revisiones: Cada ingreso debe tener cero o más revisiones, y cada revisión pertenece a un ingreso.

Consumos (1,1) --- (1,N) Medicamentos: Cada consumo debe tener al menos un medicamento asociado.

Facultativos (1,N) --- (0,N) Recetas: Un facultativo puede tener cero o más recetas, y cada receta pertenece a un facultativo.

Facultativos (1,N) --- (0,N) Revisiones: Un facultativo puede tener cero o más revisiones, y cada revisión pertenece a un facultativo.

Recetas (1,1) --- (0,N) Medicamentos: Cada receta debe tener al menos un medicamento asociado.

Revisiones (1,1) --- (0,N) Medicamentos: Cada revisión debe tener al menos un medicamento asociado.
