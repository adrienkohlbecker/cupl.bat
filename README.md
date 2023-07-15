# cupl.bat

A batch file to execute WinCUPL compilation and fitting from the command-line.

WinCUPL is a legacy application used to design logic for GALs (16V8, 22V10), SPLDs (Atmel's ATF16V8, ATF22V10) and CPLDs (Atmel's ATF1502, ATF1504 and ATF1508).
However, its GUI is clunky and unreliable, and its text editor is poor.

Consequently, it is better to write logic code in your own modern text editor, and run WinCUPL's command-line tools for compilation. It is much more convenient and error output is better.

## How to use

TL:DR; `cupl.bat FILE.pld`

### Detailed instructions

1. Write your logic just like you would in WinCUPL's GUI. Let's use one of WinCUPL's built in examples: `C:\Wincupl\Examples\Atmel\ADDER.PLD`. This example implements an adder using a 16V8 GAL.

2. Execute `cupl.bat` as follows `cupl.bat C:\Wincupl\Examples\Atmel\ADDER.PLD`

```
C:\Wincupl\Projects>cupl.bat C:\Wincupl\Examples\Atmel\ADDER.PLD
cuplx
time: 0 secs
cupla
time: 0 secs
cuplb
time: 0 secs
cuplm
time: 0 secs
cuplc
time: 0 secs
total time: 0 secs


Normal exit
Error Code = 0

"Device G16V8 does not need fitter, skipping."
"Done!"
```

3. The output files are available next to the `.PLD` file, including `.JED` for programming and `.DOC` for details on how the compilation went.

4. If your device necessitates a fitter (ATF1502, ATF1504, ATF1508), this is executed automatically by `cupl.bat`. Take `C:\Wincupl\Examples\Atmel\TIM_CNT.PLD` as an example. This file implements a 16-bit timer/counter using an ATF1508.

```
C:\Wincupl\Projects>cupl.bat C:\Wincupl\Examples\Atmel\TIM_CNT.PLD
cuplx
time: 0 secs
cupla
time: 0 secs
cuplb
time: 0 secs
cuplm
time: 1 secs
cuplc
time: 0 secs
find1508
time: 0 secs
total time: 1 secs


Normal exit
Error Code = 0

Atmel ATF1508AS Fitter Version 1.8.7.8 (02-05-03)
Copyright 1999,2000 Atmel Corporation
---------------------------------------------------------
 Fitter_Pass 1, Preassign = KEEP, LOGIC_DOUBLING : OFF
 ...
 Design fits successfully

"Done!"
```

5. And additional `.FIT` file becomes available with details on how the fitting process went.

### Pause

If you need to execute `cupl.bat` as an editor build command, and to keep `CMD.exe` open after compilation, `cupl.bat /p` pauses execution before closing the window. For example, I have mapped `C:\Wincupl\Projects\cupl.bat "$(FULL_CURRENT_PATH)" /p` to F6 in my Notepad++ configuration.
