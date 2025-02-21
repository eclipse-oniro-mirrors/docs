# @ohos.print (Print)

The **print** module provides APIs for basic print operations.

> **NOTE**
>
> The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```ts
import print from '@ohos.print';
```

## PrintTask

Implements event listeners for print tasks.

### on

on(type: 'block', callback: Callback&lt;void&gt;): void

Registers a listener for the print task blocking event. This API uses a callback to return the result.

**Required permissions**: ohos.permission.PRINT

**System capability**: SystemCapability.Print.PrintFramework

**Parameters**
| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Listening type.<br>The value is fixed at **'block'**, indicating blocking of the print task.|
| callback | Callback&lt;void&gt; | Yes| Callback used to return the result.|

**Example**

```ts
import print from '@ohos.print';
import { BusinessError } from '@ohos.base';

let file = ['file://data/print/a.png', 'file://data/print/b.png'];
print.print(file).then((printTask: print.PrintTask) => {
    printTask.on('block', () => {
        console.log('print state is block');
    })
    // ...
}).catch((error: BusinessError) => {
    console.log('print err ' + JSON.stringify(error));
})
```

### on

on(type: 'succeed', callback: Callback&lt;void&gt;): void

Registers a listener for the print task success event. This API uses a callback to return the result.

**Required permissions**: ohos.permission.PRINT

**System capability**: SystemCapability.Print.PrintFramework

**Parameters**
| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Listening type.<br>The value is fixed at **'succeed'**, indicating success of the print task.|
| callback | Callback&lt;void&gt; | Yes| Callback used to return the result.|

**Example**

```ts
import print from '@ohos.print';
import { BusinessError } from '@ohos.base';

let file = ['file://data/print/a.png', 'file://data/print/b.png'];
print.print(file).then((printTask: print.PrintTask) => {
    printTask.on('succeed', () => {
        console.log('print state is succeed');
    })
    // ...
}).catch((error: BusinessError) => {
    console.log('print err ' + JSON.stringify(error));
})
```

### on

on(type: 'fail', callback: Callback&lt;void&gt;): void

Registers a listener for the print task failure event. This API uses a callback to return the result.

**Required permissions**: ohos.permission.PRINT

**System capability**: SystemCapability.Print.PrintFramework

**Parameters**
| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Listening type.<br>The value is fixed at **'fail'**, indicating failure of the print task.|
| callback | Callback&lt;void&gt; | Yes| Callback used to return the result.|

**Example**

```ts
import print from '@ohos.print';
import { BusinessError } from '@ohos.base';

let file = ['file://data/print/a.png', 'file://data/print/b.png'];
print.print(file).then((printTask: print.PrintTask) => {
    printTask.on('fail', () => {
        console.log('print state is fail');
    })
    // ...
}).catch((error: BusinessError) => {
    console.log('print err ' + JSON.stringify(error));
})
```

### on

on(type: 'cancel', callback: Callback&lt;void&gt;): void

Registers a listener for the print task cancel event. This API uses a callback to return the result.

**Required permissions**: ohos.permission.PRINT

**System capability**: SystemCapability.Print.PrintFramework

**Parameters**
| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Listening type.<br>The value is fixed at **'cancel'**, indicating canceling of the print task.|
| callback | Callback&lt;void&gt; | Yes| Callback used to return the result.|

**Example**

```ts
import print from '@ohos.print';
import { BusinessError } from '@ohos.base';

let file = ['file://data/print/a.png', 'file://data/print/b.png'];
print.print(file).then((printTask: print.PrintTask) => {
    printTask.on('cancel', () => {
        console.log('print state is cancel');
    })
    // ...
}).catch((error: BusinessError) => {
    console.log('print err ' + JSON.stringify(error));
})
```

### off

off(type: 'block', callback?: Callback&lt;void&gt;): void

Unregisters the listener for the print task blocking event. This API uses a callback to return the result.

**Required permissions**: ohos.permission.PRINT

**System capability**: SystemCapability.Print.PrintFramework

**Parameters**
| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Listening type.<br>The value is fixed at **'block'**, indicating blocking of the print task.|
| callback | Callback&lt;void&gt; | No| Callback used to return the result.|

**Example**

```ts
import print from '@ohos.print';
import { BusinessError } from '@ohos.base';

let file = ['file://data/print/a.png', 'file://data/print/b.png'];
print.print(file).then((printTask: print.PrintTask) => {
    printTask.off('block', () => {
        console.log('unregister state block');
    })
    // ...
}).catch((error: BusinessError) => {
    console.log('print err ' + JSON.stringify(error));
})
```

