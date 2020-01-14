# UrbanDictionaryAnalysis

**İngilizce'de En Çok Kullanılan ilk 10 Kelime**

       *Veriler kelimelerin çok kullanılma sıklıklarına göre düzenlendiği için, ilk 10 kelimeyi grafikte görelim. *****

# İlgili Kütüphaneleri içeri aktaralım

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns


# csv formatlı verilerimizi okuyalım, burda gerekirse, dosya konumunu da değiştirebiliriz.

df = pd.read_csv("../input/unigram_freq.csv")
df.head(10)

# En çok kullanılan ilk 10'u görelim
top10 = df.iloc[0:10]
plt.figure(figsize=(10,6))
sns.barplot("word", "count", data=top10, palette="Blues_d").set_title("Top 10 Words")


# En az Kullanılan 10 kelimeyi grafiğe dökelim..Garip garip,zorlama uzunlukta kelimeler gelecek, şaşırmayın:)
# Buyrun İnceleyelim** ( Ancak hepsi de birkaç kelimenin yanyana gelmesi ile oluşmuş zorlama kelimeler biraz da.) (Yorum benimdir,veriyi inclediğimde tuhaf geldiği için belirttim.Zira uzun ama anlamsız ve bazısı da muzip içeriğe sahip:)

df.sort_values(by="count").iloc[0:10]

# En Uzun 10 kelime

s = df.word.str.len().sort_values(ascending=False).index
longest10 = df.reindex(s).iloc[0:10]
plt.figure(figsize=(10,6))
sns.barplot("count", "word", data=longest10, orient="h", palette="Blues_d").set_title("Top 10 Longest Words")


#Veriyi bulduğum kaynaktaki İngilizce yorumu da ekliyorum arkadaşlar. Kendisi de bu kadar uzun ve garip kelimenin İngilizce'de olduğunu bilmiyormuş. Zaten dikkatli bakınca, anadili İngilizce olanlar için de saçma ve zorlama olduğu ortaya çıkıyor.Bazıları muzip isimlere sahip: Orjinal Kaynaktaki Yorum: "Well I didn't even know that those words exist and there are actually a quite number of people used them."

#Eğer alfabedeki harfleri birer kelime gibi düşünse idik, en sıkı kullanımın A harfi ile başlayanlarda ortaya çıktığını, bu veriye göre iddia edebilirdik.


alphabet = df.reindex(s).iloc[::-1][2:28].sort_values(by="count", ascending=False)
plt.figure(figsize=(10,6))
sns.barplot("word", "count", data=alphabet, palette="Blues_d").set_title("Alphabets")

