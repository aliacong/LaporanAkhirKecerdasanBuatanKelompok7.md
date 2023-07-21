# Laporan Akhir Kecerdasan Buatan - Kelompok 7

**Anggota Kelompok :**

1. Chaidir Ali - NIM. 3.34.21.1.07
2. Widigda Rahma Mukti - NIM. 3.34.21.1.24

## Domain Proyek

Fakta dan angka diabetes menunjukkan beban global yang meningkat bagi individu, keluarga, dan negara. Atlas Diabetes IDF (2021) melaporkan bahwa 10,5% populasi orang dewasa (20-79 tahun) menderita diabetes, dengan sebagian besar tidak menyadari kondisinya [1]. Fakta ini menyoroti betapa pentingnya kesadaran akan penyakit Diabetes, karena hampir setengah dari penderita diabetes tidak menyadari bahwa mereka mengidap penyakit diabetes. Hal ini menekankan perlunya meningkatkan pemahaman tentang diabetes untuk mengatasi tantangan ini secara efektif. dengan adanya machine learning dalam memprediksi penyakit diabetes masyarakat akan terbantu dalam mendapatkan informasi yang lebih akurat dan mendalam tentang risiko diabetes serta tindakan pencegahan yang tepat.

terdapat beberapa parameter untuk memprediksi penyakit diabetes. diantaranya yaitu tingkat HbA1c dan tingkat Glukosa Darah dan lain sebagainya [2]. Salah satu bidang penelitian pembelajaran mesin yang digunakan untuk prediksi adalah regresi. Algoritma regresi dapat memprediksi nilai variabel target berdasarkan nilai variabel input (atau fitur). Beberapa penelitian terlibat dalam memprediksi diabetes.  Salah satu diantaranya adalah penelitian yang dilakukan oleh [3] yang memprediksi harga Penyakit Diabetes menggunakan beberapa algoritma machine learning seperti Random Forest, Logistic Regression, Decision Tree, K-Nearest Neighbor, dan SVC.

# Business Understanding

Tiap tahun, jumlah kejadian penyakit diabetes terus naik. Ini memicu keperluan untuk memahami situasi ini secara lebih dalam. Sebagai contoh, penting bagi masyarakat untuk meningkatkan kesadaran akan faktor risiko, tanda-tanda, dan cara pencegahan penyakit diabetes. Pengetahuan tentang pentingnya pola makan bergizi, aktivitas fisik, dan pengendalian berat badan juga menjadi kunci dalam menghadapi diabetes. Maka dari itu, penggunaan model pembelajaran mesin dalam memperkirakan penyakit diabetes dapat memberikan bantuan bagi masyarakat. Dengan adanya model tersebut, masyarakat dapat mendapatkan informasi yang lebih tepat dan dalam tentang risiko mereka terkena diabetes, sehingga mereka dapat mengambil tindakan pencegahan yang sesuai.

#### Problem Statements

Berdasarkan masalah yang telah dijelaskan, masalah untuk proyek ini adalah sebagai berikut.

1. Parameter apa yang paling mempengaruhi Diabetes ?
2. Apa proses preprocessing untuk membangun model pembelajaran mesin yang akurat?
3. Bagaimana cara membangun model pembelajaran mesin dengan akurasi tertinggi untuk memprediksi diabetes?

#### Goals

Tujuan untuk mencapai proyek ini adalah sebagai berikut:

1. menentukan karakteristik yang paling berkorelasi dengan diagnosis diabetes.
2. Bangun model pembelajaran *machine learning* yang dapat memprediksi diabetes.
3. Pilih model machine learning yang memberikan prediksi paling akurat berdasarkan proses preprocessing yang dilakukan.

####  Solution Statements

Solusi yang diusulkan untuk memecahkan masalah yang dijelaskan adalah sebagai berikut.

1. Lakukan analisis deskriptif untuk menemukan pola dalam data dan informasi tentang variabel atau parameter yang mempengaruhi diabetes.
2. Lakukan proses manipulasi data untuk menggabungkan kolom-kolom yang mempengaruhi akurasi prediksi diabetes. 
3. Melakukan proses pra-pemrosesan seperti:
   - memeriksa apakah nilai *missing value* dan duplikasi data dan *Outlier*. Jika tidak, tidak ada nilai yang hilang atau duplikat data dalam kumpulan data yang digunakan.
   - Menghapus Outlier karena Outlier adalah entri yang jauh di atas atau jauh di bawah distribusi rata-rata data.
   - Jalankan visualisasi data untuk melihat distribusi dan korelasi antar kolom
   - Membagi data menjadi set pelatihan dan tes dengan persentase 80% dan 20%. Alasan menggunakan 20% karena jumlah data yang digunakan besar, sehingga hanya dengan 20% Anda mendapatkan banyak data uji. Pengkodean kolom objek/kategori menggunakan fungsi peta.
