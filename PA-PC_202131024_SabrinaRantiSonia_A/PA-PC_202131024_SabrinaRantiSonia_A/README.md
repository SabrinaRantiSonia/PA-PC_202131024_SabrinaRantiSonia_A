# PA-PC_202131024_SabrinaRantiSonia_A
Project UAS Pengolahan Citra

Berikut ini beberapa teori yang mendukung word segmentation :
1. **Unit Dasar: Kata**: Memahami batasan antara kata-kata memungkinkan pemahaman yang tepat, analisis tata bahasa, dan pemrosesan bahasa.
2. **Hipotesis Unit Diskrit**: Hipotesis ini menyatakan bahwa pemahaman bahasa manusia didasarkan pada identifikasi kata-kata diskrit dari aliran tuturan atau teks yang kontinu. Word segmentation merupakan langkah awal untuk mengenali dan menginterpretasikan makna dari setiap kata secara individual.
3. **Ambiguitas Leksikal**: Word segmentation memungkinkan sistem NLP untuk memahami konteks dengan lebih baik dan membedakan berbagai makna dari sebuah kata.
4. **Morfologi**: Dalam Bahasa Indonesia, kata-kata dapat memiliki struktur morfologis yang kompleks, di mana afiks dan komponen kata lainnya melekat pada bentuk dasar. Word segmentation penting untuk memecah kata-kata kompleks ini menjadi bentuk dasar mereka dan menganalisanya dengan tepat.
5. **Tokenisasi**: Word segmentation terkait erat dengan tokenisasi, di mana teks dibagi menjadi unit-unit yang lebih kecil, umumnya kata-kata atau subkata. Tokenisasi adalah langkah pra-pemrosesan yang penting untuk banyak tugas NLP, termasuk penerjemahan mesin, analisis sentimen, dan penandaan kelas kata.
6. **Model Bahasa Statistik**: Word segmentation berperan penting dalam membangun model bahasa statistik. Model bahasa dilatih pada korpus teks besar, dan mengetahui batasan kata penting untuk mengestimasi probabilitas dan memprediksi kemungkinan urutan kata.
7. **Tugas-tugas NLP**: Untuk berbagai tugas NLP seperti penerjemahan mesin, pengenalan entitas bernama, dan analisis sentimen, penting untuk mengidentifikasi dan memproses kata-kata secara individual. Word segmentation memfasilitasi pengembangan algoritma NLP yang akurat dan efektif.
8. **Efisiensi**: Memecah teks menjadi kata-kata dapat signifikan meningkatkan efisiensi tugas pemrosesan bahasa. Memperlakukan setiap kata sebagai entitas terpisah memungkinkan sistem NLP untuk memproses dan menganalisis data dengan lebih efisien daripada jika menghadapi aliran teks yang kontinu.

Secara keseluruhan, word segmentation merupakan langkah mendasar yang menjadi dasar dalam berbagai tugas pemrosesan bahasa dan berkontribusi pada analisis dan pemahaman yang efektif terhadap bahasa manusia dalam aplikasi NLP.

Cara menyelesaikan Project :
A. Import gambar yang akan diproses

B. Pada reading dan resizing 

Berikut adalah penjelasan baris per baris dari kode tersebut:
1. `img = cv2.imread('nama4.jpg')`: Membaca gambar dengan nama file 'nama4.jpg' menggunakan fungsi `cv2.imread()` dari OpenCV. Gambar tersebut akan disimpan dalam variabel `img`.

2. `img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)`: Mengubah skema warna gambar dari BGR (yang digunakan oleh OpenCV) menjadi RGB menggunakan fungsi `cv2.cvtColor()`. Hal ini diperlukan agar gambar dapat ditampilkan dengan benar menggunakan matplotlib.

3. `h, w, c = img.shape`: Mengambil dimensi gambar menggunakan atribut `shape` dari `img`. Variabel `h` akan menyimpan tinggi (height) gambar, `w` akan menyimpan lebar (width) gambar, dan `c` akan menyimpan jumlah saluran warna (channels) gambar.

4. `if w > 1000:`: Memeriksa apakah lebar gambar lebih besar dari 1000 piksel. Jika iya, maka gambar akan diubah ukurannya agar lebarnya menjadi 1000 piksel, dan tingginya akan diubah secara proporsional.

