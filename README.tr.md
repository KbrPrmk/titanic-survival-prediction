<h1 align="center">🚢 Titanic Hayatta Kalma Tahmini</h1>
<p align="center"><b>Unvan bazlı yaş doldurma ve Lojistik Regresyon + Random Forest karşılaştırmasıyla Titanic yolcu hayatta kalma tahmini yapan Kaggle projesi</b></p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-3776AB?style=flat&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/scikit--learn-ML-F7931E?style=flat&logo=scikit-learn&logoColor=white" />
  <img src="https://img.shields.io/badge/Kaggle-Yarışma-20BEFF?style=flat&logo=kaggle&logoColor=white" />
  <img src="https://img.shields.io/badge/Lisans-MIT-green?style=flat" />
</p>

🇹🇷 Türkçe | 🇬🇧 [English](README.md)

---

## 📌 Genel Bakış

**Titanic Hayatta Kalma Tahmini**, [Kaggle Titanic yarışması](https://www.kaggle.com/competitions/titanic) için hazırlanmış bir ikili sınıflandırma projesidir. Amaç; yaş, cinsiyet, bilet sınıfı ve bilet ücreti gibi özelliklere dayanarak hangi yolcuların felaketten sağ kurtulduğunu tahmin etmektir. Proje; kapsamlı keşifsel veri analizi, dikkatli eksik değer doldurma (unvan bazlı yaş imputation dahil), özellik mühendisliği ve 5 katlı çapraz doğrulama ile model değerlendirme aşamalarını içermektedir.

---

## ✨ Özellikler

- 📊 **Kapsamlı EDA** — Plotly, Seaborn ve Missingno kullanılarak sınıf, cinsiyet, yaş, bilet ücreti ve binilen limana göre hayatta kalma oranı analizi
- 🧹 **Akıllı eksik değer doldurma** — yaş, unvan grubu medyanıyla (Mr, Mrs, Miss, Master, Rare); bilet ücreti, Pclass medyanıyla; binilen liman ise mod değeriyle doldurulmuştur
- 🏷️ **Unvan özellik mühendisliği** — yolcu isimleri regex ile ayrıştırılarak anlamlı kategorilere gruplanmıştır
- 🤖 **İki model karşılaştırması** — Lojistik Regresyon (StandardScaler ile) ve Random Forest, her ikisi de 5 katlı CV ile değerlendirilmiştir
- 📤 **Kaggle submission hazır** — gerekli formatta `submission.csv` oluşturulmuştur

---

## 📁 Proje Yapısı

```
titanic-survival-prediction/
├── titanic-disaster.ipynb   # Tam notebook (EDA, ön işleme, modelleme, submission)
├── README.md                # İngilizce dokümantasyon
└── README.tr.md             # Türkçe dokümantasyon
```

> `train.csv` ve `test.csv` veri seti dosyaları bu depoya dahil edilmemiştir. [Kaggle Titanic yarışması sayfasından](https://www.kaggle.com/competitions/titanic/data) indirilebilir.

---

## 📊 Veri Seti

[Kaggle Titanic veri seti](https://www.kaggle.com/competitions/titanic/data), RMS Titanic felaketinden (1912) yolcu bilgilerini içermektedir.

| Özellik | Değer |
|---|---|
| **Eğitim örneği** | 891 |
| **Test örneği** | 418 |
| **Hedef değişken** | `Survived` (0 = Hayır, 1 = Evet) |
| **Sınıf dengesi** | ~%61.6 hayatta kalmadı, ~%38.4 hayatta kaldı |

**Ön işleme sonrası kullanılan özellikler:**

| Özellik | Açıklama |
|---|---|
| `Pclass` | Bilet sınıfı (1 = 1., 2 = 2., 3 = 3.) |
| `Sex` | Cinsiyet (etiket kodlanmış) |
| `Age` | Yaş (unvan grubu medyanıyla doldurulmuş) |
| `SibSp` | Gemideki kardeş/eş sayısı |
| `Parch` | Gemideki ebeveyn/çocuk sayısı |
| `Fare` | Bilet ücreti (Pclass medyanıyla doldurulmuş) |
| `Embarked_Q`, `Embarked_S` | Binilen liman (one-hot kodlanmış) |
| `Title_Miss`, `Title_Mr`, `Title_Mrs`, `Title_Rare` | İsimden çıkarılan unvan (one-hot kodlanmış) |

> Düşürülen sütunlar: `Name`, `Ticket`, `Cabin` (%77 eksik), `PassengerId`

---

## ⚙️ Ön İşleme Aşamaları

1. **Embarked** — 2 eksik değer mod değeriyle dolduruldu (`S` / Southampton)
2. **Fare** — test setindeki 1 eksik değer, eğitim setindeki Pclass grubu medyanıyla dolduruldu
3. **Age** — 177 eğitim / 86 test eksik değeri, unvan grubu medyanıyla dolduruldu (`Master` → 3.5, `Mr` → 30.0, `Miss` → 21.0, `Mrs` → 35.0, `Rare` → 48.5)
4. **Cabin** — ~%77 eksiklik nedeniyle tamamen kaldırıldı
5. **Title** — `Name` sütunundan regex ile çıkarıldı; nadir unvanlar (`Lady`, `Countess`, `Dr`, `Rev` vb.) `Rare` olarak gruplandı; takma adlar normalize edildi (`Mlle` → `Miss`, `Ms` → `Miss`, `Mme` → `Mrs`)
6. **Kodlama** — `Sex` etiket kodlandı; `Embarked` ve `Title` one-hot kodlandı (`drop_first=True`)
7. **Ölçekleme** — Sayısal özellikler Lojistik Regresyon için `StandardScaler` ile ölçeklendi; Random Forest orijinal veriyle kullanıldı

---

## 🤖 Modeller

Her iki model de eğitim setinde **5 katlı çapraz doğrulama doğruluğu** ile değerlendirildi.

| Model | CV Doğruluğu |
|---|---|
| **Lojistik Regresyon** | %82.38 |
| **Random Forest** | %82.38 |

Son Kaggle submission için Random Forest seçilmiştir.

---

## 📈 Temel EDA Bulguları

- **Cinsiyet** — Kadınların hayatta kalma oranı erkeklerin neredeyse 3 katıdır ("önce kadınlar ve çocuklar" tahliye protokolü)
- **Pclass** — 1. sınıf yolcularının hayatta kalma oranı belirgin şekilde daha yüksektir; 3. sınıfta en yüksek ölüm oranı gözlemlenmiştir
- **Fare** — hayatta kalmayla pozitif korelasyon (+0.26); yüksek bilet ücretleri daha yüksek hayatta kalma oranıyla ilişkilidir
- **Age** — 0–10 yaş çocuklarda hayatta kalma oranı yetişkinlerden daha yüksektir; genel olarak zayıf negatif korelasyon (−0.077)

---

## 🚀 Başlarken

```bash
git clone https://github.com/KubraParmak/titanic-survival-prediction.git
cd titanic-survival-prediction
pip install -r requirements.txt
```

Ardından `train.csv` ve `test.csv` dosyalarını [Kaggle'dan](https://www.kaggle.com/competitions/titanic/data) indirip proje klasörüne koy ve notebook'u çalıştır.

<details>
<summary>📦 Gerekli bağımlılıklar</summary>

```
pandas
numpy
scikit-learn
matplotlib
seaborn
plotly
missingno
```
</details>

---

## 🛠️ Kullanılan Teknolojiler

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white" />
  <img src="https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white" />
  <img src="https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white" />
  <img src="https://img.shields.io/badge/Plotly-3F4F75?style=flat&logo=plotly&logoColor=white" />
  <img src="https://img.shields.io/badge/Seaborn-gray?style=flat" />
  <img src="https://img.shields.io/badge/Kaggle-20BEFF?style=flat&logo=kaggle&logoColor=white" />
</p>

---

## 📄 Lisans

Bu proje **MIT Lisansı** ile lisanslanmıştır.

---

## 🙋 Yazar

**Kübra Parmak**
- GitHub: [@KbrPrmk](https://github.com/KbrPrmk)
- Hugging Face: [@KubraParmak](https://huggingface.co/KubraParmak)
