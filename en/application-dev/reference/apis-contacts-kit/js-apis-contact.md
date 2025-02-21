# @ohos.contact (Contacts)

The **contact** module provides contact management functions, such as adding, deleting, and updating contacts.

>**NOTE**
>
>The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```
import contact from '@ohos.contact';
```

## contact.addContact<sup>10+</sup>

addContact(context: Context, contact: Contact, callback: AsyncCallback&lt;number&gt;): void 

Adds a contact. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.WRITE_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                       | Mandatory| Description                                                        |
| -------- | --------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                     | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| contact  | [Contact](#contact)         | Yes  | Contact information.                                                |
| callback | AsyncCallback&lt;number&gt; | Yes  | Callback used to return the result. If the operation is successful, the ID of the added contact is returned. If the operation fails, an invalid contact ID is returned.                              |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.addContact(
    context,
    {name: {fullName: 'xxx'},
      phoneNumbers: [{phoneNumber: '138xxxxxxxx'}]
    }, (err: BusinessError, data) => {
      if (err) {
        console.log(`addContact callback: err->${JSON.stringify(err)}`);
        return;
      }
      console.log(`addContact callback: success data->${JSON.stringify(data)}`);
  });
```

## contact.addContact(deprecated)<sup>7+</sup>

addContact(contact:Contact, callback:AsyncCallback&lt;number&gt;): void

Adds a contact. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [addContact](#contactaddcontact10).

**Permission required**: ohos.permission.WRITE_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                       | Mandatory| Description                          |
| -------- | --------------------------- | ---- | ------------------------------ |
| contact  | [Contact](#contact)         | Yes  | Contact information.                  |
| callback | AsyncCallback&lt;number&gt; | Yes  | Callback used to return the result, which is a contact ID.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.addContact({
      name: {fullName: 'xxx'},
      phoneNumbers: [{phoneNumber: '138xxxxxxxx'}]
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`addContact callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`addContact callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.addContact<sup>10+</sup>

addContact(context: Context, contact: Contact): Promise<number&gt;

Adds a contact. This API uses a promise to return the result.

**Permission required**: ohos.permission.WRITE_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name | Type               | Mandatory| Description                                                        |
| ------- | ------------------- | ---- | ------------------------------------------------------------ |
| context | Context             | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| contact | [Contact](#contact) | Yes  | Contact information.                                                |

**Return Value**

| Type                 | Description                                       |
| --------------------- | ------------------------------------------- |
| Promise&lt;number&gt; | Promise used to return the contact ID.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  let promise = contact.addContact(
    context,
    {name: {fullName: 'xxx'},
      phoneNumbers: [{phoneNumber: '138xxxxxxxx'}]
  });
  promise.then((data) => {
    console.log(`addContact success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
    console.error(`addContact fail: err->${JSON.stringify(err)}`);
  });
```

## contact.addContact(deprecated)<sup>7+</sup>

addContact(contact: Contact): Promise&lt;number&gt;

Adds a contact. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [addContact](#contactaddcontact10-1).

**Permission required**: ohos.permission.WRITE_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name | Type               | Mandatory| Description        |
| ------- | ------------------- | ---- | ------------ |
| contact | [Contact](#contact) | Yes  | Contact information.|

**Return Value**

| Type                 | Description                                       |
| --------------------- | ------------------------------------------- |
| Promise&lt;number&gt; | Promise used to return the contact ID.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  let promise = contact.addContact({
      name: {fullName: 'xxx'},
      phoneNumbers: [{phoneNumber: '138xxxxxxxx'}]
  });
  promise.then((data) => {
      console.log(`addContact success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`addContact fail: err->${JSON.stringify(err)}`);
  });
  ```

## contact.deleteContact<sup>10+</sup>

deleteContact(context: Context, key: string, callback: AsyncCallback&lt;void&gt;): void

Deletes a contact based on the specified contact key. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.WRITE_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                     | Mandatory| Description                                                        |
| -------- | ------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                   | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| key      | string                    | Yes  | Unique query key of a contact. One contact corresponds to one key.                        |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.                            |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context; 
  contact.deleteContact(context, 'xxx', (err: BusinessError) => {
      if (err) {
          console.log(`deleteContact callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log('deleteContact success');
  });
```

## contact.deleteContact(deprecated)<sup>7+</sup>

deleteContact(key: string, callback: AsyncCallback&lt;void&gt;): void

Deletes a contact based on the specified contact key. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [deleteContact](#contactdeletecontact10).

**Permission required**: ohos.permission.WRITE_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                     | Mandatory| Description                                |
| -------- | ------------------------- | ---- | ------------------------------------ |
| key      | string                    | Yes  | Unique query key of a contact. One contact corresponds to one key.|
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.    |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.deleteContact('xxx', (err: BusinessError) => {
      if (err) {
          console.log(`deleteContact callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log('deleteContact success');
  });
  ```


## contact.deleteContact<sup>10+</sup>

deleteContact(context: Context,  key: string): Promise&lt;void&gt;

Deletes a contact based on the specified contact key. This API uses a promise to return the result.

**Permission required**: ohos.permission.WRITE_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name | Type   | Mandatory| Description                                                        |
| ------- | ------- | ---- | ------------------------------------------------------------ |
| context | Context | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| key     | string  | Yes  | Unique query key of a contact. One contact corresponds to one key.                      |

**Return Value**

| Type               | Description                                         |
| ------------------- | --------------------------------------------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  let promise = contact.deleteContact(context, 'xxx');
  promise.then(() => {
      console.log(`deleteContact success`);
  }).catch((err: BusinessError) => {
      console.error(`deleteContact fail: err->${JSON.stringify(err)}`);
  });
  ```

## contact.deleteContact(deprecated)<sup>7+</sup>

deleteContact(key: string): Promise&lt;void&gt;

Deletes a contact based on the specified contact key. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [deleteContact](#contactdeletecontact10-1).

**Permission required**: ohos.permission.WRITE_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name| Type  | Mandatory| Description                                  |
| ------ | ------ | ---- | -------------------------------------- |
| key    | string | Yes  | Unique query key of a contact. One contact corresponds to one key.|

**Return Value**

| Type               | Description                                         |
| ------------------- | --------------------------------------------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  let promise = contact.deleteContact('xxx');
  promise.then(() => {
      console.log(`deleteContact success`);
  }).catch((err: BusinessError) => {
      console.error(`deleteContact fail: err->${JSON.stringify(err)}`);
  });
  ```


## contact.updateContact<sup>10+</sup>

updateContact(context: Context, contact: Contact, callback: AsyncCallback&lt;void&gt;): void

Updates a contact based on the specified contact information. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.WRITE_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                     | Mandatory| Description                                                        |
| -------- | ------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                   | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| contact  | [Contact](#contact)       | Yes  | Contact information. Contact ID, which is mandatory.                                                |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.                        |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.updateContact(context, {
      id: 1,
      name: {fullName: 'xxx'},
      phoneNumbers: [{phoneNumber: '138xxxxxxxx'}]
  }, (err: BusinessError) => {
      if (err) {
          console.log(`updateContact callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log('updateContact success');
  });
  ```

## contact.updateContact(deprecated)<sup>7+</sup>

updateContact(contact: Contact, callback: AsyncCallback&lt;void&gt;): void

Updates a contact based on the specified contact information. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [updateContact](#contactupdatecontact10).

**Permission required**: ohos.permission.WRITE_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                     | Mandatory| Description                                |
| -------- | ------------------------- | ---- | ------------------------------------ |
| contact  | [Contact](#contact)       | Yes  | Contact information. Contact ID, which is mandatory.                        |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.updateContact({
      id: 1,
      name: {fullName: 'xxx'},
      phoneNumbers: [{phoneNumber: '138xxxxxxxx'}]
  }, (err: BusinessError) => {
      if (err) {
          console.log(`updateContact callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log('updateContact success');
  });
  ```


## contact.updateContact<sup>10+</sup>

updateContact(context: Context,  contact: Contact, attrs: ContactAttributes, callback: AsyncCallback&lt;void&gt;): void

Updates a contact based on the specified contact information. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.WRITE_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                   | Mandatory| Description                                                        |
| -------- | --------------------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                                 | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| contact  | [Contact](#contact)                     | Yes  | Contact information. Contact ID, which is mandatory.                                               |
| attrs    | [ContactAttributes](#contactattributes) | Yes  | List of contact attributes.                                          |
| callback | AsyncCallback&lt;void&gt;               | Yes  | Callback used to return the result.                        |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.updateContact(context, {
      id: 1,
      name: {fullName: 'xxx'},
      phoneNumbers: [{phoneNumber: '138xxxxxxxx'}]
  }, {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  }, (err: BusinessError) => {
      if (err) {
          console.log(`updateContact callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log('updateContact success');
  });
  ```

## contact.updateContact(deprecated)<sup>7+</sup>

updateContact(contact: Contact, attrs: ContactAttributes, callback: AsyncCallback&lt;void&gt;): void

Updates a contact based on the specified contact information. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [updateContact](#contactupdatecontact10-1).

**Permission required**: ohos.permission.WRITE_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                   | Mandatory| Description                                |
| -------- | --------------------------------------- | ---- | ------------------------------------ |
| contact  | [Contact](#contact)                     | Yes  | Contact information. Contact ID, which is mandatory.                        |
| attrs    | [ContactAttributes](#contactattributes) | Yes  | List of contact attributes.                  |
| callback | AsyncCallback&lt;void&gt;               | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.updateContact({
      id: 1,
      name: {fullName: 'xxx'},
      phoneNumbers: [{phoneNumber: '138xxxxxxxx'}]
  }, {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  }, (err: BusinessError) => {
      if (err) {
          console.log(`updateContact callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log('updateContact success');
  });
  ```


## contact.updateContact<sup>10+</sup>

updateContact(context: Context,  contact: Contact, attrs?: ContactAttributes): Promise&lt;void&gt;

Updates a contact based on the specified contact information and attributes. This API uses a promise to return the result.

**Permission required**: ohos.permission.WRITE_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name | Type                                   | Mandatory| Description                                                        |
| ------- | --------------------------------------- | ---- | ------------------------------------------------------------ |
| context | Context                                 | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| contact | [Contact](#contact)                     | Yes  | Contact information. Contact ID, which is mandatory.                                                |
| attrs   | [ContactAttributes](#contactattributes) | No  | List of contact attributes.                                          |

**Return Value**

| Type               | Description                                             |
| ------------------- | ------------------------------------------------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  let promise = contact.updateContact(context, {
      id: 1,
      name: {fullName: 'xxx'},
      phoneNumbers: [{phoneNumber: '138xxxxxxxx'}]
  }, {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  });
  promise.then(() => {
      console.log('updateContact success');
  }).catch((err: BusinessError) => {
      console.error(`updateContact fail: err->${JSON.stringify(err)}`);
  });
```

