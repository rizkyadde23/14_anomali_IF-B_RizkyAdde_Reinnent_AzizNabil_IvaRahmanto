# Prediksi Harga Properti di Portugal dengan Regresi

Proyek **Data Science UTS 2026/2027** ini mengeksplorasi data listing properti di Portugal sebagai tahap awal untuk membangun model prediksi harga properti menggunakan pendekatan regresi.

Notebook utama, `UTS_DataScience_EDA_Properti_Portugal.ipynb`, berfokus pada **Business Understanding dan Data Understanding (Exploratory Data Analysis/EDA)**. Analisis dilakukan untuk memahami karakteristik data, memeriksa kualitasnya, menemukan pola harga dan fitur properti, serta menyusun dasar untuk tahap *data preparation* dan pemodelan berikutnya.

> **Catatan ruang lingkup:** notebook ini adalah tahap eksplorasi dan pemahaman data. Judul proyek mengarah pada prediksi dengan regresi, tetapi notebook ini belum melatih atau mengevaluasi model regresi.

## Tujuan Proyek

- Memahami struktur dataset listing properti di Portugal.
- Mengidentifikasi tipe data, nilai kosong, duplikasi, outlier, dan inkonsistensi.
- Mengeksplorasi hubungan harga dengan karakteristik fisik, lokasi, dan sertifikat energi properti.
- Memeriksa representativitas data dan potensi bias sampel.
- Menentukan langkah validasi awal untuk menyiapkan data sebelum pemodelan regresi.

## Dataset

Notebook membaca dataset CSV bernama `portugal_listinigs.csv` (perhatikan ejaan nama file yang digunakan pada konfigurasi notebook).

- **Unit observasi:** satu baris mewakili satu listing properti.
- **Target potensial:** `Price`, yaitu harga penawaran properti dalam Euro (€).
- **Cakupan analisis:** seluruh listing untuk memahami data, kemudian subset properti hunian bertipe `Apartment` dan `House` untuk sejumlah analisis dan aturan validasi.
- **Ukuran acuan dalam notebook:** 188.797 baris dan 23 kolom. Jumlah aktual dapat berbeda jika file dataset diperbarui atau diganti.

Beberapa kolom yang dianalisis antara lain:

| Kelompok | Contoh variabel | Kegunaan |
|---|---|---|
| Harga | `Price` | Harga penawaran properti |
| Lokasi | `District`, `City`, `Town` | Membandingkan distribusi listing dan harga antarwilayah |
| Tipe properti | `Type` | Memahami komposisi jenis listing |
| Luas | `TotalArea`, `LivingArea`, `BuiltArea`, `LotSize` | Mengeksplorasi hubungan ukuran dan harga |
| Fasilitas/ruangan | `NumberOfBedrooms`, `NumberOfBathrooms`, `TotalRooms`, `NumberOfWC`, `Parking`, `Garage` | Memahami karakteristik properti |
| Informasi bangunan | `ConstructionYear`, `Floor`, `ConservationStatus` | Mengeksplorasi usia dan kondisi bangunan |
| Energi | `EnergyCertificate`, `EnergyEfficiencyLevel`, `ElectricCarsCharging` | Melihat ketersediaan dan kategori informasi energi |
| Waktu publikasi | `PublishDate` | Memeriksa pola data terkait waktu publikasi |

Definisi, tipe data, jumlah nilai unik, rentang nilai, dan persentase nilai kosong diperiksa langsung melalui *data dictionary* yang dibuat oleh notebook.

## Tahapan Analisis

Notebook disusun mengikuti alur berikut.

1. **Konfigurasi dan pemuatan data**  
   Mengimpor pustaka, menetapkan seed, membaca file CSV, dan memeriksa ukuran serta tipe data.

2. **Pembuatan data dictionary**  
   Merangkum karakteristik setiap kolom, termasuk tipe data, jumlah nilai unik, nilai kosong, dan statistik ringkas.

3. **Pemeriksaan kualitas data**
   - Mengukur *missing values* per kolom dan memeriksa pola kekosongan bersama.
   - Mengidentifikasi duplikasi penuh dan kandidat duplikasi berdasarkan kombinasi atribut listing.
   - Memeriksa distribusi harga, kemencengan (*skewness*), serta nilai ekstrem pada harga dan variabel ukuran/jumlah.
   - Memeriksa inkonsistensi kategori atau format pada sejumlah kolom.

4. **Validasi awal data hunian**  
   Memilih listing bertipe `Apartment` dan `House`, lalu menerapkan tahapan validasi seperti penghapusan duplikasi dan pemeriksaan rentang harga serta variabel terkait. Detail aturan dan jumlah baris pada setiap tahap ditampilkan oleh notebook.

5. **Exploratory Data Analysis (EDA)**
   - Komposisi tipe properti.
   - Distribusi listing dan perbedaan harga antar-distrik.
   - Perbandingan harga berdasarkan sertifikat energi.
   - Korelasi Spearman antarvariabel numerik dan hubungan luas terhadap harga.
   - Perbandingan harga per meter persegi berdasarkan kondisi, tahun pembangunan, dan fasilitas.

