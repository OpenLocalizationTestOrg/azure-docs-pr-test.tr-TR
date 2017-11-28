---
title: "Öğretici: Şifrelemek ve Azure anahtar kasası kullanarak Azure Storage blobları şifresini | Microsoft Docs"
description: "Nasıl tooencrypt ve Microsoft Azure Storage ile Azure anahtar kasası için istemci tarafı şifreleme kullanarak bir blob şifresini."
services: storage
documentationcenter: 
author: adhurwit
manager: jasonsav
editor: tysonn
ms.assetid: 027e8631-c1bf-48c1-9d9b-f6843e88b583
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 01/23/2017
ms.author: adhurwit
ms.openlocfilehash: 3eb64f104f378dd09ef295c94e03167655883391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a><span data-ttu-id="801ac-103">Öğretici: Şifrelemek ve şifresini Azure anahtar kasası kullanılarak Microsoft Azure Storage blobları</span><span class="sxs-lookup"><span data-stu-id="801ac-103">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="801ac-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="801ac-104">Introduction</span></span>
<span data-ttu-id="801ac-105">Bu öğretici toomake kullanma Azure anahtar kasası ile istemci-tarafı depolama şifreleme kapsar.</span><span class="sxs-lookup"><span data-stu-id="801ac-105">This tutorial covers how toomake use of client-side storage encryption with Azure Key Vault.</span></span> <span data-ttu-id="801ac-106">Nasıl anlatılmaktadır tooencrypt ve bu teknolojilerden bir konsol uygulamasında bir blob şifresini.</span><span class="sxs-lookup"><span data-stu-id="801ac-106">It walks you through how tooencrypt and decrypt a blob in a console application using these technologies.</span></span>

<span data-ttu-id="801ac-107">**Zaman toocomplete tahmini:** 20 dakika</span><span class="sxs-lookup"><span data-stu-id="801ac-107">**Estimated time toocomplete:** 20 minutes</span></span>

<span data-ttu-id="801ac-108">Azure anahtar kasası hakkında genel bilgi için bkz: [Azure anahtar kasası nedir?](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="801ac-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="801ac-109">Azure Storage istemci tarafı şifreleme hakkında genel bilgi için bkz: [istemci tarafı şifreleme ve Microsoft Azure depolama için Azure anahtar kasası](storage-client-side-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="801ac-109">For overview information about client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="801ac-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="801ac-110">Prerequisites</span></span>
<span data-ttu-id="801ac-111">toocomplete Bu öğreticiyi izleyerek hello olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="801ac-111">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="801ac-112">Bir Azure Storage hesabı</span><span class="sxs-lookup"><span data-stu-id="801ac-112">An Azure Storage account</span></span>
* <span data-ttu-id="801ac-113">Visual Studio 2013 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="801ac-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="801ac-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="801ac-114">Azure PowerShell</span></span>

## <a name="overview-of-client-side-encryption"></a><span data-ttu-id="801ac-115">İstemci tarafı şifreleme genel bakış</span><span class="sxs-lookup"><span data-stu-id="801ac-115">Overview of client-side encryption</span></span>
<span data-ttu-id="801ac-116">Azure Storage istemci tarafı şifreleme genel bakış için bkz: [istemci tarafı şifreleme ve Microsoft Azure depolama için Azure anahtar kasası](storage-client-side-encryption.md)</span><span class="sxs-lookup"><span data-stu-id="801ac-116">For an overview of client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md)</span></span>

<span data-ttu-id="801ac-117">Aşağıda, istemci tarafı şifreleme çalışma biçimine kısa bir açıklaması verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="801ac-117">Here is a brief description of how client side encryption works:</span></span>

