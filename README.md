### **Summary Descriptive Statistics**

1. Apakah ada kolom dengan tipe data kurang sesuai, atau nama kolom dan isinya kurang sesuai?

   - Feature Dt_Customer merupakan tanggal registrasi pelanggan dengan tipe data object. Tipe data ini tidak sesuai, sehingga perlu diubah menjadi tipe Date Time.
2. Apakah ada kolom yang memiliki nilai kosong? Jika ada, apa saja?

   - Feature Income mempunyai nilai kosong karena hanya berjumlah 2216 rows.
3. Apakah ada kolom yang memiliki nilai summary agak aneh? (min/mean/median/max/unique/top/freq)

   - Feature ID merupakan identifikasi pelanggan. Berdasarkan analisis jumlah nilai unik pada feature tersebut, diketahui bahwa jumlahnya sama dengan jumlah baris dataset (2240), sehingga tidak memungkinkan untuk mengamati riwayat perjalanan pelanggan.
   - Feature Z_CostContact dan Z_Revenue hanya memiliki satu data unik, maka keduanya tidak akan memberikan hasil analisis yang signifikan.
   - Feature Dt_Customer, pelanggan paling terakhir melakukan registrasi di 29 Juni 2014, maka dengan asumsi saat ini adalah tahun 2014, ada keanehan pada Feature Year Birth dimana tahun lahir tertua ada di tahun 1893 atau usia pelanggan 121 tahun. Hal ini merupakan hal yang kurang masuk akal. Diduga terdapat kesalahan input tahun lahir oleh pelanggan/kesalahan pencatatan oleh sistem.
   - Feature Income memiliki keanehan karena memiliki nilai maksimum mencapai ratusan ribu (666.666), sedangkan nilai ukuran pemusatan dan penyebarannya hanya mencapai puluhan ribu. Diduga nilai ini merupakan outlier yang disebabkan karena kesalahan input atau pencatatan oleh sistem.
   - Feature MntFishProducts, MntFruits, MntGoldProds, MntMeatProducts, MntSweetProducts, MntWines memiliki keanehan dilihat dari nilai maksimumnya yang jauh dari nilai ukuran pemusatan atau ukuran penyebaran lainnya. Sehingga diduga terdapat nilai outlier pada feature tersebut.
   - Feature Marital Status memiliki keanehan karena memiliki 8 nilai unik. Maka pada tahap selanjutnya akan dianalisis lebih dalam setiap nilai pada feature ini.


### **Summary EDA**

1. Berdasarkan KDE Plot:

   - Normal Distribution:

     Recency memiliki distribusi yang mirip dengan distribusi normal.
   - Left-Skewed Distribution:

     Year_Birth menunjukkan kecondongan ke kiri dengan median yang lebih tinggi daripada mean.
   - Right-Skewed Distribution:

     Income dan beberapa features terkait pembelian produk menunjukkan kecondongan ke kanan, dengan mean yang lebih tinggi daripada median.
   - Bimodal Distribution:

     Kidhome dan Teenhome menunjukkan dua puncak dalam distribusinya.
   - Binary Dominated Distribution:

     Features seperti AcceptedCmp1, AcceptedCmp2, AcceptedCmp3, AcceptedCmp4, AcceptedCmp5, dan Responsee didominasi oleh nilai 0.
2. Berdasarkan Box Plot:

   - Year_Birth dan Income memiliki outlier, yang mungkin perlu dicermati lebih lanjut.
   - Pada beberapa features terkait pembelian produk (MntFishProducts, MntFruits, MntGoldProds, MntMeatProducts, MntSweetProducts, MntWines), serta features terkait aktivitas pembelian (NumCatalogPurchases, NumDealsPurchases, NumStorePurchases, NumWebPurchases, NumWebVisitsMonth), terdapat banyak nilai outlier pada nilai tinggi, menunjukkan variasi yang signifikan dalam pola pembelian atau aktivitas pelanggan.
3. Berdasarkan Count Plot (Categorical Feature):

   - Level Pendidikan:

     Mayoritas pelanggan memiliki tingkat pendidikan "Graduation," menunjukkan target pasar utama.
   - Status Perkawinan:

     Mayoritas pelanggan memiliki status perkawinan "Married," menunjukkan dominasi pasangan dalam populasi pelanggan.
   - Pertimbangan Tambahan:

   Perlu penelitian lebih lanjut untuk memahami definisi "Basic" dan "2n Cycle" dalam konteks ini.

Status perkawinan "Alone," "Absurd," dan "YOLO" perlu dipahami lebih lanjut dan mungkin dianggap sebagai data yang tidak valid atau perlu dicermati secara khusus.

