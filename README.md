# AWS-Light-Node-Documentation

# 1.Перший крок - створюємо бюджет.
## Логінимося в AWS і зверху в пошуку вписуємо “Billing and Cost Management”
![Alt text](imgs/1.png?raw=true)

## Потім натискаємо на “Billing and Cost Management” в розділі Services і вам відкриється меню “Billing and Cost Management”:
![Alt text](imgs/2.png?raw=true)

## З права в боковому меню шукаєте “Budgets” і натискаєте на нього після чого побачите наступне:
![Alt text](imgs/3.png?raw=true)

## Клікаєте на кнопку “Create a budget” і у вас появиться меню створення бюджету.
![Alt text](imgs/4.png?raw=true)

## В даному меню створення бюджету вам треба тільки змінити Budget Name (по бажанню), але саме основне це скролите вниз і шукаєте “Email recipients” - сюди вписуєте мейл на який ви хочете щоб прийшло повідомлення від AWS коли потратиться перший цент, і натискаєте кнопку “Create budget”.
![Alt text](imgs/5.png?raw=true)


## Після чого вам відкриється меню зі створеними бюджетами:
![Alt text](imgs/6.png?raw=true)

## Повторюся AWS EC2 Instance ми будемо ранити безкоштовно, одне що може бути платне це додаткові GB диску на який будуть писатися логи якщо нам не вистачить 30GB. AWS дає нам безкоштовно на цілий рік Інстанс 1 vCPU, 1GB оперативної пам’яті та 30GB ssd диск. Бюджет ми просто створюємо для підстраховки про всяк випадок.

# 2.Другий крок - створюємо EC2 Instance де буде ранитися Light Node.
## Зверху в пошуку вписуємо EC2. Натискаємо на EC2 в розділі Services і нас перекине в EC2 Dashboard.
![Alt text](imgs/7.png?raw=true)

## У вас перший раз можливо буде трошки інше меню.
## Наступне міняємо регіон в якому будемо створювати інстанс на US N.Virginia або Europe Stockholm. Просто відкриваємо випадаючий список в верхньому меню з права і вибираємо один з двох який підкреслений червоним на скріні нижче.
## Раджу вибирати US N.Virginia.
![Alt text](imgs/8.png?raw=true)

## Пояснення чому треба міняти регіон: Максимум безкоштовного storage 30GB, ми при створенні інстансу зразу створимо диск на 30GB (як це робити буде описано нижче), потім в процесі треба заходити приблизно раз в тиждень і дивитися туди скільки на диску залишилося вільного місця, якщо підходить до 30GB його можна розшири не зупняючи ноду. Вартість одного GB на місяць в US N.Virginia = 0.08$, а в Europe Stockholm = 0.0836$. Вкладую калькулятор ціни GB залежно від регіону там є дропдаун в якому вибираєш регіон і міняється ціна, нас цікавить: General Purpose SSD (gp3) - Storage ціна. Все остальне не вийде за безкоштовне. https://aws.amazon.com/ebs/pricing/?nc1=h_ls. Можливо хтось знайде дешевший регіон якщо захоче погратися з цим. Тобто 10 додаткових GB в міс буде коштувати 80-90 центів. Але спішити поки купляти думаю не треба можливо і безкоштовних 30GB цілком вистачить.

## Наступне шукаємо кнопку “Launch instance” і натискаємо її.
![Alt text](imgs/9.png?raw=true)

## Після того як натисли на кнопку “Launch instance” вам відкриється меню створення AWS EC2 Instance:
![Alt text](imgs/10.png?raw=true)

## У цьому конструктор меню спочатку в полі Name вписуєте назву вашого інстансу, ніяких обмежень немає як його назвати, але краще англійською.
## Наступне залишаєте вже вибрану по дефолту Amazon Linux як на скріні вище  та Amazon Machine Image (AMI) теж залишаєте вибрану по дефолту Amazon Linux 2023 AMI (Free tier eligible) - саме цей імедж буде безкоштовним.

## Наступне вибираємо тип інстансу (Instance type) : t2.micro (Free tier eligible).
![Alt text](imgs/11.png?raw=true)

## Потім створюємо ключ - Key pair (login) для логіну в інстанс через термінал.
![Alt text](imgs/12.png?raw=true)
## Натискаєте на “Create new key pair”. Вам відкриється вікно створення ключа.
## Все що вам треба зробити ввести “Key pair name” - в назві ключа не повинно бути ніяких пробілів, можна заюзати андерскор “_” замість пробілів ну і порада краще англійською.
![Alt text](imgs/13.png?raw=true)

## Натискаєте “Create key pair” та зберігаєте pem файл локально краще десь в окремій папці на вашому комп’ютері.

## Далі Network settings. Тут вам треба тільки вибрати “Create security group” та відмітити чекбокси на “Allow SSH traffic from” - Anywhere, “Allow HTTPS traffic from the internet” та “Allow HTTP traffic from the internet”.
![Alt text](imgs/14.png?raw=true)

## Наступне налаштування стореджа “Configure storage”. Вам треба тільки змінити розмір стореджа замість 8 GiB як по дефолту ставимо 30 GiB.
![Alt text](imgs/15.png?raw=true)

## З правої сторони у вас буде Summary вашого інстансу і під ним кнопка “Launch instance” як на скріні зверху. Клікаєте “Launch instance” і відкриється меню в якому вам буде повідомлено що інстанс створено:
![Alt text](imgs/16.png?raw=true)

## Натискаєте на id інстансу в повідомленні виділеному зеленим кольором і вас перекине на ваш інстанс.
![Alt text](imgs/17.png?raw=true)

