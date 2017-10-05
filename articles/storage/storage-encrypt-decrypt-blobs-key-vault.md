---
title: "Öğretici: Şifrelemek ve Azure anahtar kasası kullanarak Azure Storage blobları şifresini | Microsoft Docs"
description: "Şifrelemek ve şifresini çözmek için Azure anahtar kasası ile Microsoft Azure Storage istemci tarafı şifreleme kullanarak bir blob nasıl."
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
ms.openlocfilehash: 0c33742a0212e670072a947a2d2ab8304c77b973
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a><span data-ttu-id="becc0-103">Öğretici: Şifrelemek ve şifresini Azure anahtar kasası kullanılarak Microsoft Azure Storage blobları</span><span class="sxs-lookup"><span data-stu-id="becc0-103">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="becc0-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="becc0-104">Introduction</span></span>
<span data-ttu-id="becc0-105">Bu öğretici nasıl kapsayan Azure anahtar kasası ile istemci-tarafı depolama şifreleme kullanın.</span><span class="sxs-lookup"><span data-stu-id="becc0-105">This tutorial covers how to make use of client-side storage encryption with Azure Key Vault.</span></span> <span data-ttu-id="becc0-106">Bu, şifrelemek ve bu teknolojilerden bir konsol uygulamasında bir blob şifresini çözmek nasıl açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="becc0-106">It walks you through how to encrypt and decrypt a blob in a console application using these technologies.</span></span>

<span data-ttu-id="becc0-107">**Tahmini tamamlanma süresi:** 20 dakika</span><span class="sxs-lookup"><span data-stu-id="becc0-107">**Estimated time to complete:** 20 minutes</span></span>

<span data-ttu-id="becc0-108">Azure anahtar kasası hakkında genel bilgi için bkz: [Azure anahtar kasası nedir?](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="becc0-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="becc0-109">Azure Storage istemci tarafı şifreleme hakkında genel bilgi için bkz: [istemci tarafı şifreleme ve Microsoft Azure depolama için Azure anahtar kasası](storage-client-side-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="becc0-109">For overview information about client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="becc0-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="becc0-110">Prerequisites</span></span>
<span data-ttu-id="becc0-111">Bu öğreticiyi tamamlamak için aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="becc0-111">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="becc0-112">Bir Azure Storage hesabı</span><span class="sxs-lookup"><span data-stu-id="becc0-112">An Azure Storage account</span></span>
* <span data-ttu-id="becc0-113">Visual Studio 2013 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="becc0-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="becc0-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="becc0-114">Azure PowerShell</span></span>

## <a name="overview-of-client-side-encryption"></a><span data-ttu-id="becc0-115">İstemci tarafı şifreleme genel bakış</span><span class="sxs-lookup"><span data-stu-id="becc0-115">Overview of client-side encryption</span></span>
<span data-ttu-id="becc0-116">Azure Storage istemci tarafı şifreleme genel bakış için bkz: [istemci tarafı şifreleme ve Microsoft Azure depolama için Azure anahtar kasası](storage-client-side-encryption.md)</span><span class="sxs-lookup"><span data-stu-id="becc0-116">For an overview of client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md)</span></span>

<span data-ttu-id="becc0-117">Aşağıda, istemci tarafı şifreleme çalışma biçimine kısa bir açıklaması verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="becc0-117">Here is a brief description of how client side encryption works:</span></span>

