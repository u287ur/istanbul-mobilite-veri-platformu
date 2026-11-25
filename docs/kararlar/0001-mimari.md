# 0001 Mimari: batch, streaming ve tablo formatı

Durum: Önerildi
Tarih: 23 Kasım 2026

## Bağlam

<!-- Kararı gerektiren durum: kaynaklar, tüketiciler, gecikme ihtiyaçları ve kısıtlar. -->

Müşterinin toplu ulaşım verileri üzerinden karşılanması gereken iki temel ihtiyacı bulunmaktadır:

1. **Aylık hat raporu:** Her ayın kapanışından sonra hat ve ilçe bazında toplam yolcu sayılarının hesaplanması ve raporlanması.
2. **Durak yoğunluğu:** Duraklardan geçen yolcu sayılarının son 5 dakikayı aşmayacak şekilde takip edilmesi ve belirlenen eşiklerin aşılması durumunda alarm üretilmesi.

Bu iki ihtiyacın veri işleme ve gecikme gereksinimleri farklıdır.

Aylık hat raporu için yüksek hacimli verinin toplu işlenmesi yeterliyken durak yoğunluğu için sürekli veri işleme ve düşük gecikmeli sonuç üretimi gerekmektedir.

Mimari, batch ve streaming iş yüklerini birlikte desteklemeli; geçmiş verilerin analizi ile gerçek zamanlı operasyonel takibi aynı veri platformunda birleştirmelidir.

## Karar

<!-- Seçilen yol, tek cümleyle: batch ve streaming bileşenleri, tablo formatı ve katalog. -->

Aylık dosyalar batch olarak bronze, silver ve gold katmanlarından geçer.  
Geçiş olayları Kafka ve Structured Streaming ile aynı kataloğa yazılır.  
Tablo formati Iceberg, katalog Polaris olur.  

## Gerekçe

<!-- Ölçülebilir ihtiyaçlar ve elenen seçenekler. -->

Aylık rapor bir gün gecikmeyi kabul eder.  
Durak yoğunluğu en geç 5 dakikada güncellenir.  
DuckDB ve Spark aynı tabloları okur ve yazar.  

## Sonuçlar

<!-- Kararın getirdiği iş, maliyet ve risk. -->