5. `new_w = 1000`: Menyimpan lebar yang diinginkan setelah penyesuaian ukuran gambar.

6. `ar = w/h`: Menghitung rasio aspek (aspect ratio) gambar dengan membagi lebar (w) oleh tinggi (h).

7. `new_h = int(new_w/ar)`: Menghitung tinggi yang baru dengan membagi lebar baru (new_w) oleh rasio aspek (ar) dan mengubahnya menjadi bilangan bulat (integer) menggunakan fungsi `int()`. Hal ini dilakukan untuk menjaga proporsi gambar.

8. `img = cv2.resize(img, (new_w, new_h), interpolation = cv2.INTER_AREA)`: Mengubah ukuran gambar menjadi lebar baru (new_w) dan tinggi baru (new_h) menggunakan fungsi `cv2.resize()`. Metode interpolasi yang digunakan adalah `cv2.INTER_AREA`, yang baik untuk pengecilan gambar.

9. `plt.imshow(img)`: Menampilkan gambar yang telah diproses menggunakan `plt.imshow()` dari matplotlib.

C. Pada Processing
Berikut adalah penjelasan baris per baris dari kode tersebut:
1. `def thresholding(image)`: Mendefinisikan sebuah fungsi bernama `thresholding` yang memiliki satu parameter `image`, yang merupakan gambar yang akan diproses.

2. `img_gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)`: Mengubah skema warna gambar input menjadi skala abu-abu menggunakan fungsi `cv2.cvtColor()` dengan mode konversi `cv2.COLOR_BGR2GRAY`. Hasilnya disimpan dalam variabel `img_gray`.

3. `ret, thresh = cv2.threshold(img_gray, 80, 255, cv2.THRESH_BINARY_INV)`: Menerapkan thresholding pada gambar skala abu-abu `img_gray` menggunakan fungsi `cv2.threshold()`. Parameter pertama adalah gambar yang akan di-threshold, parameter kedua (80) adalah nilai threshold, parameter ketiga (255) adalah nilai maksimum yang akan diberikan pada piksel yang melebihi nilai threshold, dan parameter keempat (`cv2.THRESH_BINARY_INV`) adalah tipe thresholding yang digunakan, yaitu binary inverse thresholding. Hasil thresholding disimpan dalam variabel `thresh`.

4. `plt.imshow(thresh, cmap="gray")`: Menampilkan gambar hasil thresholding `thresh` menggunakan `plt.imshow()` dari matplotlib. `cmap="gray"` digunakan untuk menampilkan gambar dengan skema warna abu-abu.

5. `return thresh`: Mengembalikan gambar hasil thresholding `thresh` sebagai output dari fungsi `thresholding`.

6. `thresh_img = thresholding(img)`: Memanggil fungsi `thresholding` dengan gambar `img` sebagai argumen. Hasilnya disimpan dalam variabel `thresh_img`.

7. kernel = np.ones((3,85), np.uint8): Mendefinisikan kernel yang akan digunakan dalam operasi dilasi. Kernel adalah sebuah matriks yang digunakan untuk mengubah piksel-piksel dalam gambar berdasarkan operasi matematika tertentu. Pada kasus ini, kernel yang digunakan memiliki ukuran 3x85 dan terdiri dari elemen-elemen bernilai 1. Kernel ini akan digunakan dalam proses dilasi berikutnya.

8. dilated = cv2.dilate(thresh_img, kernel, iterations=1): Melakukan operasi dilasi pada gambar hasil thresholding (thresh_img) menggunakan fungsi cv2.dilate(). Operasi dilasi mengubah setiap piksel di sekitar piksel berwarna putih menjadi putih, sehingga memperluas wilayah piksel berwarna putih. Parameter pertama adalah gambar yang akan di-dilasi (thresh_img), parameter kedua adalah kernel yang digunakan (kernel), dan parameter ketiga (iterations=1) adalah jumlah iterasi yang akan dilakukan. Hasil dilasi disimpan dalam variabel dilated.

