﻿# Snippet
 
Использование: Наберите несколько символов → нажмите Tab → Вставится текстовый образец.

Размещается в `*.sublime-snippet` в любой папке пакета.

Появляется в меню `Tools | Snippets | <Your Package>`.

Меню `Tools | Developer | New Snippet...` → Sublime Text создаст основу для нового сниппета

Каждый `*.sublime-snippet` может содержать только один сниппет. Для размещения нескольких, используйте [AutoComplete.txt#.sublime-completions]

Используя Заданные Сочетания Клавши, Мы можем
 * загрузить определённый сниппет, например: `{ "keys": ["%"], "command": "insert_snippet", "args": {"name": "Packages/XML/long-tag.sublime-snippet"} }`
 * вставить сниппет без создания файла .sublime-snippet, например: `{ "keys": ["%"], "command": "insert_snippet", "args": {"contents": "%$0%"} }`
    
Пример файла `.sublime-snippet` :

```
    <snippet>
        <content>=dword:00000001</content>              // образец текста для вставки
        <tabTrigger>=d</tabTrigger>                     //Опционально: Наберите эти символы, затем нажмите Tab для вставки сниппета
        <scope>source.reg</scope>                       //Опционально: Ограничение использования сниппета определённой областью [[Scope.txt]]
        <description>dword in .reg file</description>   //Опционально: Описание, выводимое в меню сниппета
    </snippet>
```

## content:
   * Пример:    `assert ${1:condition}, ${2:message}, ${3:continue=0}`
   * Не должно содержать `]]>`  → Работает так: вставить неопределённую/пустую переменную, например: `]]$NOT_DEFINED>`
   * `$` должен быть экранирован `\$`
   * Всегда используйте табуляцию для отступов → при выполнении табуляции трансформируются в пробелы, если "translateTabsToSpaces": true
   * Маркеры полей `$1`  `$2` `$3` ... `$n`
       * Tab/Shift+Tab будет циклически перемещать курсор по полям.
       * Если поле повторяется:
            * `First Name:$1, Last Name:$2, Full Name:$1 $2`
            * Множественный курсор разместится во всех позициях → Одинаковые поля будут редактироваться одновременно.
       * `$0`   Специфическая точка выхода (При нажатии Tab курсор переместится к последнему полю)
   * Заполнители:
        * Определите значения по умолчанию, например:  `First Name: ${1:Guillermo}, Second Name: ${2:López}`
        * Можно вкладывать один в другой, например:  `Test: ${1:Parent ${2:Nested}}`
   * Можно использовать переменные:
        * Переменные среды, например: `$TM_FULLNAME`, `$TM_FILENAME`, `$TM_TAB_SIZE`, `$TM_SOFT_TABS`
        * Кастомные переменные, определённые в `.sublime-options`
        * Пример:  `User name: ${1:$TM_FULLNAME}, Табуляция равна $TM_TAB_SIZE пробелов`
        * Полный список переменных:
        ```
            | $PARAM1 .. $PARAMn | Аргументы, переданные команде insertSnippet.                             |
            | $SELECTION         | Текст, который был выбран, при срабатывании сниппета.                    |
            | $TM_CURRENT_LINE   | Содержимое строки, в которой находился курсор при срабатывании сниппета. |
            | $TM_CURRENT_WORD   | Текущее слово под курсором при срабатывании сниппета.                    |
            | $TM_FILENAME       | Имя редактируемого файла, включая расширение.                            |
            | $TM_FILEPATH       | Путь к редактируемому файлу.                                             |
            | $TM_FULLNAME       | Пользовательское Имя пользователя.                                       |
            | $TM_LINE_INDEX     | Столбец, в который вставляется сниппет, отсчитывается от 0.              |
            | $TM_LINE_NUMBER    | Строка, в которую вставляется сниппет; отсчитывается от 1.               |
            | $TM_SELECTED_TEXT  | Псевдоним для $SELECTION.                                                |
            | $TM_SOFT_TABS      | YES если translateTabsToSpaces = true, иначе NO.                         |
            | $TM_TAB_SIZE       | пробелов на табуляцию (управляется параметром tabSize).                  |
        ```
## Расширенный пример:
   ``` %${0:$SELECTION}%        //разместить текущее выделение в знаки %```
