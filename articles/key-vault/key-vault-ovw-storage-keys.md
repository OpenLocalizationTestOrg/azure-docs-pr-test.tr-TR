---
ms.assetid: 
title: "aaaAzure anahtar kasası depolama hesabı anahtarları"
description: "Depolama hesabı anahtarları Azure anahtar kasası ve anahtar tabanlı erişim tooAzure depolama hesabı arasında seemless tümleştirme sağlar."
ms.topic: article
services: key-vault
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/25/2017
ms.openlocfilehash: becdf97798a08164c48d3a7a14aea6ca54085c9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-storage-account-keys"></a>Azure anahtar kasası depolama hesabı anahtarları

Azure anahtar kasası depolama hesabı anahtarları önce geliştiricilerin kendi Azure depolama hesabı (ASA) anahtarları toomanage var ve bunları el ile veya bir dış Otomasyonu boyunca döndür. Şimdi, anahtar kasası depolama hesabı anahtarları olarak uygulanan [anahtar kasası gizli](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) bir Azure depolama hesabıyla kimlik doğrulaması için. 

Merhaba ASA anahtar özelliği, gizli döndürme yönetir ve paylaşılan erişim imzaları (SAS) bir yöntem olarak sunarak ASA anahtarı ile doğrudan iletişim hello gereksinimini kaldırır. 

