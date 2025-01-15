# Haber API Kullanım Kılavuzu

Bu kılavuz, `https://ogene.net/api/haber/` adresindeki API'nin nasıl kullanılacağını açıklar. API'ye erişim için geçerli bir Bearer Token gereklidir. Lütfen aşağıdaki adımları izleyerek API'yi kullanın.

---

## Erişim Koşulları

API'ye yapılan her istekte aşağıdaki Bearer Token başlığını eklemeniz gereklidir:

```
Authorization: Bearer a40d318d6b6ba843749422827f23d491453d3253a5358dba70e25d73af9b0505
```

Eğer token doğru değilse, sunucu 401 Unauthorized hatası döndürecektir.

---

## Kullanım

### İstek Formatı

API'ye `POST` yöntemiyle istek yapılmalıdır. İsteklerde şu alanlar gönderilir:

- **type**: İşlem türünü belirtir. (örneğin: `kategorihaberlistele`)
- **keys**: İşlemle ilgili parametreleri içerir (JSON formatında gönderilmelidir).

### Örnek İstek

#### cURL ile Örnek
```bash
curl -X POST https://ogene.net/api/haber/index.php \
-H "Authorization: Bearer a40d318d6b6ba843749422827f23d491453d3253a5358dba70e25d73af9b0505" \
-d "type=kategorihaberlistele&keys={\"KategoriID\":1}"
```

#### Yanıt
Başarılı bir istek sonucunda, sunucudan JSON formatında yanıt alınır:
```json
{
  "Sonuc": true,
  "Mesaj": "İşleminiz başarılı şekilde gerçekleşmiştir",
  "Data": [
    {
      "ID": 215266,
      "Kategori": {
        "Adi": "GÜNDEM",
        "SeoUrl": "Gundem",
        "ID": 1
      },
      "Baslik": "OgeneNet API Servisi Yayınlandı.",
      "Ozet": "OgeneNet API servislerine bir yenisini daha ekledi.",
      "OkunmaSayisi": 9,
      "YayinTarihi": "2025-01-15T09:23:21",
      "SeoUrl": "ogenenet_api_servisi_yayinladi",
      "Dosyalar": [
        {
          "Adi": "215266.jpeg",
          "ID": 428579
        },
        {
          "Adi": "215266.jpeg",
          "ID": 428578
        }
      ]
    }
  ]
}
```

---

## Desteklenen İşlemler ve Kategoriler

### İşlemler

1. **Öne Çıkanlar**
   - **type**: `onecikanlar`
   - **keys**: `{"Manset":1}`

2. **Ankara Haberleri**
   - **type**: `yerelhaber`
   - **keys**: `{"KategoriID":5}`

3. **Slider Haber**
   - **type**: `gundemsliderhaber`
   - **keys**: `{"Manset":1}`

4. **Son Dakika Haberler**
   - **type**: `sondakikahaber`
   - **keys**: `{"FlashHaber":1}`

5. **Sağ Manşet**
   - **type**: `mansetsag`
   - **keys**: `{"Manset":1}`

6. **Manşet Slider**
   - **type**: `mansetslider`
   - **keys**: `{"Manset":1}`

7. **Kategoriye Göre Haberler**
   - **type**: `kategorihaberlistele`
   - **keys**: `{"KategoriID":1}`

8. **Daha Fazla Haber**
   - **type**: `kategorihaberlistele.dahafazla`
   - **keys**: `{"KategoriID":"KATEGORI_ID","SonID":"ISTEKTEN_GELEN_SON_ID_BURAYA"}`

### Kategoriler

| Kategori Adı          | ID  |
|-----------------------|-----|
| Gündem               | 1   |
| Ekonomi              | 2   |
| Yurttan              | 5   |
| Spor                 | 7   |
| Dünya                | 8   |
| Bülten               | 9   |
| Şirket Haberleri     | 10  |

---

## Hata Kodları

- **401 Unauthorized**: Geçersiz veya eksik Bearer Token.
- **400 Bad Request**: Eksik veya hatalı parametreler.
- **500 Internal Server Error**: Sunucu tarafında bir hata oluştu.

---

## İletişim
Herhangi bir sorunla karşılaşırsanız, lütfen destek ekibimize ulaşın:
- **E-posta**: MAİL@ogene.net
- **Web**: [https://ogene.net](https://ogene.net)
