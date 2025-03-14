### Performance Testing (Before oprtimization)
- JMeter test plans through GUI & CLI `/all-student-name` endpoint
![Screenshot 2025-03-12 123923](https://github.com/user-attachments/assets/eb7c40d1-7384-44f7-821a-70d130742f60)
![Screenshot 2025-03-12 125140](https://github.com/user-attachments/assets/f777b769-d7df-44c1-8164-17a152d60fe4)
- JMeter test plans through GUI & CLI `/highest-gpa` endpoint
![Screenshot 2025-03-12 124003](https://github.com/user-attachments/assets/6f1873fd-3cd5-4c6b-aa92-13fdbcb6cd3b)
![Screenshot 2025-03-12 125227](https://github.com/user-attachments/assets/f98a9864-4f6a-4dd8-82c7-d42dee006816)
### Performance Optimization (After oprtimization)
- JMeter test plans through CLI `/all-student-name` endpoint
![Screenshot 2025-03-12 125448](https://github.com/user-attachments/assets/7198c03e-4642-47a9-8f2f-1b843c09b9a6)
- JMeter test plans through CLI `/highest-gpa` endpoint
![Screenshot 2025-03-12 125523](https://github.com/user-attachments/assets/c1969653-a23d-45d3-a1f4-7fcc7b6fdd70)
### Reflection
1. Performance testing dengan JMeter berfokus pada simulasi beban pengguna untuk mengukur respons aplikasi dalam
berbagai skenario penggunaan, terutama dalam kondisi beban tinggi. IntelliJ Profiler digunakan untuk
menganalisis performa di tingkat kode dengan memberikan wawasan mengenai penggunaan CPU, alokasi memori, dan waktu
eksekusi metode. Dengan demikian, JMeter lebih tepat digunakan untuk menguji performa aplikasi secara keseluruhan,
sedangkan IntelliJ Profiler membantu mengidentifikasi dan mengoptimalkan bagian kode yang menyebabkan inefisiensi.

2. Profiling membantu dalam mendeteksi bagian kode yang memerlukan sumber daya paling besar atau memiliki waktu
eksekusi yang terlalu lama. Dengan profiling, dapat dianalisis metode atau proses mana yang menjadi hambatan
dalam performa aplikasi. Selain itu, profiling juga dapat mengungkap adanya memory leak, penggunaan CPU yang
tidak efisien, atau operasi I/O yang berlebihan, sehingga developer dapat melakukan perbaikan secara lebih terarah.

3. IntelliJ Profiler merupakan alat yang efektif dalam mengidentifikasi bottleneck dalam kode karena menyediakan
representasi visual yang mempermudah analisis performa. Dengan fitur seperti CPU usage analysis, memory allocation tracking,
dan execution time breakdown, developer dapat langsung menemukan bagian kode yang perlu dioptimalkan.

4. Beberapa tantangan dalam performance testing dan profiling meliputi kesulitan dalam memahami data hasil analisis,
menentukan akar penyebab permasalahan performa, serta perbedaan hasil antara berbagai metode pengujian. Untuk mengatasinya saya melakukan pendekatan
seperti menggunakan filter dalam profiler untuk menyaring data yang relevan (melihat function mana yang memakan banyak waktu), membandingkan
hasil profiling dalam berbagai skenario before-after, dan melakukan uji coba berulang dengan variabel yang terkontrol.

5. IntelliJ Profiler memberikan berbagai manfaat, seperti analisis performa yang terperinci, deteksi bottleneck secara akurat,
serta kemudahan integrasi dengan lingkungan pengembangan IntelliJ IDEA. Dengan alat ini, pengembang dapat mengidentifikasi
metode yang membutuhkan optimasi, mengurangi konsumsi sumber daya yang tidak perlu, dan meningkatkan efisiensi aplikasi secara keseluruhan.

6. Ketidakkonsistenan antara hasil profiling dan performance testing dapat terjadi karena perbedaan fokus pengujian.
Profiling dengan IntelliJ Profiler lebih menyoroti performa pada tingkat kode, sedangkan pengujian dengan JMeter
lebih mencerminkan respon aplikasi dalam kondisi nyata dengan beban pengguna yang beragam. Untuk mengatasinya saya melakukan pendekatan
seperti memastikan kesamaan kondisi uji coba, membandingkan hasil profiling dan performance testing dalam berbagai skenario before-after,
dan melakukan identifikasi perbedaan testing yang dapat memengaruhi performa aplikasi.

7. Dalam mengoptimalkan kode aplikasi setelah melakukan pengujian dan profiling, saya menerapkan beberapa strategi utama.
Pertama, saya mengganti operasi iteratif yang tidak efisien dengan pendekatan berbasis query database yang lebih optimal, seperti pada metode `findStudentWithHighestGpa()`,
yang awalnya melakukan iterasi manual terhadap semua data dan kini menggunakan Native Query dengan LIMIT 1, sehingga hanya satu data dengan GPA tertinggi yang langsung diambil oleh database.
Kedua, saya mengurangi query berulang dalam metode `getAllStudentsWithCourses()` dengan menggunakan fetch join agar data mahasiswa dan mata kuliah terkait dapat diambil dalam satu query,
mengurangi beban pada aplikasi. Ketiga, saya mengoptimalkan manipulasi string dalam `joinStudentNames()` dengan menggunakan `Collectors.joining()` untuk meningkatkan efisiensi dibandingkan
dengan konkatenasi string di dalam loop. Untuk memastikan perubahan ini tidak memengaruhi fungsionalitas aplikasi, saya melakukan unit testing dan integration testing, serta membandingkan
performa sebelum dan sesudah optimasi menggunakan IntelliJ Profiler untuk mengidentifikasi peningkatan performa.
