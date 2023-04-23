# Hotel-Reservations-Cancellation-Prediction

Project Background
Saya menggunakan dataset yang berasal dari kaggle, untuk penjelasan singkatnya adalah sebagai berikut, Sebuah sarana reservasi hotel secara online mengindikasikan kemungkinan pemesanan kamar dan dapat juga melihat perilaku pelanggan. Sebagian besar pemesanan hotel dibatalkan karena sebuah alasan atau ketidakhadiran. Alasan umum pembatalan meliputi perubahan rencana, bentrok penjadwalan, dan lain sebagainya

1. Data Pipeline
Pertama dilakukan pemanggilan raw data dan menyimpannya pada sebuah variable, hal pertama yang dilakukan adalah memeriksa apakah data tersebut memeiliki duplikasi dan memiliki inkonsistensi, kemudian pada data tersebut ditemukan beberapa kolom yang tidak perlu digunakan misalanya Booking_Id, karena kolom tersebut tidak informatif, untuk itu perlu dilakukan pembuangan kolom. Kemudian dilakukan casting data, ada beberapa data yang memiliki tipe yang kurang pas, sehingga perlu diubah. Setelah semua itu dilakukan. Lalu dilakukan pemisahan antara kolom target dan kolom predictor, kemudian dipisah lagi proporsinya menjadi 3 bagian, yaitu data train, data test, da n data validasi.

2. Preprocessing
Fokus utama dari proses ini adalah melakukan persiapan pada data yang akan dilakukan pengujian model. Pertama dilakukan pengecekan apakah ada null atau tidak dalam data tersebut, untuk itu dibuat sebuah fungsi untuk memeriksa apakah ada null atau nan dalam data tersebut, hasilnya tidak ada. Kemudian untuk memenuhi kebutuhan permodelan, maka semua tipe data haruslah berbentuk numerik, permasalahannya terdapat beberapa kolom yang bertipe kategorikal atau string, untuk itu dilakukan proses One Hot Encoding, proses tersebut mengubah, dalam contohnya kolom room_type_resereved yang berisi beberapa kategori, kategori menjadi numerik. Kemudian dalam kolom target, yaitu kolom booking_status, dilakukan label encoder. Kemudian, karena data ini tidak memiliki proporsi yang seimbang, perlu dilakukan metode undersampling dan oversampling, agar tidak terjadi bias.

3. Modelling
Pada tahap modelling, dilakukan beberapa metode dan algotitma, mengingat ini adalah supervised model maka model yang digunakan antara lain xgboost, KNN, logistic regression, dan random forest. Kemudain dilakukan hyperparameter tuning pada model-model tersebut, seperti membuat range atau rentang n_estimator pada xboost, min sample split dan leave pada KNN dan lain sebagainya. Dalam pengujian model ini, akan dipilih model mana yang paling baik digunakan untuk nanti digunakan pada proses selanjutnya

4. Unit testing
Setelah proses-proses tersebut dilakukan maka perlu dilakukan unit testing, dengan menggukan library pytest, maka kita dapat mengecek apakah fungsi yang kita buat sudah dapat berjalan dengan baik atau belum. Hal ini dilakukan karena untuk mengantisipasi error dan kesalahan pada model setelah dilakukannya deployment. Pada project ini saya melakukan unit testing terhadap beberapa fungsi seperti nan_detector, test_ohe_transform, dan test le_transform

5. API
Dalam proses ini, saya melakukan passing data ke localhost saya menggunakan fastAPI. Pertama ada parameter yang berisi home, dikarenakan home ini hanya menampilkan tulisan saja maka saya menggunakan method GET. Kemudian untuk passing nilai-nilai predictor yang kemudian akan menampilkan hasil prediksi, saya menyimpannya pada parameter predict yang berbentuk method POST
berikut adalah format message untuk melakukan prediksi tersebut:

{
  "room_type_reserved": "2",
  "no_of_adults": 2,
  "no_of_children": 2,
  "avg_price_per_room": 100,
  "no_of_weekend_nights": 2,
  "no_of_week_nights": 2,
  "required_car_parking_space": 0,
  "lead_time": 200,
  "arrival_year": 2017,
  "arrival_month": 2,
  "arrival_date": 2,
  "repeated_guest": 1,
  "no_of_previous_cancellations": 5,
  "no_of_previous_bookings_not_canceled": 12,
  "no_of_special_requests": 2
}


6. Streamlit
Proses ini adalah bentuk lain dari pengoperasian API tadi, mungkin bedanya adalah User Design yang lebih rapi dan teratur, pada dasarnya adalah pengisian nilai-nilai predictor yang akan mengembalikan hasil atau prediksi berdasarkan nilai-nilai prediktor yang kita isi
