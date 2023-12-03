### **Summary Descriptive Statistics**

1. **Kolom dengan Tipe Data Tidak Sesuai:**

   - Kolom `Dt_Customer` merupakan tanggal registrasi pelanggan dengan tipe data object. Perlu diubah menjadi tipe Date Time.

2. **Kolom dengan Nilai Kosong:**

   - Kolom `Income` memiliki nilai kosong pada 2216 baris.

3. **Kolom dengan Summary Aneh:**

   - Kolom `ID` memiliki jumlah nilai unik yang sama dengan jumlah baris dataset (2240), sehingga tidak memungkinkan untuk mengamati riwayat perjalanan pelanggan.
   - Kolom `Z_CostContact` dan `Z_Revenue` hanya memiliki satu data unik.
   - Kolom `Dt_Customer` menunjukkan keanehan dengan pelanggan terakhir melakukan registrasi pada 29 Juni 2014. Terdapat juga keanehan pada `Year Birth` dengan tahun lahir tertua adalah 1893.
   - Kolom `Income` memiliki nilai maksimum mencapai ratusan ribu (666,666), sedangkan nilai ukuran pemusatan dan penyebarannya hanya mencapai puluhan ribu, diduga sebagai outlier.
   - Beberapa kolom seperti `MntFishProducts`, `MntFruits`, `MntGoldProds`, `MntMeatProducts`, `MntSweetProducts`, `MntWines` memiliki nilai maksimum yang jauh dari ukuran pemusatan atau penyebaran lainnya, menunjukkan adanya outlier.
   - Kolom `Marital Status` memiliki 8 nilai unik.

### **Summary EDA**

1. **Berdasarkan KDE Plot:**

   - **Normal Distribution:**
     - `Recency` memiliki distribusi yang mirip dengan distribusi normal.
   - **Left-Skewed Distribution:**
     - `Year_Birth` menunjukkan kecondongan ke kiri dengan median yang lebih tinggi daripada mean.
   - **Right-Skewed Distribution:**
     - `Income` dan beberapa features terkait pembelian produk menunjukkan kecondongan ke kanan, dengan mean yang lebih tinggi daripada median.
   - **Bimodal Distribution:**
     - `Kidhome` dan `Teenhome` menunjukkan dua puncak dalam distribusinya.
   - **Binary Dominated Distribution:**
     - Beberapa features campaign (`AcceptedCmp1`, `AcceptedCmp2`, `AcceptedCmp3`, `AcceptedCmp4`, `AcceptedCmp5`, dan `Responsee`) didominasi oleh nilai 0.

2. **Berdasarkan Box Plot:**

   - `Year_Birth` dan `Income` memiliki outlier yang perlu dicermati lebih lanjut.
   - Beberapa features terkait pembelian produk dan aktivitas pembelian memiliki banyak nilai outlier pada nilai tinggi, menunjukkan variasi yang signifikan dalam pola pembelian atau aktivitas pelanggan.

3. **Berdasarkan Count Plot (Categorical Feature):**

   - **Level Pendidikan:**
     - Mayoritas pelanggan memiliki tingkat pendidikan "Graduation," menunjukkan target pasar utama.
   - **Status Perkawinan:**
     - Mayoritas pelanggan memiliki status perkawinan "Married," menunjukkan dominasi pasangan dalam populasi pelanggan.

4. **Berdasarkan Lineplot (Datetime Feature):**

   - Terdapat fluktuasi dalam pendaftaran pelanggan selama periode Juli-2012 hingga Juni-2014.
   - Puncak pendaftaran terjadi pada bulan Agustus-2012 dan Oktober-2013.
   - Tren menunjukkan jumlah pendaftaran yang lebih rendah pada awal dan akhir periode, menunjukkan potensi pola musiman atau faktor lain yang memengaruhi pendaftaran pelanggan.

5. **Berdasarkan Regression Plot (Numerical Feature vs Target):**

   - Beberapa faktor seperti pendapatan, jumlah anak, recency, dan tahun kelahiran pelanggan memiliki korelasi yang kuat terhadap kemungkinan pelanggan merespon.
   - Spending pada produk tertentu, terutama `MeatProducts`, juga memiliki korelasi positif yang signifikan dengan `Response`.
   - Jenis pembelian melalui Katalog dan Web memberikan kontribusi positif yang signifikan terhadap kemungkinan pelanggan merespon, sementara pembelian dengan diskon atau melalui toko fisik tidak menunjukkan korelasi yang signifikan.
   - Campaign (`AcceptedCmp1`, `AcceptedCmp2`, `AcceptedCmp3`, `AcceptedCmp4`, `AcceptedCmp5`) juga memiliki korelasi positif yang signifikan terhadap `Response`.

