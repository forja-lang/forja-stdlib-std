# forja-stdlib-std

Librería estándar de **Forja (fa)** — 45+ módulos para I/O, matemáticas, texto, colecciones, redes, criptografía, concurrencia, formatos de datos, sistema y más.

## Uso

```fa
importar std/io
importar std/matematica
importar std/texto
```

Cada función se usa directamente tras importar el módulo:
```fa
importar std/io
importar std/ruta

funcion main() {
    imprimir("Archivo: " + ruta.nombre_archivo("/usr/local/bin/forja"))
}
```

## Módulos incluidos

### Herramientas básicas

| Módulo | Descripción | Funciones principales |
|--------|------------|----------------------|
| [`io`](io.fa) | Entrada/Salida por consola | `imprimir(mensaje)`, `imprimir_sin_salto(mensaje)`, `imprimir_varios(arr)`, `imprimir_linea()`, `pedir_texto(mensaje)`, `pedir_numero(mensaje)`, `mostrar_error(mensaje)`, `mostrar_advertencia(mensaje)`, `mostrar_info(mensaje)` |
| [`texto`](texto.fa) | Manipulación de strings | `longitud_texto(s)`, `a_mayusculas(s)`, `a_minusculas(s)`, `capitalizar(s)`, `invertir(s)`, `contar_ocurrencias(texto, patron)`, `esta_vacio(s)`, `repetir_texto(s, veces)`, `contiene(texto, patron)`, `reemplazar(texto, original, remplazo)`, `recortar(s)` |
| [`matematica`](matematica.fa) | Funciones matemáticas | `absoluto(x)`, `maximo(a, b)`, `minimo(a, b)`, `limitar(valor, minimo, maximo)`, `potencia(base, exp)`, `factorial(n)`, `es_par(n)`, `es_impar(n)`, `redondear(x)`, `suma_array(arr)`, `promedio(arr)`, `mcd(a, b)`, `mcm(a, b)`, `exacto_desde_entero(n)`, `exacto_desde_decimal(d)`, `exacto_desde_texto(t)`, `redondear_exacto(e, decimales)`, `exacto_absoluto(e)`, `exacto_potencia(base, exp)` |
| [`colecciones`](colecciones.fa) | Operaciones funcionales sobre arreglos y mapas | `mapa(arr, callback)`, `filtrar(arr, callback)`, `reducir(arr, callback, valor_inicial)`, `encontrar(arr, callback)`, `alguno(arr, callback)`, `todos(arr, callback)`, `ordenar(arr)`, `aplanar(arr)`, `unico(arr)`, `invertir(arr)`, `segmento(arr, inicio, fin)`, `claves(mapa)`, `valores(mapa)`, `pares(mapa)`, `fusionar(mapa1, mapa2)`, `filtrar_claves(mapa, callback)` |
| [`resultado`](resultado.fa) | Constructores de `Resultado<T,E>` y `Opcion<T>` | `Ok(valor)`, `Error(mensaje)`, `Alguno(valor)` / `Algo(valor)` / `Ninguno()` |
| [`prueba`](prueba.fa) | Aserciones para tests | `asegurar(condicion)`, `error_verificacion(mensaje)` |
| [`ansi`](ansi.fa) | Secuencias ANSI para terminal: colores, cursor, pantalla | `limpiar_pantalla()`, `mover_cursor(fila, col)`, `guardar_cursor()`, `restaurar_cursor()`, `mostrar_cursor(visible)`, `subir(n)`, `bajar(n)`, `adelante(n)`, `atras(n)`, `rojo(texto)`, `verde(texto)`, `azul(texto)`, `cyan(texto)`, `magenta(texto)`, `amarillo(texto)`, `negro(texto)`, `blanco(texto)`, `color(r,g,b,texto)`, `titulo(texto)`, `beep()` y variantes `*_fondo()`, más `limpiar_linea()`, `limpiar_desde_cursor()` |
| [`tui`](tui.fa) | Terminal UI interactiva | `raw_mode(activar)`, `leer_tecla()`, `tamano_terminal()` |
| [`arg`](arg.fa) | Parser de banderas CLI | `parser(nombre_app, descripcion) → ArgParser`. Métodos de resultado: `presente(nombre)`, `texto(nombre)`, `entero(nombre, default)`, `booleano(nombre)`, `posicional(indice)`, `mostrar_ayuda()` |

