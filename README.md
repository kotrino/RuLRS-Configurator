# ExpressLRS Configurator

[! [Выпуск] ()] (https://github.com/kotrino/RuLRS-Configurator/releases)
[! [Лицензия] ()] (https://github.com/kotrino/RuLRS-Configurator/blob/main/LICENSE)
<!--[! [CHAT]
[! [Открытые коллективные покровители]
-->
CompressLRS Configurator-это кроссплатформенное приложение для сборки и настройки прошивок
[RuLRS] (https://github.com/kotrino/RuLRS-Configurator/), - полностью открытой RC-системы.

<!--
## нужна помощь?Смущенный?Присоединяйтесь к сообществу!

- [Discord Chat] ()
- [Группа Facebook] ()
- [документация] ()
-->
<!--
## Поддержка Rulrs

Поддержка RuLRS так же просто, как и внести функцию, либо код, либо просто идея.
Кодировать не ваше?
Тестирование запроса на вытягивание с использованием удобной вкладки конфигуратора
и предоставления обратной связи также очень важно.
Все работают вместе.

Если у вас нет возможности внести вклад в разработку, рассмотрите возможность сделать небольшое пожертвование.
Они используются для приобретения тестового оборудования, лицензий на ПО и сертификатов, необходимых для дальнейшего
развития проекта и поддержания его надёжности. RuLRS принимает пожертвования через //ссылку//, обеспечивая
прозрачность и благодарность всем спонсорам.
-->

## Краткое руководство

Если вы хотите прошить имеющееся оборудование, пожалуйста, ознакомьтесь с руководствами [веб -сайт] (https://www.expresslrs.org/),
и [FAQ] (https://www.expresslrs.org/3.0/faq/)

## Установка

Мы предлагаем готовые сборки для 64-битных версий Windows, Linux и macOS.

Скачайте нужный установщик со страницы [RELEASES] (https://github.com/kotrino/RuLRS-Configurator/releases).

### Примечания

#### Windows

Минимально поддерживаемая версия — **Windows 8**.

#### macOS

Изменения в политике безопасности в macOS 10.14 (Mojave) и 10.15 (Catalina) приводят к тому, что при попытке открыть приложение
может возникнуть сообщение вида:

>`"RuLRS Configurator.app" не может быть открыт, так как разработчик не может быть проверен.`Чтобы обойти это, кликните правой кнопкой мыши по`RuLRS Configurator.app`, удерживая клавишу`Control`, а затем выберите пункт`Open`.
В появившемся окне подтверждения вы сможете запустить приложение (возможно, придётся повторить действие дважды).


Альтернативный способ — выполнить в терминале команду:
```bash
sudo xattr -rd com.apple.quarantine /Applications/ExpressLRS\ Configurator.app
```
#### linux

Пользователям Linux необходимо установить правила **udev** для корректной работы с платформенными платами и устройствами.
Актуальная версия правил доступна по адресу:
[https://raw.githubusercontent.com/platformio/platformio-core/master/platformio/assets/system/99-platformio-udev.rules](https://raw.githubusercontent.com/platformio/platformio-core/master/platformio/assets/system/99-platformio-udev.rules)


Скачанный файл следует разместить в директории`/etc/udev/rules.d/99-platformio-udev.rules`(предпочтительно)
или`/lib/udev/rules.d/99-platformio-udev.rules`(если в вашей системе возникнут проблемы).

Откройте терминал и выполните:
```bash
# Рекомендуемый способ
curl -fsSL https://raw.githubusercontent.com/platformio/platformio-core/master/platformio/assets/system/99-platformio-udev.rules \
  | sudo tee /etc/udev/rules.d/99-platformio-udev.rules

# Или скачайте файл вручную и скопируйте его:
sudo cp 99-platformio-udev.rules /etc/udev/rules.d/99-platformio-udev.rules
```
Перезапустите службу udev:
```bash
sudo service udev restart
# или
sudo udevadm control --reload-rules
sudo udevadm trigger
```
Если вы используете Ubuntu/Debian и работаете не под root, возможно, понадобится добавить имя пользователя в группу dialout:
```bash
sudo usermod -a -G dialout $USER
sudo usermod -a -G plugdev $USER
```Для Arch-подобных систем может потребоваться добавить пользователя в группу uucp (а иногда и в lock):```bash
sudo usermod -a -G uucp $USER
sudo usermod -a -G lock $USER
```
##### Устранение неполадок на Ubuntu 18.xx / старых версиях Debian

В Ubuntu 18.xx недоступна новая версия Git по умолчанию, а некоторые системные библиотеки могут отсутствовать.

Подробности смотрите в [Выпуск № 26] (https://github.com/expresslrs/expresslrs-configurator/issues/26).

В качестве обходного решения вручную установите необходимые пакеты:```bash
# install missing sys packages
sudo apt update
sudo apt-get install gconf2 gconf-service python3-distutils

# install git version >= 2.25
sudo add-apt-repository ppa:git-core/ppa
sudo apt update
sudo apt install git
```
<!--
## Локализация

** Пожалуйста, не отправляйте PR только с изменениями перевода; сначала прочтите и следуйте инструкциям ниже! **

RuLRS Configurator переведён на несколько языков.
Приложение определяет язык системы и пытается использовать соответствующий перевод, если он доступен.

Если вы предпочитаете английский или другой язык, отличающийся от системного,
вы можете выбрать желаемый язык в разделе «Настройки».

Мы стремимся сделать RuLRS доступным для пилотов, не владеющих английским языком в достаточной мере.
У нас есть команда добровольцев-переводчиков, но любая помощь приветствуется, особенно при добавлении новых языков.
Если вы хотите помочь с переводами, у вас есть следующие варианты:

- Для правок или улучшений существующих переводов перейдите на [сайт Crowdin](https://crowdin.com/project/expresslrs-configurator) и оставьте свои предложения.
- Если вы хотите взяться за перевод нового языка или стать редактором перевода, присоединяйтесь к нашему [Discord](), канал [#configurator-translation]().
Там вам помогут настроить всё необходимое.

Наш прогресс в локализации: ![Прогресс переводов](https://badges.awesome-crowdin.com/translation-15884405-596659_update.png)
-->

## скриншоты

! [Главный экран] (docs/readme/screenshots/main_screen.jpg)

! [Результат компиляции] (docs/readme/screenshots/compile_result.jpg)

## архитектура```
 - - - - - - - - - - - - - - - - - - - -
|          RuLRS-Configurator           |
|                   |                   |
|     renderer      |        main       |
|                   |                   |
|   configurator <----->  api-server    |
|                   |          |        |
|                   |          V        |
|                   |      platformio   |
|_ _ _ _ _ _ _ _ _ _|_ _ _ _ _ | _ _ _ _|
                               V
                        RuLRS hardware
```
Это приложение на базе Electron, состоящее из двух частей: локального сервера API,
выполняющего основную работу, и пользовательского интерфейса, который взаимодействует с сервером через GraphQL.

Во всём репозитории активно используется TypeScript и пакет @graphql-codegen/cli для генерации типов и обеспечения согласованности данных между уровнями API и UI на этапе компиляции.
GraphQL гарантирует, что типы данных соответствуют реальным объектам во время исполнения.

## Начало разработки

Предварительные условия

- node >= 16,0
- git >= 2,25
- Python >= 3,6
- Platformio >= 5.0

Запуск приложения в режиме разработки:
```bash
yarn install --frozen-lockfile
yarn start
```
Для моделирования устройств Wi-Fi в вашей локальной сети вы можете начать приложение с`MULTICAST_DNS_SIMULATOR_ENABLED`переменная среды:
```
npx cross-env MULTICAST_DNS_SIMULATOR_ENABLED=true yarn start
```
## Другие полезные команды CLI

Генерация типизации (TypeScript-типов) из схемы и GraphQL-запросов, которые находятся в папке [SRC/UI/GQL/QUERIES] (src/ui/gql/queries):
```bash
yarn run gql-codegen
```
## Юридический отказ от ответственности

Использование и эксплуатация этого типа устройств может требовать лицензии в некоторых странах, а где-то и вовсе запрещено.
Окончательная ответственность за соблюдение локальных правил лежит на пользователе.
Данное программное/аппаратное обеспечение носит экспериментальный характер и не гарантирует стабильность или надёжность.
Применяйте его на свой страх и риск.

<!--
[! [Присоединяйтесь к сообществу!] (Docs/readme/cooler.png)] (https://github.com/expresslrs/expresslrs/wiki#community)
-->
Этот проект основан на [https://github.com/ExpressLRS/ExpressLRS-Configurator](https://github.com/ExpressLRS/ExpressLRS-Configurator)
