description: Установка необходимых программ, которые необходимы для разработки Minecraft модов.

# Установка программ

Minecraft написана на языке [Java](https://ru.wikipedia.org/wiki/Java). Программы на этом языке могут выполняться только если у вас установлена виртуальная машина Java.

## Java Development Kit

Для запуска Minecraft необходима лишь среда выполнения Java (JRE).

Но для разработки собственных модов нам потребуется писать программный код и пользоваться разными инструментами. Это не входит в стандартный Java пакет,
поэтому нам нужно установить JDK (Набор инструментов разработчика Java).

!!! note ""
    **Minecraft 1.7.10** работает только с **Java 8** (1.8). Более новые выпуски Java данной версией игры не поддерживаются.

Скачайте [последнюю версию Oracle JDK](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) и следуйте инструкциям по установке. Ничего в настройках установки менять не надо.

??? warning "Принятые ограничения корпорацией Oracle"
    * **С апреля 2019 г.** для скачивания файлов нужна регистрация на сайте. Это бесплатно и подтверждать ничего, кроме E-mail не потребуется.
    * **С марта 2022 г.** скачивание файлов недоступно для пользователей из РФ. 
      Потребуется использовать прокси/VPN. При регистрации следует указывать любую другую страну и использовать иностранный почтовый сервис (напр. GMail, Outlook).

!!! success "Альтернативная JDK"
    В качестве альтернативы можно использовать JDK от другого производителя, например BellSoft.
    Здесь не придётся регистрироваться и искать обходные пути.
    **[Скачать Liberica JDK](https://bell-sw.com/pages/downloads/#/java-8-lts)**


## Forge для пользователей

Чтобы люди смогли играть с вашим модом, на их Minecraft должен быть установлен загрузчик модов MinecraftForge.

Скачайте установщик (Installer) с [официального сайта MinecraftForge](https://files.minecraftforge.net/net/minecraftforge/forge/index_1.7.10.html):

![Картинка скачивания установщика](images/download_installer.png)

Запустите скачанный файл. Выберите пункт «Install client», укажите путь к Minecraft, если он не указан и нажмите «OK».

![Картинка установщика](images/installer.png)


## Forge для разработки

!!! note ""
    Forge использует систему сборки проектов [Gradle](https://docs.gradle.org/current/userguide/what_is_gradle.html).
    Задачей систем сборки является автоматизация процессов, чтобы избавить вас от необходимости вводить множество консольных команд вручную.
    Проще говоря, Gradle делает за вас всю «грязную работу». В случае Minecraft разработки это компиляция, тестирование, обфуксация кода; упаковка всего в JAR-файл. 

### Скачивание

Скачайте набор инструментов для разработки модификаций (SRC, для новых версий MDK) с [официального сайта Forge](https://files.minecraftforge.net/net/minecraftforge/forge/index_1.7.10.html):

![Картинка скачивания MDK](images/download_mdk.png)

Создайте в любом удобном для вас месте папку и распакуйте туда скачанный архив. Вы увидите много файлов.
Не все из них вам нужны. Чтобы не захламлять рабочее пространство, удалите все файлы, кроме:

* **build.gradle** – Главный файл конфигурации проекта. Описывает процесс сборки проекта.
* **gradlew** и **gradlew.bat** – Скрипты запуска [Gradle Wrapper](https://docs.gradle.org/current/userguide/gradle_wrapper.html).
* Папка **gradle** – Здесь располагается Gradle Wrapper.

### Предварительная настройка

Команда MinecraftForge давно прекратила поддержку версии **Minecraft 1.7.10**.
Нам потребуется внести несколько небольших изменений в конфигурационные файлы скачанного проекта, исправляющие проблемы совместимости с актуальными версиями ПО.

1. **Используется слишком старая версия Gradle.**   
   Отредактируйте файл **gradle/wrapper/gradle-wrapper.properties**.
   Найдите следующую строку URL и замените `2.0` на `4.4.1`
   ```properties
   distributionUrl=https\://services.gradle.org/distributions/gradle-2.0-bin.zip
   ```
2. **Изменился URL репозитория Forge.**   
   Откройте файл **build.gradle** и самом начале замените строку `http://files.minecraftforge.net/maven` на `https://maven.minecraftforge.net/`
3. **Активируем поддержку Java 8 (опционально)**   
   В файле **build.gradle** добавьте после `archivesBaseName = "modid"` строку:
   ```groovy
   targetCompatibility = sourceCompatibility = JavaVersion.VERSION_1_8
   ```
4. **Активируем поддержку Unicode (опционально)**   
   Чтобы кириллица в исходных файлах не превращалась в «кракозябры» после сборки, в файле **build.gradle**  после блока `minecraft { ... }` добавьте ниже:
   ```groovy
   tasks.withType(JavaCompile) {
       options.encoding = 'UTF-8'
   }
   ```

## Инициализация ForgeGradle

Теперь мы можем инициализировать среду разработки, чтобы ForgeGradle подготовил необходимые файлы для нас.
Для этого выполните следующую команду в командной строке (терминале). Вариант отличается в зависимости от ОС и используемой оболочки.

```shell
# Windows (CMD)
gradlew setupDecompWorkspace
# Windows (PowerShell)
.\gradlew setupDecompWorkspace
# Linux / MacOS
./gradlew setupDecompWorkspace
```

Подготовка займёт несколько минут в зависимости от производительности вашего компьютера и скорости интернета.
По завершении вы должны увидеть сообщение «BUILD SUCCESSFUL».

!!! warning "Важно"
    Команду надо выполнять находясь в каталоге проекта, иначе получите ошибку «Неизвестная команда/файл».   
    В случае ОС Windows, откройте командную строку с помощью ++shift+"ПКМ"++ в свободной области окна проводника с файлами проекта, выбрав соответствующий пункт меню.

??? question "Как задать переменную JAVA_HOME?"
    При работе с Gradle из командной строки (терминала) требуется указание пути к JDK с помощью переменной окружения **JAVA_HOME**.
    Временно задать путь для текущего сеанса можно следующей командой в зависимости от ОС и оболочки.

    ```shell
    # Windows (CMD)
    SET JAVA_HOME="C:\Program Files\Java\jdk1.8.0_341"
    # Windows (PowerShell)
    $env:JAVA_HOME = "C:\Program Files\Java\jdk1.8.0_341"
    # Linux / MacOS
    export JAVA_HOME = '/usr/lib/jvm/jdk1.8.0_341'
    ```

    Не забудьте изменить путь к JDK на актуальный. И не закрывайте окно терминала - все остальные команды Gradle нужно вводить в этом же окне.

!!! info "Информация"
    Настройка среды ForgeGradle производится всего один раз на ПК.
    Вам не потребуется повторно вводить команду для остальных проектов, разрабатываемых на той же версии Forge и Minecraft (версия указывается в **build.gradle** в `minecraft.version`).

## Среда разработки (IDE)

Моды можно писать и в блокноте, но это очень неудобно. Нам нужна специализированная программа, которая
умеет подсвечивать код, выполнять авто-импорт и делать много других полезных вещей.

Наиболее популярными IDE на данный момент являются [Eclipse](https://www.eclipse.org/downloads/) и [IntelliJ IDEA](https://www.jetbrains.com/idea/download/).

Eclipse бесплатен. У IDEA есть бесплатная Community версия. Мы рекомендуем использовать IDEA, чтобы избежать большинства проблем при написании модификации.
Никаких платных функций в этом учебнике нам не потребуется. Выберите наиболее подходящую для вас IDE, основываясь на характеристиках вашего компьютера.