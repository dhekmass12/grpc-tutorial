<ol>
    <li>Unary RPC diawali dengan client mengirimkan single request ke server dan menunggu response dari server<br>
    Scenario: simple client-server interaction, client meminta request untuk read suatu data, kemudian server meresponse dengan data yang diinginkan.<br>
    Server Streaming RPC diawali dengan client mengirimkan single request ke server, kemudian server merespons dengan mengirimkan a stream f message.<br>
    Scenario: client request real-time weather information, lalu server mengirimkan informasi cuaca secara real-time dan continu kepada client.<br>
    Bi-directional streaming membolehkan client dan server untuk mengirimkan a stream of message secara asynchronously.<br>
    Scenario: client dan server terlibat komunikasi secara simultaneously, online, dan asynchronously pada suatu chat application. Scenario lainnya yaitu bermain game secara online dimana client dan server aktif mengirimkan data satu sama lain.
    </li>
    <li>Authentication: gunakan client-side certificates atau API keys untuk mengautentikasi clienbts sebelum membolehkan akses ke service.<br>
    Authorication: define dan enforce acess control policies untuk mengetahui yang mana client atau user yang mempunyai permission untuk mengakses spesific resources.<br>
    Data encryption: Gunakan cryptographic algorithm yang kuat dan gunakan juga key management practices untuk encrypt sensitive data saat sampai maupun saat transit.
    </li>
    <li>Memastikan thread safety dan mencegah data races saat mengakses shared resources atau state di antara multiple stream memerlukan design yang teliti dan synchronization.<br>
    Memanage memory allocation dan deallocation akan menjadi complex khususnya saat menghandle banyak concurrent streams.<br>
    Rust's ownership and borrowing system can help prevent memory leaks and resource exhaustion, but improper management may lead to performance degradation or system instability.
    </li>
    <li>Advantages: Tokio adalah asynchronous runtime yang sangat popular sehingga mudah digunakan dengan component dan library lain di Tokio, memperbolehkan asynchronous communication, mudah mengontrol concurrency secara effectively berkat mpsc::Receiver.<br>
    Disadvantages: Cukup sulit dalam mencegah memory leaks dan undefined behavior, terdapat high learning curve sehingga butuh waktu dan tenaga yang ekstra untuk mempelajarinya.
    </li>
    <li>
        <ul>
            <li>Tulis gRPC service interface di file .proto yang terpisah untuk menjaga service definition tetapi clean dan modular.</li>
            <li>Gunakaqn build system seperti `prost` atau `grpc-rs` untuk menggenerate Rust code dari file .proto supaya code tersebut digenerasi di module/folder terpisah dari application code.</li>
            <li>Implementasi setiap gRPC service di module/file nya tersendiri agar menjadi single responsibility principle (SRP).</li>
        </ul>
    </li>
    <li>Menyertakan error handling ketika payment gagal, menambahkan validasi dan verifikasi.</li>
    <li>
        <ul>
            <li>gRPC bergantung pada Protocol Buffers (protobuf) untuk mendefinisikan service interface dan data serialization. Hal ini menghasilkan clear and concise service contract, yang mana merincikan methods, parameters, dan data types exchanged di antara client dan server. </li>
            <li>Penggunaan protobuf memperkenankan language-agnostic service definitions, memperbolehkan adanya interoperability di antara beberapa programming language dan paltforms.</li>
        </ul>
    </li>
    <li>Advantages: Memperkenankan multiple request dan response untuk di multiplexed dalam single TCP connection, mendukung header compression untuk mencegah overhead saat mengirimkan HTTP headers, support server push yaitu push additional resources ke clients tanpa menunggu untuk explicit request.<br>
        Disadvantages: lebih complex, multiplexing dan header compression memakan server-side resources lebih banyak.
    </li>
    <li>
        <ul>
            <li>request-response model menggunakan unary streaming.</li>
            <li>real-time request-response model pada REST API biasanya menggunakan teknik polling atau long polling sehingga lebih tinggi latency dan low-throughput.</li>
            <li>karena tanpa frequest polling, gRPC bidirectional streaming menghasilkanb network overhead yang lebih sedikit dan responsiveness yang lebih.</li>
        </ul>
    </li>
    <li>
        <ul>
            <li>Protobuf memerlukan sebuah predefined schema (.proto file) yang mendefinisikan struktur dari data exchanged antara client dan server. Schema ini dikompilasi ke language-spesific code, mengenforce strong typing dan validasi data saat compile time.</li>
            <li>gRPC menyediakan tooling untuk menggenerate client dan server code dari protobuf schema definitions, menbgautomasi process dari message serialization, deserialization, dan RPC invocation.</li>
        </ul>
    </li>
</ol>