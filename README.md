# Penjelasan Datasets

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
<P>Kode di atas merupakan tahap awal dalam proyek analisis data menggunakan Python, di mana berbagai library penting diimpor untuk menjalankan proses tersebut. Library pandas digunakan untuk manipulasi dan analisis data dalam bentuk tabel (DataFrame), sedangkan matplotlib.pyplot dan seaborn digunakan untuk visualisasi data, dengan Seaborn memberikan tampilan grafik yang lebih menarik. numpy digunakan untuk operasi numerik dan array. Selanjutnya, dari library scikit-learn diimpor beberapa modul penting, seperti train_test_split untuk membagi dataset menjadi data latih dan data uji, DecisionTreeClassifier untuk membangun model klasifikasi berbasis pohon keputusan, serta modul metrics dan accuracy_score yang digunakan untuk mengevaluasi performa model, seperti mengukur akurasi dan membuat confusion matrix. Secara keseluruhan, impor ini mempersiapkan seluruh fondasi yang dibutuhkan untuk proses pemodelan, pelatihan, pengujian, dan evaluasi data secara lengkap dalam proyek machine learning.</P>

```python
dat1 = pd.read_csv ("MQTT DDoS Publish Flood.csv")
dat1
dat2 = pd.read_csv("MQTT DoS Publish Flood.csv")
dat2
```
<p>Kode di atas digunakan untuk membaca dua dataset dari file CSV yang berisi data serangan pada protokol MQTT, yang merupakan bagian dari analisis keamanan jaringan berbasis IoT.</p> 
<li>Baris dat1 = pd.read_csv("MQTT DDoS Publish Flood.csv") memuat dataset pertama yang berisi data serangan Distributed Denial of Service (DDoS) dengan metode Publish Flooding, kemudian disimpan dalam variabel dat1.</li> 
<li>Baris dat2 = pd.read_csv("MQTT DoS Publish Flood.csv") memuat dataset kedua yang berisi serangan Denial of Service (DoS) dengan teknik serupa dan disimpan dalam variabel dat2.</li> 
<p></p>

```python
datjoin = pd.concat([dat1, dat2],ignore_index=True)
datjoin.columns.values
```
<p>Kode ini digunakan untuk menggabungkan dua dataset (dat1 dan dat2) menjadi satu dataframe baru bernama datjoin menggunakan fungsi pd.concat() dari library Pandas. Argumen ignore_index=True memastikan bahwa indeks dari hasil gabungan akan di-reset secara berurutan, sehingga tidak mempertahankan indeks asli dari masing-masing dataset. Hal ini berguna saat ingin memperlakukan kedua dataset sebagai satu kesatuan untuk keperluan analisis atau pelatihan model. Selanjutnya, datjoin.columns.values digunakan untuk menampilkan atau mengecek daftar nama kolom (fitur) dari dataframe hasil penggabungan tersebut, untuk memastikan bahwa struktur data konsisten dan tidak terjadi duplikasi atau ketidaksesuaian kolom setelah penggabungan.</p>

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
<p>Array kolom di atas menunjukkan semua fitur (variabel) yang tersedia dalam dataset gabungan datjoin, yang terdiri dari hasil penggabungan dua file CSV: "MQTT DDoS Publish Flood.csv" dan "MQTT DoS Publish Flood.csv". Kolom-kolom ini mencakup berbagai parameter jaringan yang umum digunakan dalam analisis trafik dan deteksi serangan, seperti informasi IP dan port sumber/tujuan, ukuran dan durasi aliran data, statistik interval antar paket (IAT), flag protokol TCP (seperti SYN, ACK, FIN), hingga data agregat seperti packet size, segment size, dan bulk rate. Kolom Attack Name menunjukkan jenis serangan yang terjadi, sementara Label kemungkinan berisi nilai biner atau kategori yang menandai apakah trafik tersebut merupakan serangan atau bukan</p>

```python




