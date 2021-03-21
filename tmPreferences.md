Control miscellaneous behaviours
File name is not important
Structure: [[Plist.txt#Sublime Text PList]], example:
    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE plist PUBLIC "-//Apple Computer//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
    <plist version="1.0">
    <dict>
        <key>name</key>                         //Just a description, ST ignore this
        <string>Some description</string>
        <key>scope</key>                        //Comma-separated list of scope names to apply to [[Scope.txt]]
        <string>text.txt, source.python meta.function.python</string>
        <key>uuid</key>                        //Each file must have an unique ID
        <string>77AC23B6-8A90-11D9-BAA4-000A9584EC8D</string>
        <key>settings</key>                    //Required. A container for settings.
        <dict>
            [[#Comment:]]
            [[#cancelCompletion]]
            [[#Symbol:]]
            [[#Indent:]]
        </dict>
    </dict>
    </plist>

Shell Variables: Affect command toggle_comment line (ctrl+/) and toggle_comment block (ctrl+shift+/)
    <key>shellVariables</key>
    <array>
        <dict>
            <key>name</key>
            <string>TM_COMMENT_START</string>   //Start a comment marker
            <key>value</key>
            <string>;</string>                  //String to start a comment
        </dict>
        <dict>
            <key>name</key>
            <string>TM_COMMENT_END</string>     //[Optional] String to end a comment (match with TM_COMMENT_START to become block comment markers). If omitted, TM_COMMENT_START will be effective until end-of-line (comment line).
            <key>value</key>
            <string>:_/</string>
        </dict>

        <dict>
            <key>name</key>
            <string>TM_COMMENT_DISABLE_INDENT</string>   //Disables indentation for the TM_COMMENT_START marker.
            <key>value</key>
            <string>yes</string>
        </dict>

        Note: To define additional start/end/disable markers, name them [TM_COMMENT_START_2, TM_COMMENT_END_2, TM_COMMENT_DISABLE_INDENT_2];  [TM_COMMENT_START_3, TM_COMMENT_END_3, TM_COMMENT_DISABLE_INDENT_3] ...
    </array>

Completion:
    <key>cancelCompletion</key>     //If it matches on the current line, supresses the autocomplete popup.
    <string>^(.*\b(and|or)$)|(\s*(pass|return|and|or|(class|def|import)\s*[a-zA-Z_0-9]+)$)</string>

Symbol: [[Sublime Text.txt#Goto Definition]]
    <key>showInSymbolList</key>             //Whether to show in Goto > Symbol  (1 = true)
    <integer>1</integer>
    <key>showInIndexedSymbolList</key>      //Links symbols to the global symbol list.
    <string>1</string>
    <key>symbolTransformation</key>         //Semicolon-separated Oniguruma Regex to search-and-replace texts => customize before display in menu Goto > Symbol
    <string>
        s/\(/:  /g;                         //Search left parenthesis and replace it with a colon plus 2 spaces. /g means match all occurences
        s/,.*//g;                           //Search comma followed by any character and replace it with nothing.
        s/class\s+([A-Za-z_][A-Za-z0-9_]*.+?\)?)(\:|$)/$1/g;   //a captured symbol such as  class FooBar(object)  would show up as FooBar(object) in the symbol list.
    </string>
    <key>symbolIndexTransformation</key>
    <string>/.*/\L$1/;</string>             //Convert to lowercase (so that Goto Definition can work case-insensitively)

Indent:
    <key>decreaseIndentPattern</key>                        //If matches in current line, next lines will be indented one level further
    <string>^\s*(elif|else|except|finally)\b.*:</string>
    <key>increaseIndentPattern</key>                        //If matches in current line, next lines will be unindented one level
    <string>^\s*(class|def|elif|else|except|finally|for|if|try|with|while)\b.*:\s*$</string>
    <key>bracketIndentNextLinePattern</key>                 //If matches in current line, only the next line will be indented one level further.
    <string>insert regex here</string>
    <key>disableIndentNextLinePattern</key>                 //If it matches on the current line, the next line will not be indented further.
    <string>1</string>
    <key>unIndentedLinePattern</key>                        //The auto-indenter will ignore lines matching this regex when computing the next line’s indentation level.
    <string>insert regex here</string>