9. plt.imshow(dilated, cmap='gray'): Menampilkan gambar hasil dilasi (dilated) menggunakan plt.imshow() dari matplotlib. cmap='gray' digunakan untuk menampilkan gambar dengan skema warna abu-abu.
10. (contours, heirarchy) = cv2.findContours(dilated.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_NONE): Menggunakan fungsi cv2.findContours() untuk menemukan kontur-kontur dalam gambar dilasi (dilated). Parameter pertama adalah gambar yang akan dicari konturnya (dilated.copy()), parameter kedua (cv2.RETR_EXTERNAL) menentukan metode untuk mengambil kontur eksternal saja (tidak termasuk kontur yang berada di dalam objek), dan parameter ketiga (cv2.CHAIN_APPROX_NONE) menentukan metode pendekatan (approximation) kontur yang digunakan. Hasil pencarian kontur disimpan dalam variabel contours, sedangkan heirarchy menyimpan informasi struktur hierarki kontur.

11. sorted_contours_lines = sorted(contours, key=lambda ctr: cv2.boundingRect(ctr)[1]): Mengurutkan kontur-kontur yang ditemukan berdasarkan posisi y (vertikal) dari kotak pembatas (bounding box) masing-masing kontur. Fungsi sorted() digunakan untuk mengurutkan elemen-elemen dalam contours. Parameter pertama adalah objek yang akan diurutkan (contours), dan parameter kedua (key=lambda ctr: cv2.boundingRect(ctr)[1]) adalah fungsi kunci yang menentukan kriteria pengurutan, yaitu berdasarkan nilai y dari bounding box menggunakan fungsi cv2.boundingRect().

D. Pada Line Segemntation
1. img2 = img.copy(): Membuat salinan gambar asli (img) menggunakan fungsi copy() untuk menghindari modifikasi langsung pada gambar asli. Salinan gambar disimpan dalam variabel img2.

2. for ctr in sorted_contours_lines:: Melakukan loop untuk setiap kontur dalam daftar sorted_contours_lines.

3. x, y, w, h = cv2.boundingRect(ctr): Menghitung kotak pembatas (bounding box) untuk setiap kontur menggunakan fungsi cv2.boundingRect(). Fungsi ini mengembalikan koordinat (x, y) pojok kiri atas dari kotak pembatas, serta lebar (w) dan tinggi (h) kotak pembatas. Nilai-nilai ini disimpan dalam variabel x, y, w, dan h.

4. cv2.rectangle(img2, (x, y), (x+w, y+h), (40, 100, 250), 2): Menggambar kotak pembatas pada gambar img2 menggunakan fungsi cv2.rectangle(). Parameter pertama adalah gambar yang akan digambari (img2), parameter kedua adalah koordinat pojok kiri atas kotak pembatas, parameter ketiga adalah koordinat pojok kanan bawah kotak pembatas (dihasilkan dari penambahan x+w dan y+h), parameter keempat ((40, 100, 250)) adalah warna kotak pembatas dalam mode BGR (Biru, Hijau, Merah), dan parameter kelima (2) adalah ketebalan garis kotak pembatas.

E. Pada Text Segmentation
1. kernel = np.ones((3,15), np.uint8): Mendefinisikan kernel yang akan digunakan dalam operasi dilasi. Kernel ini memiliki ukuran 3x15 dan terdiri dari elemen-elemen bernilai 1. Kernel ini akan digunakan dalam proses dilasi berikutnya.

2. dilated2 = cv2.dilate(thresh_img, kernel, iterations=1): Melakukan operasi dilasi pada gambar hasil thresholding (thresh_img) menggunakan fungsi cv2.dilate(). Operasi dilasi ini dilakukan dengan menggunakan kernel yang telah didefinisikan sebelumnya. Hasil dilasi disimpan dalam variabel dilated2.

F. Pada Character Segmentation
1. `img3 = img.copy()`: Membuat salinan gambar asli (`img`) menggunakan fungsi `copy()` untuk menghindari modifikasi langsung pada gambar asli. Salinan gambar disimpan dalam variabel `img3`.

2. `words_list = []`: Membuat sebuah list kosong (`words_list`) yang akan digunakan untuk menyimpan koordinat kotak pembatas setiap kata.

3. `for line in sorted_contours_lines:`: Melakukan loop untuk setiap baris kontur dalam daftar `sorted_contours_lines`.

4. `x, y, w, h = cv2.boundingRect(line)`: Menghitung kotak pembatas (bounding box) untuk setiap baris kontur menggunakan fungsi `cv2.boundingRect()`. Nilai-nilai ini disimpan dalam variabel `x`, `y`, `w`, dan `h`.

