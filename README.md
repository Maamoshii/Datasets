# Analisis dan Penjelasan Dataset

```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns
from sklearn.model_selection import train_test_split
from sklearn import tree
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score
from sklearn import metrics
```
<p>
  Kode di atas merupakan tahap awal dalam proyek analisis data menggunakan Python, di mana berbagai library penting diimpor untuk menjalankan proses tersebut. Library <span style="color:blue;"><strong>pandas</strong></span> digunakan untuk manipulasi dan analisis data dalam bentuk tabel (DataFrame), sedangkan <span style="color:blue;"><strong>matplotlib.pyplot</strong></span> dan <span style="color:blue;"><strong>seaborn</strong></span> digunakan untuk visualisasi data, dengan Seaborn memberikan tampilan grafik yang lebih menarik. 
  <span style="color:blue;"><strong>numpy</strong></span> digunakan untuk operasi numerik dan array. Selanjutnya, dari library <span style="color:blue;"><strong>scikit-learn</strong></span> diimpor beberapa modul penting, seperti <span style="color:green;"><code>train_test_split</code></span> untuk membagi dataset menjadi data latih dan data uji, 
  <span style="color:green;"><code>DecisionTreeClassifier</code></span> untuk membangun model klasifikasi berbasis pohon keputusan, serta modul <span style="color:green;"><code>metrics</code></span> dan <span style="color:green;"><code>accuracy_score</code></span> yang digunakan untuk mengevaluasi performa model, seperti mengukur akurasi dan membuat confusion matrix. 
  Secara keseluruhan, impor ini mempersiapkan seluruh fondasi yang dibutuhkan untuk proses pemodelan, pelatihan, pengujian, dan evaluasi data secara lengkap dalam proyek <em>machine learning</em>.
</p>

---
```python
dat1 = pd.read_csv ("MQTT DDoS Publish Flood.csv")
dat1
dat2 = pd.read_csv("MQTT DoS Publish Flood.csv")
dat2
```
<p>
  Kode di atas digunakan untuk membaca dua dataset dari file CSV yang berisi data serangan pada protokol MQTT, yang merupakan bagian dari analisis keamanan jaringan berbasis IoT.
</p>
<ul>
  <li>Baris <code>dat1 = pd.read_csv("MQTT DDoS Publish Flood.csv")</code> memuat dataset pertama yang berisi data serangan <strong>Distributed Denial of Service (DDoS)</strong> dengan metode Publish Flooding, kemudian disimpan dalam variabel <code>dat1</code>.</li>
  <li>Baris <code>dat2 = pd.read_csv("MQTT DoS Publish Flood.csv")</code> memuat dataset kedua yang berisi serangan <strong>Denial of Service (DoS)</strong> dengan teknik serupa dan disimpan dalam variabel <code>dat2</code>.</li>
</ul>
<p></p>


---
```python
datjoin = pd.concat([dat1, dat2],ignore_index=True)
datjoin.columns.values
```
<p>
  Kode di atas digunakan untuk menggabungkan dua dataset (<code>dat1</code> dan <code>dat2</code>) menjadi satu dataframe baru bernama <code>datjoin</code> menggunakan fungsi <code>pd.concat()</code> dari library Pandas. Argumen <code>ignore_index=True</code> memastikan bahwa indeks dari hasil gabungan akan di-reset secara berurutan, sehingga tidak mempertahankan indeks asli dari masing-masing dataset. Hal ini berguna saat ingin memperlakukan kedua dataset sebagai satu kesatuan untuk keperluan analisis atau pelatihan model. 
</p>
<p>
  Selanjutnya, <code>datjoin.columns.values</code> digunakan untuk menampilkan atau mengecek daftar nama kolom (fitur) dari dataframe hasil penggabungan tersebut, untuk memastikan bahwa struktur data konsisten dan tidak terjadi duplikasi atau ketidaksesuaian kolom setelah penggabungan.