1. <span data-ttu-id="becc0-118">Azure Storage istemci SDK simetrik anahtar bir kerelik kullan bir içerik şifreleme anahtarı (CEK) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="becc0-118">The Azure Storage client SDK generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="becc0-119">Müşteri verileri bu CEK kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="becc0-119">Customer data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="becc0-120">CEK (anahtar şifreleme anahtarı (KEK) kullanılarak şifrelenir) paketlenir.</span><span class="sxs-lookup"><span data-stu-id="becc0-120">The CEK is then wrapped (encrypted) using the key encryption key (KEK).</span></span> <span data-ttu-id="becc0-121">KEK anahtar bir tanımlayıcıyla tanımlanır ve asimetrik anahtar çifti ya da bir simetrik anahtar olması ve yerel olarak yönetilebilir veya Azure anahtar Kasası ' depolanır.</span><span class="sxs-lookup"><span data-stu-id="becc0-121">The KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vault.</span></span> <span data-ttu-id="becc0-122">Depolama istemcisi KEK hiçbir zaman erişebilir.</span><span class="sxs-lookup"><span data-stu-id="becc0-122">The Storage client itself never has access to the KEK.</span></span> <span data-ttu-id="becc0-123">Yalnızca, anahtar kasası tarafından sağlanan anahtar kaydırma algoritması çağırır.</span><span class="sxs-lookup"><span data-stu-id="becc0-123">It just invokes the key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="becc0-124">Müşteriler için anahtar kaydırma/bunlar istiyorsanız açmak özel sağlayıcılar kullanmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="becc0-124">Customers can choose to use custom providers for key wrapping/unwrapping if they want.</span></span>
4. <span data-ttu-id="becc0-125">Şifrelenmiş veriler daha sonra Azure Storage hizmetine yüklenir.</span><span class="sxs-lookup"><span data-stu-id="becc0-125">The encrypted data is then uploaded to the Azure Storage service.</span></span>

## <a name="set-up-your-azure-key-vault"></a><span data-ttu-id="becc0-126">Azure anahtar kasanızı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="becc0-126">Set up your Azure Key Vault</span></span>
<span data-ttu-id="becc0-127">Öğreticide özetlenen aşağıdaki adımları gerçekleştirmeniz gereken Bu öğretici ile devam etmek için [Azure anahtar kasası ile çalışmaya başlama](../key-vault/key-vault-get-started.md):</span><span class="sxs-lookup"><span data-stu-id="becc0-127">In order to proceed with this tutorial, you need to do the following steps, which are outlined in the tutorial  [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md):</span></span>

* <span data-ttu-id="becc0-128">Bir anahtar kasası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="becc0-128">Create a key vault.</span></span>
* <span data-ttu-id="becc0-129">Bir anahtar veya gizli anahtar Kasası'na ekleyin.</span><span class="sxs-lookup"><span data-stu-id="becc0-129">Add a key or secret to the key vault.</span></span>
* <span data-ttu-id="becc0-130">Bir uygulamayı Azure Active Directory ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="becc0-130">Register an application with Azure Active Directory.</span></span>
* <span data-ttu-id="becc0-131">Anahtar veya gizli kullanmak için uygulamayı yetkilendirin.</span><span class="sxs-lookup"><span data-stu-id="becc0-131">Authorize the application to use the key or secret.</span></span>

<span data-ttu-id="becc0-132">İstemci kimliği ve bir uygulamayı Azure Active Directory'ye kaydedilirken oluşturulan ClientSecret not edin.</span><span class="sxs-lookup"><span data-stu-id="becc0-132">Make note of the ClientID and ClientSecret that were generated when registering an application with Azure Active Directory.</span></span>

<span data-ttu-id="becc0-133">Her iki anahtarı anahtar kasasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="becc0-133">Create both keys in the key vault.</span></span> <span data-ttu-id="becc0-134">Aşağıdaki adları kullanılan öğreticinin geri kalanını için varsayıyoruz: ContosoKeyVault ve TestRSAKey1.</span><span class="sxs-lookup"><span data-stu-id="becc0-134">We assume for the rest of the tutorial that you have used the following names: ContosoKeyVault and TestRSAKey1.</span></span>

## <a name="create-a-console-application-with-packages-and-appsettings"></a><span data-ttu-id="becc0-135">Paketler ve AppSettings bir konsol uygulaması oluşturun</span><span class="sxs-lookup"><span data-stu-id="becc0-135">Create a console application with packages and AppSettings</span></span>
<span data-ttu-id="becc0-136">Visual Studio'da yeni bir konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="becc0-136">In Visual Studio, create a new console application.</span></span>

