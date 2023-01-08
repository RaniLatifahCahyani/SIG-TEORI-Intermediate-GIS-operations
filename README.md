# SIG-TEORI-Intermediate GIS operations
# Performing Table Joins (QGIS3) (Project 1)
1.	Temukan file tl_2019_06_tract.zip di Browser QGIS dan kembangkan. Pilih file tl_2019_06_tract.shp dan seret ke kanvas
2.	Dialog Select Transformation akan meminta untuk mengkonversi dari EPSG:4269 ke EPSG:4326. Dialog ini menyajikan beberapa transformasi untuk mengkonversi antara koordinat antara proyeksi tersebut. Tinggalkan pilihan ke pilihan default dan klik OK
3.	Anda akan melihat layer tl_2019_06_tract dimuat di panel Layers. Lapisan ini berisi batas-batas bidang sensus di California. Klik kanan pada layer tl_2019_06_tract dan pilih Open Attribute Table
4.	Periksa atribut layer. Untuk menggabungkan tabel dengan lapisan ini, kita memerlukan atribut unik dan umum dari setiap fitur. Dalam hal ini, ada 8057 rekaman traktat individual dengan bidang GEOID. Kolom ini dapat menautkan lapisan ini dengan lapisan atau tabel lain yang berisi ID yang sama
5.	Untuk memuat data tabular, klik Open Data Source Manager
6.	Dalam dialog Pengelola Sumber Data, pilih Teks yang Dibatasi. Kemudian di sebelah kanan, klik ... di sebelah Nama file dan ramban ke folder yang tidak di-zip dengan CSV populasi California
7.	Sekarang di bawah Data Sampel, kita dapat memeriksa data bahkan sebelum memuatnya sebagai lapisan. Representasi menunjukkan bahwa tabel data berisi 2 baris header
8.	Untuk menghilangkan baris tajuk tambahan, di bawah Opsi Rekam dan Bidang atur Jumlah baris tajuk untuk dibuang ke 1. Sekarang tabel akan berisi tajuk kolom yang tepat. Karena lapisan ini hanya berisi data tabular, pilih Tanpa geometri (tabel hanya atribut) di bawah Definisi Geometri. Klik Add untuk menambahkannya sebagai layer dan kemudian klik Close untuk menutup kotak dialog ini
9.	CSV sekarang akan diimpor sebagai tabel ke QGIS dan muncul sebagai ACST5Y2019.S0101 di panel Lapisan. Sekarang klik kanan pada layer dan pilih Open Attribute Table
10.	Kolom ID berisi id unik untuk setiap record, yang dapat digunakan untuk menggabungkan tabel ini dengan layer tl_2019_06_tract. Jika Anda membandingkan nilai ID dengan kolom GEOID dari tl_2019_06_tract. Anda akan melihat bahwa itu diawali dengan 1400000US. Untuk menggabungkan kedua tabel ini dengan sukses, nilainya harus sama persis. Mari kita hapus awalan ini dan tambahkan kolom baru dengan 11 karakter terakhir yang berisi nilai yang sama persis
11.	Untuk membuat kolom baru dengan 11 digit terakhir, buka Processing Toolbox dengan pergi ke Processing ‣ Toolbox, dan cari dan temukan tabel Vector ‣ Algoritma kalkulator lapangan
12.Dalam dialog Kalkulator bidang, pilih ACST5Y2019.S0101 sebagai lapisan Input, masukkan geoid di Nama bidang, dan pilih string di Jenis Bidang Hasil. Sekarang cari substr dalam ekspresi. Kita dapat menggunakan fungsi ini untuk mengekstrak bagian yang diperlukan dari bidang id.
13. Masukkan ekspresi di bawah ini. Kami menggunakan fungsi substr dan mengekstrak nilai dari posisi -11 (nilai negatif dihitung dari akhir). Hasil akhir dapat dilihat di bagian Pratinjau. Klik Jalankan
14. Sekarang lapisan baru Dihitung akan dimuat di kanvas, mari kita periksa tabel atribut. Geoid kolom baru dengan nilai yang dapat disesuaikan dengan saluran sensus akan hadir
15. Untuk membuat gabungan tabel, buka Processing Toolbox dengan pergi ke Processing ‣ Toolbox, dan cari dan temukan Vector general ‣ Join atribut berdasarkan algoritma nilai bidang
16. Dalam dialog Gabungkan atribut berdasarkan nilai bidang, pilih tl_2019_06_tract sebagai lapisan Input dan GEOID sebagai bidang Tabel. Pilih Dihitung sebagai Input layer 2 dan geoid sebagai kolom Tabel 2. Di bawah kolom Layer2 untuk menyalin, klik ...
17. Periksa Nama Area Geografis, Perkirakan!!Jumlah!!Jumlah penduduk dan geoid. Klik Oke
18. Periksa catatan Buang yang tidak dapat digabungkan. Ini akan menghilangkan catatan tambahan apa pun di tabel populasi. Klik tombol ... di bawah layer gabungan untuk memilih lokasi file output dan pilih Save to File....
19. Beri nama geopackage keluaran sebagai california_total_population.gpkg . Klik Jalankan
20. Setelah pemrosesan selesai, verifikasi bahwa algoritme berhasil jika semua fitur 8057 digabungkan. Klik Tutup.
21. Anda akan melihat layer baru california_total_population dimuat di panel Layers. Pada titik ini, bidang dari file CSV digabungkan dengan lapisan saluran sensus. Sekarang setelah kita memiliki data kependudukan di lapisan sensus, kita dapat menatanya untuk membuat visualisasi distribusi kepadatan penduduk. Klik tombol Buka Panel Penataan Lapisan
22. Di panel Layer Styling, pilih Graduated dari menu drop-down. Saat kami ingin membuat peta kepadatan populasi, kami ingin menetapkan warna berbeda untuk setiap fitur saluran sensus berdasarkan kepadatan populasi. Kami memiliki populasi di bidang Estimasi!!Total!!Total populasi, dan bidang area di ALAND. Klik tombol Ekspresi, untuk menghitung persentase jumlah penduduk pada setiap saluran pencacahan
23. Masukkan ekspresi berikut untuk menghitung kepadatan populasi. Area fitur diberikan dalam kilometer persegi. Kami kemudian mengubahnya menjadi meter persegi dengan mengalikannya dengan 1000000 dan menghitung kepadatan penduduk dengan rumus Penduduk/Luas. Pratinjau hasilnya dan klik OK
24. Di Panel Penataan Lapisan, klik klasifikasikan dan masukkan kelas sebagai 10
25. Klik pada jalur warna untuk memilih jalur warna RdYlGn
26. Kerapatan yang lebih tinggi lebih penting, mari kita tetapkan warna hijau untuk kerapatan rendah dan merah untuk area dengan kerapatan tinggi. Klik pada jalur warna dan pilih Balikkan Jalur Warna
27. Sekarang kami memiliki visualisasi informasi kepadatan populasi yang sangat baik di California. Untuk membuatnya lebih baik, mari kita buat batas setiap saluran sensus transparan. Klik pada tab Simbol
28. Klik pada warna Stroke dan klik Stroke transparan
29. Tempat sampah dapat disesuaikan, klik pada Nilai ini akan memunculkan dialog untuk memasukkan nilai batas atas dan bawah
30. Setelah Anda puas menutup panel styling Layer. Kami sekarang memiliki visualisasi informasi kepadatan populasi yang terlihat bagus di California

