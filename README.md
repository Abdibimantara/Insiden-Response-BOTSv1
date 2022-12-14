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

<p> 9. What IP address is likely attempting a brute force password attack against imreallynotbatman.com? </p>
<p> Answer : Jawaban untuk pertanyaan ini sudah didapatkan pada pertanyaan ke tujuh. yaitu 23.22.61.114 </p>

<p> 10. What is the name of the executable uploaded by Po1s0n1vy? Please include the file extension. (For example, "notepad.exe" or "favicon.ico") </p>
</> Answer : File upload identik dengan metode "POST", dan kami menggunakan hal tersebut serta di kombinasikan dengan ip 23.22.63.114 untuk mencari file executable tersebut seperti pada gambar. </p>

![image](https://user-images.githubusercontent.com/43168046/187027770-02cd3f19-7be9-49c3-bc9d-ac06bd1673fb.png)

<p> 11. What is the MD5 hash of the executable uploaded? </p>
<p> Answer : Setelah diketahui file executable tersebut, selanjutnya adalah mengecek hash dari file tersebut. Tampak pada gambar, awalnya kami mendapati hasil yang terlalu banyak, sehingga kami memanfaatkan query "commandline" untuk menyederhanakannya </p>

![image](https://user-images.githubusercontent.com/43168046/187038048-d515199d-bc68-4300-b40b-4053538e11b7.png)

<p> 12. GCPD reported that common TTP (Tactics, Techniques, Procedures) for the Po1s0n1vy APT group, if initial compromise fails, is to send a spear-phishing email with custom malware attached to their intended target. This malware is usually connected to Po1s0n1vy's initial attack infrastructure. Using research techniques, provide the SHA256 hash of this malware.</p>
<p> Answer : berdasarakn pencarian sebelumnya, ip 23.22.63.114 merupakan ip penyerang dari grup Po1s0n1vy. berdasarkan virustotals kami menemukan beberapa sampel malware yang terhubung dengan ip tersebut. Terlihat pada gambar, kami menemukan 3 file lalu dimana 3 file tersebut termasuk malicious.</p>

![image](https://user-images.githubusercontent.com/43168046/187054771-d39e7c3e-aa25-4974-b6ed-4246129584dd.png)

<p> 13. What is the special hex code associated with the customized malware discussed in question 12? (Hint: It's not in Splunk)  </p>
<p> Answer : kami kembali mencari informasi melalui virustotals.com . Awalnya kami kembali mengecek pada bagian detail, namun sayang kami tidak mendapat apa apa. kami kembali mencari pada bagian tab comunity dan bingo, kami mendapati itu </p>

![image](https://user-images.githubusercontent.com/43168046/187054858-82e811cc-ff65-4240-b2f2-fa4bf242a48a.png)

<p> 14. One of Po1s0n1vy's staged domains has some disjointed "unique" whois information. Concatenate the two codes together and submit them as a single answer. </p>
<p> Answer : Untuk mencari informasi tersebut, dapat menggunakan tools https://www.whoxy.com/whois-history/demo_result.php . sebelumnya kami mendapati beberapa domain yang terhubung di ip 23.22.63.114, namun hanya satu domain yang memiliki kode unik. </p>

![image](https://user-images.githubusercontent.com/43168046/187055015-86624369-d44c-4d96-8d4e-0a1761101272.png)

<p> 15. What was the first brute force password used? </p>
<p> Answer : Kami menggunakan kombinasi query seperti pada gambar dibawah. query ini filter berdasarkan src ip, form data, serta timestap. Terlihat bahwa upaya bruteforce pertama kali dilakukan pada waktu 2016-08-10T21:45:10.253339Z</p>

![image](https://user-images.githubusercontent.com/43168046/187084423-accab7c5-4af8-4aa8-a471-491cf7d0d80b.png)

<p> 16. One of the passwords in the brute force attack is James Brodsky's favorite Coldplay song. Hint: we are looking for a six-character word on this one. Which is it? </p>
<p> Answer : Jujur kami tidak mengikuti Coldplay, sehingga kami kurang tau dan kami mencari di internet. berdasarkan referensi https://en.wikipedia.org/wiki/List_of_songs_recorded_by_Coldplay kami mendapatkan beberapa list kata yang teridiri dari 6 character. Kami pun melakukan trial and error pada splunk untuk mendapatkan password tersebut</p>

![image](https://user-images.githubusercontent.com/43168046/187091413-e345ab8c-ceca-4bd3-8c3d-d80f23827a29.png)

<p> 17. What was the correct password for admin access to the content management system running "imreallynotbatman.com"?</p>
<p> Answer ; Disini kami mencoba mencari tahu apakah ada ip lain selain 22 yang mencoba login. lalu kami menemukan ip 40 yang juga melakukan akses login dengan username admin serta password batman</p>

![image](https://user-images.githubusercontent.com/43168046/187091673-ebfd70ef-3688-4a05-bec9-8946ac4600fe.png)

<p> 18. What was the average password length used in the password brute-forcing attempt? (Round to a closest whole integer. For example "5" not "5.23213") </p>
<p> Answer : Berdasarkan referensi dari https://docs.splunk.com/Documentation/Splunk/latest/SearchReference/CommonEvalFunctions kita dapat memanfaatkan penggunaan fungsi untuk mendapakan informasi yang diinginkan</p>

![image](https://user-images.githubusercontent.com/43168046/187092459-7059deda-8781-4b01-b873-b27094a06001.png)

<p> 19. How many seconds elapsed between the brute force password scan identified the correct password and the compromised login? Round to 2 decimal places. </p>
<p> Answer : berdasarkan hasil dari komdinasi query yang kami masukkan, terlihat 2 tarffic yaitu traffic awal dan traffic terkahir mengugunakan password batman. berdasarkan kalkulator waktu, kami mengetahui selisih waktu tersebut adalah 1 menit 32 detik 169 milidetik, dimana itu adalah 92 detik  169 milidetik. dan bila dibulatkan menjadi 92,17 detik  </p>

![image](https://user-images.githubusercontent.com/43168046/187267435-5989d197-f5bd-4040-b4a2-acf50a953b73.png)

<p> 20 . How many unique passwords were attempted in the brute force attempt? </p>
<p> Answer : Untuk menjawab pertanyaa ini kami menggunakan fungsi dedup untu menemukan password yang tidak sama serta menjumlahkannya menggunakan fungsi count .</p>

![image](https://user-images.githubusercontent.com/43168046/187283519-6889817c-061b-4c16-bbef-7c9f876c261a.png)

<p> 21. What was the most likely IP address of we8105desk in 24AUG2016 </p>
<p> Answer : saat kami mengetikkan we8105desk pada pencarian kami menemukan bahwa we8105desk adalah account name, kami pun menambahkan parameter tersebut pada query pencarian kami. dan terlihat beberapa ip yang terkait pada we8105desk </p>

![image](https://user-images.githubusercontent.com/43168046/187297458-c33922e6-6287-4c9b-a88d-fbb863ae0c14.png)

<p> 22. Amongst the Suricata signatures that detected the Cerber malware, which one alerted the fewest number of times? Submit ONLY the signature ID value as the answer. (No punctuation, just 7 integers.) </p>
<p> Answer : Menggunakan kata kunci "cerber" dan host="suricata-ids.waynecorpinc.local" kami mendapatkan beberapa data yang cocok. namun data tersebut terlalu banyak sehingga kami memfilernya menggunakn ids signature. Terlihat pada gambar dibawah signature id malware cerber "2816763" hanya ditemukan 1 .</p>

![image](https://user-images.githubusercontent.com/43168046/187303259-1c299834-2394-4d02-8dbd-ef660252fbbc.png)

<p> 23. What fully qualified domain name (FQDN) makes the Cerber ransomware attempt to direct the user to at the end of its encryption phase? </p>
<p> Answer : Untuk menjawab pertanyan ini, kami menggunakan query not, untuk menghilangkan domain yang kami rasa normal. selain itu kami juga menggunakan query souce dan tentu saja kami memilih dns. </p>

![image](https://user-images.githubusercontent.com/43168046/187478399-a399fa40-d016-489c-a9bc-13e15879e7f9.png)

<p> 24. What was the first suspicious domain visited by we8105desk in 24AUG2016? </p>
<p> Answer : pada pertanyaan sebelumnya kami mengentaui bahwa host we8105desk menggunakan ip 192.168.250.100, kami menggunakan ip tersebut untuk mencari destinatin yang dituju berdasarkan waktu. namun hasil yang didapatkan sangatlah banyak sehingga kami juga menerapkan fungsi dedup untuk menyingkirkan destination yang kiranya sama (duplicated). Berdasarkan waktu terlihat ada beberapa domain yang kami dapatkan, kami mencoba satu persatu dan mendapatkannya . </p>

![image](https://user-images.githubusercontent.com/43168046/187495741-0d35d74a-1877-403d-80bf-3dec62fb9fbe.png)

<p> 25. During the initial Cerber infection a VB script is run. The entire script from this execution, pre-pended by the name of the launching .exe, can be found in a field in Splunk. What is the length in characters of the value of this field? </p>
<p> Answer : Untuk menemukan bidang ini, kita akan mencari di Sysmon. Sysmon dirancang untuk mencatat aktivitas yang biasanya terkait dengan aktivitas ancaman. Kami telah mempersempit pencarian kami untuk menemukan secara spesifik dari apa yang kami cari. Terdapat event yang dimulai dengan cmd.exe dan panjang bidang ini adalah 4490</p>

![image](https://user-images.githubusercontent.com/43168046/187522573-709e32f6-426d-4c30-9822-89b47f84f371.png)


<p> 26. What is the name of the USB key inserted by Bob Smith? </p>
<p> Answer : Kami telah mencari dengan berbagai query, namun belum mendapatkan hasil yang di inginkan. Namun setelah kami membaca referensi di google.</p>

![image](https://user-images.githubusercontent.com/43168046/187523515-d526556a-6132-4d01-ae13-532a7b44edf9.png)

<p> Kami akhirnya menemukan nama dari USB key dari Bob Smith tersebut</p>

![image](https://user-images.githubusercontent.com/43168046/187523898-490a0556-5ea7-47d0-95f5-3336e4d6751a.png)

<p> 27. Bob Smith's workstation (we8105desk) was connected to a file server during the ransomware outbreak. What is the IP address of the file server? </p>
<p> Answer : Kami kembali menggunakn kombinasi query seperti pada kasus nomer 24. dimana kami menemukan sebanyak 152 kali komunikasi terjadi dengan ip 192.168.250.20 </p>

![image](https://user-images.githubusercontent.com/43168046/187524814-3dfb8091-5944-42ce-83d6-85b2e776741a.png)

<p> 28. How many distinct PDFs did the ransomware encrypt on the remote file server? </p>
<p> Answer : kami menggunakan fungsi dc untuk menjumlahkan total pdf yang kami temukan. nmaun hasil awal kami ternyata salah yaitu 258</p>

![image](https://user-images.githubusercontent.com/43168046/187528773-13d7e87b-0a84-4f9a-8e6d-7d7d364f3173.png)

<p> Sehingga kami berinisiatif untuk mengecek dari 258 event data tersebut dan kami menemukan sebanyak 257 pdf mengarah ke ip 192.168.250.20</p>

![image](https://user-images.githubusercontent.com/43168046/187529144-3c66aa60-e01d-43bb-8444-29a28e745619.png)

<p> 29. The VBScript found in question 25 launches 121214.tmp. What is the ParentProcessId of this initial launch?</p>
<p> Answer : Untuk menjawab pertanyaan ini, kita kembali menggunakan query pada kasus nomer 25. disini kami melusurui lebih lanjut mengenai event tersebut dan bingo kami mendapatkan yang kami inginkan</p>

![image](https://user-images.githubusercontent.com/43168046/187537612-a8c2944d-6128-4a72-a488-a828e1701e52.png)


<p> 30. The Cerber ransomware encrypts files located in Bob Smith's Windows profile. How many .txt files does it encrypt?</p>
<p> Answer : Kita harus melihat semua kejadian di Sysmon yang berisi bob.smith , .txt dan di mana TargetFilename adalah direktori komputer bob.smiths.</p>

![image](https://user-images.githubusercontent.com/43168046/187539112-d6177ebe-547e-48c5-8513-2e7484925b46.png)

<p> 31. The malware downloads a file that contains the Cerber ransomware crypto code. What is the name of that file?</p>
<p><Answer : Untuk menjawab pertanyaan ini, kita kembali menggunakn query seperti pada kasus nomer 24. disini kami mencoba menelusuri lebih dalam evet yang mernagah ke domain solidaritedeproximite.org. disini terlihat bahwa file tersebut adalah /mhtr.jpg .</p>
 
![image](https://user-images.githubusercontent.com/43168046/187547181-b3a406c9-d27d-437b-90c6-7b0f9e8111ea.png)

 <p> 32. Now that you know the name of the ransomware's encryptor file, what obfuscation technique does it likely use?</p>
 <p> Answer : Terlihat bahwa file tersebut beformat .jpg. namun file tersebut malicous, dikarenakan telah di modifikasi oleh attacker dengan memasukan suatu scrip berbahaya. proses tersbeut dikenal dengan nama Steganography</p>

Arigatouuuu

![image](https://user-images.githubusercontent.com/43168046/187548510-23f57400-1582-45e8-a930-46771b9c87ef.png)












 
 




