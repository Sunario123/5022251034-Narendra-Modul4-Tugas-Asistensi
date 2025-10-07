# INSTITUT TEKNOLOGI SEPULUH NOPEMBER (ITS)  
## Laporan Tugas Asistensi Dasar Pemrograman P4  
---

## Identitas
| Komponen | Keterangan |
|-----------|-------------|
| **Nama** | Narendra Andhi Putra Pratama |
| **NRP** | 5022251034 |
| **Departemen** | Teknik Elektro |
| **Mata Kuliah** | Dasar Pemrograman |
| **Modul** | Modul 4 – Tugas Asistensi |
| **Topik** | Perhitungan Bunga Sederhana dan Bunga Majemuk |
| **Tanggal Praktikum** | 2 Oktober 2025 |

---

## Log Commit

| No | Tanggal | Commit Message | Deskripsi Singkat |
|----|----------|----------------|------------------|
| 1 | 2025-10-07 | `Initial Commit` | Meng-clone repository asli dari Mas Darren. |
| 2 | 2025-10-07 | `Fix struct name` | Mengubah nama struct `Rekenin` menjadi `Rekening`. |
| 3 | 2025-10-07 | `Add math.h` | Menambahkan library `<math.h>` untuk fungsi `pow()`. |
| 4 | 2025-10-07 | `Fix enum reference` | Memperbaiki penulisan `SIMPL` menjadi `SIMPLE`. |
| 5 | 2025-10-07 | `Final tested version` | Program berhasil dikompilasi dan berjalan dengan benar. |

---

## Deskripsi Program

Program ini digunakan untuk menghitung **total uang akhir nasabah** setelah dikenai **bunga sederhana (simple interest)** atau **bunga majemuk (compound interest)**.  
Data setiap nasabah disimpan menggunakan **struct** dan dialokasikan secara dinamis dengan `malloc()` agar program dapat menangani banyak nasabah secara fleksibel.

---

## Variabel Utama

| Nama Variabel | Tipe Data | Keterangan |
|----------------|------------|-------------|
| `nama` | `char[64]` | Nama lengkap nasabah |
| `pokok` | `double` | Jumlah uang awal yang disimpan |
| `rate` | `double` | Suku bunga per tahun (dalam desimal, misalnya 0.05 untuk 5%) |
| `tahun` | `int` | Lama waktu menabung (tahun) |
| `n_per_tahun` | `int` | Frekuensi kapitalisasi bunga per tahun |
| `tipe` | `InterestType` | Jenis bunga: sederhana (`SIMPLE`) atau majemuk (`COMPOUND`) |

---

## Rumus yang Digunakan

**1. Bunga Sederhana (Simple Interest):**
`A = P + (P x r x t)`


**Keterangan:**
- `A` = jumlah akhir setelah t tahun  
- `P` = pokok (uang awal)  
- `r` = suku bunga per tahun (dalam desimal)  
- `t` = lama menabung (tahun)

**2. Bunga Majemuk (Compound Interest):**
`A = P × (1 + r / n)^(n × t)`

**Keterangan:**
- `A` = jumlah akhir setelah menabung `t` tahun  
- `P` = pokok (uang awal)  
- `r` = suku bunga per tahun (dalam desimal)  
- `n` = frekuensi kapitalisasi per tahun  
- `t` = lama menabung (tahun)

---

## Fungsi Bunga Sederhana 

```c
double total_simple(const Rekening *r) {
    return r->pokok + r->pokok * r->rate * r->tahun;
}
```

## Fungsi Bunga Majemuk 
```c
double total_compound(const Rekening *r) {
    return r->pokok * pow(1 + r->rate / r->n_per_tahun, r->n_per_tahun * r->tahun);
}
```

## Perbaikan yang Dilakukan

| No | Jenis Perbaikan | Deskripsi |
|----|------------------|------------|
| 1 | **Struct Name Fix** | Mengubah `Rekenin` menjadi `Rekening` agar sesuai dengan referensi di fungsi utama. |
| 2 | **Library Addition** | Menambahkan `<math.h>` untuk menggunakan fungsi `pow()` pada perhitungan bunga majemuk. |
| 3 | **Enum Correction** | Mengganti `SIMPL` menjadi `SIMPLE` agar konsisten dengan tipe `InterestType`. |
| 4 | **Input Validation** | Menambahkan pengecekan input agar tidak terjadi perhitungan dengan nilai negatif. |
| 5 | **Final Testing** | Melakukan uji coba dengan berbagai kombinasi data dan memastikan hasil sesuai teori. |

---

## Contoh Input & Output

### Contoh Input Bunga Sederhana

```
=== Data Nasabah 1 ===
Nama lengkap: Narendra Andhi
Jumlah pokok (Rp): 1000000
Suku bunga per tahun (%), mis. 5 untuk 5%: 5
Lama menabung (tahun): 2
Pilih tipe bunga (1 = sederhana, 2 = majemuk): 1
```
---
### Contoh Output Bunga Sederhana
```
--- Ringkasan Rekening ---
Nama : Narendra Andhi
Pokok : Rp 1000000.00
Suku Bunga (%/thn) : 5.00%
Lama (tahun) : 2
Tipe : Bunga Sederhana
Total Bunga : Rp 100000.00
Total Akhir : Rp 1100000.00
```
---
### Contoh Input Bunga Majemuk
```=== Data Nasabah 1 ===
Nama lengkap: Narendra Andhi
Jumlah pokok (Rp): 1000000
Suku bunga per tahun (%), mis. 5 untuk 5%: 5
Lama menabung (tahun): 2
Pilih tipe bunga (1 = sederhana, 2 = majemuk): 2
Frekuensi kapitalisasi per tahun (mis. 12 untuk bulanan): 1
```
---
### Contoh Output Bunga Majemuk
```
--- Ringkasan Rekening ---
Nama : Narendra Andhi
Pokok : Rp 1000000.00
Suku Bunga (%/thn) : 5.00%
Lama (tahun) : 2
Kapitalisasi/thn : 1 x
Tipe : Bunga Majemuk
Total Bunga : Rp 10250.00
Total Akhir : Rp 1102500.00
```
---
