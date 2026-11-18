# Pengambilan dan Penyusunan Data: Kualitas Udara, Cuaca, dan Kendaraan Bermotor di Kota-Kota Besar Indonesia

Bagian dari proyek akhir *Analisis Kualitas Udara dan Pengaruh Faktor Cuaca serta Kendaraan Bermotor di Kota-Kota Besar Indonesia*, mata kuliah [Data Wrangling], Program Studi S1 Sains Data, Universitas Negeri Surabaya.

Repositori ini berisi notebook yang mengambil data dari sumber terbuka dan menyusunnya menjadi satu dataset harian siap pakai.

## Cakupan

- **Kota:** Jakarta, Bandung, Semarang, Surabaya, Medan, Makassar
- **Periode:** 1 Januari 2023 – 31 Desember 2025 (1.096 hari)
- **Hasil:** dataset harian dengan 6.576 baris (kota-hari) dan 27 kolom, tanpa data ganda dan tanpa data hilang

## Sumber Data

| Data | Sumber | Resolusi |
|---|---|---|
| Polutan udara (PM2.5, PM10, CO, NO2, SO2, O3, AOD, US AQI) | [Open-Meteo Air Quality API](https://open-meteo.com/en/docs/air-quality-api) | Per jam (sumber model CAMS 3-jam) |
| Cuaca (suhu, kelembapan, curah hujan, angin, tekanan, awan) | [Open-Meteo Historical Weather API](https://open-meteo.com/en/docs/historical-weather-api) | Per jam (reanalisis) |
| Jumlah kendaraan bermotor (mobil penumpang, bus, truk, sepeda motor) | Badan Pusat Statistik, *Jumlah Kendaraan Bermotor Menurut Provinsi dan Jenis Kendaraan (Unit)* | Tahunan, per provinsi |

Data kendaraan diambil dari tabel BPS 2023, 2024, dan 2025, lalu dimasukkan langsung ke notebook (variabel `BPS_MANUAL`). Setiap kota dipetakan ke provinsinya: Jakarta (DKI Jakarta), Bandung (Jawa Barat), Semarang (Jawa Tengah), Surabaya (Jawa Timur), Medan (Sumatera Utara), Makassar (Sulawesi Selatan).

## Cara Menjalankan

1. Buka `[nama_file_notebook].ipynb` di Google Colab.
2. Jalankan sel secara berurutan dari sel 1 sampai sel 6.
3. Sel 3 mengunduh data dari Open-Meteo dan memakan waktu beberapa menit.
4. Hasil tersimpan di `data/processed/dataset_harian.csv`.

Pustaka yang dipakai: `requests`, `pandas`, `numpy` (sudah tersedia di Colab).

## Isi Dataset Harian

| Kelompok | Kolom |
|---|---|
| Kunci | `kota`, `tanggal`, `provinsi`, `tahun`, `bulan` |
| Kualitas udara | `pm2_5`, `pm10`, `carbon_monoxide`, `nitrogen_dioxide`, `sulphur_dioxide`, `ozone`, `aerosol_optical_depth`, `us_aqi`, `pm2_5_maks` |
| Cuaca | `suhu_rata`, `kelembapan_rata`, `curah_hujan_total`, `angin_rata`, `tekanan_rata`, `awan_rata`, `arah_angin_dominan` |
| Kendaraan | `mobil_penumpang`, `bus`, `truk`, `sepeda_motor`, `total_kendaraan`, `proporsi_motor` |

Data per jam diagregasi menjadi harian: rata-rata untuk polutan dan sebagian besar variabel cuaca, jumlah total untuk curah hujan, dan rata-rata vektor untuk arah angin.

## Catatan dan Keterbatasan

- Data kualitas udara Open-Meteo adalah keluaran model atmosfer (CAMS), bukan pengukuran stasiun. Resolusi asli sumber globalnya 3 jam dan sekitar 45 km, sehingga nilai per jam merupakan hasil interpolasi.
- Data kendaraan BPS bersifat tahunan dan tingkat provinsi, sehingga nilainya sama untuk semua hari dalam satu tahun dan tidak mewakili kota secara tepat.
- Angka kendaraan 2025 bertanda (*) pada tabel BPS, yaitu angka sementara yang dapat direvisi.
- Kendaraan yang dicatat BPS mencakup semua jenis kecuali kendaraan TNI/Polri dan korps diplomatik.

## Atribusi

Data kualitas udara dan cuaca disediakan oleh [Open-Meteo](https://open-meteo.com/) (termasuk data CAMS dan reanalisis ERA5). Data kendaraan bermotor bersumber dari Badan Pusat Statistik (BPS). Penggunaan data ini untuk keperluan akademik dan non-komersial.

## Penulis

[Icha Meisya Kurnia] ([25031554047]), Universitas Negeri Surabaya.