### Sistema y entorno

| Módulo | Descripción | Funciones principales |
|--------|------------|----------------------|
| [`sistema`](sistema.fa) | Sistema operativo y entorno | `argumentos() → Arreglo<Texto>`, `variable_entorno(nombre) → Opcion<Texto>`, `salir(codigo)`, `directorio_actual() → Resultado<Texto, ErrorSistema>`, `tiempo_ms() → Entero`, `sistema_operativo() → Texto`, `version_forja() → Texto` |
| [`env`](env.fa) | Variables de entorno avanzadas | `obtener(nombre) → Opcion<Texto>`, `obtener_entero(nombre, default) → Entero`, `obtener_booleano(nombre, default) → Booleano`, `establecer(nombre, valor)`, `todos() → Arreglo<(Texto,Texto)>`, `cargar_archivo(ruta)`, `expandir(texto) → Texto` |
| [`ruta`](ruta.fa) | Manipulación de rutas de archivos | `normalizar(ruta) → Texto`, `unir(base, parte) → Texto`, `extension(archivo) → Texto`, `sin_extension(archivo) → Texto`, `nombre_archivo(ruta) → Texto`, `dir_padre(ruta) → Texto`, `absoluta(ruta) → Resultado<Texto, ErrorRuta>`, `es_absoluta(ruta) → Booleano`, `sep() → Texto` |
| [`archivo`](archivo.fa) | Operaciones con archivos y directorios | `leer_archivo(ruta)`, `escribir_archivo(ruta, contenido)`, `existe_archivo(ruta) → Booleano`, `eliminar_archivo(ruta)`, `copiar_archivo(origen, destino)`, `mover_archivo(origen, destino)`, `tamano_archivo(ruta)`, `crear_directorio(ruta)`, `eliminar_directorio(ruta)`, `listar_directorio(ruta)`, `info_archivo(ruta)`, `es_directorio(ruta) → Booleano` |
| [`proceso`](proceso.fa) | Lanzar subprocesos | `ejecutar(comando) → Resultado<SalidaProceso, ErrorProceso>`, `ejecutar_con_stdin(comando, entrada)`, `ejecutar_en_dir(comando, dir)` |
| [`temporizador`](temporizador.fa) | Timers, sleeps, mediciones | `nuevo(duracion_ms) → Timer`, `dormir(ms)`, `medir(inicio) → Medicion` |
| [`señales`](señales.fa) | Manejo de señales POSIX | `manejar_sigint(handler)`, `manejar_sigterm(handler)`, `ignorar(senal)`, `enviar(pid, senal)` |

### Formatos de datos

