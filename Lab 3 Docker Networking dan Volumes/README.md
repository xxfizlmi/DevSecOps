Hafiz Ilmi
235150209111005

# Lab 3: Docker Networking dan Volumes

Proyek ini menunjukkan bagaimana membuat jaringan kustom di Docker, menggunakan volume untuk menyimpan data persisten, dan memahami penggunaan bind mounts di Windows 11.

## Langkah-langkah

### 1. Membuat Jaringan Kustom dan Menghubungkan Container
#### Membuat Jaringan Kustom
Jalankan perintah berikut di terminal untuk membuat jaringan kustom:
```cmd
docker network create my-custom-network
```

#### Menjalankan Container di Jaringan Kustom
Jalankan container Nginx yang terhubung ke jaringan tersebut:
```cmd
docker run -d --name my-nginx --network my-custom-network nginx
```

Jalankan container Alpine yang juga terhubung ke jaringan yang sama:
```cmd
docker run -it --name my-alpine --network my-custom-network alpine sh
```

Di dalam container Alpine, jalankan perintah berikut untuk menguji komunikasi:
```cmd
ping my-nginx
```

### 2. Menggunakan Volume Bernama untuk Data Persisten
#### Membuat dan Menggunakan Volume Bernama
Buat volume bernama untuk penyimpanan data persisten:
```cmd
docker volume create my-volume
```

Jalankan container baru dengan volume ini:
```cmd
docker run -d --name my-container --mount source=my-volume,target=/app busybox
```

Masuk ke dalam container dan buat file di dalam volume:
```cmd
docker exec -it my-container sh
echo "Hello, Docker!" > /app/hello.txt
exit
```

#### Menghentikan dan Menghapus Container
Hentikan dan hapus container:
```cmd
docker stop my-container
docker rm my-container
```

Jalankan container baru dengan volume yang sama untuk memeriksa apakah file tetap ada:
```cmd
docker run -it --name new-container --mount source=my-volume,target=/app busybox sh
cat /app/hello.txt
```

### 3. Demonstrasi Berbagi Volume antara Container
#### Membuat dan Menjalankan Dua Container yang Berbagi Volume
Jalankan dua container yang berbagi volume bernama my-volume:
```cmd
docker run -d --name container1 --mount source=my-volume,target=/shared busybox
docker run -d --name container2 --mount source=my-volume,target=/shared busybox
```

Tambahkan data ke volume dari container1:
```cmd
docker exec -it container1 sh
echo "Data from container1" > /shared/data.txt
exit
```

Verifikasi data di container2:
```cmd
docker exec -it container2 sh
cat /shared/data.txt
exit
```

### 4. Diskusi Bind Mounts dan Penggunaannya
#### Memahami Bind Mounts
Bind mounts memungkinkan Anda untuk memetakan direktori di host ke dalam container. Tidak seperti volume, bind mounts memberikan kendali lebih atas lokasi di host yang di-mount.

#### Membuat dan Menggunakan Bind Mount
Jalankan container dengan bind mount:
```cmd
docker run -d --name my-bind-container --mount type=bind,source="C:\path\to\my-host-dir",target=/app busybox
```
Catatan: Gantilah C:\path\to\my-host-dir dengan path ke direktori di Windows Anda.