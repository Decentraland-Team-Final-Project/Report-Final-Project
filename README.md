# Report-Final-Project - Data Set E-Commerce Shipping
## Kelompok 8 : Decentraland

# Summary Stage 1
Pada stage 1 kami melakukan Exploratory Data Analysis pada Data Set E-Commerce Shipping dengan hasil pada statistik deskriptif sebagai berikut:
- Data terdiri dari 10.999 sampel (baris).
- Tidak ada null value di semua kolom.
- Tidak ada baris yang terduplikasi.
- Terdapat 10 fitur (variabel independen) dan 1 targeted variable (variabel dependen).
- Berdasarkan jenisnya, fitur terdiri dari 4 fitur kategorik (`Warehouse_block`, `Mode_of_Shipment`, `Product_importance`, dan `Gender`) dan 6 fitur numerik (`Customer_care_calls`, `Customer_rating`, `Cost_of_the_Product`, `Prior_purchases`, `Discount_offered`, dan `Weight_in_gms`).
- Satu target variabel yaitu `Reached.on.Time_Y.N` yang bertipe numerik dengan value yang sedikit tidak berimbang, hampir 60% data sampel termasuk ke dalam kategori pengiriman barang yang terlambat.
- Selain itu pada dataset tersebut juga tidak ditemukan data duplikat dan missing value.
Selain itu pada Univariate Analysis, kami mendapatkan hasil berupa :
- Outlier terlihat pada variabel `Prior_Purchases` dan `Discount_Offered`
- Variabel `Prior_Purchases` dan `Discount_Offered` membentuk pola positively skewed.
- Variabel `Weight_in_gms` membentuk pola negatively skewed.
- Variabel `Customer_Care_Calls` dan `Cost_of_The_Product` hampir mendekati distribusi normal walaupun polanya masih sedikit skewed.
Kemudian pada Multivariate Analysis menggunakan Correlation Heatmap dengan penjelasan sebagai berikut:
- Variabel `Customer_care_calls`, `Cost_of_The_Product`, `Prior_Purchases`, dan `Weight_in_gms` memiliki korelasi negatif yang lemah terhadap target variabel (`Late_Shipment`).
- Variabel `Discount_Offered` dan `Customer_Rating` memiliki korelasi positif yang lemah terhadap target variabel (`Late_Shipment`).
- Variabel `Weight_in_gms` dan `Discount_offered` memiliki korelasi negatif lemah.
- Variabel `Cost_of_The_Product` dan `Customer_Care_Calls` memiliki korelasi positif lemah.
- Tidak ada features yang redundant karena tidak ada features yang memiliki korelasi > 0.7
Dan yang terakhir adalah Business Insights yang kami dapatkan seperti pada hubungan Discount Offered dengan Variabel Target (Late Shipment)
Dengan penjelasan bahwa transaksi memiliki diskon lebih dari 10%, barang justru cenderung terlambat pengirimannya. Hal ini bisa disebabkan karena semakin besar diskon harga mengakibatkan semakin besar pula minat customer untuk berbelanja (contoh: promo diskon hari raya atau promo harbolnas), alhasil muatan barang digudang dan ekspedisi menjadi overloaded dan pengiriman barang menjadi telat. Patut diperhatikan pula gudang penyimpanan barang, tenaga kerja, dan moda pengiriman barang tertentu pastinya mempunyai kapasitas dalam pengiriman barang, ketika pengiriman barang overloaded kemungkinan pengiriman barang bisa terlambat dengan solusi : Lebih ke masalah teknis operasional pengiriman, diskon yang besar menyebabkan transaksi pembelian overloaded dan berpotensi menyebabkan barang terlambat. Harus dicari tahu teknis operasional (moda pengiriman, gudang, dan importansi produk) apa yang paling berpotensi besar terjadinya pengiriman yang terlambat. 

# Summary Stage 2
Pada tahap ini kami melakukan Data Preprocessing dan karena pada dataset ini kita tidak memiliki data duplikat dan missing value maka langsung melakukan Feature Encoding pada feature 'Warehouse_Block', 'Mode_of_Shipment', 'Product_Importance', 'Gender'. Dan One hot encoding pada feature 'Warehouse_Block', 'Mode_of_Shipment'
Kemudian dilanjutkan dengan melakukan Log/Exp Transformation pada feature 'Discount_Offered' dan 'Prior_Purchases'.
Setelah itu melakukan teknik Standardization pada feature 'Weight_in_gms'.
Dan yang terakhir adalah melakukan Outliers Handling menggunakan z-score pada semua feature dengan hasil jumlah baris sebelum outlier dihilangkan: 10999 dan jumlah baris setelah memfilter outlier: 10642


# Summary Stage 3
Untuk Stage 3 ini kami melakukan modeling dengan data yang sudah diolah pada stage 2 dengan kriteria data yang masih original, data yang sudah di log transform, data yang sudah diremove outlier menggunakan algoritma Classification seperti Logistik Regresi, K-NN, Decision Tree, Random Forest, XGBoost, dan AdaBoost.
