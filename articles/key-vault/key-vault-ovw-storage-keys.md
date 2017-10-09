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
# <a name="azure-key-vault-storage-account-keys"></a><span data-ttu-id="e9b45-103">Azure anahtar kasası depolama hesabı anahtarları</span><span class="sxs-lookup"><span data-stu-id="e9b45-103">Azure Key Vault Storage Account Keys</span></span>

<span data-ttu-id="e9b45-104">Azure anahtar kasası depolama hesabı anahtarları önce geliştiricilerin kendi Azure depolama hesabı (ASA) anahtarları toomanage var ve bunları el ile veya bir dış Otomasyonu boyunca döndür.</span><span class="sxs-lookup"><span data-stu-id="e9b45-104">Before Azure Key Vault Storage Account Keys, developers had toomanage their own Azure Storage Account (ASA) keys and rotate them manually or through an external automation.</span></span> <span data-ttu-id="e9b45-105">Şimdi, anahtar kasası depolama hesabı anahtarları olarak uygulanan [anahtar kasası gizli](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) bir Azure depolama hesabıyla kimlik doğrulaması için.</span><span class="sxs-lookup"><span data-stu-id="e9b45-105">Now, Key Vault Storage Account Keys are implemented as [Key Vault secrets](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) for authenticating with an Azure Storage Account.</span></span> 

<span data-ttu-id="e9b45-106">Merhaba ASA anahtar özelliği, gizli döndürme yönetir ve paylaşılan erişim imzaları (SAS) bir yöntem olarak sunarak ASA anahtarı ile doğrudan iletişim hello gereksinimini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="e9b45-106">hello ASA key feature manages secret rotation for you and removes hello need for your direct contact with an ASA key by offering Shared Access Signatures (SAS) as a method.</span></span> 

