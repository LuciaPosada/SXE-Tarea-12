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

## Apartado 4 

```bash
select name,city,commercial_company_name from res_partner where city='Tracy' order by commercial_company_name asc;
```

## Apartado 5

```bash
select r.name,a.name,a.invoice_date,a.amount_untaxed_signed from res_partner r left join account_move a on a.partner_id=r.id where a.move_type='in_refund' order by a.invoice_date desc;
```

## Apartado 6 

```bash
select r.name,a.name,a.amount_untaxed_signed from res_partner r left join account_move a on a.partner_id=r.id where a.move_type='out_invoice' GROUP BY r.name,a.name,a.amount_untaxed_signed HAVING COUNT(*) > (
  SELECT COUNT(*) 
    FROM res_partner
    GROUP BY name
  );
```

## Apartado 7

## Apartado 8 

