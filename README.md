# tutorial-11
# Hello MiniKube tutorial
## Compare the application logs before and after you exposed it as a Service. Try to open the app several times while the proxy into the Service is running. What do you see in the logs? Does the number of logs increase each time you open the app?
![image](https://github.com/aryakdaniswara/tutorial-11/assets/120009329/72cf593f-b680-49e7-8a0d-8533ba8cdde6)
Ketika kita mengunjungi aplikasi berkali-kali, logs akan menunjukkan get request dan timestampnya. Semakin kita sering mengunjungi aplikasi, maka akan makin banyak get request dan timestampnya yang akan ditampilkan.
##  Notice that there are two versions of kubectl get invocation during this tutorial section. The first does not have any option, while the latter has -n option with value set to kube-system. What is the purpose of the -n option and why did the output not list the pods/services that you explicitly created?
Penggunaan -n dalam perintah kubectl bertujuan untuk menampilkan detail pods dan service yang terkait dengan namespace tertentu. Ketika opsi -n tidak digunakan di kube-system, 
hanya pods dan service yang terkait dengan namespace default yang akan ditampilkan. Hal ini membuat pods atau service yang sebelumnya telah dibuat secara eksplisit di namespace kube-system tidak muncul.

## What is the difference between Rolling Update and Recreate deployment strategy?
Kedua strategi tersebut adalah metode deployment yang dapat digunakan untuk mengimplementasikan aplikasi. Perbedaan utama antara keduanya terletak pada cara menangani pembaruan. Pada rolling update, versi baru dari aplikasi menggantikan versi lama secara bertahap. Proses ini dilakukan dengan mengganti pod yang menjalankan aplikasi satu per satu. Dengan cara ini, tidak terjadi downtime selama pembaruan deployment. Sebaliknya, Recreate deployment dilakukan dengan mematikan pod yang ada terlebih dahulu, kemudian menjalankan versi terbaru. Pendekatan ini dapat menyebabkan downtime saat pembaruan berlangsung. Meskipun demikian, metode ini cenderung lebih sederhana dibandingkan strategi rolling update.
## Try deploying the Spring Petclinic REST using Recreate deployment strategy and document your attempt
Membuat deployment rest petclinic
![image](https://github.com/aryakdaniswara/tutorial-11/assets/120009329/aeacba5c-ab83-40e4-9f39-072eb83a273d)

Mengedit deployment yaml untuk mengubah versinya menjadi 3.2.1
![image](https://github.com/aryakdaniswara/tutorial-11/assets/120009329/5d4b605b-c023-44b2-9e41-9359924a9c17)

Menghapus pod dan memunculkannya lagi
![image](https://github.com/aryakdaniswara/tutorial-11/assets/120009329/d0c96f05-00ed-45e0-8f22-bbb580f20b0d)

## Prepare different manifest files for executing Recreate deployment strategy.'
- Kita perlu mendapatkan file yaml menggunakan perintah yang tadi kita gunakan sebelumnya untuk melihat file yaml tersebut kubectl get deployments/spring-petclinic-rest -o yaml
- Selanjutnya, kita perlu mengubah bagian
```
strategy:
  rollingUpdate:
    maxSurge: 25%
    maxUnavailable: 25%
  type: RollingUpdate
```
menjadi
```
strategy:
    type: Recreate
```
Pengubahan tersebut akan mengubah strategynya menjadi recreate

##  What do you think are the benefits of using Kubernetes manifest files?
Manifest files merupakan file yang digunakan untuk mendefinisikan konfigurasi dan deployment aplikasi. Menggunakan manifest files memiliki beberapa kelebihan dibandingkan dengan melakukan deployment secara manual. Pertama, manifest files mendukung automasi dalam proses CI/CD, memungkinkan integrasi dan deployment yang lebih efisien. Kedua, manifest files memastikan konsistensi, karena konfigurasi yang sama dapat diterapkan berulang kali, mengurangi risiko kesalahan manusia. Ketiga, manifest files dapat digunakan kembali, sehingga kita bisa melakukan deployment yang sama berkali-kali tanpa harus mengulangi langkah-langkah yang sama. Keempat, manifest files berfungsi sebagai dokumentasi yang lengkap mengenai konfigurasi dan infrastruktur aplikasi. Terakhir, dengan menyimpan manifest files dalam sistem version control, kita dapat melacak perubahan yang terjadi dan mengembalikan ke versi sebelumnya jika diperlukan.

