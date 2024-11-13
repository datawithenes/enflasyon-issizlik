# Enflasyon ve İşsizlik Verilerini Düzenleme

Bu proje, 2006-2019 yılları arasında enflasyon ve işsizlik oranlarını içeren bir veri setini inceleyerek, veri temizleme ve düzenleme sürecini gerçekleştirmeyi amaçlamaktadır. Veritabanında bulunan NaN (boş) değerler, bozuk veya aykırı değerler analiz edilmiş ve düzenlenmiştir. Ayrıca, verilerin doğru türde olup olmadığı kontrol edilerek uygun veri türlerine dönüştürülmüştür.

Proje, özellikle veri ön işleme, temizleme ve analiz için kullanılan Python kütüphaneleriyle gerçekleştirilmiştir.

## Proje Özeti

Bu proje kapsamında aşağıdaki işlemler yapılmıştır:

1. **Veri İçe Aktarımı**: Veritabanı içindeki işsizlik ve enflasyon verileri içeri aktarılmıştır.
2. **Veri Temizleme**: NaN (boş) değerler ve yanlış veri türleri tespit edilip düzenlenmiştir.
3. **Korelasyon Analizi**: İşsizlik ve enflasyon arasındaki ilişki incelenmiş, korelasyon hesaplanmış ve grafiksel olarak görselleştirilmiştir.
4. **Phillips Eğrisi Testi**: İşsizlik ve enflasyon arasında beklenen negatif ilişki (Phillips Eğrisi) incelenmiş ve sonuçlar değerlendirilmiştir.

## Kullanılan Araçlar ve Teknolojiler

- **Python**: Veri analizi ve işleme işlemleri için kullanılmıştır.
- **Pandas**: Veri temizleme, düzenleme ve analizi için kullanılmıştır.
- **Seaborn / Matplotlib**: Verilerin görselleştirilmesi için kullanılmıştır.
- **NumPy**: Matematiksel hesaplamalar ve veri manipülasyonu için kullanılmıştır.

## Adımlar

### 1. Veri İçe Aktarımı

İlk olarak, veri seti **Pandas** kütüphanesi kullanılarak içeri aktarılmıştır. İşsizlik ve enflasyon oranlarını içeren veri tablosunda, **NaN** (boş) değerler ve yanlış veri türleri (özellikle string veri tipindeki sayısal veriler) tespit edilmiştir.

```python
import pandas as pd

# Veri dosyasını yükle
data = pd.read_csv("data.csv")
```

### 2. Veri Temizleme

Veriyi inceledikten sonra, aşağıdaki adımlar izlenmiştir:

- **Veri Tipi Düzeltmesi**: Enflasyon ve işsizlik oranları, sayısal veriler olması gerekirken, `object` (string) türünde yer alıyordu. Bu veri türü `astype()` fonksiyonu ile `float` türüne dönüştürülmüştür.
  
```python
# Veri tiplerini düzeltme
data['Enflasyon'] = data['Enflasyon'].astype(float)
data['İşsizlik'] = data['İşsizlik'].astype(float)
```

- **NaN Değerlerinin Temizlenmesi**: Verideki eksik (NaN) değerler `dropna()` fonksiyonu ile silinmiş ve işlemin kalıcı olması sağlanmıştır.

```python
# NaN değerlerini silme
data.dropna(inplace=True)
```

### 3. Korelasyon Analizi

İşsizlik ve enflasyon arasındaki ilişkiyi anlamak için, **Pandas** ve **Seaborn** kütüphaneleri ile korelasyon analizi yapılmıştır. Korelasyon değeri `0.194711` olarak hesaplanmış olup, bu çok düşük bir pozitif korelasyon olduğunu göstermektedir.

```python
# Korelasyon hesaplama
correlation = data[['Enflasyon', 'İşsizlik']].corr()
print(correlation)

# Korelasyon grafiği
import seaborn as sns
import matplotlib.pyplot as plt

sns.heatmap(correlation, annot=True, cmap="coolwarm")
plt.title("Enflasyon ve İşsizlik Korelasyonu")
plt.show()
```

### 4. Phillips Eğrisi Testi

Phillips Eğrisi teorisi, işsizlik oranı ile enflasyon arasında negatif bir ilişki olduğunu öngörmektedir. Ancak, bu verilerde yapılan analiz sonucunda, işsizlik ve enflasyon arasında beklenen negatif ilişki tespit edilmemiştir. Korelasyon değeri oldukça düşük çıkmış, yani iki değişken arasında anlamlı bir ilişki bulunmamaktadır.

**Sonuç**: Phillips Eğrisi'nin aksine, bu dönemde işsizlik ile enflasyon arasında çok zayıf bir pozitif korelasyon gözlemlenmiştir. Bu da, teorinin verilerle uyumsuz olduğunu gösterir.

## Sonuçlar

Veri analizi ve temizleme işlemleri sonucunda şunlar elde edilmiştir:

- **NaN Değerleri**: Veri setindeki eksik değerler temizlenmiş ve veri tutarlılığı sağlanmıştır.
- **Veri Tipi Düzeltmesi**: Enflasyon ve işsizlik verilerinin doğru veri tipi ile işlenmesi sağlanmıştır.
- **Korelasyon**: İşsizlik ve enflasyon arasında çok düşük bir pozitif korelasyon (`0.194711`) bulunmuştur.
- **Phillips Eğrisi**: Phillips Eğrisi'ne göre beklenen negatif ilişki gözlemlenmemiştir.


### 1. Veriyi İndirin

Veri dosyasını bu GitHub reposundan indirerek veya kendi verinizi kullanarak analizleri çalıştırabilirsiniz.

### 2. Kodu Çalıştırın

Python betiğini çalıştırarak verileri temizleyebilir ve korelasyon analizini gerçekleştirebilirsiniz.

```bash
python enflasyon_issizlik_analizi.py
```

## Katkı Sağlama

Bu projeye katkıda bulunmak isterseniz, aşağıdaki adımları takip edebilirsiniz:

1. Projeyi fork'layın.
2. Yeni özellikler veya düzeltmeler ekleyin.
3. Pull request gönderin.

## Lisans

Bu proje [MIT Lisansı](LICENSE) altında lisanslanmıştır.