6. **Berdasarkan Lineplot (Datetime Feature vs Target):**

   - Pada rentang waktu Juli 2012 hingga Juni 2014, lebih banyak pelanggan yang mendaftar namun tidak merespon campaign.
   - Puncak pendaftaran dan respon terjadi pada Agustus 2012 - September 2012, namun jumlahnya cenderung menurun hingga akhir periode.
   - Analisis ini memberikan gambaran tentang dinamika pendaftaran dan respon campaign selama periode tersebut, yang dapat menjadi dasar untuk strategi pemasaran yang lebih efektif di masa depan.

7. **Berdasarkan Stacked Bar (Categorical Feature (normalize) vs Target):**

   - **Insight Response Campaign Berdasarkan Tingkat Pendidikan:**
     - Tingkat Response Tinggi pada Tingkat Pendidikan Tinggi: PhD (20.78%), Master (15.41%), dan Graduation (13.48%).
     - Varian Response pada Tingkat Pendidikan Rendah, dengan Basic (3.70%) lebih rendah dibandingkan dengan 2n Cycle (10.84%) dan Graduation (13.49%).
     - Pentingnya Pendidikan dalam Pengaruh Response.

   - **Insight Response Campaign Berdasarkan Status Perkawinan:**
     - Perbedaan Signifikan pada Tingkat Response: "Married" memiliki tingkat Response yang lebih rendah (11.34%) dibandingkan dengan "Divorced" (20.69%), "Single" (22.08%), dan "Together" (10.35%).
     - Tingkat Response Tinggi pada Status Perkawinan "Single" dan "Divorced" (22.08% dan 20.69%).
     - Pentingnya Personalisasi Campaign untuk Setiap Status Perkawinan.

8. **Berdasarkan Korelasi Koefisien (Heatmap):**

   - **Pentingnya Korelasi Antara Feature:**
     - Korelasi Positif terhadap Target pada campaign, produk spending, dan channel penjualan.
     - Korelasi Negatif terhadap Target hanya pada Recency dan jumlah anak.
     - Korelasi Tinggi Antara Beberapa Pasang Feature, menunjukkan adanya multicollinearity.
     - Rekomendasi untuk Proses Modeling.

### **Summary Business Insights**

Berdasarkan analisis mendalam terhadap data campaign dan karakteristik pelanggan, kami menyarankan beberapa langkah strategis untuk meningkatkan efektivitas campaign dan memaksimalkan keuntungan bisnis:

1. **Segmentasi Pelanggan Berdasarkan Respons Campaign:**
   - Melakukan segmentasi pelanggan berdasarkan respons campaign dapat membantu dalam menyesuaikan strategi pemasaran.
   - Fokuskan upaya pada kelompok pelanggan yang telah menunjukkan respons positif, seperti tingkat pendidikan Graduation, PhD, dan Master, serta status pernikahan Single, Married, dan Divorced.

2. **Personalisasi Pesan dan Penawaran:**
   - Personalisasi pesan dan penawaran campaign untuk setiap kelompok pelanggan yang telah diidentifikasi dapat meningkatkan keterlibatan.
   - Berdasarkan karakteristik unik dari setiap kelompok, buatlah pesan yang relevan dan tawarkan insentif yang sesuai dengan preferensi mereka.

3. **Penargetan Tingkat Pendidikan Tinggi:**
   - Tingkat pendidikan tinggi seperti Graduation, PhD, dan Master memiliki potensi besar untuk respons campaign.
   - Fokuskan penawaran khusus, informasi produk, dan keuntungan tambahan pada kelompok ini untuk memaksimalkan partisipasi.

4. **Optimalkan Pengeluaran Pelanggan yang Merespon:**
   - Pelanggan yang merespons campaign memiliki kecenderungan pengeluaran yang lebih tinggi pada berbagai kategori produk.
   - Optimalisasi persediaan dan promosi pada produk-produk yang paling diminati oleh kelompok pelanggan ini dapat meningkatkan nilai transaksi.

5. **Perkuat Campaign dengan Data Pembelian dan Channel:**
   - Analisis menunjukkan bahwa pelanggan yang merespons campaign memiliki rata-rata pembelian yang lebih tinggi di berbagai saluran seperti catalog, web, dan toko fisik.
   - Penguatan campaign dengan peningkatan ketersediaan produk melalui saluran ini dapat meningkatkan aksesibilitas produk bagi pelanggan.

6. **Monitoring Berkala dan Analisis Reaksi Pelanggan:**
   - Memonitoring berkala terhadap respons pelanggan dan melakukan analisis lebih lanjut terhadap perubahan tren dan preferensi (Dashboard).
   - Keterlibatan yang berkelanjutan dan penyesuaian cepat terhadap dinamika pasar dapat menjadi kunci kesuksesan jangka panjang.

Dengan menerapkan strategi ini, diharapkan perusahaan dapat meraih keberhasilan yang lebih besar dalam campaign pemasaran, meningkatkan loyalitas pelanggan, dan mengoptimalkan hasil bisnis secara keseluruhan.