| Módulo | Descripción | Funciones principales |
|--------|------------|----------------------|
| [`json`](json.fa) | Parseo y generación JSON | `parsear(texto)`, `serializar(valor)`, `leer_json(ruta)`, `escribir_json(ruta, valor)` |
| [`csv`](csv.fa) | Parseo y generación CSV | `parsear(texto) → Resultado<Arreglo<Arreglo<Texto>>, ErrorCsv>`, `parsear_con_cabeceras(texto) → Resultado<Arreglo<Mapa<Texto,Texto>>, ErrorCsv>`, `generar(filas) → Texto`, `generar_con_cabeceras(cabeceras, filas) → Texto` |
| [`toml`](toml.fa) | Parseo y generación TOML | `parsear(texto) → Resultado<Mapa<Texto>, ErrorToml>`, `generar(mapa) → Resultado<Texto, ErrorToml>` |
| [`codificacion`](codificacion.fa) | Base64, URL y Hex | `base64_codificar(texto) → Texto`, `base64_decodificar(texto) → Resultado`, `hex_codificar(texto) → Texto`, `hex_decodificar(hex) → Resultado`, `url_codificar(texto) → Texto`, `url_decodificar(texto) → Resultado` |
| [`hex`](hex.fa) | Conversión entre bases numéricas y hex | `a_decimal(hex)`, `a_binario(hex)`, `a_octal(hex)`, `decimal_a_hex(n)`, `decimal_a_binario(n)`, `decimal_a_octal(n)`, `binario_a_decimal(bin)`, `binario_a_hex(bin)`, `texto_a_hex(texto)`, `hex_a_texto(hex)`, `y_bits(a,b)`, `o_bits(a,b)`, `xor_bits(a,b)`, `complemento(a)`, `desplazar_izquierda(a,n)`, `desplazar_derecha(a,n)`, `sumar(a,b)`, `restar(a,b)`, `multiplicar(a,b)`, `dividir(a,b)`, `modulo(a,b)`, `potencia(a,exp)`, `mcd(a,b)`, `mcm(a,b)`, `medir(a)`, `iguales(a,b)`, `mayor_que(a,b)`, `menor_que(a,b)`, `validar_hex(s)`, `validar_binario(s)`, `validar_octal(s)`, `base_n_a_decimal(numero, base)`, `decimal_a_base_n(n, base)` |
| [`url`](url.fa) | Parseo y construcción de URLs | `parsear(url) → Resultado<URL, ErrorUrl>`, `construir(esquema, host, puerto, ruta, query) → Texto`, `codificar(texto) → Texto`, `decodificar(texto) → Texto`, `query_parsear(query) → Resultado` |
| [`binario`](binario.fa) | Empaquetado binario (endianness) | `empaquetar(formato, valores) → Resultado<Texto, ErrorBinario>`, `desempaquetar(formato, datos) → Resultado<Arreglo<Entero>, ErrorBinario>`, `a_hex(datos) → Texto`, `desde_hex(hex) → Resultado`, `tamano(formato) → Entero` |

### Criptografía y hash

| Módulo | Descripción | Funciones principales |
|--------|------------|----------------------|
| [`hash`](hash.fa) | Hashing criptográfico | `sha1(datos) → Resultado<Texto, ErrorHash>`, `sha224(datos)`, `sha256(datos)`, `sha384(datos)`, `sha512(datos)`, `hmac_sha256(clave, datos)` |
| [`crypto`](crypto.fa) | Criptografía: cifrado, AEAD, contraseñas | `bytes_aleatorios(n) → Resultado`, `sal(n)`, `igualdad_tiempo_constante(a,b) → Booleano`, `aes_encriptar(clave, iv, datos)`, `aes_desencriptar(clave, iv, cifrado)`, `aes_gcm_encriptar(clave, nonce, datos, ad)`, `aes_gcm_desencriptar(clave, nonce, cifrado, ad)`, `chacha20(clave, nonce, datos)`, `aead_encriptar(clave, nonce, datos, ad)`, `aead_desencriptar(clave, nonce, cifrado, ad)`, `scrypt(password, sal, n, r, longitud)`, `pbkdf2(password, sal, iteraciones, longitud)`, `hash_password(password)`, `verificar_password(password, hash) → Booleano` |

### Concurrencia y atómicos

| Módulo | Descripción | Funciones principales |
|--------|------------|----------------------|
| [`concurrencia`](concurrencia.fa) | Patrones de concurrencia alto nivel | `pool_trabajadores(num, procesar)`, `paralelo_for(inicio, fin, workers, callback)`, `mapa_paralelo(arr, workers, callback)`, `con_limite_tiempo(ms, callback)`, `reintentar(max_intentos, callback)` |
| [`atomicos`](atomicos.fa) | Primitivas lock-free | `entero_nuevo(valor_inicial) → ptr`, `entero_cargar(ptr) → Entero`, `entero_almacenar(ptr, valor)`, `entero_sumar(ptr, delta) → Entero`, `entero_intercambiar(ptr, valor) → Entero`, `entero_comparar_intercambiar(ptr, esperado, nuevo) → Booleano`, `booleano_nuevo(valor_inicial) → ptr`, `booleano_cargar(ptr) → Booleano`, `booleano_almacenar(ptr, valor)` |
| [`mmap`](mmap.fa) | Memory-Mapped Files | `abrir(ruta, offset, longitud, modo)`, `cerrar(handle)`, `leer(handle, offset, longitud)`, `escribir(handle, offset, datos)`, `sincronizar(handle)`, `tamano_archivo(ruta)`, `tamano_pagina() → Entero` |

