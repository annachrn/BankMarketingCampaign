# Bank Marketing Campaign
Capstone Module 3 - Purwadhika Project 

### **Context**

Bank X berencana meningkatkan valuasinya melaului kampanye dalam pembukaan deposito. Selama ini, Bank X tidak melakukan penawaran secara terukur untuk mengidentifikasi nasabah yang tertarik atau tidak untuk membuka deposito. Menindaklanjuti hal tersebut, Bank X merekrut seorang Strategic Marketing Analyst yang brpengalaman untuk membuat model untuk menyaring nasabah yang tertarik untuk membuka rekening deposito. Dalam memprediksi nasabah yang tertarik ini, Bank X dapat menghemat biaya pemasaran dan mengefisensi waktu. 

### **Problem Statement**

Bank X sering kali mengadakan marketing campaign, namun belum melakukan campaign yang memanfaatkan profil nasabah sehingga campaign cendrung tidak tepat sasaran. Campaign yang tidak efektif dapat memakan biaya dan waktu yang cukup besar.

### **Goals :**
Dari permasalahan tersebut, bank bertujuan untuk mengidentifikasi kategori nasabah ang tertarik untuk melakukan deposito. Dengan cara ini, upaya pemasaran dapat diarahkan kepada nasabah yang berpotensi untuk membuka rekening deposito. 
Untuk mencapai hal ini, bank menerapkan model machine learning untuk menentukan apakah seorang nasabah yang cenderung untuk membuka rekening deposito atau tidak. Akibatnya, bank dapat mendekati segmen pelanggan yang tepat untuk pembukaan rekening deposito.

### **Analytic Approach:**

Sebagai strategic marketing analyst, yang akan saya lakukan adalah membangun model untuk memprediksi nasabah yang cendrung tertarik untuk melakukan deposito atau tidak untuk meminimalisir biaya marketing. 
Saya akan membangun model dengan metode supervised learning karena datanya sudah memiliki label, dalam hal ini adalah deposit yang akan menjadi target label 
Adapun metode supervised learning yang digunakan adalah jenis klasifikasi yang akan membantu perusahaan untuk dapat menganalisis efektivitas kampanye pemasaran sebelumnya dengan memeriksa jumlah kontak, waktu kontak, hasil kampanye sebelumnya, dan interaksi pelanggan.

