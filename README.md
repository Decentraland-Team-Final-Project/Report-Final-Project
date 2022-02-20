# Report-Final-Project - Data Set E-Commerce Shipping
Data source : https://www.kaggle.com/prachi13/customer-analytics
## Kelompok 8 : Decentraland
## **Project Overview** 
• Mencari insight dari dataset dengan Exploratory Data Analysis <br>
• Melakukan data cleansing, data processing, data engineering untuk menyiapkan data sebelum modeling <br>
• Membuat model prediksi apakah shipping deliveries akan diterima telat atau tepat waktu pada customers <br>
• Memberikan analisis rekomendasi & keuntungan berdasarkan insights dan model prediksi. 

## Summary Stage 1
Pada stage 1 kami melakukan Exploratory Data Analysis pada Data Set E-Commerce Shipping dengan Data Set:
| Variable | Type | Definition | Example |
| ----------- | ----------- | ----------- | ----------- |
| ID | Nominal | Customer ID Number | 10, 15, 10995, 10996
| Warehouse_block | Nominal | Warehouse to Store the Product | A, B, C, D, F
| Mode_of_Shipment | Nominal | Mode of Product Shipping | Flight, Road, Ship
| Customer_care_calls | Discrete | Number of Calls Made | 1, 2, 5, 6
| Customer_rating | Ordinal | Company Rating by Customers | 5: Best - 4: Better - 3: Neutral - 2: Bad - 1: Worst
| Cost_of_the_Product | Discrete | Cost of Product in US Dollars | 177, 216, 236, 182
| Prior_purchases | Discrete | Number of Prior Purchase | 3, 2, 6
| Product_importance | Ordinal | Product Importance Parameter | Low, Medium, High
| Gender | Nominal | Customer Gender | Male, Female
| Discount_offered | Discrete | Product Discount in US Dollars | 65, 10, 16
| Weight_in_gms | Continous | Product Weight in grams | 4953, 5676, 2171
| Reached.on.Time_Y.N | Nominal | Target Variable, 1: NOT reached on time - 0: REACHED on time | 1, 0<br>

Dengan hasil pada statistik deskriptif sebagai berikut:
- Data terdiri dari 10.999 sampel (baris).
- Tidak ada null value di semua kolom.
- Tidak ada baris yang terduplikasi.
- Terdapat 10 fitur (variabel independen) dan 1 targeted variable (variabel dependen).
- Berdasarkan jenisnya, fitur terdiri dari 4 fitur kategorik (`Warehouse_block`, `Mode_of_Shipment`, `Product_importance`, dan `Gender`) dan 6 fitur numerik (`Customer_care_calls`, `Customer_rating`, `Cost_of_the_Product`, `Prior_purchases`, `Discount_offered`, dan `Weight_in_gms`).
- Satu target variabel yaitu `Reached.on.Time_Y.N` yang bertipe numerik dengan value yang sedikit tidak berimbang, hampir 60% data sampel termasuk ke dalam kategori pengiriman barang yang terlambat.
- Selain itu pada dataset tersebut juga tidak ditemukan data duplikat dan missing value.<br>

## Summary Stage 2
- Check missing & duplicate values<br>
- Karena pada dataset ini kita tidak memiliki data duplikat dan missing value maka langsung melakukan Feature Encoding pada feature 'Warehouse_Block', 'Mode_of_Shipment', 'Product_Importance', 'Gender' dan One hot encoding pada feature 'Warehouse_Block' dan 'Mode_of_Shipment'.<br>
- Kemudian dilanjutkan dengan melakukan Log/Exp Transformation pada feature 'Discount_Offered' dan 'Prior_Purchases'.<br>
- Setelah itu melakukan teknik Standardization pada feature 'Weight_in_gms'.<br>
- Dan yang terakhir adalah melakukan Outliers Handling menggunakan z-score pada semua feature dengan hasil jumlah baris sebelum outlier dihilangkan: 10999 dan jumlah baris setelah memfilter outlier: 10642.<br>

## Summary Stage 3
Untuk Stage 3 ini kami melakukan modeling dengan data yang sudah diolah pada stage 2 dengan kriteria data yang masih original, data yang sudah di log transform, data yang sudah diremove outlier.<br>
Dengan melakukan tahapan:<br>
• Split features & target<br>
• Split data into data train & data test<br>
• Train model dengan algoritma yang berbeda seperti Logistic Regression, Random Forest, XGBoost & AdaBoost<br>
• Evaluate model menggunakan Recall, Precision & AUC<br>
• Validate model menggunakan train dan test accuracy <br>
• Hyperparameter tuning<br>
