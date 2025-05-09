-- crear la base de datos Stage_Norwith
create database stage_northwind;

-- Crear la base de datos datamar_northwind
create database datamar_northwind;

-- Implementar la base de datos stage_northwind 
	use stage_northwind;
	create table Categorias (
	categoriaId int not null,
	nombreCategoria varchar(15),
)
	
	create table clientes(
	clienteId char(5) not null,
	compania varchar(40) not null,
	ciudad varchar(15),
	region varchar(15),
	codigoPostal char(10),
	pais nvarchar(15)
);
		
	create table Empleados(
	idEmpleado int not null,
	nombre varchar(10),
	apellido varchar(20) not null,
	fecha_contratacion date,

)

	create table Producto (
	productoId int not null,
	nombreProducto varchar(50),
	precioUnitario decimal(15,2) not null,
);

create table Proveedor (
	idProvedor int not null,
	proveedorNombre varchar (40) not null,
	ciudad varchar(15), 
	region varchar(15),
	pais varchar (15),
)

create table Ventas(
	idCliente char(5) not null,
	empleadoCodigo int not null,
	productoCodigo int not null,
	ventasOrden datetime not null,
	ventasMonto decimal(15,2) not null,
	ventasUnidades int not null,
	ventasPrecioUnitario decimal(15,2) not null,
	ventasDescuentos decimal(15,2) not null,
)

-- Crear el datamartNorthwind
use datamar_northwind
create table dimCliente(
	clienteSkey int not null,
	clienteCodigoBKey char(5) not null,
	clienteCompania varchar(40) not null,
	clienteCiudad varchar(15) not null,
	clienteRegion varchar(25) not null,
	clientePais varchar(15) not null,
	constraint pk_dimCliente
	primary key (clienteSkey)
);

drop table dimCliente

create table dimEmpleado (
	empleadoSkey int not null identity(1,1),
	empleadoCodigoBKey int not null,
	empleado_NombreCompleto varchar(100) not null,
	constraint pk_dimempleado
	primary key(empleadoSkey)
);

create table dimProducto (
productoSkey int not null identity (1,1),
productoCodigoBkey int not null,
productoNombre varchar(80) not null,
productoCategoriaNombre varchar (15) not null,
constraint pk_dimProducto
primary key (productoSkey)
);

create table dimTiempo(
	tiempo_Skey int not null identity(1,1),
	tiempoFechaActual datetime not null,
	tiempoAnios int not null,
	tiempoTrimestre int not null,
	tiempoMes int not null,
	tiempoSemana int not null,
	tiempoDiaAnio int not null,
	tiempoDiaMes int not null,
	timepoDiaSemana int not null
	constraint pk_dimTiempo
	primary key(tiempo_Skey)
);

create table FactVentas (
	clienteSkey int not null,
	empleadoSkey int not null,
	productoSkey int not null,
	tiempoSKey int not null,
	ventasNOrden int not null,
	ventasMontos decimal (15,2) not null,
	ventasUnidades int not null,
	ventasPUnitario decimal(15,2) not null,
	ventasDescuentos decimal(15,2) not null,
	constraint pk_ventas
	primary key (clienteSkey, empleadoSkey,productoSkey, tiempoSkey),
	constraint pk_factventas_dimCliente
	foreign key (clienteSKey)
	references dimCliente(ClienteSKey),
	constraint fk_factventas_dimEmpleado
	foreign key (empleadoSKey)
	references dimEmpleado(empleadoSKey),
	constraint pk_factventas_dimProducto
	foreign key(productoSkey)
	references dimProducto(productoSKey),
	constraint fk_factventas_dimTiempo
	foreign key(tiempoSKey)
	references dimTiempo(tiempoSKey)
);

