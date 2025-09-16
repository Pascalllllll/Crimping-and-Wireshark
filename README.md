
|    NRP     |      Name      |
| :--------: | :------------: |
| 5025241177 | Hosea Felix Sanjaya |

## Task 1

- Flag

  <img width="1094" height="44" alt="image" src="https://github.com/user-attachments/assets/8b60ea5c-23e1-4105-a573-59670d2dabcf" />
  

> a. Berapa banyak packet yang terekam pada file pcapng?

> _a. How many packets are recorded in the pcapng file?_

**Answer:** `9596`

- Filter expression

  `" "`

- Explanation

  `Tinggal liat di bawah ada tulisan Packets: 9596`

- Output result

  <img width="958" height="786" alt="image" src="https://github.com/user-attachments/assets/5d227e77-0578-42d4-a199-53e461619415" />


<br>
<br>

> b. Ada berapa jenis protocol (total) yang terekam pada traffic?

> _b. How many types of protocol (totals) are recorded in the traffic?_

**Answer:** `12`

- Filter expression

  `" "`

- Explanation

  `Klik Statistics, lalu klik Protocol hierarchy`

- Output result

  <img width="266" height="221" alt="image" src="https://github.com/user-attachments/assets/65cdaa45-5f30-4d0d-a339-3b1c1a54562f" />
  <br>
  
  `Terlihat ada 12 protocol, contoh : Frame, Linux cooked-mode capture, dll sampai Data.`

<br>
<br>

> c. Ada berapa jenis protocol berbasis TCP yang terekam pada traffic?

> _c. How many types of TCP-based applications protocol are recorded in the traffic?_

**Answer:** `8`

- Filter expression

  `" "`

- Explanation

  `Klik Statistics, lalu klik Protocol hierarchy`

- Output result

  <img width="210" height="150" alt="image" src="https://github.com/user-attachments/assets/779269b1-8379-484d-9656-7e8a0bc94a7b" />
  <br>
  
  `Terlihat ada 8 protocol yang berbasis TCP, contoh : Virtual Network Computing, Thrift Protocol, dll sampai Data`

  <br>
  <br>

> d. Ada berapa banyak packet dengan protokol TCP murni yang terekam pada traffic (tanpa data)?

> _d. How many packets with pure TCP protocol are recorded in the traffic (without data)?_

**Answer:** `3223`

- Filter expression

  `" "`

- Explanation

  `Klik Statistics, lalu klik Protocol hierarchy` atau bisa dengan
  `_ws.col.protocol=="TCP" && !data`

- Output result

  <img width="1053" height="300" alt="image" src="https://github.com/user-attachments/assets/639692d6-e68f-48e3-9ea4-55212f374a31" />
  <br>
  
  `Di bagian TCP End Packets terlihat total 3223`

  <img width="961" height="786" alt="image" src="https://github.com/user-attachments/assets/514f1dee-fb60-4e7a-a5f4-c72274158bc0" />

  `gambar diatas jika pakai _ws.col.protocol=="TCP" && !data`
  
  `_ws.col berarti ambil kolom dari wireshark, selanjutnya kalau protocol brarti akan diambil di kolom protocol pada wireshark`

## Task 2

- Flag

  <img width="737" height="38" alt="image" src="https://github.com/user-attachments/assets/8d99ebc3-9079-4ab4-b4b8-c1a7c08c9d92" />
  

> a. Berapa banyak packet berhasil yang berbasis murni TCP dan memiliki flag [ACK]?

> _a. How many packets succeed that are pure TCP based and have [ACK] flag?_

**Answer:** `3209`

- Filter expression

  `_ws.col.protocol =="TCP" && !data && tcp.flags.ack == 1)`

- Explanation

  `Hasilnya 3211 karena ada 2 data yang hitam tcp.analysis.lost_segment dan tcp.analysis.ack_lost_segment,`

  `jadi bisa dikurangi manual 2 atau kalau pakai kode tambahkan !(tcp.analysis.lost_segment || tcp.analysis.ack_lost_segment)`

- Output result

  <img width="959" height="785" alt="image" src="https://github.com/user-attachments/assets/52b60302-b8ea-4036-a284-7eca6109ce38" />

  <br>
  <br>

