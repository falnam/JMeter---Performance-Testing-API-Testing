# JMeter - Performance & API Testing

## 📋 Daftar Isi
1. [Pengenalan JMeter](#pengenalan-jmeter)
2. [Persiapan dan Instalasi](#persiapan-dan-instalasi)
3. [Mengenal Interface JMeter](#mengenal-interface-jmeter)
4. [Performance Testing](#performance-testing)
5. [API Testing](#api-testing)
6. [Tips dan Troubleshooting](#tips-dan-troubleshooting)

---

## 🚀 Pengenalan JMeter

### Apa itu JMeter?
JMeter adalah software gratis (open-source) yang digunakan untuk menguji performa aplikasi web, API, database, dan server. Bayangkan JMeter sebagai alat untuk "menyerang" website Anda dengan banyak pengguna virtual untuk melihat apakah website masih bisa berjalan dengan baik.

### Kegunaan JMeter:
- **Performance Testing**: Mengukur seberapa cepat aplikasi merespons
- **Load Testing**: Menguji dengan beban pengguna normal
- **Stress Testing**: Menguji dengan beban pengguna yang sangat tinggi
- **API Testing**: Menguji apakah API bekerja dengan benar

---

## 🔧 Persiapan dan Instalasi

### Persyaratan Sistem
Sebelum menginstal JMeter, pastikan komputer Anda sudah memiliki:
- **Java 8 atau versi lebih baru** (JDK atau JRE)
- **RAM minimal 4GB** (disarankan 8GB untuk testing yang kompleks)

### Langkah Instalasi

#### 1. Install Java (jika belum ada)
- Download JDK dari [Oracle](https://www.oracle.com/java/technologies/downloads/) atau [OpenJDK](https://openjdk.org/)
- Install sesuai petunjuk untuk sistem operasi Anda

#### 2. Download JMeter
1. Buka website resmi: https://jmeter.apache.org/download_jmeter.cgi
2. Pilih versi terbaru
3. Download file **Binary** (format .zip), **BUKAN source code**
4. Contoh file: `apache-jmeter-5.6.3.zip`

#### 3. Extract dan Jalankan
1. Extract file zip yang sudah didownload
2. Masuk ke folder hasil extract → folder `bin`
3. Double-click file `jmeter.bat` (Windows) atau `jmeter.sh` (Mac/Linux)
4. Tunggu beberapa saat, JMeter akan terbuka

> 💡 **Tips**: Jika JMeter tidak mau terbuka, pastikan Java sudah terinstall dengan benar. Cek dengan menjalankan `java -version` di Command Prompt/Terminal.

---

## 🖥️ Mengenal Interface JMeter

Setelah JMeter terbuka, Anda akan melihat tampilan seperti ini:

### Komponen Utama JMeter

#### 1. **Test Plan** 
- Area utama tempat Anda membuat skenario testing
- Seperti "lembar kerja" untuk semua pengujian

#### 2. **Thread Group**
- Mengatur berapa banyak pengguna virtual yang akan dibuat
- Menentukan berapa lama testing akan berjalan
- **Cara menambahkan**: Klik kanan Test Plan → Add → Threads (Users) → Thread Group

**Pengaturan Thread Group:**
- **Number of Threads (Users)**: Jumlah pengguna virtual (misal: 100 users)
- **Ramp-Up Period**: Waktu untuk mencapai jumlah pengguna maksimal (misal: 10 detik)
- **Loop Count**: Berapa kali pengujian diulang (misal: 5 kali)

#### 3. **Sampler**
- Komponen yang mengirim permintaan ke server
- Jenis sampler yang sering digunakan:
  - **HTTP Request**: Untuk website dan API
  - **JDBC Request**: Untuk database
  - **FTP Request**: Untuk server FTP

#### 4. **Listener**
- Menampilkan hasil pengujian dalam bentuk grafik, tabel, atau log
- Jenis listener populer:
  - **View Results Tree**: Melihat detail setiap request
  - **Summary Report**: Ringkasan statistik
  - **Graph Results**: Grafik performa

#### 5. **Assertion**
- Memvalidasi apakah hasil sesuai harapan
- Contoh: Memastikan response code adalah 200 (berhasil)

---

## 📈 Performance Testing

Performance testing ada 2 jenis utama:

### 1. Load Testing (Pengujian Beban Normal)

**Tujuan**: Menguji apakah sistem bisa menangani beban pengguna normal.

**Contoh Skenario**: Menguji toko online dengan 500 pengguna bersamaan selama 10 menit.

#### Langkah-langkah:

**Step 1: Buat Test Plan Baru**
- File → New

**Step 2: Tambah Thread Group**
- Klik kanan Test Plan → Add → Threads (Users) → Thread Group
- Pengaturan:
  - Number of Threads: `500`
  - Ramp-Up Period: `100` (detik)
  - Loop Count: `Forever` atau angka tertentu

**Step 3: Tambah HTTP Request**
- Klik kanan Thread Group → Add → Sampler → HTTP Request
- Pengaturan:
  - Server Name: `tokopedia.com` (contoh)
  - Protocol: `https`
  - Path: `/` (halaman utama)

**Step 4: Tambah Listener**
- Klik kanan Thread Group → Add → Listener → Summary Report
- Klik kanan Thread Group → Add → Listener → Graph Results

**Step 5: Jalankan Test**
- Klik tombol Play (▶️) atau tekan Ctrl+R
- Perhatikan hasil di listener

### 2. Stress Testing (Pengujian Beban Tinggi)

**Tujuan**: Mencari batas maksimal sistem dengan beban sangat tinggi.

**Contoh Skenario**: Menguji dengan 5000 pengguna bersamaan selama 30 menit.

#### Perbedaan dengan Load Testing:
- Number of Threads: `5000` (lebih tinggi)
- Ramp-Up Period: `30` (lebih cepat)
- Loop Count: `Forever`

### Menganalisis Hasil Performance Test

#### Metrik Penting:
- **Response Time**: Waktu server merespons (semakin kecil semakin baik)
- **Throughput**: Jumlah request per detik yang bisa ditangani
- **Error Rate**: Persentase error (idealnya 0%)
- **CPU & Memory Usage**: Penggunaan resource server

#### Indikator Sistem Sehat:
- Response time < 3 detik
- Error rate < 1%
- Throughput stabil

---

## 🔌 API Testing

API Testing adalah pengujian untuk memastikan API bekerja dengan benar dan mengembalikan data yang tepat.

### Contoh: Testing REST API

Kita akan menguji API yang bisa menerima data baru (CREATE operation).

#### Langkah-langkah:

**Step 1: Buat Test Plan Baru**
- File → New

**Step 2: Tambah Thread Group**
- Klik kanan Test Plan → Add → Threads (Users) → Thread Group
- Pengaturan untuk API testing:
  - Number of Threads: `1`
  - Ramp-Up Period: `1`
  - Loop Count: `1`

**Step 3: Tambah HTTP Request untuk API**
- Klik kanan Thread Group → Add → Sampler → HTTP Request
- Pengaturan:
  - Server Name: `jsonplaceholder.typicode.com`
  - Path: `/posts`
  - Method: `POST`
  - Body Data:
```json
{
  "title": "Belajar JMeter",
  "body": "Praktikum API Testing",
  "userId": 1
}
```

**Step 4: Tambah HTTP Header Manager**
- Klik kanan HTTP Request → Add → Config Element → HTTP Header Manager
- Tambah header:
  - Name: `Content-Type`, Value: `application/json`
  - Name: `Accept`, Value: `application/json`

**Step 5: Tambah Assertion (Validasi)**

**Response Assertion:**
- Klik kanan HTTP Request → Add → Assertions → Response Assertion
- Field to Test: `Response Code`
- Pattern to Test: `201` (kode sukses untuk POST)

**JSON Assertion:**
- Klik kanan HTTP Request → Add → Assertions → JSON Assertion
- JSON Path: `$.title`
- Expected Value: `Belajar JMeter`

**Step 6: Tambah Listener**
- Klik kanan Thread Group → Add → Listener → View Results Tree

**Step 7: Jalankan Test**
- Klik tombol Play (▶️)
- Lihat hasil di View Results Tree

### Membaca Hasil API Testing

#### Hasil Sukses:
- ✅ Warna hijau di Results Tree
- Response code 200/201
- Data yang dikembalikan sesuai harapan

#### Hasil Gagal:
- ❌ Warna merah di Results Tree
- Response code 4xx/5xx
- Assertion failure message

---

## 💡 Tips dan Troubleshooting

### Tips untuk Performance Testing

1. **Mulai dengan beban kecil** (10-50 users) lalu tingkatkan
2. **Monitor resource server** selama testing
3. **Gunakan Ramp-Up Period** yang wajar untuk simulasi realistis
4. **Jangan jalankan GUI mode** untuk test besar (gunakan command line)

### Tips untuk API Testing

1. **Selalu tambah assertion** untuk validasi
2. **Test semua HTTP methods** (GET, POST, PUT, DELETE)
3. **Test dengan data valid dan invalid**
4. **Simpan token authentication** jika diperlukan

### Troubleshooting Umum

#### JMeter Tidak Mau Terbuka
- **Solusi**: Pastikan Java terinstall
- **Cek**: Jalankan `java -version` di command prompt

#### Error "Connection Refused"
- **Penyebab**: Server target tidak bisa diakses
- **Solusi**: Cek URL, koneksi internet, atau firewall

#### Memory Error (Out of Memory)
- **Penyebab**: Thread terlalu banyak untuk RAM yang tersedia
- **Solusi**: Kurangi jumlah thread atau tambah RAM

#### Response Time Sangat Tinggi
- **Penyebab**: Server overload atau koneksi lambat
- **Solusi**: Periksa beban server dan kecepatan internet

### Command Line untuk Test Besar

Untuk test dengan ribuan users, gunakan mode non-GUI:

```bash
jmeter -n -t TestPlan.jmx -l results.jtl
```

### Best Practices

1. **Simpan Test Plan** secara berkala (Ctrl+S)
2. **Beri nama yang jelas** untuk setiap komponen
3. **Dokumentasikan skenario testing** Anda
4. **Backup hasil testing** untuk analisis lebih lanjut
5. **Koordinasi dengan tim** sebelum stress testing production

---

## 🎯 Kesimpulan

JMeter adalah tool yang powerful untuk testing aplikasi. Dengan mengikuti tutorial ini, Anda sudah bisa:

- Melakukan performance testing (load & stress testing)
- Menguji API dengan berbagai skenario
- Menganalisis hasil testing
- Troubleshooting masalah umum

**Langkah selanjutnya:**
1. Praktikkan dengan aplikasi Anda sendiri
2. Pelajari fitur advanced seperti correlation dan parameterization
3. Integrasikan dengan CI/CD pipeline
4. Belajar scripting dengan Groovy untuk skenario kompleks

Selamat mencoba! 🚀