## contact.updateContact(deprecated)<sup>7+</sup>

updateContact(contact: Contact, attrs?: ContactAttributes): Promise&lt;void&gt;

Updates a contact based on the specified contact information and attributes. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [updateContact](#contactupdatecontact10-2).

**Permission required**: ohos.permission.WRITE_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name | Type                                   | Mandatory| Description              |
| ------- | --------------------------------------- | ---- | ------------------ |
| contact | [Contact](#contact)                     | Yes  | Contact information. Contact ID, which is mandatory.      |
| attrs   | [ContactAttributes](#contactattributes) | No  | List of contact attributes.|

**Return Value**
| Type               | Description                                             |
| ------------------- | ------------------------------------------------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  let promise = contact.updateContact({
      id: 1,
      name: {fullName: 'xxx'},
      phoneNumbers: [{phoneNumber: '138xxxxxxxx'}]
  }, {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  });
  promise.then(() => {
      console.log('updateContact success');
  }).catch((err: BusinessError) => {
      console.error(`updateContact fail: err->${JSON.stringify(err)}`);
  });
  ```


## contact.isLocalContact<sup>10+</sup>

isLocalContact(context: Context,  id: number, callback: AsyncCallback&lt;boolean&gt;): void

Checks whether the ID of this contact is in the local address book. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                        | Mandatory| Description                                                        |
| -------- | ---------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                      | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| id       | number                       | Yes  | Contact ID. Each contact corresponds to one ID.                  |
| callback | AsyncCallback&lt;boolean&gt; | Yes  | Callback used to return the result. The value **true** indicates that the contact ID is in the local address book, and the value **false** indicates the opposite.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.isLocalContact(context, /*id*/1, (err: BusinessError, data) => {
      if (err) {
          console.log(`isLocalContact callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`isLocalContact callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.isLocalContact(deprecated)<sup>7+</sup>

isLocalContact(id: number, callback: AsyncCallback&lt;boolean&gt;): void

Checks whether the ID of this contact is in the local address book. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [isLocalContact](#contactislocalcontact10).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                        | Mandatory| Description                                                        |
| -------- | ---------------------------- | ---- | ------------------------------------------------------------ |
| id       | number                       | Yes  | Contact ID. Each contact corresponds to one ID.                  |
| callback | AsyncCallback&lt;boolean&gt; | Yes  | Callback used to return the result. The value **true** indicates that the contact ID is in the local address book, and the value **false** indicates the opposite.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.isLocalContact(/*id*/1, (err: BusinessError, data) => {
      if (err) {
          console.log(`isLocalContact callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`isLocalContact callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.isLocalContact<sup>10+</sup>

isLocalContact(context: Context,  id: number): Promise&lt;boolean&gt;

Checks whether the ID of this contact is in the local address book. This API uses a promise to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name | Type   | Mandatory| Description                                                        |
| ------- | ------- | ---- | ------------------------------------------------------------ |
| context | Context | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| id      | number  | Yes  | Contact ID. Each contact corresponds to one ID.                  |

**Return Value**

| Type                  | Description                                                        |
| ---------------------- | ------------------------------------------------------------ |
| Promise&lt;boolean&gt; | Promise used to return the result. The value **true** indicates that the contact ID is in the local address book, and the value **false** indicates the opposite.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  let promise = contact.isLocalContact(context, /*id*/1);
  promise.then((data) => {
      console.log(`isLocalContact success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`isLocalContact fail: err->${JSON.stringify(err)}`);
  });
```

## contact.isLocalContact(deprecated)<sup>7+</sup>

isLocalContact(id: number): Promise&lt;boolean&gt;

Checks whether the ID of this contact is in the local address book. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [isLocalContact](#contactislocalcontact10-1).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name| Type  | Mandatory| Description                                      |
| ------ | ------ | ---- | ------------------------------------------ |
| id     | number | Yes  | Contact ID. Each contact corresponds to one ID.|

**Return Value**

| Type                  | Description                                                        |
| ---------------------- | ------------------------------------------------------------ |
| Promise&lt;boolean&gt; | Promise used to return the result. The value **true** indicates that the contact ID is in the local address book, and the value **false** indicates the opposite.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  let promise = contact.isLocalContact(/*id*/1);
  promise.then((data) => {
      console.log(`isLocalContact success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`isLocalContact fail: err->${JSON.stringify(err)}`);
  });
  ```

## contact.isMyCard<sup>10+</sup>

isMyCard(context: Context,  id: number, callback: AsyncCallback&lt;boolean&gt;): void

Checks whether a contact is included in my card. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                        | Mandatory| Description                                                        |
| -------- | ---------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                      | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| id       | number                       | Yes  | Contact ID.                                        |
| callback | AsyncCallback&lt;boolean&gt; | Yes  | Callback used to return the result. The value **true** indicates that the contact is included in my card, and the value **false** indicates the opposite.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.isMyCard(context, /*id*/1, (err: BusinessError, data) => {
      if (err) {
          console.log(`isMyCard callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`isMyCard callback: success data->${JSON.stringify(data)}`);
  });
```

## contact.isMyCard(deprecated)<sup>7+</sup>

isMyCard(id: number, callback: AsyncCallback&lt;boolean&gt;): void

Checks whether a contact is included in my card. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [isMyCard](#contactismycard10).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                        | Mandatory| Description                                                        |
| -------- | ---------------------------- | ---- | ------------------------------------------------------------ |
| id       | number                       | Yes  | Contact ID.                                        |
| callback | AsyncCallback&lt;boolean&gt; | Yes  | Callback used to return the result. The value **true** indicates that the contact is included in my card, and the value **false** indicates the opposite.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.isMyCard(/*id*/1, (err: BusinessError, data) => {
      if (err) {
          console.log(`isMyCard callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`isMyCard callback: success data->${JSON.stringify(data)}`);
  });
  ```


## contact.isMyCard<sup>10+</sup>

isMyCard(context: Context,  id: number): Promise&lt;boolean&gt;

Checks whether a contact is included in my card. This API uses a promise to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name | Type   | Mandatory| Description                                                        |
| ------- | ------- | ---- | ------------------------------------------------------------ |
| context | Context | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| id      | number  | Yes  | Contact ID.                                        |

**Return Value**

| Type                  | Description                                                        |
| ---------------------- | ------------------------------------------------------------ |
| Promise&lt;boolean&gt; | Promise used to return the result. The value **true** indicates that the contact is included in my card, and the value **false** indicates the opposite.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  let promise = contact.isMyCard(context, /*id*/1);
  promise.then((data) => {
      console.log(`isMyCard success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`isMyCard fail: err->${JSON.stringify(err)}`);
  });
```

## contact.isMyCard(deprecated)<sup>7+</sup>

isMyCard(id: number): Promise&lt;boolean&gt;

Checks whether a contact is included in my card. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [isMyCard](#contactismycard10-1).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name| Type  | Mandatory| Description                |
| ------ | ------ | ---- | -------------------- |
| id     | number | Yes  | Contact ID.|

**Return Value**

| Type                  | Description                                                        |
| ---------------------- | ------------------------------------------------------------ |
| Promise&lt;boolean&gt; | Promise used to return the result. The value **true** indicates that the contact is included in my card, and the value **false** indicates the opposite.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  let promise = contact.isMyCard(/*id*/1);
  promise.then((data) => {
      console.log(`isMyCard success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`isMyCard fail: err->${JSON.stringify(err)}`);
  });
  ```

## contact.queryMyCard<sup>10+</sup>

queryMyCard(context: Context,  callback: AsyncCallback&lt;Contact&gt;): void

Queries my card. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                    | Mandatory| Description                                                        |
| -------- | ---------------------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                                  | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| callback | AsyncCallback&lt;[Contact](#contact)&gt; | Yes  | Callback used to return the result.                              |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryMyCard(context, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryMyCard callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryMyCard callback: success data->${JSON.stringify(data)}`);
  });
```

## contact.queryMyCard(deprecated)<sup>7+</sup>

queryMyCard(callback: AsyncCallback&lt;Contact&gt;): void

Queries my card. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryMyCard](#contactquerymycard10).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                    | Mandatory| Description                          |
| -------- | ---------------------------------------- | ---- | ------------------------------ |
| callback | AsyncCallback&lt;[Contact](#contact)&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryMyCard((err: BusinessError, data) => {
      if (err) {
          console.log(`queryMyCard callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryMyCard callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryMyCard<sup>10+</sup>

queryMyCard(context: Context,  attrs: ContactAttributes, callback: AsyncCallback&lt;Contact&gt;): void

Queries my card. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                    | Mandatory| Description                                                        |
| -------- | ---------------------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                                  | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| attrs    | [ContactAttributes](#contactattributes)  | Yes  | List of contact attributes.                                          |
| callback | AsyncCallback&lt;[Contact](#contact)&gt; | Yes  | Callback used to return the result.                              |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryMyCard(context, {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryMyCard callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryMyCard callback: success data->${JSON.stringify(data)}`);
  });
```

## contact.queryMyCard(deprecated)<sup>7+</sup>

queryMyCard(attrs: ContactAttributes, callback: AsyncCallback&lt;Contact&gt;): void

Queries my card. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryMyCard](#contactquerymycard10-1).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                    | Mandatory| Description                          |
| -------- | ---------------------------------------- | ---- | ------------------------------ |
| attrs    | [ContactAttributes](#contactattributes)  | Yes  | List of contact attributes.            |
| callback | AsyncCallback&lt;[Contact](#contact)&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryMyCard({
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryMyCard callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryMyCard callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryMyCard<sup>10+</sup>

queryMyCard(context: Context,  attrs?: ContactAttributes): Promise&lt;Contact&gt;

Queries my card based on the specified contact attributes. This API uses a promise to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name | Type                                   | Mandatory| Description                                                        |
| ------- | --------------------------------------- | ---- | ------------------------------------------------------------ |
| context | Context                                 | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| attrs   | [ContactAttributes](#contactattributes) | No  | List of contact attributes.                                          |

**Return Value**

| Type                              | Description                                       |
| ---------------------------------- | ------------------------------------------- |
| Promise&lt;[Contact](#contact)&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  let promise = contact.queryMyCard(context, {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  });
  promise.then((data) => {
      console.log(`queryMyCard success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`queryMyCard fail: err->${JSON.stringify(err)}`);
  });
