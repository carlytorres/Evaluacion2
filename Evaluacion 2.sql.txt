
/*CREACION DE LAS TABLAS Y CLAVES PARA DAR SOLUCION AL EJERCICIO N3*/

/* Crea la tabla CINE con su clave primaria ID*/

create table CINE 
(
   ID                   integer                        not null,
   DIRECCION            varchar(35)                    not null,
   TELEFONO             integer                        not null,
   primary key (ID)
);

/* Crea la tabla SALA con su clave primario N_SALA y clave foranea ID */

create table SALA 
(
   N_SALA               integer                        not null,
   ID                   integer                        not null,
   NOMBRE               varchar(40)                    not null,
   BUTACAS              integer                        not null,
   primary key (N_SALA),
   foreign key (ID) references CINE (ID)
);

/*Crea la tabla PROMOCION con su clave primaria IDPROMOCION*/

create table PROMOCION
(
   DESCRIPCION          varchar(30)                    not null,
   DESCUENTO            varchar(40)                    not null,
   ID_PROMOCION         integer                        not null,
   primary key (ID_PROMOCION)
);


/*Crea la tabla PELICULA con su clave primaria ID_PELICULA*/

create table PELICULA 
(
   ID_PELICULA          integer                        not null,
   TITULO_DISTR         varchar(35)                    not null,
   TITULO_ORIG          varchar(35)                    not null,
   GENERO               varchar(20)                    not null,
   IDIOMA               varchar(20)                    not null,
   SUBTITULOS           smallint                       not null,
   PAIS_ORIGEN          varchar(25)                    not null,
   ANO                  integer                        not null,
   URL                  varchar(50)                    not null,
   DURACION_H           integer                        not null,
   DURACION_M           integer                        not null,
   CALIFICACION         varchar(35)                    not null,
   FECHA_ESTRENO        date                           not null,
   RESUMEN              long varchar                   not null,
   primary key (ID_PELICULA)
);

/*Crea la tabla OPINION con su clave primaria ID_RESUMEN y la clave foranea ID_PELICULA*/

create table OPINION 
(
   ID_RESUMEN           integer                        not null,
   ID_PELICULA          integer                        not null,
   RESUMEN              long varchar                   not null,
   PERSONA              varchar(30)                    not null,
   EDAD                 integer                        not null,
   FECHA                date                           not null,
   CAIFICACION          varchar(15)                    not null,
   COMENTARIO           long varchar                   not null,
   primary key (ID_RESUMEN),
   foreign key (ID_PELICULA) references PELICULA (ID_PELICULA)
);

/*Crea la tabla PARTICIPANTE con su clave primaria ID_PARTICIPANTE*/

create table PARTICIPANTE 
(
   ID_PARTICIPANTE      integer                        not null,
   NOMBRE               varchar(40)                    not null,
   NACIONALIDAD         varchar(30)                    not null,
   primary key (ID_PARTICIPANTE)
);

/*Crea la tabla PARTICIPAN que es el detalle de los que participan en la pelicula ya sea director o actor*/
/*con su clave primaria ID_PARTICIPANTE,ID_PELICULA Y las claves foraneas ID_PARTICIPANTE, ID_PELICULA*/

create table PARTICIPAN 
(
   ID_PARTICIPANTE      integer                        not null,
   ID_PELICULA          integer                        not null,
   ACTOR                boolean                        null,
   DIRECTOR             boolean                        null,
   primary key (ID_PARTICIPANTE, ID_PELICULA),
   foreign key (ID_PARTICIPANTE) references PARTICIPANTE (ID_PARTICIPANTE),
   foreign key (ID_PELICULA) references PELICULA (ID_PELICULA)
);

/*Crea la tabla FUNCION con su clave primaria ID_FUNCION y las claves foraneas N_SALA,ID_PELICULA*/

create table FUNCION 
(
   FECHA                date                           not null,
   HORA                 time                           not null,
   ID_FUNCION           integer                        not null,
   N_SALA               integer                        not null,
   ID_PELICULA          integer                        not null,
   primary key (ID_FUNCION),
   foreign key (N_SALA) references SALA (N_SALA),
   foreign key (ID_PELICULA) references PELICULA (ID_PELICULA)
);

/*Crear tabla DISPONE que es el detalle de las promociones segun las funciones del cine */
/*con su claves primarias ID_PROMOCION,ID_FUNCION y las claves foraneas ID_PROMOCION,ID_FUNCION*/

create table DISPONE 
(
   ID_PROMOCION         integer                        not null,
   ID_FUNCION           integer                        not null,
   primary key (ID_PROMOCION, ID_FUNCION),
   foreign key (ID_PROMOCION) references PROMOCION (ID_PROMOCION),
   foreign key (ID_FUNCION) references FUNCION (ID_FUNCION)
);
