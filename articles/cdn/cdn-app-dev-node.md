---
title: "aaaGet Node.js için Azure CDN SDK hello ile başlatılan | Microsoft Docs"
description: "Bilgi nasıl toowrite Node.js uygulamaları toomanage Azure CDN."
services: cdn
documentationcenter: nodejs
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c4bb6a61-de3d-4f0c-9dca-202554c43dfa
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6c805e5fb8e0b471e8b248cb2f4b29efd6c85940
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cdn-development"></a>Azure CDN ile geliştirmeye başlama
> [!div class="op_single_selector"]
> * [Node.js](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

Merhaba kullanabilirsiniz [Node.js için Azure CDN SDK](https://www.npmjs.com/package/azure-arm-cdn) tooautomate oluşturulması ve CDN profili ve uç noktaları yönetimi.  Bu öğreticide birkaç hello kullanılabilir işlemleri gösteren basit bir Node.js konsol uygulaması hello oluşturulmasını açıklanmaktadır.  Bu öğretici tasarlanmamış toodescribe hello Azure CDN SDK tüm yönlerini Node.js için ayrıntılı olarak yazılımıdır.

toocomplete Bu öğretici, zaten olmalıdır [Node.js](http://www.nodejs.org) **4.x.x** veya üzeri yüklenir ve yapılandırılır.  Node.js uygulamanızı toocreate istediğiniz herhangi bir metin düzenleyicisi kullanabilirsiniz.  toowrite Bu öğretici, kullandım [Visual Studio Code](https://code.visualstudio.com).  

> [!TIP]
> Merhaba [Bu öğreticinin tamamlanan projeden](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) MSDN'de indirilebilir.
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a>Projenizi oluşturmak ve NPM bağımlılıkları ekleyin.
Bizim CDN profili için bir kaynak grubu oluşturduk artık ve verilen bizim Azure AD uygulama izni toomanage CDN profili ve uç noktaları grubu içindeki göre biz uygulamamızı oluşturmaya başlayabilirsiniz.

Bir klasör toostore uygulamanızı oluşturun.  Geçerli yolda hello Node.js araçları ile bir konsoldan geçerli konumu toothis yeni klasör ayarlamak ve projenizi yürüterek başlatma:

    npm init

Ardından olacak bir dizi soru tooinitialize projenizi sunulan.  İçin **giriş noktası**, Bu öğretici kullanır *app.js*.  Aşağıdaki örneğine hello my diğer seçenekleri görebilirsiniz.

![NPM init çıktı](./media/cdn-app-dev-node/cdn-npm-init.png)

Projemizin şimdi ile başlatılmış bir *packages.json* dosya.  Projemizin bazı Azure kitaplıkları NPM paketlerinde bulunan toouse geçiyor.  Merhaba Node.js (ms-rest-azure) için Azure istemci çalışma zamanı ve hello Azure CDN istemci kitaplığı Node.js (azure arm cd) için kullanacağız.  Şimdi bu toohello proje bağımlılıkları olarak ekleyin.

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

Paketleri yapılır hello sonra yükleme, hello *package.json* dosya benzer toothis örnek (sürüm numaralarını farklı olabilir) görünmelidir:

``` json
{
  "name": "cdn_node",
  "version": "1.0.0",
  "description": "Azure CDN Node.js tutorial project",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Cam Soper",
  "license": "MIT",
  "dependencies": {
    "azure-arm-cdn": "^0.2.1",
    "ms-rest-azure": "^1.14.4"
  }
}
```

Son olarak, Metin Düzenleyicisi'ni kullanarak bir boş metin dosyası oluşturun ve hello kök bizim proje klasörünün kaydedin *app.js*.  Kod yazma hazır toobegin şimdi çalışıyoruz.

## <a name="requires-constants-authentication-and-structure"></a>Sabitler, kimlik doğrulama ve yapısı gerektirir
İle *app.js* bizim düzenleyicisinde açın, şimdi yazılmış programımız temel yapısını hello Al.

1. Merhaba "Merhaba aşağıdaki ile Merhaba üstünde NPM paketlerimize gerektirir" ekleyin:
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. Bizim yöntemler kullanacağı bazı sabitleri toodefine ihtiyacımız var.  Merhaba aşağıdakileri ekleyin.  Merhaba yer tutucular hello dahil olmak üzere, emin tooreplace olması  **&lt;köşeli&gt;**, gerektiği gibi kendi değerlere sahip.
   
    ``` javascript
    //Tenant app constants
    const clientId = "<YOUR CLIENT ID>";
    const clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    const tenantId = "<YOUR TENANT ID>";
   
    //Application constants
    const subscriptionId = "<YOUR SUBSCRIPTION ID>";
    const resourceGroupName = "CdnConsoleTutorial";
    const resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. Ardından, hello CDN management istemcisi örneği ve bizim kimlik bilgileri verin.
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    Tek tek kullanıcı kimlik doğrulaması kullanıyorsanız, bu iki satır biraz farklı görünecektir.
   
   > [!IMPORTANT]
   > Yalnızca bir hizmet sorumlusu yerine toohave tek tek kullanıcı kimlik doğrulaması seçerek, bu kod örneği kullanın.  Gizli kalmasını ve tek tek kullanıcı kimlik bilgilerinizi dikkatli tooguard olmalıdır.
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    Merhaba öğelerde emin tooreplace olması  **&lt;köşeli&gt;**  bilgileri ile Merhaba düzeltin.  İçin `<redirect URI>`, hello yeniden yönlendirme URI'si Azure AD'de Merhaba uygulaması kaydolurken girdiğiniz kullanın.
4. Bizim Node.js konsol uygulaması tootake bazı komut satırı parametreleri geçiyor.  Şimdi en az bir doğrulama parametresi geçirildi.
   
   ```javascript
   //Collect command-line parameters
   var parms = process.argv.slice(2);
   
   //Do we have parameters?
   if(parms == null || parms.length == 0)
   {
       console.log("Not enough parameters!");
       console.log("Valid commands are list, delete, create, and purge.");
       process.exit(1);
   }
   ```
5. Bize toohello ana burada size hangi parametreler geçirilmiş dayalı tooother işlevleri kapalı dal programımız parçası getirir.
   
    ```javascript
    switch(parms[0].toLowerCase())
    {
        case "list":
            cdnList();
            break;
   
        case "create":
            cdnCreate();
            break;
   
        case "delete":
            cdnDelete();
            break;
   
        case "purge":
            cdnPurge();
            break;
   
        default:
            console.log("Valid commands are list, delete, create, and purge.");
            process.exit(1);
    }
    ```
6. Programımız çeşitli yerlerde biz toomake hello doğru sayıda parametre olarak geçirilen ve doğru görünmüyorsa bazı Yardım görüntüleme emin olmanız gerekir.  İşlevler toodo, oluşturalım.
   
   ```javascript
   function requireParms(parmCount) {
       if(parms.length < parmCount) {
           usageHelp(parms[0].toLowerCase());
           process.exit(1);
       }
   }
   
   function usageHelp(cmd) {
       console.log("Usage for " + cmd + ":");
       switch(cmd)
       {
           case "list":
               console.log("list profiles");
               console.log("list endpoints <profile name>");
               break;
   
           case "create":
               console.log("create profile <profile name>");
               console.log("create endpoint <profile name> <endpoint name> <origin hostname>");
               break;
   
           case "delete":
               console.log("delete profile <profile name>");
               console.log("delete endpoint <profile name> <endpoint name>");
               break;
   
           case "purge":
               console.log("purge <profile name> <endpoint name> <path>");
               break;
   
           default:
               console.log("Invalid command.");
       }
   }
   ```
7. Son olarak, geri işiniz bittiğinde yöntemi toocall ihtiyaç duydukları şekilde hello işlevleri biz hello CDN yönetim istemcisini kullanarak zaman uyumsuz,.  Merhaba CDN Yönetimi istemcisi (varsa) hello çıktısını görüntülemek ve düzgün bir şekilde hello programdan çıkmak olalım.
   
    ```javascript
    function callback(err, result, request, response) {
        if (err) {
            console.log(err);
            process.exit(1);
        } else {
            console.log((result == null) ? "Done!" : result);
            process.exit(0);
        }
    }
    ```

Merhaba temel programımız yapısını yazılır, biz bizim parametrelere göre çağrılan hello işlevler oluşturmanız gerekir.

## <a name="list-cdn-profiles-and-endpoints"></a>Liste CDN profili ve uç noktaları
Kod toolist ile bizim varolan profil ve uç noktaları başlayalım.  My kod açıklamaları beklenen hello sözdizimi sağlar, bu nedenle, her bir parametreyi gider biliyoruz.

```javascript
// list profiles
// list endpoints <profile name>
function cdnList(){
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profiles":
            console.log("Listing profiles...");
            cdnClient.profiles.listByResourceGroup(resourceGroupName, callback);
            break;

        case "endpoints":
            requireParms(3);
            console.log("Listing endpoints...");
            cdnClient.endpoints.listByProfile(parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a>CDN profili ve uç noktaları oluşturma
Ardından, biz hello işlevleri toocreate profilleri ve uç noktaları yazacaksınız.

```javascript
function cdnCreate() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profile":
            cdnCreateProfile();
            break;

        case "endpoint":
            cdnCreateEndpoint();
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}

// create profile <profile name>
function cdnCreateProfile() {
    requireParms(3);
    console.log("Creating profile...");
    var standardCreateParameters = {
        location: resourceLocation,
        sku: {
            name: 'Standard_Verizon'
        }
    };

    cdnClient.profiles.create(parms[2], standardCreateParameters, resourceGroupName, callback);
}

// create endpoint <profile name> <endpoint name> <origin hostname>        
function cdnCreateEndpoint() {
    requireParms(5);
    console.log("Creating endpoint...");
    var endpointProperties = {
        location: resourceLocation,
        origins: [{
            name: parms[4],
            hostName: parms[4]
        }]
    };

    cdnClient.endpoints.create(parms[3], endpointProperties, parms[2], resourceGroupName, callback);
}
```

## <a name="purge-an-endpoint"></a>Bir uç noktası
Tooperform bizim programında isteyebilirsiniz, hello uç noktası oluşturuldu varsayıldığında, bizim endpoint içeriğinde bir ortak görev temizleme.

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a>CDN profili ve uç noktaları Sil
Biz içerecektir hello son işlevi uç noktaları ve profilleri siler.

```javascript
function cdnDelete() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        // delete profile <profile name>
        case "profile":
            requireParms(3);
            console.log("Deleting profile...");
            cdnClient.profiles.deleteIfExists(parms[2], resourceGroupName, callback);
            break;

        // delete endpoint <profile name> <endpoint name>
        case "endpoint":
            requireParms(4);
            console.log("Deleting endpoint...");
            cdnClient.endpoints.deleteIfExists(parms[3], parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="running-hello-program"></a>Merhaba programı çalıştırma
Biz şimdi sık kullanılan bizim hata ayıklayıcıyı kullanma Node.js programımız yürütebilir veya hello konsolunda.

> [!TIP]
> Visual Studio Code, hata ayıklayıcı olarak kullanıyorsanız, ortam toopass hello komut satırı parametreleri de yukarı tooset gerekir.  Visual Studio Code olmadığından bu hello **lanuch.json** dosya.  Adlı bir özellik arayın **args** ve benzer toothis tanıyarak dize değerleri, parametre için bir dizi ekleyin: `"args": ["list", "profiles"]`.
> 
> 

Bizim profilleri listeleyerek başlayalım.

![Liste profilleri](./media/cdn-app-dev-node/cdn-list-profiles.png)

Biz, boş bir dizi geri aldı.  Herhangi bir profil bizim kaynak grubunda yok olduğundan, bu beklenir.  Artık bir profili oluşturalım.

![Profil oluşturma](./media/cdn-app-dev-node/cdn-create-profile.png)

Şimdi, bir uç nokta ekleyelim.

![Uç noktası oluşturma](./media/cdn-app-dev-node/cdn-create-endpoint.png)

Son olarak, şirketinizdeki bizim profilini silin.

![Profili Sil](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a>Sonraki Adımlar
Bu kılavuzda toosee tamamlandı hello projeden [hello örnek indirme](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).

Merhaba Node.js, görünüm hello için Azure CDN SDK toosee hello başvurusunu [başvuru](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).

Node.js, görünüm hello hello Azure SDK'sı üzerinde belgeleri ek toofind [tam başvuru](http://azure.github.io/azure-sdk-for-node/).

CDN kaynaklarınızı yönetmek [PowerShell](cdn-manage-powershell.md).

