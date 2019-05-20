# Apa itu *K-Nearest Neighbour??*

## 

IAlgoritme *k-nearest neighbor* (k-NN atau KNN) adalah sebuah metode untuk melakukan [klasifikasi](https://id.wikipedia.org/wiki/Pengenalan_pola) terhadap objek berdasarkan data pembelajaran yang jaraknya paling dekat dengan objek tersebut.

Data pembelajaran diproyeksikan ke ruang berdimensi banyak, dimana masing-masing dimensi merepresentasikan fitur dari data. Ruang ini dibagi menjadi bagian-bagian berdasarkan klasifikasi data pembelajaran. Sebuah titik pada ruang ini ditandai kelas *c* jika kelas *c* merupakan klasifikasi yang paling banyak ditemui pada *k* buah tetangga terdekat titk tersebut. Dekat atau jauhnya tetangga biasanya dihitung berdasarkan jarak Euclidean.

Pada fase pembelajaran, algoritme ini hanya melakukan penyimpanan vektor-vektor fitur dan klasifikasi dari data pembelajaran. Pada fase klasifikasi, fitur-fitur yang sama dihitung untuk data test (yang klasifikasinya tidak diketahui). Jarak dari vektor yang baru ini terhadap seluruh vektor data pembelajaran dihitung, dan sejumlah *k* buah yang paling dekat diambil. Titik yang baru klasifikasinya diprediksikan termasuk pada klasifikasi terbanyak dari titik-titik tersebut.

Nilai *k* yang terbaik untuk algoritme ini tergantung pada data; secara umumnya, nilai *k* yang tinggi akan mengurangi efek *noise* pada klasifikasi, tetapi membuat batasan antara setiap klasifikasi menjadi lebih kabur. Nilai *k* yang bagus dapat dipilih dengan optimasi parameter, misalnya dengan menggunakan cross-validation. Kasus khusus di mana klasifikasi diprediksikan berdasarkan data pembelajaran yang paling dekat (dengan kata lain, *k* = 1) disebut algoritme *nearest neighbor*.

Ketepatan algoritme k-NN ini sangat dipengaruhi oleh ada atau tidaknya fitur-fitur yang tidak relevan, atau jika bobot fitur tersebut tidak setara dengan relevansinya terhadap klasifikasi. Riset terhadap algoritme ini sebagian besar membahas bagaimana memilih dan memberi bobot terhadap fitur, agar performa klasifikasi menjadi lebih baik.

Terdapat beberapa jenis algoritme pencarian tetangga terdekat, diantaranya:

- Linear scan
- Pohon kd
- Pohon Balltree
- Pohon metrik
- Locally-sensitive hashing (LSH)

Algoritme k-NN ini memiliki konsistensi yang kuat. Ketika jumlah data mendekati tak hingga, algoritme ini menjamin *error rate* yang tidak lebih dari dua kali *Bayes error rate* (*error rate* minimum untuk distribusi data tertentu).



sumber: <https://id.wikipedia.org/wiki/KNN>

## Kelebihan dan Kekurangan *KNN*

**Kelebihan**

- Sangat nonlinear

  - kNN merupakan salah satu algoritma (model) pembelajaran mesin yang bersifat nonparametrik. Pembahasan mengenai ***model parametrik*** dan mode l***nonparametrik*** bisa menjadi artikel sendiri, namun secara singkat, definisi model nonparametrik adalah model yang tidak mengasumsikan apa-apa mengenai distribusi instance di dalam dataset. Model nonparametrik biasanya lebih sulit diinterpretasikan, namun salah satu kelebihannya adalah garis keputusan kelas yang dihasilkan model tersebut bisa jadi sangat fleksibel dan nonlinear.

    

    *Perbandingan garis keputusan kelas kNN (garis putus-putus abu-abu) dengan model klasifikasi linear (garis lurus ungu)*

     

    Pada ilustrasi di atas, kNN dapat melakukan klasifikasi dengan tepat karena garis keputusan kelasnya nonlinear. Bandingkan dengan model linear (**e.g. logistic regression**) yang tentunya akan menghasilkan banyak misklasifikasi jika garis keputusan kelas dalam *dataset* sebenarnya bersifat nonlinear.

- Mudah dipahami dan diimplementasikan

  - Dari paparan yang diberikan dan penjelasan cara menghitung jarak dalam artikel ini, cukup jelas bahwa algoritma kNN mudah dipahami dan juga mudah dimplementasikan. Untuk mengklasifikasi instance x menggunakan kNN, kita cukup mendefinisikan fungsi untuk menghitung jarak antar-instance, menghitung jarak x dengan semua instance lainnya berdasarkan fungsi tersebut, dan menentukan kelas x sebagai kelas yang paling banyak muncul dalam k instance terdekat.

    **Kekurangan**

    - [ ] Perlu menunjukkan parameter K (jumlah tetangga terdekat)

    - [ ] Tidak menangani nilai hilang (missing value) secara implisit

      - Jika terdapat nilai hilang pada satu atau lebih variabel dari suatu instance, perhitungan jarak instance tersebut dengan instance lainnya menjadi tidak terdefinisi. Bagaimana coba, menghitung jarak dalam ruang 3-dimensi jika salah satu dimensi hilang? Karenanya, sebelum menerapkan kNN kerap dilakukan **imputasi** untuk mengisi nilai-nilai hilang yang ada pada dataset. Contoh teknik imputasi yang paling umum adalah mengisi nilai hilang pada suatu variabel dengan nilai rata-rata variabel tersebut (mean imputation).

        - [ ] Sensitif terhadap data pencilan (outlier)

        Seperti yang telah dijelaskan Ali pada artikel sebelumnya, kNN bisa jadi sangat fleksibel jika k kecil. Fleksibilitas ini mengakibatkan kNN cenderung sensitif terhadap data pencilan, khususnya pencilan yang terletak di “tengah-tengah” kelas yang berbeda. Lebih jelasnya, perhatikan ilustrasi di bawah. Pada gambar kiri, seluruh instance bisa diklasifikasikan dengan benar ke dalam kelas biru dan jingga. Tetapi, ketika ditambahkan instance biru di antara instance jingga, beberapa instance jingga menjadi salah terklasifikasi.Perlu dipilih k yang tepat untuk mengurangi dampak data pencilan dalam kNN.

        ![](assets\images\data m.JPG)

    

- [ ] Rentan terhadap variabel yang non-informatif

  Meskipun kita telah menstandardisasi rentang variabel, kNN tetap tidak dapat mengetahui variabel mana yang signifikan dalam klasifikasi dan mana yang tidak. Lihat contoh berikut:

  irrelevant variabel non-informatif

  Pada ilustrasi di atas, klasifikasi sebetulnya bisa dilakukan menggunakan variabel a saja (perhatikan garis vertikal yang memisahkan kedua kelas secara linear). Namun, kNN tidak dapat mengetahui bahwa variabel b tidak informatif. Alhasil, dua instance kelas biru terklasifikasi dengan salah, karena kedua instance tersebut dekat dengan instance kelas jingga dalam dimensi b. Andaikan kita hanya menggunakan variabel a dan membuang variabel b, semua instance akan terklasifikasi dengan tepat.Pemilihan variabel sebelum menerapkan kNN dapat membantu menangani permasalahan di atas. Selain itu, kita juga bisa memberi bobot pada variabel dalam perhitungan jarak antar-instance. Variabel yang kita tahu noninformatif kita beri bobot yang kecil.

  - [ ] Rentan terhadap dimensionalitas yang tinggi

    Berbagai permasalahan yang timbul dari tingginya dimensionalitas (baca: banyaknya variabel) menimpa sebagian besar algoritma pembelajaran mesin, dan kNN adalah salah satu algoritma yang paling rentan terhadap tingginya dimensionalitas. Hal ini karena semakin banyak dimensi, ruang yang bisa ditempati instance semakin besar, sehingga semakin besar pula kemungkinan bahwa nearest neighbour dari suatu instance sebetulnya sama sekali tidak “near“.

    ![](assets\images\da m.JPG)

dimensi data knn

Masalah tingginya dimensionalitas (terkadang) bisa diatasi dengan **pemilihan variabel** atau **rekayasa fitur**, misalnya dengan **PCA**.

- [ ] Rentan terhadap perbedaan rentang variabel

  Dalam perhitungan jarak antar-instance, kNN menganggap semua variabel setara atau sama penting (lihat bagian penjumlahan pada rumus perhitungan jarak di atas). Jika terdapat variabel p yang memiliki rentang jauh lebih besar dibanding variabel-variabel lainnya, maka perhitungan jarak akan didominasi oleh p. Misalkan ada dua variabel, a dan b, dengan rentang variabel a 0 sampai 1.000 dan rentang variabel b 0 sampai 10. Kuadrat selisih dua nilai variabel b tidak akan lebih dari 100, sedangkan untuk variabel a kuadrat selisihnya bisa mencapai 1.000.000. Hal ini bisa mengecoh kNN sehingga kNN menganggap a tidak membawa pengaruh dalam perhitungan jarak karena rentangnya sangat besar dibanding rentang b.Ilustrasinya diberikan di bawah ini. Manakah yang merupakan nearest neighbour dari instance x? Jika dilihat dari “kacamata” komputer, nearest neighbour x bukanlah y, melainkan z, Mengapa?

  Untuk mengatasi perbedaan rentang, biasanya dilakukan preproses berupa standardisasi rentang semua variabel sebelum menerapkan algoritma kNN. Contohnya yaitu melalui

   operasi centre-scale atau operasi min-max skala dataset knn

  ![](assets\images\daata.JPG)

  Nilai komputasi yang tinggi.

  Untuk mengklasifikasi sebuah instance x, kNN harus menghitung jarak antara x dengan semua instance lain dalam dataset yang kita miliki. Dengan kata lain, kompleksitas waktu klasifikasi kNN berbanding lurus dengan jumlah instance latih. Jika dataset yang kita miliki berukuran besar (terdiri dari banyak instance dan/atau banyak variabel), proses ini bisa jadi sangat lambat. Bayangkan, jika kita punya 10.000 instance dengan masing-masing 20 variabel dan kita ingin mengklasifikasi 100 instance baru (instance uji), maka total operasi yang harus dilakukan menjadi:**(100 instance uji x 10.000 instance latih) x 20 variabel/instance x 2 operasi/variabel = 40 juta operasi**Beberapa cara pengindexan (K-D tree) dapat digunakan untuk mereduksi biaya komputasi.

  

  ## Contoh perhitngan KNN  data Iris dengan bahasa python

  #### Importing Libraries

  ```python
  from sklearn import datasets
  import pandas as pd
  ```

### Importing the Dataset

untuk menginportkan data ke dalam program:

```python
from sklearn.linear_model import logistic_regression_path

iris=datasets.load_iris()

print(iris.data)
print(iris.target)
```



## Train Test Split

Untuk menghindari pemasangan berlebihan, kami akan membagi dataset kami menjadi pelatihan dan pemisahan uji, yang memberi kami ide yang lebih baik tentang bagaimana algoritma kami dilakukan selama fase pengujian. Dengan cara ini, algoritma kami diuji pada data yang tidak terlihat, seperti pada aplikasi produksi.

Untuk membuat pelatihan dan menguji pemisahan, jalankan skrip berikut:

``` python
from sklearn.model_selection import train_test_split
x_train, x_test, y_train, y_test=train_test_split(iris.data,iris.target,test_size=0.33)
```

### Training dan Prediksi

* Langkah pertama adalah mengimpor kelas KNeighborsClassifier dari perpustakaan sklearn.neighbors. Di baris kedua, kelas ini diinisialisasi dengan satu parameter, yaitu n_neigbours. Ini pada dasarnya adalah nilai untuk K. Tidak ada nilai ideal untuk K dan dipilih setelah pengujian dan evaluasi, namun untuk memulai, 5 tampaknya menjadi nilai yang paling umum digunakan untuk algoritma KNN.

  ```python
  from sklearn.neighbors import KNeighborsClassifier
  clf=KNeighborsClassifier(n_neighbors=3).fit(x_train,y_train)
  ```

#### Accuration

```python
from sklearn.metrics import accuracy_score
print("accuracy is ")
print(accuracy_score(y_test,clf.predict(x_test)))

import matplotlib.pyplot as plt

accuracy_values=[]
```



#### Comparing Error Rate with the K Value

* Salah satu cara untuk membantu Anda menemukan nilai K terbaik adalah dengan memplot grafik nilai K dan tingkat kesalahan yang sesuai untuk dataset.
  
  Di bagian ini, kami akan memplot kesalahan rata-rata untuk nilai prediksi set tes untuk semua nilai K antara 1 dan 40.

  Untuk melakukannya, pertama-tama mari kita menghitung rata-rata kesalahan untuk semua nilai yang diprediksi di mana K berkisar dari 1 dan 40. Jalankan skrip berikut:
  
  ```python
  import numpy as np
  accuracy_values=np.array(accuracy_values)
  
  plt.plot(accuracy_values[:,0],accuracy_values[:,1])
  plt.xlabel("K")
  plt.ylabel("accuracy")
  plt.show()
  ```
  
  

### output

![](assets\images\ex.JPG)

![](assets\images\ey.JPG)

![](assets\images\ez.JPG)



### grafik

![](assets\images\grafik.JPG)