LINK PROJECT : https://github.com/RaniLatifahCahyani/SIG-TEORI-Intermediate-GIS-operations/blob/main/SIG-Teori%20Intermediate%20Project%201/1.%20Performing%20Table%20Joins%20(QGIS3).qgz

LINK HASIL LAYOUT : https://github.com/RaniLatifahCahyani/SIG-TEORI-Intermediate-GIS-operations/blob/main/SIG-Teori%20Intermediate%20Project%201/layout%20project%201.jpeg


# Performing Spatial Joins (QGIS3) (Project 2)
1.	Temukan file nybb_19a.zip di Peramban QGIS dan kembangkan. Pilih layer nybb_19a/nybb.shp dan seret ke kanvas. Ini adalah lapisan poligon yang mewakili batas wilayah di kota New York.
2.	Selanjutnya, cari file V_SSS_SEGMENTRATING_1.zip dan perluas. Pilih layer dot_V_SSS_SEGMENTRATING_1_20190129.shp dan tambahkan ke kanvas. Ini adalah lapisan garis dari semua jalan di kota.
3.	Mari kita periksa atribut yang tersedia untuk setiap fitur lapisan dot_V_SSS_SEGMENTRATING_1_20190129. Klik kanan dan pilih Buka Tabel Atribut.
4.	Anda akan melihat atribut bernama Rating_B yang memiliki nilai dalam kisaran 0-10 yang mewakili peringkat segmen jalan. Atribut RatingWord memiliki peringkat deskriptif. Kita dapat menggunakan kolom Rating_B untuk menghitung rating rata-rata.
5.	Anda mungkin telah memperhatikan bahwa beberapa fitur memiliki peringkat NR. Ini adalah segmen yang tidak diberi peringkat. Memasukkan mereka ke dalam analisis kami tidak akan benar. Sebelum kita melakukan penggabungan spasial, mari siapkan Filter untuk mengecualikan rekaman ini. Klik kanan layer dot_V_SSS_SEGMENTRATING_1_20190129 dan pilih Filter
6.	Di Pembuat Kueri, ketikkan ekspresi berikut untuk memilih semua rekaman yang tidak diberi peringkat NR. Anda juga dapat membuat ekspresi secara interaktif dengan mengklik Bidang, Operator, dan memilih Nilai yang sesuai. Klik Oke
7.	Anda akan melihat lapisan dot_V_SSS_SEGMENTRATING_1_20190129 sekarang memiliki ikon filter yang menunjukkan bahwa ada filter aktif yang diterapkan pada lapisan ini. Sekarang kita bisa melakukan penggabungan spasial menggunakan layer ini. Pergi ke Memproses ‣ Toolbox.
8.	Cari dan temukan Vector general ‣ Gabungkan atribut berdasarkan algoritma lokasi (ringkasan). Klik dua kali untuk meluncurkannya
9.	Dalam dialog Gabung atribut berdasarkan lokasi (ringkasan), pilih nybb sebagai lapisan Input. Lapisan jalan dot_V_SSS_SEGMENTRATING_1_20190129 akan menjadi lapisan Gabung. Anda dapat membiarkan predikat Geometri ke Persimpangan default. Klik tombol ... di sebelah Bidang untuk meringkas
10.	Pilih Rating_B dan klik OK
11.	Demikian pula, klik tombol ... di sebelah Ringkasan untuk menghitung
12.	Pilih rata-rata sebagai operator ringkasan dan klik OK. Sekarang kita siap untuk memulai pemrosesan. Klik Jalankan
13.	Algoritme pemrosesan akan bekerja melalui fitur dan menerapkan gabungan spasial. Verifikasi bahwa pekerjaan pemrosesan berhasil dan klik Tutup.
14.Kembali ke jendela utama QGIS, Anda akan melihat layer Joined layer baru ditambahkan ke kanvas. Buka tabel atribut untuk lapisan ini. Anda akan melihat kolom baru Rating_B_mean ditambahkan ke input layer borough dengan rating rata-rata semua jalan yang bersinggungan dengan fitur tersebut
15. Sekarang kita dapat melakukan operasi terbalik. Terkadang analisis Anda memerlukan atribut dari lapisan lain berdasarkan hubungan spasial tetapi tidak menghitung ringkasan apa pun. Kita dapat menggunakan atribut Gabung dengan algoritme lokasi untuk analisis semacam itu. Tugasnya adalah menambahkan nama borough ke setiap fitur di layer jalan berdasarkan poligon borough mana yang bersinggungan dengannya. Sebelum kita menjalankan algoritme ini, mari hapus filter dari lapisan dot_V_SSS_SEGMENTRATING_1_20190129. Klik ikon filter dan tekan Hapus di Pembuat Kueri. Klik Oke
16. Matikan layer Joined di panel Layers. Temukan Vector general ‣ Gabung atribut berdasarkan algoritme lokasi di Processing Toolbox dan klik dua kali untuk meluncurkannya.
17. Pilih dot_V_SSS_SEGMENTRATING_1_20190129 sebagai layer Input dan nybb sebagai layer Join. Anda dapat membiarkan predikat Geometri ke Persimpangan default. Klik tombol ... di sebelah Fields untuk menambahkan dan memilih BoroName. Klik Oke.
18. Segmen garis dapat melintasi batas wilayah, jadi kami memilih tipe Penggabungan sebagai fitur Peti terpisah untuk setiap fitur yang terletak (satu-ke-banyak). Klik Jalankan
19. Setelah pemrosesan selesai, buka tabel atribut dari layer Joined yang baru ditambahkan. Anda akan melihat bahwa ada atribut BoroName baru yang ditambahkan ke setiap fitur jalan

LINK PROJECT : https://github.com/RaniLatifahCahyani/SIG-TEORI-Intermediate-GIS-operations/blob/main/SIG-Teori-Intermediate%20Project%202/Project2_Performing%20Spatial%20Joins%20(QGIS3).qgz

LINK HASIL LAYOUT : https://github.com/RaniLatifahCahyani/SIG-TEORI-Intermediate-GIS-operations/blob/main/SIG-Teori-Intermediate%20Project%202/layout_project2.png

