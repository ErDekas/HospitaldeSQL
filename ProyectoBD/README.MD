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
