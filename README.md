#FinalProject_BankMarketingCampaign
Folder ini berisi Final Project Purwadhika BSD terkait Bank Marketing Campaign

# Bank Marketing Campaign
by: <br>
1. Cindy Fransisca
2. Muhammad Zulfikar Muslim

## 1. Business Understanding

### Context  

Umumnya pendapatan utama suatu bank berasal dari bunga pinjaman yang diberikan kepada nasabah. Pinjaman yang diberikan kepada nasabah itu sendiri umumnya berasal dari deposito nasabah lain. Semakin besar jumlah deposito yang dimiliki sebuah bank, maka semakin besar jumlah pendapatan yang kemungkinan bisa dimiliki oleh sebuah bank. 

Dengan semakin tingginya persaingan antara bank dalam menawarkan produk depositonya, maka salah satu cara pemasaran yang dilakukan adalah dengan melakukan direct marketing. Biasanya nasabah terpilih dihubungi secara langsung melalui: kontak pribadi, telepon seluler, surat, dan email atau kontak lainnya untuk mengiklankan produk/jasa baru atau memberikan penawaran. Akan tetapi, tidak semua nasabah tertarik untuk melakukan deposito sehingga terkadang biaya marketing yang dikeluarkan menjadi sia-sia. 

Tim marketing ingin mengetahui nasabah mana yang berpotensi melakukan deposito sehingga dapat memaksimalkan pendapatan dari deposito dan meminimalisir biaya yang diperlukan untuk marketing.


### Problem Statement :

Bank XYZ merupakan salah satu Bank terkemuka di Portugal yang saat ini tengah mengalami penurunan pendapatan dan mereka ingin mengetahui tindakan apa yang harus diambil. Setelah dilakukan penyelidikan internal, Bank XYZ menemukan bahwa akar masalahnya adalah persentase nasabah yang melakukan deposito di bank masih tergolong rendah. Oleh karenanya Bank XYZ akan menawarkan produk term deposit kepada nasabahnya.

Akan tetapi jika kita menghubungi semua nasabah untuk menawarkan produk deposito tersebut, maka sistem kerja menjadi tidak efisien dan biaya yang diperlukan tinggi. Selain itu dari segi waktu juga kita berpotensi kehilangan kesempatan untuk mendapatkan nasabah potensial lebih cepat karena nasabah yang dihubungi oleh tim marketing saat ini masih dipilih secara acak.

Adapun jika kita hanya menghubungi sebagian nasabah, maka kita bisa kehilangan nasabah yang sebenarnya berpotensi melakukan deposito. Selain itu besarnya sumber data nasabah yang dimiliki juga tidak memungkinkan bagi seorang analis untuk menghasilkan informasi dan melakukan adaptasi terhadap perubahan data yang dinamis dengan cepat.

Oleh karena itu, tim marketing Bank XYZ memerlukan kemampuan untuk memprediksi nasabah mana yang akan tertarik memesan deposito sehingga dapat meminimalisir biaya marketing sekaligus memaksimalkan pendapatan dari deposito.

### Goals :

Maka berdasarkan permasalahan tersebut, tim marketing Bank XYZ ingin mengetahui karakteristik dari pelanggan yang melakukan deposito, sehingga mereka dapat membuat program-program yang lebih tepat sasaran untuk meningkatkan jumlah pelanggan yang melakukan deposito.

Tim marketing juga ingin memiliki kemampuan untuk memprediksi nasabah mana yang akan melakukan deposito, sehingga dapat memfokuskan upaya-upaya pemasaran kepada nasabah tersebut.

Hal ini tidak hanya memungkinkan Bank XYZ untuk memperoleh nasabah deposit secara lebih efektif tetapi juga meningkatkan kepuasan nasabah dengan mengurangi iklan yang tidak diinginkan oleh nasabah tertentu.


### Analytic Approach :

Jadi kita akan menganalisis data untuk menemukan pola yang membedakan nasabah yang melakukan deposito atau tidak.

Kemudian kita akan membangun model klasifikasi yang akan membantu tim marketing untuk dapat memprediksi seorang nasabah akan melakukan deposito atau tidak.

### Evaluation Metric

Karena fokus utama kita adalah nasabah yang melakukan deposito, maka target yang kita tetapkan adalah sebagai berikut:

Target :
- 0 : no (tidak melakukan deposito)
- 1 : yes (melakukan deposito)

