Это репозиторий для разных типс и трикс. небольшие рецепты, такие как ховер эффекты, тренировка по флексам и т.п.

<h2>Новый поддомен</h2>

Для этого создан отдельный поддомен <a href="http://recipes.birlink.click/">recipes.birlink.click</a>

1. Создал новый поддомен в разделе "Управление доменами и поддоменами". Домен никуда не направил.
2. В панели Хестия добавил домен с тем же названием.
3. На стороне Бегета пришлось подправить нс записи, поскольку он не был никуда прилинкован. Будем ждать, когда изменения вступят в силу.
4. Добавил ссл и включил редирект на хттпс. Поддомен работает.

<h2>Синхронизация редактора с сайтом</h2>

1. Создал фтп по пути "remote_path": "/"
2. Установил для Саблайм Sftp, настройки открываются через файл - сфтп - сетап сервер, но открываются как неизвестный файл. нужно сохранить как sftp-config.json
	2.1 минимальные настройки
	 <code>
	 "type": "ftp",
    "sync_down_on_open": true,
    "sync_same_age": true,
    "host": "example.com",
    "user": "username",
    "password": "password",
    "remote_path": "/",
	</code>
3. Процесс не может получить доступ к файлу, так как этот файл занят другим процессом: 
	3.1 на Хестия поменял remote_path": "/" на remote_path": "/public_html".
	Чтобы изменения вступили в силу, нужно повторно запустить файл-сфтп-брауз серверс и выбрать файл джсон-конфиг
	3.2 в джсоне тоже нужно вместо / прописать /public_html. странно, в ВСкод нужно было вписать просто /, поскольку папка паблик хтмл уже указан.
4. удается подключиться к серверу, но работать возможно только с сервером. Просматривать файлы, уталять и т.д.
5. Оказывается, надо было настроить сфтп не через глобально файл - сфтп, а нажать правую кнопку на нужную папку в сайдбаре и настроить сфтп для этой папки/сайта
	5.1 перенастроил сфтп, для конкретного поддомена, также включил аплоад он сейв. будем проверять
	5.2. ошибка failure (Disconnected - possible PASV mode error, try setting ftp_passive_mode to false in sftp-config.json)
	расскомментировал пассив мод в настройках, теперь все работает, отправляется на сервер
	время проверить на примере файла Индекс.хтмл
6. залил файл индекса, но на сервере не открывается. ошибка 403. Вчера такое уже было
	6.1 проверил через файл-менеджер, файл индекса не передался на сервер.
	получается, папка сайта синхронизируется, но ничего не передается.
	6.2 оказалось, нечему было передаваться, поскольку индекс.хтмл был создан до настройки сфтп, а файлы загружаются при сохрании. внес правки в индекс, сохранил, все улетело и работает.

todo: очистить редми, убрать ошибки и оставить только рабочую инструкцию


# recipes