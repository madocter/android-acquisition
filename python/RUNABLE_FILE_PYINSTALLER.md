# Make executable file with pyinstaller
**Note:** Guide is done using psio_assist (abandoned and useless software) as a model.


## Linux instructions

Install pyinstaller with python package installer:

```bash
pip install pyinstaller
```

Launch for first time pyinstaller:

```bash
python3 -m PyInstaller --onefile --windowed --add-binary "/usr/lib/x86_64-linux-gnu/libpython3.10.so.1.0:." psio_assist.py
```

Add shared libraries to avoid errors:

```bash
--add-binary "/usr/lib/x86_64-linux-gnu/libpython3.10.so.1.0:."
```

Now you will have file: `psio_assist.spec`

And in `Dist` directory the executable file but might not be able to run because **hidden imports**

Check necessary imports by running the executable and checking the error or checking the source code.

Open and edit the file named: `psio_assist.spec` and add the imports, example:

`imports: hiddenimports=['PIL._tkinter_finder', 'PIL.ImageTk'],`

(This doesn't work, don't do it)

`files: datas=[('data/psio_assist.db', 'data'), ('config', '.')],`

Example:

```
a = Analysis(
['psio_assist.py'],
pathex=[],
binaries=[('/usr/lib/x86_64-linux-gnu/libpython3.10.so.1.0', '.')],
datas=[],
hiddenimports=['PIL._tkinter_finder', 'PIL.ImageTk'],
hookspath=[],
hooksconfig={},
runtime_hooks=[],
excludes=[],
noarchive=False,
optimize=0,
)
pyz = PYZ(a.pure)

exe = EXE(
pyz,
a.scripts,
a.binaries,
a.datas,
[],
name='psio_assist',
debug=False,
bootloader_ignore_signals=False,
strip=False,
upx=True,
upx_exclude=[],
runtime_tmpdir=None,
console=False,
disable_windowed_traceback=False,
argv_emulation=False,
target_arch=None,
codesign_identity=None,
entitlements_file=None,
)
```

Save and launch pyinstaller but this time to operate with the spec file:

```bash
python3 -m PyInstaller psio_assist.spec
```

In case the software have resources such as data or config:

Copy `data` directory from src and `config` file and put in same place than the psio_assist file in dist directory that we generated with pyinstaller.

Now you have the executable file for LINUX, and do not need python or any dependency to execute it.


## Windows instructions

```bash
pip install pyinstaller
python -m PyInstaller --onefile --windowed psio_assist.py
```

In case the software have resources such as data or config:

Copy `data` directory from src and `config` file and put in same place than the psio_assist file in dist directory that we generated with pyinstaller.

Now you have the executable file for Windows, and do not need python or any dependency to execute it.