> b. Berapa banyak packet berhasil yang berbasis murni TCP yang hanya memiliki flag [ACK]?

> _b. How many packets succeed that are pure TCP based and have only [ACK] flag?_

**Answer:** `3172`

- Filter expression

  `_ws.col.protocol =="TCP" && tcp.flags == 0x010`

- Explanation

  `kita pakai ws.col untuk mencari kolom spesifik di wiresharl, selanjutnya pilih protocol untuk masuk ke kolom protocol, ketik TCP untuk murni TCP, lalu untuk tcp.flag pakai 0x010 untuk hanya ACK`

- Output result

<img width="959" height="786" alt="image" src="https://github.com/user-attachments/assets/76208bf8-0653-4c79-b9e6-e449d761a043" />


  `Sebenarnya data yang terdisplay ada 3174, tapi setelah lihat lebih lagi terdapat 2 fata yang berwarna hitam seperti TCP ACKed unseen segment dan TCP Previous segment not captured, ketika tidak mengincludekan keduanya maka dapat hasil yang benar`

  <br>
  <br>

> c. Berapa banyak packet berhasil yang berbasis murni TCP dan memiliki flag selain hanya [ACK]?

> _c. How many packets succeed that are pure TCP based and contain flags other than just [ACK] flag?_

**Answer:** `49`

- Filter expression

  `_ws.col.protocol=="TCP" && !data && tcp.flags !== 0x010`

- Explanation

  `Kita pakai 0x010 yang adalah ACK`

- Output result

<img width="959" height="789" alt="image" src="https://github.com/user-attachments/assets/e09ec615-b200-4db0-bafd-e80c5fbdfa87" />


  <br>
  <br>

## Task 3

- Flag

  <img width="734" height="38" alt="image" src="https://github.com/user-attachments/assets/97f177b7-d762-44e8-9c21-4e9a925abee3" />


> a. Pada port berapa client telnet terbuka?

> _a. In what port is the telnet client open?_

**Answer:** `54184`

- Filter expression

  `telnet`

- Explanation

  `Sebelumnya saya menambahkan kolom baru dengan field diisi tcp.srcport, lalu ketika di display telnet nampak angka dari port clientnya`

- Output result

  <img width="961" height="784" alt="image" src="https://github.com/user-attachments/assets/9f3e0fce-f48d-44e2-9e5e-5ba019bac9f7" />


  <br>
  <br>

> b. Berapa byte file response yang dikirim dari server?

> _b. How many bytes of the response files are sent from the server?_

**Answer:** `1449`

- Filter expression

  `telnet`

- Explanation

  `follow lalu tcp stream, ubah entire conversation, jawaban tertera di pilihan`

- Output result

<img width="920" height="790" alt="image" src="https://github.com/user-attachments/assets/642c1a13-572f-4148-9837-cffdd54cf1b2" />


  <br>
  <br>

> c. Apa username yang digunakan client telnet untuk berhubungan dengan server?

> _c. What telnet client's username is used to connect with the server?_

**Answer:** `jovyan`

- Filter expression

  `telnet`

- Explanation

  `follow salah satu data lalu TCP stream, ada username bernama jovyan`

- Output result

  <img width="752" height="790" alt="image" src="https://github.com/user-attachments/assets/ae802048-3294-4b88-b1a7-09c10011e7c6" />

  `pakai telnet karena tidak terenkripsi jadi bisa dibaca`

  <br>
  <br>

> d. Apa password client telnet?

> _d. What is the telnet client's password?_

**Answer:** `123`

- Filter expression

  `telnet`

- Explanation

  `follow salah satu data lalu TCP stream, ada password: 123`

- Output result

  <img width="752" height="790" alt="image" src="https://github.com/user-attachments/assets/c4559f6f-247f-43e0-8007-961a33a7846b" />

  `pakai telnet karena tidak terenkripsi jadi bisa dibaca`

  <br>
  <br>

## Task 4

- Flag

  <img width="738" height="36" alt="image" src="https://github.com/user-attachments/assets/1fab3b00-f150-4ef8-8a81-c282adea8eb4" />