### off

off(type: 'succeed', callback?: Callback&lt;void&gt;): void

Unregisters the listener for the print task success event. This API uses a callback to return the result.

**Required permissions**: ohos.permission.PRINT

**System capability**: SystemCapability.Print.PrintFramework

**Parameters**
| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Listening type.<br>The value is fixed at **'succeed'**, indicating success of the print task.|
| callback | Callback&lt;void&gt; | No| Callback used to return the result.|

**Example**

```ts
import print from '@ohos.print';
import { BusinessError } from '@ohos.base';

let file = ['file://data/print/a.png', 'file://data/print/b.png'];
print.print(file).then((printTask: print.PrintTask) => {
    printTask.off('succeed', () => {
        console.log('unregister state succeed');
    })
    // ...
}).catch((error: BusinessError) => {
    console.log('print err ' + JSON.stringify(error));
})
```

### off

off(type: 'fail', callback?: Callback&lt;void&gt;): void

Unregisters the listener for the print task failure event. This API uses a callback to return the result.

**Required permissions**: ohos.permission.PRINT

**System capability**: SystemCapability.Print.PrintFramework

**Parameters**
| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Listening type.<br>The value is fixed at **'fail'**, indicating failure of the print task.|
| callback | Callback&lt;void&gt; | No| Callback used to return the result.|

**Example**

```ts
import print from '@ohos.print';
import { BusinessError } from '@ohos.base';

let file = ['file://data/print/a.png', 'file://data/print/b.png'];
print.print(file).then((printTask: print.PrintTask) => {
    printTask.off('fail', () => {
        console.log('unregister state fail');
    })
    // ...
}).catch((error: BusinessError) => {
    console.log('print err ' + JSON.stringify(error));
})
```

### off

off(type: 'cancel', callback?: Callback&lt;void&gt;): void

Unregisters the listener for the print task cancel event. This API uses a callback to return the result.

**Required permissions**: ohos.permission.PRINT

**System capability**: SystemCapability.Print.PrintFramework

**Parameters**
| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Listening type.<br>The value is fixed at **'cancel'**, indicating canceling of the print task.|
| callback | Callback&lt;void&gt; | No| Callback used to return the result.|

**Example**

```ts
import print from '@ohos.print';
import { BusinessError } from '@ohos.base';

let file = ['file://data/print/a.png', 'file://data/print/b.png'];
print.print(file).then((printTask: print.PrintTask) => {
    printTask.off('cancel', () => {
        console.log('unregister state cancel');
    })
    // ...
}).catch((error: BusinessError) => {
    console.log('print err ' + JSON.stringify(error));
})
```

## PrintDocumentAdapter<sup>11+</sup>

Provides information about the document to print. This API must be implemented by a third-party application.

### onStartLayoutWrite

onStartLayoutWrite(jobId: string, oldAttrs: PrintAttributes, newAttrs: PrintAttributes, fd: number, writeResultCallback: (jobId: string, writeResult: PrintFileCreationState) => void): void

Updates the file to be printed. This API uses **writeResultCallback** as the callback.

**Required permissions**: ohos.permission.PRINT

**System capability**: SystemCapability.Print.PrintFramework

**Parameters**
| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| jobId | string | Yes| ID of the print job.|
| oldAttrs | PrintAttributes | Yes| Old print attributes.|
| newAttrs | PrintAttributes | Yes| New print attributes.|
| fd | number | Yes| File descriptor.|
| writeResultCallback | (jobId: string, writeResult: PrintFileCreationState) | Yes| Callback used to return the result.|

**Example**

```ts
import print from '@ohos.print';
import { BusinessError } from '@ohos.base';

class MyPrintDocumentAdapter implements print.PrintDocumentAdapter {
    onStartLayoutWrite(jobId: string, oldAttrs: print.PrintAttributes, newAttrs: print.PrintAttributes, fd: number,
        writeResultCallback: (jobId: string, writeResult: print.PrintFileCreationState) => void) {
        writeResultCallback(jobId, print.PrintFileCreationState.PRINT_FILE_CREATED);
    };
    onJobStateChanged(jobId: string, state: print.PrintDocumentAdapterState) {
        if (state == print.PrintDocumentAdapterState.PREVIEW_DESTROY) {
            console.log('PREVIEW_DESTROY');
        } else if (state == print.PrintDocumentAdapterState.PRINT_TASK_SUCCEED) {
            console.log('PRINT_TASK_SUCCEED');
        } else if (state == print.PrintDocumentAdapterState.PRINT_TASK_FAIL) {
            console.log('PRINT_TASK_FAIL');
        } else if (state == print.PrintDocumentAdapterState.PRINT_TASK_CANCEL) {
            console.log('PRINT_TASK_CANCEL');
        } else if (state == print.PrintDocumentAdapterState.PRINT_TASK_BLOCK) {
            console.log('PRINT_TASK_BLOCK');
        }
    }
}
```