<span data-ttu-id="becc0-137">Gerekli nuget paketleri Paket Yöneticisi konsolunda ekleyin.</span><span class="sxs-lookup"><span data-stu-id="becc0-137">Add necessary nuget packages in the Package Manager Console.</span></span>

```
Install-Package WindowsAzure.Storage

// This is the latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

<span data-ttu-id="becc0-138">AppSettings App.Config ekleyin.</span><span class="sxs-lookup"><span data-stu-id="becc0-138">Add AppSettings to the App.Config.</span></span>

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

<span data-ttu-id="becc0-139">Aşağıdakileri ekleyin `using` deyimleri ve projeye System.Configuration başvuru eklemek emin olun.</span><span class="sxs-lookup"><span data-stu-id="becc0-139">Add the following `using` statements and make sure to add a reference to System.Configuration to the project.</span></span>

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

## <a name="add-a-method-to-get-a-token-to-your-console-application"></a><span data-ttu-id="becc0-140">Konsol uygulamanız için bir belirteç almak üzere bir yöntem ekleyin</span><span class="sxs-lookup"><span data-stu-id="becc0-140">Add a method to get a token to your console application</span></span>
<span data-ttu-id="becc0-141">Aşağıdaki yöntem, anahtar kasanızı erişim için kimlik doğrulaması gerekli anahtar kasası sınıflar tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="becc0-141">The following method is used by Key Vault classes that need to authenticate for access to your key vault.</span></span>

```csharp
private async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);
    ClientCredential clientCred = new ClientCredential(
        ConfigurationManager.AppSettings["clientId"],
        ConfigurationManager.AppSettings["clientSecret"]);
    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)
        throw new InvalidOperationException("Failed to obtain the JWT token");

    return result.AccessToken;
}
```

## <a name="access-storage-and-key-vault-in-your-program"></a><span data-ttu-id="becc0-142">Depolama ve anahtar kasası programınıza erişim</span><span class="sxs-lookup"><span data-stu-id="becc0-142">Access Storage and Key Vault in your program</span></span>
<span data-ttu-id="becc0-143">Main işlevi aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="becc0-143">In the Main function, add the following code.</span></span>

```csharp
// This is standard code to interact with Blob storage.
StorageCredentials creds = new StorageCredentials(
    ConfigurationManager.AppSettings["accountName"],
       ConfigurationManager.AppSettings["accountKey"]);
CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
CloudBlobClient client = account.CreateCloudBlobClient();
CloudBlobContainer contain = client.GetContainerReference(ConfigurationManager.AppSettings["container"]);
contain.CreateIfNotExists();

