# labbayk-modelos

Archivos públicos que descarga la app **Labbayk** cuando el usuario los necesita, para no inflar el instalador.
Aquí no hay nada privado: ni claves, ni datos de usuarios.

| Carpeta | Qué es | Origen y licencia |
|---|---|---|
| `mushaf-hafs-v4/` | Letras por página del Mushaf de Medina (riwaya de Hafs) con colores de tajweed, 604 archivos `pN.woff2` (COLRv1). | Complejo del Rey Fahd para la Impresión del Noble Corán (KFGQPC), versión QPC V4 Tajweed (impresión de 1441 H), tal como la publica la Quranic Universal Library (qul.tarteel.ai). Sin modificar. |
| `tiempos/afasy/` | Tiempos palabra a palabra (ms) de la recitación de Mishary Alafasy, una sura por archivo, para resaltar la palabra que suena. | API pública de Quran.com (audio de quranicaudio.com). |
| `recitacion/` | (más adelante) modelos de reconocimiento de recitación. | Se indicará con cada modelo. |

La app comprueba la integridad de cada archivo con su SHA-256 antes de usarlo.
