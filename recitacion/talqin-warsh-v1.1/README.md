---
license: apache-2.0
language:
- ar
pipeline_tag: automatic-speech-recognition
library_name: sherpa-onnx
tags:
- quran
- warsh
- streaming
- zipformer
- ctc
- tajweed
---

# Talqin streaming model v1.1 (Warsh)

تلقين: نموذج صغير يسمع تلاوة القرآن الكريم برواية ورش عن نافع مباشرةً على الهاتف، فيتابع القارئ كلمةً كلمة ويعرف موضعه من المصحف.

A small model that hears a Quran recitation (riwayah of Warsh from Nafi') as it comes, on the reciter's own phone. The
Talqin app uses it to follow the reciter word by word and find the ayah, with no server.

- **What it writes:** the recitation's sounds (60 symbols, `tokens.txt`), one every 40 ms, about 0.4 s after they are
  said. Not words: the Talqin app places these sounds in the Quran.
- **Model:** a causal (streaming) Zipformer with CTC, 22.3M parameters. `model.int8.onnx` (25 MB) hears 0.32 s
  slices, 8-bit. The same model, files and sounds as v1.0: it replaces it as it is.
- **Runs with:** [sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx) (`OnlineRecognizer`, `zipformer2Ctc`), on
  Android, iPhone, computers and in the browser (WebAssembly). It runs 2–15 times faster than real time on phones.
- **Accuracy:** 0.8% sound error on 7 reciters it never heard (3,656 clips, 8.45 h); in a simulated home room (echo,
  noise, phone microphone) 4.3%. The app's search places 98.3% of phrases right with it.

## What's new in v1.1

v1.0 taught to hear ordinary home recordings. It was trained further from v1.0 on the same 1,511 hours of 59
reciters, with new effects: a room's echo, higher voices (for women and children), faster reading (up to 1.3x),
another voice behind the reciter, stronger noise, an overdriven microphone, and phrases joined with short pauses.

Sound error through the 8-bit model, the same 200 test clips of reciters neither model trained on:

|       | As recorded | In a room | Fast (1.25x) | Higher voice |
|-------|-------------|-----------|--------------|--------------|
| v1.0  | 1.83%       | 8.91%     | 2.84%        | 2.78%        |
| v1.1  | 0.81%       | 3.64%     | 0.94%        | 1.14%        |

In the Talqin app's own following (whole recitations through the app's tracker), it mishears about half as many
sounds as v1.0, also on a real phone recording, and the marker keeps up much better in a room.

## Files

| File | What it is |
|---|---|
| `model.int8.onnx` | The model (0.32 s slices, 8-bit) |
| `tokens.txt` | Its 60 sounds |
| `manifest.json` | Version, sizes and SHA-256 of the files (the app checks them) |

Each version is a tag: `v1.0`, `v1.1`.

## Use

```python
import sherpa_onnx
rec = sherpa_onnx.OnlineRecognizer.from_zipformer2_ctc(tokens="tokens.txt", model="model.int8.onnx", num_threads=1)
```

## Limits

It follows the recitation; it is not a judge of mistakes (it heard the same Quran text many times in training, so it
partly knows it by heart). Talqin checks mistakes with a larger model on its server. The test rooms and higher voices
are made the same way as the training effects, so real rooms, women and children may gain less than the table shows.

هذا النموذج يعمل بالذكاء الاصطناعي وقد يخطئ، وهو للإعانة فقط ولا يجب الاعتماد عليه 100% أو تقديمه بديلاً عن معلّم متقن ومجاز.

## License

Apache License 2.0. Made by Talqin (https://github.com/TalqinCore).