4. Berdasarkan Lineplot (Datetime Feature):

   - Terdapat fluktuasi dalam pendaftaran pelanggan selama periode Juli-2012 hingga Juni-2014.
   - Puncak pendaftaran terjadi pada bulan Agustus-2012 dan Oktober-2013.
   - Tren menunjukkan jumlah pendaftaran yang lebih rendah pada awal dan akhir periode, menunjukkan potensi pola musiman atau faktor lain yang memengaruhi pendaftaran pelanggan.
5. Berdasarkan Regression Plot (Numerical Feature vs Target)

   - Beberapa faktor seperti pendapatan, jumlah anak, recency, dan tahun kelahiran pelanggan memiliki korelasi yang kuat terhadap kemungkinan pelanggan merespon.
   - Spending pada produk tertentu, terutama MeatProducts, juga memiliki korelasi positif yang signifikan dengan Response.
   - Jenis pembelian melalui Katalog dan Web memberikan kontribusi positif yang signifikan terhadap kemungkinan pelanggan merespon, sementara pembelian dengan diskon atau melalui toko fisik tidak menunjukkan korelasi yang signifikan.
   - Campaign (AcceptedCmp1, AcceptedCmp2, AcceptedCmp3, AcceptedCmp4, AcceptedCmp5) juga memiliki korelasi positif yang signifikan terhadap Response.
6. Berdasarkan Lineplot (Datetime Feature vs Target)

   - Pada rentang waktu Juli 2012 hingga Juni 2014, lebih banyak pelanggan yang mendaftar namun tidak merespon campaign.
   - Puncak pendaftaran dan respon terjadi pada Agustus 2012 - September 2012, namun jumlahnya cenderung menurun hingga akhir periode.
   - Analisis ini memberikan gambaran tentang dinamika pendaftaran dan respon campaign selama periode tersebut, yang dapat menjadi dasar untuk strategi pemasaran yang lebih efektif di masa depan.
7. Berdasarkan Stacked Bar (Categorical Feature,normalize vs Target)

   **Insight Response Campaign Berdasarkan Tingkat Pendidikan:**

   1. Tingkat Response Tinggi pada Tingkat Pendidikan Tinggi:

      - Pelanggan dengan tingkat pendidikan **PhD (20.78%)** memiliki tingkat Response Campaign tertinggi.
      - Diikuti oleh **Master (15.41%)** dan **Graduation (13.48%)**.
      - Tingkat pendidikan tinggi berkorelasi positif dengan kemungkinan merespon Campaign.
   2. Varian Response pada Tingkat Pendidikan Rendah:

      - Tingkat Response lebih bervariasi pada tingkat pendidikan rendah.

      -**Basic (3.70%)** menunjukkan Response lebih rendah dibandingkan dengan **2n Cycle (10.84%)** dan **Graduation (13.49%)**.

      - Pelanggan dengan tingkat pendidikan rendah cenderung memiliki tingkat Response yang lebih rendah.
   3. Pentingnya Pendidikan dalam Pengaruh Response:

      - Pelanggan dengan tingkat pendidikan tinggi, seperti PhD dan Master, cenderung lebih Responsif terhadap Campaign.
      - Informasi ini dapat menjadi kunci dalam merancang Campaign yang lebih efektif dan menargetkan kelompok pelanggan yang lebih cenderung merespon berdasarkan tingkat pendidikan mereka.

   **Insight Response Campaign Berdasarkan Status Perkawinan:**

   1. Perbedaan Signifikan pada Tingkat Response:

      - Terdapat perbedaan signifikan dalam tingkat Response Campaign antara status perkawinan.

      -**"Married"** memiliki tingkat Response yang lebih rendah (11.34%) dibandingkan dengan **"Divorced" (20.69%)**, **"Single" (22.08%)**, dan **"Together" (10.35%)**.
   2. Tingkat Response Tinggi pada Status Perkawinan "Single" dan "Divorced":

      -**"Single"** dan **"Divorced"** menunjukkan tingkat Response Campaign yang lebih tinggi, masing-masing sebesar **22.08%** dan **20.69%**.

      - Status perkawinan ini dapat menjadi faktor penting dalam menentukan Response positif terhadap Campaign.
   3. Pentingnya Personalisasi Campaign untuk Setiap Status Perkawinan:

      - Perusahaan dapat mempertimbangkan strategi pemasaran yang lebih personal dan disesuaikan dengan masing-masing status perkawinan.
      - Status perkawinan seperti **"Married"** mungkin memerlukan pendekatan yang berbeda untuk meningkatkan Response Campaign.
