# Satis Takip

Windows icin C# / WPF tabanli SATIŞÇIM satis takip ve kasa uygulamasi.

## Kalici veri

SQLite veritabani su konumda tutulur:

```text
C:\Users\Kullanici\AppData\Local\SatisTakip\satis_takip.db
```

Uygulama acilisinda varsayilan yonetici girisi `admin / 051575045` bilgisidir.

Uygulamada kalici olarak urun/stok, satis, iade, gider, musteri/veresiye, tahsilat, kullanici ve stok hareketi kayitlari bulunur. Sol menudeki veritabani yedekleme ve geri yukleme secenekleri kullanilabilir.

Urunlerde kritik stok esigi ayarlanabilir (varsayilan 5); bu esik ve altindaki urunler `Kritik stok` ekraninda listelenir. Stok girisleri, satislar, iadeler ve elle yapilan stok duzeltmeleri hareket gecmisine kullanici bilgisiyle kaydedilir.

`Satış Raporları` ekraninda tarih araligina gore net satis, maliyet, brut kar ve adet bazinda en cok satilan urunler goruntulenir. Karma odeme tutarlari nakit ve kart olarak ayri saklanir, satis gecmisi ve gun sonu raporunda da bu paylar ayri gosterilir. Yonetici `Kullanici yonetimi` ekranindan yonetici ve kasiyer hesaplari olusturabilir. Kasiyer kasa, musteri/veresiye ve yalnizca goruntulenebilir kritik stok uyarilarina erisebilir.

## Kurulum ve guncelleme

Kurulum dosyasi `setup-output/SATISCIM-Setup-1.0.0.exe` konumundadir. Yeni setup ayni `AppId` ile derlendigi icin eski uygulamanin uzerine guncelleme yapar; kullanici veritabani `AppData\Local\SatisTakip` altinda kaldigi icin silinmez.

Otomatik guncelleme icin sonraki adim, yeni setup dosyalarinin yayinlanacagi web veya GitHub Releases adresini belirlemektir. Bu adres verildiginde uygulamaya surum manifesti kontrolu eklenebilir.

## Calistirma

```powershell
cd SatisTakip
dotnet run
```

## Excel aktarim formati

Ilk sayfanin ilk satiri baslik olarak atlanir. Sutunlar su sirada olmali:

1. Barkod
2. Urun adi
3. Kategori
4. Satis fiyati
5. Alis maliyeti
6. Stok miktari (istege bagli)
7. Kritik stok esigi (istege bagli, varsayilan 5)

Ornek:

| Barkod | Urun adi | Kategori | Satis fiyati | Alis maliyeti | Stok | Kritik stok esigi |
|---|---|---|---:|---:|---:|---:|
| 1001 | Tam Yagli Sut | Sut Urunleri | 32,50 | 24,00 | 12 | 5 |

## Release cikti

```powershell
dotnet publish SatisTakip\SatisTakip.csproj -c Release -r win-x64 --self-contained false -o publish
```

Gun sonu ekraninda toplam ciro, urun maliyeti, brut kar, toplam gider ve net kar gorulur. Rapor penceresindeki `Yazdir` dugmesiyle yaziciya aktarilabilir. Urun, satis ve stok hareketleri SQLite veritabaninda kalici olarak saklanir.