### onJobStateChanged

onJobStateChanged(jobId: string, state: PrintDocumentAdapterState): void

Registers a listener for print job state changes.

**Required permissions**: ohos.permission.PRINT

**System capability**: SystemCapability.Print.PrintFramework

**Parameters**
| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| jobId | string | Yes| ID of the print job.|
| state | PrintDocumentAdapterState | Yes| New state of the print job.|

**Example**

```ts
import print from '@ohos.print';
import { BusinessError } from '@ohos.base';

class MyPrintDocumentAdapter implements print.PrintDocumentAdapter {
    onStartLayoutWrite(jobId: string, oldAttrs: print.PrintAttributes, newAttrs: print.PrintAttributes, fd: number,
        writeResultCallback: (jobId: string, writeResult: print.PrintFileCreationState) => void) {
        writeResultCallback(jobId, print.PrintFileCreationState.PRINT_FILE_CREATED);
    };
    onJobStateChanged(jobId: string, state: print.PrintDocumentAdapterState) {
        if (state == print.PrintDocumentAdapterState.PREVIEW_DESTROY) {
            console.log('PREVIEW_DESTROY');
        } else if (state == print.PrintDocumentAdapterState.PRINT_TASK_SUCCEED) {
            console.log('PRINT_TASK_SUCCEED');
        } else if (state == print.PrintDocumentAdapterState.PRINT_TASK_FAIL) {
            console.log('PRINT_TASK_FAIL');
        } else if (state == print.PrintDocumentAdapterState.PRINT_TASK_CANCEL) {
            console.log('PRINT_TASK_CANCEL');
        } else if (state == print.PrintDocumentAdapterState.PRINT_TASK_BLOCK) {
            console.log('PRINT_TASK_BLOCK');
        }
    }
}
```

## print

print(files: Array&lt;string&gt;, callback: AsyncCallback&lt;PrintTask&gt;): void

Prints files. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.PRINT

**System capability**: SystemCapability.Print.PrintFramework

**Parameters**
| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| file | Array&lt;string&gt; | Yes| List of files to print. Images in .jpg, .png, .gif, .bmp, or .webp format are supported.|
| callback | AsyncCallback&lt;PrintTask&gt; | Yes| Callback used to return the result.|

**Example**

```ts
import print from '@ohos.print';
import { BusinessError } from '@ohos.base';

// Pass in the URIs of the files.
let file = ['file://data/print/a.png', 'file://data/print/b.png'];
// Alternatively, pass in the file IDs.
//let file = ['fd://1', 'fd://2'];
print.print(file, (err: BusinessError, printTask: print.PrintTask) => {
    if (err) {
        console.log('print err ' + JSON.stringify(err));
    } else {
        printTask.on('succeed', () => {
            console.log('print state is succeed');
        })
        // ...
    }
})
```

## print

print(files: Array&lt;string&gt;): Promise&lt;PrintTask&gt;

Prints files. This API uses a promise to return the result.

**Required permissions**: ohos.permission.PRINT

**System capability**: SystemCapability.Print.PrintFramework

**Parameters**
| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| file | Array&lt;string&gt; | Yes| List of files to print. Images in .jpg, .png, .gif, .bmp, or .webp format are supported.|

**Return value**
| **Type**| **Description**|
| -------- | -------- |
| Promise&lt;PrintTask&gt; | Print result.|

**Example**

```ts
import print from '@ohos.print';
import { BusinessError } from '@ohos.base';

// Pass in the URIs of the files.
let file = ['file://data/print/a.png', 'file://data/print/b.png'];
// Alternatively, pass in the file IDs.
//let file = ['fd://1', 'fd://2'];
print.print(file).then((printTask: print.PrintTask) => {
    printTask.on('succeed', () => {
        console.log('print state is succeed');
    })
    // ...
}).catch((error: BusinessError) => {
    console.log('print err ' + JSON.stringify(error));
})
```

