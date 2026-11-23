# labbayk-modelos

Archivos públicos que descarga la app **Labbayk** cuando el usuario los necesita, para no inflar el instalador.
Aquí no hay nada privado: ni claves, ni datos de usuarios.

| Carpeta | Qué es | Origen y licencia |
|---|---|---|
| `mushaf-hafs-v4/` | Letras por página del Mushaf de Medina (riwaya de Hafs) con colores de tajweed, 604 archivos `pN.woff2` (COLRv1). | Complejo del Rey Fahd para la Impresión del Noble Corán (KFGQPC), versión QPC V4 Tajweed (impresión de 1441 H), tal como la publica la Quranic Universal Library (qul.tarteel.ai). Sin modificar. |
| `tiempos/<recitador>/` | Tiempos palabra a palabra (ms) de 9 recitadores de Hafs (afasy, abdulbasit, husary, minshawi, sudais, shuraim, shatri, husary-muallim, dussary), una sura por archivo, para resaltar la palabra que suena. Las pocas palabras sin tiempo se rellenan repartiendo el hueco entre sus vecinas (`informe.json`). | API pública de Quran.com, medidos sobre el audio de quranicaudio.com que usa la app. |
| `recitacion/talqin-warsh-v1.1/` | Modelo que escucha la recitación en el móvil (Zipformer CTC en streaming, 60 sonidos, 25 MB, 8 bits) para seguirla palabra a palabra. | Talqin (huggingface.co/talqin/talqin-stream-warsh, v1.1), Apache 2.0, sin modificar (ver `ORIGEN.txt`). |

La app comprueba la integridad de cada archivo con su SHA-256 antes de usarlo.