</p>

---
```python
array(['Flow ID', 'Src IP', 'Src Port', 'Dst IP', 'Dst Port', 'Protocol',
       'Timestamp', 'Flow Duration', 'Total Fwd Packet',
       'Total Bwd packets', 'Total Length of Fwd Packet',
       'Total Length of Bwd Packet', 'Fwd Packet Length Max',
       'Fwd Packet Length Min', 'Fwd Packet Length Mean',
       'Fwd Packet Length Std', 'Bwd Packet Length Max',
       'Bwd Packet Length Min', 'Bwd Packet Length Mean',
       'Bwd Packet Length Std', 'Flow Bytes/s', 'Flow Packets/s',
       'Flow IAT Mean', 'Flow IAT Std', 'Flow IAT Max', 'Flow IAT Min',
       'Fwd IAT Total', 'Fwd IAT Mean', 'Fwd IAT Std', 'Fwd IAT Max',
       'Fwd IAT Min', 'Bwd IAT Total', 'Bwd IAT Mean', 'Bwd IAT Std',
       'Bwd IAT Max', 'Bwd IAT Min', 'Fwd PSH Flags', 'Bwd PSH Flags',
       'Fwd URG Flags', 'Bwd URG Flags', 'Fwd Header Length',
       'Bwd Header Length', 'Fwd Packets/s', 'Bwd Packets/s',
       'Packet Length Min', 'Packet Length Max', 'Packet Length Mean',
       'Packet Length Std', 'Packet Length Variance', 'FIN Flag Count',
       'SYN Flag Count', 'RST Flag Count', 'PSH Flag Count',
       'ACK Flag Count', 'URG Flag Count', 'CWR Flag Count',
       'ECE Flag Count', 'Down/Up Ratio', 'Average Packet Size',
       'Fwd Segment Size Avg', 'Bwd Segment Size Avg',
       'Fwd Bytes/Bulk Avg', 'Fwd Packet/Bulk Avg', 'Fwd Bulk Rate Avg',
       'Bwd Bytes/Bulk Avg', 'Bwd Packet/Bulk Avg', 'Bwd Bulk Rate Avg',
       'Subflow Fwd Packets', 'Subflow Fwd Bytes', 'Subflow Bwd Packets',
       'Subflow Bwd Bytes', 'FWD Init Win Bytes', 'Bwd Init Win Bytes',
       'Fwd Act Data Pkts', 'Fwd Seg Size Min', 'Active Mean',
       'Active Std', 'Active Max', 'Active Min', 'Idle Mean', 'Idle Std',
       'Idle Max', 'Idle Min', 'Attack Name', 'Label'], dtype=object)
```
<p>
  Array kolom di atas menunjukkan semua fitur (variabel) yang tersedia dalam dataset gabungan <code>datjoin</code>, yang terdiri dari hasil penggabungan dua file CSV: <strong>"MQTT DDoS Publish Flood.csv"</strong> dan <strong>"MQTT DoS Publish Flood.csv"</strong>.
</p>

---
```python
x = datjoin.iloc[:,9:55]
x
y = datjoin.iloc[:,83]
y
```
<p>
  Kode di atas digunakan untuk memisahkan fitur dan label dari dataset <code>datjoin</code>, sebagai persiapan untuk proses pelatihan model machine learning. Variabel <code>x</code> diisi dengan data dari kolom ke-10 hingga ke-55 (<code>iloc[:, 9:55]</code>), yang berisi berbagai fitur jaringan seperti ukuran paket, durasi aliran, dan flag TCP yang akan digunakan sebagai input bagi model. Sementara itu, variabel <code>y</code> diisi dengan kolom ke-84 (<code>iloc[:, 83]</code>), yang berfungsi sebagai target output. Pemisahan ini merupakan langkah penting dalam <strong>supervised learning</strong> untuk memungkinkan model mempelajari hubungan antara fitur dan target.