5. `roi_line = dilated2[y:y+w, x:x+w]`: Memperoleh ROI (Region of Interest) atau bagian gambar yang sesuai dengan batas kotak pembatas baris. `dilated2` adalah gambar hasil dilasi, dan `y:y+w` serta `x:x+w` adalah range untuk memperoleh ROI.

6. `(cnt, heirarchy) = cv2.findContours(roi_line.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_NONE)`: Menggunakan fungsi `cv2.findContours()` untuk menemukan kontur-kontur pada gambar ROI (`roi_line`). Hasilnya disimpan dalam variabel `cnt` dan `heirarchy`. Metode `cv2.RETR_EXTERNAL` digunakan untuk mengambil kontur eksternal saja, dan `cv2.CHAIN_APPROX_NONE` digunakan untuk mengambil semua titik kontur.

7. `sorted_contour_words = sorted(cnt, key=lambda cntr: cv2.boundingRect(cntr)[0])`: Mengurutkan kontur-kontur yang ditemukan dalam setiap kata berdasarkan posisi x (horizontal) dari kotak pembatasnya menggunakan fungsi `sorted()`. Kontur-kontur yang diurutkan disimpan dalam variabel `sorted_contour_words`.

8. `for word in sorted_contour_words:`: Melakukan loop untuk setiap kontur kata dalam daftar `sorted_contour_words`.

9. `if cv2.contourArea(word) < 400:`: Mengecek luas kontur kata menggunakan fungsi `cv2.contourArea()`. Jika luas kontur kata kurang dari 400, maka kata tersebut diabaikan dan program melanjutkan ke kata berikutnya menggunakan pernyataan `continue`.

10. `x2, y2, w2, h2 = cv2.boundingRect(word)`: Menghitung kotak pembatas (bounding box) untuk setiap kontur kata menggunakan fungsi `cv2.boundingRect()`. Nilai-nilai ini disimpan dalam variabel `x2`, `y2`, `w2`, dan `h2`.

11. `words_list.append([x+x2, y+y2, x+x2+w2, y+y2+h2])`: Menambahkan koordinat kotak pembatas kata ke dalam list `words_list`. Koordinat tersebut dihitung dengan menjumlahkan koordinat baris dengan koordinat kata.

12. `cv2.rectangle(img3, (x+x2, y+y2), (x+x2+w2, y+y2+h2), (255, 255, 100), 2)`: Menggambar kotak pembatas pada gambar `img3` menggunakan fungsi `cv2.rectangle()`. Kotak pembatas ini digambar dengan menggunakan koordinat yang telah dihitung sebelumnya. Parameter keempat (`(255, 255, 100)`) adalah warna kotak pembatas dalam mode BGR (Biru, Hijau, Merah), dan parameter kelima (`2`) adalah ketebalan garis kotak pembatas.

13. `img3 = img.copy()`: Membuat salinan gambar asli (`img`) menggunakan fungsi `copy()` untuk menghindari modifikasi langsung pada gambar asli. Salinan gambar disimpan dalam variabel `img3`.

14. `characters_list = []`: Membuat sebuah list kosong (`characters_list`) yang akan digunakan untuk menyimpan koordinat kotak pembatas setiap huruf.

15. `for line in sorted_contours_lines:`: Melakukan loop untuk setiap baris kontur dalam daftar `sorted_contours_lines`.

16. `x, y, w, h = cv2.boundingRect(line)`: Menghitung kotak pembatas (bounding box) untuk setiap baris kontur menggunakan fungsi `cv2.boundingRect()`. Nilai-nilai ini disimpan dalam variabel `x`, `y`, `w`, dan `h`.

17. `roi_line = dilated2[y:y+h, x:x+w]`: Memperoleh ROI (Region of Interest) atau bagian gambar yang sesuai dengan batas kotak pembatas baris. `dilated2` adalah gambar hasil dilasi, dan `y:y+h` serta `x:x+w` adalah range untuk memperoleh ROI.

18. `(cnt, hierarchy) = cv2.findContours(roi_line.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_NONE)`: Menggunakan fungsi `cv2.findContours()` untuk menemukan kontur-kontur pada gambar ROI (`roi_line`). Hasilnya disimpan dalam variabel `cnt` dan `hierarchy`. Metode `cv2.RETR_EXTERNAL` digunakan untuk mengambil kontur eksternal saja, dan `cv2.CHAIN_APPROX_NONE` digunakan untuk mengambil semua titik kontur.

