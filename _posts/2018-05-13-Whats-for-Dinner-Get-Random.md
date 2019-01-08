---
layout: post
title: "What's for Dinner?: Get-Random"
date: 2018-05-13
---
### Introduction

Often, as a family, it gets to 5:00PM and the inevitable question is asked.

**What's for dinner?**

My wife came up with a wonderful idea. Collect a list of all of our favourite meals.
Number them, use a random number generator and **BOOM**, *What's for dinner?* Is answered.

Always thinking of ways to use PowerShell, it seemed like the perfect use for [Get-Random](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/get-random?view=powershell-6).

Today is Mother's Day in Australia. I thought using *Get-Random* and using it to
generate our meal list would be a great Mother's Day present... :).
We no longer need to generate a number and then look at our list. It can be done automatically.

To all the Mum's out there, Thank You. Thank You for everything you do. Thank You
for everything you do that isn't recognised and Thank You for being you!

To my wife, Thank You for being the best Mum our kids could ask for.

Now, to the code...
### PowerShell Code Block
```powershell
Get-Random @('Spaghetti Bolognaise','Tuna Pasta Bake','Steak and Vegies',
             'Silverside and Vegies','Toasted Sangas','Tacos','Chicken Pasta',
             'Chicken Pasta Bake'.'Pancakes','FODMAP Soup and Sandwiches',
             'Chicken Tenders and Vegies','Roast Vegies','Lasagna','Fried Rice',
             'Roast Beef','Sausages and Gravy','Spaghetti Carbonara','Beans on Toast',
             'Rissotto','Braised Steak and Mash','Baked Potatoes','Homemade Pizza',
             'Hot Dogs','Nuggets and Chips','Nachos','Sharron''s Chicken and Salad',
             'Chicken and Leek Pie','Shepherds Pie')
```
Those with a keen eye may have noticed *Sharron''s Chicken and Salad*.
As a single quote is used as an apostrophe, PowerShell thinks the string has finished at *'Sharron'*. Therefore, we need to use two single quotes side by side.

Below is the error without *'Sharron''s'*.

```powershell
PS C:\Users\timha\Desktop> .\randomMeals.ps1
At C:\Users\timha\Desktop\randomMeals.ps1:7 char:63
+ ...            'Hot Dogs','Nuggets and Chips','Nachos','Sharron's Chicken ...
+                                                                 ~
Unexpected token 's' in expression or statement.

At C:\Users\timha\Desktop\randomMeals.ps1:8 char:51
+              'Chicken and Leek Pie','Shepherds Pie')
+                                                   ~~
The string is missing the terminator: '.

At C:\Users\timha\Desktop\randomMeals.ps1:10 char:2
+
Missing closing ')' in subexpression.
    + CategoryInfo          : ParserError: (:) [], ParseException
    + FullyQualifiedErrorId : UnexpectedToken
```
Single quotes inside single quotes cannot be escaped by using the the normal escape character, the backtick `.
A work around could be to use double quotes *"Sharron's Chicken and Salad"* around the string.
For more information on this, [Richard Mueller's PowerShell Escape article](http://www.rlmueller.net/PowerShellEscape.htm) has a good explanation of escaping characters.

To execute the script, I saved the file as a .PS1 file. As long as [PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/setup/installing-windows-powershell?view=powershell-6) is installed on your computer, it knows how to run this file.
[How to Write and Run Scripts in the Windows PowerShell ISE](https://docs.microsoft.com/en-us/powershell/scripting/core-powershell/ise/how-to-write-and-run-scripts-in-the-windows-powershell-ise?view=powershell-6) and [Running Scripts](https://technet.microsoft.com/en-us/library/bb613481(v=vs.85).aspx) have further information on how to runs scripts from your computer. Please note the *Execution Policy* section in both documents to enable the script to run.

### Results

```powershell
PS C:\Users\timha\Desktop> .\randomMeals.ps1
Shepherds Pie
PS C:\Users\timha\Desktop> .\randomMeals.ps1
Silverside and Vegies
PS C:\Users\timha\Desktop> .\randomMeals.ps1
Rissotto
PS C:\Users\timha\Desktop> .\randomMeals.ps1
Fried Rice
PS C:\Users\timha\Desktop> .\randomMeals.ps1
Sharron's Chicken and Salad
```

Feel free to change the meals, or, use the idea to randomise anything.

Usually, in a script like above, I would use parameter completion and use:
```powershell
Get-Random -InputObject @('String1','String2')
```
However, this generated the error *Get-Random : Cannot validate argument on parameter 'InputObject'.*
See [PowerShell GitHub Issue 3682](https://github.com/PowerShell/PowerShell/issues/3682) for further information.

*Get-Random* has a lot of uses as shown by running [Get-Help](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/get-help?view=powershell-6) against it, or by viewing the documentation as linked above.
```powershell
Get-Help Get-Random -Full
```

Hope you're having a great day and this is of use.

Thanks, Tim.
