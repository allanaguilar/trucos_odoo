# Ejemplo de consulta SQL en Odoo

```
cad_short = self.default_code
                    # cad_short = "131012"
                    self.env.cr.execute("SELECT * FROM product_template  WHERE default_code LIKE '" + cad_short + "%' ")
                    if self.env.cr.rowcount:
                        res = self.env.cr.dictfetchall()
                        for fila in res:
                            mayor = 0
                            numero_correlativo = fila['default_code']
                            numero_correlativo = numero_correlativo[6:9]
                            if numero_correlativo == '':
                                numero_correlativo = '0'
                            numero = int(numero_correlativo)
                            if numero > mayor:
                                mayor = numero
 ```
 
 # Ejemplo de consulta SQL en Odoo buscando un elemento

```
contpm = 0
            numero2 = 0
            for task in order.list_task_ids:
                numero2 = numero2 + 1
                contpm = contpm + 1
                self.env.cr.execute("SELECT id FROM maintenance_tree  WHERE contador = '" + str(contp) + "'")
                if self.env.cr.rowcount:
                    parent_code = self.env.cr.fetchone()[0]
                vals3 = {'cod': "TA" + str(task.id), 'name': order.desc + " / " + task.task_id.name, 'parent_id': parent_code , 'end': task.end,
                         'numero': str(numero) + "."+ str(numero2),
                         'costo_rc': task.importe, 'costo': task.importe,
                         'type': 'TA',
                         'deadline': task.deadline,
                         'peticion': order.request_name,
                         'sector': order.sector_name,
                         'responsable': task.employee_id.name}
                self.env['maintenance.tree'].create(vals3)
 ```
 
 
 
 # Usos de CR

```
cr.dictfetchall() will give you [{'reg_no': 123},{'reg_no': 543},].
cr.dictfetchone() will give you {'reg_no': 123}.
cr.fetchall() will give you '[(123),(543)]'.
cr.fetchone() will give you '(123)'.
```