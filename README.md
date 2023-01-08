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


