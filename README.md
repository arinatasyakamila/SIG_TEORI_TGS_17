# SIG_TEORI_TGS_17
 performing spatial queries

1. Temukan file metro_stations_accessbility.zip di Peramban QGIS dan kembangkan. Pilih file metro_stations_accessbility.shp dan seret ke kanvas. Metro_stations_accessbility layer baru akan dimuat di panel Layers.


2. Lapisan data untuk bar dan pub dalam format CSV. Untuk memuatnya di QGIS, pergi ke Layer ‣ Add Layer ‣ Add Delimited Text Layer…. ( Lihat Mengimpor File Spreadsheet atau CSV (QGIS3) untuk detail lebih lanjut tentang mengimpor file CSV)

3. Di Manajer Sumber Data | Dialog Teks yang Dibatasi, telusuri dan pilih file Bars_and_pubs__with_patron_capacity.csv yang diunduh sebagai Nama file. Kolom bidang X dan bidang Y harus dipilih secara otomatis untuk masing-masing koordinat x dan koordinat y. Klik Tambahkan.

4. Anda akan melihat layer Bars_and_pubs__with_patron_capacity baru ditambahkan ke panel Layers. Kedua layer input berada di Geograhpic Coordinate Reference System (CRS) EPSG:4326 WGS84. Untuk melakukan analisis spasial, disarankan untuk menggunakan Projected Coordinate Reference System (CRS). Jadi sekarang kita akan memproyeksikan ulang kedua layer ke CRS regional yang sesuai yang meminimalkan distorsi dan memungkinkan kita bekerja dalam satuan jarak seperti meter, bukan derajat. Pergi ke Memproses ‣ Toolbox.

5. Cari dan temukan Vector general ‣ Alat lapisan proyeksi ulang. Klik dua kali untuk meluncurkannya.

6. Pilih Bars_and_pubs__with_patron_capacity sebagai lapisan Input. Klik tombol Select CRS di sebelah Target CRS.

7. Saat memilih sistem koordinat yang diproyeksikan untuk analisis Anda, tempat pertama yang harus dicari adalah CRS regional untuk area yang diminati. Untuk Australia, Map Grid of Australia (MGA) 2020 adalah sistem grid berbasis UTM yang digunakan untuk pemetaan lokal dan regional. Melbourne termasuk dalam UTM Zone 55, jadi kita bisa memilih GDA 2020 / MGA zone 55 EPSG:7855` CRS.


Catatan

Jika Anda tidak yakin dengan CRS lokal untuk wilayah tempat Anda bekerja, memilih CRS untuk zona UTM berdasarkan datum WGS84 adalah pilihan yang aman. Anda dapat mengetahui nomor zona UTM wilayah Anda menggunakan UTM Grid Zones of the World.

8. Selanjutnya, klik tombol … di sebelah Diproyeksikan ulang dan pilih Simpan ke GeoPackage. Geopackage adalah data spasial format data terbuka yang direkomendasikan dan merupakan format pertukaran data default untuk QGIS3. Satu file GeoPackage .gpkg dapat berisi beberapa layer vektor dan raster.

9. Beri nama geopackage sebagai spatialquery dan klik Save.

10. Saat diminta nama lapisan, masukkan bar_and_pubs dan klik OK. Klik Jalankan untuk memproyeksikan ulang lapisan.

11. Jendela akan beralih ke tab Log dan Anda akan melihat algoritme berjalan dan membuat lapisan keluaran bar_and_pubs baru.

12. Sekarang kita akan memproyeksikan ulang layer metro_stations_accessbility. Beralih kembali ke tab Parameter di jendela Reproject layer. Pilih metro_stations_accessbility sebagai lapisan Input. Pertahankan Target CRS yang sama. Selanjutnya, klik tombol … di sebelah Diproyeksikan ulang dan pilih Simpan ke GeoPackage. Pilih file output spatialquery yang sama (Ingat bahwa satu file geopackage dapat berisi beberapa layer, jadi kami akan menyimpan layer baru ke file geopackage yang sama). Masukkan metro_stations sebagai nama Layer. Klik Jalankan.

13. Kembali ke jendela utama QGIS, Anda akan melihat 2 layer baru dimuat di panel Layers: bars_and_pubs dan metro_stations. Anda dapat mematikan visibilitas untuk lapisan asli. Sekarang, kami siap untuk melakukan kueri spasial. Karena kami tertarik untuk memilih bar dan pub dalam jarak 500m dari stasiun metro, langkah pertama adalah membuat buffer di sekitar stasiun metro yang mewakili area pencarian kami. Cari dan temukan Vector geometry ‣ Buffer tool di Processing Toolbox dan klik dua kali untuk meluncurkannya.

14. Dalam dialog Buffer, pilih metro_stations sebagai lapisan Input. Tetapkan 500 meter sebagai Jarak. Simpan output ke geopackage spatialquery yang sama dan masukkan metro_stations_buffers sebagai nama Layer. Klik Jalankan.


15. Anda akan melihat layer metro_stations_buffers baru dimuat di panel Layers. Sekarang kita dapat mengetahui titik mana dari layer bars_and_pubs yang termasuk dalam poligon dari layer metro_stations_buffers. Cari Vector selection ‣ Extract by Location tool dari Processing Toolbox dan klik dua kali untuk meluncurkannya.


Catatan

Ekstrak berdasarkan lokasi akan membuat layer baru dengan fitur yang cocok dari kueri spasial. Jika Anda hanya ingin memilih fitur, gunakan alat Pilih berdasarkan lokasi.

Dalam dialog Ekstrak berdasarkan lokasi, pilih bar_and_pubs sebagai fitur Ekstrak dari. Centang Intersect sebagai predikat geometri. Tetapkan metro_stations_buffers sebagai Dengan membandingkan fitur dari. Simpan output ke geopac