## print<sup>11+</sup>

print(files: Array&lt;string&gt;, context: Context, callback: AsyncCallback&lt;PrintTask&gt;): void

Prints files. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.PRINT

**System capability**: SystemCapability.Print.PrintFramework

**Parameters**
| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| file | Array&lt;string&gt; | Yes| List of files to print. Images in .jpg, .png, .gif, .bmp, or .webp format are supported.|
| context | Context | Yes| UIAbility context used to start printing.|
| callback | AsyncCallback&lt;PrintTask&gt; | Yes| Callback used to return the result.|

**Example**

```ts
import print from '@ohos.print';
import { BusinessError } from '@ohos.base';

// Pass in the URIs of the files.
let file = ['file://data/print/a.png', 'file://data/print/b.png'];
// Alternatively, pass in the file IDs.
//let file = ['fd://1', 'fd://2'];
let context = getContext(this);
print.print(file, context, (err: BusinessError, printTask: print.PrintTask) => {
    if (err) {
        console.log('print err ' + JSON.stringify(err));
    } else {
        printTask.on('succeed', () => {
            console.log('print state is succeed');
        })
        // ...
    }
})
```

## print<sup>11+</sup>

print(files: Array&lt;string&gt;, context: Context): Promise&lt;PrintTask&gt;

Prints files. This API uses a promise to return the result.

**Required permissions**: ohos.permission.PRINT

**System capability**: SystemCapability.Print.PrintFramework

**Parameters**
| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| file | Array&lt;string&gt; | Yes| List of files to print. Images in .jpg, .png, .gif, .bmp, or .webp format are supported.|
| context | Context | Yes| UIAbility context used to start printing.|

**Return value**
| **Type**| **Description**|
| -------- | -------- |
| Promise&lt;PrintTask&gt; | Print result.|

**Example**

```ts
import print from '@ohos.print';
import { BusinessError } from '@ohos.base';

// Pass in the URIs of the files.
let file = ['file://data/print/a.png', 'file://data/print/b.png'];
// Alternatively, pass in the file IDs.
//let file = ['fd://1', 'fd://2'];
let context = getContext(this);
print.print(file, context).then((printTask: print.PrintTask) => {
    printTask.on('succeed', () => {
        console.log('print state is succeed');
    })
    // ...
}).catch((error: BusinessError) => {
    console.log('print err ' + JSON.stringify(error));
})
```

## print<sup>11+</sup>

print(jobName: string, printAdapter: PrintDocumentAdapter, printAttributes: PrintAttributes, context: Context): Promise&lt;PrintTask&gt;

Prints a file. This API uses a promise to return the result.

**Required permissions**: ohos.permission.PRINT

**System capability**: SystemCapability.Print.PrintFramework

**Parameters**
| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| jobName | string | Yes| Name of the file to print.|
| printAdapter | PrintDocumentAdapter | Yes| Feature implemented by a third-party application.|
| printAttributes | PrintAttributes | Yes| Print attributes.|
| context | Context | Yes| UIAbility context used to start printing.|

**Return value**
| **Type**| **Description**|
| -------- | -------- |
| Promise&lt;PrintTask&gt; | Print result.|

**Example**

```ts
import print from '@ohos.print';
import { BusinessError } from '@ohos.base';

let jobName : string = "jobName";
let printAdapter : print.PrintDocumentAdapter | null = null;
let printAttributes : print.PrintAttributes = {
    copyNumber: 1,
    pageRange: {
        startPage: 0,
        endPage: 5,
        pages: []
    },
    pageSize: print.PrintPageType.PAGE_ISO_A3,
    directionMode: print.PrintDirectionMode.DIRECTION_MODE_AUTO,
    colorMode: print.PrintColorMode.COLOR_MODE_MONOCHROME,
    duplexMode: print.PrintDuplexMode.DUPLEX_MODE_NONE
}
let context = getContext();

print.print(jobName, printAdapter, printAttributes, context).then((printTask: print.PrintTask) => {
    printTask.on('succeed', () => {
        console.log('print state is succeed');
    })
    // ...
}).catch((error: BusinessError) => {
    console.log('print err ' + JSON.stringify(error));
})
```

## PrintAttributes<sup>11+</sup>

Defines the print attributes.

**System capability**: SystemCapability.Print.PrintFramework

