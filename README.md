# Threat Hunting with Splunk [Boss of The SOC v1Cyberdefender]
 Repositori ini berisi writeup yang saya tulis mengenai Boss of The SOC v1 - Threat Hunting yang berasal dari platform CyberDefender.org. dimana pada case kali ini kita menggunakan siem splunk untuk membantu dalam melakukan proses Threat Hunting.
 ![image](https://user-images.githubusercontent.com/43168046/185632851-8f74c509-32dc-4ac0-ab51-81109ecc1936.png)

# Source Link :
https://cyberdefenders.org/blueteam-ctf-challenges/15

# Challenge Details : 
Scenario 1 (APT):

The focus of this hands on lab will be an APT scenario and a ransomware scenario. You assume the persona of Alice Bluebird, the analyst who has recently been hired to protect and defend Wayne Enterprises against various forms of cyberattack.

In this scenario, reports of the below graphic come in from your user community when they visit the Wayne Enterprises website, and some of the reports reference "P01s0n1vy." In case you are unaware, P01s0n1vy is an APT group that has targeted Wayne Enterprises. Your goal, as Alice, is to investigate the defacement, with an eye towards reconstructing the attack via the Lockheed Martin Kill Chain.

![image](https://user-images.githubusercontent.com/43168046/185633458-5d59f271-3d4e-4667-8521-e3f9256eaa29.png)

Scenario 2 (Ransomeware):

In the second scenario, one of your users is greeted by this image on a Windows desktop that is claiming that files on the system have been encrypted and payment must be made to get the files back. It appears that a machine has been infected with Cerber ransomware at Wayne Enterprises and your goal is to investigate the ransomware with an eye towards reconstructing the attack. 

![image](https://user-images.githubusercontent.com/43168046/185633253-29b73eec-9ae8-450a-90d2-09057c4bce09.png)

# Question
<p> 1. This is a simple question to get you familiar with submitting answers. What is the name of the company that makes the software that you are using for this competition? Just a six-letter word with no punctuation.</p>
<p> Answer : Software yang digunakan dalam kasus kali ini adalah splunk. dimana Software tersebut termasuk dalam kategori SIEM (Security information and event management) yang memiliki fungsi yaitu memberikan laporan dan peringatan. Fitur laporan SIEM akan mengumpulkan dan menampilkan insiden terkait keamanan, seperti aktivitas berbahaya hingga upaya log-in yang gagal. hal ini dapat membantu tugas dari SOC</p> 

![image](https://user-images.githubusercontent.com/43168046/186939421-81e3433c-a7fd-4b7b-8d03-bb666256d90f.png)

<p> 2. What is the likely IP address of someone from the Po1s0n1vy group scanning imreallynotbatman.com for web application vulnerabilities? </p>
<p> Answer : aktivitas Scanning umumnya dilakukan beberapa kali dalam satuan waktu, sehingga menghasilkan jumlah traffic yang lebih banyak ketimbang yang lain. sehingga disini kami menggunakan query seperti digambar. Terlihat bahwa ip 40.80.148.42 terindikasi memiliki jumlah traffic yang lebih banyak dari pada yang lain yaitu sebanyak 38416</p>

![image](https://user-images.githubusercontent.com/43168046/187012609-2550d23a-bcdb-4c1e-bdcc-704951ddf279.png)

<p> 3. What company created the web vulnerability scanner used by Po1s0n1vy? Type the company name. (For example, "Microsoft" or "Oracle") </p>
<p> Answer : Untuk menjawab pertanyaa ini, kami mencari informasi tersebut di masing masing log yang terekam oleh splunk. Dengan menggunakan bantuan dari ip yang telah diketahui sbeelumnya kami mendapatkan infomrasi bahwa, tools scanner yang dipakai pada kasus ini adalah Acunetix web vulnerability scanner dengan company Acunetix. </p>

![image](https://user-images.githubusercontent.com/43168046/187012851-c5456b42-a79e-4349-81d7-5bf4a8560be0.png)

<p> 4. What content management system is imreallynotbatman.com likely using? (Please do not include punctuation such as . , ! ? in your answer. We are looking for alpha characters only.)</p>
<p> Content Management System atau yang bisas disebut dengan CMS adalah software yang memungkinkan Anda untuk membuat dan mengelola website dengan mudah.Umumnya, sebuah CMS akan memberikan Anda sebuah antarmuka (user interface) di mana Anda bisa mengatur tampilan, fitur dan isi website dengan praktis. Berdasarkan gambar dibawah diketahui bahwa cms yang digunkan pada kasus ini adalah Joomla. </p>

![image](https://user-images.githubusercontent.com/43168046/187019306-4f72e1bd-dae8-438e-a8da-479653598acd.png)

<p> 5. What is the name of the file that defaced the imreallynotbatman.com website? Please submit only the name of the file with the extension (For example, "notepad.exe" or "favicon.ico").</p>
<p> Answer : Sebelumnya pada kasus nomer 2, kami mendapati tiga ip yaitu 192.168.250.70 yang mana kami yakini ini adalah ip korban, alasannya adalah ip lokal, ip kedua adalah 40.80.148.42, sebagai ip grup Po1s0n1vy yang melakukan scanning, serta ip 23.22.63.114. Kami telah berspekulasi pada ip kedua namun tidak menemukan hal yang kami inginkan. namun pada ip ketiga kami menemukan url yang mendirect ke hal lainnya (defaced) .</p>

![image](https://user-images.githubusercontent.com/43168046/187022251-90dee4d1-d5b1-479e-b7d5-60e7750f4c0a.png)

<p> 6. This attack used dynamic DNS to resolve to the malicious IP. What is the fully qualified domain name (FQDN) associated with this attack?.</p>
<p> Answer : Untuk melancarakan serangan Defaced web, biasanya attacker akan menggunakan dns lainnya. sehingga user akan secara otomatis di arahkan ke url tersebut , dimana url tersebut terlihat pada gambar dibawah.</p>

![image](https://user-images.githubusercontent.com/43168046/187022251-90dee4d1-d5b1-479e-b7d5-60e7750f4c0a.png)

<p> 7. What IP address has Po1s0n1vy tied to domains that are pre-staged to attack Wayne Enterprises? </p>
<p> Answer : Pertanyaan ini masih bersangkutan dengan pertanyaan sebelumnya. domain yang digunakan oleh grup Po1s0n1vy dalam melancarkan serangan deface berada pada ip 23.22.63.114.</p>

![image](https://user-images.githubusercontent.com/43168046/187022697-a25cf1e4-214d-4125-a485-944313c8cdff.png)

<p> 8. Based on the data gathered from this attack and common open-source intelligence sources for domain names, what is the email address most likely associated with the Po1s0n1vy APT group?</p>
<p> Answer : Open Source Intelligence (OSINT) adalah metode yang digunakan untuk mencari informasi sebanyak mungkin mengenai suatu target. disini kita akan berushaka mencari alamat email yang terhubung berdasarkan ip 23.22.63.114. Sebelumnya kami tidak menemukan email yang tertaut pada ip tersebut namun terlihat bawah pada ip tersebut tertaut pada dns www.po1s0n1vy.com, dan kami menemukan data email tersebut </p>

![image](https://user-images.githubusercontent.com/43168046/187023188-e4ea63b0-721c-4f8b-b7bc-b4e0345c4d93.png)




