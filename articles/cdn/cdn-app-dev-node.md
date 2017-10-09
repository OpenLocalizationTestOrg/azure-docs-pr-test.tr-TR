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
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="9c911-103">Azure CDN ile geliştirmeye başlama</span><span class="sxs-lookup"><span data-stu-id="9c911-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c911-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="9c911-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="9c911-105">.NET</span><span class="sxs-lookup"><span data-stu-id="9c911-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="9c911-106">Merhaba kullanabilirsiniz [Node.js için Azure CDN SDK](https://www.npmjs.com/package/azure-arm-cdn) tooautomate oluşturulması ve CDN profili ve uç noktaları yönetimi.</span><span class="sxs-lookup"><span data-stu-id="9c911-106">You can use hello [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="9c911-107">Bu öğreticide birkaç hello kullanılabilir işlemleri gösteren basit bir Node.js konsol uygulaması hello oluşturulmasını açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9c911-107">This tutorial walks through hello creation of a simple Node.js console application that demonstrates several of hello available operations.</span></span>  <span data-ttu-id="9c911-108">Bu öğretici tasarlanmamış toodescribe hello Azure CDN SDK tüm yönlerini Node.js için ayrıntılı olarak yazılımıdır.</span><span class="sxs-lookup"><span data-stu-id="9c911-108">This tutorial is not intended toodescribe all aspects of hello Azure CDN SDK for Node.js in detail.</span></span>

