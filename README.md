# README - Prueba de carga con K6

## DESCRIPCIÓN GENERAL

Este proyecto contiene una prueba de carga automatizada al servicio de autenticación de la API pública https://fakestoreapi.com/auth/login, utilizando la herramienta K6.

El objetivo es evaluar el comportamiento del endpoint bajo condiciones de concurrencia moderada, validando:
- Alcanzar al menos 20 TPS
- Tiempo de respuesta < 1.5 segundos (p95)
- Tasa de error < 3%

---

## REQUISITOS

- K6 v1.5.0 o superior
- Sistema operativo: Windows, Linux o macOS
- Conexión a internet activa

---

## INSTALACIÓN DE K6 EN WINDOWS

### Opción 1: Usando Chocolatey (recomendado)
1. Instala Chocolatey si no lo tienes: https://chocolatey.org/install
2. Luego ejecuta:
```powershell
   choco install k6
```

### Opción 2: Manual
1. Descarga el binario desde: https://github.com/grafana/k6/releases
2. Extrae el archivo a `C:\k6\`
3. Agrega la carpeta al PATH del sistema:
```powershell
   set PATH=%PATH%;C:\k6
```

---

## INSTRUCCIONES DE EJECUCIÓN

1. **Descargar el proyecto:**

**Opción 1:** Descarga manual
- Hacer clic en `<> Code` → Pestaña `Local` → `Download ZIP`

**Opción 2:** Ejecutar con Codespaces
- Hacer clic en `<> Code` → Pestaña `Codespaces`


2. **Ejecutar la prueba:**
En Windows (PowerShell o Terminal de VS Code), navegar a la ruta de la carpeta donde está el proyecto y ejecutar el siguiente comando:

```powershell
   k6 run scripts\login_test.js
```

3. **Generar resumen de resultados:**
```powershell
   k6 run scripts\login_test.js > textSummary.txt
```

---

## ESTRUCTURA DEL PROYECTO
```
EJERCICIO1_PERFORMANCE-K6/
├── data/
│   └── users.csv                  # Credenciales de prueba
├── scripts/
│   └── login_test.js              # Script principal de K6
├── pruebas-de-ejecucion/          # Capturas de evidencias
├── textSummary.txt                # Resultados de la ejecución
├── conclusiones.txt               # Análisis técnico del ejercicio
└── README.md                      # Este archivo
```

---

## CONFIGURACIÓN DE LA PRUEBA

- **Duración total:** 3 minutos
- **Etapa 1 (30s):** Ramp-up de 0 a 20 VUs
- **Etapa 2 (2m):** Carga sostenida con 40 VUs
- **Etapa 3 (30s):** Ramp-down de 40 a 0 VUs

**Umbrales definidos:**
- TPS: ≥ 20 req/s
- Tiempo de respuesta p95: < 1500 ms
- Tasa de error: < 3%

---

## RESULTADOS OBTENIDOS

- ✅ TPS alcanzado: **29.06 req/s**
- ✅ Tiempo de respuesta p95: **381.88 ms**
- ✅ Tasa de error: **0%**
- ✅ Total de peticiones: **5,255**
- ✅ Checks exitosos: **100%**

---

## DATOS DE PRUEBA

Los usuarios utilizados están en `data/users.csv`:
```csv
user,passwd
donero,ewedon
kevinryan,kev02937@
johnd,m38rmF$
derek,jklg*_56
mor_2314,83r5^_
```

---

## NOTAS IMPORTANTES

- El endpoint probado: https://fakestoreapi.com/auth/login
- El servidor responde con código **HTTP 201** (Created) en lugar de 200
- Todos los usuarios del CSV fueron validados correctamente
- El script ajusta el sleep a 0.5s para alcanzar el TPS requerido

---

## TECNOLOGÍAS UTILIZADAS

- K6 v1.5.0
- JavaScript ES6
- FakeStoreAPI

---