Type 1 error : False Positive (nasabah yang aktualnya tidak deposit tetapi diprediksi deposit)\
Konsekuensi: Kerugian dari biaya telemarketing, ketidaknyamanan nasabah

Type 2 error : False Negative (nasabah yang aktualnya deposit tetapi diprediksi tidak akan deposit)\
Konsekuensi: Kehilangan potensi pendapatan dari nasabah potensial

Untuk memberikan gambaran konsekuensi secara kuantitatif, maka kita akan coba hitung dampak biaya berdasarkan asumsi berikut :
- Gaji telemarketing di Portugal sekitar 2450 Euro per bulan.
- Hari kerja dalam sebulan : 22 hari
- Jam kerja dalam sehari : 8 jam
- Upah per jam = 2450 Euro/bulan x (22 hari/ bulan x 8 jam/hari) = 13.92 Euro/jam
- Rata-rata durasi telemarketing per orang sekitar 372 detik.
- Rata-rata jumlah deposit per nasabah sekitar 2500 Euro per orang. ([sumber](https://www.ceicdata.com/en/portugal/banking-indicators/pt-deposit-accounts-per-1000-adults-commercial-banks))
- Interest Rate : 2% ([sumber](https://take-profit.org/en/statistics/interest-rate/portugal/))
- Lending Rate : 3.27% ([sumber](https://take-profit.org/en/statistics/interest-rate/portugal/))

Berdasarkan asumsi di atas maka kita dapat coba kuantifikasi konsekuensinya sebagai berikut :
- Hilangnya biaya dan waktu untuk telemarketing --> maka kita menyia-nyiakan biaya sebesar = 13.92 x 372/3600 = 1.44 Euro per orang
- Hilangnya potensi pendapatan --> maka kita kehilangan potensi pendapatan sebesar = (3.27% - 2%) * 2500 Euro = 31.75 Euro per orang

Berdasarkan konsekuensinya, maka sebisa mungkin yang akan kita lakukan adalah membuat model yang dapat mengurangi jumlah False Negative (nasabah yang aktualnya akan deposit tetapi diprediksi tidak deposit). Selain itu, sebisa mugkin kita juga akan meminimalisir telemarketing yang tidak tepat sasaran. Metric utama yang akan kita gunakan adalah recall karena False Negative memiliki kerugian yang jauh lebih besar



## 2. Data Understanding


- Sumber dataset : https://archive.ics.uci.edu/ml/datasets/bank+marketing
- Periode pembuatan data : Mei 2008 - November 2010
- Dataset menggambarkan hasil marketing campaign dari sebuah bank di Portugal kepada 41.000+ nasabah. Metode marketing yang dilakukan berupa kontak langsung melalui telepon untuk menawarkan program term deposit.
- Setiap baris merepresentasikan informasi dari seorang nasabah dan keadaan sosial-ekonomi dari marketing campaign sebelumnya.
- Terdapat missing values dalam dataset yang diberi label 'unknown'

### Attribute Information


**Informasi demografi nasabah**

| Attribute | Data Type | Description |
| --- | --- | --- | 
|Age |Integer | age of client |
|Job |Text | type of job (categorical: "admin.","blue-collar","entrepreneur","housemaid","management","retired","self-employed","services","student","technician","unemployed","unknown") |
|Marital |Text | marital status (categorical: "divorced","married","single","unknown"; note: "divorced" means divorced or widowed) |
|Education |Text | level of education (categorical: "basic.4y","basic.6y","basic.9y","high.school","illiterate","professional.course","university.degree","unknown") |
|Default |Text | has credit in default? (categorical: "no","yes","unknown") |
|Housing |Text | has housing loan? (categorical: "no","yes","unknown") |
|Loan |Text | has personal loan? (categorical: "no","yes","unknown") |

**Informasi terkait campaign saat ini**

| Attribute | Data Type | Description |
| --- | --- | --- | 
|Contact |Text | contact communication type (categorical: "cellular","telephone") |
|Month |Text | last contact month of year (categorical: "jan", "feb", "mar", …, "nov", "dec") |
|Day_of_week |Text | last contact day of the week (categorical: "mon","tue","wed","thu","fri") |
|Duration |Integer | last contact duration, in seconds. Important note: this attribute highly affects the output target (e.g., if duration=0 then y="no") |
|Campaign |Integer | number of contacts performed during this campaign and for this client (numeric, includes last contact) |

**Informasi terkait campaign sebelumnya**

| Attribute | Data Type | Description |
| --- | --- | --- | 
|Pdays |Integer | pdays: number of days that passed by after the client was last contacted from a previous campaign (numeric; 999 means client was not previously contacted) |
|Previous |Integer | previous: number of contacts performed before this campaign and for this client |
|Poutcome |Text | poutcome: outcome of the previous marketing campaign (categorical: "failure","nonexistent","success") |

**Informasi terkait keadaan sosial-ekonomi**

| Attribute | Data Type | Description |
| --- | --- | --- | 
|Emp.var.rate |Float | employment variation rate - quarterly indicator |
|Cons.price.idx |Float | consumer price index - monthly indicator |
|Cons.conf.idx |Float | consumer confidence index - monthly indicator |
|Euribor3m |Float | euribor 3 month rate - daily indicator |
|Nr.employed |Float | number of employees - quarterly indicator |

**Target**

| Attribute | Data Type | Description |
| --- | --- | --- | 
|Y |Text | has the client subscribed a term deposit? (binary: "yes","no") |


## 3. Exploratory Data Analysis

### Karakteristik nasabah yang tertarik dengan deposito

Untuk menentukan karkteristik dari nasabah yang tertarik dengan deposito, kita akan mencoba menjawab beberapa pertanyaan berikut:
- Apa pekerjaan yang memiliki persentase nasabah melakukan deposito paling tinggi?
- Bagaimana cara kontak yang lebih diminati oleh nasabah yang melakukan deposito?
- Kapan waktu terbaik untuk melakukan kontak terhadap nasabah yang tertarik dengan deposito?
- Berapa lama durasi kontak yang optimal agar nasabah melakukan deposito?
- Apakah campaign sebelumnya berpengaruh terhadap campaign saat ini?

**Analisis lengkap terlampir pada notebook**

## 4. Preprocessing

Tahapan preprocessing yang dilakukan sebelum modeling
1. Remove Data Duplication
2. Fill Missing Values
3. Encoding
4. Scaling
5. Oversampling

## 5. Methodology (Modeling/Analysis)

**Analisis lengkap terlampir pada notebook**

## 6. Conclusion and Recommendation 

### Conclusion

**Karakteristik nasabah yang tertarik dengan deposito:**
- Nasabah yang tertarik dengan deposito cenderung memiliki pekerjaan **student** dalam usia sekolah (**teenage**) dan baru menamatkan jenjang Pendidikan **basic.6y**.
- Nasabah juga cenderung tertarik dengan deposito jika sudah pensiun (**retired**) dan masuk dalam kategori usia **senior** (60 tahun ke atas).
- Nasabah yang bukan student maupun retired cenderung melakukan deposito jika tingkat pendidikan **university.degree** atau berada dalam kategori usia **senior**
- Nasabah yang dikontak menggunakan **cellular** memiliki kecenderungan deposito 2.83x lebih tinggi dibandingkan menggunakan telephone dan waktu durasi telepon yang lebih cepat.
- Waktu terbaik untuk menghubungi nasabah adalah di pertengahan minggu (**Selasa - Kamis**) dan ketika **euribor 3-month rate sedang turun atau di bawah 2**
- Nasabah yang sebelumnya sudah pernah melakukan deposito (**success**) memiliki kecenderungan untuk deposito 4-7x lebih tinggi dibandingkan failure atau nonexistent.
- Jumlah kontak yang optimal kepada nasabah **minimal sebanyak 3x** karena dapat meningkatkan persentase subscribe 3,12x dibandingkan hanya dikontak 1x, namun jumlah kontak sebaiknya **tidak lebih dari 10x**.

<br>

**Karakteristik model machine learning yang didapat:**
- Metric utama yang kita gunakan adalah **recall**, karena meminimalkan False Negative kita anggap lebih penting dibandingkan False Positive.
- Model terbaik yang kita gunakan adalah model **Light GBM** benchmark dengan **scale_pos_weight=30**.
- Berdasarkan model Light GBM, fitur/kolom yang paling berpengaruh terhadap target (Deposit) adalah `age`, `euribor3m` dan `campaign`.
- Interpretasi SHAP untuk model LightGBM :
    - Semakin rendah `euribor3m` (warna biru), semakin besar kemungkinan nasabah untuk deposito.
    - Pada saat jumlah pegawai (`nr.employed`) di Bank tersebut rendah (warna biru), nasabah cenderung memiliki kemungkinan deposito yang lebih tinggi. 
    - Nasabah yang dikontak melalui telepon `contact_telephone` (warna merah = yes), cenderung rendah kemungkinannya untuk deposito.
    - Nasabah dengan jumlah `campaign` yang tinggi (warna merah), cenderung memiliki kemungkinan deposito yang lebih rendah dibandingkan dengan nasabah dengan jumlah yang rendah.
    <br>
    <br>
- **Precision** = 0.16 yang berarti dari total pelanggan yang diklasifikasikan deposit, hanya **16%**-nya yang berhasil terprediksi dengan benar.
- **Recall** =  0.89 yang berarti dari total nasabah yang aslinya deposit, **89%**-nya berhasil diprediksi dengan benar.
- **False Positive Rate** (aktualnya tidak deposit, diprediksi deposit) = **61%**
- **False Negative Rate** (aktualnya deposit, diprediksi tidak deposit) = **11%**
- Penerapan model machine learning dapat meningkatkan profit sebesar **5,5%**
- Sebelum adanya model machine learning, tim marketing cenderung menelepon nasabah secara acak. Namun dengan adanya machine learning, kita dapat memprioritaskan untuk menelepon nasabah potensial dengan probabilitas deposit tertinggi ke terendah. Sehingga kita bisa mendapatkan potensial customer lebih cepat.
- Dengan machine learning juga kita dapat mengurangi durasi campaign karena kita sudah dapat memetakan nasabah-nasabah yang potensial (tidak lagi menelepon secara acak)


### Recommendation

Beberapa langkah aksi yang dapat dilakukan perusahaan untuk meningkatkan jumlah nasabah yang akan deposito di antaranya :
- Lebih memfokuskan upaya marketing kita kepada kategori pekerjaan **student** dan **retired** karena memiliki persentase subscribe 2-4x lebih besar dibandingkan pekerjaan lain.
- Memfokuskan upaya kepada nasabah student yang masih berada dalam usia sekolah (**teenage**) atau menawarkan produk-produk khusus pelajar terutama yang baru menamatkan jenjang Pendidikan **basic.6y** atau setara Sekolah Dasar.
- Mencoba melakukan pendekatan kepada nasabah yang sudah pensiun dan masuk dalam kategori usia **senior** (60 tahun ke atas) karena memiliki kemungkinan deposito yang jauh lebih tinggi.
- Untuk nasabah dengan pekerjaan selain student dan retired, tim marketing dapat menargetkan program deposito pada nasabah dengan tingkat pendidikan **university.degree** atau nasabah yang berada dalam kategori usia **senior**.
- Melakukan kontak melalui **cellular** saja karena dapat meningkatkan kemungkinan deposito serta meningkatkan produktivitas (rata-rata durasi yang lebih cepat). Selain itu ketika ada nasabah yang baru mendaftar agar dipastikan untuk mencantumkan nomor cellullar.
- Meningkatkan upaya marketing di pertengahan minggu (**Selasa-Kamis**) karena memiliki kemungkinan subscribe lebih tinggi dibandingkan Senin atau Jumat.
- Melakukan kontak kepada nasabah ketika **euribor 3-month rate sedang turun atau di bawah 2**.
- Mengutamakan kelompok nasabah yang sebelumnya sudah pernah melakukan deposito (**success**) untuk ditawarkan deposito.
- Melakukan kontak kepada nasabah minimal sebanyak **3x** karena dapat meningkatkan persentase subscribe namun tidak lebih dari 10x

<br>

Hal-hal yang bisa dilakukan untuk mengembangkan project dan modelnya lebih baik lagi diantaranya:
- Menambahkan jumlah data terutama pada kategori job student dan retired untuk memperoleh informasi yang lebih akurat.
- Menambahkan fitur-fitur atau kolom baru seperti tingkat bunga deposito yang ditawarkan, penghasilan per bulan, jumlah saldo di bank, atau jumlah hutang nasabah yang kemungkinan berpengaruh terhadap kecenderungan nasabah untuk melakukan deposito atau tidak.
- Melakukan penambahan data khususnya untuk kelas minoritas (Deposito) agar dapat membantu meningkatkan performa model.
- Mencoba algorithm ML yang berbeda (misal algoritma Logistic Regression, CatBoost, etc) 
- Menganalisa data-data yang model yang masih salah tebak (False Negative dan terutama False Positive) untuk mengetahui alasan dan karakteristiknya.