6. **Representativitas dan potensi bias sampel**  
   Memeriksa konsentrasi listing berdasarkan distrik serta distribusi wilayah untuk memahami keterbatasan representasi dataset.

7. **Ringkasan angka kunci**  
   Menampilkan kembali metrik penting agar hasil analisis dapat dibandingkan dengan laporan UTS.

## Teknologi dan Pustaka

- **Python** — bahasa pemrograman untuk analisis.
- **Jupyter Notebook** — lingkungan kerja interaktif.
- **Pandas** — pemuatan, manipulasi, dan analisis data tabular.
- **NumPy** — komputasi numerik.
- **Matplotlib** — visualisasi distribusi, perbandingan, dan hubungan antarvariabel.

## Struktur Proyek

Susunan file yang disarankan:

```text
project/
├── UTS_DataScience_EDA_Properti_Portugal.ipynb
├── portugal_listinigs.csv
├── README.md
├── requirements.text
└── figures/
    └── # Grafik hasil analisis yang disimpan oleh notebook
```

Folder `figures/` dibuat secara otomatis oleh notebook. Grafik yang dihasilkan disimpan di folder tersebut ketika sel terkait dijalankan.

## Cara Menjalankan

### 1. Siapkan Python dan virtual environment (opsional, tetapi disarankan)

Windows:

```bash
python -m venv .venv
.venv\Scripts\activate
```

macOS/Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 2. Instal dependensi

```bash
pip install pandas numpy matplotlib jupyter
```

### 3. Letakkan dataset

Tempatkan `portugal_listinigs.csv` di direktori yang sama dengan notebook. Jika nama atau lokasi file berbeda, sesuaikan nilai `DATA_PATH` pada sel konfigurasi notebook. Notebook juga mendukung pengaturan lokasi file melalui environment variable `DATA_PATH`.

Contoh di PowerShell:

```powershell
$env:DATA_PATH = "path\ke\dataset.csv"
```

### 4. Jalankan notebook

```bash
jupyter notebook
```

Buka `UTS_DataScience_EDA_Properti_Portugal.ipynb`, kemudian jalankan seluruh sel secara berurutan menggunakan **Run All**. Jalankan dari awal agar variabel dan hasil perhitungan yang dibutuhkan oleh sel berikutnya sudah tersedia.

## Output yang Dihasilkan

- Ringkasan ukuran dan struktur dataset.
- *Data dictionary*.
- Tabel dan visualisasi kualitas data.
- Ringkasan pemeriksaan duplikasi, outlier, dan validasi awal.
- Grafik distribusi tipe properti, harga per wilayah, dan kategori sertifikat energi.
- Analisis korelasi serta hubungan luas properti dengan harga.
- Tabel perbandingan harga per meter persegi berdasarkan kondisi, usia, dan fasilitas.
- Ringkasan angka kunci untuk membantu penyusunan laporan.
- File grafik pada folder `figures/`.

Angka hasil analisis bergantung pada versi dataset yang digunakan. Karena itu, gunakan file CSV yang sama dengan laporan jika ingin mereproduksi angka dan grafik secara konsisten.

## Catatan Interpretasi

- Harga yang sangat tinggi atau jauh dari mayoritas data tidak otomatis merupakan kesalahan; nilai tersebut perlu diperiksa berdasarkan konteks properti.
- Nilai kosong dapat menunjukkan informasi yang tidak dicantumkan pada listing, bukan selalu berarti nilai sebenarnya nol.
- Hubungan atau korelasi antara suatu fitur dan harga tidak membuktikan hubungan sebab-akibat.
- Harga penawaran belum tentu sama dengan harga transaksi akhir.
- Konsentrasi listing pada wilayah tertentu dapat menyebabkan hasil analisis kurang mewakili seluruh Portugal.
- Aturan validasi yang diterapkan merupakan keputusan analitis yang perlu didokumentasikan dan ditinjau sebelum membangun model.

## Pengembangan Selanjutnya

Setelah tahap pemahaman data, pekerjaan dapat dilanjutkan dengan:

1. **Data Preparation:** menangani nilai kosong, duplikasi, kategori, tipe data, dan nilai ekstrem berdasarkan aturan yang terdokumentasi.
2. **Feature Engineering:** memilih atau membentuk fitur yang relevan serta menghindari kebocoran data (*data leakage*).
3. **Train-test split:** membagi data untuk pelatihan dan evaluasi dengan strategi yang sesuai.
4. **Modeling:** melatih model regresi sebagai baseline dan membandingkannya dengan model alternatif.
5. **Evaluation:** mengevaluasi model menggunakan metrik seperti MAE, RMSE, dan R².
6. **Kesimpulan:** mendokumentasikan performa, keterbatasan, dan kemungkinan penggunaan model.

## Kontributor

Proyek ini disusun oleh :  
1. Rizky Adde Rachmad / 123240150
2. Aziz Nabil Putra Darmawan / 123240239
3. Reinnent Rasika Zahrain / 123240242
4. Iva Rohmanto / 123240252
  
untuk memenuhi tugas **UTS Data Science Tahun Akademik 2026/2027**.

---
