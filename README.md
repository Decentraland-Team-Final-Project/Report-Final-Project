# Report-Final-Project - Data Set E-Commerce Shipping
Data source : https://www.kaggle.com/prachi13/customer-analytics
## Kelompok 8 : Decentraland
## **Project Overview** 
• Mencari insight dari dataset dengan Exploratory Data Analysis (EDA) <br>
• Melakukan data cleansing, data processing, data engineering untuk menyiapkan data sebelum modeling (Pre-Processing) <br>
• Dari beberapa feature yang ada, mencoba untuk membuat model prediksi apakah shipping deliveries akan diterima telat atau tepat waktu pada customers <br>
• Memberikan analisis rekomendasi/solusi dan keuntungan apa saja yang bisa diperoleh jika performa model yang kita bangun memuaskan. 

## Summary Stage 1
Pada stage 1 kami melakukan Exploratory Data Analysis pada Data Set E-Commerce Shipping dengan Data Set:
| Variable | Type | Definition | Example |
| ----------- | ----------- | ----------- | ----------- |
| ID | Nominal | Customer ID Number | 10, 15, 10995, 10996
| Warehouse_Block | Nominal | Warehouse to Store the Product | A, B, C, D, F
| Mode_of_Shipment | Nominal | Mode of Product Shipping | Flight, Road, Ship
| Customer_Care_Calls | Discrete | Number of Calls Made | 1, 2, 5, 6
| Customer_Rating | Ordinal | Company Rating by Customers | 5: Best - 4: Better - 3: Neutral - 2: Bad - 1: Worst
| Cost_of_The_Product | Discrete | Cost of Product in US Dollars | 177, 216, 236, 182
| Prior_Purchases | Discrete | Number of Prior Purchase | 3, 2, 6
| Product_Importance | Ordinal | Product Importance Parameter | Low, Medium, High
| Gender | Nominal | Customer Gender | Male, Female
| Discount_Offered | Discrete | Product Discount in US Dollars | 65, 10, 16
| Weight_in_gms | Continous | Product Weight in grams | 4953, 5676, 2171
| Late_Shipment | Nominal | Target Variable, 1: NOT reached on time - 0: REACHED on time | 1, 0<br>

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

