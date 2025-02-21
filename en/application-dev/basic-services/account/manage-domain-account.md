# Managing Domain Accounts (for System Applications Only)

The user can add a domain account to a device so that the domain account user can log in to the system and use the device.

## Before You Start

1. Request the following permissions. For details, see [Requesting Permissions for system_basic Applications](../../security/AccessToken/determine-application-mode.md#requesting-permissions-for-system_basic-applications).
   - ohos.permission.MANAGE_LOCAL_ACCOUNTS
   - ohos.permission.GET_DOMAIN_ACCOUNTS

2. Import the **osAccount** module.

   ```ts
   import account_osAccount from '@ohos.account.osAccount';
   import { AsyncCallback, BusinessError } from '@ohos.base';
   ```

3. Obtain an **AccountManager** instance of the system account.

   ```ts
   let osAccountMgr = account_osAccount.getAccountManager();
   ```

## Checking for a Domain Account

Before adding a domain account, the user may need to check whether the domain account exists. You can use [hasAccount](../../reference/apis-basic-services-kit/js-apis-osAccount-sys.md#hasaccount10) to check whether a domain account exists.

**Procedure**

1. Define the domain account to check.

   ```ts
   let domainAccountInfo: account_osAccount.DomainAccountInfo = {
     accountName: 'testAccountName',
     domain: 'testDomain'
   }
   ```

2. Use [hasAccount](../../reference/apis-basic-services-kit/js-apis-osAccount-sys.md#hasaccount10) to check whether the domain account exists.

   ```ts
   let isAccountExisted: boolean = await account_osAccount.DomainAccountManager.hasAccount(domainAccountInfo);
   ```

## Adding a Domain Account

The user can add a domain account in **Settings** to allow the domain account user to log in to and use the device. You can use [createOsAccountForDomain](../../reference/apis-basic-services-kit/js-apis-osAccount-sys.md#createosaccountfordomain) to implement this operation.

**Procedure**

1. Define domain account information, including the domain name, account name, and account ID (optional).

   ```ts
   let domainInfo: account_osAccount.DomainAccountInfo = {
     domain: 'testDomain',
     accountName: 'testAccountName'
   };
   ```

2. Use [createOsAccountForDomain](../../reference/apis-basic-services-kit/js-apis-osAccount-sys.md#createosaccountfordomain) to create a domain account on the device.

   ```ts
   try {
     accountMgr.createOsAccountForDomain(account_osAccount.OsAccountType.NORMAL, domainInfo,
     (err: BusinessError, osAccountInfo: account_osAccount.OsAccountInfo)=>{
       console.log('createOsAccountForDomain err:' + JSON.stringify(err));
       console.log('createOsAccountForDomain osAccountInfo:' + JSON.stringify(osAccountInfo));
   });
   } catch (e) {
   console.log('createOsAccountForDomain exception: ' + JSON.stringify(e));
   }
   ```

## Deleting a Domain Account

The user can delete the domain account that is not required. Since a domain account is in one-to-one relationship with a system account, you can use [removeOsAccount](../../reference/apis-basic-services-kit/js-apis-osAccount-sys.md#removeosaccount) to delete the system account. The domain account is deleted as well.

**Procedure**

1. Use [getOsAccountLocalIdForDomain](../../reference/apis-basic-services-kit/js-apis-osAccount.md#getosaccountlocalidfordomain9) to obtain the system account ID based on the domain account information.

   ```ts
   let domainInfo: account_osAccount.DomainAccountInfo = {
       domain: 'testDomain',
       accountName: 'testAccountName'
   };

   try {
     let localId: number = accountMgr.getOsAccountLocalIdForDomain(domainInfo);
   } catch (err) {
     console.log('getOsAccountLocalIdForDomain exception: ' + JSON.stringify(err));
   }
   ```

2. Use [removeOsAccount](../../reference/apis-basic-services-kit/js-apis-osAccount-sys.md#removeosaccount) to delete the system account.

   ```ts
   try {
     accountMgr.removeOsAccount(osAccountInfo.localId, (err: BusinessError)=>{
       if (err) {
           console.log('removeOsAccount failed, error: ' + JSON.stringify(err));
       } else {
           console.log('removeOsAccount successfully');
       }
     });
   } catch (err) {
     console.log('removeOsAccount exception: ' + JSON.stringify(err));
   }
   ```

## Obtaining Domain Account Information

After passing the authentication, the user can query their own or others' domain account information. You can use [getAccountInfo](../../reference/apis-basic-services-kit/js-apis-osAccount-sys.md#getaccountinfo10) to implement this operation.

**Procedure**

1. Specify the query options, including the domain name and account name. The option type is [GetDomainAccountInfoOptions](../../reference/apis-basic-services-kit/js-apis-osAccount-sys.md#getdomainaccountinfooptions10).

   ```ts
   let options: account_osAccount.GetDomainAccountInfoOptions = {
       domain: 'testDomain',
       accountName: 'testAccountName'
   }
   ```

2. Use [getAccountInfo](../../reference/apis-basic-services-kit/js-apis-osAccount-sys.md#getaccountinfo10) to obtain domain account information.

   ```ts
   try {
     account_osAccount.DomainAccountManager.getAccountInfo(domainAccountInfo,
       (err: BusinessError, result: account_osAccount.DomainAccountInfo) => {
       if (err) {
           console.log('call getAccountInfo failed, error: ' + JSON.stringify(err));
       } else {
           console.log('getAccountInfo result: ' + result);
       }
     });
   } catch (err) {
       console.log('getAccountInfo exception = ' + JSON.stringify(err));
   }
   ```