## Або в пошуку зверху екрана вписуєте EC2 і в розділі Services натискаєте на EC2.
![Alt text](imgs/18.png?raw=true)

## Вам відкриється EC2 Dashboard:
![Alt text](imgs/19.png?raw=true)

## Натискаєте в боковому меню на Instances або посередині вікна в розділі Resources теж можна натиснути на Instances (running). І вам відкриються ваші інстанси:
![Alt text](imgs/36.png?raw=true)

## Перевіряємо чи все вірно створилося. Виділяєте ваш інстанс і знизу відкриються деталі інстансу. Відкриваєте вкладку Security
![Alt text](imgs/20.png?raw=true)

## Inbound rules та Outbound rules у вас повинні бути одинакові як на скріні нижче, тільки Security group rule id будуть інші.
![Alt text](imgs/21.png?raw=true)

## Далі переходите на вкладку Details під інстансом, вона сама перша і копіюєте Public IPv4 address - ви будете конектитися за допомогою локального(на вашому коп’ютері) термінала до вашого AWS EC2 Instance через цю Public IPv4 address.
![Alt text](imgs/22.png?raw=true)

## Інстанс на AWS створено.

# 3. Третій крок конектимося до AWS Instance.

# 3.1 Якщо у вас mac чи лінукс:
## Відкриваєте термінал, переходити у папочку де у вас збережений ключ за допомогою команди `cd` і запускаєте команду:
`chmod 0400 your_key_pair_file.pem`
## де “your_key_pair_file.pem” це назва ключа який ви згенерували під час створення AWS EC2 Instance - у вас має бути ваша назва. Потім запускаєте команду:
`ssh -i your_key_pair_file.pem ec2-user@your_Public_IPv4_address`
## де “your_key_pair_file.pem” - назва вашого ключа та “your_Public_IPv4_address” ваш Public IPv4 address - де його взяти описано вище.
## Після цього вас може попросити в терміналі прописати yes та натиснути клавішу Enter.
## Наступний крок це запуск Light Node на AWS EC2 Instance який буде описано нижче в Четвертому кроці.

# 3.2 Якщо у Вас Windows 10 або вище.
## Скачуєте PuTTY тут: https://www.putty.org/
![Alt text](imgs/23.png?raw=true)

## Встановлюємо скачаний PuTTY
![Alt text](imgs/24.png?raw=true)

## Просто натискаємо Next > Next > Install.
## Після того як встановили йдемо в пуск і в пошуку вводимо P і там бачимо нашу програмку та відкриваємо її розташування.
![Alt text](imgs/25.png?raw=true)

## В папці відкриваємо puttygen.exe та натискаємо Load
![Alt text](imgs/26.png?raw=true)

## Вибираємо All Files і відкриваємо збережений ключ “your_key_pair_file.pem” - де “your_key_pair_file.pem” це назва ключа який ви згенерували під час створення AWS EC2 Instance - у вас має бути ваша назва.
![Alt text](imgs/27.png?raw=true)

## Після того як відкрили його натискаєм Ок > Save private key
## Даємо йому назву і зберігаєм в фоматі .ppk
![Alt text](imgs/28.png?raw=true)

## Далі йдем в нашу папку з програмою PuTTY і відкриваємо putty.exe
![Alt text](imgs/29.png?raw=true)

## Після чого в Host Name (or IP address) вписуємо “your_Public_IPv4_address” ваш Public IPv4 address - де його взяти описано вище.
![Alt text](imgs/30.png?raw=true)

## Далі вибираємо SSH > Auth > Credentials потім натискаємо Browse... і вставляємо наш ключ в форматі .ppk який ми зберігали
## Після чого натискаємо Open
![Alt text](imgs/31.png?raw=true)

## Натискаємо Accept
![Alt text](imgs/32.png?raw=true)

## Далі вводимо ec2-user і натискаємо Enter
![Alt text](imgs/33.png?raw=true)

## Після того як натиснули Enter у вас має відображатися в терміналі з’єднання з AWS EC2 Instance як на скріні нижче
![Alt text](imgs/34.png?raw=true)

## Після того як виконали всі кроки успішно то побачимо таке

## А далі робимо все що написано в 4-тому кроці.

# 4. Четвертий крок: Запуск Light Node.
## Заходимо в утилиту screen комадою:
`screen -S nubit`
## Якщо screen не встановлено:
`sudo apt install screen`, для Mac `brew install screen`
## Запускаємо Light Node:
`curl -sL1 https://nubit.sh/ | bash`
## На цьому етапі треба бути уважними: Light Node згенерує вам адрес кошелька (ADDRESS), мнемонічну фразу (MNEMONIC), PUBKEY та AUTH KEY - вони виділені червоним на скріні нижче. Раджу ОБОВ’ЯЗКОВО зберегти собі адрес кошелька (ADDRESS), мнемонічну фразу (MNEMONIC), PUBKEY та AUTH KEY кудись в безпечне місце де у вас до цього всього завжди буде доступ.
![Alt text](imgs/35.png?raw=true)

## Наступне виходимо з утиліти screen набором клавіш:
`CTRL+A, +D (для Мас: control+A+D).`

## Щоб переконатися, що вузол працює успішно, вводимо команду:
`$HOME/nubit-node/bin/nubit das sampling-stats --node.store $HOME/.nubit-light-nubit-alphatestnet-1`

## Щоб дізнатися свою адресу і pubkey, вводимо:
`$HOME/nubit-node/bin/nkey list --p2p.network nubit-alphatestnet-1 --node.type light`

## Щоб дізнатися свою мнемонічну фразу, вводимо команду:
`cat $HOME/nubit-node/mnemonic.txt`