// The Resolver object is used to interact with Key Vault for Azure Storage.
// This is where the GetToken method from above is used.
KeyVaultKeyResolver cloudResolver = new KeyVaultKeyResolver(GetToken);
```

> [!NOTE]
> <span data-ttu-id="becc0-144">Anahtar kasası nesne modelleri</span><span class="sxs-lookup"><span data-stu-id="becc0-144">Key Vault Object Models</span></span>
> 
> <span data-ttu-id="becc0-145">Dikkat edilmesi gereken gerçekte iki anahtar kasası nesne modeli olduğunu anlamak önemlidir: bir REST API (KeyVault ad alanı) dayanır ve diğer istemci tarafı şifreleme uzantısıdır.</span><span class="sxs-lookup"><span data-stu-id="becc0-145">It is important to understand that there are actually two Key Vault object models to be aware of: one is based on the REST API (KeyVault namespace) and the other is an extension for client-side encryption.</span></span>
> 
> <span data-ttu-id="becc0-146">Anahtar kasası istemci REST API'si ile etkileşim kurar ve JSON Web anahtarları ve gizli anahtarları için anahtar kasasına içerdiği şeyler iki tür anlar.</span><span class="sxs-lookup"><span data-stu-id="becc0-146">The Key Vault Client interacts with the REST API and understands JSON Web Keys and secrets for the two kinds of things that are contained in Key Vault.</span></span>
> 
> <span data-ttu-id="becc0-147">Anahtar kasası uzantıları Azure Storage istemci tarafı şifreleme için özel olarak oluşturulmuş görünen sınıflarıdır.</span><span class="sxs-lookup"><span data-stu-id="becc0-147">The Key Vault Extensions are classes that seem specifically created for client-side encryption in Azure Storage.</span></span> <span data-ttu-id="becc0-148">Anahtarları (IKey) ve anahtar çözümleyici kavramını esas sınıfları için bir arabirimi içerir.</span><span class="sxs-lookup"><span data-stu-id="becc0-148">They contain an interface for keys (IKey) and classes based on the concept of a Key Resolver.</span></span> <span data-ttu-id="becc0-149">Bilmeniz gereken IKey iki uygulamaları vardır: RSAKey ve SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="becc0-149">There are two implementations of IKey that you need to know: RSAKey and SymmetricKey.</span></span> <span data-ttu-id="becc0-150">Artık bir anahtar kasası içerdiği şeyler ile çakıştığı için gerçekleşmeden, ancak bu noktada (anahtarı ve gizli anahtar kasası istemci tarafından alınan IKey uygulamak için) bağımsız sınıfları etmektedir.</span><span class="sxs-lookup"><span data-stu-id="becc0-150">Now they happen to coincide with the things that are contained in a Key Vault, but at this point they are independent classes (so the Key and Secret retrieved by the Key Vault Client do not implement IKey).</span></span>
> 
> 

## <a name="encrypt-blob-and-upload"></a><span data-ttu-id="becc0-151">BLOB şifrelemek ve karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="becc0-151">Encrypt blob and upload</span></span>
<span data-ttu-id="becc0-152">Bir blob şifrelemek ve Azure depolama hesabınıza yüklemek için aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="becc0-152">Add the following code to encrypt a blob and upload it to your Azure storage account.</span></span> <span data-ttu-id="becc0-153">**ResolveKeyAsync** yöntemi bir IKey döndürür.</span><span class="sxs-lookup"><span data-stu-id="becc0-153">The **ResolveKeyAsync** method that is used returns an IKey.</span></span>

```csharp
// Retrieve the key that you created previously.
// The IKey that is returned here is an RsaKey.
// Remember that we used the names contosokeyvault and testrsakey1.
var rsa = cloudResolver.ResolveKeyAsync("https://contosokeyvault.vault.azure.net/keys/TestRSAKey1", CancellationToken.None).GetAwaiter().GetResult();

// Now you simply use the RSA key to encrypt by setting it in the BlobEncryptionPolicy.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(rsa, null);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

// Reference a block blob.
CloudBlockBlob blob = contain.GetBlockBlobReference("MyFile.txt");

// Upload using the UploadFromStream method.
using (var stream = System.IO.File.OpenRead(@"C:\data\MyFile.txt"))
    blob.UploadFromStream(stream, stream.Length, null, options, null);
