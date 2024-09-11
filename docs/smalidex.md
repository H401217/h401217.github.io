# Pou Modding

this is beta and only works on 1.4.120

This wiki will only refer to Android modding, due to the limitations with Apple version.

Pou app (android) can be decompiled using APKtool

You can add things like buttons, minigames, potions, clothing. But it isn't recomended to create "infinite points" mods in Pou or mods that could get banned.

Requirements to understand this xdd
* know smali
* know how to use apktool
* know how to use jarsigner (android doesnt accept unsigned apk bc yes)
* uninstall original pou app (idk how to change package name like playstark) dont forget to save ur data
* know adb

## Folders list
This is a list about some interesting folders in Pou, these are located in "smali" folder (apktool projects). Pou code is ordered in folders that are not self explainatory (optimization)
* "s6/" - Network Folder
* "z6/" - options menu
* "q9/a" - pou state?
* "y8" - potions
* "x8/c" - put potions

## Creating a button

### Group of buttons
You can use [this button template](./smalifiles/buttongroupHorz.md). Remember replacing "\[MAIN]" with the file instance, and "\[BUTTON1]" with the button file/instance.
[group of buttons](./smalifiles/buttonGroup.md)
[binary button](./smalifiles/binarybutton.md)

## Creating a potion
Before creating a potion you should assign an ID to it (NUMBERS after 8 are recomended)

### Image
Your potion image should be located in `assets/images/potions`, its file name should be `[ID].png` (for example: `9.png`).
It is recomended having the potion size as equal as the other potions, or else it will look more bigger or more smaller.

### Name & description
(this was made when my internet was down so i dont have android documentation)

The game's strings are located in `res/values/strings.xml` and `res/values/public.xml`. `public.xml` asigns an number to "Keys" (string template), and `strings.xml` locates strings for the templates.

|ID|Key|Value|
|-|-|-|
|0x4632|some_key|Some Key|

In `public.xml` you should go in the part between "string" and "style" types. It should look like this:
```xml
    <public type="string" name="yes" id="0x7f1103f0" />
    <public type="string" name="you_got_N_coins" id="0x7f1103f1" />
    <public type="style" name="AlertDialog.AppCompat" id="0x7f120000" />
```
After the line that contains "you_got_N_coins" you can put 2 xml values for the Name and the Description of your potion, but summing "1" to the last string id after every line
```xml
    <public type="string" name="you_got_N_coins" id="0x7f1103f1" />
    <public type="string" name="MY_new_potion_title" id="0x7f1103f2" />
    <public type="string" name="MY_new_potion_desc" id="0x7f1103f3" />
```
Then, in `strings.xml`, you can also go to the end of the text and put 2 lines indicating your potion name
```xml
    <string name="yes">Yes</string>
    <string name="you_got_N_coins">You got # coins!</string>

    <string name="MY_new_potion_title">Potion Title</string>
    <string name="MY_new_potion_desc">A potion description</string>

</resources>
```

### Smali
The potion code should be in `smali/y8/`, you can add any name to the file, but it should end with `.smali`

[Potion template](./smalifiles/potion.md)


After that, you can go to `smali/x8/c.smali`, and at the end of `public constructor <init>` you can put this code (before `return-void`):
```smali
    new-instance p1, Ly8/[NAME];
    invoke-direct {p1}, Ly8/[NAME];-><init>()V
    invoke-virtual {p0, p1}, Ld7/b;->c(Lk8/j;)V
```
Replace \[NAME\] with your potion file name (without the `.smali`)