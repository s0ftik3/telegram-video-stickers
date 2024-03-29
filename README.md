# Видеостикеры Telegram

<div align="center">
    <a href="https://telegram.org/blog/video-stickers-better-reactions">
        <img src="./preview.gif" alt="preview">
    </a>
</div>

## Навигация

-   [Вступление](#вступление)
-   [Требования](#требования)
-   [Создание .WEBM видеофайла](#создание-.WEBM-видеофайла)
    -   [Adobe Media Encoder](#adobe-media-encoder)
    -   [Handbrake](#handbrake)
    -   [ffmpeg](#ffmpeg)
        -   [Установка](#установка)
        -   [Команды](#команды)
    -   [Telegram боты](#telegram-боты)
-   [Создание набора видеостикеров](#создание-набора-видеостикеров)
-   [Заключение](#заключение)

## Вступление

В этой статье подробно описано, как создать видеостикер для Telegram. видеостикеры основаны на .WEBM формате, который совместим со множеством графических редакторов для создания изображений с высокой детализацией. Поддержка такого вида стикеров начинается с версии Telegram 8.5 и выше.

## Требования

Для того, чтобы [@Stickers](https://t.me/stickers) принял Ваш стикер, он должен соответствовать некоторым стандартам, которые были описаны Telegram [здесь](https://core.telegram.org/stickers#video-stickers). Там же Вы найдёте и другую информацию, связанную со стикерами в целом.

Немного о стандарте, который требует Telegram:

-   Одна из сторон видео должна быть строго 512 пикселей — другая же сторона может быть и меньше.
-   Длительность видео не должна привышать 3-х секунд.
-   Количество кадров в секунду не должно привышать отметку в 30 FPS.
-   Лучше использовать зацикленное видео.
-   Размер видео не должен привышать 256 КБ.
-   Видео должно быть в формате .WEBM, с использованием VP9 кодека.
-   Видео не должно содержать аудиодорожку.

## Создание .WEBM видеофайла

Итак, на данный момент существует несколько способов создания видеофайла такого формата. Здесь я опишу только те способы, который известны лично мне. Если Вы знаете какой-то ещё, дополняйте эту статью через PR.

### Adobe Media Encoder

(Далее перевод [этой страницы](https://core.telegram.org/stickers/webm-vp9-encoding#encoding-with-adobe-media-encoder))

Для корректной работы Adobe Media Encoder, требуется установить плагин для поддержки кодирования видео в формате .WEBM. Модифицированная версия плагина от [fnord software](https://github.com/fnordware/AdobeWebM) поможет Вам в кодировании Ваших видеостикеров с помощью Media Encoder.

-   [Windows WEBM плагин](https://core.telegram.org/file/464001139/fd54/udyaRyjzBQ0.837957.zip/cd1e72526a65d383e5)\
    Установочный путь\
    `C:\Program Files\Adobe\Common\Plug-ins\7.0\MediaCore`

-   [macOS WEBM плагин (M1 и Intel)](https://core.telegram.org/file/464001958/101cc/d7q2KrY6DDU.1628141.zip/15bbe083289d292ce6)\
    Установочный путь\
    `~/Library/Application Support/Adobe/Common/Plug-ins/7.0/MediaCore`

После установки плагина, формат .WEBM появится в списке форматов во вкладке "Очередь".

На macOS, Вам возможно потребуется открыть Настройки > Защита и безопасность, чтобы подтвердить установку.

### Handbrake

Handbrake — это приложение, которое может конвертировать Ваш видеофайл в другой формат.

-   [Скачать Handbrake для Windows, macOS или Linux](https://handbrake.fr/downloads.php)

После установки (Windows) импортируйте Ваш видеофайл следуя инструкциям. Обрежьте видео до 3-ех секунд и поставьте VP9 кодек. Если Ваше видео не соответствует размеру 512 на 512 пикселей, то Вам следует сначала его обрезать. Более подробный гайд по этой программе будет чуть позже.

### FFmpeg

FFmpeg — это утилита, с помощью которой можно легко конвертировать аудио- и видеофайлы в нужный Вам формат. Вообще, эта утилита может много чего, но нам не понадобиться весь её спектр возможностей.

#### Установка.

Открываем [эту ссылку](https://ffmpeg.org/download.html) и скачиваем нужную Вам версию. В моём случае — версия для Windows (далее всё будет про установку на Windows. Если у Вас macOS или другая операционная система, и Вы можете составить установочный гайд — прошу во вкладку для PR).

<details>
    <summary>Открыть скриншот</summary>
    <a href="https://ffmpeg.org/download.html"><img src="./images/ffmpeg-1.png" alt="ffmpeg"></a>
</details>

<br>

В открывшемся окне выбираем ссылку, которая показана на скриншоте ниже (должна содержать `full`).

<details>
    <summary>Открыть скриншот</summary>
    <a href="https://ffmpeg.org/download.html"><img src="./images/ffmpeg-2.png" alt="ffmpeg"></a>
</details>

<br>

Далее загруженный архив распаковываем в папку, даём ей имя FFmpeg, чтобы не запутаться. Переносим эту папку в корень диска C (или любой другой литерал, диск должен быть тот, на который Вы устанавливали Windows).

<details>
    <summary>Открыть скриншот</summary>
    <a href="https://ffmpeg.org/download.html"><img src="./images/ffmpeg-3.png" alt="ffmpeg"></a>
</details>

<br>

Затем открываем поиск (кнопка Windows + S) и вводим `Изменение системных переменных среды`.

<details>
    <summary>Открыть скриншот</summary>
    <a href="https://ffmpeg.org/download.html"><img src="./images/ffmpeg-4.png" alt="ffmpeg"></a>
</details>

<br>

В открывшемся окне нажимаем на кнопку `Переменные среды`.

<details>
    <summary>Открыть скриншот</summary>
    <a href="https://ffmpeg.org/download.html"><img src="./images/ffmpeg-5.png" alt="ffmpeg"></a>
</details>

<br>

Находим переменную `path`, жмём на неё и изменяем.

<details>
    <summary>Открыть скриншот</summary>
    <a href="https://ffmpeg.org/download.html"><img src="./images/ffmpeg-6.png" alt="ffmpeg"></a>
</details>

<br>

В пустой ячейке вписываем путь к FFmpeg. Не забываем указать, что путь должен быть к папке bin внутри FFmpeg.

<details>
    <summary>Открыть скриншот</summary>
    <a href="https://ffmpeg.org/download.html"><img src="./images/ffmpeg-7.png" alt="ffmpeg"></a>
</details>

<br>

Сохраняем всё и прожимаем "Ок".

Далее проверяем, корректно ли мы всё сделали. Открываем командную строку (`кнопка Windows + R`, вписываем `cmd`, жмём `ОК`). Пишем следующую команду: `ffmpeg -version`. Если ответ похож на тот, что показан ниже — Вы сделали всё правильно.

<details>
    <summary>Открыть скриншот</summary>
    <a href="https://ffmpeg.org/download.html"><img src="./images/ffmpeg-8.png" alt="ffmpeg"></a>
</details>

#### Команды.

А как конвертировать то в .WEBM? Ниже список команд с их описанием. Всё что Вам нужно — это путь к Вашему исходному файлу. Т. е. например, у меня есть видеофайл под названием input.mp4 на рабочем столе и я хочу конвертировать его в WEBM. Команды основаны на этом случае, поэтому там везде как входной файл указан input.mp4 (у Вас это может быть и C:/Users/User/.../input.mp4 и т. д.). И ещё, так как я перешёл в папку рабочего стола, я не пишу полный путь до файла. Чтобы перейти в папку рабочего стола через терминал, введите следующую команду `cd Desktop`.

1. Обрезает картинку до минимально возможного квадрата 512 на 512 пикселей.

```bash
ffmpeg -i input.mp4 -c:v libvpx-vp9 -pix_fmt yuva420p -b:a 256k -c:a libopus -t 2.99 -vf crop=w='min(iw\,ih)':h='min(iw\,ih)',scale=512:512,setsar=1 -an output.webm
```

<details>
    <summary>Открыть скриншот</summary>
    <a href="https://ffmpeg.org/download.html"><img src="./images/ffmpeg-9.png" alt="ffmpeg"></a>
</details>

<br>

<div align="center">
    <a href="https://ffmpeg.org/download.html">
        <img src="./images/ffmpeg-command-1.png" alt="ffmpeg">
    </a>
</div>

2. Полностью помещает картинку в масштабе 512 на 512 пикселей.

```bash
ffmpeg -i input.mp4 -c:v libvpx-vp9 -pix_fmt yuva420p -b:a 256k -c:a libopus -t 2.99 -vf scale=512:512:force_original_aspect_ratio=decrease -an output.webm
```

<div align="center">
    <a href="https://ffmpeg.org/download.html">
        <img src="./images/ffmpeg-command-2.png" alt="ffmpeg">
    </a>
</div>

3. Сжимает картинку в масштабе 512 на 512 пикселей.

```bash
ffmpeg -i input.mp4 -c:v libvpx-vp9 -pix_fmt yuva420p -b:a 256k -c:a libopus -t 2.99 -vf scale=512:512,setsar=1 -an output.webm
```

<div align="center">
    <a href="https://ffmpeg.org/download.html">
        <img src="./images/ffmpeg-command-3.png" alt="ffmpeg">
    </a>
</div>

Результат будет сохранён в той директории, в которой Вы находитесь в терминале (если, конечно, Вы ручками сами не впишите путь до output.webm).

### Telegram боты

Есть и более простой способ, однако не всегда он является самым лучшим. Работа ffmpeg довольно требовательная вещь, поэтому у большинства ботов есть лимиты в использовании, да и не все они будут Вам моментально отвечать из-за высокого спроса. В любом случае, попробовать можете.

Вот список ботов, которых я знаю и пробовал на данный момент:

-   [@toWebmBot](https://t.me/toWebmBot) — мой бот, конвертирует Ваше видео в видеостикер и автоматически создаёт стикер-пак, добавляя его туда.
-   [@fStikBot](https://t.me/fStikBot) — многофункциональный бот, также умеет конвертировать в видеостикер. Больше опций по управлению Вашими стикер-паками.
-   [@converterSticker_bot](https://t.me/converterSticker_bot) — конвертирует Ваше видео в файл .WEBM
-   [@VideoToStickerBot](https://t.me/VideoToStickerBot) — также создаёт стикер пак. Есть возможность выбрать начало и конец Вашего видеостикера, если Вы используете длинное видео.
-   [@AnimatedStickersRoBot](https://t.me/AnimatedStickersRoBot) — конвертирует в видеостикер, создаёт стикер-пак.
-   [@VideoStickerXBot](https://t.me/VideoStickerXBot) — конвертирует в видеостикер, создаёт стикер-пак, есть возможность извлечь .WEBM в виде документа.

# Создание набора видеостикеров

Если Вам всё-таки удалось конвертировать нужный видеофайл в .WEBM со всеми обязательными параметрами, или же у Вас уже был таковой файл, Вам нужно создать набор стикеров. Для этого запустите официального бота [@Stickers](https://t.me/stickers) и отправьте ему команду `/newvideo`. Далее проследуйте инструкциям, которые Вам будет присылать бот. По-сути, Вам просто нужно будет дать название набору, его короткую ссылку, добавить туда нужные .WEBM файлы и сохранить.

<div align="center">
    <a href="https://t.me/stickers">
        <img src="./images/stickers-bot.png" alt="stickers-bot">
    </a>
</div>

# Заключение

Статья будет пополняться. Если Вы хотите помочь — создавайте PR с Вашими дополнениями. Если хотите добавить бота в список — также создавайте PR. Для связи со мной — [@vychs](https://t.me/vychs).
