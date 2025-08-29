# Установка Visual Studio 6.0 в Windows 10

*Сокращённый перевод статьи [Kirk Stowell](https://www.codeproject.com/script/Membership/View.aspx?mid=126). [Install Visual Studio 6.0 on Windows 10](https://www.codeproject.com/Articles/1191047/Install-Visual-Studio-on-Windows)*

Эта статья представляет собой пошаговый процесс установки `Visual Studio 6.0` в `Windows 10`. Здесь говорится о `Visual Studio Enterprise`, однако такой же подход должен работать и с версией `Professional`. В статье показано, как убрать следы прошлых неудачных попыток и какие настройки отключить в мастере установки.

## Зачистка прошлых попыток

### Удаление папок установки

Вам надо удалить папки, созданные в ходе прошлых неудачных попыток. Обычно они находятся в `C:\Program Files (x86)`
*Примечание. Если у вас установлена новая студия, например 2017, не трогайте папку `C:\Program Files (x86)\Microsoft Visual Studio\2017`.*

- `C:\Program Files (x86)\Microsoft Visual Studio\Common`
- `C:\Program Files (x86)\Microsoft Visual Studio\MSDN`
- `C:\Program Files (x86)\Microsoft Visual Studio\MSDN98`
- `C:\Program Files (x86)\Microsoft Visual Studio\VB98`
- `C:\Program Files (x86)\Microsoft Visual Studio\VC98`
- `C:\Program Files (x86)\Microsoft Visual Studio\*.HTM`
- `C:\Program Files (x86)\Microsoft Visual Studio\*.TXT`
- `C:\Program Files (x86)\Common Files\Microsoft Shared\MSDesigners98`
- `C:\Program Files (x86)\Common Files\Microsoft Shared\MSDN`
- `C:\Program Files (x86)\Common Files\Microsoft Shared\VS98`
- `C:\Program Files (x86)\Common Files\Microsoft Shared\Wizards98`

### Удаление разделов реестра

- `HKEY_LOCAL_MACHINE\Software\Microsoft\DevStudio`
- `HKEY_LOCAL_MACHINE\Software\Microsoft\HTML Help Collections`
- `HKEY_LOCAL_MACHINE\Software\Microsoft\MSVSDG`
- `HKEY_LOCAL_MACHINE\Software\Microsoft\Visual Basic\6.0`
- `HKEY_LOCAL_MACHINE\Software\Microsoft\Visual Component Manager`
- `HKEY_LOCAL_MACHINE\Software\Microsoft\Visual Modeler`
- `HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\6.0`
- `HKEY_LOCAL_MACHINE\Software\Wow6432Node\Microsoft\DevStudio`
- `HKEY_LOCAL_MACHINE\Software\Wow6432Node\Microsoft\HTML Help Collections`
- `HKEY_LOCAL_MACHINE\Software\Wow6432Node\Microsoft\MSVSDG`
- `HKEY_LOCAL_MACHINE\Software\Wow6432Node\Microsoft\Visual Basic\6.0`
- `HKEY_LOCAL_MACHINE\Software\Wow6432Node\Microsoft\Visual Component Manager`
- `HKEY_LOCAL_MACHINE\Software\Wow6432Node\Microsoft\Visual Modeler`
- `HKEY_LOCAL_MACHINE\Software\Wow6432Node\Microsoft\VisualStudio\6.0`
- `HKEY_CURRENT_USER\Software\Microsoft\DevStudio`
- `HKEY_CURRENT_USER\Software\Microsoft\MSVSDG`
- `HKEY_CURRENT_USER\Software\Microsoft\Visual Basic\6.0`
- `HKEY_CURRENT_USER\Software\Microsoft\Visual Modeler`
- `HKEY_CURRENT_USER\Software\Microsoft\VisualFoxPro`
- `HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\6.0`

## Подготовка файлов для установки

### Шаг 1

Создайте в удобном для вас месте папку и поместите в неё копию дистрибутива. Копия нужна по той причине, что в неё будут вноситься изменения. Если у вас многодисковый дистрибутив, в процессе копирования пропускайте дублирующиеся имена файлов.

### Шаг 2

Откройте для редактирования файл `SETUPWIZ.INI` и в секции `[setup wizard]` удалите значение после знака равенства в  записи `VmPath=ie4\msjavx86.exe`, если такая есть. Это в процессе установки создаст пустую переменную окружения и не позволит мастеру поставить очень древнюю версию `MS Java`. Отредактированный INI-файл выглядит примерно так:

![](https://cloudfront.codeproject.com/articles/1191047/setupwiz_ini.png)

### Шаг 3

Перейдите в папку, созданную на первом шаге и найдите в ней файл `SETUP.EXE`. В свойствах этого файла выставьте режим совместимости с `Windows XP SP3` (можно также `SP2`) и убедитесь, что стоит галочка `Выполнять  эту программу от имени администратора`.

![](https://cloudfront.codeproject.com/articles/1191047/setup_exe.png)

## Запуск мастера установки

Запустите `SETUP.EXE`; продвигаясь вперёд шаг за шагом, можете оставлять всё по умолчанию, пока не встретите выбор типа установки, выберите `Custom`. Если мастер спросит, ставить ли `Source Safe`, ответьте `NO`.

### Custom Settings

На этот момент перед вами должен быть диалог `Visual Studio 6.0 Enterprise - Custom`. В этой статье мы ставим только `Visual Basic 6.0` и `Visual C++ 6.0`, поэтому вы можете отключить опции `Visual FoxPro 6.0`, `Visual InterDev 6.0` и `Visual SourceSafe 6.0`. Теперь выберите пункт `Visual C++ 6.0` и нажмите кнопку `Change Option...` для установки библиотек поддержки Юникода в MFC.

![](https://cloudfront.codeproject.com/articles/1191047/custom.png)

### Установка библиотек поддержки Юникода

Хотя эта часть является необязательной, большинство современных приложений должны обеспечивать поддержку нескольких языков, и вам понадобится эта опция, если вы планируете поддерживать такие языки, как китайский, японский или арабский. Перед переходом к следующему диалогу выберите пункт `VC++ MFC and Template Libraries` и нажмите кнопку `Change Option...` Тут мы должны выбрать все пункты (кнопка `Select All`), диалог будет выглядеть так:

![](https://cloudfront.codeproject.com/articles/1191047/unicode.png)

Нажмите кнопку `OK`. Продолжайте нажимать `OK` до возвращения к диалогу `Visual Studio 6.0 Enterprise - Custom`.

### Запрет провайдеров ADO, RDS и OLE DB

Выберите пункт `Data Access` и нажмите кнопку `Change Option...` В открывшемся диалоге снимите галочку с пункта `ADO, RDS and OLE DB Providers`. Всплывёт сообщение, в котором говорится, что компонент является важной частью приложения. Игнорируем предупреждение и жмём кнопку `OK`. Если оставить эту опцию включённой, установка студии окончится неудачей.

### Запрет Visual Studio Analyzer

Последний параметр, который нам нужно отключить, - это анализатор `Visual Studio`. Если оставить этот флажок, установка не удастся. Для отключения выберите пункт `Enterprise Tools` и нажмите кнопку `Change Option...` Снимите флажок с `Visual Studio Analyzer` в диалоговом окне `Enterprise Tools` и нажмите кнопку `OK`.

![](https://cloudfront.codeproject.com/articles/1191047/analyzer.png)

### Завершение установки

Теперь всё готово к старту; нажмите кнопку `Continue`, чтобы начать процесс. В диалоговом окне `Setup Environment Variables` просто оставьте пункт `Register Environment Variables` неотмеченным и нажмите кнопку `OK`. Теперь инсталлятор должен сделать своё дело. После завершения вам будет предложено перезаписать настройки JIT, выберите `NO`. Далее вы должны увидеть диалоговое окно `Restart Windows`, означающее, что установка прошла успешно. Закройте все открытые приложения и нажмите кнопку `Restart Windows`.

![](https://cloudfront.codeproject.com/articles/1191047/restart.png)

После перезагрузки вас спросят, нужно ли ставить MSDN. Поступите так, как считаете нужным.

## Установка Service Pack 6

После успешного завершения установки самой студии необходимо поставить её последний сервиспак. Скачайте его, распакуйте в локальную папку и запустите `SETUPSP6.EXE`. Выполните те же действия, что и в шаге 3 для `SETUP.EXE`, измените совместимость с `Windows XP SP3` и запустите исполняемый файл от имени администратора. Следуйте инструкциям, чтобы завершить установку.
После завершения снова выполните действия, описанные в шаге 3 выше, и дважды проверьте режим совместимости для файлов .exe, расположенных в `C:\Program Files (x86)\Microsoft Visual Studio\Common\MSDev98\Bin\`. Теперь `Visual Studio 6.0` готова к использованию.

## Совместимость програм

Если на первом запуске студии всплывёт диалог  `Program Compatibility Assistant`, поставьте флажок `Don't show this message again` и нажмите кнопку `Run the program without getting help`.

![](https://cloudfront.codeproject.com/articles/1191047/vs-compat.png)

## Отладка

Если ваше приложение виснет и вылетает на этапе отладки, в настройках `Tools->Options` перейдите на вкладку `Debug` и снимите флажки `OLE RPC debugging` и `Debug commands invoke Edit and Continue`, затем перезапустите студию. После этого продвижение по коду в отладке не должно вызывать проблем.

![](https://cloudfront.codeproject.com/articles/1191047/vs-debug.png)
