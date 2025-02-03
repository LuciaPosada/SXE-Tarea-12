
## Apartado 1 

**Elabora y ejecuta una sentencia que cree una tabla llamada “EmpresasFCT“con los siguientes campos: idEmpresa, nombre, quiereAlumnos, numAlumnos y fechaContacto.**

Consulta:

```bash
CREATE TABLE EmpresasFCT (
    idEmpresa SERIAL PRIMARY KEY,
    nombre VARCHAR(40),
    quiereAlumnos BOOLEAN,
    numAlumnos INTEGER,
    fechaContacto DATE
);
```

## Apartado 2 

**Inserta 5 registros inventados en la tabla a través de una sentencia SQL.**

Consulta:

```bash
insert into EmpresasFCT values (DEFAULT,'PrimoPlus',FALSE,0,'2025-01-30');
insert into EmpresasFCT values (DEFAULT,'Microsoft',TRUE,3,'2025-01-27');
insert into EmpresasFCT values (DEFAULT,'Nintendo',TRUE,1,'2024-12-29');
insert into EmpresasFCT values (DEFAULT,'ZARA',TRUE,1,'2025-01-05');
insert into EmpresasFCT values (DEFAULT,'Atlus',FALSE,0,'2025-01-17');
```

## Apartado 3

**Muestra todos los datos de la tabla EmpresasFCT ordenados por fechaContacto, de modo que en la primera fila salga el que tenga fecha más reciente.**

Consulta:

```bash
SELECT * from EmpresasFCT order by fechacontacto desc;
```

> Resultado de las querys del apartado 1, 2 y 3 ↓
>
> ![Apartado 1_2_3](/img/apartado3.png)

## Apartado 4 

**Obten un listado de todos los contactos de Odoo (no empresas) con la siguiente información: nombre, cuya ciudad sea Tracy, nombre comercial de la empresa. Ordenados alfabéticamente por el nombre comercial de la empresa**

Consulta: 

```bash
SELECT name,
       city,
       commercial_company_name
from res_partner
       where city='Tracy'
       and is_company=False 
       order by commercial_company_name asc;
```

> Resultado de la querys de este apartado↓
>
> ![Apartado 4](/img/apartado4.png)

## Apartado 5

**Obtén un listado de empresas proveedoras, que han emitido algún reembolso, con la siguiente información: nombre de empresa, número de factura, fecha de la factura, total factura SIN impuestos.
Ordenadas por fecha de factura de modo que la primera sea la más reciente.**

Consulta:

```bash
SELECT r.name,
       a.name,
       a.invoice_date,
       a.amount_untaxed_signed
from res_partner r
left join account_move a
on a.partner_id=r.id
       where a.move_type='in_refund'
       order by a.invoice_date desc;
```

> Resultado de la querys de este apartado ↓
>
> ![Apartado 5](/img/apartado5.png)

## Apartado 6 

**Obtén un listado de empresas clientes, a las que se les ha emitido más de dos facturas de venta (solo venta) confirmadas, mostrando los siguientes datos: nombre de la empresa, número de facturas, total facturado SIN IMPUESTOS.**

Consulta:

```bash
SELECT r.name,
       count(distinct a.name) as num_facturas,
       sum(distinct a.amount_untaxed_signed) as total_sin_impuestos
from res_partner r 
join account_move a
on a.partner_id=r.id 
       where a.move_type='out_invoice' 
       and state='posted'
       group by r.name
       having count(*) > 2
```

> Resultado de la querys de este apartado ↓
>
> ![Apartado 6](/img/apartado6.png)

## Apartado 7

**Crea una sentencia que actualice el correo de los contactos cuyo dominio es @bilbao.example.com a @bilbao.bizkaia.neus.**

Consulta:

```bash
UPDATE res_partner set email = replace(email, '@bilbao.example.com', '@bilbao.bizkaia.neus');
```

> Entradas de la BD antes de la consulta ↓
>
> ![Apartado 7](/img/apartado7.1.png)
> 
> Resultado de la querys de este apartado ↓
> 
> ![Apartado 7](/img/apartado7.2.png)

## Apartado 8 

**Crea una sentencia que elimine todos los contactos pertenecientes a la empresa “Ready Mat”, pero mantén la empresa.**

Consulta:

```bash
DELETE from res_partner where commercial_company_name='Ready Mat' and is_company=FALSE;
```

> Entradas de la BD antes de la consulta ↓
>
> ![Apartado 8](/img/apartado8.1.png)
> 
> Resultado de la querys de este apartado ↓
> 
> ![Apartado 8](/img/apartado8.2.1.png)