### Redes y comunicación

| Módulo | Descripción | Funciones principales |
|--------|------------|----------------------|
| [`sockets`](sockets.fa) | Sockets TCP/UDP nativos | `conectar(direccion, puerto)`, `conectar_con_timeout(direccion, puerto, timeout_ms)`, `enviar(socket, datos)`, `recibir(socket, tamano)`, `recibir_simple(socket)`, `cerrar(socket)`, `escuchar(puerto)`, `escuchar_con_backlog(puerto, backlog)`, `aceptar(servidor)`, `udp_escuchar(puerto)`, `udp_enviar(socket, datos, direccion, puerto)`, `udp_recibir(socket, tamano)`, `udp_recibir_simple(socket)`, `es_valido(socket) → Booleano`, `obtener_info(socket)`, `direccion_local(socket)`, `direccion_remota(socket)`, `configurar_timeout(socket, segundos)` |
| [`red`](red.fa) | DNS, DoH, ICMP Ping, MAC | `validar_ipv4(ip) → Booleano`, `validar_ipv6(ip) → Booleano`, `validar_mac(mac) → Booleano`, `dns_resolver(host)`, `dns_resolver_tipo(host, tipo)`, `doh_resolver(host, servidor_doh)`, `ping(host)`, `interfaces()` |
| [`servidor_web`](servidor_web.fa) | Servidor HTTP/1.1 | `obtener(servidor, ruta, manejador)`, `enviar(servidor, ruta, manejador)`, `actualizar(servidor, ruta, manejador)`, `eliminar(servidor, ruta, manejador)`, `usar(servidor, middleware)`, `servir_estaticos(servidor, prefijo, dir)`, `habilitar_cors(servidor)`, `fijar_max_cuerpo(servidor, max_bytes)`, `iniciar(servidor)`, `detener(servidor)`, `html(respuesta, contenido)`, `texto_plano(respuesta, contenido)`, `redirigir(respuesta, url)`, `error_respuesta(respuesta, codigo)` |
| [`cliente_http`](cliente_http.fa) | Cliente HTTP/1.1 | `obtener(url)`, `obtener_con_opciones(url, opciones)`, `enviar(url, cuerpo)`, `enviar_con_opciones(url, cuerpo, opciones)`, `actualizar(url, cuerpo)`, `eliminar(url)`, `modificar_parcial(url, cuerpo)` |
| [`servidor_h2`](servidor_h2.fa) | Servidor HTTP/2 (h2c) | `obtener(servidor, ruta, manejador)`, `enviar(servidor, ruta, manejador)`, `actualizar(servidor, ruta, manejador)`, `eliminar(servidor, ruta, manejador)`, `usar(servidor, middleware)`, `iniciar(servidor)`, `detener(servidor)` |
| [`cliente_h2`](cliente_h2.fa) | Cliente HTTP/2 (h2c) | `obtener(url)`, `obtener_con_opciones(url, opciones)`, `enviar(url, cuerpo)`, `enviar_con_opciones(url, cuerpo, opciones)`, `actualizar(url, cuerpo)`, `eliminar(url)`, `modificar_parcial(url, cuerpo)` |
| [`cliente_h3`](cliente_h3.fa) | Cliente HTTP/3 (QUIC) | `h3_obtener(url) → Resultado<RespuestaH3, Texto>`, `h3_enviar(url, cuerpo)`, `h3_solicitud(metodo, url, cabeceras, cuerpo)` |
| [`quic`](quic.fa) | Transporte QUIC (RFC 9000) | `quic_conectar(host, puerto) → Resultado<ConexionQUIC, Texto>`. Métodos: `abrir_stream()`, `enviar(datos)`, `recibir(max_bytes)`, `cerrar()` |
| [`websocket`](websocket.fa) | WebSocket (RFC 6455) | `aceptar(socket, cabeceras)`, `conectar(url)`. Métodos de conexión: `enviar_texto(mensaje)`, `enviar_binario(datos)`, `recibir_texto()`, `enviar_ping()`, `enviar_pong()`, `cerrar(mensaje)`, `esta_abierta() → Booleano` |
| [`tls`](tls.fa) | TLS/SSL | `conectar(host, puerto) → Resultado<Entero, ErrorTLS>`, `conectar_con_pin(host, puerto, pin_sha256)`, `enviar(conn, datos)`, `recibir(conn, tamano)`, `cerrar(conn)` |

