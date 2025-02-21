# raw_dir.h


## Overview

Provides APIs for operating the **rawfile** directory, including traversing and closing the **rawfile** directory.

**Since**: 8

**Related module**: [Rawfile] (rawfile.md)


## Summary


### Types

| Name| Description| 
| -------- | -------- |
| [RawDir](rawfile.md#rawdir) | Provides access to the **rawfile** directory.| 


### Functions

| Name| Description| 
| -------- | -------- |
| [OH_ResourceManager_GetRawFileName](rawfile.md#oh_resourcemanager_getrawfilename) ([RawDir](rawfile.md#rawdir) \*rawDir, int index) | Obtains the name of a rawfile based on the index.| 
| [OH_ResourceManager_GetRawFileCount](rawfile.md#oh_resourcemanager_getrawfilecount) ([RawDir](rawfile.md#rawdir) \*rawDir) | Obtains the number of files in the [RawDir](rawfile.md#rawdir) directory.| 
| [OH_ResourceManager_CloseRawDir](rawfile.md#oh_resourcemanager_closerawdir) ([RawDir](rawfile.md#rawdir) \*rawDir) | Closes a [RawDir](rawfile.md#rawdir) and releases all associated resources.| 
