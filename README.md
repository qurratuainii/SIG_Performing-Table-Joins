# SIG_Performing-Table-Joins

*Tutorial Performing Table Joins

1. Download terlebih dahulu file tl_2019_06_tract.zip dan ACST5Y2019_S0101.zip 

2. Temukan file tl_2019_06_tract.zip pada browser dan pili file tl_2019_06_tract.shp dan seret ke kanvas (*Gambar 1*)

3. Pilih Select Transformation akan meminta untuk mengkonversi dari EPSG:4269 ke EPSG:4326. Jendela ini menyajikan beberapa transformasi untuk mengkonversi antara koordinat antara proyeksi tersebut. Lalu pilihan default dan klik OK (*Gambar 2*)

4. Kita akan melihat layer tl_2019_06_tract dimuat di layer panel. Lapisan ini berisi batas-batas bidang sensus di California. Klik kanan pada layer tl_2019_06_tract dan pilih Open Attribute Table (*Gambar 3*)

5. Periksa atribut layer. Untuk menggabungkan tabel dengan lapisan ini, kita memerlukan atribut unik dan umum dari setiap fitur. Dalam hal ini, ada 9057 rekaman traktat individual dengan bidang GEOID. Kolom ini dapat menautkan lapisan dengan lapisan atau tabel lain yang berisi ID yang sama (*Gambar 4*)

6. Untuk memuat data tabular, klik Open Data Source Manager (*Gambar 5*)

7. Pada Data Source Manager, pilih Delimited Text. Kemudian di sebelah kanan, klik ... di sebelah File name dan browse ke folder yang tidak di zip dengan California population CSV (*Gambar 6*)

8. Sekarang di bawah Sample data, kita dapat memeriksa data bahkan sebelum memuatnya sebagai apisan, Representation menunjukkan bahwa tabel data berisi 2 baris header (*Gambar 7*)

9. Untuk menghilangkan baris tajuk tambahan, di bawah Record dan Fields Option atur jumlah baris tajuk ke 1. Sekarang tabel akan berisi tajuk kolom yang tepat. Karena lapisan ini hanya berisi data tabular, pilih No geometry(attribute only table). Klik Add untuk menambahkannya sebagai layer dan kemudian klik Close untuk menutup kotak dialog ini (*Gambar 8*)

10. CSV sekarang akan diimpor sebagai tabel ke QGIS dan muncul sebagai ACST5Y2019.S0101 di layer panel. Sekarang klik kanan pada layer dan pilih Open Attribute Table (*Gambar 9*)

11. Kolom ID berisi id unik untuk setiap record, yang dapat digunakan untuk menggabungkan tabel ini dengan leyer tl_2019_06_tract. Jika kita membandingkan nilai ID dengan kolom GEOID dari tl_2019_06_tract. Kita akan melihat bahwa itu diawali dengan 1400000US. Untuk menggabungkan kedua tabel ini dengan sukses, nilainya harus sama persis. Hapus terlebih dahulu awalan ini dan tambahkan kolom baru dengan 11 karakter terakhir yang berisi nilai yang sama persisi (*Gambar 10*)

12. Untuk membuat kolom baru dengan 11 digit terakhir, buka Processing Toolbox dan cari Vector table lalu pilih Field calculator (*Gambar 11*)

13. Pada dialog Field calculator, pilih ACST5Y2019.S0101  sebagai input layer, masukkan geoid di Field name, dan pilih string untuk Result Field type. Sekarang cari substr dalam ekspresi. Kita dapat menggunakan fungsi ini untuk mengestrak bagian yang diperlukan dari kolom id (*Gambar 12*)

14. Masukkan ekspresi berikut ini substr("id", -11). Kita menggunakan fungsi substr dan mengestrak nilai dari posisi -11 (nilai negatif dihitung dari akhir). Hasil akhir dapat dilihat di bagian Previed. Klik Run (*Gambar 13*)

15. Sekarang lapisan baru Calclated akan dimuat di kanvas, kita periksa tabel atribut. Geoid kolom baru dengan nilai yang dapat disesuaikan dengan saluran sensus (*Gambar 14*)

16. Untuk membuat gabungan tabel, buka Peocessing Toolbox dan cari Vector general dan plih Join attributes by field value (*Gambar 15*)

17. Pada Join attribute by field value, pilih tl_2019_06_tract sebagai input layer dan GEOID sebagai Table field. Pilih Calculated sebagai input layer 2 dan geoid sebagai table field 2. Di bawah kolom Layer2 untuk menyalin klik ... (*Gambar 16*)

18. Periksa Geographic Area Name, Estimate!!Total!!Total population , dan geoid. Lalu klik OK (*Gambar 17*)

19. Pilih Discrad records yang tidak dapat digabungkan. Ini akan menghilangkan catatan tambahan apa pun di tabel populasi. Klik tombol ... di bawah layer gabungan untuk memilih Save to File (*Gambar 18*)

20. Beri nama output geopackage dengan california_total_population.gpkg. Lalu klik Run (*Gambar 19*)

21. Setelah pemrosesan selesai, verifikasi bahwa algoritme berhasil jika semua fitur 8057 digabungkan. Klik close (*Gambar 20*)

22. Kita akan melihat layer baru california_total_population dimuat di panel LAyers. Pada titik ini, bidang dari file CSV digabungkan dengan lapisan saluran sensus. Sekatang setelah kita memiliki data kependudukan di lapisan sensus, kita dapat menatanya untuk membuat visualisasi distribusi kepadatan penduduk. Klik tombol Open the Later Styling (*Gambar 21*)

23. Pada Layer Styling panel, pilih Graduated dari menu drop-down. Saat kita ingin membuat peta kepadatan populasi, kita ingin menetapkan warna berbeda untuk setiap fitur saluran sensus berdasarkan kepadatan populasi. Kita memiliki populasi di tabel Estimate!!Total!!Total population dan tabel area di ALAND. Klik tombol Expression untuk menghitung persentase jumlah penduduk pada setiap saluran pencacahan (*Gambar 22*)

24. MAsukkan ekspresi berikut ini 1000000 * ("Estimate!!Total!!Total population"/"ALAND") untuk menghitung kepadatan populasi. Area fitur diberikan dalam kilometer persegi. Kemudian mengubah menjadi meter persegi dengan mengalikannya dengan  1000000 dan menghitung kepadatan penduduk dengan rumus Population/Area. Preview hasil dan klik OK (*Gambar 23*)

25. Pada LAyer Styling panel, klik classify dan masukkan classes sebagai 10 (*Gambar 24*)

26. Klik pada color ramp lalu pilih warna RdTIGn (*Gambar 25*)

27. Kepadatan yang lebih tinggi lebih penting, kita tetapkan warna hijau untuk kepadatan rendah dan merah untu area kepadatan tinggi, Klik pada color ramp dan pilih Invert Color ramp (*Gambar 26*)

28. Sekarang kita memiliki visualisasi informasi kepadatan populasi yang sangat baik di California. Untuk membuatnya lebih baik, mari kita buat batas setiap sensus transparan. Klik pada Syombol tab (*Gambar 27*)

29. Klik pada Stroke color dan klik Transparent stroke (*Gambar 28*)

30. Klik pada values akan memunculkan dialog untuk memasukkan nilai batas atas dan bawah (*Gambar 29*)

31. Setelah kita puas dengan hasilnya tutup layer styling panel. Kita sekarang memiliki visualisasi informasi kepadatan populasi yang terlihat bagus di California (*Gambar 30*)