8. Berdasarkan Korelasi Koefisien (Heatmap)

   **Pentingnya Korelasi Antara Feature:**

   1.**Korelasi Positif terhadap Target:**

   - Feature yang termasuk dalam campaign (AcceptedCmp1, AcceptedCmp2, dst.), feature yang termasuk dalam produk spending seperti (MntWines, MntMeatProducts, dst.), feature yang termasuk pada channel penjualan seperti (NumCatalogPurchases, NumWebPurchases, dst.) mempunyai korelasi positif terhadap target.

   2.**Korelasi Negatif terhadap Target:**

   - Hanya beberapa feature yang mempunyai nilai korelasi negatif terhadap target, yaitu Recency dan jumlah anak (Teenhome dan Kidhome).

   3.**Korelasi Tinggi Antara Beberapa Pasang Feature:**

   - Korelasi antara beberapa pasang feature cukup tinggi, menunjukkan adanya multicollinearity.
   - Contohnya, "MntMeatProducts" dengan “NumCatalogPurchases” (0.72), “MntWines” dengan dengan “NumCatalogPurchases” dan “NumStorePurchases” (0.64), "Income" dan beberapa feature pengeluaran makanan ("MntWines", "MntFruits", "MntMeatProducts").

   **Rekomendasi untuk Proses Modeling:**

   1.**Analisis Lanjut dan Seleksi Fitur:**

   - Analisis lebih lanjut diperlukan untuk memahami signifikansi feature-feature yang berkorelasi tinggi dan apakah mereka memiliki dampak domain yang penting.
   - Seleksi fitur dan evaluasi signifikansi fitur akan menjadi langkah kritis dalam proses modeling.

   2.**Penanganan Multicollinearity:**

   - Penerapan PCA bisa menjadi solusi untuk mengatasi multicollinearity dan mereduksi dimensi.
   - Perlu melakukan standarisasi atau normalisasi pada data sebelum menerapkan teknik ini.

   3.**Fokus pada Feature dengan Korelasi Tinggi terhadap Target:**

   - Perlu menganalisis feature-feature dengan korelasi tinggi terhadap target ("Response") karena kemungkinan memiliki kontribusi yang signifikan pada model.

### **Summary Business Insights**

Berdasarkan analisis mendalam terhadap data campaign dan karakteristik pelanggan, kami menyarankan beberapa langkah strategis untuk meningkatkan efektivitas campaign dan memaksimalkan keuntungan bisnis:

1. **Segmentasi Pelanggan Berdasarkan Respons campaign:**

   Melakukan segmentasi pelanggan berdasarkan respons campaign dapat membantu dalam menyesuaikan strategi pemasaran. Fokuskan upaya pada kelompok pelanggan yang telah menunjukkan respons positif, seperti tingkat pendidikan Graduation, PhD, dan Master, serta status pernikahan Single, Married, dan Divorced.
2. **Personalisasi Pesan dan Penawaran:**

   Personalisasi pesan dan penawaran campaign untuk setiap kelompok pelanggan yang telah diidentifikasi dapat meningkatkan keterlibatan. Berdasarkan karakteristik unik dari setiap kelompok, buatlah pesan yang relevan dan tawarkan insentif yang sesuai dengan preferensi mereka.
3. **Penargetan Tingkat Pendidikan Tinggi:**

   Tingkat pendidikan tinggi seperti Graduation, PhD, dan Master memiliki potensi besar untuk respons campaign. Fokuskan penawaran khusus, informasi produk, dan keuntungan tambahan pada kelompok ini untuk memaksimalkan partisipasi.
4. **Optimalkan Pengeluaran Pelanggan yang Merespon:**

   Pelanggan yang merespons campaign memiliki kecenderungan pengeluaran yang lebih tinggi pada berbagai kategori produk. Optimalisasi persediaan dan promosi pada produk-produk yang paling diminati oleh kelompok pelanggan ini dapat meningkatkan nilai transaksi.
5. **Perkuat campaign dengan Data Pembelian dan Channel:**

   Analisis menunjukkan bahwa pelanggan yang merespons campaign memiliki rata-rata pembelian yang lebih tinggi di berbagai saluran seperti catalog, web, dan toko fisik. Penguatan campaign dengan peningkatan ketersediaan produk melalui saluran ini dapat meningkatkan aksesibilitas produk bagi pelanggan.
6. **Pemantauan Terus-Menerus dan Analisis Reaksi Pelanggan:**

   Melakukan pemantauan terus-menerus terhadap respons pelanggan dan melakukan analisis lebih lanjut terhadap perubahan tren dan preferensi. Keterlibatan yang berkelanjutan dan penyesuaian cepat terhadap dinamika pasar dapat menjadi kunci kesuksesan jangka panjang.

Dengan menerapkan strategi ini, diharapkan perusahaan dapat meraih keberhasilan yang lebih besar dalam campaign pemasaran, meningkatkan loyalitas pelanggan, dan mengoptimalkan hasil bisnis secara keseluruhan.