</p>


---
```python
x = x[y.notnull()]
y = y[y.notnull()]
```
<p>
  Kode diatas digunakan untuk menghapus baris yang mengandung nilai NaN (<strong>Not a Number</strong>) pada variabel fitur (<code>x</code>) dan label (<code>y</code>). Baris pertama, <code>x = x[y.notnull()]</code>, memastikan bahwa hanya data dalam <code>x</code> yang memiliki label valid (tidak NaN) pada <code>y</code> yang dipertahankan. Dengan menggunakan <code>y.notnull()</code>, kode ini menghasilkan array boolean yang menunjukkan elemen mana dalam <code>y</code> yang tidak kosong, dan hanya baris yang sesuai dengan kondisi tersebut yang dipertahankan dalam <code>x</code>. Begitu juga dengan baris kedua, <code>y = y[y.notnull()]</code>, yang memastikan bahwa hanya elemen-elemen dalam <code>y</code> yang tidak mengandung NaN yang tetap ada.</p>

---
```python
x_train,x_test,y_train,y_test = train_test_split(x,y, test_size=0.2, random_state=42)
iqbal = DecisionTreeClassifier(criterion ='entropy', splitter='random')
iqbal.fit(x_train, y_train)
```
<p>
  Kode di atas digunakan untuk melatih model klasifikasi pohon keputusan (<strong>decision tree</strong>) menggunakan data yang telah dipisahkan sebelumnya menjadi fitur (<code>x</code>) dan label (<code>y</code>). Pertama, fungsi <code>train_test_split()</code> dari Scikit-learn digunakan untuk membagi data menjadi dua bagian, yaitu data latih (<code>x_train</code>, <code>y_train</code>) dan data uji (<code>x_test</code>, <code>y_test</code>), dengan proporsi 80% untuk pelatihan dan 20% untuk pengujian. Parameter <code>random_state=42</code> digunakan agar pembagian data bersifat konsisten saat kode dijalankan berulang kali. Selanjutnya, dibuat objek <code>iqbal</code> dari kelas <code>DecisionTreeClassifier</code> dengan parameter <code>criterion='entropy'</code>, yang berarti model akan menggunakan <strong>information gain</strong> untuk menentukan pemisahan terbaik pada setiap simpul pohon, dan <code>splitter='random'</code>, yang berarti pemilihan fitur dan nilai split dilakukan secara acak. Terakhir, model dilatih menggunakan data latih dengan <code>iqbal.fit(x_train, y_train)</code>, yang memungkinkan model mempelajari pola dari data untuk digunakan dalam proses klasifikasi di tahap selanjutnya.
</p>

---
```python
y_pred = iqbal.predict(x_test)
y_pred
hasil output y_pred = array(['MQTT DDoS Publish Flood', 'MQTT DDoS Publish Flood',
                      'MQTT DDoS Publish Flood', ..., 'MQTT DDoS Publish Flood',
                      'MQTT DDoS Publish Flood', 'MQTT DDoS Publish Flood'], dtype=object)
```
<p>
  Kode ini digunakan untuk memprediksi label dari data uji menggunakan model pohon keputusan yang telah dilatih sebelumnya. Baris <code>y_pred = iqbal.predict(x_test)</code> menjalankan metode <code>predict()</code> dari objek model <code>iqbal</code>, yang menghasilkan prediksi terhadap input <code>x_test</code>, yaitu data fitur yang sebelumnya tidak dilihat oleh model saat pelatihan. Hasil prediksi ini disimpan dalam variabel <code>y_pred</code>, yang berisi array label hasil prediksi untuk setiap sampel di data uji. Dalam contoh output yang ditampilkan, semua prediksi adalah <strong>'MQTT DDoS Publish Flood'</strong>, yang menunjukkan bahwa model cenderung mengklasifikasikan seluruh sampel uji ke dalam satu kelas tersebut.
</p>

