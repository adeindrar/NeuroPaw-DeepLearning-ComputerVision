# Computer Vision Prediksi Gambar Kucing, Anjing dan Manusia 📷

Project ini akan membuat model Computer Vision dengan Artificial Neural Nerwork yang akan mempelajari pola visual dan membentuk representasi fitur dari data gambar secara otomatis. Pembuatan model akan mengklasifikasikan gambar manusia, anjing dan kucing yang akan digunakan dalam sistem otomatisasi seperti kamera pintar yang dapat mengenali siapa atau apa yang tertangkap kamera. Dengan demikian lingkungan kantor atau pusat belanja akan terjaga dari hewan atau makhluk hidup yang tidak kita inginkan.

## Daftar Isi 🗒️
1. [Link Terkait Project](#link-terkait-project-)
2. [Project Overview](#project-overview-)
3. [Latar Belakang Masalah](#latar-belakang-masalah-)
4. [Metode yang Digunakan](#metode-yang-digunakan-️)
5. [Kesimpulan, Model Improvement, Business Insight, Potensi Kerugian](#kesimpulan-model-improvement-business-insight-potensi-kerugian-)
6. [File yang Tersedia](#file-yang-tersedia-)
7. [Libraries](#libraries-)
8. [Author](#author-️)

## Link Terkait Project ⛓️‍💥

 - [Dataset](https://www.kaggle.com/datasets/raunakgola/paws-people-and-pals-a-visual-trio)
 - [Deployment NeuroPaw](https://huggingface.co/spaces/adeindrar/NeuroPaw)

## Project Overview 📝

Dalam proyek ini, saya melakukan berbagai proses untuk menghasilkan model terbaik. Tahapan-tahapan untuk menghasilkan model terbaik ini terdiri dari beberapa bagian hingga nanti akan membandingkan 2 model untuk menentukan model terbaik:

1. **Import Libraries**:
    - Import seluruh library yang diperlukan dalam proses pembuatan model agar mudah dibaca saat memerlukan dokumentasi.

2. **Data Loading**:
    - Load dataset yang akan digunakan sebagai acuan model, buat 2 dataframe yang terdiri dari data train dan test.

3. **Exploratory Data Analysis (EDA)**:
    - Melakukan analisis dengan mengambil sample gambar dari data train untuk melihat beberapa karakteristik dari gambar kucing, anjing dan manusia. Seperti warna dan bentuk, ukuran, ruang warna (RGB, CMYK), angle, dan karakteristik lainnya.

4. **Feature Engineering**:
    - Pada bagian ini dilakukan data augmentation pada data train agar data semakin bervariasi, lalu lanjut memisahkan data train dan val dari dataframe train. Lanjut mengambil data test dari dataframe test. Masing-masing class ditetapkan cat:0, dog:1, human:2.

5. **ANN Training (Sequential API)**:
    - Melakukan model definition dimana dilakukan pembangunan arsitektur pada model pertama.
    - Selanjutnya dilakukan model training sebanyak 50 epoch untuk melihat performa pada model.
    - Melakukan model evaluation yang terdiri dari visualisasi loss dan accuracy pada model, score predict pada data test, melihat nilai classification report (precision, recall dan f1-score), melihat karakteristik masing-masing TP,FP,FN dan TN.
    - Memberikan insight dari model pertama.

6. **ANN Improvement (Sequential API)**:
     - Melakukan model definition dimana dilakukan pembangunan arsitektur pada model kedua.
    - Selanjutnya dilakukan model training sebanyak 50 epoch untuk melihat performa pada model.
    - Melakukan model evaluation yang terdiri dari visualisasi loss dan accuracy pada model, score predict pada data test, melihat nilai classification report (precision, recall dan f1-score), melihat karakteristik masing-masing TP,FP,FN dan TN.
    - Memberikan insight dari model kedua.
    - Membandingkan model pertama dan kedua dan menentukan model terbaik.

7. **Model Saving**:
    - Save model terbaik untuk di test menggunakan data inference.
    - Save juga class_name/class_indices untuk prediksi data inference nanti.

## Latar Belakang Masalah 🧐

Untuk menjaga kenyamanan, kesehatan dan ketertiban dalam sebuah ruangan diperlukan adanya aturan-aturan yang berlaku. Salah satu contohnya adalah aturan siapa saja yang diperbolehkan masuk dalam sebuah ruangan seperti kantor atau pusat belanja. Maka dari itu diperlukan adanya sistem pemantauan keamanan yang dapat membedakan antara manusia dan objek visual lainnya. Umumnya hewan peliharaan ataupun liar merupakan makhluk hidup yang biasanya sering muncul di sekitar kita. Hewan ini biasanya berupa anjing dan kucing maka dari itu project kali ini akan membuat model klasifikasi yang memiliki kemampuan dalam membedakan manusia, anjing dan kucing.

## Metode yang Digunakan 🛠️

- Computer vision
- ANN Training
- ANN Improvement
- Data Augmentation

## Kesimpulan, Model Improvement, Business Insight, Potensi Kerugian 🧠

**Kesimpulannya**:

Kemampuan model dalam memprediksi objek visual dapat ditentukan dengan membuat arsitektur yang tepat. Dimana arsitektur yang telah ditambahkan beberapa regulasi dapat meningkatkan performance pada model sehingga model_2 memiliki akurasi 91% pada data testnya. Setelah dilakukan inference, hanya terdapat satu kesalahan prediksi yaitu dog diprediksi sebagai human. Ini merupakan hasil yang cukup memuaskan mengingat score pada model yang cukup tinggi.

**Model Improvement:**

Model dapat dilakuakan improvement lanjutan seperti:
- Menaikkan fine-tuning dropout rate misal menjari 0.3-0.5.
- Mengurangi atau menambahkan unit di Dense layer
- Menggunakan EarlyStopping + ReduceLROnPlateu agar training lebih efisien
- Eksperimen optimizer selain adam
- Menambahkan dataset yang lebih bervariasi tidak hanya menampilkan wajah yang menghadap kamera

**Business Insight:**

Dalam konteks bisnis aplikasi deteksi gambar cat, dog dan human agar dapat mengontrol akses ke sebuah ruangan. Beberapa ketentuan harus dimiliki yaitu:
- Sistem harus sangat andal -> kesalahan deteksi bisa langsung berdampak pada operasional
- Contoh dampaknya:
    - False negative (anjing/kucing tidak terdeteksi) -> pintu terbuka dan kebersihan terganggu, potensi komplain pelanggan.
    - False positive (manusia terdeteksi sebagai kucing/anjing) -> pintu tidak terbuka, ganggu kenyamanan pengguna dan terjadi hambatan pekerjaan.
- Akurasi tinggi saja tidak cukup sehingga kita perlu:
    - Robustness atau stabil menghadapi berbagai kondisi pencahayaan, pose dan angle.
    - Low false positive/negative.
    - Efisiensi (model yang ringan, cepat untuk real-time).

**Potensi Kerugian**
- Operational failure - jika model salah memprediksi, toko atau kantor bisa kehilangan reputasi sehingga membuat pelanggan kecewa bahkan kehilangan pendapatan.
- Maintenance cost - model yang belum stabil butuh sering diperbarui atau diperbaiki, yang akan menambah beban tim teknis.
- Latency issue - dengan total parameter 295.363 (1.13 MB), model tidak terlalu besar tapi tidak juga super ringan. Jika hardware pintu otomatis terbasar, waktu memprediksi inference bisa jadi masalah.
- Scalability dan Security Risk - jika model tidak diuji di skenario nyata seperti kamera dengan kualitas buruk/malam hari, bisa bocor dan gagal secara tak terduga.

## File yang Tersedia 📂

- `inference_ade_indra.ipynb`: Jupyter Notebook yang berisikan data inference atau data yang belum pernah dilihat oleh model untuk melihat performa model.
- `computer_vision_ade_indra.ipynb`: Jupyter Notebook berisi langkah-langkah analisis data, pemilihan model terbaik, evaluasi model dan insight yang didapatkan.
- `class_name.txt` : Isi dari class_indices, cat:0, dog:1, human:2.
- `README.md`: Penjelasan dari proyek ini.
- `.gitignore`: Untuk mengignore dataset yang digunakan karen terlalu besar.


## Libraries 📚
- Pandas
- Numpy
- Seaborn
- Matplotlib
- Tensorflow
- jmd_imagescraper
- Scikit-learn

## Author ✍️
**Ade Indra Rukmana**

[LinkedIn](https://www.linkedin.com/in/ade-indra-rukmana/)