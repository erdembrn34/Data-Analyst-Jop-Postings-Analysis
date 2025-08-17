# Data Analyst Job Postings Analysis

Bu proje, Kaggle'daki [Data Analyst Jobs](https://www.kaggle.com/datasets/andrewmvd/data-analyst-jobs) veri seti kullanılarak yapılmıştır.

## İçerik
- Maaş analizi
- Lokasyon analizi
- En yüksek ortalama maaş veren şehirler
- Kelime bulutu
- En çok aranan beceriler
- Şirket analizi

## Kullanım
1. Kaggle'dan veri setini indirin.
2. `data_analyst_jobs_analysis.ipynb` dosyasını açın ve çalıştırın.
3. Grafikleri ve analizleri görüntüleyin.

## Gereksinimler
```bash
pip install pandas matplotlib seaborn wordcloud

## 2️⃣ Jupyter Notebook (`data_analyst_jobs_analysis.ipynb`) Örneği
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from wordcloud import WordCloud

# Veri yükleme
# df = pd.read_csv('DataAnalystJob.csv')  # Dosya adınızı buraya yazın

# 1️⃣ Genel Bilgi
print(df.info())
print(df.head())

# 2️⃣ Maaş Analizi
plt.figure(figsize=(10,5))
sns.histplot(df['avg_salary'], bins=30, kde=True)
plt.title("Ortalama Maaş Dağılımı")
plt.xlabel("Ortalama Maaş (USD)")
plt.ylabel("İlan Sayısı")
plt.show()

# 3️⃣ Lokasyon Analizi
top_locations = df['Location'].value_counts().head(10)
plt.figure(figsize=(10,5))
sns.barplot(x=top_locations.values, y=top_locations.index)
plt.title("En Çok İlan Veren Şehirler")
plt.xlabel("İlan Sayısı")
plt.ylabel("Şehir")
plt.show()

# 4️⃣ En Yüksek Ortalama Maaş Veren Şehirler
top_salary_locations = df.groupby('Location')['avg_salary'].mean().sort_values(ascending=False).head(10)
plt.figure(figsize=(10,5))
sns.barplot(x=top_salary_locations.values, y=top_salary_locations.index)
plt.title("En Yüksek Ortalama Maaş Veren Şehirler")
plt.xlabel("Ortalama Maaş (USD)")
plt.ylabel("Şehir")
plt.show()

# 5️⃣ Kelime Bulutu
text = " ".join(desc for desc in df['Job Description'].dropna())
wordcloud = WordCloud(width=800, height=400, background_color='white').generate(text)
plt.figure(figsize=(10,5))
plt.imshow(wordcloud, interpolation='bilinear')
plt.axis("off")
plt.show()

# 6️⃣ Beceriler Analizi
skills = ['Python', 'SQL', 'Excel', 'Tableau', 'R', 'Power BI']
skill_counts = df[skills].sum().sort_values(ascending=False)
plt.figure(figsize=(10,5))
sns.barplot(x=skill_counts.index, y=skill_counts.values)
plt.title("En Çok Aranan Beceriler")
plt.ylabel("İlan Sayısı")
plt.show()

# 7️⃣ Şirket Analizi
top_companies = df.groupby('Company Name').size().sort_values(ascending=False).head(10)
plt.figure(figsize=(10,5))
sns.barplot(x=top_companies.values, y=top_companies.index)
plt.title("En Çok İlan Veren Şirketler")
plt.xlabel("İlan Sayısı")
plt.show()