> a. Apa perintah pertama yang ditulis client pada koneksi telnet?

> _a. What is the first command that client wrote on telnet connection?_

**Answer:** `echo`

- Filter expression

  `telnet`

- Explanation

  `follow salah satu data lalu TCP stream, ada echo`

- Output result

  <img width="752" height="790" alt="image" src="https://github.com/user-attachments/assets/991b66b0-3755-4a33-8dcd-5e0bb85e1022" />


  <br>
  <br>

> b. Apa nama file .txt di server (ditulis bersama ekstensinya)?

> _b. What is the name of .txt file on the server (write with the extension)?_

**Answer:** `test.txt`

- Filter expression

  `telnet`

- Explanation

  `follow salah satu data lalu TCP stream, ada tulisan test.txt, cari yang ada .txt nya`

- Output result

  <img width="751" height="786" alt="image" src="https://github.com/user-attachments/assets/94503bf8-f84d-4c21-b846-a9a211316369" />


  <br>
  <br>

> c. Apa kata pertama dari frasa yang dimasukkan client ke dalam file sebelumnya?

> _c. What is the first word that the client inserted into the previous file?_

**Answer:** `Jarkom`

- Filter expression

  `telnet`

- Explanation

  `follow salah satu data lalu TCP stream, tulisan pertama "Jarkom" setelah cat test.txt`

- Output result

  <img width="750" height="788" alt="image" src="https://github.com/user-attachments/assets/f3052290-34ac-465e-9d45-6a28891fed49" />

`Terlihat yang mau disampaikan setelah cat test.txt kata pertama adalah Jarkom`

  <br>
  <br>

## Task 5

- Flag

 <img width="739" height="40" alt="image" src="https://github.com/user-attachments/assets/fdf2300d-63a4-4b09-9494-66356c8016f2" />


> a. Berapa banyak packet berbasis HTTP yang terekam pada file pcapng?

> _a. How many HTTP packets are recorded in the pcapng file?_

**Answer:** `298`

- Filter expression

  `http`

- Explanation

  `terlihat packet displayed : 298`

- Output result

  <img width="964" height="799" alt="image" src="https://github.com/user-attachments/assets/72d77a64-c786-4ace-8bc7-05edaa989fe4" />


  <br>
  <br>

> b. Ada berapa HTTP packet yang berupa response?

> _b. How many response HTTP packets are recorded in the traffic?_

**Answer:** `149`

- Filter expression

  `http.response`

- Explanation

  `untuk mencari response pada http maka pakai http.response`

- Output result

  <img width="959" height="804" alt="image" src="https://github.com/user-attachments/assets/5207376a-9ce9-4d47-9a00-3966143febd7" />

  <br>
  <br>

> c. Ada berapa paket berbasis HTTP yang berhasil?

> _c. How many HTTP packets that succeed?_

**Answer:** `296`

- Filter expression

  `http` -2 atau

  `http && !(tcp.analysis.lost_segment || tcp.analysis.ack_lost_segment || tcp.analysis.retransmission || tcp.analysis.duplicate_ack || tcp.analysis.out_of_order)`

- Explanation

  `bisa pakai http saja tapi nanti cari data yang berwarna hitam dan kurngkan saja, atau pakai cara ke dua dengan menegasikan semua kemungkinan file hitamm`

- Output result

  <img width="960" height="798" alt="image" src="https://github.com/user-attachments/assets/e12cf2de-08f0-47f2-98e2-a297a056b67f" />


  <br>
  <br>

> d. Apa alamat IP dari client HTTP yang tersambung lokal dengan mesin lain?

> _d. What is the client HTTP IP Address in connection with other local machine?_

**Answer:** `172.16.16.101`

- Filter expression

  `http`

- Explanation

  `Ada di barisan source terlihat semua ip dari http sama yaitu : 172.16.16.101`

- Output result

  <img width="958" height="798" alt="image" src="https://github.com/user-attachments/assets/5e630288-0139-436f-bc4a-fc29551b92d9" />


  <br>
  <br>

## Task 6

- Flag

  <img width="738" height="39" alt="image" src="https://github.com/user-attachments/assets/815b0575-c858-4339-8db5-0132c1fc342f" />