1. <span data-ttu-id="801ac-118">Hello Azure Storage istemci SDK simetrik anahtar bir kerelik kullan bir içerik şifreleme anahtarı (CEK) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="801ac-118">hello Azure Storage client SDK generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="801ac-119">Müşteri verileri bu CEK kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="801ac-119">Customer data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="801ac-120">Merhaba CEK sonra (Merhaba anahtar şifreleme anahtarı (KEK) kullanılarak şifrelenir) paketlenir.</span><span class="sxs-lookup"><span data-stu-id="801ac-120">hello CEK is then wrapped (encrypted) using hello key encryption key (KEK).</span></span> <span data-ttu-id="801ac-121">Merhaba KEK anahtar bir tanımlayıcıyla tanımlanır ve asimetrik anahtar çifti ya da bir simetrik anahtar olması ve yerel olarak yönetilebilir veya Azure anahtar kasasında depolanan.</span><span class="sxs-lookup"><span data-stu-id="801ac-121">hello KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vault.</span></span> <span data-ttu-id="801ac-122">Merhaba depolama istemcinin kendisi hiçbir zaman erişim toohello KEK olur.</span><span class="sxs-lookup"><span data-stu-id="801ac-122">hello Storage client itself never has access toohello KEK.</span></span> <span data-ttu-id="801ac-123">Yalnızca, anahtar kasası tarafından sağlanan hello anahtar kaydırma algoritması çağırır.</span><span class="sxs-lookup"><span data-stu-id="801ac-123">It just invokes hello key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="801ac-124">Müşteriler toouse özel sağlayıcılar anahtarı sarmalama/bunlar istiyorsanız açmak için seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="801ac-124">Customers can choose toouse custom providers for key wrapping/unwrapping if they want.</span></span>
4. <span data-ttu-id="801ac-125">Merhaba şifrelenmiş verileri ise toohello Azure depolama hizmeti karşıya yüklendi.</span><span class="sxs-lookup"><span data-stu-id="801ac-125">hello encrypted data is then uploaded toohello Azure Storage service.</span></span>

## <a name="set-up-your-azure-key-vault"></a><span data-ttu-id="801ac-126">Azure anahtar kasanızı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="801ac-126">Set up your Azure Key Vault</span></span>
<span data-ttu-id="801ac-127">Sipariş tooproceed Bu öğretici'de, aşağıdaki hello öğreticide özetlenen adımları toodo hello ihtiyacınız [Azure anahtar kasası ile çalışmaya başlama](../key-vault/key-vault-get-started.md):</span><span class="sxs-lookup"><span data-stu-id="801ac-127">In order tooproceed with this tutorial, you need toodo hello following steps, which are outlined in hello tutorial  [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md):</span></span>

* <span data-ttu-id="801ac-128">Bir anahtar kasası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="801ac-128">Create a key vault.</span></span>
* <span data-ttu-id="801ac-129">Bir anahtar veya gizli toohello anahtar kasası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="801ac-129">Add a key or secret toohello key vault.</span></span>
* <span data-ttu-id="801ac-130">Bir uygulamayı Azure Active Directory ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="801ac-130">Register an application with Azure Active Directory.</span></span>
* <span data-ttu-id="801ac-131">Merhaba uygulama toouse hello anahtar veya gizli yetkilendirin.</span><span class="sxs-lookup"><span data-stu-id="801ac-131">Authorize hello application toouse hello key or secret.</span></span>

<span data-ttu-id="801ac-132">Merhaba ClientID Not ve bir uygulamayı Azure Active Directory'ye kaydedilirken oluşturulan ClientSecret yapın.</span><span class="sxs-lookup"><span data-stu-id="801ac-132">Make note of hello ClientID and ClientSecret that were generated when registering an application with Azure Active Directory.</span></span>

<span data-ttu-id="801ac-133">Her iki anahtarı hello anahtar kasasına oluşturun.</span><span class="sxs-lookup"><span data-stu-id="801ac-133">Create both keys in hello key vault.</span></span> <span data-ttu-id="801ac-134">Başlangıç Öğreticisi hello kalanı için adlarından hello kullanılan varsayıyoruz: ContosoKeyVault ve TestRSAKey1.</span><span class="sxs-lookup"><span data-stu-id="801ac-134">We assume for hello rest of hello tutorial that you have used hello following names: ContosoKeyVault and TestRSAKey1.</span></span>

## <a name="create-a-console-application-with-packages-and-appsettings"></a><span data-ttu-id="801ac-135">Paketler ve AppSettings bir konsol uygulaması oluşturun</span><span class="sxs-lookup"><span data-stu-id="801ac-135">Create a console application with packages and AppSettings</span></span>
<span data-ttu-id="801ac-136">Visual Studio'da yeni bir konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="801ac-136">In Visual Studio, create a new console application.</span></span>

