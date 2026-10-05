---
name: mep-datasheet-indexer-pro
description: Se activa ante peticiones de fichas técnicas, datasheets o especificaciones de productos MEP (climatización, electricidad, fontanería, PCI). Realiza búsqueda web, prioriza la versión más reciente del fabricante, resuelve discrepancias cronológicas y extrae parámetros técnicos en Sistema Internacional (SI) organizados en tablas.
allowed-tools: [google_search, personal_context]
---

# Skill: Extractor e Indexador de Fichas Técnicas MEP

## 1. Activación y Alcance
* Este skill se ejecuta al detectar palabras clave como "datasheet", "ficha técnica", "catálogo técnico" o "curva de rendimiento" seguidas de un modelo o marca de producto de instalaciones.
* El objetivo es evitar datos obsoletos y proporcionar una tabla de diseño lista para justificación técnica.

## 2. Protocolo de Búsqueda y Verificación
1.  **Búsqueda Multifuente:** Localiza el producto en la web oficial del fabricante. Si no está disponible, utiliza portales de distribución técnica contrastada.
2.  **Validación Cronológica:**
    * Extrae la fecha de revisión, código de edición o año de copyright del documento.
    * Si existen múltiples versiones, selecciona la de fecha más reciente.
    * En caso de encontrar discrepancias en datos críticos (ej. consumo eléctrico o dimensiones), realiza una triangulación con una tercera fuente y adopta el dato del documento con la fecha de publicación más tardía.
3.  **Detección de Reemplazo:** Si el producto está descatalogado, indica el modelo que el fabricante propone como sustituto actual.

## 3. Extracción y Normalización de Datos
Extrae la información y organízala estrictamente bajo el **Sistema Internacional de Unidades (SI)**. No inventes datos; usa "N/D" si el parámetro no existe.

### Tabla de Identificación
| Campo | Detalle |
| :--- | :--- |
| Fabricante / Marca | [Nombre] |
| Modelo / Serie | [Referencia exacta] |
| Versión Documento | [Fecha o código de revisión] |

### Tabla de Parámetros Técnicos (Ejemplo según especialidad)
* **Mecánica/Clima:** Potencias térmicas ($kW$), caudales de aire ($m³/h$), presiones estáticas ($Pa$), rendimientos ($COP$/$EER$/$SEER$).
* **Electricidad:** Tensión ($V$), intensidad nominal ($A$), poder de corte ($kA$), grado IP, sección de embornado.
* **Hidráulica:** Caudales ($l/min$ o $m³/h$), altura manométrica ($m.c.i.$), diámetros nominales ($DN$ o pulgadas).

## 4. Instrucciones de Salida
1.  **Bloque Crítico:** Si el producto tiene una advertencia técnica relevante (ej. requiere accesorios específicos para cumplir normativa), lístalo al inicio en un bloque de cita (`>`).
2.  **Cuerpo:** Presenta las tablas generadas en el paso 3.
3.  **Fuentes:** Incluye el enlace directo a la datasheet analizada bajo el epígrafe "Fuente Verificada".
4.  **Rigurosidad:** No añadas comentarios subjetivos sobre la calidad del producto; cíñete a los datos técnicos verificables.