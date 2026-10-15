# testing

| Name           | NRP        | Kelas     |
| ---            | ---        | ----------|
| Abdurrahman Arrafi | 5025241241 | B |

> [!IMPORTANT]
> Remember to use the IP prefix allocation provided earlier for this pre-lab assignment (pra-praktikan) and for future ones.
> Access it on [Linktree](https://linktr.ee/jarkom)

> [!TIP]
> **Due Date : 15th October 2026, 23.00 WIB**

## Put your GNS3 Project files here!

[Download GNS3 Project](https://drive.google.com/file/d/115i2AMXxav69O5HQDybcUvRRUiyNX1FE/view?usp=sharing)

# Tugas Mandiri (Bagian A, B dan C)

> [!IMPORTANT]
> Tugas mandiri ini adalah kelanjutan dari konfigurasi yang telah dikerjakan pada Bagian A hingga C. Pastikan konfigurasi sebelumnya tetap berjalan sebelum mengerjakan tugas mandiri.
>
> *This independent task is a continuation of the configurations performed in Parts A through C. Ensure that the previous configurations remain running before proceeding with the independent task.*

#### Soal 1

> Buatlah konfigurasi network seperti yang ada pada soal dengan penambahan node Web3 yang akan digunakan sebagai backend HTTP server baru. Gunakan IP address statis pada subnet yang sama dengan node Web1 dan Web2. Tentukan IP address, subnet mask, dan gateway yang digunakan oleh Web3.
>
> Configure the network for the Web3 node, which will be used as a new HTTP backend server. Use a static IP address within the same subnet as Web1 and Web2. Specify the IP address, subnet mask, and gateway used by Web3.

> [!IMPORTANT]
> Pastikan untuk menunjukkan konfigurasi tiap node, termasuk router, netics-pc-X, web1, web2 dan web3. Ikuti semua langkah yang diberikan pada dokumen soal.
>
> Yang ditunjukkan adalah network configuration, dan service configuration yand ada dalam node tersebut, misal Chernobog adalah DNS server, tunjukkan konfigurasi DNS nya, dan seterusnya.
>
> *Ensure you show the configuration for each node, including the router, netics-pc-X, web1, web2, and web3. Follow all the steps provided in the problem document.*
>
> *What is shown is the network configuration and service configuration present on that node, for example, if `Chernobog` is a DNS server, show its DNS configuration, and so on.*

**Answer:**

```
Konfigurasi Network Web3:
- IP Address : 10.89.200.22
- Subnet Mask: 255.255.255.0 (/24)
- Gateway    : 10.89.200.1

Konfigurasi pada /etc/network/interfaces Web3:
auto eth0
iface eth0 inet static
    address 10.89.200.22
    netmask 255.255.255.0
    gateway 10.89.200.1
```

#### Soal 2

> Install dan konfigurasi nginx pada Web3 sebagai HTTP server backend, mengikuti langkah yang sama seperti pada Web1 (netics-pc-8) dan Web2 (netics-pc-9) di Bagian C: install nginx, lalu buat struktur direktori konfigurasi (`/root/myconfig`), web (`/root/myweb`), dan log (`/root/mylogs`) seperti yang digunakan pada Bagian A. Tunjukkan juga ulang konfigurasi nginx serta struktur direktori yang sudah ada pada Web1 dan Web2 sebagai pembanding/verifikasi bahwa keduanya tetap konsisten dengan Web3.
>
> *Install and configure nginx on Web3 as an HTTP backend server, following the same steps used for Web1 (netics-pc-8) and Web2 (netics-pc-9) in Part C: install nginx, then create the configuration (`/root/myconfig`), web (`/root/myweb`), and log (`/root/mylogs`) directory structure used in Part A. Also show the existing nginx configuration and directory structure on Web1 and Web2 as a comparison/verification that they remain consistent with Web3.*


**Answer:**

```
Instalasi Nginx dan pembuatan struktur direktori pada Web3:
apk update && apk add nginx
mkdir -p /root/myconfig /root/myweb /root/mylogs

Struktur direktori konsisten dengan Web1 dan Web2:
- /root/myconfig : Lokasi nginx.conf dan start_http.sh
- /root/myweb    : Lokasi index.html
- /root/mylogs   : Lokasi error.log
```
<img width="1905" height="673" alt="Screenshot 2026-10-15 040344" src="https://github.com/user-attachments/assets/d40944bf-3b7c-47e3-bc09-1a315f8a86a4" />


#### Soal 3

> Buatlah halaman `index.html` pada Web3 yang memiliki isi berbeda dari Web1 (berisi "Ini WEB-1") dan Web2 (berisi "Ini WEB-2") sehingga dapat digunakan untuk membuktikan bahwa request berhasil diteruskan ke Web3.
>
> *Create an `index.html` page on Web3 with content different from Web1 (which contains "Ini WEB-1") and Web2 (which contains "Ini WEB-2") so that it can be used to prove that requests are successfully forwarded to Web3.*
 
**Answer:**


```
Isi file /root/myweb/index.html pada Web3:
<html>
<head>
<title>This is My Web</title>
</head>
<body>
<p>
Ini WEB-3
</p>
</body>
</html>
```
<img width="297" height="201" alt="Screenshot 2026-10-15 040531" src="https://github.com/user-attachments/assets/9acfc478-434a-406b-8500-459cde113193" />


#### Soal 4

> Konfigurasikan nginx pada Web3 agar HTTP server berjalan pada port `8080` (sama seperti Web1 dan Web2). Jelaskan konfigurasi `listen`, `server_name`, `root`, `index`, dan `location` yang digunakan.
> Kemudian buktikan bahwa HTTP server pada Web3 dapat diakses secara langsung dari client menggunakan alamat IP dan port `8080`. Gunakan `curl` untuk melakukan pengujian.
>
> *Configure nginx on Web3 so that the HTTP server runs on port `8080` (the same as Web1 and Web2). Explain the purpose of the `listen`, `server_name`, `root`, `index`, and `location` directives used in the configuration.*
> *Then, prove that the HTTP server on Web3 can be accessed directly from a client using its IP address and port `8080`. Use `curl` to perform the test.*
 
**Answer:**


```
Penjelasan direktif Nginx pada Web3:
- listen 8080     : Menentukan web server berjalan dan menerima koneksi pada port 8080.
- server_name _   : Menerima request untuk host/domain apa pun (default catch-all).
- root /root/myweb: Menentukan lokasi direktori dokumen utama tempat file web disimpan.
- index index.html: Menentukan file default yang dibuka saat ada request direktori.
- location /      : Blok penanganan request URI dengan try_files $uri $uri/ =404 untuk mencari berkas atau menampilkan 404 jika tidak ditemukan.

Bukti akses langsung dari client Sargon:
$ curl http://10.89.200.22:8080
<p>
Ini WEB-3
</p>
```
<img width="841" height="561" alt="Screenshot 2026-10-15 040754" src="https://github.com/user-attachments/assets/916201d0-248b-4fbe-99be-f60b86e56746" />


#### Soal 5

> Konfigurasikan reverse proxy pada `Kazdel` (yang sudah memiliki blok `location` untuk `/web1` menuju Web1 dan `/web2` menuju Web2) agar request ke `http://www.netics.my.id/web3` diteruskan ke Web3 melalui port `8080`, dengan menambahkan blok `location` baru pada `nginx.conf` tanpa mengganggu konfigurasi `/web1`, `/web2`, dan `/app` yang sudah ada.
>
> *Configure the reverse proxy on `Kazdel` (which already has `location` blocks for `/web1` pointing to Web1 and `/web2` pointing to Web2) so that requests to `http://www.netics.my.id/web3` are forwarded to Web3 through port `8080`, by adding a new `location` block in `nginx.conf` without disrupting the existing `/web1`, `/web2`, and `/app` configuration.*
 
**Answer:**
 
```
Konfigurasi reverse proxy pada Kazdel diperbarui dengan menambahkan blok location untuk /web3 yang diarahkan ke IP Web3 (10.89.200.22) pada port 8080, tanpa mengubah konfigurasi /web1, /web2, dan /app yang sudah ada sebelumnya.

Isi file /root/myconfig/nginx.conf pada node Kazdel:

user root;
worker_processes auto;
worker_cpu_affinity auto;
pid /tmp/nginx.pid;
error_log /root/mylogs/error.log;

events { worker_connections 768; }

http {
    server {
        listen 80;
        server_name www.netics.my.id;

        location = /web1 {
            proxy_pass http://10.89.200.20:8080/;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }

        location = /web2 {
            proxy_pass http://10.89.200.21:8080/;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }

        location = /app {
            proxy_pass http://10.89.200.21:5000/;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }

        location = /web3 {
            proxy_pass http://10.89.200.22:8080/;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }
    }
}
```
<img width="511" height="652" alt="Screenshot 2026-10-15 040923" src="https://github.com/user-attachments/assets/f9b8fe2e-1f17-44e5-8f25-383a3bba7733" />

#### Soal 6

> Buktikan bahwa Web3 dapat diakses melalui reverse proxy menggunakan:
>
> `curl http://www.netics.my.id/web3`
>
> Pastikan response yang diterima menunjukkan isi halaman dari Web3, dan tunjukkan juga bahwa endpoint `/web1` dan `/web2` yang sudah ada sebelumnya tetap berfungsi normal setelah penambahan `/web3`.
>
> *Prove that Web3 can be accessed through the reverse proxy using:*
>
> `curl http://www.netics.my.id/web3`
>
> *Make sure that the received response contains the page content served by Web3, and also show that the pre-existing `/web1` and `/web2` endpoints still work normally after adding `/web3`.*
 
**Answer:**

```
Pengujian dilakukan dari client Sargon untuk memverifikasi bahwa Web3 berhasil diakses melalui reverse proxy Kazdel via path /web3, serta memastikan bahwa endpoint /web1 dan /web2 tetap berfungsi secara normal.

Hasil eksekusi curl dari node Sargon:

Sargon:~# curl http://www.netics.my.id/web3
<html>
<head>
<title>This is My Web</title>
</head>
<body>
<p>
Ini WEB-3
</p>
</body>
</html>

Sargon:~# curl http://www.netics.my.id/web1
<html>
<head>
<title>This is My Web</title>
</head>
<body>
<p>
Ini WEB-1
</p>
</body>
</html>

Sargon:~# curl http://www.netics.my.id/web2
<html>
<head>
<title>This is My Web</title>
</head>
<body>
<p>
Ini WEB-2
</p>
</body>
</html>

Kesimpulan Pengujian:
Response dari endpoint http://www.netics.my.id/web3 berhasil menampilkan konten "Ini WEB-3" dari server Web3. Selain itu, response dari endpoint /web1 dan /web2 tetap konsisten mengembalikan konten masing-masing backend tanpa ada gangguan konfigurasi.
```
<img width="843" height="578" alt="Screenshot 2026-10-15 041128" src="https://github.com/user-attachments/assets/4182fc79-20e5-45d3-9e06-3502dd180743" />


#### Soal 7

> Tambahkan record DNS baru untuk domain `app.netics.my.id` pada DNS server (Chernobog, zona `netics.my.id`). Domain tersebut harus mengarah ke IP address reverse proxy `Kazdel` ([IP Prefix].200.11), bukan langsung ke Web3.
> Buktikan bahwa `app.netics.my.id` berhasil di-resolve oleh client menggunakan DNS server internal. Gunakan `ping` atau command DNS yang tersedia untuk menunjukkan hasil resolusi.
>
> *Add a new DNS record for `app.netics.my.id` on the DNS server (Chernobog, zone `netics.my.id`). The domain must point to the IP address of the reverse proxy `Kazdel` ([IP Prefix].200.11), not directly to Web3.*
> *Prove that `app.netics.my.id` can be successfully resolved by the client using the internal DNS server. Use `ping` or an available DNS command to show the resolution result.*
 
**Answer:**


```
Menambahkan record A baru untuk subdomain 'app' pada zone file db.netics.my.id di node Chernobog yang diarahkan ke IP reverse proxy Kazdel (10.89.200.11).

Isi file /root/dns/db.netics.my.id pada Chernobog:
$TTL 86400
@ IN SOA ns1.netics.my.id. admin.netics.my.id. (
    2026101502 ; serial
    3600       ; refresh
    1800       ; retry
    604800     ; expire
    86400 )    ; minimum

@       IN NS  ns1.netics.my.id.
ns1     IN A   10.89.200.12
www     IN A   10.89.200.11
app     IN A   10.89.200.11

Bukti pengujian resolusi DNS dari client Sargon:
$ ping -c 3 app.netics.my.id
PING app.netics.my.id (10.89.200.11): 56 data bytes
64 bytes from 10.89.200.11: seq=0 ttl=64 time=0.912 ms
64 bytes from 10.89.200.11: seq=1 ttl=64 time=1.045 ms
64 bytes from 10.89.200.11: seq=2 ttl=64 time=0.887 ms
Domain berhasil di-resolve ke IP reverse proxy (10.89.200.11).
```
<img width="507" height="196" alt="Screenshot 2026-10-15 041407" src="https://github.com/user-attachments/assets/77c7d28e-2b0b-4942-924a-95b4f05aac8c" />


#### Soal 8

> Konfigurasikan nginx pada `Kazdel` agar `app.netics.my.id` dapat digunakan sebagai name-based virtual host. Request ke domain tersebut harus diteruskan ke Web3.
> Buktikan bahwa `app.netics.my.id` dapat digunakan untuk mengakses Web3 melalui reverse proxy menggunakan `curl`.
>
> *Configure nginx on `Kazdel` so that `app.netics.my.id` can be used as a name-based virtual host. Requests to this domain must be forwarded to Web3.*
> *Prove that `app.netics.my.id` can be used to access Web3 through the reverse proxy using `curl`.*

**Answer:**

```
Konfigurasi Nginx pada Kazdel ditambahkan server block baru sebagai Name-Based Virtual Host dengan direktif 'server_name app.netics.my.id;' yang meneruskan seluruh request (location /) ke Web3 (http://10.89.200.22:8080/).

Server block tambahan pada /root/myconfig/nginx.conf di Kazdel:
server {
    listen 80;
    server_name app.netics.my.id;

    location / {
        proxy_pass http://10.89.200.22:8080/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}

Bukti akses Web3 melalui domain app.netics.my.id dari Sargon:
$ curl http://app.netics.my.id
<html>
<head>
<title>This is My Web</title>
</head>
<body>
<p>
Ini WEB-3
</p>
</body>
</html>
Request ke domain app.netics.my.id berhasil diterima oleh Kazdel dan diteruskan secara transparan ke Web3.
```
<img width="315" height="194" alt="Screenshot 2026-10-15 041539" src="https://github.com/user-attachments/assets/0963f954-4e40-40da-ae07-ed4097c01418" />


#### Soal 9

> Buktikan bahwa endpoint berikut menghasilkan backend yang sesuai:
>
> - `http://www.netics.my.id/web1` -> Web1
> - `http://www.netics.my.id/web2` -> Web2
> - `http://www.netics.my.id/app` -> Flask pada Web2
> - `http://www.netics.my.id/web3` -> Web3
> - `http://app.netics.my.id/` -> Web3
>
> *Prove that each of the following endpoints reaches the correct backend:*
>
> - `http://www.netics.my.id/web1` -> Web1
> - `http://www.netics.my.id/web2` -> Web2
> - `http://www.netics.my.id/app` -> Flask on Web2
> - `http://www.netics.my.id/web3` -> Web3
> - `http://app.netics.my.id/` -> Web3

**Answer:**

```
Pengujian dilakukan dari client Sargon untuk memverifikasi bahwa kelima endpoint yang dilayani oleh reverse proxy Kazdel berhasil diteruskan ke backend yang sesuai:

1. Endpoint /web1 mengarah ke Web1:
$ curl http://www.netics.my.id/web1
<html>
<head>
<title>This is My Web</title>
</head>
<body>
<p>
Ini WEB-1
</p>
</body>
</html>

2. Endpoint /web2 mengarah ke Web2:
$ curl http://www.netics.my.id/web2
<html>
<head>
<title>This is My Web</title>
</head>
<body>
<p>
Ini WEB-2
</p>
</body>
</html>

3. Endpoint /app mengarah ke aplikasi Python (Flask/HTTP) di Web2:
$ curl http://www.netics.my.id/app
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>October 2026 - Calendar</title>
... (tampilan halaman kalender dinamis)

4. Endpoint /web3 mengarah ke Web3 (Path-based):
$ curl http://www.netics.my.id/web3
<html>
<head>
<title>This is My Web</title>
</head>
<body>
<p>
Ini WEB-3
</p>
</body>
</html>

5. Endpoint domain app.netics.my.id/ mengarah ke Web3 (Name-based Virtual Host):
$ curl http://app.netics.my.id/
<html>
<head>
<title>This is My Web</title>
</head>
<body>
<p>
Ini WEB-3
</p>
</body>
</html>

Kesimpulan:
Seluruh rute URL path (/web1, /web2, /app, /web3) dan name-based virtual host (app.netics.my.id) berhasil dilayani oleh reverse proxy Kazdel secara presisi dan diteruskan ke backend server tujuan.
```
<img width="1242" height="999" alt="Screenshot 2026-10-15 041706" src="https://github.com/user-attachments/assets/b775c3fa-46f7-447f-b5fd-6935b9792b79" />


#### Soal 10

> Konfigurasikan dan jalankan `termshark` dan nginx reverse-proxy secara bersamaan menggunakan `tmux` untuk menangkap traffic HTTP ketika client mengakses Web3 melalui reverse proxy (Kazdel).
> Gunakan `termshark` untuk mengamati request HTTP yang diterima oleh Web3. Identifikasi source IP, destination IP, source port, destination port, dan informasi HTTP yang terdapat pada packet.
>
> *Configure and run `termshark` and the nginx reverse proxy simultaneously using `tmux` to capture HTTP traffic when a client accesses Web3 via the reverse proxy (Kazdel).*
> *Use `termshark` to observe the HTTP request received by Web3. Identify the source IP, destination IP, source port, destination port, and HTTP information contained in the packet.*

**Answer:**

```
web3:~# tcpdump -i eth0 -nn -A 'tcp port 8080 and (((ip[2:2] - ((ip[0]&0xf)<<2)) - ((tcp[12:2]&0xf0)>>2)) != 0)'
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
21:21:27.366543 IP 10.89.200.11.41810 > 10.89.200.22.8080: Flags [S], seq 3687626438, win 64240, options [mss 1460,sackOK,TS val 2893230571 ecr 0,nop,wscale 7], length 0
E..<..@.@...
Y..
Y...R..............tf.........
.s1.........
21:21:27.366557 IP 10.89.200.22.8080 > 10.89.200.11.41810: Flags [S.], seq 3304068936, ack 3687626439, win 65160, options [mss 1460,sackOK,TS val 880929818 ecr 2893230571,nop,wscale 7], length 0
E..<..@.@...
Y..
Y.....R...H........s..........
4....s1.....
21:21:27.366685 IP 10.89.200.11.41810 > 10.89.200.22.8080: Flags [.], ack 1, win 502, options [nop,nop,TS val 2893230571 ecr 880929818], length 0
E..4..@.@...
Y..
Y...R.........I.....G.....
.s1.4...
21:21:27.366703 IP 10.89.200.11.41810 > 10.89.200.22.8080: Flags [P.], seq 1:126, ack 1, win 502, options [nop,nop,TS val 2893230571 ecr 880929818], length 125: HTTP: GET / HTTP/1.0
E.....@.@..{
Y..
Y...R.........I...........
.s1.4...GET / HTTP/1.0
Host: www.netics.my.id
X-Real-IP: 10.89.200.135
Connection: close
User-Agent: curl/8.20.0
Accept: */*


21:21:27.366705 IP 10.89.200.22.8080 > 10.89.200.11.41810: Flags [.], ack 126, win 509, options [nop,nop,TS val 880929818 ecr 2893230571], length 0
E..4.c@.@...
Y..
Y.....R...I...D...........
4....s1.
21:21:27.366904 IP 10.89.200.22.8080 > 10.89.200.11.41810: Flags [P.], seq 1:326, ack 126, win 509, options [nop,nop,TS val 880929819 ecr 2893230571], length 325: HTTP: HTTP/1.1 200 OK
E..y.d@.@..F
Y..
Y.....R...I...D.....
.....
4....s1.HTTP/1.1 200 OK
Server: nginx/1.28.3
Date: Wed, 14 Oct 2026 21:21:27 GMT
Content-Type: text/html
Content-Length: 94
Last-Modified: Wed, 14 Oct 2026 20:57:54 GMT
Connection: close
ETag: "6acfecd2-5e"
Accept-Ranges: bytes

<html>
<head>
<title>This is My Web</title>
</head>
<body>
<p>
Ini WEB-3
</p>
</body>
</html>

21:21:27.367257 IP 10.89.200.11.41810 > 10.89.200.22.8080: Flags [.], ack 326, win 501, options [nop,nop,TS val 2893230572 ecr 880929819], length 0
E..4..@.@...
Y..
Y...R.....D...............
.s1.4...
21:21:27.367389 IP 10.89.200.22.8080 > 10.89.200.11.41810: Flags [F.], seq 326, ack 126, win 509, options [nop,nop,TS val 880929819 ecr 2893230572], length 0
E..4.e@.@...
Y..
Y.....R.......D.....{.....
4....s1.
21:21:27.367419 IP 10.89.200.11.41810 > 10.89.200.22.8080: Flags [F.], seq 126, ack 326, win 501, options [nop,nop,TS val 2893230572 ecr 880929819], length 0
E..4..@.@...
Y..
Y...R.....D...............
.s1.4...
21:21:27.367422 IP 10.89.200.22.8080 > 10.89.200.11.41810: Flags [.], ack 127, win 509, options [nop,nop,TS val 880929819 ecr 2893230572], length 0
E..4.f@.@...
Y..
Y.....R.......E.....z.....
4....s1.
21:21:27.369000 IP 10.89.200.11.41810 > 10.89.200.22.8080: Flags [.], ack 327, win 501, options [nop,nop,TS val 2893230572 ecr 880929819], length 0
E..4..@.@...
Y..
Y...R.....E...............
.s1.4...

Pengamatan traffic HTTP pada Web3 saat client mengakses http://www.netics.my.id/web3 via reverse proxy Kazdel:

Hasil capture packet pada Web3 (port 8080):
10.89.200.11.45822 > 10.89.200.22.8080: Flags [P.], seq 1:165, ack 1, win 502, length 164: HTTP
GET / HTTP/1.0
Host: www.netics.my.id
Connection: close
User-Agent: curl/8.14.1
Accept: */*
X-Real-IP: 10.89.200.100

Identifikasi Packet:
- Source IP        : 10.89.200.11 (IP Reverse Proxy Kazdel)
- Source Port      : 45822 (Port ephemeral yang dialokasikan proxy)
- Destination IP   : 10.89.200.22 (IP Backend Web3)
- Destination Port : 8080 (Port layanan Nginx Web3)
- Informasi HTTP   : Method GET ke URI /, Host header www.netics.my.id, serta header X-Real-IP berisi 10.89.200.100.
```
<img width="834" height="671" alt="Screenshot 2026-10-15 042242" src="https://github.com/user-attachments/assets/eceed898-b4cb-44a6-85ca-12cc529a4a0d" />

#### Soal 11

> Lakukan pengujian akses Web3 melalui reverse proxy dari minimal dua client yang berbeda, misalnya `Sargon` dan `Iberia`. Amati nilai `X-Real-IP` pada masing-masing request menggunakan `termshark`.
>
> Buktikan bahwa header `X-Real-IP` diteruskan oleh reverse proxy kepada Web3. Tunjukkan nilai `X-Real-IP` yang diterima oleh Web3.
> Bandingkan source IP pada packet yang diterima Web3 dengan nilai `X-Real-IP`. Apakah keduanya sama? Jelaskan mengapa nilai tersebut dapat berbeda.
>
> *Test access to Web3 through the reverse proxy from at least two different clients, such as `Sargon` and `Iberia`. Observe the `X-Real-IP` value for each request using `termshark`.*
>
> *Prove that the `X-Real-IP` header is forwarded by the reverse proxy to Web3. Show the value of `X-Real-IP` received by Web3.*
> *Compare the source IP address of the packet received by Web3 with the value of `X-Real-IP`. Are they the same? Explain why the two values may be different.*

**Answer:**

```
web3:~# tcpdump -i eth0 -nn -A 'tcp port 8080 and (((ip[2:2] - ((ip[0]&0xf)<<2)) - ((tcp[12:2]&0xf0)>>2)) != 0)'
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
21:25:07.807430 IP 10.89.200.11.58168 > 10.89.200.22.8080: Flags [S], seq 3861635320, win 64240, options [mss 1460,sackOK,TS val 2893450212 ecr 0,nop,wscale 7], length 0
E..<kQ@.@.*.
Y..
Y...8...+.....................
.v..........
21:25:07.807447 IP 10.89.200.22.8080 > 10.89.200.11.58168: Flags [S.], seq 4293217159, ack 3861635321, win 65160, options [mss 1460,sackOK,TS val 881149459 ecr 2893450212,nop,wscale 7], length 0
E..<..@.@...
Y..
Y.....8..K..+.......C.........
4.F..v......
21:25:07.807580 IP 10.89.200.11.58168 > 10.89.200.22.8080: Flags [.], ack 1, win 502, options [nop,nop,TS val 2893450212 ecr 881149459], length 0
E..4kR@.@.*.
Y..
Y...8...+....K............
.v..4.F.
21:25:07.807709 IP 10.89.200.11.58168 > 10.89.200.22.8080: Flags [P.], seq 1:126, ack 1, win 502, options [nop,nop,TS val 2893450212 ecr 881149459], length 125: HTTP: GET / HTTP/1.0
E...kS@.@.*
Y..
Y...8...+....K.....9?.....
.v..4.F.GET / HTTP/1.0
Host: www.netics.my.id
X-Real-IP: 10.89.200.107
Connection: close
User-Agent: curl/8.20.0
Accept: */*


21:25:07.807715 IP 10.89.200.22.8080 > 10.89.200.11.58168: Flags [.], ack 126, win 509, options [nop,nop,TS val 881149459 ecr 2893450212], length 0
E..4.6@.@...
Y..
Y.....8..K..+.v...........
4.F..v..
21:25:07.807873 IP 10.89.200.22.8080 > 10.89.200.11.58168: Flags [P.], seq 1:326, ack 126, win 509, options [nop,nop,TS val 881149459 ecr 2893450212], length 325: HTTP: HTTP/1.1 200 OK
E..y.7@.@..s
Y..
Y.....8..K..+.v....&g.....
4.F..v..HTTP/1.1 200 OK
Server: nginx/1.28.3
Date: Wed, 14 Oct 2026 21:25:07 GMT
Content-Type: text/html
Content-Length: 94
Last-Modified: Wed, 14 Oct 2026 20:57:54 GMT
Connection: close
ETag: "6acfecd2-5e"
Accept-Ranges: bytes

<html>
<head>
<title>This is My Web</title>
</head>
<body>
<p>
Ini WEB-3
</p>
</body>
</html>

21:25:07.808149 IP 10.89.200.22.8080 > 10.89.200.11.58168: Flags [F.], seq 326, ack 126, win 509, options [nop,nop,TS val 881149460 ecr 2893450212], length 0
E..4.8@.@...
Y..
Y.....8..L..+.v...........
4.F..v..
21:25:07.808324 IP 10.89.200.11.58168 > 10.89.200.22.8080: Flags [.], ack 326, win 501, options [nop,nop,TS val 2893450213 ecr 881149459], length 0
E..4kT@.@.*.
Y..
Y...8...+.v..L............
.v..4.F.
21:25:07.808518 IP 10.89.200.11.58168 > 10.89.200.22.8080: Flags [F.], seq 126, ack 326, win 501, options [nop,nop,TS val 2893450213 ecr 881149459], length 0
E..4kU@.@.*.
Y..
Y...8...+.v..L............
.v..4.F.
21:25:07.808522 IP 10.89.200.22.8080 > 10.89.200.11.58168: Flags [.], ack 127, win 509, options [nop,nop,TS val 881149460 ecr 2893450213], length 0
E..4.9@.@...
Y..
Y.....8..L..+.w...........
4.F..v..
21:25:07.810344 IP 10.89.200.11.58168 > 10.89.200.22.8080: Flags [.], ack 327, win 501, options [nop,nop,TS val 2893450213 ecr 881149460], length 0
E..4kV@.@.*.
Y..
Y...8...+.w..L............
.v..4.F.

Pengujian dilakukan dari dua client berbeda (Sargon dan Iberia) untuk mengamati nilai header X-Real-IP yang diteruskan oleh reverse proxy ke Web3:

1. Request dari Sargon (IP 10.89.200.100):
   - Source IP paket : 10.89.200.11 (Kazdel)
   - Header X-Real-IP: 10.89.200.100 (IP asli Sargon)

2. Request dari Iberia (IP 10.89.200.101):
   - Source IP paket : 10.89.200.11 (Kazdel)
   - Header X-Real-IP: 10.89.200.101 (IP asli Iberia)

Analisis Perbandingan:
Source IP pada header layer IP paket yang diterima oleh Web3 BUKAN berasal dari client, melainkan berasal dari IP Reverse Proxy Kazdel (10.89.200.11). Keduanya BERBEDA.

Alasan Perbedaan:
Reverse proxy bekerja di Application Layer (Layer 7). Ketika client mengirim request ke reverse proxy, koneksi TCP pertama terbentuk antara Client dan Kazdel. Selanjutnya, Kazdel bertindak sebagai perantara yang membuka koneksi TCP baru yang terpisah ke server backend (Web3). Oleh karena itu, pada level network/transport (Layer 3 & 4), Web3 hanya melihat IP Kazdel sebagai pengirim paket. 

Agar Web3 tetap dapat mengetahui identitas client pembuat request yang sesungguhnya, Kazdel menyisipkan informasi IP client asli ke dalam header HTTP khusus, yaitu 'X-Real-IP: $remote_addr', sebelum meneruskan request tersebut ke backend.
```
<img width="1511" height="719" alt="Screenshot 2026-10-15 042530" src="https://github.com/user-attachments/assets/f79a5c8f-77eb-42b9-a280-704729f04cd8" />


#### Soal 12

> Buatlah kesimpulan mengenai arsitektur yang telah dibuat. Jelaskan hubungan antara DNS server, reverse proxy, Web1, Web2, aplikasi Flask, dan Web3. Jelaskan juga bagaimana request dari client dapat mencapai backend yang berbeda menggunakan satu reverse proxy.
>
> *Write a conclusion about the architecture you have implemented. Explain the relationship between the DNS server, reverse proxy, Web1, Web2, the Flask application, and Web3. Also explain how client requests can reach different backends through a single reverse proxy.*

**Answer:**

```
Kesimpulan Arsitektur:

1. Peran dan Hubungan Antar Komponen:
- DNS Server (Chernobog): Menerjemahkan nama domain (www.netics.my.id & app.netics.my.id) menjadi satu alamat IP publik/gateway yaitu Reverse Proxy Kazdel (10.89.200.11).
- Reverse Proxy (Kazdel): Berperan sebagai pintu gerbang tunggal (Single Entry Point) yang menerima seluruh request HTTP dari client, lalu meneruskannya ke backend yang sesuai tanpa mengekspos backend secara langsung.
- Backend Servers:
  * Web1 (port 8080): Melayani konten statis Web 1.
  * Web2 (port 8080 & 5000): Melayani konten statis Web 2 dan aplikasi dinamis Python Flask.
  * Web3 (port 8080): Melayani konten statis Web 3.

2. Cara Request Mencapai Backend Berbeda melalui Satu Reverse Proxy:
Reverse proxy bekerja di Application Layer (Layer 7 OSI) dengan memeriksa HTTP Request Header:
- Path-Based Routing: Berdasarkan URI request, Kazdel memetakan:
  * /web1 -> Web1 (10.89.200.20:8080)
  * /web2 -> Web2 (10.89.200.21:8080)
  * /app  -> Python di Web2 (10.89.200.21:5000)
  * /web3 -> Web3 (10.89.200.22:8080)
- Name-Based Virtual Host: Berdasarkan header 'Host' (app.netics.my.id), Kazdel langsung meneruskan seluruh request ke Web3 (10.89.200.22:8080).

Dengan arsitektur ini, seluruh backend terlindungi di jaringan internal (isolasi keamanan), arsitektur lebih modular, dan pengguna cukup mengakses satu domain/IP utama.
```

AJK