---
```python
akurasi = accuracy_score(y_test,y_pred)*100
print(f"Akurasi model: {akurasi:.2f}%")
output nya = Akurasi model: 99.96%
```
<p>
  Kode diatas digunakan untuk menghitung dan menampilkan akurasi model dalam bentuk persentase. Pertama, fungsi <code>accuracy_score(y_test, y_pred)</code> digunakan untuk menghitung akurasi dengan membandingkan prediksi (<code>y_pred</code>) terhadap nilai sebenarnya (<code>y_test</code>). Hasil akurasi tersebut kemudian dikalikan dengan 100 untuk mengonversinya menjadi persentase. Setelah itu, akurasi ditampilkan menggunakan fungsi <code>print()</code> dengan format dua angka desimal (<code>akurasi:.2f%</code>), sehingga hasilnya muncul sebagai persentase yang mudah dipahami, seperti "94.96%". Kode ini memberikan gambaran jelas tentang seberapa baik model dalam memprediksi data uji.
</p>

---
```python
conf = plt.figure(figsize = (50, 30))
tree.plot_tree(iqbal, feature_names = x.columns.values, class_names = np.array(['MQTT DDoS Publish Flood.csv','MQTT DoS Publish Flood.csv']), filled = True)
plt.show()
```
<p>
  Kode diatas digunakan untuk memvisualisasikan struktur pohon keputusan (<em>decision tree</em>) yang telah dilatih menggunakan data. Pertama, <code>plt.figure(figsize=(50, 30))</code> membuat gambar dengan ukuran besar (lebar 50 inci dan tinggi 30 inci) agar seluruh pohon dapat ditampilkan dengan jelas. Kemudian, <code>tree.plot_tree()</code> digunakan untuk menggambarkan struktur pohon dari model <code>iqbal</code>, dengan beberapa parameter tambahan: <code>feature_names=x.columns.values</code> untuk menampilkan nama fitur di setiap simpul, <code>class_names=np.array(['MQTT DDoS Publish Flood.csv', 'MQTT DoS Publish Flood.csv'])</code> untuk menampilkan nama kelas target, dan <code>filled=True</code> untuk memberikan warna pada setiap simpul berdasarkan kelas dominan di simpul tersebut. Terakhir, <code>plt.show()</code> digunakan untuk menampilkan visualisasi pohon tersebut secara lengkap.
</p>

---
```python
label = np.array([ 'DDoS Publish Flood.csv','MQTT DoS Publish Flood.csv'])
matrix = metrics.confusion_matrix(y_test, y_pred)
plt.figure(figsize=(10, 10))
sns.heatmap(matrix, annot=True, xticklabels=label, yticklabels=label)
plt.xlabel('Prediksi')
plt.ylabel('Fakta')
plt.show()
```
<p>
  Kode diatas digunakan untuk menghitung dan memvisualisasikan <em>confusion matrix</em> dari hasil prediksi model klasifikasi dalam bentuk <em>heatmap</em>, sehingga memudahkan analisis kinerja model terhadap dua kelas serangan yang berbeda.
</p>
<p>
  Pertama, <code>label = np.array(['DDoS Publish Flood.csv', 'MQTT DoS Publish Flood.csv'])</code> membuat array berisi nama dua kelas yang akan digunakan sebagai label pada sumbu X dan Y grafik. Selanjutnya, <code>metrics.confusion_matrix(y_test, y_pred)</code> menghitung <em>confusion matrix</em> dengan membandingkan hasil prediksi model (<code>y_pred</code>) dengan nilai sebenarnya dari data uji (<code>y_test</code>), menghasilkan sebuah matriks 2x2 yang menunjukkan jumlah prediksi benar dan salah untuk masing-masing kelas. Setelah itu, <code>plt.figure(figsize=(10, 10))</code> mengatur ukuran gambar agar lebih jelas. Fungsi <code>sns.heatmap(matrix, annot=True, xticklabels=label, yticklabels=label)</code> digunakan untuk menampilkan matriks tersebut dalam bentuk peta warna (<em>heatmap</em>), dengan anotasi angka di setiap sel serta label kelas pada sumbu X (<em>prediksi</em>) dan Y (<em>fakta</em>). Terakhir, <code>plt.xlabel('Prediksi')</code> dan <code>plt.ylabel('Fakta')</code> memberikan label pada grafik, dan <code>plt.show()</code> menampilkan hasil visualisasi. <em>Heatmap</em> ini sangat berguna untuk mengevaluasi performa model dalam mengklasifikasikan jenis serangan yang berbeda.
