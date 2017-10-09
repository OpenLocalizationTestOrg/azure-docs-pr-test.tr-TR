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
ms.openlocfilehash: e387dd419a51b5b1df62d10ead97268e8295ff56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a>Öğretici: Şifrelemek ve şifresini Azure anahtar kasası kullanılarak Microsoft Azure Storage blobları
## <a name="introduction"></a>Giriş
Bu öğretici toomake kullanma Azure anahtar kasası ile istemci-tarafı depolama şifreleme kapsar. Nasıl anlatılmaktadır tooencrypt ve bu teknolojilerden bir konsol uygulamasında bir blob şifresini.

**Zaman toocomplete tahmini:** 20 dakika

Azure anahtar kasası hakkında genel bilgi için bkz: [Azure anahtar kasası nedir?](../../key-vault/key-vault-whatis.md).

Azure Storage istemci tarafı şifreleme hakkında genel bilgi için bkz: [istemci tarafı şifreleme ve Microsoft Azure depolama için Azure anahtar kasası](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

## <a name="prerequisites"></a>Ön koşullar
toocomplete Bu öğreticiyi izleyerek hello olması gerekir:

* Bir Azure Storage hesabı
* Visual Studio 2013 veya üzeri
* Azure PowerShell

## <a name="overview-of-client-side-encryption"></a>İstemci tarafı şifreleme genel bakış
Azure Storage istemci tarafı şifreleme genel bakış için bkz: [istemci tarafı şifreleme ve Microsoft Azure depolama için Azure anahtar kasası](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

Aşağıda, istemci tarafı şifreleme çalışma biçimine kısa bir açıklaması verilmiştir:

1. Hello Azure Storage istemci SDK simetrik anahtar bir kerelik kullan bir içerik şifreleme anahtarı (CEK) oluşturur.
2. Müşteri verileri bu CEK kullanılarak şifrelenir.
3. Merhaba CEK sonra (Merhaba anahtar şifreleme anahtarı (KEK) kullanılarak şifrelenir) paketlenir. Merhaba KEK anahtar bir tanımlayıcıyla tanımlanır ve asimetrik anahtar çifti ya da bir simetrik anahtar olması ve yerel olarak yönetilebilir veya Azure anahtar kasasında depolanan. Merhaba depolama istemcinin kendisi hiçbir zaman erişim toohello KEK olur. Yalnızca, anahtar kasası tarafından sağlanan hello anahtar kaydırma algoritması çağırır. Müşteriler toouse özel sağlayıcılar anahtarı sarmalama/bunlar istiyorsanız açmak için seçebilirsiniz.
4. Merhaba şifrelenmiş verileri ise toohello Azure depolama hizmeti karşıya yüklendi.

## <a name="set-up-your-azure-key-vault"></a>Azure anahtar kasanızı ayarlayın
Sipariş tooproceed Bu öğretici'de, aşağıdaki hello öğreticide özetlenen adımları toodo hello ihtiyacınız [Azure anahtar kasası ile çalışmaya başlama](../../key-vault/key-vault-get-started.md):

* Bir anahtar kasası oluşturun.
* Bir anahtar veya gizli toohello anahtar kasası ekleyin.
* Bir uygulamayı Azure Active Directory ile kaydedin.
* Merhaba uygulama toouse hello anahtar veya gizli yetkilendirin.

Merhaba ClientID Not ve bir uygulamayı Azure Active Directory'ye kaydedilirken oluşturulan ClientSecret yapın.

Her iki anahtarı hello anahtar kasasına oluşturun. Başlangıç Öğreticisi hello kalanı için adlarından hello kullanılan varsayıyoruz: ContosoKeyVault ve TestRSAKey1.

## <a name="create-a-console-application-with-packages-and-appsettings"></a>Paketler ve AppSettings bir konsol uygulaması oluşturun
Visual Studio'da yeni bir konsol uygulaması oluşturun.

Gerekli nuget paketlerini hello Paket Yöneticisi konsolu ekleyin.

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

AppSettings toohello App.Config ekleyin.

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

Merhaba aşağıdakileri ekleyin `using` deyimleri ve yapma emin tooadd bir başvuru tooSystem.Configuration toohello projesi.

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

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a>Yöntem tooget bir belirteç tooyour konsol uygulaması ekleyin
Merhaba aşağıdaki yöntemi tooauthenticate erişim tooyour anahtar kasası için gereken anahtar kasası sınıflar tarafından kullanılır.

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

## <a name="access-storage-and-key-vault-in-your-program"></a>Depolama ve anahtar kasası programınıza erişim
Hello ana işlevi, hello aşağıdaki kodu ekleyin.

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
> Anahtar kasası nesne modelleri
> 
> Gerçekte iki anahtar kasası nesnesi olduğunu toounderstand modeller toobe farkında önemlidir: bir REST API (KeyVault ad alanı) hello üzerinde dayanır ve hello diğer istemci tarafı şifreleme için bir uzantısıdır.
> 
> Merhaba anahtar kasası istemci hello REST API ile etkileşim kurar ve JSON Web anahtarları ve gizli anahtarları hello iki tür anahtar Kasası ' bulunan şeyler için anlar.
> 
> Azure Storage istemci tarafı şifreleme için özel olarak oluşturulmuş göründüğü sınıfları Hello anahtar kasası uzantılarıdır. Anahtarları (IKey) ve anahtar çözümleyici hello kavramı tabanlı sınıflar için bir arabirimi içerir. Tooknow gereken IKey iki uygulamaları vardır: RSAKey ve SymmetricKey. Bir anahtar kasası içerdiği hello şeyler ile toocoincide gerçekleşir, ancak bu noktada (Merhaba anahtarı ve gizli anahtar kasası istemci hello tarafından alınan IKey uygulamak için) bağımsız sınıfları etmektedir artık.
> 
> 

## <a name="encrypt-blob-and-upload"></a>BLOB şifrelemek ve karşıya yükleme
Merhaba aşağıdaki tooencrypt blob kod ve tooyour Azure depolama hesabı karşıya ekleyin. Merhaba **ResolveKeyAsync** yöntemi bir IKey döndürür.

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

Merhaba bir ekran görüntüsü aşağıda verilmiştir [Klasik Azure portalı](https://manage.windowsazure.com) istemci tarafı şifreleme anahtar kasasında depolanan anahtar kullanılarak şifrelenmiş bir blobu için. Merhaba **Keyıd** hello URI KEK hello gibi davranan bir anahtar kasası hello anahtar için bir özelliktir. Merhaba **EncryptedKey** özelliği hello şifrelenmiş hello CEK sürümünü içerir.

![Şifreleme meta verileri içeren Blob meta verileri gösteren ekran görüntüsü](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> Merhaba BlobEncryptionPolicy Oluşturucusu bakarsanız, bu bir anahtar ve/veya bir çözümleyici alabilen görürsünüz. Şu anda mevcut sağ çözümleyici için şifreleme kullanamazsınız, çünkü şimdi varsayılan anahtar destekleyen unutmayın.
> 
> 

## <a name="decrypt-blob-and-download"></a>Blob şifresini çözmek ve indirme
Ne zaman kullanarak izin ver hello çözümleyici şifre çözme gerçekten olduğu sınıflarının algılama. şifreleme için kullanılan hello anahtar Hello Kimliğini; böylece, tooretrieve hello anahtarı için bir sebep meta verilerinde hello blob ile ilişkili olan ve anahtar ve blob arasındaki ilişkiyi hello unutmayın. Yalnızca toomake hello anahtara anahtar kasasına kalmasını gerekir.   

Merhaba özel anahtar bir RSA anahtarı kalır anahtar kasasında böylece şifre çözme toooccur için hello şifrelenmiş anahtar CEK tooKey kasası şifre çözme için gönderilen hello içeren hello blob meta veriler.

Merhaba, yeni karşıya yüklediğiniz toodecrypt hello blob aşağıdaki ekleyin.

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> Birkaç diğer tür çözümleyiciler toomake anahtar yönetimi dahil olmak üzere kolaylaştırır: AggregateKeyResolver ve CachingKeyResolver.
> 
> 

## <a name="use-key-vault-secrets"></a>Anahtar kasası gizlilikleri kullanın
Gizli aslında bir simetrik anahtar hello yolu toouse gizli anahtarı istemci tarafı şifreleme ile Merhaba SymmetricKey sınıfı olduğundan. Ancak, yukarıda belirtildiği gibi anahtar kasasında bir gizlilik tooa SymmetricKey tam olarak eşleşmiyor. Birkaç şey toounderstand vardır:

* bir SymmetricKey Hello anahtarında sahip toobe sabit uzunluk: 128, 192, 256, 384 veya 512 bit.
* bir SymmetricKey Hello anahtarında Base64 ile kodlanmış olmalıdır.
* SymmetricKey kullanılacak bir anahtar kasası gizlilik toohave "application/octet-stream" anahtar kasasında bir içerik türü gerekiyor.

İşte bir örnek SymmetricKey kullanılabilir anahtar kasasında bir gizli anahtar oluşturma PowerShell'de.
Merhaba sabit kodlu değer, $key, yalnızca Tanıtım amaçlı olduğunu unutmayın. Kendi kodunuzu bu anahtarı toogenerate isteyeceksiniz.

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

Konsol uygulamanızın aynı tooretrieve gibi önce SymmetricKey bu gizli çağrı hello kullanabilirsiniz.

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
Bu kadar. Keyfini çıkarın!

## <a name="next-steps"></a>Sonraki adımlar
Microsoft Azure depolama C# ile kullanma hakkında daha fazla bilgi için bkz: [.NET için Microsoft Azure Storage istemci Kitaplığı](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Hello Blob REST API'si hakkında daha fazla bilgi için bkz: [Blob hizmeti REST API'si](https://msdn.microsoft.com/library/azure/dd135733.aspx).

Merhaba son hakkında bilgi için Microsoft Azure Storage, toohello gidin [Microsoft Azure depolama ekibi blogu](http://blogs.msdn.com/b/windowsazurestorage/).
