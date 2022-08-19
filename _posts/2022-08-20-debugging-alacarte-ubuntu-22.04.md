### Symptom

Native APT-installed of alacarte (aka Main Menu editor) NOT responding when I was adding a new item

### Log

$ alacarte

### Debugging

add the block of code that would help us see the variables

```py
    try:
        filename = editor.icon_file
        raise
    except:
        extype, value, tb = sys.exc_info()
        pdb.post_mortem(tb)
```

```py
def get_icon_string(editor, image):
    try:
        filename = editor.icon_file
        raise
    except:
        extype, value, tb = sys.exc_info()
        pdb.post_mortem(tb)

    if filename is not None:
        return try_icon_name(filename)

    return image.props.icon_name
```

run the program again we find out `editor.icon_file` is supposed to hold the path of user selected icon, but the attribute will go missing if not selected by user

```
-> raise
(Pdb) editor.icon_file
'/home/ng/Pictures/py.svg'
```
```
-> filename = editor.icon_file
(Pdb) editor.icon_file
*** AttributeError: 'LauncherEditor' object has no attribute 'icon_file'
```

### final fix

```py
def get_icon_string(editor, image):
    if hasattr(editor, "icon_file"):
        return try_icon_name(editor.icon_file)

    return image.props.icon_name
```