19. `sorted_contour_words = sorted(cnt, key=lambda cntr: cv2.boundingRect(cntr)[0])`: Mengurutkan kontur-kontur yang ditemukan dalam setiap kata berdasarkan posisi x (horizontal) dari kotak pembatasnya menggunakan fungsi `sorted()`. Kontur-kontur yang diurutkan disimpan dalam variabel `sorted_contour_words`.

20. `for word in sorted_contour_words:`: Melakukan loop untuk setiap kontur kata dalam daftar `sorted_contour_words`.

21. `if cv2.contourArea(word) < 400:`: Mengecek luas kontur kata menggunakan fungsi `cv2.contourArea()`. Jika luas kontur kata kurang dari 400, maka kata tersebut diabaikan dan program melanjutkan ke kata berikutnya menggunakan pernyataan `continue`.

22. `x2, y2, w2, h2 = cv2.boundingRect(word)`: Menghitung kotak pembatas (bounding box) untuk setiap kontur kata menggunakan fungsi `cv2.boundingRect()`. Nilai-nilai ini disimpan dalam variabel `x2`, `y2`, `w2`, dan `h2`.

23. `roi_word = roi_line[y2:y2+h2, x2:x2+w2]`: Memperoleh ROI (Region of Interest) atau bagian gambar yang sesuai dengan batas kotak pembatas kata. ROI ini diambil dari gambar ROI (`roi_line`) menggunakan `y2:y2+h2` dan `x2:x2+w2` sebagai range.

24. `(cnt_chars, _) = cv2.findContours(roi_word.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_NONE)`: Menemukan kontur-kontur pada gambar ROI kata (`roi_word`) menggunakan fungsi `cv2.findContours()`. Hasilnya disimpan dalam variabel `cnt_chars` dan `_`. Metode `cv2.RETR_EXTERNAL` digunakan untuk mengambil kontur eksternal saja, dan `cv2.CHAIN_APPROX_NONE` digunakan untuk mengambil semua titik kontur.

25. `sorted_contour_chars = sorted(cnt_chars, key=lambda cntr: cv2.boundingRect(cntr)[0])`: Mengurutkan kontur-kontur yang ditemukan dalam setiap karakter dalam kata berdasarkan posisi x (horizontal) dari kotak pembatasnya menggunakan fungsi `sorted()`. Kontur-kontur yang diurutkan disimpan dalam variabel `sorted_contour_chars`.

26. `for character in sorted_contour_chars:`: Melakukan loop untuk setiap kontur karakter dalam daftar `sorted_contour_chars`.

27. `x3, y3, w3, h3 = cv2.boundingRect(character)`: Menghitung kotak pembatas (bounding box) untuk setiap kontur karakter menggunakan fungsi `cv2.boundingRect()`. Nilai-nilai ini disimpan dalam variabel `x3`, `y3`, `w3`, dan `h3`.

28. Segmentasi per huruf:
    - `char_x = x + x2 + x3 + x4`: Menambahkan koordinat x dari baris, kata, dan karakter untuk mendapatkan koordinat x absolut dari karakter.
    - `char_y = y + y2 + y3 + y4`: Menambahkan koordinat y dari baris, kata, dan karakter untuk mendapatkan koordinat y absolut dari karakter.
    - `char_w = w4`: Lebar karakter tetap sama dengan lebar bounding box karakter.
    - `char_h = h4`: Tinggi karakter tetap sama dengan tinggi bounding box karakter.
    - `characters_list.append([char_x, char_y, char_x + char_w, char_y + char_h])`: Menambahkan koordinat karakter ke dalam daftar karakter (`characters_list`), dengan format [x_min, y_min, x_max, y_max].
    - `cv2.rectangle(img3, (char_x, char_y), (char_x + char_w, char_y + char_h), (255, 255, 100), 2)`: Menggambar kotak pembatas untuk setiap karakter menggunakan fungsi `cv2.rectangle()`. Kotak pembatas ini digambar dengan menggunakan koordinat yang telah dihitung sebelumnya. Parameter keempat (`(255, 255, 100)`) adalah warna kotak pembatas dalam mode BGR (Biru, Hijau, Merah), dan parameter kelima (`2`) adalah ketebalan garis kotak pembatas.

Sekian Penjelasan saya terimakasih