> a. Apakah kamu menemukan fake flag? Tuliskan seluruhnya!

> _a. Did you find the fake flag? Write it whole!_

**Answer:** `FakeFlag{JarkomGampang}`

- Filter expression

  `frame contains "flag"`

- Explanation

  `Karena disuruh mencari flag maka pakai kata kunci flag di display filter, lalu follow tcp stream file flag.txt, lalu dapat fake flag nya`

- Output result

  <img width="756" height="786" alt="image" src="https://github.com/user-attachments/assets/4db6b1ea-b90b-4e99-82d7-f924bc9f9831" />


  <br>
  <br>

> b. Tuliskan username dan password yang tertulis! (format username:password)

> _b. Write the written username and password! (format username:password)_

**Answer:** `Rey:123`

- Filter expression

  `http.request`

- Explanation

  `lalu cari yang api nya janggal, ketemu passwd.txt, lalu follow tcp stream`

- Output result

 <img width="756" height="786" alt="image" src="https://github.com/user-attachments/assets/ee14dab8-598b-4fab-a3d1-1735c3e3809e" />


  <br>
  <br>

## Task 7

- Flag

 <img width="739" height="39" alt="image" src="https://github.com/user-attachments/assets/e7045b6d-224b-4af6-9b83-7d40400b9ffa" />


> Apa nama gambar yang direquest oleh client? (tulis dengan ekstensinya)

> _What is the image that is being requested by the client? (write with its extension)_

**Answer:** `donalbebek.jpg`

- Filter expression

  `http.request`

- Explanation

  `lalu cari yang format jpg karena gambar, ketemu donalbebek.jpg`

- Output result

 <img width="964" height="805" alt="image" src="https://github.com/user-attachments/assets/d4c77dd0-3833-4bb7-ac9b-2dfdf7cfa1b0" />


  <br>
  <br>

## Task 8

- Flag

 <img width="739" height="42" alt="image" src="https://github.com/user-attachments/assets/7630ecb8-0bed-4dca-bafd-6d517bbfd79e" />


> a. Berapa banyak packet berbasis FTP yang terekam pada file pcapng? (with the data)

> _a. How many FTP packets are recorded in the pcapng file? (with the data)_

**Answer:** `81`

- Filter expression

  `ftp || ftp-data`

- Explanation

  `saat liat protocol hierarchy ada tcp dan tcp data, agar si data tidak ikut filter maka pakai || agar baik ftp maupun ftp-data tertampilkan`

- Output result

  <img width="1103" height="804" alt="image" src="https://github.com/user-attachments/assets/e73052f9-0a5e-4332-b8ac-72c1e8ee2c9b" />


  <br>
  <br>

> b. Apa username dan password client di koneksi FTP? (tulis dalam format username:password)

> _b. What is the client's username and password in FTP connection? (write in following format username:password)_

**Answer:** `rey:password123lingangu`

- Filter expression

  `ftp`

- Explanation

  `tinggal lihat pada info bisa tau username dan passwordnya`

- Output result

 <img width="1103" height="802" alt="image" src="https://github.com/user-attachments/assets/04c6db91-b857-4fe4-bea6-181a2c556895" />

  <br>
  <br>

> c. What is the client's command for showing server directory that was sent on request packet?

> _c. Apa command client untuk melihat direktori server yang dikirimkan dalam request packet?_

**Answer:** `LIST`

- Filter expression

  `tcp.request.command`

- Explanation

  `input satu satu dan dapap hasilnya LIST`

- Output result

  <img width="1103" height="805" alt="image" src="https://github.com/user-attachments/assets/9dc00e77-bd9e-42d6-9404-e5d0029e7f7f" />


  <br>
  <br>

## Task 9

- Flag

 <img width="747" height="43" alt="image" src="https://github.com/user-attachments/assets/b039fb50-d59a-4086-a4be-f223fdbf67db" />
 

> a. Apa alamat IP dari FTP server?

> _a. What is the FTP server IP Address?_

**Answer:** `172.16.16.101`

- Filter expression

  `ftp`

- Explanation

  `di kolom source adalah IP address`

