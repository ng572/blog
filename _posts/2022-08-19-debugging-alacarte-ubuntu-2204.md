---
layout: post
title: debugging alacarte ubuntu-22.04
comments: true
---

### Symptom

Native APT-installed alacarte (aka Main Menu editor) NOT responding when I was adding a new item

### Log

    $ alacarte
    ...
    Traceback (most recent call last):
      File "/usr/share/alacarte/Alacarte/ItemEditor.py", line 186, in on_response
        self.save()
      File "/usr/share/alacarte/Alacarte/ItemEditor.py", line 176, in save
        util.fillKeyFile(self.keyfile, self.get_keyfile_edits())
      File "/usr/share/alacarte/Alacarte/ItemEditor.py", line 234, in get_keyfile_edits
        Icon=get_icon_string(self, self.builder.get_object('icon-image')),
      File "/usr/share/alacarte/Alacarte/ItemEditor.py", line 58, in get_icon_string
        filename = editor.icon_file
    AttributeError: 'LauncherEditor' object has no attribute 'icon_file'

### Debugging

add the block of code that would open up the debugger

```py
    try:
        filename = editor.icon_file
        raise
    except:
        extype, value, tb = sys.exc_info()
        pdb.post_mortem(tb)
```
so it looks like this
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

### Final fix

```py
def get_icon_string(editor, image):
    if hasattr(editor, "icon_file"):
        return try_icon_name(editor.icon_file)

    return image.props.icon_name
```