**Attributes**
| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| copyNumber | number | No| Copy of the file list.|
| pageRange | PrintPageRange | No| Range of pages to print.|
| pageSize | PrintPageSize \| PrintPageType | No| Page size of the files to print.|
| directionMode | PrintDirectionMode | No| Print direction mode.|
| colorMode | PrintColorMode | No| Color mode of the files to print.|
| duplexMode | PrintDuplexMode | No| Duplex mode of the files to print.|

## PrintPageRange<sup>11+</sup>

Defines the print range.

**System capability**: SystemCapability.Print.PrintFramework

**Attributes**
| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| startPage | number | No| Start page.|
| endPage | number | No| End page.|
| pages | Array&lt;number&gt; | No| Discrete pages.|


## PrintPageSize<sup>11+</sup>

Defines the size of the printed page.

**System capability**: SystemCapability.Print.PrintFramework

**Attributes**
| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| id | string | Yes| Page size ID.|
| name | string | Yes| Page size name.|
| width | number | Yes| Page width, in millimeters.|
| height | number | Yes| Page height, in millimeters.|



## PrintDirectionMode<sup>11+</sup>

Enumerates the print direction modes.

**System capability**: SystemCapability.Print.PrintFramework

| **Name**| **Value**| **Description**|
| -------- | -------- | -------- |
| DIRECTION_MODE_AUTO | 0 | Automatic.|
| DIRECTION_MODE_PORTRAIT | 1 | Portrait mode.|
| DIRECTION_MODE_LANDSCAPE | 2 | Landscape mode.|

## PrintColorMode<sup>11+</sup>

Enumerates the color modes.

**System capability**: SystemCapability.Print.PrintFramework

| **Name**| **Value**| **Description**|
| -------- | -------- | -------- |
| COLOR_MODE_MONOCHROME | 0 | Black and white.|
| COLOR_MODE_COLOR | 1 | Color.|

## PrintDuplexMode<sup>11+</sup>

Enumerates the duplex modes.

**System capability**: SystemCapability.Print.PrintFramework

| **Name**| **Value**| **Description**|
| -------- | -------- | -------- |
| DUPLEX_MODE_NONE | 0 | Simplex (single-sided).|
| DUPLEX_MODE_LONG_EDGE | 1 | Duplex (double-sided) with flipping on long edge.|
| DUPLEX_MODE_SHORT_EDGE | 2 | Duplex (double-sided) with flipping on short edge.|

## PrintPageType<sup>11+</sup>

Enumerates the print page types.

**System capability**: SystemCapability.Print.PrintFramework

| **Name**| **Value**| **Description**|
| -------- | -------- | -------- |
| PAGE_ISO_A3 | 0 | A3.|
| PAGE_ISO_A4 | 1 | A4.|
| PAGE_ISO_A5 | 2 | A5.|
| PAGE_JIS_B5 | 3 | B5.|
| PAGE_ISO_C5 | 4 | C5.|
| PAGE_ISO_DL | 5 | DL.|
| PAGE_LETTER | 6 | Letter.|
| PAGE_LEGAL | 7 | Legal.|
| PAGE_PHOTO_4X6 | 8 | 4 x 6 photo paper.|
| PAGE_PHOTO_5X7 | 9 | 5 x 7 photo paper.|
| PAGE_INT_DL_ENVELOPE | 10 | International envelope DL.|
| PAGE_B_TABLOID | 11 | B Tabloid.|

## PrintDocumentAdapterState<sup>11+</sup>

Enumerates the print job states.

**System capability**: SystemCapability.Print.PrintFramework

| **Name**| **Value**| **Description**|
| -------- | -------- | -------- |
| PREVIEW_DESTROY | 0 | The preview fails.|
| PRINT_TASK_SUCCEED | 1 | The print job is successful.|
| PRINT_TASK_FAIL | 2 | The print job failed.|
| PRINT_TASK_CANCEL | 3 | The print job is canceled.|
| PRINT_TASK_BLOCK | 4 | The print job is blocked.|

## PrintFileCreationState<sup>11+</sup>

Enumerates the print file creation status.

**System capability**: SystemCapability.Print.PrintFramework

| **Name**| **Value**| **Description**|
| -------- | -------- | -------- |
| PRINT_FILE_CREATED | 0 | The print file is created successfully.|
| PRINT_FILE_CREATION_FAILED | 1 | The print file fails to be created.|
| PRINT_FILE_CREATED_UNRENDERED | 2 | The print file is successfully created but not rendered.|