### **Tahapan Pekerjaan:**
1. Data understanding -> untuk memahami data
2. Data cleaning -> untuk membersihkan data (seperti missing value, outlier)
3. Data analysis -> suatu proses analisis data yang digunakan untuk menyelidiki berbagai fitur (variabel) dalam dataset, memahami strukturnya, mengidentifikasi pola, dan menarik kesimpulan awal (dari fitur numerikal dan kategorikal)
4. Data preparation -> feature engineering dan feature scalling
5. Modelling and evaluation
   
   > Membuat model menggunakan beberapa model untuk mencari model terbaik:
   a. Logistic Regression
   b. K-Nearest Neighbors (KNN)
   c. Decision Trees
   d. Random Forest
   e. Extreme Gradient Boosting (XGB)
   f. Light Gradient Boosting Machine (LGBM)

   > Melakukan cross validation, oversampling menggunakan RandomOverSampler, dan hyperparamater tunning dengan paramater sebagai berikut:
   Hyperparamater yang digunakan:
   a. `model__learning_rate`
       Ini adalah hyperparameter yang mengontrol laju pembelajaran dari model Lightbm yang digunakan. Laju pembelajaran (learning rate) adalah seberapa besar langkah yang diambil olehalgoritma optimisasi pada 
       setiap iterasi untuk memperbarui bobot model. Rentang nilai yang digunakan adalah [0.1, 0.075, 0.125, 0.05], yang akan dicoba  empat nilai yang berbeda untuk hyperparameter ini selama proses tuning.
   b. `model__estimators`: Ini adalah hyperparameter yang mengontrol jumlah estimator atau pohon dalam model ensemble. Jumlah estimator ini mempengaruhi kompleksitas model ensemble dan dapat memengaruhi 
       kinerjanya. Rentang nilai yang dipakai adalah [100,200, 300, 400, 500, 600, 700, 800, 900, 1000].
   Pipeline model machine learning:

   ![image](https://github.com/annachrn/BankMarketingCampaign/assets/150541362/464ca6ad-5624-4a3b-b365-b87c5a39d0cb)

   
### **Kesimpulan:**

Model akhir yang kita gunakan adalah model Light Gradient Boosting Machine (LightGBM) yang sudah dilakukan tunning. 
![image](https://github.com/annachrn/BankMarketingCampaign/assets/150541362/c48e7d2e-872f-421e-a4ed-3a1a93f11dcc)

Jika kita menggunakan model tersebut untuk menyaring/memilih nasabah untuk penawaran deposito, model tersebut dapat mengurangi 77% nasabah yang tidak tertarik melakukan deposito untuk kita approach dan 60% nasabah yang diprediksi tertarik untuk kita approach.

Model kita ini memiliki ketepatan prediksi nasabah yang tertarik sebesar 68% (precisionnya), jadi setiap model kita memprediksi bahwa seorang nasabah itu tertarik, maka kemungkinan tebakannya benar itu sebesar 68%.

Analisis bisnis:

Diasumsikan biaya pemasaran untuk satu pelanggan sekitar Rp50.000, kita memiliki total pelanggan 1000, di antaranya 500 tidak ingin membuka rekening deposito dan 500 ingin membuka rekening deposito, maka hitungannya kurang lebih akan seperti ini :


**Tanpa Model:**

- Total Biaya => 1000 x Rp50.000 = Rp50.000.000
- Total Nasabah Tertarik yang didapatkan => 1000 orang (karena semua nasabah ditawarkan)
- Total Kandidat Tertarik yang tidak didapatkan => 0 orang (karena semua kita tawarkan)
- Biaya yang terbuang => 500 x Rp50.000 = Rp25.000.000 (karena 500 orang menolak dan menjadi sia-sia)

**Dengan Model:**

Dengan Model (hanya nasabah yang diprediksi oleh model tertarik yang kita check dan tawarkan) :
- Total Biaya => (300 x Rp50.000) + (115 x Rp50.000) = Rp15.000.000 + Rp5.750.000 = Rp 20.750.0000
- Total Kandidat Tertarik yang didapatkan => 300 orang (karena recall 1/yg tertarik itu 60%)
- Total Kandidat Tertarik yang tidak didapatkan => 200 orang (karena recall 1/yg tertarik itu 60%)
- Biaya yang terbuang => 115 x Rp50.000 =Rp5.750.000 (berdasarkan recall 0/yg tidak tertarik (115 orang menolak tawaran/tidak tertarik))
- Jumlah penghematan => 77 x Rp50.000 = Rp3.850.000

**Selisih tanpa model dan dengan model: 50.000.000 - 20.750.000 = Rp29.250.000**

Berdasarkan perhitungan di atas, dapat disimpulkan bahwa dengan menggunakan model yang dibuat, bank dapat mengurangi biaya pemasaran dan potensi kerugian profit dari seorang pelanggan.

Model ini dapat digunakan oleh:
Bank’s Marketing Team. 


### **Rekomendasi:**
For business:
Hal-hal yang bisa dilakukan untuk mengembangkan project dan modelnya lebih baik lagi :
1. Mendekati prospek pada awal periode bank baru (Mei-Juli) akan menjadi pilihan yang baik karena banyak yang telah menunjukkan hasil positif dari riwayat data.
2. Fokuskan kampanye deposito pada nasabah yang tidak memiliki cicilan KPR rumah dan pinjaman, karena analisis menyarankan bahwa nasabah tanpa cicilan KPR rumah lebih cenderung terlibat dengan penawaran deposito.
3. Membuka prospek yang lebih luas untuk menghubungi nasabah tidak terbatas dari nomor handphone (celluler) atau nomor telepon rumah. Karena banyak nasabah yang tidak memiliki device tersebut.
4. Semakin dekat hari dari kontak terakhir dengan klien dari kamapanye pemasaran sebelumnya tidak menjamin nasabah untuk tertarik membuka deposito. Jadi, setelah kampanye dilakukan tidak perlu terburu-buru untuk menghubungi nasabah karena dalam kurun waktu yang dekat dari kampanye dilakukan kemungkinan nasabah masih dalam pertimbangan.
5. Perlu ada pembaharuan data nasabah secara berkala karena berdasarkan data nasabah yang sudah pensiun, nasabah yang statusnya masih student dan nasabah yang tidak memiliki pekerjaan cendrung lebih tertarik untuk melakukan deposito.

For model: 
1. Akan lebih baik bila ada fitur durasi kontak saat melakukan penawaran deposito kepada nasabah untuk mempertajam analisis.
2. Akan lebih baik bila ada fitur suku bunga deposito yang ditawarkan, yang dapat berpotensi mempengaruhi keputusan seseorang untuk terlibat dalam deposito.
3. Mencoba algorithm ML yang lain dan juga mencoba hyperparameter tuning kembali, coba gunakan teknik oversampling yang berbeda juga selain Random Over Sampling, seperti SMOTENC, SMoTENN, dll.

### **Limitasi Model**
1. Limitasi pada fitur `job` :
   
Model hanya mampu memprediksi pelanggan dengan peran pekerjaan yang terdaftar sebagai admin, services, housemaid, technician, management, student, blue collar, entrepreneur, retired, self-employed, unemployed. Untuk peran pekerjaan yang tidak ada dalam kolom, akan dikategorikan sebagai  `unknown` dan akan memberikan bias pada data. 

2.  Limitasi pada fitur `contact`:
    
Selama proses pembuatan model, opsi contact yang tersedia adalah celluler, telephone, dan unknown. Oleh karena itu, ketika menemui data yang tidak dapat ditentukan, bisa dikategorikan sebagai tidak diketahui, meskipun ini mungkin memperkenalkan bias ke dalam data.

3. Limitasi pada fitur `balance`:

Selama proses pembuatan model, saldo (balance) nasabah di kategorisasi menjadi very low, low, medium dan high. Very low dilihat dari kategori nasabah yang memiliki nilai minimum dari saldo sedangkan nilai high adalah saldo diatas 5000 (melihat nilai maksimum dari saldo nasabah) 
Kategori tersebut bisa disesuaikan dengan saldo nasabah yang cendrung fluktuatif. 

   


  