</p>


---
```python
datjoin['Attack Name'].value_counts().plot(kind='bar', figsize=(10,5), color='skyblue')
plt.title('Jumlah Serangan berdasarkan Attack Name')
plt.xlabel('Jenis Serangan')
plt.ylabel('Jumlah')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

  <p>
    Kode diatas digunakan untuk membuat <strong>visualisasi berupa diagram batang (bar chart)</strong> 
    yang menunjukkan jumlah masing-masing jenis serangan berdasarkan kolom <code>'Attack Name'</code> 
    dalam dataset <code>datjoin</code>.
  </p>

  <p><strong>Langkah-langkahnya sebagai berikut:</strong></p>
  <ul>
    <li><code>datjoin['Attack Name'].value_counts()</code> menghitung jumlah kemunculan masing-masing jenis serangan berdasarkan nama serangan.</li>
    <li><code>.plot(kind='bar', figsize=(10,5), color='skyblue')</code> membuat grafik batang berukuran 10x5 inci dengan warna batang biru muda.</li>
    <li><code>plt.title('Jumlah Serangan berdasarkan Attack Name')</code> memberi judul pada grafik.</li>
    <li><code>plt.xlabel('Jenis Serangan')</code> dan <code>plt.ylabel('Jumlah')</code> memberi label pada sumbu X dan Y.</li>
    <li><code>plt.xticks(rotation=45)</code> memutar label sumbu X sebesar 45 derajat agar mudah dibaca.</li>
    <li><code>plt.tight_layout()</code> mengatur tata letak agar elemen tidak saling tumpang tindih.</li>
    <li><code>plt.show()</code> menampilkan grafiknya.</li>
  </ul>

  <p>
    Visualisasi ini berguna untuk melihat <strong>distribusi atau dominasi jenis serangan</strong> 
    dalam dataset secara cepat dan jelas.
  </p>

---
```python
datjoin['Attack Name'].value_counts().plot(kind='pie', autopct='%1.1f%%', figsize=(8,8))
plt.title('Distribusi Jenis Serangan (Attack Name)')
plt.ylabel('')
plt.show()
```
<p><p>
    Kode diatas digunakan untuk membuat <strong>visualisasi pie chart (diagram lingkaran)</strong> 
    yang menunjukkan distribusi persentase masing-masing jenis serangan berdasarkan kolom <code>'Attack Name'</code> dalam dataset <code>datjoin</code>.
  </p>

  <p><strong>Langkah-langkah penjelasan kode:</strong></p>
  <ul>
    <li><code>datjoin['Attack Name'].value_counts()</code> menghitung jumlah masing-masing jenis serangan.</li>
    <li><code>.plot(kind='pie', autopct='%1.1f%%', figsize=(8,8))</code> membuat diagram lingkaran berukuran 8x8 inci, dengan persentase tiap segmen ditampilkan hingga satu angka di belakang koma.</li>
    <li><code>plt.title('Distribusi Jenis Serangan (Attack Name)')</code> memberikan judul pada grafik.</li>
    <li><code>plt.ylabel('')</code> menghapus label pada sumbu Y untuk tampilan yang lebih bersih.</li>
    <li><code>plt.show()</code> menampilkan hasil visualisasi.</li>
  </ul>
</p>



