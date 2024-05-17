# tutorial-11
# Hello MiniKube tutorial
## Compare the application logs before and after you exposed it as a Service. Try to open the app several times while the proxy into the Service is running. What do you see in the logs? Does the number of logs increase each time you open the app?
![image](https://github.com/aryakdaniswara/tutorial-11/assets/120009329/72cf593f-b680-49e7-8a0d-8533ba8cdde6)
Ketika kita mengunjungi aplikasi berkali-kali, logs akan menunjukkan get request dan timestampnya. Semakin kita sering mengunjungi aplikasi, maka akan makin banyak get request dan timestampnya yang akan ditampilkan.
##  Notice that there are two versions of kubectl get invocation during this tutorial section. The first does not have any option, while the latter has -n option with value set to kube-system. What is the purpose of the -n option and why did the output not list the pods/services that you explicitly created?
Penggunaan -n dalam perintah kubectl bertujuan untuk menampilkan detail pods dan service yang terkait dengan namespace tertentu. Ketika opsi -n tidak digunakan di kube-system, 
hanya pods dan service yang terkait dengan namespace default yang akan ditampilkan. Hal ini membuat pods atau service yang sebelumnya telah dibuat secara eksplisit di namespace kube-system tidak muncul.