```

## contact.queryMyCard(deprecated)<sup>7+</sup>

queryMyCard(attrs?: ContactAttributes): Promise&lt;Contact&gt;

Queries my card based on the specified contact attributes. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryMyCard](#contactquerymycard10-2).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name| Type                                   | Mandatory| Description              |
| ------ | --------------------------------------- | ---- | ------------------ |
| attrs  | [ContactAttributes](#contactattributes) | No  | List of contact attributes.|

**Return Value**
| Type                              | Description                                       |
| ---------------------------------- | ------------------------------------------- |
| Promise&lt;[Contact](#contact)&gt; | Promise used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  let promise = contact.queryMyCard({
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  });
  promise.then((data) => {
      console.log(`queryMyCard success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`queryMyCard fail: err->${JSON.stringify(err)}`);
  });
  ```


## contact.selectContact(deprecated)<sup>7+</sup>

selectContact(callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Selects a contact. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [selectContacts](#contactselectcontacts10).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.Contacts

**Parameters**

| Name  | Type                                                 | Mandatory| Description                                |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------ |
| callback | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.selectContact((err: BusinessError, data) => {
      if (err) {
          console.log(`selectContact callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`selectContact callback: success data->${JSON.stringify(data)}`);
  });
  ```


## contact.selectContact(deprecated)<sup>7+</sup>

selectContact(): Promise&lt;Array&lt;Contact&gt;&gt;

Selects a contact. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [selectContacts](#contactselectcontacts10-1).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.Contacts

**Return Value**

| Type                                           | Description                                             |
| ----------------------------------------------- | ------------------------------------------------- |
| Promise&lt;Array&lt;[Contact](#contact)&gt;&gt; | Promise used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  let promise = contact.selectContact();
  promise.then((data) => {
      console.log(`selectContact success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`selectContact fail: err->${JSON.stringify(err)}`);
  });
  ```

## contact.selectContacts<sup>10+</sup>

selectContacts(callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Selects a contact. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Applications.Contacts

**Parameters**

| Name  | Type                                                 | Mandatory| Description                                |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------ |
| callback | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.selectContacts((err: BusinessError, data) => {
      if (err) {
          console.log(`selectContacts callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`selectContacts callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.selectContacts<sup>10+</sup>

selectContacts(): Promise&lt;Array&lt;Contact&gt;&gt;

Selects a contact. This API uses a promise to return the result.

**System capability**: SystemCapability.Applications.Contacts

**Return Value**

| Type                                           | Description                                             |
| ----------------------------------------------- | ------------------------------------------------- |
| Promise&lt;Array&lt;[Contact](#contact)&gt;&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  let promise = contact.selectContacts();
  promise.then((data) => {
      console.log(`selectContacts success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`selectContacts fail: err->${JSON.stringify(err)}`);
  });
  ```

## contact.selectContacts<sup>10+</sup>

selectContacts(options: ContactSelectionOptions, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Selects a contact. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Applications.Contacts

**Parameters**

| Name  | Type                                                 | Mandatory| Description                                |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------ |
| options | [ContactSelectionOptions](#contactselectionoptions10) | Yes  | Contact selection options.|
| callback | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.selectContacts({
    isMultiSelect:false
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`selectContacts callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`selectContacts callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.selectContacts<sup>10+</sup>

selectContacts(options: ContactSelectionOptions): Promise&lt;Array&lt;Contact&gt;&gt;

Selects a contact. This API uses a promise to return the result.

**System capability**: SystemCapability.Applications.Contacts

**Return Value**

| Type                                           | Description                                             |
| ----------------------------------------------- | ------------------------------------------------- |
| options | [ContactSelectionOptions](#contactselectionoptions10) | Yes  | Contact selection options.|
| Promise&lt;Array&lt;[Contact](#contact)&gt;&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  let promise = contact.selectContacts({isMultiSelect:false});
  promise.then((data) => {
      console.log(`selectContacts success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`selectContacts fail: err->${JSON.stringify(err)}`);
  });
  ```

## contact.queryContact<sup>10+</sup>

queryContact(context: Context,  key: string,  callback: AsyncCallback&lt;Contact&gt;): void

Queries a contact based on the specified key. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                    | Mandatory| Description                                                        |
| -------- | ---------------------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                                  | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| key      | string                                   | Yes  | Contact key. Each contact corresponds to one key.                      |
| callback | AsyncCallback&lt;[Contact](#contact)&gt; | Yes  | Callback used to return the result.                            |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryContact(context, 'xxx', (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContact callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContact callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContact(deprecated)<sup>7+</sup>

queryContact(key: string,  callback: AsyncCallback&lt;Contact&gt;): void

Queries a contact based on the specified key. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryContact](#contactquerycontact10).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                    | Mandatory| Description                                  |
| -------- | ---------------------------------------- | ---- | -------------------------------------- |
| key      | string                                   | Yes  | Contact key. Each contact corresponds to one key.|
| callback | AsyncCallback&lt;[Contact](#contact)&gt; | Yes  | Callback used to return the result.      |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryContact('xxx', (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContact callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContact callback: success data->${JSON.stringify(data)}`);
  });
  ```


## contact.queryContact<sup>10+</sup>

queryContact(context: Context,  key: string, holder: Holder, callback: AsyncCallback&lt;Contact&gt;): void

Queries a contact based on the specified key. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                    | Mandatory| Description                                                        |
| -------- | ---------------------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                                  | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| key      | string                                   | Yes  | Contact key. Each contact corresponds to one key.                      |
| holder   | [Holder](#holder)                        | Yes  | Application that creates the contacts.                                      |
| callback | AsyncCallback&lt;[Contact](#contact)&gt; | Yes  | Callback used to return the result.                            |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryContact(context, 'xxx', {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContact callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContact callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContact(deprecated)<sup>7+</sup>

queryContact(key: string, holder: Holder, callback: AsyncCallback&lt;Contact&gt;): void

Queries a contact based on the specified key. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryContact](#contactquerycontact10-1).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                    | Mandatory| Description                                  |
| -------- | ---------------------------------------- | ---- | -------------------------------------- |
| key      | string                                   | Yes  | Contact key. Each contact corresponds to one key.|
| holder   | [Holder](#holder)                        | Yes  | Application that creates the contacts.                |
| callback | AsyncCallback&lt;[Contact](#contact)&gt; | Yes  | Callback used to return the result.      |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryContact('xxx', {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContact callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContact callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContact<sup>10+</sup>

queryContact(context: Context,  key: string,  attrs: ContactAttributes, callback: AsyncCallback&lt;Contact&gt;): void

Queries a contact based on the specified key. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                    | Mandatory| Description                                                        |
| -------- | ---------------------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                                  | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| key      | string                                   | Yes  | Contact key. Each contact corresponds to one key.                      |
| attrs    | [ContactAttributes](#contactattributes)  | Yes  | List of contact attributes.                                          |
| callback | AsyncCallback&lt;[Contact](#contact)&gt; | Yes  | Callback used to return the result.                            |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryContact(context, 'xxx', {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContact callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContact callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContact(deprecated)<sup>7+</sup>

queryContact(key: string,  attrs: ContactAttributes, callback: AsyncCallback&lt;Contact&gt;): void

Queries a contact based on the specified key. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryContact](#contactquerycontact10-2).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                    | Mandatory| Description                                  |
| -------- | ---------------------------------------- | ---- | -------------------------------------- |
| key      | string                                   | Yes  | Contact key. Each contact corresponds to one key.|
| attrs    | [ContactAttributes](#contactattributes)  | Yes  | List of contact attributes.                    |
| callback | AsyncCallback&lt;[Contact](#contact)&gt; | Yes  | Callback used to return the result.      |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryContact('xxx', {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContact callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContact callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContact<sup>10+</sup>

queryContact(context: Context,  key: string, holder: Holder, attrs: ContactAttributes, callback: AsyncCallback&lt;Contact&gt;): void

Queries a contact based on the specified key. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                    | Mandatory| Description                                                        |
| -------- | ---------------------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                                  | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| key      | string                                   | Yes  | Contact key. Each contact corresponds to one key.                      |
| holder   | [Holder](#holder)                        | Yes  | Application that creates the contacts.                                      |
| attrs    | [ContactAttributes](#contactattributes)  | Yes  | List of contact attributes.                                          |
| callback | AsyncCallback&lt;[Contact](#contact)&gt; | Yes  | Callback used to return the result.                            |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryContact(context, 'xxx', {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContact callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContact callback: success data->${JSON.stringify(data)}`);
  });
```

## contact.queryContact(deprecated)<sup>7+</sup>

queryContact(key: string, holder: Holder, attrs: ContactAttributes, callback: AsyncCallback&lt;Contact&gt;): void

Queries a contact based on the specified key. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryContact](#contactquerycontact10-3).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                    | Mandatory| Description                                  |
| -------- | ---------------------------------------- | ---- | -------------------------------------- |
| key      | string                                   | Yes  | Contact key. Each contact corresponds to one key.|
| holder   | [Holder](#holder)                        | Yes  | Application that creates the contacts.                |
| attrs    | [ContactAttributes](#contactattributes)  | Yes  | List of contact attributes.                    |
| callback | AsyncCallback&lt;[Contact](#contact)&gt; | Yes  | Callback used to return the result.      |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryContact('xxx', {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContact callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContact callback: success data->${JSON.stringify(data)}`);
  });
  ```


## contact.queryContact<sup>10+</sup>

queryContact(context: Context,  key: string, holder?: Holder, attrs?: ContactAttributes): Promise&lt;Contact&gt;

Queries contacts based on the specified key, application, and attributes. This API uses a promise to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name | Type                                   | Mandatory| Description                                                        |
| ------- | --------------------------------------- | ---- | ------------------------------------------------------------ |
| context | Context                                 | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| key     | string                                  | Yes  | Contact key. Each contact corresponds to one key.                      |
| holder  | [Holder](#holder)                       | No  | Application that creates the contacts.                                      |
| attrs   | [ContactAttributes](#contactattributes) | No  | List of contact attributes.                                          |

**Return Value**
| Type                              | Description                                           |
| ---------------------------------- | ----------------------------------------------- |
| Promise&lt;[Contact](#contact)&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  let promise = contact.queryContact(context, 'xxx', {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  });
  promise.then((data) => {
      console.log(`queryContact success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`queryContact fail: err->${JSON.stringify(err)}`);
  });
  ```

## contact.queryContact(deprecated)<sup>7+</sup>

queryContact(key: string, holder?: Holder, attrs?: ContactAttributes): Promise&lt;Contact&gt;

Queries contacts based on the specified key, application, and attributes. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryContact](#contactquerycontact10-4).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name| Type                                   | Mandatory| Description                                  |
| ------ | --------------------------------------- | ---- | -------------------------------------- |
| key    | string                                  | Yes  | Contact key. Each contact corresponds to one key.|
| holder | [Holder](#holder)                       | No  | Application that creates the contacts.                |
| attrs  | [ContactAttributes](#contactattributes) | No  | List of contact attributes.                    |

**Return Value**
| Type                              | Description                                           |
| ---------------------------------- | ----------------------------------------------- |
| Promise&lt;[Contact](#contact)&gt; | Promise used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  let promise = contact.queryContact('xxx', {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  });
  promise.then((data) => {
      console.log(`queryContact success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`queryContact fail: err->${JSON.stringify(err)}`);
  });
  ```

## contact.queryContacts<sup>10+</sup>

queryContacts(context: Context,  callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries all contacts. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                                 | Mandatory| Description                                                        |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                                               | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| callback | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.                      |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryContacts(context, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContacts callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContacts callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContacts(deprecated)<sup>7+</sup>

queryContacts(callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries all contacts. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryContacts](#contactquerycontacts10).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                                 | Mandatory| Description                                  |
| -------- | ----------------------------------------------------- | ---- | -------------------------------------- |
| callback | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryContacts((err: BusinessError, data) => {
      if (err) {
          console.log(`queryContacts callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContacts callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContacts<sup>10+</sup>