# Performing Spatial Queries (QGIS3)(Project 3)
1.	Temukan file metro_stations_accessbility.zip di Peramban QGIS dan kembangkan. Pilih file metro_stations_accessbility.shp dan seret ke kanvas. Metro_stations_accessbility layer baru akan dimuat di panel Layers
2.	Lapisan data untuk bar dan pub dalam format CSV. Untuk memuatnya di QGIS, pergi ke Layer ‣ Add Layer ‣ Add Delimited Text Layer.... ( Lihat Mengimpor Spreadsheets atau file CSV (QGIS3) untuk detail lebih lanjut tentang mengimpor file CSV)
3.	Di Manajer Sumber Data | Dialog Teks yang Dibatasi, telusuri dan pilih file Bars_and_pubs__with_patron_capacity.csv yang diunduh sebagai Nama file. Kolom bidang X dan bidang Y harus dipilih secara otomatis untuk masing-masing koordinat x dan koordinat y. Klik Tambahkan.
4.	Anda akan melihat layer Bars_and_pubs__with_patron_capacity baru ditambahkan ke panel Layers. Kedua layer input berada di Geograhpic Coordinate Reference System (CRS) EPSG:4326 WGS84. Untuk melakukan analisis spasial, disarankan untuk menggunakan Projected Coordinate Reference System (CRS). Jadi sekarang kita akan memproyeksikan ulang kedua layer ke CRS regional yang sesuai yang meminimalkan distorsi dan memungkinkan kita bekerja dalam satuan jarak seperti meter, bukan derajat. Pergi ke Memproses ‣ Toolbox
5.	Cari dan temukan Vector general ‣ Alat lapisan proyeksi ulang. Klik dua kali untuk meluncurkannya.
6.	Pilih Bars_and_pubs__with_patron_capacity sebagai lapisan Input. Klik tombol Select CRS di sebelah Target CRS.
7.	Saat memilih sistem koordinat yang diproyeksikan untuk analisis Anda, tempat pertama yang harus dicari adalah CRS regional untuk area yang diminati. Untuk Australia, Map Grid of Australia (MGA) 2020 adalah sistem grid berbasis UTM yang digunakan untuk pemetaan lokal dan regional. Melbourne termasuk dalam UTM Zone 55, jadi kita bisa memilih GDA 2020 / MGA zone 55 EPSG:7855` CRS.
8.	Selanjutnya, klik tombol ... di sebelah Diproyeksikan ulang dan pilih Simpan ke GeoPackage. Geopackage adalah data spasial format data terbuka yang direkomendasikan dan merupakan format pertukaran data default untuk QGIS3. Satu file GeoPackage .gpkg dapat berisi beberapa layer vektor dan raster.
9.	Beri nama geopackage sebagai spatialquery dan klik Save.
10.	Saat diminta nama lapisan, masukkan bar_and_pubs dan klik OK. Klik Jalankan untuk memproyeksikan ulang lapisan.
11.	Jendela akan beralih ke tab Log dan Anda akan melihat algoritme berjalan dan membuat lapisan keluaran bar_and_pubs baru.




12.	Sekarang kita akan memproyeksikan ulang layer metro_stations_accessbility. Beralih kembali ke tab Parameter di jendela Reproject layer. Pilih metro_stations_accessbility sebagai lapisan Input. Pertahankan Target CRS yang sama. Selanjutnya, klik tombol ... di sebelah Diproyeksikan ulang dan pilih Simpan ke GeoPackage. Pilih file output spatialquery yang sama (Ingat bahwa satu file geopackage dapat berisi beberapa layer, jadi kami akan menyimpan layer baru ke file geopackage yang sama). Masukkan metro_stations sebagai nama Layer. Klik Jalankan
13.	Kembali ke jendela utama QGIS, Anda akan melihat 2 layer baru dimuat di panel Layers: bars_and_pubs dan metro_stations. Anda dapat mematikan visibilitas untuk lapisan asli. Sekarang, kami siap untuk melakukan kueri spasial. Karena kami tertarik untuk memilih bar dan pub dalam jarak 500m dari stasiun metro, langkah pertama adalah membuat buffer di sekitar stasiun metro yang mewakili area pencarian kami. Cari dan temukan Vector geometry ‣ Buffer tool di Processing Toolbox dan klik dua kali untuk meluncurkannya.
14.	Dalam dialog Buffer, pilih metro_stations sebagai lapisan Input. Tetapkan 500 meter sebagai Jarak. Simpan output ke geopackage spatialquery yang sama dan masukkan metro_stations_buffers sebagai nama Layer. Klik Jalankan.
15.	Anda akan melihat layer metro_stations_buffers baru dimuat di panel Layers. Sekarang kita dapat mengetahui titik mana dari layer bars_and_pubs yang termasuk dalam poligon dari layer metro_stations_buffers. Cari Vector selection ‣ Extract by Location tool dari Processing Toolbox dan klik dua kali untuk meluncurkannya
16.	Dalam dialog Ekstrak berdasarkan lokasi, pilih bar_and_pubs sebagai fitur Ekstrak dari. Centang Intersect sebagai predikat geometri. Tetapkan metro_stations_buffers sebagai Dengan membandingkan fitur dari. Simpan output ke geopackage spatialquery sebagai layer yang dipilih. Klik Jalankan.
17.	Setelah pemrosesan selesai, Anda akan melihat layer yang dipilih ditambahkan ke panel Layers. Perhatikan bahwa lapisan ini hanya berisi poin dari bars_and_pubs yang termasuk dalam poligon buffer
18.	Analisis kami selesai. Anda mungkin memperhatikan bahwa poligon penyangga terlihat berbentuk oval. Ini karena Proyek CRS kami masih disetel ke EPSG:4326 WGS84. Untuk memvisualisasikan hasil dengan lebih baik, Anda dapat pergi ke Project ‣ Properties ‣ CRS dan pilih GDA 2020 / MGA zone 55 EPSG:7855 yang kami gunakan untuk analisis. Setelah diatur ke CRS ini, buffer akan muncul dalam bentuk yang benar.

LINK PROJECT : https://github.com/RaniLatifahCahyani/SIG-TEORI-Intermediate-GIS-operations/blob/main/SIG_Teori%20Intermediate%20Project%203/Projrct%203_Performing%20Spatial%20Queries%20(QGIS3).qgz

LINK HASIL LAYOUT : https://github.com/RaniLatifahCahyani/SIG-TEORI-Intermediate-GIS-operations/blob/main/SIG_Teori%20Intermediate%20Project%203/layout_project%203.png

# Nearest Neighbor Analysis (QGIS3) (Project 4)
1.	Temukan file ne_10m_populated_places_simple.zip yang diunduh di panel Browser dan luaskan. Seret file ne_10m_populated_places_simple.shp ke kanvas.
2.	Anda akan melihat layer baru ne_10m_populated_places_simple dimuat di panel Layers. Lapisan ini berisi titik-titik yang mewakili tempat berpenduduk. Sekarang kita akan memuat lapisan gempa bumi. Lapisan ini hadir sebagai file teks Tab Serepated Values (TSV). Untuk memuat file ini, klik tombol Open Data Source Manager pada Data Source Toolbar. Anda juga dapat menggunakan pintasan keyboard Ctrl + L.
3.	Di kotak dialog Manajer Sumber Data, pilih Teks yang Dibatasi.
4.	Klik tombol ... di sebelah Nama file dan telusuri file gempa bumi-2021-11-25_13-39-30_+0530.tsv yang diunduh. Bergantung pada sistem operasi, Anda mungkin tidak melihat file di direktori yang diunduh. Jika demikian, alihkan ke Semua file (*; .) dalam dialog Pilih File Teks yang Dibatasi untuk Dibuka. Setelah dibuka, pilih Pembatas khusus di bagian Format file, dan centang Tab. Di bagian Definisi geometri, pilih Koordinat titik. Secara default nilai bidang X dan bidang Y akan diisi secara otomatis dengan bidang yang sesuai di input. Dalam kasus kami, mereka adalah Bujur dan Lintang. Anda dapat membiarkan CRS Geometri ke default EPSG:4326 - WGS 84 CRS. Jika file Anda berisi koordinat dalam CRS yang berbeda, Anda dapat memilih CRS yang sesuai di sini. Klik Tambahkan diikuti oleh Tutup.
5.	Perbesar dan jelajahi kedua set data. Setiap titik merah mewakili lokasi kejadian gempa bumi, dan setiap titik hijau mewakili lokasi tempat berpenduduk. Tujuan kita adalah menemukan titik terdekat dari lapisan tempat berpenduduk untuk setiap titik di lapisan gempa. Mari periksa tabel Atribut lapisan gempa bumi. Pilih layer dan klik ikon Open Attribute Table di Toolbar.
6.	Ada 2586 fitur, tetapi data berisi sedikit entri tanpa informasi lintang atau bujur. Kami harus menghapusnya sebelum melanjutkan lebih jauh. Tutup Tabel Atribut.
7.	Pergi ke Pemrosesan ‣ Kotak Alat ‣ Geometri vektor ‣ Hapus alat geometri nol. Klik dua kali untuk membukanya.
8.	Di kotak dialog Hapus Geometri Null, pilih gempa bumi-2021-11-25_13-39-30_+0530 sebagai lapisan Input dan centang kotak Juga hapus geometri kosong. Klik Jalankan. Setelah pemrosesan selesai, klik Tutup
9.	Sebuah layer baru Non null geometries akan ditambahkan ke panel Layers. Untuk analisis kita akan menggunakan layer ini sebagai pengganti layer aslinya. Hapus centang pada layer gempa bumi-2021-11-25_13-39-30_+0530 di panel Layers untuk menyembunyikannya. Pilih layer Non null geometries dan klik tombol Open Attribute Table dari Attributes Toolbar.
10.	Anda akan melihat jumlah fitur total yang lebih rendah karena semua baris dengan nilai lintang dan bujur kosong telah dihapus. Tutup tabel atribut




11.	Sekarang saatnya untuk melakukan analisis tetangga terdekat. Cari dan temukan Pemrosesan ‣ Toolbox ‣ Analisis vektor ‣ Jarak ke alat hub (baris ke hub) terdekat. Klik dua kali untuk meluncurkannya.
12.	Dalam kotak dialog Distance to Nearest Hub (Line to Hub), pilih Non null geometries sebagai layer Source points. Pilih ne_10m_populated_places_simple sebagai layer Destination hubs. Pilih nama sebagai atribut nama lapisan Hub. Alat ini juga akan menghitung jarak garis lurus antara tempat berpenduduk dan gempa terdekat. Tetapkan Kilometer sebagai unit Pengukuran. Klik ... di Jarak Hub dan klik Simpan ke Berkas... untuk menyimpan berkas sebagai gempa bumi_dengan_kota terdekat.gpkg . Klik Jalankan. Setelah pemrosesan selesai, klik Tutup.
13.	Kembali ke jendela utama QGIS, Anda akan melihat lapisan garis baru bernama gempa bumi_dengan_kota terdekat dimuat di panel Lapisan. Lapisan ini memiliki ciri-ciri garis yang menghubungkan setiap titik gempa dengan tempat berpenduduk terdekat. Pilih layer gempa bumi_dengan_terdekat_kota dan klik ikon Buka Tabel Atribut di Bilah Alat.
14.	Gulir ke kanan ke kolom terakhir, dan Anda akan melihat 2 atribut baru bernama HubName dan HubDist ditambahkan ke fitur gempa asli. Ini adalah nama jarak ke tetangga terdekat dari layer tempat berpenduduk.

LINK PROJECT : https://github.com/RaniLatifahCahyani/SIG-TEORI-Intermediate-GIS-operations/blob/main/SIG-Teori-Intermediate%20Project%204/Project%204_Nearest%20Neighbor%20Analysis%20(QGIS3).qgz

LINK HASIL LAYOUT : https://github.com/RaniLatifahCahyani/SIG-TEORI-Intermediate-GIS-operations/blob/main/SIG-Teori-Intermediate%20Project%204/Layout%20Project_4.jpeg

# Sampling Raster Data using Points or Polygons (QGIS3) (Project 5)
1.	Buka zip dan ekstrak 2018_Gaz_ua_national.zip dan tl_2018_us_county.zip ke folder di komputer Anda. Buka QGIS dan temukan file us.tmax_nohads_ll_20190501_float.tif di Browser QGIS, seret ke kanvas
2.	Anda akan melihat layer raster baru us.tmax_nohads_ll_20190501_float dimuat di panel Layers. Lapisan raster ini berisi suhu maksimum yang tercatat pada setiap piksel dalam derajat Celcius. Selanjutnya kita akan memuat file titik area perkotaan. File ini hadir sebagai file teks dalam format Tab Separated Values (TSV). Klik tombol Buka Pengelola Sumber Data di Bilah Alat Sumber Data
3.	Beralih ke tab Teks Dibatasi. Klik tombol ... di sebelah Nama file dan tentukan jalur ke file teks yang Anda unduh. Di bagian File format, pilih Custom delimiters dan centang Tab. Pilih INTPTLONG sebagai bidang X dan INTPTLAT sebagai bidang Y. Klik Tambah lalu Tutup
4.	Lapisan titik baru 2018_Gaz_ua_national akan dimuat di panel Lapisan. Sekarang kita siap untuk mengekstrak nilai dari lapisan raster pada titik-titik ini. Pergi ke Memproses ‣ Toolbox.
5.	Cari dan temukan analisis Raster ‣ Contoh algoritme nilai raster. Klik dua kali untuk meluncurkannya.
6.	Pilih 2018_Gaz_ua_national sebagai Lapisan Titik Input. Pilih us.tmax_nohads_ll_20190501_float sebagai Lapisan Raster untuk dijadikan sampel. Luaskan parameter Lanjutan dan masukkan tmax sebagai awalan kolom Keluaran. Klik Jalankan. Setelah pemrosesan selesai, klik Tutup.
7.	Layer baru Sampled Points akan dimuat di panel Layers. Pilih alat Identifikasi di Bilah Alat Atribut dan klik titik mana saja. Anda akan melihat atribut ditampilkan di panel Identifikasi Hasil. Anda akan melihat atribut baru bernama tmax_1 ditambahkan ke setiap fitur. Ini adalah nilai piksel dari lapisan raster yang diekstraksi di lokasi titik. Angka 1 mewakili nomor pita raster. Jika lapisan raster memiliki banyak pita, Anda akan melihat banyak kolom baru di lapisan keluaran.
8.	Bagian pertama dari analisis kami selesai. Mari kita hapus lapisan yang tidak perlu. Tahan tombol Shift dan pilih Sampled Points dan layer 2018_Gaz_ua_national. Klik kanan dan pilih Hapus untuk menghapusnya dari QGIS. Saat diminta untuk Hapus 2 entri legenda?, pilih OK.
9.	Sekarang kita akan menggunakan lapisan kabupaten untuk mengambil sampel raster dan menghitung suhu rata-rata untuk setiap kabupaten. Temukan file tl_2018_us_county.shp di Browser QGIS, seret ke kanvas
10.	Lapisan baru tl_2018_us_county akan dimuat ke panel Lapisan. Pergi ke Memproses ‣ Toolbox.
11.	Cari dan temukan analisis Raster ‣ Algoritme statistik zona dan klik dua kali untuk meluncurkannya.


12.	Pilih us.tmax_nohads_ll_20190501_float sebagai layer Raster dan tl_2018_us_county sebagai layer Vector yang berisi zona. Masukkan tmax_ sebagai awalan kolom Keluaran. Klik ... di sebelah Statistik untuk menghitung
13.	Pilih hanya nilai Mean dan klik OK.
14.	Klik Jalankan untuk memulai pemrosesan. Algoritme mungkin membutuhkan waktu beberapa menit untuk selesai. Klik Tutup
15.	Seperti disebutkan sebelumnya, algoritma Zonal Statistics tidak membuat layer baru, tetapi memodifikasi layer zona. Klik kanan layer tl_2018_us_county, dan pilih Open Attribute Table.
16.	Anda akan melihat kolom baru bernama tmax_mean ditambahkan ke tabel atribut. Ini berisi nilai suhu rata-rata yang diekstraksi di atas poligon untuk setiap fitur. Ada beberapa nilai nol karena kabupaten tersebut (milik Alaska, Hawaii, dan Puerto Riko) berada di luar jangkauan lapisan raster
 
LINK PROJECT : https://github.com/RaniLatifahCahyani/SIG-TEORI-Intermediate-GIS-operations/blob/main/SIG-Teori%20Intermediate%20Project%205/Project%205_Sampling%20Raster%20Data%20using%20Points%20or%20Polygons%20(QGIS3).qgz

LINK HASIL LAYOUT : https://github.com/RaniLatifahCahyani/SIG-TEORI-Intermediate-GIS-operations/blob/main/SIG-Teori%20Intermediate%20Project%205/layout%20project%205.png

# Calculating Raster Area (QGIS3) (Project 6)
1.	Buka zip semua file yang diunduh. Di Browser, cari folder yang berisi file batas WDPA_WDOECM_Apr2022_Publicc_10744_shp-polygons.shp dan drag-and-drop ke kanvas QGIS.
2.	Sekarang cari petak raster penutup dunia ESA_WorldCover_10m_2020_v100_N24_E093_Map.tif dan letakkan di kanvas QGIS.
3.	Anda sekarang akan memiliki layer vektor batas dan raster tutupan lahan dimuat di panel Layers. Mari potong raster tutupan lahan ke batas taman nasional. Pergi ke Processing ‣ Toolbox untuk membuka Processing toolbox. Cari dan temukan GDAL ‣ Ekstraksi raster ‣ Klip raster dengan algoritma lapisan topeng. Klik dua kali untuk meluncurkannya.
4.	Dalam dialog Clip Raster by Mask Layer, pilih layer ESA_WorldCover_10m_2020_v100_N24_E093_Map sebagai layer Input dan layer WDPA_WDOECM_Apr2022_Publicc_10744_shp-polygons sebagai Layer Mask. Masukkan -9999 di Tetapkan nilai nodata yang ditentukan ke bagian pita keluaran
5.	Sekarang buka bagian Advanced Parameters dan pilih High Compression in Profile. Sekarang di bawah Clipped (mask), klik pada ... dan pilih Save To File.... Masukkan nama file sebagai worldcover_cliped.tif. Klik Jalankan.
6.	Sekarang lapisan worldcover_cliped akan dimuat di kanvas QGIS. Klik kanan layer ESA_WorldCover_10m_2020_v100_N24_E093_Map dan pilih Remove Layer...
7.	Kedua layer kami hadir dalam Geographic CRS EPSG:4326. CRS ini memiliki satuan derajat dan tidak cocok untuk menghitung luas. Pertama-tama kita harus memproyeksikan ulang layer ke Projected CRS. untuk analisis regional seperti ini, UTM adalah pilihan yang baik untuk proyeksi CRS. Kami akan memproyeksikan ulang layer ke CRS untuk zona UTM lokal. Buka kotak alat Pemrosesan dan cari Vector general ‣ Algoritma lapisan proyeksi ulang. Klik dua kali untuk meluncurkannya.
8.	Dalam dialog Reproject Layer, pilih layer WDPA_WDOECM_Apr2022_Publicc_10744_shp-polygons sebagai layer Input, klik tombol Select CRS di bawah Target CRS.
9.	Area minat kami termasuk dalam Zona UTM 46N. Cari 46 N dan pilih zona WGS 84 / UTM 46N CRS.
10.	Pada bagian Reprojected, klik ... dan pilih Save To File.... Masukkan nama sebagai nationalpark_reprojected.gpkg. Klik Jalankan
11.	Sekarang layer nationalpark_reprojected akan dimuat di kanvas. Klik kanan layer WDPA_WDOECM_Apr2022_Publicc_10744_shp-polygons dan pilih Remove Layer... untuk menghapusnya. Sekarang kita akan memproyeksikan ulang layer raster. Di Kotak Alat Pemrosesan, cari dan temukan GDAL ‣ Proyeksi raster ‣ Warp (proyeksi ulang)
12.	Dalam dialog Warp (Reproject) pilih worldcover_cliped sebagai Input layer, pilih WGS 84 / UTM zone 46N CRS di Target CRS. Buka Parameter Lanjutan dan pilih Kompresi Tinggi di Profil.
13.	Sekarang di bawah Reprojected, klik ... dan pilih Save To File.... Masukkan nama sebagai worldcover_reprojected.tif. Klik Jalankan.
14.	Sekarang lapisan worldcover_reprojected akan dimuat di kanvas, hapus lapisan worldcover_cliped. Mari atur layer proyek ke zona UTM. Klik pada layer mana saja dan pilih Layer CRS ‣ Set Project CRS from Layer.
15.	Sekarang proyek CRS akan diperbarui. Mari atur simbologi lapisan raster sesuai nama kelas dan warna kumpulan data ESA WorldCover. Klik kanan pada layer worldcover_reprojected dan klik Properties...
16.	Dalam dialog Layer Properties, pilih Symbology. Anda dapat melihat warna Layer divisualisasikan dalam nada putih-hitam. Untuk memperbaikinya, klik Style ‣ Load Style.... Telusuri dan pilih file ESAWorldCover_ColorLegend.qml.
17.	Sekarang Anda dapat melihat warna simbol yang diperbarui dan deskripsi kelas. Klik Oke
18.	Perluas layer worldcover_reprojected di panel Layers untuk melihat legenda dengan deskripsi kelas yang benar
19.	Sekarang mari kita hitung luas untuk setiap kelas. Di kotak alat pemrosesan, cari dan temukan alat laporan nilai unik lapisan Raster. Klik dua kali untuk membukanya.
20.	Dalam dialog Raster Layer Unique Values Report, pilih layer Input sebagai worldcover_reprojected. Di bawah tabel Unique values klik ... dan pilih Save to File.... Masukkan nama sebagai class_areas.gpkg. Klik Jalankan
21.	Sekarang layer class_areas akan ditambahkan ke panel Layers. Klik kanan pada layer dan klik Open Attribute Table. Kolom m2 memuat luas untuk setiap kelas dalam meter persegi.
22.	Mari ubah luas menjadi kilometer persegi. Di Processing Toolbox, cari dan pilih tabel Vektor ‣ Kalkulator Bidang
23.	Dalam dialog Field Calculator, pilih layer class_areas di Layer Input. Masukkan nama Bidang sebagai area_sqkm. Di bidang Hasil, pilih Float. Di jendela Ekspresi, masukkan ekspresi di bawah ini. Ini akan mengubah sqmt menjadi sqkm dan membulatkan hasilnya menjadi 2 tempat desimal. Di bawah Terhitung klik pada ... dan pilih Simpan Ke File... . Masukkan nama sebagai class_area_sqkm.gpkg. Klik Jalankan
24.	Sekarang lapisan class_area_sqkm akan dimuat di kanvas. Buka tabel Atribut dan periksa kolom area_sqkm yang baru ditambahkan. Anda akan melihat bahwa kolom Nilai berisi angka untuk setiap kelas. Agar hasilnya lebih mudah diinterpretasikan, Mari tambahkan juga deskripsi untuk setiap nomor kelas. Deskripsi kelas tersedia di Panduan Pengguna Produk ESA




25.	Buka Field Calculator, dan pilih layer class_areas_sqkm di Input Layer. Masukkan Nama bidang sebagai tutupan lahan, pada jenis bidang Hasil, pilih String. Di jendela Expression masukkan ekspresi di bawah ini. Ekspresi ini menggunakan pernyataan CASE untuk menetapkan nilai berdasarkan beberapa kondisi. Di bawah Terhitung klik pada ... dan pilih Simpan Ke File... . Masukkan nama sebagai class_area_with_landcover.gpkg. Klik Jalankan.
26.	Sekarang lapisan class_area_with_landcover akan dimuat di kanvas. Buka tabel Atribut. Kolom tutupan lahan akan berisi nama tutupan lahan terhadap setiap nilai tutupan lahan
27.	Mari ekspor hasil ini sebagai file excel. Sebelum mengekspor, kami juga akan mengatur tabel dan menghapus kolom yang tidak diinginkan. Di Processing Toolbox, cari dan pilih Vector table ‣ Refactor field
28.	Dalam dialog Refactor Fields, pilih layer class_area_with_landcover di Layer Input. Pilih semua kolom kecuali area_sqkm dan tutupan lahan, lalu klik Hapus kolom yang dipilih.
29.	Anda juga dapat mengubah urutan bidang dalam tabel menggunakan tombol Pindahkan Bidang yang Dipilih. Setelah Anda selesai mengedit, klik tombol ... di sebelah Refactored dan pilih Save To File.... Pilih File XLSX (*.xlsx) sebagai formatnya. Masukkan nama file sebagai park_area_by_landcover.xlsx dan klik Save. Dalam dialog Bidang Refaktor, klik Jalankan untuk menerapkan perubahan Anda.
30.	Hasilnya akan menjadi spreadsheet dengan tutupan lahan dan kolom luas km persegi.

LINK PROJECT : https://github.com/RaniLatifahCahyani/SIG-TEORI-Intermediate-GIS-operations/blob/main/SIG-Teori%20Intermediate%20Project%206/Project%206_Calculating%20Raster%20Area%20(QGIS3).qgz

LINK HASIL LAYOUT : https://github.com/RaniLatifahCahyani/SIG-TEORI-Intermediate-GIS-operations/blob/main/SIG-Teori%20Intermediate%20Project%206/layout%20project%206.png

# Creating Heatmaps (QGIS3) (Project 7)
1.	We will first load a basemap layer from OpenStreetMap and then import the CSV data. In the Browser tab, scroll down and locate the XYZ Tiles section.
2.	Bentangkan untuk melihat layer petak OpenStreetMap. Seret dan lepas ke kanvas utama. Selanjutnya kita akan memuat file CSV. Klik tombol Buka Pengelola Sumber Data.
3.	Beralih ke tab Teks Dibatasi. Di sini kita akan mengimpor data kejahatan yang datang dalam file teks format CSV. Klik tombol ... di sebelah Nama file dan telusuri file 2019-02-surrey-street.csv yang diunduh. Bidang X dan bidang Y di bagian Definisi Geometri akan diisi secara otomatis dengan kolom Bujur dan Lintang. CRS Geometri harus dibiarkan ke standar EPSG:4326 - definisi WGS 84. Pastikan data terlihat benar di panel Data sampel dan klik Tambah, diikuti dengan Tutup
4.	Anda akan melihat 2 lapisan - OpenStreetMap dan 2019-02-surrey-street dimuat di panel Lapisan QGIS. Klik kanan layer 2019-02-surrey-street dan pilih Zoom to Layer
5.	Anda akan melihat layer poin insiden kejahatan dihamparkan pada peta dasar OpenStreetMap. Zoom dan Pan untuk menjelajahi data. Datanya cukup padat dan sulit untuk mengetahui di mana terdapat konsentrasi kejahatan yang tinggi. Di sinilah visualisasi peta panas akan berguna. Pilih layer 2019-02-surrey-street dan klik tombol panel Open the Layer Styling
6.	Pilih Heatmap sebagai perender di menu dropbox. Panel Layer Styling bersifat interaktif dan Anda dapat segera melihat efek perubahan Anda tercermin di kanvas. Lapisan sekarang akan ditampilkan di jalan warna skala abu-abu default.
7.	Peta panas biasanya dirender menggunakan jalur warna kuning-ke-merah atau putih-ke-merah di mana konsentrasi titik yang lebih tinggi menghasilkan lebih banyak panas. Klik menu dropdown Color ramp dan pilih Reds color-ramp.
8.	Selanjutnya Anda harus memilih Radius. Parameter ini menentukan lingkungan melingkar di sekitar setiap titik di mana titik tersebut akan memiliki pengaruh. Nilai ini akan sangat bergantung pada jenis data masukan Anda. Untuk data kami, anggap saja insiden kejahatan akan berdampak hingga 5 Kilometer dari lokasi. Perhatikan bahwa CRS proyek saat ini diatur ke EPSG: 3857 di sudut kanan bawah. CRS ini memiliki satuan meter, jadi kita harus menentukan 5000 meter sebagai radiusnya. Parameter lain yang disembunyikan dari menu ini adalah bentuk Kernel. Ini adalah fungsi yang menentukan bagaimana pengaruh suatu titik harus tersebar pada radius yang diberikan. Perender Heatmap menggunakan fungsi Quartic untuk perhitungan ini. Ada jenis kernel lain seperti Triangular, Uniform, Triweight, dan Epanechnikov yang dapat ditentukan saat menggunakan metode pembuatan peta panas berbeda yang dijelaskan nanti di tutorial ini. Lihat posting ini untuk penjelasan dan panduan yang bagus untuk memilih radius dan bentuk kernel yang tepat.
9.	Visualisasi peta panas sudah siap. Kita bisa mengatur Opacity dari heatmap di bagian Layer Rendering di bagian bawah. Atur opacity menjadi 60% agar Anda dapat melihat peta dasar beserta peta panasnya.
10.	Untuk banyak jenis analisis, hanya mempertimbangkan kerapatan poin sudah cukup baik. Namun terkadang, Anda mungkin ingin memberikan kepentingan yang berbeda untuk setiap poin. Kejahatan yang lebih kejam seharusnya memiliki pengaruh lebih besar pada peta panas keluaran daripada perampokan. Demikian pula, kadang-kadang suatu titik dapat mewakili beberapa pengamatan di satu lokasi yang perlu diperhitungkan dalam analisis. Untuk melakukannya, Anda dapat menyediakan kolom bobot numerik opsional yang menentukan nilai untuk setiap poin. Mari tambahkan bidang bobot dan gunakan untuk menyempurnakan peta panas. Klik kanan layer 2019-02-surrey-street dan pilih Open Attribute Table.




11.	Anda akan melihat bidang teks bernama Jenis kejahatan di data input yang menjelaskan jenis kejahatan. Kita dapat menggunakan ini untuk mengkategorikan berbagai jenis kejahatan dan menetapkan bobot yang lebih tinggi untuk kejahatan yang lebih kejam.
12.	Klik Kalkulator lapangan terbuka
13.	Kami sekarang akan memasukkan rumus yang menggunakan jenis Kejahatan dan menentukan nilai bobotnya. QGIS memiliki cara praktis untuk menambahkan bidang yang dihitung menggunakan Bidang Virtual. Bidang virtual disimpan dalam proyek QGIS dan tidak mengubah data sumber. Ini juga dihitung secara dinamis dan dapat digunakan di mana saja di QGIS seperti halnya nilai atribut lainnya. Masukkan bobot sebagai nama bidang Keluaran dan atur jenis bidang Keluaran ke Bilangan bulat (bilangan bulat). Masukkan ekspresi berikut di Editor ekspresi. Di sini kita menggunakan pernyataan CASE untuk menetapkan nilai yang berbeda berdasarkan kondisi yang berbeda. Klik Oke.
14.	Atribut baru akan ditambahkan untuk setiap fitur dengan nilai bobot yang sesuai
15.	Kembali ke panel Layer Styling, klik menu drop-down untuk Weight points by dan pilih bidang bobot yang baru ditambahkan
16.	Anda akan melihat perubahan rendering peta panas untuk memperhitungkan parameter bobot. Tutup panel Layer Styling
17.	Jika Anda memerlukan visualisasi peta panas untuk disimpan sebagai lapisan raster permanen atau ingin menyesuaikan peta panas dengan opsi lanjutan seperti kernel yang berbeda atau radius dinamis, Anda dapat menggunakan Peta Panas (Estimasi Kepadatan Kernel) dari Kotak Alat Pemrosesan. Kami sekarang akan menggunakan algoritma ini. Pergi ke Memproses ‣ Toolbox
18.	Sebelum kita dapat membuat peta panas, kita perlu memproyeksikan ulang data sumber ke CRS yang diproyeksikan. Karena jarak memainkan peran penting dalam perhitungan peta panas, tidak benar menggunakan CRS geografis. Cari dan temukan algoritma Vector general ‣ Proyeksi ulang layer.
19.	Pada dialog Reproject layer, klik tombol Select CRS untuk Target CRS. Cari dan pilih EPSG:27700 OSGB 1936 / British National Grid CRS. CRS yang diproyeksikan ini adalah pilihan yang baik untuk data di Inggris. Klik Jalankan.
20.	Sebuah layer baru bernama Reprojected akan ditambahkan ke panel Layers. Hapus centang pada kotak di sebelah layer lama 2019-02-surrey-street untuk menyembunyikannya
21.	Cari dan temukan algoritma Interpolation ‣ Heatmap (Kernel Density Estimation).
22.	Pada dialog Heatmap (Kernel Density Estimation), kita akan menggunakan parameter yang sama seperti sebelumnya. Pilih Radius sebagai 5000 meter dan Weight from field sebagai weight. Atur ukuran Pixel X dan ukuran Pixel Y menjadi 50 meter. Biarkan Kernel membentuk nilai default Quartic. Klik Jalankan
23.	Setelah pemrosesan selesai, lapisan raster baru bernama OUTPUT akan dimuat. Visualisasi default jelek karena menggunakan penyaji abu-abu Singleband. Klik tombol panel Open the Layer Styling
24.	Ubah render menjadi Singleband Pseudocolor dan pilih jalur warna Merah. Lapisan sekarang terlihat seperti visualisasi peta panas yang telah kita buat sebelumnya.

LINK PROJECT : https://github.com/RaniLatifahCahyani/SIG-TEORI-Intermediate-GIS-operations/blob/main/SIG-Teori-Intermediate%20Project%207/Project%207_%20(Creating%20Heatmaps%20(QGIS3).qgz

LINK LAYOUT : https://github.com/RaniLatifahCahyani/SIG-TEORI-Intermediate-GIS-operations/blob/main/SIG-Teori-Intermediate%20Project%207/layout%20project%207.jpeg

# Animating Time Series Data (QGIS3) (Project 8)
1.	Di Panel Peramban QGIS, temukan direktori tempat Anda menyimpan data unduhan. Luaskan ne_10m_land.zip dan pilih layer ne_10m_land.shp. Seret layer ke kanvas. Selanjutnya, cari file ASAM_shp.zip. Luaskan dan pilih layer asam_data_download/ASAM_events.shp dan seret ke kanvas
2.	Setelah lapisan dimuat, Anda dapat melihat masing-masing titik yang mewakili insiden lokasi pembajakan. Ada ribuan insiden dan sulit ditentukan dengan lebih banyak pembajakan. Daripada poin individual, cara yang lebih baik untuk memvisualisasikan data ini adalah melalui peta panas. Pilih layer ASAM_events dan klik tombol Open the layer Styling Panel di panel Layers. Klik tarik-turun Simbol tunggal
3.	Di drop-down pemilihan perender, pilih Perender peta panas. Selanjutnya, pilih jalur warna Viridis dari pemilih Jalur warna.
4.	Sesuaikan nilai Radius ke 5.0. Di bagian bawah, luaskan bagian Layer Rendering dan sesuaikan Opacity menjadi 75,0%. Ini memberikan efek visual yang bagus dari hotspot dengan lapisan tanah di bawahnya
5.	Sekarang mari kita animasikan data ini untuk menunjukkan peta insiden pembajakan tahunan. Klik kanan pada layer ASAM_event, dan pilih Properties.
6.	Di kotak dialog Properti lapisan, pilih tab Temporal dan aktifkan dengan mengklik kotak centang.
7.	Data sumber berisi atribut dateofocc - mewakili tanggal terjadinya insiden. Ini adalah bidang yang akan digunakan untuk menentukan poin yang diberikan untuk setiap periode waktu. Pilih Bidang Tunggal dengan Data/Waktu di menu Tarik-turun Konfigurasi, dateofocc sebagai Bidang
8.	Sekarang simbol jam akan muncul di sebelah nama layer. Klik pada Panel Kontrol Temporal (ikon Jam) dari Bilah Alat Navigasi Peta
9.	Klik pada Animated Temporal Navigation (ikon putar) untuk mengaktifkan kontrol animasi. Klik Atur ke Rentang Penuh (ikon segarkan) di sebelah Rentang untuk secara otomatis mengatur rentang waktu agar cocok dengan kumpulan data
10.	Sekarang Anda siap untuk melihat animasi. Tetapkan Langkah sebagai 1 Tahun lalu klik tombol Putar untuk memulai animasi.
11.	Akan sangat membantu juga untuk menampilkan label yang menunjukkan kerangka waktu saat ini di peta. Kita dapat melakukannya dengan menggunakan dekorasi Judul bawaan. Pergi ke Lihat ‣ Dekorasi ‣ Label Judul
12.	Klik kotak centang untuk mengaktifkannya dan klik tombol Sisipkan Ekspresi dan masukkan ekspresi berikut untuk menampilkan tahun. Di sini variabel @map_start_time berisi stempel waktu potongan waktu saat ini yang ditampilkan. Jadi kita bisa menggunakan stempel waktu itu dan memformatnya untuk menampilkan tahun kejadian. Lihat Dokumentasi QGIS untuk detail tentang berbagai opsi pemformatan yang didukung untuk stempel waktu.
13.	Pilih ukuran font sebagai 25, atur warna bilah latar belakang sebagai Putih dan atur transparansi menjadi 50%. Di Penempatan pilih Kanan Bawah. Sekarang klik Oke.
14.	Setelah parameter diatur sesuai, tahun akan ditampilkan seperti yang ditunjukkan. Untuk mengekspor ini sebagai gambar dan mengonversinya sebagai GIF pilih Ekspor Animasi (simpan ikon) di jendela kontrol Temporal.
15.	Klik pada ... Direktori keluaran untuk memilih direktori tempat gambar akan disimpan.
16.	Di bawah Extent pilih Hitung dari Layer ‣ ne_10_land layer. Klik Simpan
17.	Setelah ekspor selesai, Anda akan melihat gambar PNG untuk setiap tahun (total 18 gambar) di direktori keluaran.
18.	Sekarang mari buat GIF animasi dari gambar-gambar ini. Ada banyak opsi untuk membuat animasi dari masing-masing bingkai gambar. Saya suka ezgif untuk alat yang mudah dan online. Kunjungi situs dan klik Pilih File dan pilih semua file .png. Setelah dipilih, klik Unggah dan buat GIF! tombol. Setelah dibuat, Anda dapat mengunduh GIF menggunakan tombol Simpan.

LINK : https://github.com/RaniLatifahCahyani/SIG-TEORI-Intermediate-GIS-operations/tree/main/SIG-Teori%20Intermediate%20Project%208

# Handling Invalid Geometries (QGIS3) (Project 9)
1.	Telusuri file India-States.zip yang diunduh di Peramban QGIS. Perluas dan seret file India-States.shp ke kanvas peta.
2.	Anda akan melihat layer India-States baru dimuat di panel Layers. Pergi ke Memproses ‣ Toolbox
3.	Kami akan mencoba menjalankan algoritme pemrosesan pada lapisan input untuk mendemonstrasikan bagaimana geometri yang tidak valid dapat menyebabkan masalah selama operasi geoproses. Cari dan temukan Kartografi ‣ Algoritma pewarnaan topologi. Klik dua kali untuk meluncurkannya.
4.	Dalam dialog pewarnaan Topologi, pilih India-States sebagai lapisan Input. Simpan semua parameter lain ke default dan klik Jalankan.
5.	Saat algoritme berjalan, Anda akan melihat peringatan ditampilkan di tab Log. 1 fitur di lapisan input memiliki geometri yang tidak valid dan dilewati selama pemrosesan. Pengaturan default untuk menangani geometri yang tidak valid di Kotak Alat Pemrosesan terletak di Pengaturan ‣ Opsi ‣ Pemrosesan ‣ Umum ‣ Pemfilteran fitur yang tidak valid dan diatur ke Lewati (abaikan) fitur dengan geometri yang tidak valid. Ini adalah pengaturan default yang bagus, tetapi jika masukan Anda besar, Anda mungkin melewatkan peringatan ini dan mungkin tidak mengetahui bahwa fitur masukan telah dilewati. Anda mungkin ingin mengubah nilainya menjadi Hentikan eksekusi algoritme saat geometri tidak valid.
6.	Kembali ke jendela utama QGIS, Anda akan melihat layer baru Berwarna ditambahkan ke panel Layers. Perhatikan bahwa layer baru tidak memiliki status yang geometrinya tidak valid. Kami sekarang tahu bahwa poligon keadaan tertentu ini memiliki geometri yang tidak valid tetapi kami tidak tahu apa penyebabnya. Kita dapat dengan mudah mengetahuinya. Cari dan temukan geometri Vektor ‣ Periksa algoritme validitas
7.	Dalam dialog Check Validity, pilih India-States sebagai Input layer. Pilih GEOS sebagai Metode. Klik Jalankan
8.	Saat algoritme selesai diproses, Anda akan melihat 3 lapisan baru di panel Lapisan - Keluaran valid, Keluaran tidak valid, dan Keluaran kesalahan. Keluaran Error lapisan berisi lokasi dan deskripsi kesalahan geometri. Klik kanan dan pilih Buka Tabel Atribut.
9.	Anda akan melihat bahwa pesan kesalahannya adalah Ring self-intersection. Pilih baris dan klik tombol Zoom map to selected features. Saat memperbesar, Anda akan melihat akar penyebab galat geometri.
10.	QGIS hadir dengan algoritme bawaan untuk memperbaiki kesalahan geometri secara otomatis. Cari dan temukan geometri Vektor ‣ Perbaiki algoritma geometri. Klik dua kali untuk menjalankannya
11.	Dalam dialog Fix Geometries, pilih India-States sebagai Input layer dan klik Run.

12.	Sebuah layer baru Fixed Geometries akan ditambahkan ke panel Layers. Pada titik ini, kesalahan geometri telah diperbaiki dan Anda dapat menjalankan algoritme pemrosesan apa pun pada lapisan ini tanpa masalah. Tetapi kita dapat melihat bahwa masih ada celah antara poligon yang berdekatan yang tidak terduga dan dapat menyebabkan kesalahan topologi di kemudian hari. Kami juga dapat memperbaikinya dengan mengedit poligon. Klik tombol Toggle Editing di Digitizing Toolbar. Pilih Vertex Tool dan dari drop-down pilih Vertex Tool (Current Layer)

13.	Saat alat vertex aktif, klik pada vertex untuk memilihnya. Anda dapat menekan tombol Delete untuk menghapus simpul atau menyeretnya untuk memindahkannya. Anda dapat memindahkan simpul sehingga tepi poligon sekarang menyentuh poligon yang berdekatan.

14.	Setelah selesai, klik tombol Toggle Editing lagi dan klik Save

15.	Mari jalankan lagi algoritma Kartografi ‣ Pewarnaan topologi.

16.	Dalam dialog Topological Coloring, pastikan Anda memilih Fixed Geometries sebagai Input layer. Klik Jalankan

17.	Anda akan melihat algoritme berjalan tanpa kesalahan dan lapisan baru Berwarna akan ditambahkan ke panel Lapisan. Perhatikan bahwa algoritme tidak mewarnai layer dengan sendirinya, tetapi bekerja dengan menambahkan kolom baru bernama color_id ke setiap poligon yang dapat digunakan untuk menetapkan warna unik yang berbeda dari poligon yang berdekatan. Pilih layer Colored dan klik tombol Open the Layer Styling Panel.

18.	Pilih Penyaji yang dikategorikan dan kolom color_id sebagai Nilai. Klik Klasifikasikan. Anda sekarang akan melihat peta berwarna sehingga poligon yang berdekatan memiliki warna yang berbeda

LINK PROJECT : https://github.com/RaniLatifahCahyani/SIG-TEORI-Intermediate-GIS-operations/blob/main/SIG-Teori%20Intermediate%20Project%209/Project%209_Handling%20Invalid%20Geometries%20(QGIS3).qgz

LINK HASIL LAYOUT : https://github.com/RaniLatifahCahyani/SIG-TEORI-Intermediate-GIS-operations/blob/main/SIG-Teori%20Intermediate%20Project%209/layout%20project%209.jpeg



