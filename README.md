## Apartado 1 

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

```bash
insert into EmpresasFCT values (DEFAULT,'PrimoPlus',FALSE,0,'2025-01-30');
insert into EmpresasFCT values (DEFAULT,'Microsoft',TRUE,3,'2025-01-27');
insert into EmpresasFCT values (DEFAULT,'Nintendo',TRUE,1,'2024-12-29');
insert into EmpresasFCT values (DEFAULT,'ZARA',TRUE,1,'2025-01-05');
insert into EmpresasFCT values (DEFAULT,'Atlus',FALSE,0,'2025-01-17');
```

## Apartado 3

```bash
select * from EmpresasFCT order by fechacontacto desc;
```

> Resultado de las querys del apartado 1,2 y 3↓
>
> ![Apartado 1_2_3](/img/apartado3.png)

## Apartado 4 

```bash
select name,city,commercial_company_name from res_partner where city='Tracy' order by commercial_company_name asc;
```

> Resultado de la querys de este apartado↓
>
> ![Apartado 4](/img/apartado4.png)

## Apartado 5

```bash
select r.name,a.name,a.invoice_date,a.amount_untaxed_signed from res_partner r left join account_move a on a.partner_id=r.id where a.move_type='in_refund' order by a.invoice_date desc;
```

> Resultado de la querys de este apartado↓
>
> ![Apartado 5](/img/apartado5.png)

## Apartado 6 

```bash
select r.name,a.name,a.amount_untaxed_signed
from res_partner r join account_move a on a.partner_id=r.id 
where a.move_type='out_invoice' group by r.name,a.name,a.amount_untaxed_signed 
having count(a.id) > 2
```

## Apartado 7

```bash
UPDATE res_partner SET email = replace(email, '@bilbao.example.com', '@bilbao.bizkaia.neus');
```

## Apartado 8 

```bash
DELETE from res_partner where commercial_company_name='Ready Mat';
```

