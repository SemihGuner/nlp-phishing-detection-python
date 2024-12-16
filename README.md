# Yapay Zeka Kullanarak Zararlı İnternet Sitelerinin Engellenmesi

## Genel Bakış
Bu proje, **derin öğrenme** ve **transformer tabanlı mimariler** kullanarak URL'ler üzerinden oltalama (phishing) internet sitelerini tespit etmeyi amaçlar. İnternet kullanımının ve oltalama saldırılarının hızla artmasıyla, bu çalışma, zararlı ve zararsız internet sitelerini etkili bir şekilde ayırt edebilen yapay zeka destekli sistemler geliştirmeye odaklanmaktadır.
Düzce Üniversitesi Bilgisayar Mühendisliği Lisans Programı 2024 Mezuniyet Tezi projemdir.

## Temel Özellikler
- Üç ana sinir ağı modeli test edilmiştir:
  - **BERT (Bidirectional Encoder Representations from Transformers)**
  - **DistilBERT (BERT'in hafif sürümü)**
  - **Evrimsel Sinir Ağları (CNNs)**
- Açık kaynak veri setleri ve API'lerin bir kombinasyonunu kullanarak dengeli bir eğitim ve doğrulama veri seti oluşturur.
- Oltalama internet sitelerinin tespitinde yüksek doğruluk oranlarına ulaşır; BERT diğer modellerden üstün performans göstermektedir.

## Veri Seti
Veri seti, üç ana kaynaktan elde edilen URL'leri birleştirerek oluşturulmuştur:
1. **Kaggle "Malicious And Benign URLs" veri seti**:
   - 450,176 etiketli URL içerir (%77 zararsız, %23 zararlı).
2. **Ulusal Siber Olaylarla Mücadele Merkezi (USOM)**:
   - 266,578 oltalama URL’si içerir.
3. **PhishTank API**:
   - 39,172 zararlı URL içerir.

Önişleme ve dengeleme sonrası elde edilen nihai veri seti:
- **100,000 zararsız URL**
- **100,000 zararlı URL**

## Modeller ve Sonuçlar
### 1. **BERT**
- En yüksek performansı elde etmiştir:
  - **%98 Doğruluk**
  - **%98 F1 Skoru**
- BERT, Keras'tan alınan ön eğitimli modeller kullanılarak eğitilmiş ve veri seti üzerinde ince ayar yapılmıştır.

### 2. **DistilBERT**
- BERT'ten daha hızlı ve kaynak açısından daha verimli ancak daha az etkili:
  - **%93 Doğruluk**
  - Güncel URL'ler için yanlış tahminlerde bulunma sorunları gözlemlenmiştir.

### 3. **CNN**
- Keras ve önceden eğitilmiş GloVe gömmelerini kullanarak özel olarak tasarlanmış model:
  - **%91 Doğruluk**
  - Etkili olmasına rağmen, CNN'ler bağlam çıkarma konusunda transformer tabanlı modellerin gerisinde kalmıştır.

| Model       | Doğruluk | Kesinlik | Geri Çağırma | F1-Skoru |
|-------------|----------|----------|--------------|----------|
| **BERT**    | %98      | %98      | %98          | %98      |
| **DistilBERT** | %93      | %93      | %93          | %93      |
| **CNN**     | %91      | %91      | %91          | %91      |

## Yöntem
1. **Veri Önişleme**:
   - Protokoller (ör. `https://`, `ftp://`) ve `www` alt alan adları kaldırılmıştır.
   - URL'lerden noktalama işaretleri ve özel karakterler çıkarılmıştır.

2. **Model Eğitimi**:
   - **Google Colab** ve TPU desteği kullanılarak daha hızlı eğitim sağlanmıştır.
   - Modellere verilerle fine-tuning uygulanmıştır.

3. **Değerlendirme**:
   - Sonuçlar mevcut literatür ile karşılaştırılmıştır.
   - Her modelin güçlü ve zayıf yönleri vurgulanmıştır.

## Sonuç
- **BERT**, URL tabanlı oltalama tespitinde en etkili modeldir ancak hesaplama açısından pahalıdır.
- **DistilBERT**, kaynak kısıtlı ortamlar için uygundur ancak bazı performans sınırlamaları vardır.
- **CNN'ler**, daha basit görevler için uygun bir alternatiftir ancak transformerların bağlamsal anlama yeteneklerinden yoksundur.

Gelecekteki çalışmalar, gerçek zamanlı oltalama tespiti için hafif transformer modellerinin keşfedilmesini ve bu modellerin siber güvenlik sistemlerine entegre edilmesini içerebilir.

## Kaynaklar
1. Kaggle Veri Seti: [Malicious and Benign URLs](https://www.kaggle.com/datasets/siddharthkumar25/malicious-and-benign-urls)
2. PhishTank API: [PhishTank](https://phishtank.org/)
3. [USOM Resmi Web Sitesi](https://www.usom.gov.tr)

---
**Yazar**: Semih Güner  
**Danışman**: Dr. Öğr. Üyesi Büşra Takgil  
**Üniversite**: Düzce Üniversitesi  
**Yıl**: 2024
