description: Установка необходимых программ, которые необходимы для разработки Minecraft модов.

# Установка программ

Minecraft написана на языке Java. Программы на этом языке могут выполняться только если у вас установлена виртуальная машина Java.

Если вы хоть раз запускали Minecraft на данном компьютере, то Java у вас уже установлена. В противном случае, скачайте и установите [Java 8](https://java.com/ru/download/).

## JDK

Для запуска Minecraft необходима лишь среда выполнения Java, которую вы установили выше.

Но для разработки собственных модов нам потребуется писать программный код и пользоваться разными библиотеками. Это не входит в стандартный Java пакет,
поэтому нам нужно установить JDK (Java Development Kit) (Комплект инструментов для разработки на Java).

Скачайте [JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) и следуйте инструкциям по установке. Ничего в настройках установки менять не надо.

## Forge

Установка Forge для конечных пользователей вашего мода и для вас, как разработчика различается.

### Forge для пользователей

Чтобы люди смогли играть с вашим модом, на их Minecraft должен быть установлен движок Forge.

Скачайте установщик (Installer) с [официального сайта Forge](https://files.minecraftforge.net/):

![Картинка скачивания установщика](images/download_installer_1.png)

Запустите скачанный файл. Выберите пункт "Install client", укажите путь к Minecraft (если он не указан) и нажмите
OK.

![Картинка установщика](images/installer_1.png)

Как понять, куда установлен Minecraft? По умолчанию на Windows он устанавливается по следующему пути:
`C:\Users\*ПОЛЬЗОВАТЕЛЬ*\AppData\Roaming\.minecraft`, где `*ПОЛЬЗОВАТЕЛЬ*` имя текущего пользователя компьютера.
На linux:
`/home/*ПОЛЬЗОВАТЕЛЬ*/.minecraft/`, где `*ПОЛЬЗОВАТЕЛЬ*` имя текущего пользователя компьютера.

### Forge для разработки

Скачайте набор инструментов для разработки модификаций (MDK) с [официального сайта Forge](https://files.minecraftforge.net/):

![Картинка скачивания MDK](images/download_mdk_1.png)

Создайте в любом удобном для вас месте папку и распакуйте туда скачанный архив. Вы увидите много файлов.
Не все из них вам нужны. Чтобы не захламлять рабочее пространство, удалите все файлы, кроме:

* build.gradle
* gradlew.bat
* gradle
* папки src
* папки gradle

## Среда разработки

Моды можно писать и в блокноте, но это очень неудобно. Нам нужна специализированная программа, которая
умеет подсвечивать код, выполнять авто-импорт и делать много других полезных вещей.

Наиболее популярными IDE на данный момент являются [Eclipse](https://www.eclipse.org/downloads/) и [Intellij Idea](https://www.jetbrains.com/idea/#chooseYourEdition).

Обе среды бесплатны, но у Intellij Idea есть платная версия. Никаких платных функций в этом учебнике нам
не потребуется.

Достаточно часто моды пишут на Eclipse, так как и сам Minecraft был написан с помощью этой IDE.
С другой стороны, Eclipse выглядит немного устаревше, а Intellij пофункциональнее.

Выбирайте то, что нравится вам.