- Output result

  <img width="1100" height="795" alt="image" src="https://github.com/user-attachments/assets/740606ea-8156-41b1-8eb8-5152c67490d0" />


  <br>
  <br>

> b. Berapa banyak file yang ada dalam direktori FTP server?

> _b. How many files are there inside the FTP server directory?_

**Answer:** `7`

- Filter expression

  `" "`

- Explanation

  `statistic > protocol heirarchy, di bagian ftp-data kurangkan packets (10) dengan end packets (3)`

- Output result

  <img width="875" height="634" alt="image" src="https://github.com/user-attachments/assets/a72352eb-94dc-4fd4-a5e2-a14cbc14d3f9" />


  <br>
  <br>

> c. Apa nama dari file yang digunakan dalam page.html? (tulis lengkap namanya beserta ekstensinya dan dipisahkan dengan koma ',')

> _c. What are the filenames used in the page.html? (write the filebames with their extensions and separate them with comma ',')_

**Answer:** `pokijan.jpg,research_center.jpg`

- Filter expression

  `ftp-data`

- Explanation

  `follow dan tcp stream yang ada page.html, ada 2 sintaks jpg`

- Output result

<img width="917" height="791" alt="image" src="https://github.com/user-attachments/assets/48fe009b-aee9-4f84-8b5e-be3161fdfe11" />


  <br>
  <br>

## Task 10

- Flag

  <img width="740" height="39" alt="image" src="https://github.com/user-attachments/assets/a513a92e-4f72-4517-a366-35519fee24bd" />


> a. Apa nama file yang mengandung string terencode?

> _a. What is the filename that contains encoded string?_

**Answer:** `secret.txt`

- Filter expression

  `ftp-data`

- Explanation

  `kita saring dengan ftp-data dan menemukan secret.txt`

- Output result
<img width="1099" height="795" alt="image" src="https://github.com/user-attachments/assets/f0bebb5d-4fc2-4a0c-a61a-f8fcf0ff32f3" />
<br><br>
  `Terlihat ada 2 secret.txt`

  

  <br>
  <br>

> b. Apa nama file hasil copy file sebelumnya?

> _b. What is the filename of the previous file copy?_

**Answer:** `secret1.txt`

- Filter expression

  `ftp-data`

- Explanation

  `Terdapat secret1.txt dibawah secret.txt yang mana merupakan copy dari file sebelumnya`

- Output result

  <img width="1099" height="797" alt="image" src="https://github.com/user-attachments/assets/1ca68c1b-d000-4e74-b8ef-a6ab0e78bd4f" />
  <br><br>
  
  `Terlihat dibawah secret.txt ada secret1.txt yang adalah copy file secret.txt`

  <br>
  <br>

> c. What is the decoded string from the previous file?

> _c. Apa decoded string dari file tersebut?_

**Answer:** `Pada suatu hari Rey bertemu dengan Nailong the Milk Dragon. Ketika bertemu, Rey mengajarkan Nailong apa itu Jaringan Komputer. Nailong pun senang karena ternyata Jaringan Komputer itu gampang.`

- Filter expression

  `" "`

- Explanation

  `Pilih salah satu file antara secret.txt atau secret1.txt, lalu klik kanan file itu, lalu follow, lalu TCP stream untuk melihat tulisan yang nantinya akan kita decode `

- Output result

<img width="751" height="802" alt="image" src="https://github.com/user-attachments/assets/55132c0e-6834-4717-9dc4-61b7f256675f" />
<br><br>

  `Itu adalah tulisan yang akan di decode`

<br>
<img width="982" height="681" alt="image" src="https://github.com/user-attachments/assets/603813a5-7088-4610-ba6d-aa43ebaf9424" />
<br><br>

  `Itu kalimat setelah di decode`

  <br>
  <br>

## Summary

`[opsional] untuk mempermudah pengerjaan setiap soal bisa disaring dahulu pakai capture filter --> tcp.analysis.lost_segment || tcp.analysis.ack_lost_segment || tcp.analysis.retransmission || tcp.analysis.duplicate_ack || tcp.analysis.out_of_order`

`Cuman saya telat sadar`

## Problems