```

<span data-ttu-id="becc0-154">Bir ekran görüntüsü aşağıda verilmiştir [Klasik Azure portalı](https://manage.windowsazure.com) istemci tarafı şifreleme anahtar kasasında depolanan anahtar kullanılarak şifrelenmiş bir blobu için.</span><span class="sxs-lookup"><span data-stu-id="becc0-154">Following is a screenshot from the [Azure Classic Portal](https://manage.windowsazure.com) for a blob that has been encrypted by using client-side encryption with a key stored in Key Vault.</span></span> <span data-ttu-id="becc0-155">**Keyıd** KEK davranan bir anahtar kasası anahtar URI'sini bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="becc0-155">The **KeyId** property is the URI for the key in Key Vault that acts as the KEK.</span></span> <span data-ttu-id="becc0-156">**EncryptedKey** özelliği CEK şifrelenmiş sürümünü içerir.</span><span class="sxs-lookup"><span data-stu-id="becc0-156">The **EncryptedKey** property contains the encrypted version of the CEK.</span></span>

![Şifreleme meta verileri içeren Blob meta verileri gösteren ekran görüntüsü](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> <span data-ttu-id="becc0-158">BlobEncryptionPolicy Oluşturucusu bakarsanız, bu bir anahtar ve/veya bir çözümleyici alabilen görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="becc0-158">If you look at the BlobEncryptionPolicy constructor, you will see that it can accept a key and/or a resolver.</span></span> <span data-ttu-id="becc0-159">Şu anda mevcut sağ çözümleyici için şifreleme kullanamazsınız, çünkü şimdi varsayılan anahtar destekleyen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="becc0-159">Be aware that right now you cannot use a resolver for encryption because it does not currently support a default key.</span></span>
> 
> 

## <a name="decrypt-blob-and-download"></a><span data-ttu-id="becc0-160">Blob şifresini çözmek ve indirme</span><span class="sxs-lookup"><span data-stu-id="becc0-160">Decrypt blob and download</span></span>
<span data-ttu-id="becc0-161">Şifre çözme, aslında çözümleyici sınıflarını kullanarak yaptığınızda algılama adıdır.</span><span class="sxs-lookup"><span data-stu-id="becc0-161">Decryption is really when using the Resolver classes make sense.</span></span> <span data-ttu-id="becc0-162">Bu yüzden anahtarı almak ve anahtar blob arasındaki ilişkiyi unutmayın için bir sebep şifreleme için kullanılan anahtar kimliği blob meta verilerinde ilişkilendirilir.</span><span class="sxs-lookup"><span data-stu-id="becc0-162">The ID of the key used for encryption is associated with the blob in its metadata, so there is no reason for you to retrieve the key and remember the association between key and blob.</span></span> <span data-ttu-id="becc0-163">Yalnızca anahtar anahtar kasasına olmaya devam ettiğinden emin olmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="becc0-163">You just have to make sure that the key remains in Key Vault.</span></span>   

<span data-ttu-id="becc0-164">Özel anahtar bir RSA anahtarı, anahtar kasasına kalır şekilde gerçekleşmesi şifre çözme için CEK içeren blob meta verilerden şifrelenmiş anahtar şifre çözme için anahtar Kasası'na gönderilir.</span><span class="sxs-lookup"><span data-stu-id="becc0-164">The private key of an RSA Key remains in Key Vault, so for decryption to occur, the Encrypted Key from the blob metadata that contains the CEK is sent to Key Vault for decryption.</span></span>

<span data-ttu-id="becc0-165">Yeni karşıya yüklediğiniz blob şifresini çözmek için aşağıdakileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="becc0-165">Add the following to decrypt the blob that you just uploaded.</span></span>

```csharp
// In this case, we will not pass a key and only pass the resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> <span data-ttu-id="becc0-166">Birkaç anahtar yönetimi, dahil olmak üzere kolaylaştırmak için çözümleyiciler diğer tür vardır: AggregateKeyResolver ve CachingKeyResolver.</span><span class="sxs-lookup"><span data-stu-id="becc0-166">There are a couple of other kinds of resolvers to make key management easier, including: AggregateKeyResolver and CachingKeyResolver.</span></span>
> 
> 

## <a name="use-key-vault-secrets"></a><span data-ttu-id="becc0-167">Anahtar kasası gizlilikleri kullanın</span><span class="sxs-lookup"><span data-stu-id="becc0-167">Use Key Vault secrets</span></span>
<span data-ttu-id="becc0-168">Aslında bir simetrik anahtar gizli olduğu için bir gizli anahtar istemci tarafı şifreleme ile kullanılacak şekilde SymmetricKey sınıftır.</span><span class="sxs-lookup"><span data-stu-id="becc0-168">The way to use a secret with client-side encryption is via the SymmetricKey class because a secret is essentially a symmetric key.</span></span> <span data-ttu-id="becc0-169">Ancak, yukarıda belirtildiği gibi anahtar kasasında bir gizlilik SymmetricKey için tam olarak eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="becc0-169">But, as noted above, a secret in Key Vault does not map exactly to a SymmetricKey.</span></span> <span data-ttu-id="becc0-170">Anlamak için birkaç şey vardır:</span><span class="sxs-lookup"><span data-stu-id="becc0-170">There are a few things to understand:</span></span>

