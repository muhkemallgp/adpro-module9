#### Nama : Muh. Kemal Lathif Galih Putra
#### NPM : 2206081225
#### Kelas : ADPRO - A
#### ASDOS : REN

# TUTORIAL - 9
## Refleksi

1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?

    __Jawaban:__

    Perbedaan utama antara unary streaming dan server streaming adalah
    
     __Pada unary, client hanya mengirimkan data kecil dan satu kali ke server__.
    
    __Pada server streaming, server mengirimkan informasi dalam jumlah besar melalui satu stream (beberapa data cukup besar berkali-kali hingga menjadi data besar keseluruhan)__.  
    
    __Bidirectional streaming mirip dengan server streaming, tetapi kini client juga terlibat dalam pengiriman data dengan cara yang sama dengan server streaming__, 

    - __Unary__ cocok digunakan untuk __autentikasi/autorisasi dan pengiriman form__, sedangkan 

    - __server streaming__ cocok untuk mengirimkan data dalam jumlah besar seperti __harga saham atau berita__.
    
    - __Bidirectional__ cocok untuk __kolaborasi editing__ atau __permainan real-time atau chatbot__.

2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?

    __Jawaban:__

    GRPC membutuhkan validasi autorisasi/autentikasi secara berulang untuk setiap potongan data yang dikirimkan, berbeda dengan REST yang hanya memerlukan validasi sekali untuk setiap permintaan. Selain itu, setiap potongan data yang dikirimkan baik oleh server maupun klien dalam GRPC harus dienkripsi secara terpisah untuk menjaga privasi. Jadi, GRPC menuntut proses autorisasi/autentikasi/enkripsi yang berulang dalam satu permintaan aliran data, sementara REST hanya memerlukan validasi sekali karena koneksi ditutup setelah respons.

    Dalam kata lain dengan GRPC yang melakukan enkripsi secara otomatis berulang-ulang dibandingkan REST yang dilakukan manual, lebih baik GRPC dalam security consideration in auth/author/encryp

3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?

    __Jawaban__
    
    Dalam pengembangan aplikasi chat menggunakan Rust gRPC, terdapat beberapa masalah yang mungkin timbul saat menangani streaming dua arah, seperti sinkronisasi pesan yang kurang tepat antara pengirim dan penerima, potensi deadlock jika kedua ujung saluran saling menunggu, risiko overflow buffer jika pesan tidak dikonsumsi dengan cepat, perlunya mekanisme pemulihan kesalahan untuk koneksi yang tidak stabil, serta perhatian khusus terhadap konkurensi dan masalah keamanan seperti enkripsi pesan dan otentikasi pengguna

4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?

    __Jawaban__
    
    Menggunakan tokio_stream::wrappers::ReceiverStream untuk streaming respons dalam layanan Rust gRPC menawarkan 
    - Fleksibilitas dengan dukungan untuk berbagai jenis receiver, seperti channel atau future.
    - Memudahkan integrasi dengan komponen lain dalam ekosistem `Tokio.` 
    
    Meskipun demikian, pendekatan ini juga membawa 
    - Kompleksitas tambahan dan potensi overhead kecil, terutama bagi pengembang yang belum terbiasa dengan pemrograman asinkron dan konsep `Tokio.` 

5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?

    __Jawaban__
    
    Dengan struktur yang sesuai, Rust gRPC memfasilitasi peningkatan maintainability dan ekstensibility. Hal ini karena dengan menggunakan protokol __.proto dan diintegrasikan dengan sebuah interface__ yang memungkinkan implementasi class di Rust dapat dibuat, memudahkan dalam penambahan fitur dan perubahan kode secara keseluruhan. 

6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?

    __Jawaban__
    
    Untuk menangani logika pemrosesan pembayaran yang lebih kompleks dalam implementasi MyPaymentService, langkah-langkah tambahan yang mungkin diperlukan meliputi 
    - Validasi dan penanganan kesalahan yang cermat
    - Otentikasi dan otorisasi pengguna
    - Integrasi dengan gateway pembayaran eksternal
    - Manajemen status transaksi
    - Skalabilitas
    - Penegakan aturan bisnis
    - Notifikasi acara
    - Rekonsiliasi transaksi
    - Pengujian yang cermat. 
    
    Atau bahkan dalam general nya bisa saja kita ubah pattern dari networking yang digunakan yang awalnya unary menjadi server streaming

    Dengan langkah-langkah ini, logika pemrosesan pembayaran dapat ditingkatkan untuk menangani skenario yang lebih kompleks dengan efektif.

7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?

    __Jawaban__

    Dengan penggunaan gRPC, tidak perlu lagi khawatir tentang bagaimana mengakses modul melalui metode HTTP (communication protocol). Ini karena gRPC secara otomatis mengelola pemanggilan method yang diinginkan melalui definisi yang telah disepakati dalam file proto. Hal ini memungkinkan client untuk dengan mudah memanggil fungsi dari server, menyederhanakan konektivitas dan operasi antar berbagai teknologi, platform, dan sistem yang terdistribusi.

8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?

    __Jawaban__
    
    HTTP/2 memiliki kelebihan dalam mengizinkan banyak permintaan dan tanggapan dilakukan dalam satu koneksi, namun jika dibandingkan dengan HTTP/1.1, hal ini dapat menimbulkan biaya overhead yang lebih tinggi untuk kinerja dan penggunaan memori, terutama untuk pengiriman data yang kecil. Walaupun demikian, HTTP/2 tetap lebih efisien untuk pengiriman data yang besar. Dalam konteks REST API, HTTP/2 lebih sesuai karena mendukung fitur-fitur seperti multiplexing, kompresi header, server push, dan prioritas aliran, serta memiliki dukungan yang lebih luas di infrastruktur web, meskipun WebSocket lebih cocok untuk komunikasi real-time.

9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?

    __Jawaban__
    
    Model permintaan-tanggapan dari REST API cenderung bersifat satu arah, di mana klien membuat permintaan dan server memberikan tanggapan. Ini berbeda dengan kemampuan streaming bidireksional dari gRPC yang memungkinkan klien dan server untuk saling berkomunikasi secara langsung dan real-time. Dalam konteks responsivitas dan komunikasi real-time, gRPC dapat menyediakan kinerja yang lebih baik karena kemampuannya untuk mengirim dan menerima data secara asinkron dan secara langsung, sementara REST API perlu menunggu permintaan dari klien sebelum memberikan tanggapan.

10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?

    __Jawaban__

    GRPC menggunakan Protocol Buffers memberikan keunggulan dalam efisiensi, keandalan, dan keamanan dalam pertukaran data antar layanan. Ini berbeda dengan penggunaan JSON dalam REST API yang lebih fleksibel tetapi kurang efisien dan kurang ketat dalam struktur datanya. Jadi, sementara gRPC bisa sedikit lebih rumit untuk dipelajari, ia menawarkan kinerja yang lebih baik dan memastikan konsistensi dalam pertukaran data. 
    
    Jika kita ingin membangun aplikasi yang membutuhkan kecepatan tinggi dan keamanan, gRPC mungkin menjadi pilihan yang bagus. Akan tetapi, jika kita lebih memilih fleksibilitas dalam struktur data dan kenyamanan dalam pembelajaran, REST API dengan JSON bisa menjadi alternatif yang baik.
    
