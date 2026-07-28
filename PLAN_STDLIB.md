# Plan Integral de stdlib Forja

## Prioridades

### Fase 1 — Sin nuevas funciones nativas (pure Forja + natives existentes)
| Módulo | Dependencias |
|--------|-------------|
| env.fa | _sistema_variable_entorno (existente) |
| arg.fa | _sistema_argumentos (existente) |

### Fase 2 — Necesitan nuevas natives simples
| Módulo | Natives requeridas |
|--------|-------------------|
| ruta.fa | _path_normalizar, _path_extension, _path_unir, _path_absoluto, _path_dir_padre |
| proceso.fa | _proceso_ejecutar, _proceso_stdout, _proceso_stderr, _proceso_stdin, _proceso_esperar, _proceso_codigo_salida, _proceso_pipe |
| temporizador.fa | _timer_nuevo, _timer_esperar, _timer_cancelar, _timer_duracion_ms |
| binario.fa | _binario_empaquetar, _binario_desempaquetar, _binario_tamano, _binario_a_hex, _binario_desde_hex |
| csv.fa | _csv_parsear_linea, _csv_generar_linea |
| url.fa | _url_parsear, _url_construir |

### Fase 3 — Necesitan natives medianas
| Módulo | Natives requeridas |
|--------|-------------------|
| atomicos.fa | _atomico_entero_nuevo, _atomico_cargar, _atomico_almacenar, _atomico_intercambiar, _atomico_sumar, _atomico_booleano_nuevo |
| canales.fa | _canal_nuevo, _canal_enviar, _canal_recibir, _canal_cerrar (complementa concurrencia.fa) |
| señales.fa | _senal_registrar, _senal_esperar, _senal_enviar |
| log.fa | _log_escribir, _log_configurar |
| perfilado.fa | _perfilado_iniciar, _perfilado_detener, _perfilado_resultado, _perfilado_frame_time |

### Fase 4 — Necesitan natives complejas o externas
| Módulo | Natives requeridas |
|--------|-------------------|
| compresion.fa | _zstd_comprimir, _zstd_descomprimir, _gzip_comprimir, _gzip_descomprimir |
| toml.fa | _toml_parsear_texto, _toml_generar_texto |
| tls.fa | _tls_conectar, _tls_mano, _tls_enviar, _tls_recibir, _tls_cerrar |
| ffi.fa | _ffi_cargar_libreria, _ffi_obtener_funcion, _ffi_llamar, _ffi_liberar |

## Arquitectura

Cada módulo sigue el patrón:

```
# módulo: nombre
# Descripción
# Uso: importar "std/nombre"

importar "std/resultado"

clase ErrorModulo {
    mensaje: Texto
    codigo: Entero
    constructor(mensaje: Texto, codigo: Entero) {
        este.mensaje = mensaje
        este.codigo = codigo
    }
}

# Validación en Forja + delegación a native _prefijada
funcion operacion(args) -> Resultado<Tipo, ErrorModulo> {
    si (validación falla) {
        retornar Error(nuevo ErrorModulo("mensaje", codigo))
    }
    retornar Ok(_operacion_nativa(args))
}
```

## Registro de Natives (Rust side)

Cada nueva función nativa se registra en `NativeRegistry::new()`:
```rust
reg.registrar_ruta();
reg.registrar_proceso();
// etc.
```

Y cada `registrar_*` llama a `self.registrar("_nombre", native_fn)`.
