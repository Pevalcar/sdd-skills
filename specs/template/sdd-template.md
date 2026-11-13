# Especificación — {{spec_id}}

{{nombre_funcionalidad}}

## Resumen Ejecutivo

{{breve descripcion de 2-3 lineas}}

## Historias de Usuario

### RF-001: {{titulo_rf_1}}

**Como** {{tipo_usuario}}  
**Quiero** {{objetivo}}  
**Para** {{beneficio}}

- [ ] Hecho cuando: {{criterio_aceptacion}}

### RF-002: {{titulo_rf_2}}

**Como** {{tipo_usuario}}  
**Quiero** {{objetivo}}  
**Para** {{beneficio}}

- [ ] Hecho cuando: {{criterio_aceptacion}}

## Restricciones

- {{restriccion_tecnica}}
- {{restriccion_de_negocio}}

## Criterios de Prueba

| RF | Input | Output | Estados |
|----|-------|--------|---------|
| RF-001 | {{casos}} | {{resultados}} | {{estados_verificables}} |

## API (si aplica)

### Endpoin 1

```
POST /api/{{endpoint}}
Body:
{
  "param1": "type",
  "param2": "type"
}

Response:
{
  "status": "success|error",
  "data": {...}
}
```

## Notas

- {{observaciones_tecnicas}}
- {{dependencias}}

---

**Plantilla usada:** specs/template/sdd-template.md