### Bases de datos

| Módulo | Descripción | Funciones principales |
|--------|------------|----------------------|
| [`sqlite`](sqlite.fa) | Base de datos SQLite | `abrir(ruta)`, `cerrar(conexion)`, `ejecutar(conexion, sql)`, `consultar(conexion, sql)`, `consultar_una(conexion, sql)`, `ejecutar_con_parametros(conexion, sql, valores)`, `consultar_con_parametros(conexion, sql, valores)`, `ultimo_id(conexion)`, `transaccion(conexion)`, `confirmar(conexion)`, `deshacer(conexion)`, `tablas(conexion)`, `columnas(conexion, tabla)`, `ejecutar_simple(conexion, sql)` |

### Aleatoriedad y logging

| Módulo | Descripción | Funciones principales |
|--------|------------|----------------------|
| [`aleatorio`](aleatorio.fa) | Números aleatorios (xorshift32) | `semilla(valor)`, `entero(max) → Entero`, `decimal() → Decimal`, `elemento(arr)`, `mezclar(arr)` |
| [`log`](log.fa) | Logging estructurado | `configurar(nivel, archivo)`, `depurar(mensaje)`, `informacion(mensaje)`, `advertencia(mensaje)`, `error(mensaje)`, `critico(mensaje)` |
| [`perfilado`](perfilado.fa) | Benchmarks y profiling | `iniciar(etiqueta)`, `detener(etiqueta) → Resultado<ReportePerfilado, ErrorPerfilado>`, `medir(etiqueta, iteraciones, bloque)`, `reportes() → Arreglo<ReportePerfilado>` |

### Fechas

| Módulo | Descripción | Funciones principales |
|--------|------------|----------------------|
| [`fecha`](fecha.fa) | Fechas y horas | `ahora() → Texto`, `hoy() → Texto`, `hora_actual() → Texto`, `formatear(ts, formato) → Texto`, `parsear(texto, formato) → Resultado<Entero, ErrorFecha>`, `formato_largo(ts) → Texto`, `formato_corto(ts) → Texto` |

### Interoperabilidad

| Módulo | Descripción | Funciones principales |
|--------|------------|----------------------|
| [`ffi`](ffi.fa) | Foreign Function Interface | `cargar_libreria(ruta) → Resultado<Entero, ErrorFFI>`, `obtener_funcion(lib, nombre)`, `llamar_entero(fn_ptr, args)`, `llamar_texto(fn_ptr, args)`, `liberar(lib)` |

## Ejemplo

```fa
importar std/io
importar std/ruta
importar std/env
importar std/perfilado

funcion main() {
    perfilado.iniciar("main")

    variable ruta_abs = ruta.absoluta(".")
    imprimir("Directorio: " + ruta_abs)

    variable usuario_opt = env.obtener("USER")
    coincidir (usuario_opt) {
        caso Alguno(v) -> { imprimir("Usuario: " + v) }
        caso Ninguno ->   { imprimir("Usuario: desconocido") }
    }

    variable reporte = perfilado.detener("main")
    imprimir("Tiempo: " + reporte.tiempo_total_ms + "ms")
}
```
