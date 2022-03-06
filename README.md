# Report-Final-Project - Data Set E-Commerce Shipping
Data source : https://www.kaggle.com/prachi13/customer-analytics
## Kelompok 8 : Decentraland
### Mentor
1.  [Gerry Chandra Zheng](https://www.linkedin.com/in/gerrychandra/).
### Member
1. [Dharma Setiawan](https://www.linkedin.com/in/dharma-setiawan/).
2. [Muhammad Farhan Atmawinanda](https://www.linkedin.com/in/atmawinanda/).
3. [Fikri Diva Sambasri](https://www.linkedin.com/in/fikridivasambasri/).
4. [Ahmad Ilham Habibi](https://www.linkedin.com/in/ahmad-ilham-habibi-886b4b123/).
5. [Ilham Ibnu Affan](https://www.linkedin.com/in/ilhamibnuaffan/).

## **Project Overview** 
• Mencari insight dari dataset dengan Exploratory Data Analysis (EDA) <br>
• Melakukan data cleansing, data processing, data engineering untuk menyiapkan data sebelum modeling (Pre-Processing) <br>
• Dari beberapa feature yang ada, mencoba untuk membuat model prediksi apakah shipping deliveries akan diterima telat atau tepat waktu pada customers <br>
• Memberikan analisis rekomendasi/solusi dan keuntungan apa saja yang bisa diperoleh jika performa model yang kita bangun memuaskan. 

## Business Background
Decentraland adalah sebuah perusahaan e-commerce yang menjual berbagai produk elektronik. 
Sebagai perusahaan data science consultant independen, kami di-hire oleh Decentraland untuk mengolah suatu data set shipment. Kami diminta untuk mencari solusi bagaimana cara mengatasi permasalahan yang mereka punya melalui data set tersebut.

## Problem Statement
Data set E-Commerce Shipping menunjukan bahwa dari 10.999 sampel transaksi pembelian online, 59.7% transaksi diantaranya masih terjadi keterlambatan waktu pengiriman barang.
Keterlambatan yang tinggi ini tentunya berkaitan dengan customer happiness dan potential revenue. Customer akan mendapatkan experience yang kurang baik dalam menggunakan layanan Decentraland. Keterlambatan ini juga menyebabkan company mengalami potential revenue loss.

![problem statement](https://user-images.githubusercontent.com/45113535/156904411-51d1656b-4649-4f39-886e-e169e37ef50b.jpg)

## Exploratory Data Analysis
Pada stage 1 kami melakukan Exploratory Data Analysis pada Data Set E-Commerce Shipping dengan Data Set:
| Variable | Variable Rename | Type | Definition | Example |
| ----------- | ----------- | ----------- | ----------- | ----------- |
| ID | ID | Nominal | Customer ID Number | 10, 15, 10995, 10996
| Warehouse_Block | Warehouse | Nominal | Warehouse to Store the Product | A, B, C, D, F
| Mode_of_Shipment | Shipment | Nominal | Mode of Product Shipping | Flight, Road, Ship
| Customer_Care_Calls | Calls | Discrete | Number of Calls Made | 1, 2, 5, 6
| Customer_Rating | Rating | Ordinal | Company Rating by Customers | 5: Best - 4: Better - 3: Neutral - 2: Bad - 1: Worst
| Cost_of_The_Product | Cost | Discrete | Cost of Product in US Dollars | 177, 216, 236, 182
| Prior_Purchases | Purchases | Discrete | Number of Prior Purchase | 3, 2, 6
| Product_Importance | Importance | Ordinal | Product Importance Parameter | Low, Medium, High
| Gender | Gender | Nominal | Customer Gender | Male, Female
| Discount_Offered | Discount | Discrete | Product Discount in US Dollars | 65, 10, 16
| Weight_in_gms | Weight (gram) | Continous | Product Weight in grams | 4953, 5676, 2171
| Late_Shipment | Late | Nominal | Target Variable, 1: NOT reached on time - 0: REACHED on time | 1, 0<br>

1. Distribusi Data Variabel Numerik
![distribusi variabel numerik](https://user-images.githubusercontent.com/45113535/156906405-c34b9a72-6062-4fc4-a646-2c5afd76a93c.jpg)
- Variabel Calls dan Cost sudah cukup simetrik distribusinya mendekati distribusi normal (mean dan median tidak berbeda jauh).
- Variabel Discount pola persebarannya membentuk positively skewed (mean>median), sedangkan variabel Weight (gram) membentuk negatively skewed (median>mean).

2. Fitur yang tidak mempengaruhi keterlambatan
![shipment](https://user-images.githubusercontent.com/45113535/156906905-60675a6c-5cd6-4252-9cc7-922243fe23f6.jpg)
![warehouse](https://user-images.githubusercontent.com/45113535/156906961-484e31db-8e09-4d0d-bf8e-b781cffde792.jpg)
![purchases](https://user-images.githubusercontent.com/45113535/156906970-4e4511c9-a068-4fd3-a2e1-7a8182db40fe.jpg)
![calls](https://user-images.githubusercontent.com/45113535/156906975-9885245b-740e-4dc4-be55-e19c00d58fb7.jpg)
![importance](https://user-images.githubusercontent.com/45113535/156907055-469244f3-f58e-4622-a32a-bc1ef72e8357.jpg)
- Customer care calls, shipment, warehouse block, product importance, dan prior purchase memiliki ratio yang kurang lebih sama. Maka dari itu, kami tidak menganalisis lebih lanjut.
- Permasalahan keterlambatan tidak disebabkan oleh fitur-fitur diatas

3. Fitur-Fitur yang Berpengaruh terhadap Keterlambatan
![fitur berpengaruh](https://user-images.githubusercontent.com/45113535/156907118-209391e7-de2b-4ae5-9a60-60c675e9abf6.jpg)
- Discount yang lebih dari 10 persen terkonfirmasi terlambat. Hal ini bisa mengindikasikan beberapa bulan dimana promo diberikan besar-besaran sehingga pengiriman mengalami keterlambatan.
- Berat barang yang berkisar 2-4 kg terkonfirmasi terlambat. Hal ini mengindikasikan bahwa ada kemungkinan banyak customer membeli barang-barang kategori ringan.

4. Korelasi fitur

![korelasi fitur](https://user-images.githubusercontent.com/45113535/156907198-cacbe402-e2a2-41ff-bf31-b10d7072e179.jpg)
- Feature Discount dan Weight adalah 2 fitur yang paling berkorelasi dengan feature target yaitu Late.
- Tidak ada feature yang redundant di dataset ini.

## Data Preprocessing
![data preprocessing](https://user-images.githubusercontent.com/45113535/156907226-d390476a-1c45-4adc-bee7-b614af1cfb73.jpg)

keterangan:
- Dataset1 : Dataset original
- Dataset2 : Dataset dengan penghapusan outlier menggunakan z-score
- Dataset3 : Dataset dengan penghapusan outlier menggunakan IQR

## Model Evaluation Terbaik
![model evaluasi](https://user-images.githubusercontent.com/45113535/156907297-ec7ef83d-7279-42c5-ad1a-e75045783215.jpg)
- Dataset 1 boosting hyperparameter Adaboost menghasilkan performa terbaik (AUC Data Training lebih besar daripada AUC Data Testing dengan gap perbedaan yang dekat dan nilainya relatif lebih tinggi dibandingkan hasil di dataset 2 dan 3).

## Business Insight & Recomendation
1. Banyak sekali delays yang terjadi pada order dengan diskon diatas 10%. Hal ini dapat diantisipasi dengan memberikan notifikasi kepada pelanggan ketika terjadi diskon yang besar seperti “Harbolnas” yang memungkinkan barang tidak terkirim dengan tepat waktu.
Kami juga menyarankan untuk membuat chatbot khusus untuk menangani pertanyaan-pertanyaan dari customer. Chatbot ini dapat menjawab pertanyaan-pertanyaan dari customer. Customer akan tetap puas karena pertanyaan-pertanyaan mereka terjawab.
2. Berat barang antara 2-4 kg mengalami keterlambatan yang signifikan. Pihak decentraland perlu untuk memberi notifikasi kepada pembeli di rentang tersebut seperti barang akan terlambat x hari sebelum pelanggan menekan tombol buy. Selanjutnya, menurut Desy (2019), pihak e-commerce perlu memberikan voucher sebagai pengganti keterlambatan. Pihak e-commerce juga dapat memberikan promo voucher/kupon apabila barang yang terprediksi on time ternyata late. Hal ini dapat mengurangi customer pain point dan membuat customer tetap puas dan tetap berbelanja di e-commerce Decentraland. Percobaan voucher ini bisa dibilang lumayan risky dan membuat customer ketergantungan sehingga kami memutuskan untuk melakukan AB Testing.

<!--
Dengan hasil pada statistik deskriptif sebagai berikut:
- Data terdiri dari 10.999 sampel (baris).
- Tidak ada null value di semua kolom.
- Tidak ada baris yang terduplikasi.
- Terdapat 10 fitur (variabel independen) dan 1 targeted variable/label (variabel dependen).
- Berdasarkan jenisnya, fitur terdiri dari 5 feature kategorik (`Warehouse_Block`, `Mode_of_Shipment`, `Product_Importance`,`Customer_Rating`, dan `Gender`) dan 5 feature numerik (`Customer_Care_Calls`, `Cost_of_The_Product`, `Prior_Purchases`, `Discount_Offered`, dan `Weight_in_gms`).
- Satu target variabel, yaitu `Late_Shipment` yang bertipe numerik memiliki value yang sedikit tidak berimbang, hampir 59% data sampel termasuk ke dalam kategori pengiriman barang yang terlambat.
- Selain itu pada dataset tersebut juga tidak ditemukan data missing value.
- Berdasarkan persebarannya, terdapat dua feature numerik yang bersifat positively skewed, yaitu `Discount_Offered` dan `Prior_Purchases`. Satu kasus negatively skewed ditemukan terjadi pada feature `Weight_in_gms`, sementara feature numerik lainnya (`Customer_Care_Calls` dan `Cost_of_The_Product`)cenderung mendekati distribusi normal.<br>

## Summary Stage 2
- Check missing & duplicate values<br>
- Karena pada dataset ini kita tidak memiliki data duplikat dan missing value, maka bisa langsung dilakukan Feature Encoding procedure pada feature-feature kategorik. Label encoding dilakukan pada feature `Product_Importance` dan `Gender` serta One hot encoding dilakukan pada feature `Warehouse_Block` dan `Mode_of_Shipment`.<br>
- Kemudian dilanjutkan dengan melakukan Log/Exp Transformation pada feature `Discount_Offered` dan `Prior_Purchases`. Hal ini dilakukan agar dua feature yang semula distribusinya berbentuk positively skewed itu berubah mendekati distribusi normal. Hal ini penting dilakukan jika kedepannya kita perlu membuat model linear regresi yang membutuhkan asumsi persebaran data feature harus mendekati distribusi normal.<br>
- Setelah itu melakukan teknik Standardization pada feature `Weight_in_gms` yang berbentuk negatively skewed. Argumentasinya masih sama seperti poin sebelumnya, diharapkan dengan transformasi ini, persebaran data feature `Weight_in_gms` bisa mendekati distribusi normal.<br>
- Dan yang terakhir adalah melakukan Outliers Handling, kami mencoba dua alternatif. Outlier Handling dengan Filtering Z-Score < 3 dan Filtering min-max IQR Limit pada feature yang memiliki outlier terjauh (`Discount_Offered`).<br>

## Summary Stage 3
Untuk Stage 3 ini kami melakukan modeling eksperimen dengan berbagai macam alternatif data set yang sudah diolah pada stage 2, antara lain model dengan data set tanpa data treatment (masih original), data yang sudah di log transform (ingin mencari tahu apakah jika sebaran semua feature sudah mendekati distribusi normal bisa mempengaruhi performa model?), dan data set yang sudah dilakukan outlier filtering (Apakah dengan mengurangi noise/outlier bisa memperbaiki performa model?).<br>
Tahapan-tahapan yang dilakukan:<br>
• Split features & target<br>
• Split data into data train & data test<br>
• Train model dengan algoritma yang berbeda seperti Logistic Regression, Random Forest, XGBoost, dan AdaBoost<br>
• Evaluate model menggunakan Recall, Precision, Average Precision, dan AUC<br>
• Validate model menggunakan train dan test accuracy <br>
• Hyperparameter tuning menggunakan beberapa hyperparameter tertentu.<br>

Adapun dalam proses mencoba sebuah algorithma dan model, kami menetapkan syarat dan ketentuan sebagai berikut:<br>
• One hot encoding yang di drop adalah ship dan gudang F, ship memiliki multikol paling tinggi terhadap fitur mode of shipment lainnya, sedangkan gudang F memiliki multikol paling tinggi terhadap fitur gudang lainnya.<br>
• Scoring yang digunakan hyperparameter tuning semua algorithma adalah ROC AUC, ROC AUC sudah mengakomodir False negative dan False positive dalam perhitungannya, ROC AUC juga lebih robust terhadap imbalance, data kita sedikit imbalance (59%-41%).<br>
• Hyperparameter yang digunakan pada Hyperparameter Tuning Log Regression adalah 'Best penalty' dan 'Best C'.<br>
• Hyperparameter yang digunakan pada Hyperparameter Tuning kNN adalah 'Best n_neighbors', 'Best p', 'Best algorithm', dan 'weights'.<br>
• Hyperparameter yang digunakan pada Hyperparameter Tuning Decision Tree adalah 'max_depth', 'min_samples_split', 'min_samples_leaf', 'max_features', 'criterion', dan 'splitter'.<br>
• Hyperparameter yang digunakan pada Hyperparameter Tuning Random Forrest adalah 'n_estimators', 'bootstrap', 'criterion', 'max_depth', 'min_samples_split', 'min_samples_leaf', 'max_features', dan 'n_jobs'.<br>
• Hyperparameter yang digunakan pada Hyperparameter Tuning AdaBoost adalah 'n_estimators', 'learning_rate', dan 'algorithm'.<br>
• Hyperparameter yang digunakan pada Hyperparameter Tuning XGBoost adalah 'max_depth', 'min_child_weight', 'gamma', 'tree_method', 'colsample_bytree',  'eta',  'lambda', dan 'alpha'.<br>
-->
