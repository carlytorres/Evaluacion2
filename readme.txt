1.-Dadas las siguientes tablas:

empleado (idEmpleado, nombreEmpleado,  fechaIngreso)
servicio (idServicio, nombreServicio, valorServicio)
vehiculo (idVehiculo, marcaVehiculo, modeloVehiculo)
prestación_servicio (idPrestacionServicio, IdServicio, idEmpleado, idVehiculo, fecha)

Crear las consultas

a.- Mostrar la cantidad de prestaciones de servicios ejecutados entre el 01 de octubrey el 26 de noviembre del 2018.

select count(idPrestacionServicio) from prestación_servicio between 2018-10-01 and 2018-11-26

b.-Mostrar la cantidad total de prestaciones realizadas agrupadas por idVehiculo.

select idVehiculo, count(idPrestacionServicio) from prestación_servicio group by idVehiculo

c.- Mostrar los vehículos con la menor cantidad de prestaciones de servicios realizados.

select idVehiculo,count(*) as Prestaciones from prestacion_servicio group by idVehiculo having COUNT(*) = 
( select MIN(contador) from ( select idVehiculo, count(*) as contador from prestacion_servicio GROUP BY idVehiculo) T )

2.-Crear con DDL unatabla empleado que contenga losiguiente:

IdEmpleado
nombre
apellido
dirección
teléfono
idDepartamento.

create table empleado
(
idEmpleado 	int 		not null,
nombre 		varchar(15)	not null,
apellido	varchar(15)	not null,
direccion	varchar(30)	not null,
telefono	varchar(15)	not null,
idDepartamento	int 	not null,
PRIMARY KEY (idEmpleado)
FOREIGN KEY (idDepartamento) REFERENCES departamento(idDepartamento) 
)