<span data-ttu-id="801ac-137">Gerekli nuget paketlerini hello Paket Yöneticisi konsolu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="801ac-137">Add necessary nuget packages in hello Package Manager Console.</span></span>

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

<span data-ttu-id="801ac-138">AppSettings toohello App.Config ekleyin.</span><span class="sxs-lookup"><span data-stu-id="801ac-138">Add AppSettings toohello App.Config.</span></span>

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

<span data-ttu-id="801ac-139">Merhaba aşağıdakileri ekleyin `using` deyimleri ve yapma emin tooadd bir başvuru tooSystem.Configuration toohello projesi.</span><span class="sxs-lookup"><span data-stu-id="801ac-139">Add hello following `using` statements and make sure tooadd a reference tooSystem.Configuration toohello project.</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Configuration;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.Azure.KeyVault;
using System.Threading;        
using System.IO;
```

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a><span data-ttu-id="801ac-140">Yöntem tooget bir belirteç tooyour konsol uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="801ac-140">Add a method tooget a token tooyour console application</span></span>
<span data-ttu-id="801ac-141">Merhaba aşağıdaki yöntemi tooauthenticate erişim tooyour anahtar kasası için gereken anahtar kasası sınıflar tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="801ac-141">hello following method is used by Key Vault classes that need tooauthenticate for access tooyour key vault.</span></span>

```csharp
private async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);
    ClientCredential clientCred = new ClientCredential(
        ConfigurationManager.AppSettings["clientId"],
        ConfigurationManager.AppSettings["clientSecret"]);
    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)
        throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

## <a name="access-storage-and-key-vault-in-your-program"></a><span data-ttu-id="801ac-142">Depolama ve anahtar kasası programınıza erişim</span><span class="sxs-lookup"><span data-stu-id="801ac-142">Access Storage and Key Vault in your program</span></span>
<span data-ttu-id="801ac-143">Hello ana işlevi, hello aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="801ac-143">In hello Main function, add hello following code.</span></span>

```csharp
// This is standard code toointeract with Blob storage.
StorageCredentials creds = new StorageCredentials(
    ConfigurationManager.AppSettings["accountName"],
       ConfigurationManager.AppSettings["accountKey"]);
CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
CloudBlobClient client = account.CreateCloudBlobClient();
CloudBlobContainer contain = client.GetContainerReference(ConfigurationManager.AppSettings["container"]);
contain.CreateIfNotExists();

// hello Resolver object is used toointeract with Key Vault for Azure Storage.
// This is where hello GetToken method from above is used.
KeyVaultKeyResolver cloudResolver = new KeyVaultKeyResolver(GetToken);
```