<span data-ttu-id="9c911-109">toocomplete Bu öğretici, zaten olmalıdır [Node.js](http://www.nodejs.org) **4.x.x** veya üzeri yüklenir ve yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="9c911-109">toocomplete this tutorial, you should already have [Node.js](http://www.nodejs.org) **4.x.x** or higher installed and configured.</span></span>  <span data-ttu-id="9c911-110">Node.js uygulamanızı toocreate istediğiniz herhangi bir metin düzenleyicisi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c911-110">You can use any text editor you want toocreate your Node.js application.</span></span>  <span data-ttu-id="9c911-111">toowrite Bu öğretici, kullandım [Visual Studio Code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="9c911-111">toowrite this tutorial, I used [Visual Studio Code](https://code.visualstudio.com).</span></span>  

> [!TIP]
> <span data-ttu-id="9c911-112">Merhaba [Bu öğreticinin tamamlanan projeden](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) MSDN'de indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="9c911-112">hello [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a><span data-ttu-id="9c911-113">Projenizi oluşturmak ve NPM bağımlılıkları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9c911-113">Create your project and add NPM dependencies</span></span>
<span data-ttu-id="9c911-114">Bizim CDN profili için bir kaynak grubu oluşturduk artık ve verilen bizim Azure AD uygulama izni toomanage CDN profili ve uç noktaları grubu içindeki göre biz uygulamamızı oluşturmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c911-114">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission toomanage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="9c911-115">Bir klasör toostore uygulamanızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9c911-115">Create a folder toostore your application.</span></span>  <span data-ttu-id="9c911-116">Geçerli yolda hello Node.js araçları ile bir konsoldan geçerli konumu toothis yeni klasör ayarlamak ve projenizi yürüterek başlatma:</span><span class="sxs-lookup"><span data-stu-id="9c911-116">From a console with hello Node.js tools in your current path, set your current location toothis new folder and initialize your project by executing:</span></span>

    npm init

<span data-ttu-id="9c911-117">Ardından olacak bir dizi soru tooinitialize projenizi sunulan.</span><span class="sxs-lookup"><span data-stu-id="9c911-117">You will then be presented a series of questions tooinitialize your project.</span></span>  <span data-ttu-id="9c911-118">İçin **giriş noktası**, Bu öğretici kullanır *app.js*.</span><span class="sxs-lookup"><span data-stu-id="9c911-118">For **entry point**, this tutorial uses *app.js*.</span></span>  <span data-ttu-id="9c911-119">Aşağıdaki örneğine hello my diğer seçenekleri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c911-119">You can see my other choices in hello following example.</span></span>

![NPM init çıktı](./media/cdn-app-dev-node/cdn-npm-init.png)

<span data-ttu-id="9c911-121">Projemizin şimdi ile başlatılmış bir *packages.json* dosya.</span><span class="sxs-lookup"><span data-stu-id="9c911-121">Our project is now initialized with a *packages.json* file.</span></span>  <span data-ttu-id="9c911-122">Projemizin bazı Azure kitaplıkları NPM paketlerinde bulunan toouse geçiyor.</span><span class="sxs-lookup"><span data-stu-id="9c911-122">Our project is going toouse some Azure libraries contained in NPM packages.</span></span>  <span data-ttu-id="9c911-123">Merhaba Node.js (ms-rest-azure) için Azure istemci çalışma zamanı ve hello Azure CDN istemci kitaplığı Node.js (azure arm cd) için kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="9c911-123">We'll use hello Azure Client Runtime for Node.js (ms-rest-azure) and hello Azure CDN Client Library for Node.js (azure-arm-cd).</span></span>  <span data-ttu-id="9c911-124">Şimdi bu toohello proje bağımlılıkları olarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9c911-124">Let's add those toohello project as dependencies.</span></span>

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

<span data-ttu-id="9c911-125">Paketleri yapılır hello sonra yükleme, hello *package.json* dosya benzer toothis örnek (sürüm numaralarını farklı olabilir) görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="9c911-125">After hello packages are done installing, hello *package.json* file should look similar toothis example (version numbers may differ):</span></span>

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

<span data-ttu-id="9c911-126">Son olarak, Metin Düzenleyicisi'ni kullanarak bir boş metin dosyası oluşturun ve hello kök bizim proje klasörünün kaydedin *app.js*.</span><span class="sxs-lookup"><span data-stu-id="9c911-126">Finally, using your text editor, create a blank text file and save it in hello root of our project folder as *app.js*.</span></span>  <span data-ttu-id="9c911-127">Kod yazma hazır toobegin şimdi çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="9c911-127">We're now ready toobegin writing code.</span></span>

## <a name="requires-constants-authentication-and-structure"></a><span data-ttu-id="9c911-128">Sabitler, kimlik doğrulama ve yapısı gerektirir</span><span class="sxs-lookup"><span data-stu-id="9c911-128">Requires, constants, authentication, and structure</span></span>
<span data-ttu-id="9c911-129">İle *app.js* bizim düzenleyicisinde açın, şimdi yazılmış programımız temel yapısını hello Al.</span><span class="sxs-lookup"><span data-stu-id="9c911-129">With *app.js* open in our editor, let's get hello basic structure of our program written.</span></span>

1. <span data-ttu-id="9c911-130">Merhaba "Merhaba aşağıdaki ile Merhaba üstünde NPM paketlerimize gerektirir" ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9c911-130">Add hello "requires" for our NPM packages at hello top with hello following:</span></span>
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. <span data-ttu-id="9c911-131">Bizim yöntemler kullanacağı bazı sabitleri toodefine ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="9c911-131">We need toodefine some constants our methods will use.</span></span>  <span data-ttu-id="9c911-132">Merhaba aşağıdakileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9c911-132">Add hello following.</span></span>  <span data-ttu-id="9c911-133">Merhaba yer tutucular hello dahil olmak üzere, emin tooreplace olması  **&lt;köşeli&gt;**, gerektiği gibi kendi değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="9c911-133">Be sure tooreplace hello placeholders, including hello **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="9c911-134">Ardından, hello CDN management istemcisi örneği ve bizim kimlik bilgileri verin.</span><span class="sxs-lookup"><span data-stu-id="9c911-134">Next, we'll instantiate hello CDN management client and give it our credentials.</span></span>
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="9c911-135">Tek tek kullanıcı kimlik doğrulaması kullanıyorsanız, bu iki satır biraz farklı görünecektir.</span><span class="sxs-lookup"><span data-stu-id="9c911-135">If you are using individual user authentication, these two lines will look slightly different.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="9c911-136">Yalnızca bir hizmet sorumlusu yerine toohave tek tek kullanıcı kimlik doğrulaması seçerek, bu kod örneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="9c911-136">Only use this code sample if you are choosing toohave individual user authentication instead of a service principal.</span></span>  <span data-ttu-id="9c911-137">Gizli kalmasını ve tek tek kullanıcı kimlik bilgilerinizi dikkatli tooguard olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9c911-137">Be careful tooguard your individual user credentials and keep them secret.</span></span>
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="9c911-138">Merhaba öğelerde emin tooreplace olması  **&lt;köşeli&gt;**  bilgileri ile Merhaba düzeltin.</span><span class="sxs-lookup"><span data-stu-id="9c911-138">Be sure tooreplace hello items in **&lt;angle brackets&gt;** with hello correct information.</span></span>  <span data-ttu-id="9c911-139">İçin `<redirect URI>`, hello yeniden yönlendirme URI'si Azure AD'de Merhaba uygulaması kaydolurken girdiğiniz kullanın.</span><span class="sxs-lookup"><span data-stu-id="9c911-139">For `<redirect URI>`, use hello redirect URI you entered when you registered hello application in Azure AD.</span></span>
4. <span data-ttu-id="9c911-140">Bizim Node.js konsol uygulaması tootake bazı komut satırı parametreleri geçiyor.</span><span class="sxs-lookup"><span data-stu-id="9c911-140">Our Node.js console application is going tootake some command-line parameters.</span></span>  <span data-ttu-id="9c911-141">Şimdi en az bir doğrulama parametresi geçirildi.</span><span class="sxs-lookup"><span data-stu-id="9c911-141">Let's validate that at least one parameter was passed.</span></span>
   
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
5. <span data-ttu-id="9c911-142">Bize toohello ana burada size hangi parametreler geçirilmiş dayalı tooother işlevleri kapalı dal programımız parçası getirir.</span><span class="sxs-lookup"><span data-stu-id="9c911-142">That brings us toohello main part of our program, where we branch off tooother functions based on what parameters were passed.</span></span>
   
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
6. <span data-ttu-id="9c911-143">Programımız çeşitli yerlerde biz toomake hello doğru sayıda parametre olarak geçirilen ve doğru görünmüyorsa bazı Yardım görüntüleme emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c911-143">At several places in our program, we'll need toomake sure hello right number of parameters were passed in and display some help if they don't look correct.</span></span>  <span data-ttu-id="9c911-144">İşlevler toodo, oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="9c911-144">Let's create functions toodo that.</span></span>
   
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
7. <span data-ttu-id="9c911-145">Son olarak, geri işiniz bittiğinde yöntemi toocall ihtiyaç duydukları şekilde hello işlevleri biz hello CDN yönetim istemcisini kullanarak zaman uyumsuz,.</span><span class="sxs-lookup"><span data-stu-id="9c911-145">Finally, hello functions we'll be using on hello CDN management client are asynchronous, so they need a method toocall back when they're done.</span></span>  <span data-ttu-id="9c911-146">Merhaba CDN Yönetimi istemcisi (varsa) hello çıktısını görüntülemek ve düzgün bir şekilde hello programdan çıkmak olalım.</span><span class="sxs-lookup"><span data-stu-id="9c911-146">Let's make one that can display hello output from hello CDN management client (if any) and exit hello program gracefully.</span></span>
   
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

<span data-ttu-id="9c911-147">Merhaba temel programımız yapısını yazılır, biz bizim parametrelere göre çağrılan hello işlevler oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c911-147">Now that hello basic structure of our program is written, we should create hello functions called based on our parameters.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="9c911-148">Liste CDN profili ve uç noktaları</span><span class="sxs-lookup"><span data-stu-id="9c911-148">List CDN profiles and endpoints</span></span>
<span data-ttu-id="9c911-149">Kod toolist ile bizim varolan profil ve uç noktaları başlayalım.</span><span class="sxs-lookup"><span data-stu-id="9c911-149">Let's start with code toolist our existing profiles and endpoints.</span></span>  <span data-ttu-id="9c911-150">My kod açıklamaları beklenen hello sözdizimi sağlar, bu nedenle, her bir parametreyi gider biliyoruz.</span><span class="sxs-lookup"><span data-stu-id="9c911-150">My code comments provide hello expected syntax so we know where each parameter goes.</span></span>

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

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="9c911-151">CDN profili ve uç noktaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="9c911-151">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="9c911-152">Ardından, biz hello işlevleri toocreate profilleri ve uç noktaları yazacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9c911-152">Next, we'll write hello functions toocreate profiles and endpoints.</span></span>

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

## <a name="purge-an-endpoint"></a><span data-ttu-id="9c911-153">Bir uç noktası</span><span class="sxs-lookup"><span data-stu-id="9c911-153">Purge an endpoint</span></span>
<span data-ttu-id="9c911-154">Tooperform bizim programında isteyebilirsiniz, hello uç noktası oluşturuldu varsayıldığında, bizim endpoint içeriğinde bir ortak görev temizleme.</span><span class="sxs-lookup"><span data-stu-id="9c911-154">Assuming hello endpoint has been created, one common task that we might want tooperform in our program is purging content in our endpoint.</span></span>

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="9c911-155">CDN profili ve uç noktaları Sil</span><span class="sxs-lookup"><span data-stu-id="9c911-155">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="9c911-156">Biz içerecektir hello son işlevi uç noktaları ve profilleri siler.</span><span class="sxs-lookup"><span data-stu-id="9c911-156">hello last function we will include deletes endpoints and profiles.</span></span>

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

## <a name="running-hello-program"></a><span data-ttu-id="9c911-157">Merhaba programı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9c911-157">Running hello program</span></span>
<span data-ttu-id="9c911-158">Biz şimdi sık kullanılan bizim hata ayıklayıcıyı kullanma Node.js programımız yürütebilir veya hello konsolunda.</span><span class="sxs-lookup"><span data-stu-id="9c911-158">We can now execute our Node.js program using our favorite debugger or at hello console.</span></span>

> [!TIP]
> <span data-ttu-id="9c911-159">Visual Studio Code, hata ayıklayıcı olarak kullanıyorsanız, ortam toopass hello komut satırı parametreleri de yukarı tooset gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c911-159">If you're using Visual Studio Code as your debugger, you'll need tooset up your environment toopass in hello command-line parameters.</span></span>  <span data-ttu-id="9c911-160">Visual Studio Code olmadığından bu hello **lanuch.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="9c911-160">Visual Studio Code does this in hello **lanuch.json** file.</span></span>  <span data-ttu-id="9c911-161">Adlı bir özellik arayın **args** ve benzer toothis tanıyarak dize değerleri, parametre için bir dizi ekleyin: `"args": ["list", "profiles"]`.</span><span class="sxs-lookup"><span data-stu-id="9c911-161">Look for a property named **args** and add an array of string values for your parameters, so that it looks similar toothis:  `"args": ["list", "profiles"]`.</span></span>
> 
> 

<span data-ttu-id="9c911-162">Bizim profilleri listeleyerek başlayalım.</span><span class="sxs-lookup"><span data-stu-id="9c911-162">Let's start by listing our profiles.</span></span>

![Liste profilleri](./media/cdn-app-dev-node/cdn-list-profiles.png)

<span data-ttu-id="9c911-164">Biz, boş bir dizi geri aldı.</span><span class="sxs-lookup"><span data-stu-id="9c911-164">We got back an empty array.</span></span>  <span data-ttu-id="9c911-165">Herhangi bir profil bizim kaynak grubunda yok olduğundan, bu beklenir.</span><span class="sxs-lookup"><span data-stu-id="9c911-165">Since we don't have any profiles in our resource group, that's expected.</span></span>  <span data-ttu-id="9c911-166">Artık bir profili oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="9c911-166">Let's create a profile now.</span></span>

![Profil oluşturma](./media/cdn-app-dev-node/cdn-create-profile.png)

<span data-ttu-id="9c911-168">Şimdi, bir uç nokta ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="9c911-168">Now, let's add an endpoint.</span></span>

![Uç noktası oluşturma](./media/cdn-app-dev-node/cdn-create-endpoint.png)

<span data-ttu-id="9c911-170">Son olarak, şirketinizdeki bizim profilini silin.</span><span class="sxs-lookup"><span data-stu-id="9c911-170">Finally, let's delete our profile.</span></span>

![Profili Sil](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a><span data-ttu-id="9c911-172">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="9c911-172">Next Steps</span></span>
<span data-ttu-id="9c911-173">Bu kılavuzda toosee tamamlandı hello projeden [hello örnek indirme](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span><span class="sxs-lookup"><span data-stu-id="9c911-173">toosee hello completed project from this walkthrough, [download hello sample](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span></span>

<span data-ttu-id="9c911-174">Merhaba Node.js, görünüm hello için Azure CDN SDK toosee hello başvurusunu [başvuru](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span><span class="sxs-lookup"><span data-stu-id="9c911-174">toosee hello reference for hello Azure CDN SDK for Node.js, view hello [reference](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span></span>

<span data-ttu-id="9c911-175">Node.js, görünüm hello hello Azure SDK'sı üzerinde belgeleri ek toofind [tam başvuru](http://azure.github.io/azure-sdk-for-node/).</span><span class="sxs-lookup"><span data-stu-id="9c911-175">toofind additional documentation on hello Azure SDK for Node.js, view hello [full reference](http://azure.github.io/azure-sdk-for-node/).</span></span>

<span data-ttu-id="9c911-176">CDN kaynaklarınızı yönetmek [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9c911-176">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

