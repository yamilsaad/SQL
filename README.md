# SQL
#CREACION DE TABLAS E INSERT DE VALORES

create table CLIENTE(
	Nombre varchar(50)not null,
	Apellido varchar(50)not null,
	DNI int not null,
	Telefono int not null,
	Fecha_Alta varchar(10)not null,
	primary key (DNI));

create table ARTICULOS(
	Nombre varchar(50) not null,
	Cod_Articulo int not null,
	Descripcion varchar(50) not null,
	Unidades_Disponibles int not null,
	primary key (Cod_Articulo));
	

create table VENTA(
	Fecha_Hora varchar(50)not null,
	DNI_CLIENTE int not null,
	Cod_Articulo1 int not null,
	Cantidad_Vendida int not null,
	primary key (Fecha_Hora),
	foreign key (DNI_CLIENTE) references CLIENTE(DNI),
	foreign key (Cod_Articulo1) references ARTICULOS(Cod_Articulo));
 
insert into ARTICULOS values('Yerba',001,'Paquete_1kg',90);
insert into ARTICULOS values('Azucar',002,'Paquete_1kg',87);
insert into ARTICULOS values('Pan',003,'Bolsa_1/2kg',105);
insert into ARTICULOS values('Lecha_Larga_Vida',004,'Caja_Tetrapack',103);
insert into ARTICULOS values('Bolsa_Caramelo',005,'Bolsa_250grs',66);
insert into ARTICULOS values('Queso_Cremoso',006,'Paquete_250grs',42);

insert into CLIENTE values('Juan','Piquete',33445566,0111567899879,'15/05/2015');
insert into CLIENTE values('Carlos','Calabresa',34347788,0111564566549,'16/06/2016');
insert into CLIENTE values('Esteban','Quito',33556677,0111561233219,'17/07/2017');
insert into CLIENTE values('Andrea','Lira',33445588,0342155398022,'18/08/2018');
insert into CLIENTE values('Laura','Agnat',22445566,0342156378022,'19/09/2019');
insert into CLIENTE values('Marixa','Bella',25335999,0342154348022,'20/10/2020');

insert into VENTA values('01/01/2019''11:30',33445566,001,5);
insert into VENTA values('01/02/2019''12:30',34347788,002,4);
insert into VENTA values('01/05/2019''10:30',33556677,001,7);
insert into VENTA values('13/04/2019''09:30',33445588,002,3);
insert into VENTA values('13/07/2019''09:00',22445566,003,2);
insert into VENTA values('14/01/2019''10:00',25335999,003,1);
insert into VENTA values('14/02/2019''11:00',33445566,004,1);
insert into VENTA values('14/06/2019''18:00',34347788,001,4);
insert into VENTA values('14/06/2019''18:05',33556677,005,6);
insert into VENTA values('14/07/2019''18:30',33445588,004,3);
insert into VENTA values('14/08/2019''18:00',22445566,006,5);
insert into VENTA values('14/09/2019''19:00',25335999,003,2);

#ALGUNAS CONSULTAS SQL

select NOMBRE,DNI,FECHA_ALTA
from CLIENTE
where FECHA_ALTA >= '15/09/2012';

select nombre, sum(cantidad_vendida)
from cliente join venta on dni_cliente = dni
group by nombre

select c.nombre,c.apellido,a.nombre
from cliente c join venta v on c.dni = v.dni_cliente
join articulos a on a.cod_articulo= v.cod_articulo1
order by v.fecha_hora desc;

select nombre, sum(cantidad_vendida)
from articulos join venta on cod_articulo=cod_articulo1
group by nombre
order by nombre asc;

select dni
from cliente join venta on dni=dni_cliente
group by dni
having sum (cantidad_vendida)>10;

#CREACION DE FUNCIONES

create function ventas_cliente(dni_cliente int)
returns int
as
'select count(*)
from venta
where dni_cliente=$1
group by dni_cliente'
LANGUAGE SQL;


