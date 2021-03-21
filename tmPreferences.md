# Контролируйте разное поведение

Название файла не имеет значения. *Далее в сдвоенных квадратных скобках указано что-то вроде ссылок на разделы*

## Для примера структура [[Plist.txt#Sublime Text PList]]:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple Computer//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
    <dict>
        <key>name</key>                         //Просто описание. Sublime Text проигнорирует это
        <string>Некое описание</string>
        <key>scope</key>                        // Список областей, разделённых запятыми, применимых к [[Scope.txt]]
        <string>text.txt, source.python meta.function.python</string>
        <key>uuid</key>                        // Каждый файл должен содержать один уникальный айди
        <string>77AC23B6-8A90-11D9-BAA4-000A9584EC8D</string>
        <key>settings</key>                    // Важно. Контейнер настроек. Эти настройки подробно описываются ниже
        <dict>
            [[#Comment:]]
            [[#cancelCompletion]]
            [[#Symbol:]]
            [[#Indent:]]
        </dict>
    </dict>
</plist>
```

## Переменные оболочки [shellVariables]:

Влияют на строку команды `toggle_comment` (ctrl+/) и блок команды `toggle_comment` (ctrl+shift+/)
```xml
    <key>shellVariables</key>
    <array>
        <dict>
            <key>name</key>
            <string>TM_COMMENT_START</string>   // метка начала комментария
            <key>value</key>
            <string>;</string>                  // строка комментария
        </dict>
        <dict>
            <key>name</key>
            <string>TM_COMMENT_END</string>     //[Опционально] Строка конца комментария (совпадает с TM_COMMENT_START для установки метки блока комментария). Если опущено, TM_COMMENT_START будет эффективен до конца строки (comment line).
            <key>value</key>
            <string>:_/</string>
        </dict>

        <dict>
            <key>name</key>
            <string>TM_COMMENT_DISABLE_INDENT</string>   //отключает отступ для метки TM_COMMENT_START.
            <key>value</key>
            <string>yes</string>
        </dict>

        Заметьте: Чтобы определить дополнительные метки start/end/disable, назовите их [TM_COMMENT_START_2, TM_COMMENT_END_2, TM_COMMENT_DISABLE_INDENT_2];  [TM_COMMENT_START_3, TM_COMMENT_END_3, TM_COMMENT_DISABLE_INDENT_3] ...
    </array>
```
## Завершение [Completion]:
```xml
    <key>cancelCompletion</key>     //Если это совпадает с текущей строкой, подавляется всплывающее окно автозаполнения.
    <string>^(.*\b(and|or)$)|(\s*(pass|return|and|or|(class|def|import)\s*[a-zA-Z_0-9]+)$)</string>
```
## Указатель [Symbol]: [[Sublime Text.txt#Goto Definition]]
```xml
    <key>showInSymbolList</key>             //Покажется ли в Goto > Symbol  (1 = true)
    <integer>1</integer>
    <key>showInIndexedSymbolList</key>      //Ссылки на символы в глобальном списке символов.
    <string>1</string>
    <key>symbolTransformation</key>         //Разделённая точкой с запятой регулярка для поиска и замены текстов => настраиваются перед отображением в меню Goto > Symbol
    <string>
        s/\(/:  /g;                         //Поиск левой скобки и замена её двоеточием с двумя пробелами. /g означает соответствие всем вхождениям
        s/,.*//g;                           //Найдите запятую, за которой следует любой символ и замените на ничего.
        s/class\s+([A-Za-z_][A-Za-z0-9_]*.+?\)?)(\:|$)/$1/g;   //захваченный символ, такой как класс FooBar (объект), будет отображаться как FooBar (объект) в списке символов .
    </string>
    <key>symbolIndexTransformation</key>
    <string>/.*/\L$1/;</string>             //преобразуем к нижнему регистру (так что определение Goto может работать нечувствительно к регистру)
```
## Отступ [Indent]:
```xml
    <key>decreaseIndentPattern</key>                        // Если совпадает с текущей строкой, следующие строки будут на отступ дальше
    <string>^\s*(elif|else|except|finally)\b.*:</string>
    <key>increaseIndentPattern</key>                        //Если совпадает в текущей строке, следующие строки будут удалены на один уровень
    <string>^\s*(class|def|elif|else|except|finally|for|if|try|with|while)\b.*:\s*$</string>
    <key>bracketIndentNextLinePattern</key>                 //Если совпадает в текущей строке, следующая строка будет иметь на один отступ больше
    <string>Вставьте сюда регэксп</string>
    <key>disableIndentNextLinePattern</key>                 //If it matches on the current line, the next line will not be indented further. Если найдено в текущей строке, следующая строка не будет иметь большего отступа
    <string>1</string>
    <key>unIndentedLinePattern</key>                        // Автоотступ будет игнорировать строки, соответствующие данной регулярке, когда будет вычислять отступ.
    <string>Вставьте сюда регэксп</string>
```