Azure Storage hesapları hakkında daha fazla genel bilgi için bkz: [Azure storage hesapları hakkında](https://docs.microsoft.com/azure/storage/storage-create-storage-account).

## <a name="supporting-interfaces"></a>Arabirimleri destekleme

Hello Azure depolama hesabı anahtarları özellik hello REST, .NET başlangıçta kullanılabilir / C# ve PowerShell arabirimleri. Daha fazla bilgi için bkz: [anahtar kasası başvurusu](https://docs.microsoft.com/azure/key-vault/).


## <a name="storage-account-keys-behavior"></a>Depolama hesabı anahtarları davranışı

### <a name="what-key-vault-manages"></a>Anahtar kasası ne yönetir

Depolama hesabı anahtarlarını kullandığınızda anahtar kasası sizin adınıza birkaç iç yönetim işlevleri gerçekleştirir.

1. Azure anahtar kasası anahtarları bir Azure depolama hesabı (ASA) yönetir. 
    - Dahili olarak, Azure anahtar kasası (eşitleme) anahtarları bir Azure depolama hesabı ile listeleyebilirsiniz.  
    - Azure anahtar kasası yeniden oluşturur (döndüğü) hello anahtarları düzenli aralıklarla. 
    - Anahtar değerleri hiç yanıt toocaller döndürülür. 
    - Azure anahtar kasası depolama hesapları hem Klasik depolama hesaplarını anahtarları yönetir. 
2. Azure anahtar kasası, hello kasası/nesne sahibi, toocreate SAS (hesabı veya hizmet SAS) tanımları sağlar. 
    - SAS tanımı kullanılarak oluşturulan hello SAS değeri hello REST URI yolu gizlilik olarak döndürülür. Daha fazla bilgi için bkz: [Azure anahtar kasası depolama hesabı işlemleri](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).

### <a name="naming-guidance"></a>Adlandırma

Depolama hesabı adları 3 ile 24 karakter arasında olmalı ve yalnızca sayıyla küçük harf içermelidir.  
 
Bir SAS tanımı adı yalnızca 0-9, a-z, A-Z uzunluğunda 1 102 karakter olmalıdır.

## <a name="developer-experience"></a>Geliştirici deneyimi 

### <a name="before-azure-key-vault-storage-keys"></a>Önce depolama anahtarları Azure anahtar kasası 

Geliştiriciler bir depolama hesabı anahtar tooget erişim tooAzure depolama yöntemlerle aşağıdaki tooneed toodo hello kullanılır. 
 
 ```
//create storage account using connection string containing account name 
// and hello storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a>Azure anahtar kasası depolama anahtarları sonra 

```
//Please make sure tooset storage permissions appropriately on your key vault
Set-AzureRmKeyVaultAccessPolicy -VaultName 'yourVault' -ObjectId yourObjectId -PermissionsToStorage all

//Use PowerShell command tooget Secret URI 

Set-AzureKeyVaultManagedStorageSasDefinition -Service Blob -ResourceType Container,Service -VaultName yourKV  
-AccountName msak01 -Name blobsas1 -Protocol HttpsOnly -ValidityPeriod ([System.Timespan]::FromDays(1)) -Permission Read,List

//Get SAS token from Key Vault

var secret = await kv.GetSecretAsync("SecretUri");

// Create new storage credentials using hello SAS token. 

var accountSasCredential = new StorageCredentials(secret.Value); 

// Use credentials and hello Blob storage endpoint toocreate a new Blob service client. 

var accountWithSas = new CloudStorageAccount(accountSasCredential, new Uri ("https://myaccount.blob.core.windows.net/"), null, null, null); 

var blobClientWithSas = accountWithSas.CreateCloudBlobClient(); 
 
// If SAS token is about tooexpire then Get sasToken again from Key Vault and update it.

accountSasCredential.UpdateSASToken(sasToken);

  ```
 
 ### <a name="developer-best-practices"></a>Geliştirici en iyi uygulamalar 

- Yalnızca anahtar kasası toomanage ASA anahtarlarınızı izin verir. Toomanage çalışmayın bunları kendiniz, anahtar Kasası'nın işlemlerle çalışmasını engeller. 
- Birden fazla anahtar kasası nesnesi tarafından yönetilen ASA anahtarları toobe izin vermez. 
- Gerekirse toomanually ASA tuşlarınızı yeniden oluşturmak, bunları anahtar kasası yeniden öneririz. 

## <a name="getting-started"></a>Başlarken

### <a name="setup-for-role-based-access-control-rbac-permissions"></a>Rol tabanlı erişim denetimi (RBAC) izinler için Kurulum

Anahtar kasası gereken izinleri çok*listesi* ve *yeniden* için bir depolama hesabı anahtarları. Merhaba aşağıdaki adımları kullanarak bu izinlerini ayarlayabilirsiniz:

- Anahtar kasasının objectID alın: 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- Depolama anahtarı işleci rolü tooAzure anahtar kasası kimlik atayın: 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > Bir Klasik hesap türü için hello rol çok parametre*"Klasik depolama hesabı anahtarı işleci hizmet rolü"*.

### <a name="storage-account-onboarding"></a>Depolama hesabı ekleme 

Örnek: Olarak bir depolama eklediğiniz bir anahtar kasası nesne sahibi hesap nesnesi tooyour Azure anahtar kasası tooonboard bir depolama hesabı.

Hazırlama sırasında anahtar kasası hello hello ekleme hesabının kimliğini çok izinlere sahip tooverify gereken*listesi* ve çok*yeniden* depolama anahtarları. İçinde tooverify bu izinleri sipariş, anahtar kasası alır bir OBO (adına, üzerinde) belirteci hello kimlik doğrulama hizmeti tarafından İzleyici tooAzure Kaynak Yöneticisi'ni ayarlayın ve yapar bir *listesi* anahtar çağrısı toohello Azure depolama hizmeti. Merhaba, *listesi* çağrısı başarısız olursa, anahtar kasası nesne oluşturma HTTP durum kodu ile başarısız hello *Yasak*. Bu şekilde listelenen hello anahtarlar, anahtar kasası varlık depolamada önbelleğe alınır. 

Anahtar kasası hello kimlik olduğunu doğrulamalısınız *yeniden* anahtarlarınızı yeniden sahipliğini almadan önce izinleri. OBO belirteci aracılığıyla kimliği hello yanı sıra anahtar kasası birinci taraf kimlik hello tooverify bu izinlere sahiptir:

- Anahtar kasası hello depolama hesabı kaynakta RBAC izinleri listeler.
- Anahtar kasası hello yanıt eylemleri ve Eylemler olmayan normal ifadeyle eşleşen aracılığıyla doğrular. 

At destekleyen bazı örnekleri Bul [anahtar kasası - yönetilen depolama hesabı anahtarları örnekleri](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).

Merhaba kimlik yoksa *yeniden* izinler veya anahtar Kasası'nın ilk taraf kimlik yoksa *listesi* veya *yeniden* izni sonra hello ekleme İstek bir uygun hata kodu ve ileti döndürme başarısız olur. 

kullandığınızda birinci taraf, PowerShell veya CLI yerel istemci uygulamalarının hello OBO belirteci yalnızca çalışır.

## <a name="other-applications"></a>Diğer uygulamalar

- Anahtar kasası depolama hesabı anahtarları kullanılarak oluşturulan SAS belirteci daha da fazla denetimli erişim tooan Azure depolama hesabı sağlayın. Daha fazla bilgi için bkz: [kullanarak paylaşılan erişim imzaları](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).

## <a name="see-also"></a>Ayrıca bkz.

- [Anahtarlar, gizli diziler ve sertifikalar hakkında](https://docs.microsoft.com/rest/api/keyvault/)
- [Anahtar kasası ekip blogu](https://blogs.technet.microsoft.com/kv/)
