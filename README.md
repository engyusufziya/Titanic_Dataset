# Titanic Veri Seti Analizi

Bu proje, Titanic veri seti üzerinde temel Veri Keşfi (EDA) adımlarını uygulayarak veri temizleme, eksik değer analizi, görselleştirme ve bazı öngörüsel çıkarımlarda bulunmayı amaçlamaktadır.

## İçindekiler

- [Genel Bakış](#genel-bakış)  
- [Kullanılan Kütüphaneler](#kullanılan-kütüphaneler)  
- [Veri Seti Hakkında](#veri-seti-hakkında)  
- [Yapılan Adımlar](#yapılan-adımlar)  
  - [1. Veri Yükleme](#1-veri-yükleme)  
  - [2. Veri Keşfi (EDA)](#2-veri-keşfi-eda)  
  - [3. Eksik Değer Analizi ve Doldurma](#3-eksik-değer-analizi-ve-doldurma)  
  - [4. Özellik Mühendisliği (Feature Engineering)](#4-özellik-mühendisliği-feature-engineering)  
  - [5. Veri Görselleştirme](#5-veri-görselleştirme)  
- [Sonuçlar ve Çıkarımlar](#sonuçlar-ve-çıkarımlar)  


---

## Genel Bakış
Bu proje, **Titanic** veri seti üzerinde yapılan bir **Exploratory Data Analysis (EDA)** çalışmasını içerir. Proje kapsamında, veri setindeki sütunlar incelenmiş, eksik değerler tespit edilmiş ve uygun yöntemlerle doldurulmuştur. Ardından çeşitli grafiklerle verinin yapısı ve hayatta kalmayı etkileyen faktörler analiz edilmiştir.

## Kullanılan Kütüphaneler
- **NumPy**: Sayısal işlemler ve dizi manipülasyonu.  
- **Pandas**: Veri işleme ve DataFrame yapısı.  
- **Seaborn**: İleri düzey veri görselleştirme kütüphanesi.  
- **Matplotlib**: Temel veri görselleştirme fonksiyonları.

## Veri Seti Hakkında
**Titanic** veri seti, 1912 yılında gerçekleşen Titanic faciasına dair yolcu bilgilerini içerir. Temel sütunlar şunlardır:

- **Survived**: Yolcunun hayatta kalıp kalmadığını gösterir (0 = Hayır, 1 = Evet).  
- **Pclass**: Bilet sınıfı (1 = First, 2 = Second, 3 = Third).  
- **Name**: Yolcunun adı.  
- **Sex**: Yolcunun cinsiyeti.  
- **Age**: Yolcunun yaşı.  
- **SibSp**: Yanındaki kardeş/eş sayısı.  
- **Parch**: Yanındaki ebeveyn/çocuk sayısı.  
- **Ticket**: Bilet numarası.  
- **Fare**: Bilet ücreti.  
- **Cabin**: Kabin numarası.  
- **Embarked**: Biniş limanı (C = Cherbourg, Q = Queenstown, S = Southampton).

## Yapılan Adımlar

### 1. Veri Yükleme
```python
df = pd.read_csv('/content/train.csv')
```
Veri, `pd.read_csv` fonksiyonu ile DataFrame’e aktarıldı. `df.head()` ve `df.tail()` gibi fonksiyonlarla ilk ve son satırlar görüntülendi.

### 2. Veri Keşfi (EDA)
- `df.info()` ile veri setinin genel bilgileri, veri tipleri ve eksik değer durumları incelendi.  
- `df.describe()` ile temel istatistiksel özet (ortalama, standart sapma, min, max) elde edildi.  
- `df.count()` ve döngüler kullanılarak sütunlardaki eksik değer sayıları tespit edildi.

### 3. Eksik Değer Analizi ve Doldurma
- `df.isnull().sum()` veya bir döngü kullanılarak eksik veriler sütun bazında analiz edildi.  
- **Age** sütunundaki eksik değerler **medyan** ile, **Cabin** sütunundaki eksik değerler `"Bilinmeyen"` olarak, **Embarked** sütunundaki eksik değerler de **mod** (en sık görülen değer) ile dolduruldu.

### 4. Özellik Mühendisliği (Feature Engineering)
- `HasCabin` sütunu oluşturuldu:  
  ```python
  df['HasCabin'] = df['Cabin'].notnull().astype('int')
  ```
  Bu sayede, kabin bilgisi olan ve olmayan yolcular 1 ve 0 olarak etiketlendi.  
- Ek olarak, **AgeGroup** gibi kategorik bir yaş değişkeni oluşturularak farklı yaş gruplarının hayatta kalma oranları incelendi.

### 5. Veri Görselleştirme
- **Seaborn** ve **Matplotlib** ile çeşitli grafikler oluşturuldu:  
  - **countplot** ve **barplot** grafikleriyle **cinsiyet, sınıf, biniş limanı, aile bilgisi** gibi değişkenlerin hayatta kalmaya etkisi incelendi.  
  - **histplot** ile **Age** (yaş) dağılımı gözlemlendi.  
  - **heatmap** ile sayısal değişkenler arasındaki korelasyon analiz edildi.

## Sonuçlar ve Çıkarımlar
- **Cinsiyet (Sex)**: Kadın yolcuların hayatta kalma oranı, erkek yolculara göre çok daha yüksektir.  
- **Sınıf (Pclass)**: 1. sınıfta seyahat eden yolcuların hayatta kalma oranı, 2. ve 3. sınıfa göre belirgin biçimde yüksektir.  
- **Yaş (Age)**: Çocuklar ve genç yolcuların hayatta kalma oranı nispeten daha yüksek, yaşlı yolcularınki ise daha düşüktür.  
- **Bilet Ücreti (Fare)**: Bilet ücreti arttıkça (daha pahalı biletler), hayatta kalma olasılığı da artmaktadır.  
- **HasCabin**: Kabin bilgisi olanların hayatta kalma oranı, kabin bilgisi olmayanlara göre daha yüksek bulunmuştur.

Bu çıkarımlar, Titanic kazasındaki tarihsel gerçeklerle de uyum göstermektedir.

Keyifli incelemeler!