4. Lakukan pemilihan model
   - Memilih 5 algoritma yang menghasilkan model dengan performa terbaik
   - Kinerja model terbaik tercermin dalam kesalahan kuadrat rata-rata (MSE), kesalahan kuadrat akar rata-rata (RMSE), dan kesalahan R-kuadrat (R2).

## Data Understanding

Dataset yang digunakan dalam proyek ini diambil dari dokumentasi dari Kaggle. Klik tautan berikut:  [Diabetes prediction dataset](https://www.kaggle.com/datasets/iammustafatz/diabetes-prediction-dataset) untuk mengakses dataset yang dipakai. berikut variabel variabe yang yang ada pada dataset :

1. **gender**: Jenis kelamin
2. **age**: Umur
3. **hypertension**: Model Handphone
4. **heart_disease**: Penyakit jantung
5. **smoking_history**: Riwayat merokok
6. **bmi**:Indeks Massa Tubuh
7. **HbA1c_level**: mengukur rata-rata jumlah sel darah merah atau hemoglobin
8. **blood_glucose_level**: Kadar glukosa darah
9. **diabetes**: indikasi diabetes

Pada dataset, terdapat 4 fitur numerikal dan 5 fitur kategorikal. Ringkasan statistik dari data-data numerikal dapat dilihat pada Tabel 1.

<div style="text-align:center">Tabel 1. Ringkasan Statistik Deskriptif</div>

|           |    age    | hypertension | heart_disease |    bmi    | HbA1c_level | blood_glucose_level | diabetes  |
| :-------: | :-------: | :----------: | :-----------: | :-------: | :---------: | :-----------------: | :-------: |
| **count** | 100000.00 |  100000.00   |   100000.00   | 100000.00 |  100000.00  |      100000.00      | 100000.00 |
| **mean**  |   41.89   |     0.07     |     0.04      |   27.32   |    5.53     |       138.06        |   0.09    |
|  **std**  |   22.52   |     0.26     |     0.19      |   6.64    |    1.07     |        40.71        |   0.28    |
|  **min**  |   0.08    |     0.00     |     0.00      |   10.01   |    3.50     |        80.00        |   0.00    |
|  **25%**  |   24.00   |     0.00     |     0.00      |   23.63   |    4.80     |       100.00        |   0.00    |
|  **50%**  |   43.00   |     0.00     |     0.00      |   27.32   |    5.80     |       140.00        |   0.00    |
|  **75%**  |   60.00   |     0.00     |     0.00      |   29.58   |    6.20     |       159.00        |   0.00    |
|  **max**  |   80.00   |     1.00     |     1.00      |   95.69   |    9.00     |       300.00        |   1.00    |

Pada tahap *Data Understanding* dilakukan analisis data eksploratif untuk mendapatkan wawasan tentang karakteristik data, memahami struktur data, dan mengidentifikasi potensi masalah atau kesalahan yang mungkin terjadi. Kegiatan Data Understanding yang dilakukan pada Proyek ini antara lain :

- Memberikan informasi seperti jumlah data, *missing value*, duplikasi data, korelasi antar kolom, dan sebaran data.
- Melakukan manipulasi data karena *machine learning* dapat dilakukan dengan angka, hanya angka. Jadi pada dasarnya mengubah data menjadi angka.
- Melakukan visualisasi data untuk mengetahui korelasi dan sebaran data. gambaran korelasi antar kolom di gambarkan pada Gambar 1. Seperti yang bisa kita lihat di Heat Map, Tingkat HbA1c dan Tingkat Glukosa Darah berkorelasi dengan diabetes. Ini mungkin membantu melacak pola distribusi data. Faktanya, setiap fitur lainnya berkorelasi dengan diabetes, namun tingkat korelasinya tidak tinggi seperti fitur yang disebutkan.

<div style="text-align:center">Gambar 1. Visualisasi Korelasi Data menggunakan Heatmap</div>

![Gambar1](C:\Users\Lenovo\Pictures\heatmap.png)

contoh gambaran dari sebaran data ditunjukan pada Gambar 2 berikut . Visualisasi yang ditunjukan pada Gambar 2 menunjukan bahwa ada ketidakseimbangan data pada kolom gender, smoking_history, hypertension, dan heart_disiase.

<div style="text-align:center">Gambar 2. Visualisasi Data pada Data
</div>

![Gambar2](C:\Users\Lenovo\Pictures\download.png)

## Data Preparation

Teknik data preparation yang dilakukan pada proyek ini adalah sebagai berikut : 

1. Feature Selection : Melakukan seleksi fitur untuk menyeleksi kolom yang berperan sebagai data fitur dan kolom yang menjadi data label.

2. Data Splitting: Membagi dataset menjadi data latih dan data uji. Pada proyek ini perbandingan data latih dan data uji adalah 80 : 20.

3. Menampilkan informasi jumlah data latih dan data uji. Jumlah data latih adalah 79958, sedangkan data uji terdat 19990 data. jumlah data fitur yang dipakai untuk pelatihan adalah 8.

## Modelling

Pada tahap ini dilakukan proses pelatihan untuk mendapatkan model dengan performa terbaik. Logistic Regression,  Decision Tree classifier, K Neighbor classification , Random Forest calssification, dan SVC. algoritma tersebut memiliki kecenderungan untuk memberikan hasil yang baik dalam prediksi penyakit diabetes.

- Logistic Regression

  Logistic Regression adalah sebuah algoritma pembelajaran *machine learning* yang dapat digunakan untuk permasalahan klasifikasi biner. Algoritma ini menggunakan fungsi logistik (sigmoid) untuk memodelkan probabilitas kelas target sebagai fungsi linier dari fitur-fitur input. Hasilnya adalah prediksi probabilitas untuk setiap kelas, dan kelas dengan probabilitas tertinggi dianggap sebagai prediksi akhir.

- Decision Tree Classifier

  Decision Tree Classifier menggunakan struktur pohon untuk memprediksi kelas target berdasarkan serangkaian aturan dan fitur-fitur data. Setiap simpul dalam pohon mewakili pengujian pada fitur tertentu, sedangkan cabang-cabangnya merepresentasikan kemungkinan hasil dari pengujian tersebut. Prediksi kelas dibuat dengan mengikuti jalur dari akar pohon ke daun yang sesuai dengan fitur-fitur data.

- K Neighbor Classification

  K-Nearest Neighbors adalah algoritma klasifikasi yang menggunakan jarak antara data untuk memprediksi kelas target. Algoritma ini mencari K titik data terdekat dari data yang akan diprediksi, dan mayoritas kelas dari tetangga terdekat tersebut digunakan sebagai prediksi akhir.

- Random Forest Classification

  Random Forest adalah kumpulan pohon keputusan yang digunakan untuk masalah klasifikasi. Algoritma ini menggunakan konsep ensemble learning, di mana beberapa pohon keputusan dibangun secara acak dan hasil prediksi dari setiap pohon digabungkan untuk menghasilkan prediksi akhir. Setiap pohon bekerja secara independen dan menghasilkan prediksi berdasarkan subkumpulan fitur dan data yang diambil dengan penggantian.

- Support Vector Machines (SVC)

  SVM merupakan algoritma pembelajaran *machine learning* yang digunakan untuk pengklasifikasian serta regresi. Dalam konteks klasifikasi, SVM mencari hyperplane terbaik yang memisahkan dua kelas data dengan margin terbesar. Hyperplane ini dipilih sedemikian rupa sehingga jarak antara data paling dekat dengan hyperplane (disebut vektor pendukung) dan hyperplane itu sendiri maksimal. SVM juga dapat menggunakan fungsi kernel untuk mengatasi kasus ketika data tidak linear terpisah secara linier di ruang fitur asli.

## Evaluation

- Metrik evaluasi yang digunakan adalah *Mean Square Error* (MSE), *Root Mean Square Error* (RMSE), dan *R Square* (R2 Score)

- MSE mengurangi nilai data aktual dari data perkiraan dan hasilnya dikuadratkan (*kuadrat*) dan dijumlahkan dan dibagi dengan jumlah data yang ada.  Rumus dari MSE adalah sebagai berikut 
  $$
  MSE = \frac{1}{n} \Sigma_{i=1}^n({y}-\hat{y})^2
  $$
  Diketahui:

  - n = Jumlah Data
  - yi = *Actual Value* / Nilai Sebenarnya
  - ŷi = *Predicted Value* / Nilai Prediksi

- RMSE adalah jumlah kesalahan kuadrat atau perbedaan antara nilai aktual dan nilai prediksi. Satu-satunya cara untuk menghitungnya adalah dengan melakukan root pada mse dengan fungsi *np.sqrt*.  Rumus dari RMSE adalah sebagai berikut.
  $$
  RMSE = \sqrt{(\frac{1}{n})\sum_{i=1}^{n}(y_{i} - x_{i})^{2}}
  $$
  Diketahui:

  - n = Jumlah Data
  - yi = *Actual Value* / Nilai Sebenarnya
  - ŷi = *Predicted Value* / Nilai Prediksi

- Nilai skor R2 digunakan sebagai ukuran seberapa baik garis regresi mendekati nilai data asli yang ditentukan oleh model.  Rumus dari R2 Score adalah sebagai berikut.
  $$
  R^2 = 1 - {SS_R \over SS_T} =  1 - {\sum_{i} (y_i - ŷ_p) ^ 2 \over \sum_{i} (y_i - ȳ) ^ 2}
  $$

  - SSR : Kuadrat dari selisih nilai Y prediksi dengan nilai rata-rata Y = ∑ (Ypred – Yrata-rata)²
  - SST : Kuadrat dari selisih nilai Y aktual dengan nilai rata-rata Y = ∑ (Yaktual – Yrata-rata)²

- Setelah melalui tahap pelatihan dan evaluasi menggunakan MSE, RMSE, dan R Square, diperoleh hasil bahwa algoritma **Random Forest Classification** memiliki performa yang paling baik seperti ditunjukan Tabel 3. Maksud performa yang paling baik adalah memiliki nilai MSE dan RMSE yang mendekati nilai 0, serta memiliki nilai R2 Score yang mendekati nilai 1.

  <div style="text-align:center">Tabel 3. Hasil Pengujian dari 3 Algoritma Teratas</div>

  |  id  | Model Name                    | MSE                 | R2 Score           | RMSE                |
  | :--: | :---------------------------- | ------------------- | ------------------ | ------------------- |
  |  1   | Logistic-Regression           | 0.04042021010505253 | 0.9595797898949475 | 0.2010477806518951  |
  |  2   | Decision Tree Classifier      | 0.04842421210605303 | 0.9515757878939469 | 0.22005502063359753 |
  |  3   | K-Neighbor Classification     | 0.04062031015507754 | 0.9593796898449225 | 0.20154480929827376 |
  |  4   | Random Forest Classification  | 0.02991495747873937 | 0.9700850425212606 | 0.17295940991671824 |
  |  5   | Support Vector Machines (SVC) | 0.03666833416708354 | 0.9633316658329164 | 0.19148977562022348 |

## Conclussion

1. Berdasarkan hasil pengukuran, terdapat 8 kolom atau fitur yang mempengaruhi Diabetes yaitu gender, age, hypertension, heart_disiase, smoking_history, bmi, HbA1c_level, blood_glucose_level, diabetes.
2. Berdasarkan hasil pengujian model, diperoleh hasil bahwa algoritma Random Forest Classification memiliki performa yang paling baik yaitu memiliki nilai RMSE paling kecil dan R2 Score paling besar.
3. menghilangkan nilai-nilai outlier dari dataset, agar dapat meningkatkan performa atau skor *machine learning*. Outlier adalah nilai yang secara signifikan berbeda dari nilai-nilai lain dalam dataset, dan dapat mempengaruhi analisis atau model pembelajaran mesin. Dengan menghapus nilai-nilai outlier, maka dapat membersihkan dataset dari gangguan yang tidak diinginkan dan meningkatkan akurasi.
4. Rekayasa fitur adalah proses memanipulasi atau mengubah fitur-fitur dalam dataset untuk meningkatkan pemahaman dan kinerja dalam menganalisis data tersebut. Dengan melakukan rekayasa fitur, maka pemahaman komputer terhadap dataset akan meningkat dan analisis data akan menjadi lebih baik.

# Referensi

[1] IDF,"Facts & figures" .Available: https://idf.org/about-diabetes/facts-figures/

[2] Aishwarya Mujumdara, Dr. Vaidehi Vb, "Diabetes Prediction using Machine Learning Algorithms" 2019, doi: https://doi.org/10.1016/j.procs.2020.01.047

[3] Rishab Bothra, "DIABETES PREDICTION USING MACHINE LEARNING ALGORITHMS", doi : [10.33564/IJEAST.2021.v06i05.020](http://dx.doi.org/10.33564/IJEAST.2021.v06i05.020)