# Expressions

Parameter values passed into a CommandBox command don't have to be static.  Any part of the paramter which is enclosed in backticks (`) will be evaluated as a CommandBox expression. That means that the enclosed text will be first executed as thought it were a separate command and its output will be substituted in its place.

an be used as an expression, including calls to native OS binaries or CFML functions, or REPL one-liners.  Note that any text that a command immediately flushes to the console during its execution (like a download progress bar) will not be returned by the expression, though it will display on the console.

## Express Yourself

Take for instance, this simple command that prints out the contents of a file:

```bash
cat defaultServer.txt
```

It can be used as a dynamic parameter like so:

```bash
server start name=`cat defaultServer.txt`
```


In the example above, the contents of the defaultServer.txt file will be passed in as the value of the "name" parameter to the "server start" command.  If the contents of the file was the text `myServer`, the equivalent final command would be:

```bash
server start name=myServer
```

There can be more than one expression in a single parameter value.  Expressions can also be combined with static text and they will all be evaluated in the order they appear:

```bash
echo "Your CommandBox version is `ver` and this app is called '`package show name`'!!"
```

That would output something similar to:
```
Your CommandBox version is 2.5.0 and this app is called 'Brad's cool app'!
```

If you need to use an actual backtick in a parameter value, escape it with a backslash.

```bash
echo "Nothing to \`see\` here"
```

Which outputs

```
Nothing to `see` here
```