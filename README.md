# Standout · MVP de Control de Caja Larga Estadía

## Qué es
Una app estática en un solo archivo HTML para validar la lógica de tesorería y caja de larga estadía.

Sirve para:
- cargar movimientos bancarios diarios,
- cargar liquidaciones resumidas por apartamento,
- registrar provisiones,
- separar capas de caja,
- mostrar cuánto del banco es realmente de Standout,
- detectar descuadre entre saldo bancario real y saldo esperado.

## Qué NO es todavía
No es aún un sistema multiusuario con base de datos real.
No se conecta automáticamente con Bancolombia.
No clasifica movimientos con IA de forma autónoma.

## Cómo abrirlo
Solo abre el archivo `standout_tesoreria_mvp.html` en tu navegador.

## Cómo montarlo en GitHub Pages
1. Crea un repositorio nuevo en GitHub.
2. Sube el archivo `standout_tesoreria_mvp.html`.
3. Renómbralo a `index.html`.
4. En GitHub, entra a **Settings > Pages**.
5. En **Build and deployment**, elige **Deploy from a branch**.
6. Selecciona la rama principal y la carpeta `/root`.
7. Guarda y GitHub te dará una URL pública.

## Flujo correcto de uso
1. Crear o actualizar las cuentas del mes con saldo inicial y saldo real.
2. Cargar movimientos diarios del banco.
3. Cargar liquidaciones resumidas por apartamento.
4. Cargar provisiones relevantes.
5. Revisar el dashboard.
6. Si el descuadre no es 0, ir a reportes y revisar por cuenta y rubro.

## Estructura funcional del MVP
### 1. Dashboard
Responde la pregunta principal:
- cuánto hay en banco,
- cuánto es realmente de Standout,
- cuánto está comprometido con terceros,
- cuánto queda disponible para operar,
- si el descuadre bancario es 0.

### 2. Cuentas
Por cada cuenta bancaria del mes:
- saldo inicial,
- saldo real,
- conciliación contra movimientos.

### 3. Movimientos
Entrada diaria de banco.
Campos:
- fecha
- cuenta
- tipo
- rubro
- subrubro
- apartamento
- descripción
- valor

### 4. Liquidaciones
Resumen mensual por apartamento.
Campos:
- canon
- depósito recibido
- depósito devuelto
- extras/daños
- gastos del propietario
- gastos Standout
- comisión bruta
- IVA
- giro al propietario
- retenciones

### 5. Provisiones
Para ICA, compras por volumen, reservas internas y demás partidas que no quieres perder del radar.

### 6. Reportes
Consultas por:
- mes
- apartamento
- cuenta
- rubro

## Lógica financiera del dashboard
### Banco real
Suma de saldos reales cargados por cuenta.

### Banco esperado
Saldo inicial del mes + movimientos netos del mes.

### Descuadre bancario
Banco real - banco esperado.

### Caja real Standout
Banco real
- depósitos en custodia pendientes
- giros a propietarios pendientes
- IVA pendiente
- retenciones pendientes

### Caja disponible
Caja real Standout
- provisiones internas pendientes

## Ruta recomendada de evolución
### Fase 1
Usar este MVP 2 a 4 semanas para validar categorías, procesos y responsables.

### Fase 2
Llevarlo a una app con backend real:
- login por usuario,
- base de datos,
- adjuntos,
- bitácora,
- permisos,
- histórico mensual.

### Fase 3
Agregar agente asistente:
- clasificación sugerida de movimientos,
- alertas automáticas,
- cierre diario guiado,
- detección de anomalías.

## Observación importante
Este MVP usa `localStorage`. Eso significa que la información vive en ese navegador y en ese equipo.
Para no perder la base:
- exporta el JSON con frecuencia,
- o migra rápido a una versión con backend.