queryContacts(context: Context,  holder: Holder, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries all contacts. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                                 | Mandatory| Description                                                        |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                                               | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| holder   | [Holder](#holder)                                     | Yes  | Application that creates the contacts.                                      |
| callback | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.                      |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryContacts(context, {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContacts callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContacts callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContacts(deprecated)<sup>7+</sup>

queryContacts(holder: Holder, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries all contacts. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryContacts](#contactquerycontacts10-1).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                                 | Mandatory| Description                                  |
| -------- | ----------------------------------------------------- | ---- | -------------------------------------- |
| holder   | [Holder](#holder)                                     | Yes  | Application that creates the contacts.                |
| callback | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryContacts({
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContacts callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContacts callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContacts<sup>10+</sup>

queryContacts(context: Context,  attrs: ContactAttributes, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries all contacts. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                                 | Mandatory| Description                                                        |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                                               | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| attrs    | [ContactAttributes](#contactattributes)               | Yes  | List of contact attributes.                                          |
| callback | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.                      |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryContacts(context, {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContacts callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContacts callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContacts(deprecated)<sup>7+</sup>

queryContacts(attrs: ContactAttributes, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries all contacts. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryContacts](#contactquerycontacts10-2).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                                 | Mandatory| Description                                  |
| -------- | ----------------------------------------------------- | ---- | -------------------------------------- |
| attrs    | [ContactAttributes](#contactattributes)               | Yes  | List of contact attributes.                    |
| callback | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryContacts({
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContacts callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContacts callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContacts<sup>10+</sup>

queryContacts(context: Context,  holder: Holder, attrs: ContactAttributes, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries all contacts. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                                 | Mandatory| Description                                                        |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                                               | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| holder   | [Holder](#holder)                                     | Yes  | Application that creates the contacts.                                      |
| attrs    | [ContactAttributes](#contactattributes)               | Yes  | List of contact attributes.                                          |
| callback | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.                      |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryContacts(context, {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContacts callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContacts callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContacts(deprecated)<sup>7+</sup>

queryContacts(holder: Holder, attrs: ContactAttributes, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries all contacts. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryContacts](#contactquerycontacts10-3).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                                 | Mandatory| Description                                  |
| -------- | ----------------------------------------------------- | ---- | -------------------------------------- |
| holder   | [Holder](#holder)                                     | Yes  | Application that creates the contacts.                |
| attrs    | [ContactAttributes](#contactattributes)               | Yes  | List of contact attributes.                    |
| callback | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryContacts({
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContacts callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContacts callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContacts<sup>10+</sup>

queryContacts(context: Context,  holder?: Holder, attrs?: ContactAttributes): Promise&lt;Array&lt;Contact&gt;&gt;

Queries all contacts based on the specified application and attributes. This API uses a promise to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name | Type                                   | Mandatory| Description                                                        |
| ------- | --------------------------------------- | ---- | ------------------------------------------------------------ |
| context | Context                                 | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| holder  | [Holder](#holder)                       | No  | Application that creates the contacts.                                      |
| attrs   | [ContactAttributes](#contactattributes) | No  | List of contact attributes.                                          |

**Return Value**
| Type                                           | Description                                               |
| ----------------------------------------------- | --------------------------------------------------- |
| Promise&lt;Array&lt;[Contact](#contact)&gt;&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  let promise = contact.queryContacts(context, {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  });
  promise.then((data) => {
      console.log(`queryContacts success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`queryContacts fail: err->${JSON.stringify(err)}`);
  });
  ```

## contact.queryContacts(deprecated)<sup>7+</sup>

queryContacts(holder?: Holder, attrs?: ContactAttributes): Promise&lt;Array&lt;Contact&gt;&gt;

Queries all contacts based on the specified application and attributes. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryContacts](#contactquerycontacts10-4).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name| Type                                   | Mandatory| Description                  |
| ------ | --------------------------------------- | ---- | ---------------------- |
| holder | [Holder](#holder)                       | No  | Application that creates the contacts.|
| attrs  | [ContactAttributes](#contactattributes) | No  | List of contact attributes.    |

**Return Value**

| Type                                           | Description                                               |
| ----------------------------------------------- | --------------------------------------------------- |
| Promise&lt;Array&lt;[Contact](#contact)&gt;&gt; | Promise used to return the result.|

**Example**

```js
  import { BusinessError } from '@ohos.base';
  let promise = contact.queryContacts({
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  });
  promise.then((data) => {
      console.log(`queryContacts success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`queryContacts fail: err->${JSON.stringify(err)}`);
  });
```

## contact.queryContactsByPhoneNumber<sup>10+</sup>

queryContactsByPhoneNumber(context: Context,  phoneNumber: string, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries contacts based on the specified phone number. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name     | Type                                                 | Mandatory| Description                                                        |
| ----------- | ----------------------------------------------------- | ---- | ------------------------------------------------------------ |
| context     | Context                                               | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| phoneNumber | string                                                | Yes  | Phone number of the contacts.                                          |
| callback    | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.                      |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryContactsByPhoneNumber(context, '138xxxxxxxx', (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContactsByPhoneNumber callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContactsByPhoneNumber callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContactsByPhoneNumber(deprecated)<sup>7+</sup>

queryContactsByPhoneNumber(phoneNumber: string, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries contacts based on the specified phone number. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryContactsByPhoneNumber](#contactquerycontactsbyphonenumber10).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name     | Type                                                 | Mandatory| Description                                  |
| ----------- | ----------------------------------------------------- | ---- | -------------------------------------- |
| phoneNumber | string                                                | Yes  | Phone number of the contacts.                    |
| callback    | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryContactsByPhoneNumber('138xxxxxxxx', (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContactsByPhoneNumber callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContactsByPhoneNumber callback: success data->${JSON.stringify(data)}`);
  });
  ```


## contact.queryContactsByPhoneNumber<sup>10+</sup>

queryContactsByPhoneNumber(context: Context,  phoneNumber: string, holder: Holder, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries contacts based on the specified phone number. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name     | Type                                                 | Mandatory| Description                                                        |
| ----------- | ----------------------------------------------------- | ---- | ------------------------------------------------------------ |
| context     | Context                                               | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| phoneNumber | string                                                | Yes  | Phone number of the contacts.                                          |
| holder      | [Holder](#holder)                                     | Yes  | Application that creates the contacts.                                      |
| callback    | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.                      |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryContactsByPhoneNumber(context, '138xxxxxxxx', {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContactsByPhoneNumber callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContactsByPhoneNumber callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContactsByPhoneNumber(deprecated)<sup>7+</sup>

queryContactsByPhoneNumber(phoneNumber: string, holder: Holder, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries contacts based on the specified phone number. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryContactsByPhoneNumber](#contactquerycontactsbyphonenumber10-1).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name     | Type                                                 | Mandatory| Description                                  |
| ----------- | ----------------------------------------------------- | ---- | -------------------------------------- |
| phoneNumber | string                                                | Yes  | Phone number of the contacts.                    |
| holder      | [Holder](#holder)                                     | Yes  | Application that creates the contacts.                |
| callback    | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryContactsByPhoneNumber('138xxxxxxxx', {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContactsByPhoneNumber callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContactsByPhoneNumber callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContactsByPhoneNumber<sup>10+</sup>

queryContactsByPhoneNumber(context: Context,  phoneNumber: string, attrs: ContactAttributes, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries contacts based on the specified phone number. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name     | Type                                                 | Mandatory| Description                                                        |
| ----------- | ----------------------------------------------------- | ---- | ------------------------------------------------------------ |
| context     | Context                                               | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| phoneNumber | string                                                | Yes  | Phone number of the contacts.                                          |
| attrs       | [ContactAttributes](#contactattributes)               | Yes  | List of contact attributes.                                          |
| callback    | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.                      |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryContactsByPhoneNumber(context, '138xxxxxxxx', {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContactsByPhoneNumber callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContactsByPhoneNumber callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContactsByPhoneNumber(deprecated)<sup>7+</sup>

queryContactsByPhoneNumber(phoneNumber: string, attrs: ContactAttributes, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries contacts based on the specified phone number. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryContactsByPhoneNumber](#contactquerycontactsbyphonenumber10-2).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name     | Type                                                 | Mandatory| Description                                  |
| ----------- | ----------------------------------------------------- | ---- | -------------------------------------- |
| phoneNumber | string                                                | Yes  | Phone number of the contacts.                    |
| attrs       | [ContactAttributes](#contactattributes)               | Yes  | List of contact attributes.                    |
| callback    | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryContactsByPhoneNumber('138xxxxxxxx', {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContactsByPhoneNumber callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContactsByPhoneNumber callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContactsByPhoneNumber<sup>10+</sup>

queryContactsByPhoneNumber(context: Context,  phoneNumber: string, holder: Holder, attrs: ContactAttributes, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries contacts based on the specified phone number. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name     | Type                                                 | Mandatory| Description                                                        |
| ----------- | ----------------------------------------------------- | ---- | ------------------------------------------------------------ |
| context     | Context                                               | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| phoneNumber | string                                                | Yes  | Phone number of the contacts.                                          |
| holder      | [Holder](#holder)                                     | Yes  | Application that creates the contacts.                                      |
| attrs       | [ContactAttributes](#contactattributes)               | Yes  | List of contact attributes.                                          |
| callback    | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.                      |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryContactsByPhoneNumber(context, '138xxxxxxxx', {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContactsByPhoneNumber callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContactsByPhoneNumber callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContactsByPhoneNumber(deprecated)<sup>7+</sup>

queryContactsByPhoneNumber(phoneNumber: string, holder: Holder, attrs: ContactAttributes, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries contacts based on the specified phone number. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryContactsByPhoneNumber](#contactquerycontactsbyphonenumber10-3).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name     | Type                                                 | Mandatory| Description                                  |
| ----------- | ----------------------------------------------------- | ---- | -------------------------------------- |
| phoneNumber | string                                                | Yes  | Phone number of the contacts.                    |
| holder      | [Holder](#holder)                                     | Yes  | Application that creates the contacts.                |
| attrs       | [ContactAttributes](#contactattributes)               | Yes  | List of contact attributes.                    |
| callback    | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryContactsByPhoneNumber('138xxxxxxxx', {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContactsByPhoneNumber callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContactsByPhoneNumber callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContactsByPhoneNumber<sup>10+</sup>

queryContactsByPhoneNumber(context: Context,  phoneNumber: string, holder?: Holder, attrs?: ContactAttributes): Promise&lt;Array&lt;Contact&gt;&gt;

Queries contacts based on the specified phone number, application, and attributes. This API uses a promise to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name     | Type                                   | Mandatory| Description                                                        |
| ----------- | --------------------------------------- | ---- | ------------------------------------------------------------ |
| context     | Context                                 | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| phoneNumber | string                                  | Yes  | Phone number of the contacts.                                          |
| holder      | [Holder](#holder)                       | No  | Application that creates the contacts.                                      |
| attrs       | [ContactAttributes](#contactattributes) | No  | List of contact attributes.                                          |

**Return Value**

| Type                                           | Description                                               |
| ----------------------------------------------- | --------------------------------------------------- |
| Promise&lt;Array&lt;[Contact](#contact)&gt;&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  let promise = contact.queryContactsByPhoneNumber(context, '138xxxxxxxx', {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  });
  promise.then((data) => {
      console.log(`queryContactsByPhoneNumber success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`queryContactsByPhoneNumber fail: err->${JSON.stringify(err)}`);
  });
  ```

## contact.queryContactsByPhoneNumber(deprecated)<sup>7+</sup>

queryContactsByPhoneNumber(phoneNumber: string, holder?: Holder, attrs?: ContactAttributes): Promise&lt;Array&lt;Contact&gt;&gt;

Queries contacts based on the specified phone number, application, and attributes. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryContactsByPhoneNumber](#contactquerycontactsbyphonenumber10-4).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name     | Type                                   | Mandatory| Description                  |
| ----------- | --------------------------------------- | ---- | ---------------------- |
| phoneNumber | string                                  | Yes  | Phone number of the contacts.    |
| holder      | [Holder](#holder)                       | No  | Application that creates the contacts.|
| attrs       | [ContactAttributes](#contactattributes) | No  | List of contact attributes.    |

**Return Value**

| Type                                           | Description                                               |
| ----------------------------------------------- | --------------------------------------------------- |
| Promise&lt;Array&lt;[Contact](#contact)&gt;&gt; | Promise used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  let promise = contact.queryContactsByPhoneNumber('138xxxxxxxx', {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, {
      attributes: [contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE]
  });
  promise.then((data) => {
      console.log(`queryContactsByPhoneNumber success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`queryContactsByPhoneNumber fail: err->${JSON.stringify(err)}`);
  });
  ```

## contact.queryContactsByEmail<sup>10+</sup>

queryContactsByEmail(context: Context,  email: string, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries contacts based on the specified email address. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                                 | Mandatory| Description                                                        |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                                               | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| email    | string                                                | Yes  | Email address of the contact.                                          |
| callback | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.                      |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryContactsByEmail(context, 'xxx@email.com', (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContactsByEmail callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContactsByEmail callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContactsByEmail(deprecated)<sup>7+</sup>

queryContactsByEmail(email: string, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries contacts based on the specified email address. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryContactsByEmail](#contactquerycontactsbyemail10).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                                 | Mandatory| Description                                  |
| -------- | ----------------------------------------------------- | ---- | -------------------------------------- |
| email    | string                                                | Yes  | Email address of the contact.                    |
| callback | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryContactsByEmail('xxx@email.com', (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContactsByEmail callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContactsByEmail callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContactsByEmail<sup>10+</sup>

queryContactsByEmail(context: Context,  email: string, holder: Holder, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries contacts based on the specified email address. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                                 | Mandatory| Description                                                        |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                                               | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| email    | string                                                | Yes  | Email address of the contact.                                          |
| holder   | [Holder](#holder)                                     | Yes  | Application that creates the contacts.                                      |
| callback | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.                      |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryContactsByEmail(context, 'xxx@email.com', {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContactsByEmail callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContactsByEmail callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContactsByEmail(deprecated)<sup>7+</sup>

queryContactsByEmail(email: string, holder: Holder, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries contacts based on the specified email address. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryContactsByEmail](#contactquerycontactsbyemail10-1).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                                 | Mandatory| Description                                  |
| -------- | ----------------------------------------------------- | ---- | -------------------------------------- |
| email    | string                                                | Yes  | Email address of the contact.                    |
| holder   | [Holder](#holder)                                     | Yes  | Application that creates the contacts.                |
| callback | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryContactsByEmail('xxx@email.com', {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContactsByEmail callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContactsByEmail callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContactsByEmail<sup>10+</sup>

queryContactsByEmail(context: Context,  email: string, attrs: ContactAttributes, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries contacts based on the specified email address. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                                 | Mandatory| Description                                                        |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                                               | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| email    | string                                                | Yes  | Email address of the contact.                                          |
| attrs    | [ContactAttributes](#contactattributes)               | Yes  | List of contact attributes.                                          |
| callback | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.                        |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryContactsByEmail(context, 'xxx@email.com', {
      attributes: [contact.Attribute.ATTR_EMAIL, contact.Attribute.ATTR_NAME]
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContactsByEmail callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContactsByEmail callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContactsByEmail(deprecated)<sup>7+</sup>

queryContactsByEmail(email: string, attrs: ContactAttributes, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries contacts based on the specified email address. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryContactsByEmail](#contactquerycontactsbyemail10-2).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                                 | Mandatory| Description                                |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------ |
| email    | string                                                | Yes  | Email address of the contact.                  |
| attrs    | [ContactAttributes](#contactattributes)               | Yes  | List of contact attributes.                  |
| callback | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryContactsByEmail('xxx@email.com', {
      attributes: [contact.Attribute.ATTR_EMAIL, contact.Attribute.ATTR_NAME]
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContactsByEmail callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContactsByEmail callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContactsByEmail<sup>10+</sup>

queryContactsByEmail(context: Context,  email: string, holder: Holder, attrs: ContactAttributes, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries contacts based on the specified email address. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                                 | Mandatory| Description                                                        |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                                               | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| email    | string                                                | Yes  | Email address of the contact.                                          |
| holder   | [Holder](#holder)                                     | Yes  | Application that creates the contacts.                                      |
| attrs    | [ContactAttributes](#contactattributes)               | Yes  | List of contact attributes.                                          |
| callback | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.                        |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryContactsByEmail(context, 'xxx@email.com', {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, {
      attributes: [contact.Attribute.ATTR_EMAIL, contact.Attribute.ATTR_NAME]
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContactsByEmail callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContactsByEmail callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContactsByEmail(deprecated)<sup>7+</sup>

queryContactsByEmail(email: string, holder: Holder, attrs: ContactAttributes, callback: AsyncCallback&lt;Array&lt;Contact&gt;&gt;): void

Queries contacts based on the specified email address. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryContactsByEmail](#contactquerycontactsbyemail10-3).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                                 | Mandatory| Description                                |
| -------- | ----------------------------------------------------- | ---- | ------------------------------------ |
| email    | string                                                | Yes  | Email address of the contact.                  |
| holder   | [Holder](#holder)                                     | Yes  | Application that creates the contacts.              |
| attrs    | [ContactAttributes](#contactattributes)               | Yes  | List of contact attributes.                  |
| callback | AsyncCallback&lt;Array&lt;[Contact](#contact)&gt;&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryContactsByEmail('xxx@email.com', {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, {
      attributes: [contact.Attribute.ATTR_EMAIL, contact.Attribute.ATTR_NAME]
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryContactsByEmail callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryContactsByEmail callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryContactsByEmail<sup>10+</sup>

queryContactsByEmail(context: Context,  email: string, holder?: Holder, attrs?: ContactAttributes): Promise&lt;Array&lt;Contact&gt;&gt;

Queries contacts based on the specified email address, application, and attributes. This API uses a promise to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name | Type                                   | Mandatory| Description                                                        |
| ------- | --------------------------------------- | ---- | ------------------------------------------------------------ |
| context | Context                                 | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| email   | string                                  | Yes  | Email address of the contact.                                          |
| holder  | [Holder](#holder)                       | No  | Application that creates the contacts.                                      |
| attrs   | [ContactAttributes](#contactattributes) | No  | List of contact attributes.                                          |

**Return Value**

| Type                                           | Description                                               |
| ----------------------------------------------- | --------------------------------------------------- |
| Promise&lt;Array&lt;[Contact](#contact)&gt;&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  let promise = contact.queryContactsByEmail(context, 'xxx@email.com', {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, {
      attributes: [contact.Attribute.ATTR_EMAIL, contact.Attribute.ATTR_NAME]
  });
  promise.then((data) => {
      console.log(`queryContactsByEmail success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`queryContactsByEmail fail: err->${JSON.stringify(err)}`);
  });
  ```

## contact.queryContactsByEmail(deprecated)<sup>7+</sup>

queryContactsByEmail(email: string, holder?: Holder, attrs?: ContactAttributes): Promise&lt;Array&lt;Contact&gt;&gt;

Queries contacts based on the specified email address, application, and attributes. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryContactsByEmail](#contactquerycontactsbyemail10-4).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name| Type                                   | Mandatory| Description                  |
| ------ | --------------------------------------- | ---- | ---------------------- |
| email  | string                                  | Yes  | Email address of the contact.    |
| holder | [Holder](#holder)                       | No  | Application that creates the contacts.|
| attrs  | [ContactAttributes](#contactattributes) | No  | List of contact attributes.    |

**Return Value**

| Type                                           | Description                                               |
| ----------------------------------------------- | --------------------------------------------------- |
| Promise&lt;Array&lt;[Contact](#contact)&gt;&gt; | Promise used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  let promise = contact.queryContactsByEmail('xxx@email.com', {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, {
      attributes: [contact.Attribute.ATTR_EMAIL, contact.Attribute.ATTR_NAME]
  });
  promise.then((data) => {
      console.log(`queryContactsByEmail success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`queryContactsByEmail fail: err->${JSON.stringify(err)}`);
  });
  ```

## contact.queryGroups<sup>10+</sup>

queryGroups(context: Context,  callback: AsyncCallback&lt;Array&lt;Group&gt;&gt;): void

Queries all groups of this contact. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                             | Mandatory| Description                                                        |
| -------- | ------------------------------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                                           | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| callback | AsyncCallback&lt;Array&lt;[Group](#group)&gt;&gt; | Yes  | Callback used to return the result.                        |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryGroups(context, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryGroups callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryGroups callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryGroups(deprecated)<sup>7+</sup>

queryGroups(callback: AsyncCallback&lt;Array&lt;Group&gt;&gt;): void

Queries all groups of this contact. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryGroups](#contactquerygroups10).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                             | Mandatory| Description                                |
| -------- | ------------------------------------------------- | ---- | ------------------------------------ |
| callback | AsyncCallback&lt;Array&lt;[Group](#group)&gt;&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryGroups((err: BusinessError, data) => {
      if (err) {
          console.log(`queryGroups callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryGroups callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryGroups<sup>10+</sup>

queryGroups(context: Context,  holder: Holder, callback: AsyncCallback&lt;Array&lt;Group&gt;&gt;): void

Queries all groups of this contact. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                             | Mandatory| Description                                                        |
| -------- | ------------------------------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                                           | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| holder   | [Holder](#holder)                                 | Yes  | Application that creates the contacts.                                      |
| callback | AsyncCallback&lt;Array&lt;[Group](#group)&gt;&gt; | Yes  | Callback used to return the result.                        |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryGroups(context, {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryGroups callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryGroups callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryGroups(deprecated)<sup>7+</sup>

queryGroups(holder: Holder, callback: AsyncCallback&lt;Array&lt;Group&gt;&gt;): void

Queries all groups of this contact. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryGroups](#contactquerygroups10-1).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                             | Mandatory| Description                                |
| -------- | ------------------------------------------------- | ---- | ------------------------------------ |
| holder   | [Holder](#holder)                                 | Yes  | Application that creates the contacts.              |
| callback | AsyncCallback&lt;Array&lt;[Group](#group)&gt;&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryGroups({
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryGroups callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryGroups callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryGroups<sup>10+</sup>

queryGroups(context: Context,  holder?: Holder): Promise&lt;Array&lt;Group&gt;&gt;

Queries all groups of this contact based on the specified application. This API uses a promise to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name | Type             | Mandatory| Description                                                        |
| ------- | ----------------- | ---- | ------------------------------------------------------------ |
| context | Context           | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| holder  | [Holder](#holder) | No  | Application that creates the contacts.                                      |

**Return Value**

| Type                                       | Description                                             |
| ------------------------------------------- | ------------------------------------------------- |
| Promise&lt;Array&lt;[Group](#group)&gt;&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  let promise = contact.queryGroups(context, {
      holderId: 0,
      bundleName: "",
      displayName: ""
  });
  promise.then((data) => {
      console.log(`queryGroups success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`queryGroups fail: err->${JSON.stringify(err)}`);
  });
  ```

## contact.queryGroups(deprecated)<sup>7+</sup>

queryGroups(holder?: Holder): Promise&lt;Array&lt;Group&gt;&gt;

Queries all groups of this contact based on the specified application. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryGroups](#contactquerygroups10-2).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name| Type             | Mandatory| Description                  |
| ------ | ----------------- | ---- | ---------------------- |
| holder | [Holder](#holder) | No  | Application that creates the contacts.|

**Return Value**

| Type                                       | Description                                             |
| ------------------------------------------- | ------------------------------------------------- |
| Promise&lt;Array&lt;[Group](#group)&gt;&gt; | Promise used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  let promise = contact.queryGroups({
      holderId: 0,
      bundleName: "",
      displayName: ""
  });
  promise.then((data) => {
      console.log(`queryGroups success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`queryGroups fail: err->${JSON.stringify(err)}`);
  });
  ```

## contact.queryHolders<sup>10+</sup>

queryHolders(context: Context, callback: AsyncCallback&lt;Array&lt;Holder&gt;&gt;): void

Queries all applications that have created contacts. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                               | Mandatory| Description                                                        |
| -------- | --------------------------------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                                             | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| callback | AsyncCallback&lt;Array&lt;[Holder](#holder)&gt;&gt; | Yes  | Callback used to return the result.        |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryHolders(context, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryHolders callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryHolders callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryHolders(deprecated)<sup>7+</sup>

queryHolders(callback: AsyncCallback&lt;Array&lt;Holder&gt;&gt;): void

Queries all applications that have created contacts. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryHolders](#contactqueryholders10).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                                               | Mandatory| Description                                                |
| -------- | --------------------------------------------------- | ---- | ---------------------------------------------------- |
| callback | AsyncCallback&lt;Array&lt;[Holder](#holder)&gt;&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryHolders((err: BusinessError, data) => {
      if (err) {
          console.log(`queryHolders callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryHolders callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryHolders<sup>10+</sup>

queryHolders(context: Context): Promise&lt;Array&lt;Holder&gt;&gt;

Queries all applications that have created contacts. This API uses a promise to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name | Type   | Mandatory| Description                                                        |
| ------- | ------- | ---- | ------------------------------------------------------------ |
| context | Context | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|

**Return Value**

| Type                                         | Description                                                        |
| --------------------------------------------- | ------------------------------------------------------------ |
| Promise&lt;Array&lt;[Holder](#holder)&gt;&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  let promise = contact.queryHolders(context);
  promise.then((data) => {
      console.log(`queryHolders success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`queryHolders fail: err->${JSON.stringify(err)}`);
  });
  ```

## contact.queryHolders(deprecated)<sup>7+</sup>

queryHolders(): Promise&lt;Array&lt;Holder&gt;&gt;

Queries all applications that have created contacts. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryHolders](#contactqueryholders10-1).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Return Value**

| Type                                         | Description                                                        |
| --------------------------------------------- | ------------------------------------------------------------ |
| Promise&lt;Array&lt;[Holder](#holder)&gt;&gt; | Promise used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  let promise = contact.queryHolders();
  promise.then((data) => {
      console.log(`queryHolders success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`queryHolders fail: err->${JSON.stringify(err)}`);
  });
  ```

## contact.queryKey<sup>10+</sup>

queryKey(context: Context,  id: number, callback: AsyncCallback&lt;string&gt;): void

Queries the key of a contact based on the specified contact ID. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                       | Mandatory| Description                                                        |
| -------- | --------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                     | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| id       | number                      | Yes  | Contact ID.                                        |
| callback | AsyncCallback&lt;string&gt; | Yes  | Callback used to return the result.                     |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryKey(context, /*id*/1, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryKey callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryKey callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryKey(deprecated)<sup>7+</sup>

queryKey(id: number, callback: AsyncCallback&lt;string&gt;): void

Queries the key of a contact based on the specified contact ID. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryKey](#contactquerykey10).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                       | Mandatory| Description                                   |
| -------- | --------------------------- | ---- | --------------------------------------- |
| id       | number                      | Yes  | Contact ID.                   |
| callback | AsyncCallback&lt;string&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryKey(/*id*/1, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryKey callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryKey callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryKey<sup>10+</sup>

queryKey(context: Context,  id: number, holder: Holder, callback: AsyncCallback&lt;string&gt;): void

Queries the key of a contact based on the specified contact ID. This API uses an asynchronous callback to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                       | Mandatory| Description                                                        |
| -------- | --------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                     | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| id       | number                      | Yes  | Contact ID.                                        |
| holder   | [Holder](#holder)           | Yes  | Application that creates the contacts.                                      |
| callback | AsyncCallback&lt;string&gt; | Yes  | Callback used to return the result.                     |

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  contact.queryKey(context, /*id*/1, {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryKey callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryKey callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryKey(deprecated)<sup>7+</sup>

queryKey(id: number, holder: Holder, callback: AsyncCallback&lt;string&gt;): void

Queries the key of a contact based on the specified contact ID. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryKey](#contactquerykey10-1).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name  | Type                       | Mandatory| Description                                   |
| -------- | --------------------------- | ---- | --------------------------------------- |
| id       | number                      | Yes  | Contact ID.                   |
| holder   | [Holder](#holder)           | Yes  | Application that creates the contacts.                 |
| callback | AsyncCallback&lt;string&gt; | Yes  | Callback used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  contact.queryKey(/*id*/1, {
      holderId: 0,
      bundleName: "",
      displayName: ""
  }, (err: BusinessError, data) => {
      if (err) {
          console.log(`queryKey callback: err->${JSON.stringify(err)}`);
          return;
      }
      console.log(`queryKey callback: success data->${JSON.stringify(data)}`);
  });
  ```

## contact.queryKey<sup>10+</sup>

queryKey(context: Context,  id: number, holder?: Holder): Promise&lt;string&gt;

Queries the key of a contact based on the specified contact ID and application. This API uses a promise to return the result.

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name | Type             | Mandatory| Description                                                        |
| ------- | ----------------- | ---- | ------------------------------------------------------------ |
| context | Context           | Yes  | Application context. For the application context of the stage model, see [Context](../apis-ability-kit/js-apis-inner-application-context.md).|
| id      | number            | Yes  | Contact ID.                                        |
| holder  | [Holder](#holder) | No  | Application that creates the contacts.                                      |

**Return Value**

| Type                 | Description                                                |
| --------------------- | ---------------------------------------------------- |
| Promise&lt;string&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 201      | Permission denied. |
| 401      | Parameter error.   |

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  // Obtain the context.
  let context = getContext(this) as Context;
  let promise = contact.queryKey(context, /*id*/1, {
      holderId: 0,
      bundleName: "",
      displayName: ""
  });
  promise.then((data) => {
      console.log(`queryKey success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`queryKey fail: err->${JSON.stringify(err)}`);
  });
  ```

## contact.queryKey(deprecated)<sup>7+</sup>

queryKey(id: number, holder?: Holder): Promise&lt;string&gt;

Queries the key of a contact based on the specified contact ID and application. This API uses a promise to return the result.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 10. You are advised to use [queryKey](#contactquerykey10-2).

**Permission required**: ohos.permission.READ_CONTACTS

**System capability**: SystemCapability.Applications.ContactsData

**Parameters**

| Name| Type             | Mandatory| Description                  |
| ------ | ----------------- | ---- | ---------------------- |
| id     | number            | Yes  | Contact ID.  |
| holder | [Holder](#holder) | No  | Application that creates the contacts.|

**Return Value**

| Type                 | Description                                                |
| --------------------- | ---------------------------------------------------- |
| Promise&lt;string&gt; | Promise used to return the result.|

**Example**

  ```js
  import { BusinessError } from '@ohos.base';
  let promise = contact.queryKey(/*id*/1, {
      holderId: 0,
      bundleName: "",
      displayName: ""
  });
  promise.then((data) => {
      console.log(`queryKey success: data->${JSON.stringify(data)}`);
  }).catch((err: BusinessError) => {
      console.error(`queryKey fail: err->${JSON.stringify(err)}`);
  });
  ```

## ContactSelectionOptions<sup>10+</sup>

Defines the contact selection options.

**System capability**: SystemCapability.Applications.Contacts

|                Name              |                  Type                | Mandatory |        Description     |
| --------------------------------- | ------------------------------------- | ---- | ---------------- |
| isMultiSelect <sup>10+</sup>         | boolean | No  | Whether multiple contacts can be selected.    |



## Contact

Defines a contact.

**System capability**: SystemCapability.Applications.ContactsData

### Constant

| Name              | Value  | Description            |
| ------------------ | ---- | ---------------- |
| INVALID_CONTACT_ID | -1   | Default contact ID.|


### Attributes

|       Name       |                   Type                 | Readable| Writable| Description                                  |
| ----------------- | --------------------------------------- | ---- | ---- | -------------------------------------- |
| id                | number                                  | Yes  | No  | Contact ID.                          |
| key               | string                                  | Yes  | No  | Contact key.                         |
| contactAttributes | [ContactAttributes](#contactattributes) | Yes  | Yes  | List of contact attributes.                    |
| emails            | [Email](#email)[]                       | Yes  | Yes  | List of email addresses of the contact.                |
| events            | [Event](#event)[]                       | Yes  | Yes  | List of important dates such as birthdays and anniversaries of the contact.|
| groups            | [Group](#group)[]                       | Yes  | Yes  | List of groups of the contact.                    |
| imAddresses       | [ImAddress](#imaddress)[]               | Yes  | Yes  | List of instant message addresses of the contact.            |
| phoneNumbers      | [PhoneNumber](#phonenumber)[]           | Yes  | Yes  | List of phone numbers of the contact.                |
| portrait          | [Portrait](#portrait)                   | Yes  | Yes  | Contact portrait.                        |
| postalAddresses   | [PostalAddress](#postaladdress)[]       | Yes  | Yes  | List of postal addresses of the contact.                |
| relations         | [Relation](#relation)[]                 | Yes  | Yes  | List of relationships with the contact.                    |
| sipAddresses      | [SipAddress](#sipaddress)[]             | Yes  | Yes  | List of Session Initiation Protocol (SIP) addresses of the contact. |
| websites          | [Website](#website)[]                   | Yes  | Yes  | List of websites of the contact.                    |
| name              | [Name](#name)                           | Yes  | Yes  | Contact name.                        |
| nickName          | [NickName](#nickname)                   | Yes  | Yes  | Contact nickname.                        |
| note              | [Note](#note)                           | Yes  | Yes  | Contact notes.                        |
| organization      | [Organization](#organization)           | Yes  | Yes  | Organization of the contact.                    |


**Example**

Create contact data in JSON format:


```js
let myContact: contact.Contact = {
    phoneNumbers: [{
        phoneNumber: "138xxxxxxxx"
    }],
    name: {
        fullName: "fullName",
        namePrefix: "namePrefix"
    },
    nickName: {
        nickName: "nickName"
    }
};
```


  Or, create data by configuring a new Contact object.

```js
let myContact = new contact.Contact();
let name = new contact.Name();
name.fullName = "fullName";
let phoneNumber = new contact.PhoneNumber();
phoneNumber.phoneNumber = "138xxxxxxxx";
myContact.name = name;
myContact.phoneNumbers = [phoneNumber];
```


## ContactAttributes

Provides a list of contact attributes, which are generally used as arguments. 
If **null** is passed, all attributes are queried by default.

**System capability**: SystemCapability.Applications.ContactsData

| Name      |            Type          | Readable| Writable| Description            |
| ---------- | ------------------------- | ---- | ---- | ---------------- |
| attributes | [Attribute](#attribute)[] | Yes  | Yes  | List of contact attributes.|


**Example**

Create contact data in JSON format:


```js
let contactAttributes: contact.ContactAttributes = {
    attributes: [
        contact.Attribute.ATTR_EMAIL,
        contact.Attribute.ATTR_NAME,
        contact.Attribute.ATTR_PHONE
    ]
};
```

Or, create data by configuring a **ContactAttributes** object.


```js
let contactAttributes = new contact.ContactAttributes();
contactAttributes.attributes = [contact.Attribute.ATTR_EMAIL];
```


## Attribute

Enumerates contact attributes.

**System capability**: SystemCapability.Applications.ContactsData

| Name                 | Description                              |
| --------------------- | ---------------------------------- |
| ATTR_CONTACT_EVENT    | Important dates such as birthday and anniversaries of the contact.|
| ATTR_EMAIL            | Email address of the contact.                |
| ATTR_GROUP_MEMBERSHIP | Groups of the contact.                    |
| ATTR_IM               | IM addresses of the contact.            |
| ATTR_NAME             | Contact name.                    |
| ATTR_NICKNAME         | Contact nickname.                    |
| ATTR_NOTE             | Contact notes.                    |
| ATTR_ORGANIZATION     | Organization of the contact.                |
| ATTR_PHONE            | Phone number of the contacts.                |
| ATTR_PORTRAIT         | Contact portrait.                    |
| ATTR_POSTAL_ADDRESS   | Postal address of the contact.                |
| ATTR_RELATION         | Relationship with the contact.                    |
| ATTR_SIP_ADDRESS      | SIP addresses of the contact. |
| ATTR_WEBSITE          | Website that stores the contact information.                    |


**Example**

Create contact data in JSON format:

```js
let attributes = [contact.Attribute.ATTR_EMAIL, contact.Attribute.ATTR_NAME, contact.Attribute.ATTR_PHONE];
```


## Email

Defines a contact's email.

**System capability**: SystemCapability.Applications.ContactsData

### Constant

| Name            | Value  | Description            |
| ---------------- | ---- | ---------------- |
| CUSTOM_LABEL     | 0    | Custom mailbox type.|
| EMAIL_HOME       | 1    | Home mailbox.  |
| EMAIL_WORK       | 2    | Work mailbox.  |
| EMAIL_OTHER      | 3    | Other mailbox.  |
| INVALID_LABEL_ID | -1   | Invalid mailbox.  |


### Attributes

| Name       |   Type  | Readable| Writable| Description            |
| ----------- | -------- | ---- | ---- | ---------------- |
| email       | string   | Yes  | Yes  | Email addresses      |
| labelName   | string   | Yes  | Yes  | Name of the mailbox type.|
| displayName | string   | Yes  | Yes  | Displayed name of the mailbox.|
| labelId     | number   | Yes  | Yes  | Mailbox type.    |


**Example**

  Create contact data in JSON format:

```js
let email: contact.Email = {
    email: "xxx@email.com",
    displayName: "displayName"
}
```


  Or, create data by configuring an **Email** object.

```js
let email = new contact.Email();
email.email = "xxx@email.com";
```


## Holder

Defines an application that creates the contact.

**System capability**: SystemCapability.Applications.ContactsData

| Name       | Type  | Readable| Writable| Description        |
| ----------- | ------ | ---- | ---- | ------------ |
| bundleName  | string | Yes  | No  | Bundle name. The value is **com.ohos.contacts**.|
| displayName | string | Yes  | No  | Application name.  |
| holderId    | number | Yes  | Yes  | Application ID.    |


**Example**

  Create contact data in JSON format:

```js
let holder: contact.Holder = {
  bundleName: "com.ohos.contacts",
  displayName: "displayName",
  holderId: 0
};
```

  Or, create data by configuring a **Holder** object.

```js
let holder = new contact.Holder();
holder.holderId = 0;
```


## Event

Defines a contact's event.

**System capability**: SystemCapability.Applications.ContactsData

### Constant

| Name             | Value  | Description              |
| ----------------- | ---- | ------------------ |
| CUSTOM_LABEL      | 0    | Custom event.  |
| EVENT_ANNIVERSARY | 1    | Anniversary event.|
| EVENT_OTHER       | 2    | Other event.    |
| EVENT_BIRTHDAY    | 3    | Birthday event.    |
| INVALID_LABEL_ID  | -1   | Invalid event.    |


### Attributes

|    Name  |   Type  | Readable| Writable| Description          |
| --------- | -------- | ---- | ---- | -------------- |
| eventDate | string   | Yes  | Yes  | Event date.  |
| labelName | string   | Yes  | Yes  | Event type.|
| labelId   | number   | Yes  | Yes  | Event type ID.    |


**Example**

  Create contact data in JSON format:

```js
let event: contact.Event = {
    eventDate: "xxxxxx"
};
```

  Or, create data by configuring an **Event** object.

```js
let event = new contact.Event();
event.eventDate = "xxxxxx";
```


## Group

Defines a contact group.

**System capability**: SystemCapability.Applications.ContactsData

| Name   |   Type  | Readable| Writable| Description              |
| ------- | -------- | ---- | ---- | ------------------ |
| groupId | number   | Yes  | Yes  | ID of a contact group.  |
| title   | string   | Yes  | Yes  | Name of a contact group.|


**Example**

  Create contact data in JSON format:

```js
let group: contact.Group = {
    groupId: 1,
    title: "title"
};
```

  Or, create data by configuring a **Group** object.

```js
let group = new contact.Group();
group.title = "title";
```


## ImAddress

Enumerates IM addresses.

**System capability**: SystemCapability.Applications.ContactsData

### Constant

| Name            | Value  | Description                |
| ---------------- | ---- | -------------------- |
| CUSTOM_LABEL     | -1   | Custom IM|
| IM_AIM           | 0    | AIM   |
| IM_MSN           | 1    | MSN   |
| IM_YAHOO         | 2    | Yahoo |
| IM_SKYPE         | 3    | Skype |
| IM_QQ            | 4    | QQ    |
| IM_ICQ           | 6    | ICQ   |
| IM_JABBER        | 7    | JABBER|
| INVALID_LABEL_ID | -2   | Invalid IM|


### Attributes

| Name     |   Type  | Readable| Writable| Description              |
| --------- | -------- | ---- | ---- | ------------------ |
| imAddress | string   | Yes  | Yes  | IM address.    |
| labelName | string   | Yes  | Yes  | IM name.|
| labelId   | number   | Yes  | Yes  | IM ID.    |


**Example**

  Create contact data in JSON format:

```js
let imAddress: contact.ImAddress = {
    imAddress: "imAddress",
    labelName: "labelName"
};
```


  Or, create data by configuring an **ImAddress** object.

```js
let imAddress = new contact.ImAddress();
imAddress.imAddress = "imAddress";
```


## Name

Defines a contact's name.

**System capability**: SystemCapability.Applications.ContactsData

| Name              |   Type  | Readable| Writable| Description                       |
| ------------------ | -------- | ---- | ---- | --------------------------- |
| familyName         | string   | Yes  | Yes  | Family name.         |
| familyNamePhonetic | string   | Yes  | Yes  | Family name in pinyin.     |
| fullName           | string   | Yes  | Yes  | Full name of the contact.             |
| givenName          | string   | Yes  | Yes  | Given name of the contact.|
| givenNamePhonetic  | string   | Yes  | Yes  | Given name of the contact in pinyin.         |
| middleName         | string   | Yes  | Yes  | Middle name of the contact.           |
| middleNamePhonetic | string   | Yes  | Yes  | Middle name of the contact in pinyin.       |
| namePrefix         | string   | Yes  | Yes  | Prefix of the contact name.         |
| nameSuffix         | string   | Yes  | Yes  | Suffix of the contact name.         |


**Example**

  Create contact data in JSON format:

```js
let name: contact.Name = {
    familyName: "familyName",
    fullName: "fullName"
};
```

  Or, create data by configuring a **Name** object.

```js
let name = new contact.Name();
name.familyName = "familyName";
name.fullName = "fullName";
```


## NickName

Defines a contact's nickname.

**System capability**: SystemCapability.Applications.ContactsData

| Name    |   Type  | Readable| Writable| Description          |
| -------- | -------- | ---- | ---- | -------------- |
| nickName | string   | Yes  | Yes  | Contact nickname.|


**Example**

  Create contact data in JSON format:

```js
let nickName: contact.NickName = {
    nickName: "nickName"
};
```

  Or, create data by configuring a **NickName** object.

```js
let nickName = new contact.NickName();
nickName.nickName = "nickName";
```


## Note

Defines a contact's note.

**System capability**: SystemCapability.Applications.ContactsData

| Name       |   Type  | Readable| Writable| Description              |
| ----------- | -------- | ---- | ---- | ------------------ |
| noteContent | string   | Yes  | Yes  | Notes of the contact.|


**Example**

  Create contact data in JSON format:

```js
let note: contact.Note = {
    noteContent: "noteContent"
};
```

  Or, create data by configuring a **Note** object.

```js
let note = new contact.Note();
note.noteContent = "noteContent";
```


## Organization

Defines a contact's organization.

**System capability**: SystemCapability.Applications.ContactsData

| Name |   Type  | Readable| Writable| Description      |
| ----- | -------- | ---- | ---- | ---------- |
| name  | string   | Yes  | Yes  | Organization name.|
| title | string   | Yes  | Yes  | Job title.|


**Example**

  Create contact data in JSON format:

```js
let organization: contact.Organization = {
    name: "name",
    title: "title"
};
```

  Or, create data by configuring an **Organization** object.

```js
let organization = new contact.Organization();
organization.name = "name";
organization.title = "title";
```


## PhoneNumber

Defines a contact's phone number.

**System capability**: SystemCapability.Applications.ContactsData

### Constant

| Name            | Value  | Description                                            |
| ---------------- | ---- | ------------------------------------------------ |
| CUSTOM_LABEL     | 0    | Custom phone type.                                |
| NUM_HOME         | 1    | Home phone.                                  |
| NUM_MOBILE       | 2    | Mobile phone.                                  |
| NUM_WORK         | 3    | Work phone.                                  |
| NUM_FAX_WORK     | 4    | Work fax.                              |
| NUM_FAX_HOME     | 5    | Family fax.                              |
| NUM_PAGER        | 6    | Pager.                                |
| NUM_OTHER        | 7    | Other phone type.                                  |
| NUM_CALLBACK     | 8    | Callback phone.                                  |
| NUM_CAR          | 9    | Car phone.                                  |
| NUM_COMPANY_MAIN | 10   | Company phone.                                  |
| NUM_ISDN         | 11   | Integrated Services Digital Network (ISDN) phone.                |
| NUM_MAIN         | 12   | Main phone.                                    |
| NUM_OTHER_FAX    | 13   | Other fax phone.                                  |
| NUM_RADIO        | 14   | Wireless phone.                                  |
| NUM_TELEX        | 15   | Telex phone.                                  |
| NUM_TTY_TDD      | 16   | Teletypewriter (TTY) or Test Driven Development (TDD) phone.|
| NUM_WORK_MOBILE  | 17   | Work mobile phone.                              |
| NUM_WORK_PAGER   | 18   | Work pager.                            |
| NUM_ASSISTANT    | 19   | Assistant phone.                                  |
| NUM_MMS          | 20   | MMS phone.                                  |
| INVALID_LABEL_ID | -1   | Invalid phone type.                                  |


### Attributes

| Name       |   Type  | Readable| Writable| Description              |
| ----------- | -------- | ---- | ---- | ------------------ |
| labelName   | string   | Yes  | Yes  | Phone number type.|
| phoneNumber | string   | Yes  | Yes  | Phone number.        |
| labelId     | number   | Yes  | Yes  | Phone number ID.    |


**Example**

  Create contact data in JSON format:

```js
let phoneNumber: contact.PhoneNumber = {
    phoneNumber: "138xxxxxxxx",
    labelId: contact.PhoneNumber.NUM_HOME
};
```

  Or, create data by configuring a new **PhoneNumber** object.

```js
let phoneNumber = new contact.PhoneNumber();
phoneNumber.phoneNumber = "138xxxxxxxx";
```


## Portrait

Defines a contact's portrait.

**System capability**: SystemCapability.Applications.ContactsData

| Name|   Type  | Readable| Writable| Description          |
| ---- | -------- | ---- | ---- | -------------- |
| uri  | string   | Yes  | Yes  | Contact portrait.|


**Example**

  Create contact data in JSON format:

```js
let portrait: contact.Portrait = {
    uri: "uri"
};
```

  Or, create data by configuring a new **Portrait** object.

```js
let portrait = new contact.Portrait();
portrait.uri = "uri";
```


## PostalAddress

Defines a contact's postal address.

**System capability**: SystemCapability.Applications.ContactsData

### Constant

| Name            | Value  | Description                |
| ---------------- | ---- | -------------------- |
| CUSTOM_LABEL     | 0    | Custom postal address type.|
| ADDR_HOME        | 1    | Home address.      |
| ADDR_WORK        | 2    | Work address.      |
| ADDR_OTHER       | 3    | Other addresses.      |
| INVALID_LABEL_ID | -1   | Invalid address type.      |


### Attributes

| Name         |   Type  | Readable| Writable| Description                      |
| ------------- | -------- | ---- | ---- | -------------------------- |
| city          | string   | Yes  | Yes  | City where the contact is located.        |
| country       | string   | Yes  | Yes  | Country/Region where the contact is located.        |
| labelName     | string   | Yes  | Yes  | Postal address type.        |
| neighborhood  | string   | Yes  | Yes  | Neighbor of the contact.            |
| pobox         | string   | Yes  | Yes  | Email of the contact.            |
| postalAddress | string   | Yes  | Yes  | Postal address of the contact.        |
| postcode      | string   | Yes  | Yes  | Postal code of the region where the contact is located.|
| region        | string   | Yes  | Yes  | Area where the contact is located.        |
| street        | string   | Yes  | Yes  | Street where the contact resides.        |
| labelId       | number   | Yes  | Yes  | Postal address type.            |


**Example**

  Create contact data in JSON format:

```js
let postalAddress: contact.PostalAddress = {
    city: "city",
    postalAddress: "postalAddress"
};
```

  Or, create data by configuring a new **PostalAddress** object.

```js
let postalAddress = new contact.PostalAddress();
postalAddress.city = "city";
postalAddress.postalAddress = "postalAddress";
```


## Relation

Defines a contact's relationship.

**System capability**: SystemCapability.Applications.ContactsData

### Constant

| Name                     | Value  | Description              |
| ------------------------- | ---- | ------------------ |
| CUSTOM_LABEL              | 0    | Custom relationship.  |
| RELATION_ASSISTANT        | 1    | Assistant.    |
| RELATION_BROTHER          | 2    | Sibling.    |
| RELATION_CHILD            | 3    | Child.    |
| RELATION_DOMESTIC_PARTNER | 4    | Domestic partner.|
| RELATION_FATHER           | 5    | Father.    |
| RELATION_FRIEND           | 6    | Friend.    |
| RELATION_MANAGER          | 7    | Manager.  |
| RELATION_MOTHER           | 8    | Mother.    |
| RELATION_PARENT           | 9    | Parent.    |
| RELATION_PARTNER          | 10   | Partner.|
| RELATION_REFERRED_BY      | 11   | Referrer.  |
| RELATION_RELATIVE         | 12   | Relative.    |
| RELATION_SISTER           | 13   | Sister.    |
| RELATION_SPOUSE           | 14   | Spouse.    |
| INVALID_LABEL_ID          | -1   | Invalid relationship.  |


### Attributes

| Name        |   Type  | Readable| Writable| Description          |
| ------------ | -------- | ---- | ---- | -------------- |
| labelName    | string   | Yes  | Yes  | Relationship type.|
| relationName | string   | Yes  | Yes  | Relationship name.    |
| labelId      | number   | Yes  | Yes  | Relationship ID.    |


**Example**

  Create contact data in JSON format:

```js
let relation: contact.Relation = {
    relationName: "relationName",
    labelId: contact.Relation.RELATION_ASSISTANT
};
```

  Or, create data by configuring a new **Relation** object.

```js
let relation = new contact.Relation();
relation.relationName = "relationName";
relation.labelId = contact.Relation.RELATION_ASSISTANT;
```


## SipAddress

Defines a contact's SIP address.

**System capability**: SystemCapability.Applications.ContactsData

### Constant

| Name            | Value  | Description                               |
| ---------------- | ---- | ----------------------------------- |
| CUSTOM_LABEL     | 0    | Custom SIP address.|
| SIP_HOME         | 1    | Home SIP address.  |
| SIP_WORK         | 2    | Work SIP address.  |
| SIP_OTHER        | 3    | Other SIP address.  |
| INVALID_LABEL_ID | -1   | Invalid SIP address.  |


### Attributes

| Name      |   Type  | Readable| Writable| Description                             |
| ---------- | -------- | ---- | ---- | --------------------------------- |
| labelName  | string   | Yes  | Yes  | SIP address type.|
| sipAddress | string   | Yes  | Yes  | SIP address.        |
| labelId    | number   | Yes  | Yes  | SIP address ID.    |

**Example**

  Create contact data in JSON format:

```js
let sipAddress: contact.SipAddress = {
    sipAddress: "sipAddress"
};
```

  Or, create data by configuring a new **SipAddress** object.

```js
let sipAddress = new contact.SipAddress();
sipAddress.sipAddress = "sipAddress";
```


## Website

Defines a contact's website.

**System capability**: SystemCapability.Applications.ContactsData

| Name   |   Type  | Readable| Writable| Description              |
| ------- | -------- | ---- | ---- | ------------------ |
| website | string   | Yes  | Yes  | Website of the contact.|


**Example**

  Create contact data in JSON format:

```js
let website: contact.Website = {
    website: "website"
};
```

  Or, create data by configuring a new **Website** object.

```js
let website = new contact.Website();
website.website = "website";
```