* <span data-ttu-id="becc0-171">Bir SymmetricKey anahtarında sabit uzunlukta olması gerekir: 128, 192, 256, 384 veya 512 bit.</span><span class="sxs-lookup"><span data-stu-id="becc0-171">The key in a SymmetricKey has to be a fixed length: 128, 192, 256, 384, or 512 bits.</span></span>
* <span data-ttu-id="becc0-172">Bir SymmetricKey anahtarında Base64 ile kodlanmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="becc0-172">The key in a SymmetricKey should be Base64 encoded.</span></span>
* <span data-ttu-id="becc0-173">SymmetricKey kullanılacak bir anahtar kasası gizli anahtarı kasaya "application/octet-stream" içerik türü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="becc0-173">A Key Vault secret that will be used as a SymmetricKey needs to have a Content Type of "application/octet-stream" in Key Vault.</span></span>

<span data-ttu-id="becc0-174">İşte bir örnek SymmetricKey kullanılabilir anahtar kasasında bir gizli anahtar oluşturma PowerShell'de.</span><span class="sxs-lookup"><span data-stu-id="becc0-174">Here is an example in PowerShell of creating a secret in Key Vault that can be used as a SymmetricKey.</span></span>
<span data-ttu-id="becc0-175">Lütfen $key, sabit kodlanmış değeri yalnızca Tanıtım amaçlı olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="becc0-175">Please note that the hard coded value, $key, is for demonstration purpose only.</span></span> <span data-ttu-id="becc0-176">Kendi kodunuzu bu anahtarı oluşturmak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="becc0-176">In your own code you'll want to generate this key.</span></span>

```csharp
// Here we are making a 128-bit key so we have 16 characters.
//     The characters are in the ASCII range of UTF8 so they are
//    each 1 byte. 16 x 8 = 128.
$key = "qwertyuiopasdfgh"
$b = [System.Text.Encoding]::UTF8.GetBytes($key)
$enc = [System.Convert]::ToBase64String($b)
$secretvalue = ConvertTo-SecureString $enc -AsPlainText -Force

// Substitute the VaultName and Name in this command.
$secret = Set-AzureKeyVaultSecret -VaultName 'ContoseKeyVault' -Name 'TestSecret2' -SecretValue $secretvalue -ContentType "application/octet-stream"
```

<span data-ttu-id="becc0-177">Konsol uygulamanızın bu gizlilik bir SymmetricKey olarak almak için önce araması olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="becc0-177">In your console application, you can use the same call as before to retrieve this secret as a SymmetricKey.</span></span>

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
<span data-ttu-id="becc0-178">Bu kadar.</span><span class="sxs-lookup"><span data-stu-id="becc0-178">That's it.</span></span> <span data-ttu-id="becc0-179">Keyfini çıkarın!</span><span class="sxs-lookup"><span data-stu-id="becc0-179">Enjoy!</span></span>

## <a name="next-steps"></a><span data-ttu-id="becc0-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="becc0-180">Next steps</span></span>
<span data-ttu-id="becc0-181">Microsoft Azure depolama C# ile kullanma hakkında daha fazla bilgi için bkz: [.NET için Microsoft Azure Storage istemci Kitaplığı](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="becc0-181">For more information about using Microsoft Azure Storage with C#, see [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="becc0-182">Blob REST API'si hakkında daha fazla bilgi için bkz: [Blob hizmeti REST API'si](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span><span class="sxs-lookup"><span data-stu-id="becc0-182">For more information about the Blob REST API, see [Blob Service REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span></span>

<span data-ttu-id="becc0-183">Microsoft Azure depolama en son bilgiler için Git [Microsoft Azure depolama ekibi blogu](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="becc0-183">For the latest information on Microsoft Azure Storage, go to the [Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>
