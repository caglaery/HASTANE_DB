# HASTANE_DB
# Hastane Veritabanı Yönetim Sistemi

Bu proje, bir hastane yönetim sistemi için veritabanı tasarımı ve uygulamalarını içermektedir. Veritabanı; hastalar, doktorlar, poliklinikler, personel ve randevular gibi temel unsurları kapsayan tablolar ile veri yönetimi işlevlerini optimize eden prosedürler, fonksiyonlar, trigger'lar ve görünümler sunar.

## Proje Hedefleri
- Hastane veritabanı yapısını oluşturmak ve yönetmek.
- Randevu sistemini optimize ederek kolayca sorgulanabilir bir yapı sağlamak.
- Veri güvenliği ve işlem geçmişi için loglama mekanizması geliştirmek.
- Poliklinik bazında randevu analizleri sunmak.

## İçerik
### Tablolar
- **HASTALAR:** Hasta bilgilerini tutar (adı, soyadı, doğum tarihi, cinsiyet, telefon).
- **DOKTORLAR:** Doktor bilgilerini tutar (adı, soyadı, uzmanlık, telefon).
- **POLIKLINIK:** Poliklinik bilgilerini tutar (adı, açıklama).
- **RANDEVU:** Randevu bilgilerini tutar (hasta, doktor, poliklinik, tarih, açıklama).
- **PERSONEL:** Personel bilgilerini tutar (adı, soyadı, departman, telefon).

### Önemli Bileşenler
1. **Stored Procedure:** 
   - Poliklinik bazında randevuları sıralar. Örneğin:
     ```sql
     EXEC PoliklinikRandevularDESC @POLIKLINIK_ID = 1;
     ```
2. **Trigger:**
   - Randevu silindiğinde bilgileri loglar. 
   - **Log Tablosu:** `RANDEVU_LOG` tablosunda silinen randevular kayıt altına alınır.
3. **Fonksiyon:**
   - Belirli bir hastanın toplam randevu sayısını döner.
     ```sql
     SELECT dbo.fn_HastaRandevuSayisi(2);
     ```
4. **View:**
   - Tüm randevuların detaylı listesini sunar.
     ```sql
     SELECT * FROM vw_Tum_Randevular;
     ```
5. **Transaction Yönetimi:**
   - Veri bütünlüğünü korumak için TRY-CATCH bloğu ile işlem kontrolü.

### Kullanım
1. Veritabanını oluşturun:
   ```sql
   CREATE DATABASE HASTANE_DB;
