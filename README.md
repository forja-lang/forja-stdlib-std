# forja-stdlib-std

Librería estándar de **Forja (fa)**.

Proporciona módulos esenciales para entrada/salida, matemáticas, texto, colecciones, concurrencia, JSON, hashing, redes y más.

## Uso

```fa
importar "std/io"
importar "std/matematica"
importar "std/texto"
```

## Módulos incluidos

| Módulo | Descripción | Funciones principales |
|---|---|---|
| [`io`](io.fa) | Entrada/Salida por consola | `imprimir()`, `imprimir_sin_salto()`, `leer_linea()`, `esperar_tecla()` |
| [`matematica`](matematica.fa) | Operaciones matemáticas | `abs()`, `potencia()`, `raiz_cuadrada()`, `seno()`, `coseno()`, `aleatorio()`, `max()`, `min()` |
| [`texto`](texto.fa) | Manipulación de strings | `longitud()`, `a_mayusculas()`, `a_minusculas()`, `recortar()`, `contiene()`, `reemplazar()`, `dividir()`, `invertir()` |
| [`colecciones`](colecciones.fa) | Operaciones con arreglos | `longitud()`, `contiene()`, `invertir()`, `ordenar()`, `map()`, `filtrar()`, `reducir()`, `unico()`, `mezclar()` |
| [`json`](json.fa) | Parseo y generación JSON | `json_parsear()`, `json_stringificar()` |
| [`resultado`](resultado.fa) | Helpers para Resultado/Opcion | `es_ok()`, `es_error()`, `obtener()`, `obtener_o_default()` |
| [`fecha`](fecha.fa) | Fechas y tiempos | `fecha_actual()`, `timestamp()`, `formatear_fecha()`, `diferencia_dias()` |
| [`hash`](hash.fa) | Hashing criptográfico | `hash_sha256()`, `hash_md5()` |
| [`concurrencia`](concurrencia.fa) | Concurrencia simplificada | `hilo()`, `canal()`, `enviar()`, `recibir()`, `seleccionar()` |
| [`codificacion`](codificacion.fa) | Codificación/Decodificación | `base64_codificar()`, `base64_decodificar()`, `url_codificar()`, `url_decodificar()` |
| [`sistema`](sistema.fa) | Interacción con el SO | `ejecutar_comando()`, `variable_entorno()`, `plataforma()` |
| [`archivo`](archivo.fa) | Operaciones con archivos | `leer_archivo()`, `escribir_archivo()`, `existe_archivo()`, `eliminar_archivo()`, `copiar_archivo()` |
| [`sockets`](sockets.fa) | Sockets TCP/UDP | `conectar_tcp()`, `escuchar_tcp()`, `enviar()`, `recibir()` |
| [`servidor_web`](servidor_web.fa) | Servidor HTTP básico | `servidor_http()`, `ruta()`, `respuesta()` |
| [`cliente_http`](cliente_http.fa) | Cliente HTTP | `http_get()`, `http_post()`, `http_put()`, `http_delete()` |
| [`servidor_h2`](servidor_h2.fa) | Servidor HTTP/2 | `servidor_h2()`, `ruta_h2()`, `respuesta_h2()` |
| [`cliente_h2`](cliente_h2.fa) | Cliente HTTP/2 | `h2_get()`, `h2_post()` |
| [`websocket`](websocket.fa) | WebSocket | `ws_conectar()`, `ws_enviar()`, `ws_recibir()` |
| [`prueba`](prueba.fa) | Testing | `assert()`, `assert_igual()`, `assert_diferente()`, `assert_verdadero()`, `assert_falso()` |
| [`aleatorio`](aleatorio.fa) | Aleatoriedad | `aleatorio_entero()`, `aleatorio_decimal()`, `aleatorio_rango()` |
| [`sqlite`](sqlite.fa) | Base de datos SQLite | `abrir()`, `cerrar()`, `ejecutar()`, `consultar()`, `consultar_una()`, `ejecutar_con_parametros()`, `consultar_con_parametros()`, `ultimo_id()`, `transaccion()`, `confirmar()`, `deshacer()`, `tablas()`, `columnas()` |

## Ejemplo

```fa
importar "std/io"
importar "std/matematica"

funcion main() {
    variable num = 16
    imprimir("La raíz cuadrada de " + num + " es " + raiz_cuadrada(num))
}
```