> [!NOTE]
> <span data-ttu-id="801ac-144">Anahtar kasası nesne modelleri</span><span class="sxs-lookup"><span data-stu-id="801ac-144">Key Vault Object Models</span></span>
> 
> <span data-ttu-id="801ac-145">Gerçekte iki anahtar kasası nesnesi olduğunu toounderstand modeller toobe farkında önemlidir: bir REST API (KeyVault ad alanı) hello üzerinde dayanır ve hello diğer istemci tarafı şifreleme için bir uzantısıdır.</span><span class="sxs-lookup"><span data-stu-id="801ac-145">It is important toounderstand that there are actually two Key Vault object models toobe aware of: one is based on hello REST API (KeyVault namespace) and hello other is an extension for client-side encryption.</span></span>
> 
> <span data-ttu-id="801ac-146">Merhaba anahtar kasası istemci hello REST API ile etkileşim kurar ve JSON Web anahtarları ve gizli anahtarları hello iki tür anahtar Kasası ' bulunan şeyler için anlar.</span><span class="sxs-lookup"><span data-stu-id="801ac-146">hello Key Vault Client interacts with hello REST API and understands JSON Web Keys and secrets for hello two kinds of things that are contained in Key Vault.</span></span>
> 
> <span data-ttu-id="801ac-147">Azure Storage istemci tarafı şifreleme için özel olarak oluşturulmuş göründüğü sınıfları Hello anahtar kasası uzantılarıdır.</span><span class="sxs-lookup"><span data-stu-id="801ac-147">hello Key Vault Extensions are classes that seem specifically created for client-side encryption in Azure Storage.</span></span> <span data-ttu-id="801ac-148">Anahtarları (IKey) ve anahtar çözümleyici hello kavramı tabanlı sınıflar için bir arabirimi içerir.</span><span class="sxs-lookup"><span data-stu-id="801ac-148">They contain an interface for keys (IKey) and classes based on hello concept of a Key Resolver.</span></span> <span data-ttu-id="801ac-149">Tooknow gereken IKey iki uygulamaları vardır: RSAKey ve SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="801ac-149">There are two implementations of IKey that you need tooknow: RSAKey and SymmetricKey.</span></span> <span data-ttu-id="801ac-150">Bir anahtar kasası içerdiği hello şeyler ile toocoincide gerçekleşir, ancak bu noktada (Merhaba anahtarı ve gizli anahtar kasası istemci hello tarafından alınan IKey uygulamak için) bağımsız sınıfları etmektedir artık.</span><span class="sxs-lookup"><span data-stu-id="801ac-150">Now they happen toocoincide with hello things that are contained in a Key Vault, but at this point they are independent classes (so hello Key and Secret retrieved by hello Key Vault Client do not implement IKey).</span></span>
> 
> 

## <a name="encrypt-blob-and-upload"></a><span data-ttu-id="801ac-151">BLOB şifrelemek ve karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="801ac-151">Encrypt blob and upload</span></span>
<span data-ttu-id="801ac-152">Merhaba aşağıdaki tooencrypt blob kod ve tooyour Azure depolama hesabı karşıya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="801ac-152">Add hello following code tooencrypt a blob and upload it tooyour Azure storage account.</span></span> <span data-ttu-id="801ac-153">Merhaba **ResolveKeyAsync** yöntemi bir IKey döndürür.</span><span class="sxs-lookup"><span data-stu-id="801ac-153">hello **ResolveKeyAsync** method that is used returns an IKey.</span></span>

```csharp
// Retrieve hello key that you created previously.
// hello IKey that is returned here is an RsaKey.
// Remember that we used hello names contosokeyvault and testrsakey1.
var rsa = cloudResolver.ResolveKeyAsync("https://contosokeyvault.vault.azure.net/keys/TestRSAKey1", CancellationToken.None).GetAwaiter().GetResult();

// Now you simply use hello RSA key tooencrypt by setting it in hello BlobEncryptionPolicy.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(rsa, null);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

// Reference a block blob.
CloudBlockBlob blob = contain.GetBlockBlobReference("MyFile.txt");

// Upload using hello UploadFromStream method.
using (var stream = System.IO.File.OpenRead(@"C:\data\MyFile.txt"))
    blob.UploadFromStream(stream, stream.Length, null, options, null);
```

