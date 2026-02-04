<p align="center">
  <img src="https://nutuk.io/logo.png" alt="Nutuk Logo" width="200" />
</p>

<h1 align="center">nutuk.io</h1>

<p align="center">
  <strong>Yüksek kaliteli metin-ses dönüşümü (TTS) platformu</strong>
</p>

<p align="center">
  <a href="https://nutuk.io">Website</a> •
  <a href="https://nutuk.io/docs">API Docs</a> •
  <a href="https://nutuk.io/studio">Studio</a>
</p>

---

## nutuk.io Nedir?

Nutuk, Dil metinlerini doğal ve akıcı seslere dönüştüren modern bir TTS (Text-to-Speech) platformudur. Chatterbox TTS modeli üzerine inşa edilmiş olup, yüksek kaliteli ses klonlama ve çoklu dil desteği sunar.

### Özellikler

- **Doğal Türkçe Seslendirme** - Türkçe fonetik yapısına optimize edilmiş ses üretimi
- **Ses Klonlama** - 20-30 saniyelik ses örneğiyle kendi sesinizi klonlayın
- **SSML Desteği** - Gelişmiş ses kontrolü için SSML markup desteği
- **Çoklu Dil** - Türkçe, İngilizce, Almanca, Fransızca ve 12+ dil desteği
- **Çoklu Format** - MP3, WAV, OGG, FLAC çıktı formatları
- **REST API** - Kolay entegrasyon için modern REST API

---

## Hızlı Başlangıç

### 1. API Anahtarı Alın

[nutuk.io/api-keys](https://nutuk.io/api-keys) sayfasından ücretsiz API anahtarınızı oluşturun.

### 2. İlk İsteğinizi Gönderin

#### cURL

```bash
curl -X POST https://api.nutuk.io/api/v1/tts/generate \
  -H "Content-Type: application/json" \
  -H "X-API-Key: nk_your_api_key_here" \
  -d '{
    "text": "Merhaba dünya! Nutuk ile metinlerinizi sese dönüştürün.",
    "voice_id": "nutuk_ana_ses",
    "language": "tr",
    "format": "mp3"
  }'
```

#### Python

```python
import requests
import base64

response = requests.post(
    'https://api.nutuk.io/api/v1/tts/generate',
    headers={
        'Content-Type': 'application/json',
        'X-API-Key': 'nk_your_api_key_here'
    },
    json={
        'text': 'Merhaba dünya! Nutuk ile metinlerinizi sese dönüştürün.',
        'voice_id': 'nutuk_ana_ses',
        'language': 'tr',
        'format': 'mp3'
    }
)

data = response.json()

# Ses dosyasını kaydet
if 'audio_url' in data:
    audio_base64 = data['audio_url'].split(',')[1]
    audio_bytes = base64.b64decode(audio_base64)

    with open('output.mp3', 'wb') as f:
        f.write(audio_bytes)
```

#### JavaScript / Node.js

```javascript
const response = await fetch('https://api.nutuk.io/api/v1/tts/generate', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'X-API-Key': 'nk_your_api_key_here'
  },
  body: JSON.stringify({
    text: 'Merhaba dünya! Nutuk ile metinlerinizi sese dönüştürün.',
    voice_id: 'nutuk_ana_ses',
    language: 'tr',
    format: 'mp3'
  })
});

const data = await response.json();
console.log(data);
// {
//   "audio_url": "data:audio/mpeg;base64,...",
//   "char_count": 52,
//   "processing_ms": 1523,
//   "format": "mp3"
// }
```

---

## API Referansı

### Base URL

```
https://api.nutuk.io
```

### Authentication

Tüm API isteklerinde `X-API-Key` header'ı gereklidir:

```
X-API-Key: nk_your_api_key_here
```

### Endpoints

| Method | Endpoint | Açıklama |
|--------|----------|----------|
| `POST` | `/api/v1/tts/generate` | Metin → Ses dönüşümü |
| `POST` | `/api/v1/tts/stream` | Streaming TTS |
| `GET` | `/api/public/voices` | Mevcut sesleri listele |

### TTS Generate Parameters

| Parametre | Tip | Default | Açıklama |
|-----------|-----|---------|----------|
| `text` | string | - | Seslendirilecek metin (max 5000 karakter) |
| `voice_id` | string | - | Ses ID'si |
| `language` | string | `"tr"` | Dil kodu (tr, en, de, fr, ...) |
| `format` | string | `"mp3"` | Çıktı formatı (mp3, wav, ogg, flac) |
| `bitrate` | string | `"192k"` | Bitrate (128k, 192k, 256k, 320k) |
| `speed` | float | `1.0` | Konuşma hızı (0.5 - 2.0) |
| `stability` | float | `0.5` | Ses stabilitesi (0.0 - 1.0) |
| `clarity` | float | `0.75` | Telaffuz netliği (0.0 - 1.0) |
| `exaggeration` | float | `0.5` | İfade yoğunluğu (0.0 - 1.0) |
| `speaker_boost` | boolean | `false` | Konuşmacı güçlendirme |

### Desteklenen Diller

| Kod | Dil |
|-----|-----|
| `tr` | Türkçe |
| `en` | İngilizce |
| `de` | Almanca |
| `fr` | Fransızca |
| `es` | İspanyolca |
| `it` | İtalyanca |
| `pt` | Portekizce |
| `nl` | Felemenkçe |
| `pl` | Lehçe |
| `ru` | Rusça |
| `ar` | Arapça |
| `zh-cn` | Çince |
| `ko` | Korece |
| `hi` | Hintçe |
| `hu` | Macarca |
| `cs` | Çekçe |

### Response Format

```json
{
  "audio_url": "data:audio/mpeg;base64,//uQx...",
  "char_count": 52,
  "processing_ms": 1523,
  "quota_used": 52,
  "quota_remaining": 9948,
  "format": "mp3"
}
```

---

## Destek

- **Docs:** [nutuk.io/docs](https://nutuk.io/docs)
- **Email:** support@nutuk.io
- **GitHub Issues:** [github.com/nutuk-io](https://github.com/nutuk-io)

---

<p align="center">
  <sub>Built with ❤️ in Turkey</sub>
</p>