<span data-ttu-id="e9b45-107">Azure Storage hesapları hakkında daha fazla genel bilgi için bkz: [Azure storage hesapları hakkında](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="e9b45-107">For more general information on Azure Storage Accounts, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span></span>

## <a name="supporting-interfaces"></a><span data-ttu-id="e9b45-108">Arabirimleri destekleme</span><span class="sxs-lookup"><span data-stu-id="e9b45-108">Supporting interfaces</span></span>

<span data-ttu-id="e9b45-109">Hello Azure depolama hesabı anahtarları özellik hello REST, .NET başlangıçta kullanılabilir / C# ve PowerShell arabirimleri.</span><span class="sxs-lookup"><span data-stu-id="e9b45-109">hello Azure Storage Account keys feature is initially available through hello REST, .NET/C# and PowerShell interfaces.</span></span> <span data-ttu-id="e9b45-110">Daha fazla bilgi için bkz: [anahtar kasası başvurusu](https://docs.microsoft.com/azure/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="e9b45-110">For more information, see [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>


## <a name="storage-account-keys-behavior"></a><span data-ttu-id="e9b45-111">Depolama hesabı anahtarları davranışı</span><span class="sxs-lookup"><span data-stu-id="e9b45-111">Storage account keys behavior</span></span>

### <a name="what-key-vault-manages"></a><span data-ttu-id="e9b45-112">Anahtar kasası ne yönetir</span><span class="sxs-lookup"><span data-stu-id="e9b45-112">What Key Vault manages</span></span>

<span data-ttu-id="e9b45-113">Depolama hesabı anahtarlarını kullandığınızda anahtar kasası sizin adınıza birkaç iç yönetim işlevleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="e9b45-113">Key Vault performs several internal management functions on your behalf when you use Storage Account Keys.</span></span>

1. <span data-ttu-id="e9b45-114">Azure anahtar kasası anahtarları bir Azure depolama hesabı (ASA) yönetir.</span><span class="sxs-lookup"><span data-stu-id="e9b45-114">Azure Key Vault manages keys of an Azure Storage Account (ASA).</span></span> 
    - <span data-ttu-id="e9b45-115">Dahili olarak, Azure anahtar kasası (eşitleme) anahtarları bir Azure depolama hesabı ile listeleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9b45-115">Internally, Azure Key Vault can list (sync) keys with an Azure Storage Account.</span></span>  
    - <span data-ttu-id="e9b45-116">Azure anahtar kasası yeniden oluşturur (döndüğü) hello anahtarları düzenli aralıklarla.</span><span class="sxs-lookup"><span data-stu-id="e9b45-116">Azure Key Vault regenerates (rotates) hello keys periodically.</span></span> 
    - <span data-ttu-id="e9b45-117">Anahtar değerleri hiç yanıt toocaller döndürülür.</span><span class="sxs-lookup"><span data-stu-id="e9b45-117">Key values are never returned in response toocaller.</span></span> 
    - <span data-ttu-id="e9b45-118">Azure anahtar kasası depolama hesapları hem Klasik depolama hesaplarını anahtarları yönetir.</span><span class="sxs-lookup"><span data-stu-id="e9b45-118">Azure Key Vault manages keys of both Storage Accounts and Classic Storage Accounts.</span></span> 
2. <span data-ttu-id="e9b45-119">Azure anahtar kasası, hello kasası/nesne sahibi, toocreate SAS (hesabı veya hizmet SAS) tanımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="e9b45-119">Azure Key Vault allows you, hello vault/object owner, toocreate SAS (account or service SAS) definitions.</span></span> 
    - <span data-ttu-id="e9b45-120">SAS tanımı kullanılarak oluşturulan hello SAS değeri hello REST URI yolu gizlilik olarak döndürülür.</span><span class="sxs-lookup"><span data-stu-id="e9b45-120">hello SAS value, created using SAS definition, is returned as a secret via hello REST URI path.</span></span> <span data-ttu-id="e9b45-121">Daha fazla bilgi için bkz: [Azure anahtar kasası depolama hesabı işlemleri](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span><span class="sxs-lookup"><span data-stu-id="e9b45-121">For more information, see [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span></span>

### <a name="naming-guidance"></a><span data-ttu-id="e9b45-122">Adlandırma</span><span class="sxs-lookup"><span data-stu-id="e9b45-122">Naming guidance</span></span>

<span data-ttu-id="e9b45-123">Depolama hesabı adları 3 ile 24 karakter arasında olmalı ve yalnızca sayıyla küçük harf içermelidir.</span><span class="sxs-lookup"><span data-stu-id="e9b45-123">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>  
 
<span data-ttu-id="e9b45-124">Bir SAS tanımı adı yalnızca 0-9, a-z, A-Z uzunluğunda 1 102 karakter olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e9b45-124">A SAS definition name must be 1-102 characters in length containing only 0-9, a-z, A-Z.</span></span>

## <a name="developer-experience"></a><span data-ttu-id="e9b45-125">Geliştirici deneyimi</span><span class="sxs-lookup"><span data-stu-id="e9b45-125">Developer experience</span></span> 

### <a name="before-azure-key-vault-storage-keys"></a><span data-ttu-id="e9b45-126">Önce depolama anahtarları Azure anahtar kasası</span><span class="sxs-lookup"><span data-stu-id="e9b45-126">Before Azure Key Vault Storage Keys</span></span> 

<span data-ttu-id="e9b45-127">Geliştiriciler bir depolama hesabı anahtar tooget erişim tooAzure depolama yöntemlerle aşağıdaki tooneed toodo hello kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e9b45-127">Developers used tooneed toodo hello following practices with a storage account key tooget access tooAzure storage.</span></span> 
 
 ```
//create storage account using connection string containing account name 
// and hello storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a><span data-ttu-id="e9b45-128">Azure anahtar kasası depolama anahtarları sonra</span><span class="sxs-lookup"><span data-stu-id="e9b45-128">After Azure Key Vault Storage Keys</span></span> 

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
 
 ### <a name="developer-best-practices"></a><span data-ttu-id="e9b45-129">Geliştirici en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="e9b45-129">Developer best practices</span></span> 

- <span data-ttu-id="e9b45-130">Yalnızca anahtar kasası toomanage ASA anahtarlarınızı izin verir.</span><span class="sxs-lookup"><span data-stu-id="e9b45-130">Only allow Key Vault toomanage your ASA keys.</span></span> <span data-ttu-id="e9b45-131">Toomanage çalışmayın bunları kendiniz, anahtar Kasası'nın işlemlerle çalışmasını engeller.</span><span class="sxs-lookup"><span data-stu-id="e9b45-131">Do not attempt toomanage them yourself, you will interfere with Key Vault's processes.</span></span> 
- <span data-ttu-id="e9b45-132">Birden fazla anahtar kasası nesnesi tarafından yönetilen ASA anahtarları toobe izin vermez.</span><span class="sxs-lookup"><span data-stu-id="e9b45-132">Do not allow ASA keys toobe managed by more than one Key Vault object.</span></span> 
- <span data-ttu-id="e9b45-133">Gerekirse toomanually ASA tuşlarınızı yeniden oluşturmak, bunları anahtar kasası yeniden öneririz.</span><span class="sxs-lookup"><span data-stu-id="e9b45-133">If you need toomanually regenerate your ASA keys, we recommend that you regenerate them via Key Vault.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="e9b45-134">Başlarken</span><span class="sxs-lookup"><span data-stu-id="e9b45-134">Getting started</span></span>

### <a name="setup-for-role-based-access-control-rbac-permissions"></a><span data-ttu-id="e9b45-135">Rol tabanlı erişim denetimi (RBAC) izinler için Kurulum</span><span class="sxs-lookup"><span data-stu-id="e9b45-135">Setup for role-based access control (RBAC) permissions</span></span>

<span data-ttu-id="e9b45-136">Anahtar kasası gereken izinleri çok*listesi* ve *yeniden* için bir depolama hesabı anahtarları.</span><span class="sxs-lookup"><span data-stu-id="e9b45-136">Key Vault needs permissions too*list* and *regenerate* keys for a storage account.</span></span> <span data-ttu-id="e9b45-137">Merhaba aşağıdaki adımları kullanarak bu izinlerini ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e9b45-137">Set up these permissions using hello following steps:</span></span>

- <span data-ttu-id="e9b45-138">Anahtar kasasının objectID alın:</span><span class="sxs-lookup"><span data-stu-id="e9b45-138">Get ObjectId of Key Vault:</span></span> 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- <span data-ttu-id="e9b45-139">Depolama anahtarı işleci rolü tooAzure anahtar kasası kimlik atayın:</span><span class="sxs-lookup"><span data-stu-id="e9b45-139">Assign Storage Key Operator role tooAzure Key Vault Identity:</span></span> 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > <span data-ttu-id="e9b45-140">Bir Klasik hesap türü için hello rol çok parametre*"Klasik depolama hesabı anahtarı işleci hizmet rolü"*.</span><span class="sxs-lookup"><span data-stu-id="e9b45-140">For a classic account type, set hello role parameter too*"Classic Storage Account Key Operator Service Role"*.</span></span>

### <a name="storage-account-onboarding"></a><span data-ttu-id="e9b45-141">Depolama hesabı ekleme</span><span class="sxs-lookup"><span data-stu-id="e9b45-141">Storage account onboarding</span></span> 

<span data-ttu-id="e9b45-142">Örnek: Olarak bir depolama eklediğiniz bir anahtar kasası nesne sahibi hesap nesnesi tooyour Azure anahtar kasası tooonboard bir depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="e9b45-142">Example: As a Key Vault object owner you add a storage account object tooyour Azure Key Vault tooonboard a storage account.</span></span>

<span data-ttu-id="e9b45-143">Hazırlama sırasında anahtar kasası hello hello ekleme hesabının kimliğini çok izinlere sahip tooverify gereken*listesi* ve çok*yeniden* depolama anahtarları.</span><span class="sxs-lookup"><span data-stu-id="e9b45-143">During onboarding, Key Vault needs tooverify that hello identity of hello onboarding account has permissions too*list* and too*regenerate* storage keys.</span></span> <span data-ttu-id="e9b45-144">İçinde tooverify bu izinleri sipariş, anahtar kasası alır bir OBO (adına, üzerinde) belirteci hello kimlik doğrulama hizmeti tarafından İzleyici tooAzure Kaynak Yöneticisi'ni ayarlayın ve yapar bir *listesi* anahtar çağrısı toohello Azure depolama hizmeti.</span><span class="sxs-lookup"><span data-stu-id="e9b45-144">In order tooverify these permissions, Key Vault gets an OBO (On Behalf Of) token from hello authentication service, audience set tooAzure Resource Manager, and makes a *list* key call toohello Azure Storage service.</span></span> <span data-ttu-id="e9b45-145">Merhaba, *listesi* çağrısı başarısız olursa, anahtar kasası nesne oluşturma HTTP durum kodu ile başarısız hello *Yasak*.</span><span class="sxs-lookup"><span data-stu-id="e9b45-145">If hello *list* call fails, hello Key Vault object creation fails with a HTTP status code of *Forbidden*.</span></span> <span data-ttu-id="e9b45-146">Bu şekilde listelenen hello anahtarlar, anahtar kasası varlık depolamada önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="e9b45-146">hello keys listed in this fashion are cached with your key vault entity storage.</span></span> 

<span data-ttu-id="e9b45-147">Anahtar kasası hello kimlik olduğunu doğrulamalısınız *yeniden* anahtarlarınızı yeniden sahipliğini almadan önce izinleri.</span><span class="sxs-lookup"><span data-stu-id="e9b45-147">Key Vault must verify that hello identity has *regenerate* permissions before it can take ownership of regenerating your keys.</span></span> <span data-ttu-id="e9b45-148">OBO belirteci aracılığıyla kimliği hello yanı sıra anahtar kasası birinci taraf kimlik hello tooverify bu izinlere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="e9b45-148">tooverify that hello identity, via OBO token, as well as hello Key Vault first party identity has these permissions:</span></span>

- <span data-ttu-id="e9b45-149">Anahtar kasası hello depolama hesabı kaynakta RBAC izinleri listeler.</span><span class="sxs-lookup"><span data-stu-id="e9b45-149">Key Vault lists RBAC permissions on hello storage account resource.</span></span>
- <span data-ttu-id="e9b45-150">Anahtar kasası hello yanıt eylemleri ve Eylemler olmayan normal ifadeyle eşleşen aracılığıyla doğrular.</span><span class="sxs-lookup"><span data-stu-id="e9b45-150">Key Vault validates hello response via regular expression matching of actions and non-actions.</span></span> 

<span data-ttu-id="e9b45-151">At destekleyen bazı örnekleri Bul [anahtar kasası - yönetilen depolama hesabı anahtarları örnekleri](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span><span class="sxs-lookup"><span data-stu-id="e9b45-151">Find some supporting examples at [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span></span>

<span data-ttu-id="e9b45-152">Merhaba kimlik yoksa *yeniden* izinler veya anahtar Kasası'nın ilk taraf kimlik yoksa *listesi* veya *yeniden* izni sonra hello ekleme İstek bir uygun hata kodu ve ileti döndürme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="e9b45-152">If hello identity does not have *regenerate* permissions or if Key Vault's first party identity doesn’t have *list* or *regenerate* permission, then hello onboarding request fails returning an appropriate error code and message.</span></span> 

<span data-ttu-id="e9b45-153">kullandığınızda birinci taraf, PowerShell veya CLI yerel istemci uygulamalarının hello OBO belirteci yalnızca çalışır.</span><span class="sxs-lookup"><span data-stu-id="e9b45-153">hello OBO token will only work when you use first-party, native client applications of either PowerShell or CLI.</span></span>

## <a name="other-applications"></a><span data-ttu-id="e9b45-154">Diğer uygulamalar</span><span class="sxs-lookup"><span data-stu-id="e9b45-154">Other applications</span></span>

- <span data-ttu-id="e9b45-155">Anahtar kasası depolama hesabı anahtarları kullanılarak oluşturulan SAS belirteci daha da fazla denetimli erişim tooan Azure depolama hesabı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="e9b45-155">SAS tokens, constructed using Key Vault storage account keys, provide even more controlled access tooan Azure storage account.</span></span> <span data-ttu-id="e9b45-156">Daha fazla bilgi için bkz: [kullanarak paylaşılan erişim imzaları](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="e9b45-156">For more information, see [Using shared access signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

## <a name="see-also"></a><span data-ttu-id="e9b45-157">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="e9b45-157">See also</span></span>

- [<span data-ttu-id="e9b45-158">Anahtarlar, gizli diziler ve sertifikalar hakkında</span><span class="sxs-lookup"><span data-stu-id="e9b45-158">About keys, secrets, and certificates</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
- [<span data-ttu-id="e9b45-159">Anahtar kasası ekip blogu</span><span class="sxs-lookup"><span data-stu-id="e9b45-159">Key Vault Team Blog</span></span>](https://blogs.technet.microsoft.com/kv/)