<span data-ttu-id="801ac-154">Merhaba bir ekran görüntüsü aşağıda verilmiştir [Klasik Azure portalı](https://manage.windowsazure.com) istemci tarafı şifreleme anahtar kasasında depolanan anahtar kullanılarak şifrelenmiş bir blobu için.</span><span class="sxs-lookup"><span data-stu-id="801ac-154">Following is a screenshot from hello [Azure Classic Portal](https://manage.windowsazure.com) for a blob that has been encrypted by using client-side encryption with a key stored in Key Vault.</span></span> <span data-ttu-id="801ac-155">Merhaba **Keyıd** hello URI KEK hello gibi davranan bir anahtar kasası hello anahtar için bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="801ac-155">hello **KeyId** property is hello URI for hello key in Key Vault that acts as hello KEK.</span></span> <span data-ttu-id="801ac-156">Merhaba **EncryptedKey** özelliği hello şifrelenmiş hello CEK sürümünü içerir.</span><span class="sxs-lookup"><span data-stu-id="801ac-156">hello **EncryptedKey** property contains hello encrypted version of hello CEK.</span></span>

![Şifreleme meta verileri içeren Blob meta verileri gösteren ekran görüntüsü](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> <span data-ttu-id="801ac-158">Merhaba BlobEncryptionPolicy Oluşturucusu bakarsanız, bu bir anahtar ve/veya bir çözümleyici alabilen görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="801ac-158">If you look at hello BlobEncryptionPolicy constructor, you will see that it can accept a key and/or a resolver.</span></span> <span data-ttu-id="801ac-159">Şu anda mevcut sağ çözümleyici için şifreleme kullanamazsınız, çünkü şimdi varsayılan anahtar destekleyen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="801ac-159">Be aware that right now you cannot use a resolver for encryption because it does not currently support a default key.</span></span>
> 
> 

## <a name="decrypt-blob-and-download"></a><span data-ttu-id="801ac-160">Blob şifresini çözmek ve indirme</span><span class="sxs-lookup"><span data-stu-id="801ac-160">Decrypt blob and download</span></span>
<span data-ttu-id="801ac-161">Ne zaman kullanarak izin ver hello çözümleyici şifre çözme gerçekten olduğu sınıflarının algılama.</span><span class="sxs-lookup"><span data-stu-id="801ac-161">Decryption is really when using hello Resolver classes make sense.</span></span> <span data-ttu-id="801ac-162">şifreleme için kullanılan hello anahtar Hello Kimliğini; böylece, tooretrieve hello anahtarı için bir sebep meta verilerinde hello blob ile ilişkili olan ve anahtar ve blob arasındaki ilişkiyi hello unutmayın.</span><span class="sxs-lookup"><span data-stu-id="801ac-162">hello ID of hello key used for encryption is associated with hello blob in its metadata, so there is no reason for you tooretrieve hello key and remember hello association between key and blob.</span></span> <span data-ttu-id="801ac-163">Yalnızca toomake hello anahtara anahtar kasasına kalmasını gerekir.</span><span class="sxs-lookup"><span data-stu-id="801ac-163">You just have toomake sure that hello key remains in Key Vault.</span></span>   

<span data-ttu-id="801ac-164">Merhaba özel anahtar bir RSA anahtarı kalır anahtar kasasında böylece şifre çözme toooccur için hello şifrelenmiş anahtar CEK tooKey kasası şifre çözme için gönderilen hello içeren hello blob meta veriler.</span><span class="sxs-lookup"><span data-stu-id="801ac-164">hello private key of an RSA Key remains in Key Vault, so for decryption toooccur, hello Encrypted Key from hello blob metadata that contains hello CEK is sent tooKey Vault for decryption.</span></span>

<span data-ttu-id="801ac-165">Merhaba, yeni karşıya yüklediğiniz toodecrypt hello blob aşağıdaki ekleyin.</span><span class="sxs-lookup"><span data-stu-id="801ac-165">Add hello following toodecrypt hello blob that you just uploaded.</span></span>

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> <span data-ttu-id="801ac-166">Birkaç diğer tür çözümleyiciler toomake anahtar yönetimi dahil olmak üzere kolaylaştırır: AggregateKeyResolver ve CachingKeyResolver.</span><span class="sxs-lookup"><span data-stu-id="801ac-166">There are a couple of other kinds of resolvers toomake key management easier, including: AggregateKeyResolver and CachingKeyResolver.</span></span>
> 
> 

## <a name="use-key-vault-secrets"></a><span data-ttu-id="801ac-167">Anahtar kasası gizlilikleri kullanın</span><span class="sxs-lookup"><span data-stu-id="801ac-167">Use Key Vault secrets</span></span>
<span data-ttu-id="801ac-168">Gizli aslında bir simetrik anahtar hello yolu toouse gizli anahtarı istemci tarafı şifreleme ile Merhaba SymmetricKey sınıfı olduğundan.</span><span class="sxs-lookup"><span data-stu-id="801ac-168">hello way toouse a secret with client-side encryption is via hello SymmetricKey class because a secret is essentially a symmetric key.</span></span> <span data-ttu-id="801ac-169">Ancak, yukarıda belirtildiği gibi anahtar kasasında bir gizlilik tooa SymmetricKey tam olarak eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="801ac-169">But, as noted above, a secret in Key Vault does not map exactly tooa SymmetricKey.</span></span> <span data-ttu-id="801ac-170">Birkaç şey toounderstand vardır:</span><span class="sxs-lookup"><span data-stu-id="801ac-170">There are a few things toounderstand:</span></span>

* <span data-ttu-id="801ac-171">bir SymmetricKey Hello anahtarında sahip toobe sabit uzunluk: 128, 192, 256, 384 veya 512 bit.</span><span class="sxs-lookup"><span data-stu-id="801ac-171">hello key in a SymmetricKey has toobe a fixed length: 128, 192, 256, 384, or 512 bits.</span></span>
* <span data-ttu-id="801ac-172">bir SymmetricKey Hello anahtarında Base64 ile kodlanmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="801ac-172">hello key in a SymmetricKey should be Base64 encoded.</span></span>
* <span data-ttu-id="801ac-173">SymmetricKey kullanılacak bir anahtar kasası gizlilik toohave "application/octet-stream" anahtar kasasında bir içerik türü gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="801ac-173">A Key Vault secret that will be used as a SymmetricKey needs toohave a Content Type of "application/octet-stream" in Key Vault.</span></span>

<span data-ttu-id="801ac-174">İşte bir örnek SymmetricKey kullanılabilir anahtar kasasında bir gizli anahtar oluşturma PowerShell'de.</span><span class="sxs-lookup"><span data-stu-id="801ac-174">Here is an example in PowerShell of creating a secret in Key Vault that can be used as a SymmetricKey.</span></span>
<span data-ttu-id="801ac-175">Merhaba sabit kodlu değer, $key, yalnızca Tanıtım amaçlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="801ac-175">Please note that hello hard coded value, $key, is for demonstration purpose only.</span></span> <span data-ttu-id="801ac-176">Kendi kodunuzu bu anahtarı toogenerate isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="801ac-176">In your own code you'll want toogenerate this key.</span></span>

```csharp
// Here we are making a 128-bit key so we have 16 characters.
//     hello characters are in hello ASCII range of UTF8 so they are
//    each 1 byte. 16 x 8 = 128.
$key = "qwertyuiopasdfgh"
$b = [System.Text.Encoding]::UTF8.GetBytes($key)
$enc = [System.Convert]::ToBase64String($b)
$secretvalue = ConvertTo-SecureString $enc -AsPlainText -Force

// Substitute hello VaultName and Name in this command.
$secret = Set-AzureKeyVaultSecret -VaultName 'ContoseKeyVault' -Name 'TestSecret2' -SecretValue $secretvalue -ContentType "application/octet-stream"
```

<span data-ttu-id="801ac-177">Konsol uygulamanızın aynı tooretrieve gibi önce SymmetricKey bu gizli çağrı hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="801ac-177">In your console application, you can use hello same call as before tooretrieve this secret as a SymmetricKey.</span></span>

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
<span data-ttu-id="801ac-178">Bu kadar.</span><span class="sxs-lookup"><span data-stu-id="801ac-178">That's it.</span></span> <span data-ttu-id="801ac-179">Keyfini çıkarın!</span><span class="sxs-lookup"><span data-stu-id="801ac-179">Enjoy!</span></span>

## <a name="next-steps"></a><span data-ttu-id="801ac-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="801ac-180">Next steps</span></span>
<span data-ttu-id="801ac-181">Microsoft Azure depolama C# ile kullanma hakkında daha fazla bilgi için bkz: [.NET için Microsoft Azure Storage istemci Kitaplığı](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="801ac-181">For more information about using Microsoft Azure Storage with C#, see [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="801ac-182">Hello Blob REST API'si hakkında daha fazla bilgi için bkz: [Blob hizmeti REST API'si](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span><span class="sxs-lookup"><span data-stu-id="801ac-182">For more information about hello Blob REST API, see [Blob Service REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span></span>

<span data-ttu-id="801ac-183">Merhaba son hakkında bilgi için Microsoft Azure Storage, toohello gidin [Microsoft Azure depolama ekibi blogu](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="801ac-183">For hello latest information on Microsoft Azure Storage, go toohello [Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>
