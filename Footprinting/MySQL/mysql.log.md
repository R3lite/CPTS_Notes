nn[38;2;153;153;153mmap -sV -sC 10.129.127.209 -Pn -oA initial_scan[47Dnmnmanmap --s-                                          [42D[38;2;153;153;153msV -sC 10.129.127.209 -Pn -oA initial_scan[42D-A                                         [41D ----ssccrriippt mysql* --pp3333006 10.129.210.114[14D10.129.210.114[?1l>[?2004l
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-05-18 15:19 EDT
Stats: 0:01:20 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 86.54% done; ETC: 15:20 (0:00:11 remaining)
Stats: 0:03:22 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 92.45% done; ETC: 15:22 (0:00:16 remaining)
Stats: 0:05:54 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 95.19% done; ETC: 15:25 (0:00:17 remaining)
NSE: [mysql-brute] usernames: Time limit 10m00s exceeded.
NSE: [mysql-brute] usernames: Time limit 10m00s exceeded.
NSE: [mysql-brute] passwords: Time limit 10m00s exceeded.
Nmap scan report for 10.129.210.114
Host is up (0.051s latency).

PORT     STATE SERVICE VERSION
3306/tcp open  mysql   MySQL 8.0.27-0ubuntu0.20.04.1
| mysql-enum: 
|   Accounts: No valid accounts found
|_  Statistics: Performed 8 guesses in 5 seconds, average tps: 1.6
| mysql-info: 
|   Protocol: 10
|   Version: 8.0.27-0ubuntu0.20.04.1
|   Thread ID: 12
|   Capabilities flags: 65535
|   Some Capabilities: InteractiveClient, SwitchToSSLAfterHandshake, Support41Auth, LongPassword, ODBCClient, Speaks41ProtocolOld, SupportsTransactions, Speaks41ProtocolNew, FoundRows, IgnoreSigpipes, LongColumnFlag, SupportsCompression, IgnoreSpaceBeforeParenthesis, SupportsLoadDataLocal, ConnectWithDatabase, DontAllowDatabaseTableColumn, SupportsMultipleStatments, SupportsMultipleResults, SupportsAuthPlugins
|   Status: Autocommit
|   Salt: uyC)1\x1Bk;\x01L\\x1Bn<\x03{}N_u
|_  Auth Plugin Name: caching_sha2_password
| mysql-brute: 
|   Accounts: No valid accounts found
|_  Statistics: Performed 44040 guesses in 600 seconds, average tps: 74.0

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 613.04 seconds
                                                                                                                                                                                                                                            
[J┌──(kali㉿kali)-[~]
└─$ [?1h=[?2004hmm[38;2;153;153;153man nikto[8Dmy       myssqmysql --u robin --p p robin --h 10.129.210.114[?1l>[?2004l
Enter password: 
ERROR 1049 (42000): Unknown database 'robin'
                                                                                                                                                                                                                                            
[J┌──(kali㉿kali)-[~]
└─$ [?1h=[?2004hmm[38;2;153;153;153mysql -u robin -p robin -h 10.129.210.114[40Dmymyssqmysql --h                                 [33D- [38;2;153;153;153mu robin -p robin -h 10.129.210.114[34D                                   [35D[38;2;153;153;153m-u robin -p robin -h 10.129.210.114[35D                                   [36D[38;2;153;153;153m -u robin -p robin -h 10.129.210.114[36Dmysq                                     [37D[38;2;153;153;153ml -u robin -p robin -h 10.129.210.114[37Ds                                      [38D[38;2;153;153;153mql -u robin -p robin -h 10.129.210.114[38Dmy                                       [39D[38;2;153;153;153msql -u robin -p robin -h 10.129.210.114[39Dm                                        [40Dm[38;2;153;153;153mysql -u robin -p robin -h 10.129.210.114[40D                                         [41Dmysql -u robin -p robin -h 10.129.210.114probin[P[18C [24D[?1l>[?2004l
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MySQL connection id is 373
Server version: 8.0.27-0ubuntu0.20.04.1 (Ubuntu)

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MySQL [(none)]>	show databases;
+--------------------+
| Database           |
+--------------------+
| customers          |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.062 sec)

MySQL [(none)]>	use customers
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
MySQL [customers]> show tables;
+---------------------+
| Tables_in_customers |
+---------------------+
| myTable             |
+---------------------+
1 row in set (0.056 sec)

MySQL [customers]> select * from myTable [41G;
+----+---------------------+------------------------------------------+--------------------+-------------+-------------------------------+-----------------------------------+---------------------+------+
| id | name                | email                                    | country            | postalZip   | city                          | address                           | pan                 | cvv  |
+----+---------------------+------------------------------------------+--------------------+-------------+-------------------------------+-----------------------------------+---------------------+------+
|  1 | Emery Reyes         | diam.eu@icloud.htb                       | Spain              | 26-579      | Quảng Ngãi                    | 675-4432 Nunc Av.                 | 519358 9482346334   | 144  |
|  2 | Kristen Trujillo    | tellus.id@google.htb                     | Costa R.htb        | 376420      | Chiclayo                      | 101-8154 Ac Rd.                   | 546871 777532 7590  | 125  |
|  3 | Fletcher Jimenez    | lobortis@outlook.htb                     | Germany            | 3515        | Timaru                        | 9562 Dui, St.                     | 559 47883 93145 224 | 550  |
|  4 | Boris Sharp         | donec@protonmail.htb                     | Pakistan           | 1317        | Jönköping                     | 728-7809 Cras Road                | 4716447833847468    | 536  |
|  5 | Ruth Carson         | suspendisse.aliquet@yahoo.htb            | Pakistan           | 14945       | Oviedo                        | 324-8221 Ut Road                  | 5164782453566544    | 449  |
|  6 | Caryn Porter        | neque@aol.htb                            | New Zealand        | 3798        | Vichy                         | Ap #770-5801 Donec Rd.            | 4916 475 64 6748    | 590  |
|  7 | G.htbe Stein        | eget@google.htb                          | Spain              | 80125       | Jeonju                        | 305-2770 Lectus. Rd.              | 485 51263 38542 847 | 402  |
|  8 | Emery Watson        | non@icloud.htb                           | Austria            | 23940       | Secunderabad                  | Ap #542-2284 Mauris, Street       | 4716 5544 1838 4955 | 411  |
|  9 | Silas Holder        | metus@hotmail.htb                        | Netherlands        | 63-851      | San Cristóbal de la Laguna    | Ap #604-7295 Duis St.             | 5186 1252 1481 7760 | 863  |
| 10 | Patrick Walls       | aliquet@yahoo.htb                        | Indonesia          | 776718      | Weelde                        | 118-5893 Rhoncus. Ave             | 513 51634 82351 610 | 430  |
| 11 | Barclay Knight      | ut.nec@yahoo.htb                         | Poland             | FX6 7KT     | Sankt Wendel                  | 977-1992 Lacus. Avenue            | 4532532734638447    | 592  |
| 12 | Benjamin Church     | bibendum@yahoo.htb                       | Italy              | 2209        | Dunedin                       | Ap #744-2093 Et Rd.               | 4532684336623       | 887  |
| 13 | Kaitlin Lane        | vulputate.ullamcorper@yahoo.htb          | Colombia           | 21718       | Karnal                        | P.O. Box 257, 6002 Nisi Road      | 526 26236 38237 281 | 206  |
| 14 | Xena Robles         | sed.pharetra.felis@yahoo.htb             | France             | 45767       | Gansu                         | P.O. Box 528, 1077 Hendrerit St.  | 4916377837825       | 609  |
| 15 | France.htb Bowen    | at.egestas.a@aol.htb                     | Brazil             | 346211      | Calbuco                       | 4127 Donec Avenue                 | 4539267757536227    | 950  |
| 16 | Dacey Moore         | donec.est@google.htb                     | Colombia           | 58978-64484 | Wałbrzych                     | 509-5117 Odio Rd.                 | 535718 6638623286   | 385  |
| 17 | Amity Norton        | libero@outlook.htb                       | Mexico             | 727010      | Ulyanovsk                     | 135-2273 Donec St.                | 5584 5235 2526 7360 | 682  |
| 18 | Lee Kline           | nullam.nisl@protonmail.htb               | India              | 323603      | Tianjin                       | 7496 Sed St.                      | 4485 4586 6858 1865 | 699  |
| 19 | Nehru Best          | porttitor@aol.htb                        | South Korea        | 86248-126   | Nottingham                    | Ap #863-5830 Sit Av.              | 546729 525363 3228  | 237  |
| 20 | Isaiah Shields      | consectetuer.adipiscing.elit@outlook.htb | Russian Federation | 6656        | Landenne                      | 664-4572 Ornare St.               | 526357 6725656236   | 689  |
| 21 | Wing Hunt           | nullam.ut.nisi@protonmail.htb            | Mexico             | 7572        | Barranquilla                  | Ap #102-7529 Fusce Av.            | 518537 6364865833   | 636  |
| 22 | Elijah Be.htbt      | porttitor.eros@protonmail.htb            | Belgium            | 182672      | Mérida                        | 625-4778 Tellus. St.              | 4716 1868 1582 4380 | 486  |
| 23 | Whoopi Arnold       | at.sem.molestie@icloud.htb               | Peru               | 58939-421   | Gumi                          | 2523 Duis Av.                     | 431295 6816415539   | 904  |
| 24 | Sandra Malone       | arcu.sed@google.htb                      | Sweden             | 10313       | Yekaterinburg                 | 587-5713 Duis St.                 | 535259 775468 3794  | 634  |
| 25 | Petra Castaneda     | nam.porttitor@outlook.htb                | Austria            | 927788      | Faridabad                     | 609-3290 Dapibus Ave              | 4929 3555 4568 4421 | 992  |
| 26 | Marvin Welch        | amet.ornare.lectus@outlook.htb           | Turkey             | 373446      | Agu.htbliente (San Francisco] | P.O. Box 540, 3664 Vestibulum St. | 4485221576310       | 739  |
| 27 | Yardley Sargent     | egestas@google.htb                       | Nigeria            | 37-476      | Newtonmore                    | 187-4374 Pede Av.                 | 453995 985347 4218  | 152  |
| 28 | Richard Gomez       | iaculis.nec@hotmail.htb                  | Pakistan           | 8742        | Bendigo                       | 9610 Pede, Avenue                 | 453972 3652232650   | 818  |
| 29 | Jamal Hartman       | feugiat.lorem.ipsum@aol.htb              | Belgium            | 3532 NJ     | Uddevalla                     | Ap #818-7127 Feugiat Street       | 536 24517 72645 963 | 404  |
| 30 | Ira Jimenez         | augue.eu@hotmail.htb                     | Nigeria            | 57676       | Galway                        | 765-5415 Vitae Ave                | 5421 6832 2533 5763 | 134  |
| 31 | Iris Patterson      | facilisi.sed.neque@aol.htb               | Costa R.htb        | 37337       | Rennes                        | 501-5659 Eu, Avenue               | 521 82671 22625 356 | 342  |
| 32 | Dana Mayer          | penatibus.et@icloud.htb                  | Canada             | 541542      | Sousa                         | Ap #921-8076 Posuere, St.         | 4024007157848398    | 526  |
| 33 | Octavia Cantu       | neque@outlook.htb                        | Ireland            | 80589-89583 | Belfast                       | 285-6930 Nec Street               | 514873 244492 4196  | 463  |
| 34 | Gage Howard         | eleifend.nunc.risus@protonmail.htb       | Mexico             | 76-627      | Guápiles                      | 644-4786 Nisl Av.                 | 4532 7755 4955 4255 | 694  |
| 35 | Christine Davenport | neque.morbi.quis@hotmail.htb             | Costa R.htb        | 44-821      | Linares                       | 387-2148 Tristique Road           | 452837 956842 7760  | 919  |
| 36 | Olga Shepherd       | posuere@hotmail.htb                      | Belgium            | A5L 8W8     | Guápiles                      | 1514 Accumsan Ave                 | 5133863972378260    | 731  |
| 37 | Stone Langley       | risus.donec@outlook.htb                  | Australia          | 8470        | Gaziantep                     | 989-4653 Lectus Rd.               | 4556734294789       | 324  |
| 38 | Dora Decker         | felis.nulla.tempor@icloud.htb            | Russian Federation | 97-428      | Itanagar                      | Ap #240-2201 Aliquam Road         | 4024 007 14 7143    | 577  |
| 39 | Galvin Cameron      | mauris@yahoo.htb                         | Peru               | 47795-113   | Weyburn                       | 107-9775 Bibendum. Av.            | 448591 194284 3360  | 282  |
| 40 | Rylee Zamora        | mauris.a.nunc@yahoo.htb                  | Austria            | 21347       | Luik                          | Ap #992-3534 In Rd.               | 492 96771 72883 632 | 249  |
| 41 | Yvette Love         | diam.proin@protonmail.htb                | Poland             | 867445      | Cork                          | 447-6584 Eu Avenue                | 4688 594 12 5157    | 423  |
| 42 | Imani Kinney        | aliquam.ornare@outlook.htb               | Vietnam            | 4789        | Haripur                       | 812-7425 Et Rd.                   | 547566 4142882785   | 275  |
| 43 | Louis Bird          | tristique@protonmail.htb                 | Chile              | 342352      | Huasco                        | 203-9462 Erat Ave                 | 4795 272 25 8752    | 681  |
| 44 | Philip Bentley      | vitae.erat@google.htb                    | Ireland            | 82745       | Hong Kong                     | 754-3216 Mattis Street            | 559975 3538532574   | 523  |
| 45 | Kevin Simmons       | ultrices@aol.htb                         | Belgium            | 60433       | Watson Lake                   | P.O. Box 672, 7175 Tellus. St.    | 555564 5225122846   | 804  |
| 46 | Colorado Stevenson  | aliquam.adipiscing.lacus@protonmail.htb  | Brazil             | 366140      | Sint-Jans-Molenbeek           | 517-3815 Aenean Rd.               | 4539 691 72 7413    | 822  |
| 47 | Raya Patton         | semper.et.lacinia@yahoo.htb              | Chile              | 10917       | Abeokuta                      | 522-2194 Nisi Avenue              | 455 63994 24212 284 | 492  |
| 48 | Mufutau Johnston    | ipsum@google.htb                         | China              | 9472 FW     | Chandigarh                    | 564-120 Lorem Rd.                 | 535388 1779662416   | 288  |
| 49 | Leonard Jacobson    | aliquet.vel.vulputate@aol.htb            | Mexico             | 758028      | Camiña                        | P.O. Box 458, 481 Cubilia St.     | 4539647385476625    | 383  |
| 50 | Nora Best           | sed.consequat.auctor@yahoo.htb           | United States      | 51817       | Sangju                        | 937-810 Feugiat Rd.               | 491 63582 84493 652 | 910  |
| 51 | Carter Long         | morbi.sit@icloud.htb                     | Germany            | 15184       | Rangiora                      | 696-2843 Ultrices Road            | 5482 3583 6651 4254 | 127  |
| 52 | Christopher Montoya | bibendum.ullamcorper@protonmail.htb      | United Kingdom     | D6J 3JQ     | Ningxia                       | P.O. Box 998, 4282 Erat, Road     | 4532 243 86 7456    | 740  |
| 53 | Marah Du.htbn       | dictum.sapien@google.htb                 | Belgium            | 13732       | Mastung                       | Ap #821-9828 Lobortis St.         | 5278611274422475    | 354  |
| 54 | Shay Marquez        | nullam.feugiat.placerat@yahoo.htb        | Colombia           | 943199      | Delft                         | 7683 Lorem Rd.                    | 5388634554786176    | 226  |
| 55 | Brandon Mayo        | gravida.aliquam@aol.htb                  | South Korea        | 3442 VL     | Słupsk                        | Ap #320-2381 Senectus Av.         | 542823 7772627362   | 242  |
| 56 | Lucius Herman       | class.aptent@google.htb                  | Belgium            | 978016      | Heilongjiang                  | 8554 Amet St.                     | 546 17855 39776 227 | 420  |
| 57 | Justine Atkinson    | lorem.donec@protonmail.htb               | Netherlands        | 5376        | Algarrobo                     | 117-5490 Purus. Street            | 549616 968589 3830  | 147  |
| 58 | Erich Hicks         | sem.vitae@protonmail.htb                 | Poland             | LB2 5BQ     | Silvassa                      | P.O. Box 654, 4350 Cras Road      | 453976 1133267143   | 246  |
| 59 | Gay Morse           | felis.orci@aol.htb                       | Nigeria            | I8X 0R1     | Dover                         | P.O. Box 597, 2068 Dolor. Road    | 455676 5238367748   | 969  |
| 60 | Jane Daugherty      | a.tortor.nunc@outlook.htb                | South Korea        | 3313        | Soissons                      | 3243 Cursus St.                   | 402400 719918 4513  | 277  |
| 61 | Branden Grimes      | sapien.gravida.non@outlook.htb           | Spain              | 27574-086   | Jauche                        | 2177 Ornare, St.                  | 5169455394956471    | 948  |
| 62 | Hannah Gallagher    | a.sollicitudin@hotmail.htb               | Russian Federation | 30023       | IJlst                         | 1326 Fusce St.                    | 528235 5241422382   | 481  |
| 63 | Victor Livingston   | urna.justo@outlook.htb                   | Indonesia          | 65174       | Curitiba                      | P.O. Box 495, 7831 Nec, Rd.       | 524164 789461 8658  | 812  |
| 64 | Cain Nguyen         | vivamus.nisi@icloud.htb                  | United States      | 4815 XP     | Anamur                        | 238-1803 Nunc Rd.                 | 402 40071 66324 746 | 663  |
| 65 | Wylie Edwards       | et.eros.proin@icloud.htb                 | Ireland            | 313661      | La Roche-sur-Yon              | 504-7645 Nulla St.                | 453 21864 39169 578 | 503  |
| 66 | Lucius Dejesus      | orci.donec@outlook.htb                   | Belgium            | 4024        | Dublin                        | 802-8273 Luctus St.               | 453274 672582 4499  | 346  |
| 67 | Perry Irwin         | eu.tellus.eu@protonmail.htb              | Turkey             | 2214 VZ     | Çermik                        | Ap #650-2563 Ante, Avenue         | 448562 7364679732   | 128  |
| 68 | Rooney Carpenter    | semper@aol.htb                           | Spain              | 423241      | Salem                         | P.O. Box 528, 9665 Mauris Street  | 526433 755731 5378  | 372  |
| 69 | Willa M.htbrty      | vehicula.aliquet@icloud.htb              | New Zealand        | 20784-17169 | Aparecida de Goiânia          | 2743 Sit Av.                      | 513128 684681 3258  | 474  |
| 70 | Sydney Howell       | ipsum@aol.htb                            | India              | 248233      | Badajoz                       | 748-1092 Eleifend Rd.             | 554 53448 96271 438 | 545  |
| 71 | Evangeline Clay     | eget.mollis@yahoo.htb                    | South Korea        | UI1 3ZW     | Novgorod                      | 869-8279 Suscipit Road            | 402400 718176 9388  | 298  |
| 72 | Drake Ashley        | vitae@yahoo.htb                          | France             | 858797      | Smolensk                      | Ap #511-3737 Semper. Avenue       | 448545 6695644268   | 742  |
| 73 | Yolanda English     | quisque@yahoo.htb                        | Mexico             | 86716       | Tehuacán                      | Ap #702-5601 Cras Avenue          | 4716 8524 8686 4373 | 143  |
| 74 | India Good          | urna.nunc.quis@protonmail.htb            | Netherlands        | 38450-22965 | Bama                          | Ap #858-7292 Porttitor St.        | 453255 425477 5888  | 520  |
| 75 | Brendan Humphrey    | pellentesque.habitant@yahoo.htb          | India              | 866588      | Altach                        | Ap #138-1109 A St.                | 492997 473978 8812  | 741  |
| 76 | Kevyn Yates         | orci.luctus@yahoo.htb                    | Australia          | 524249      | Khyber Agency                 | P.O. Box 841, 3533 Lorem Rd.      | 471 65346 26667 946 | 978  |
| 77 | Brenden Ferrell     | dolor@yahoo.htb                          | Mexico             | 5575        | Banjarbaru                    | 589 Dolor Av.                     | 491689 737379 9388  | 822  |
| 78 | Medge Tanner        | sed.et@icloud.htb                        | Ireland            | 8461        | Nicoya                        | Ap #583-362 Lorem, St.            | 471 68228 18655 245 | 582  |
| 79 | Petra Maxwell       | vulputate.nisi@hotmail.htb               | Pakistan           | 6271        | Kraków                        | P.O. Box 768, 7395 Magna. Avenue  | 4485146832731       | 293  |
| 80 | Nayda White         | ante.lectus@protonmail.htb               | United Kingdom     | 871677      | Ludvika                       | Ap #394-8994 Blandit Ave          | 485255 2336622492   | 945  |
| 81 | Leroy Moore         | nunc@outlook.htb                         | India              | 110602      | Abaetetuba                    | 477-6650 Turpis Av.               | 4916 324 58 9271    | 311  |
| 82 | Fleur M.htbll       | libero@aol.htb                           | New Zealand        | 4444        | Ulsan                         | Ap #256-7097 Dapibus St.          | 5345 9936 4195 4680 | 744  |
| 83 | Hanna Finch         | cursus.integer@outlook.htb               | United States      | 48968       | Arequipa                      | Ap #758-5939 Gravida Avenue       | 4024 0071 9785 2228 | 306  |
| 84 | Myles Koch          | ligula@protonmail.htb                    | Russian Federation | 81636       | Hereford                      | 356-6096 Pede. Ave                | 534315 715275 8847  | 831  |
| 85 | Hashim Waters       | aenean.euismod.mauris@aol.htb            | India              | 96531-615   | Pondicherry                   | P.O. Box 562, 6205 Et Road        | 402400 7126848131   | 936  |
| 86 | Quinn Salinas       | mi.lacinia.mattis@google.htb             | United States      | A7L 2H9     | Hudson Bay                    | 6417 Eget Street                  | 5487 6745 5153 1985 | 431  |
| 87 | Karly Wright        | tempor.diam@icloud.htb                   | Belgium            | 05122       | Kielce                        | 871-224 Ut Street                 | 513239 182594 9922  | 196  |
| 88 | Otto Lang           | ultrices@google.htb                      | France             | 76733-267   | Belfast                       | 4708 Auctor Rd.                   | 5322224628183391    | 595  |
| 89 | Hannah Mullen       | donec.tempus.lorem@hotmail.htb           | Peru               | 52018       | Mount Gambier                 | Ap #918-5986 Egestas Avenue       | 526114 931428 6484  | 599  |
| 90 | Keefe Farmer        | eleifend.egestas.sed@outlook.htb         | Austria            | 314247      | Bhatinda                      | Ap #176-4321 Metus. Rd.           | 558717 273482 2453  | 976  |
| 91 | Rylee Walton        | lobortis.tellus.justo@yahoo.htb          | Brazil             | 161682      | Morelia                       | P.O. Box 340, 8204 Diam. Ave      | 5561 8537 7945 1635 | 143  |
| 92 | Quemby Owens        | cursus.et@google.htb                     | Peru               | 72447-13788 | Port Blair                    | Ap #923-4694 Pellentesque Avenue  | 545342 8473632383   | 341  |
| 93 | Barrett Becker      | ante@hotmail.htb                         | Spain              | 53568-22888 | Tierra Amarilla               | 785-8439 Tristique St.            | 471 67388 99195 366 | 463  |
| 94 | Maia Becker         | aenean@icloud.htb                        | Germany            | 34254       | Kano                          | Ap #156-3599 Congue. St.          | 4539394362289883    | 478  |
| 95 | Lisandra Mcknight   | eget@aol.htb                             | Colombia           | 67856       | Väners.htb                    | Ap #341-9804 Donec St.            | 547182 782221 4629  | 212  |
| 96 | Sade Baker          | ipsum.suspendisse@protonmail.htb         | Costa R.htb        | 87786       | Lloydminster                  | 236 Nec St.                       | 455665 3477829976   | 257  |
| 97 | August Hubbard      | metus.vitae.velit@yahoo.htb              | Brazil             | 32544-18823 | Mataram                       | Ap #990-9767 Varius Road          | 555667 2237542554   | 909  |
| 98 | Kalia England       | in.scelerisque.scelerisque@outlook.htb   | Costa R.htb        | 513554      | Saint-Malo                    | 483-4213 Lacus, Rd.               | 5282574593582235    | 939  |
| 99 | Tobias Whitney      | nulla.cras.eu@outlook.htb                | Spain              | 3511        | Municipal District            | Ap #382-4871 Vel, Avenue          | 492 95773 27461 179 | 919  |
+----+---------------------+------------------------------------------+--------------------+-------------+-------------------------------+-----------------------------------+---------------------+------+
99 rows in set (0.054 sec)

MySQL [customers]> [20Gselect * from myTable;[21Ghow tables;[20Guse customers[20Gshow databases;[35G[35G[20Guse customers[20Gshow tables;[21Gelect * from myTable;[20G[20G[20Gshow tables;[31G[30G[29G[28G[27G[26G[25Gcolumns from My[39G[38GmyTable;
+-----------+--------------------+------+-----+---------+----------------+
| Field     | Type               | Null | Key | Default | Extra          |
+-----------+--------------------+------+-----+---------+----------------+
| id        | mediumint unsigned | NO   | PRI | NULL    | auto_increment |
| name      | varchar(255)       | YES  |     | NULL    |                |
| email     | varchar(255)       | YES  |     | NULL    |                |
| country   | varchar(100)       | YES  |     | NULL    |                |
| postalZip | varchar(20)        | YES  |     | NULL    |                |
| city      | varchar(255)       | YES  |     | NULL    |                |
| address   | varchar(255)       | YES  |     | NULL    |                |
| pan       | varchar(255)       | YES  |     | NULL    |                |
| cvv       | varchar(255)       | YES  |     | NULL    |                |
+-----------+--------------------+------+-----+---------+----------------+
9 rows in set (0.054 sec)

MySQL [customers]> sh[21G[20Gselect * from myYa[37G[36GTable where name = "Otto Lang";
+----+-----------+---------------------+---------+-----------+---------+-----------------+------------------+------+
| id | name      | email               | country | postalZip | city    | address         | pan              | cvv  |
+----+-----------+---------------------+---------+-----------+---------+-----------------+------------------+------+
| 88 | Otto Lang | ultrices@google.htb | France  | 76733-267 | Belfast | 4708 Auctor Rd. | 5322224628183391 | 595  |
+----+-----------+---------------------+---------+-----------+---------+-----------------+------------------+------+
1 row in set (0.050 sec)

MySQL [customers]> ^DBye
                                                                                                                                                                                                                                            
[J┌──(kali㉿kali)-[~]
└─$ [?1h=[?2004h