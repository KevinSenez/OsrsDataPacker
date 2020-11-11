# OsrsDataPacker

## Info
this tool can be used to pack data from the OSRS cache to a RS2 cache.
Packing is done with an offset, which you can customize in your specific packer. 
The tool was created and tested with the 718 revision, but should be able the handle others RS2 cache revisions.

**This tool is unstable, use within your own risk. Always make a backup of your cache**

Currently supports
 - Objects
 - Items
 - Models
 - Maps
 - SpotAnimations
 - RenderAnimations
 - MapLayers
 
 Animations are almost done, will be pushed on a later date.
 Widgets/Interfaces might also be done on a later date.
## How To

Run the DataPackerTool.java file, atm there is no support for running individual packers. When you run this class it will run ALL the packers.
You can easly add singe datapackers to your main. Example:
```
 var objectPacker = new OsrsObjectPacker();
 objectPacker.packAllData(sourceCache,destinationCache);
 
```

## I tried the tool, but the osrs data isn't working ? 
I modified my client so there are multiple decoders, one for my revision and for the osrs revision.
On certain dataloaders you've to implement these offsets. Example of reading the modelIds from osrs objects:
```
if (opcode == 5) {
					length = buffer.readUnsignedByte();
					int[] models = new int[length];
					for (index = 0; index < length; index++) {
						models[index] = (buffer.readUnsignedShort() + Settings.OSRS_MODELS_OFFSET);
					}
					modelTypes = new byte[23];
					modelIds = new int[23][];
					for (index = 0; index <= 22; index++) {
						modelTypes[index] = ((byte) index);
						modelIds[index] = models;
					}
				}
```
 
Most of the osrs definitions can also be found in this tool.

## Creating a new packer
inherit from IDataPacker and fill in the methods.
