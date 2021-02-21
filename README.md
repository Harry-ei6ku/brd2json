# brd2json
**ULP for Eagle and Fusion 360 Electronics which generates a JSON representation of the board.**

The primary purpose is to integrate with [openscopeproject/InteractiveHtmlBom](https://github.com/openscopeproject/InteractiveHtmlBom), as the format of the objects in the generated JSON file is aligned with the internal data structures used in that tool.

## Implementation Status and Limitations
The ULP is mostly feature-complete.  Some known limitations:
* __Proportional fonts__ aren't supported (won't be rendered) - use vector fonts if you want them rendered.  An easy solution here is to set the "Always Vector Font" option in the Eagle/Fusion 360 Electronics preferences.
* __Polygons__ - Autodesk redefined polygon object type(s) in Fusion 360 Electronics.  For now polygons are not supported on the `main` branch, so it remains compatible with both Eagle and Fusion 360 Electronics.  The `fusion` branch adds support for UL_POLYSHAPE for Fusion 360 Electronics, but breaks compatibility with Eagle.

![brd2json demo](https://j.gifs.com/gZw31k.gif)

## Usage
* With your board open in Eagle or Fusion 360, simply run the ULP and the JSON file will be automatically generated
* Upon completion, a dialog will pop up listing the full path of the generated JSON file, for easy copy-paste.
  Using Fusion 360 Electronics On Windows 10, it will look something like this:
  
    `C:\Users\<username>\AppData\Local\Temp\Neutron\ElectronFileOutput\<autogenerated gibberish>\<boardname>.json`
* Finally, pass the .json file as an argument to InteractiveHtmlBom. This is the same as the method listed in the wiki for processing an EasyEDA JSON file.

  `python generate_interactive_bom.py "<path>\<boardname>.json"`
  
### Extra Fields
All attributes of each element are inserted in the JSON file for (optional) use.  To display a particular attribute as an additional column in the resulting interactive BOM, use the `--extra-fields` command-line argument.  For instance:

`python generate_interactive_bom.py "<path>\<boardname>.json" --extra-fields ASSY` will include the attribute "ASSY" as an added column - any elements which lack this attribute will simply be blank.
