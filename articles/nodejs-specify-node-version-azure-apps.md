---
title: "aaaSpecifying Node.js sürümünü"
description: "Nasıl toospecify hello Azure Web siteleri ve bulut Hizmetleri tarafından kullanılan Node.js sürümünü öğrenin"
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 09c27bfc43c132b6d66f9a2943179e06ee75bedc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a><span data-ttu-id="1850a-103">Bir Azure uygulamasında Node.js sürümünü belirtme</span><span class="sxs-lookup"><span data-stu-id="1850a-103">Specifying a Node.js version in an Azure application</span></span>
<span data-ttu-id="1850a-104">Bir Node.js uygulaması barındırdığında, uygulamanızın belirli bir Node.js sürümünü kullandığı tooensure isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1850a-104">When hosting a Node.js application, you may want tooensure that your application uses a specific version of Node.js.</span></span> <span data-ttu-id="1850a-105">Vardır birkaç yolu tooaccomplish bu Azure üzerinde barındırılan uygulamalar için.</span><span class="sxs-lookup"><span data-stu-id="1850a-105">There are several ways tooaccomplish this for applications hosted on Azure.</span></span>

## <a name="default-versions"></a><span data-ttu-id="1850a-106">Varsayılan sürümleri</span><span class="sxs-lookup"><span data-stu-id="1850a-106">Default versions</span></span>
<span data-ttu-id="1850a-107">Azure tarafından sağlanan hello Node.js sürümleri sürekli olarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1850a-107">hello Node.js versions provided by Azure are constantly updated.</span></span> <span data-ttu-id="1850a-108">Aksi belirtilmediği sürece hello belirtilen varsayılan sürüm hello `WEBSITE_NODE_DEFAULT_VERSION` ortam değişkeni kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1850a-108">Unless otherwise specified, hello default version that is specified in hello `WEBSITE_NODE_DEFAULT_VERSION` environment variable will be used.</span></span> <span data-ttu-id="1850a-109">toooverride hello adımları bu makalenin aşağıdaki bölümlerde bu varsayılan değeri</span><span class="sxs-lookup"><span data-stu-id="1850a-109">toooverride this default value, follow hello steps in following sections of this article</span></span>

> [!NOTE]
> <span data-ttu-id="1850a-110">Azure bulut hizmeti (web veya çalışan rolü) uygulamanızı barındırma ve ilk kez hello uygulama dağıtılan hello ise, Azure toouse deneyecek, geliştirme ortamınızı yüklediğiniz gibi aynı Node.js sürümünü Merhaba, Azure üzerinde kullanılabilir hello varsayılan sürümlerinden birini eşleşir.</span><span class="sxs-lookup"><span data-stu-id="1850a-110">If you are hosting your application in an Azure Cloud Service (web or worker role,) and it is hello first time you have deployed hello application, Azure will attempt toouse hello same version of Node.js as you have installed on your development environment if it matches one of hello default versions available on Azure.</span></span>
>
>

## <a name="versioning-with-packagejson"></a><span data-ttu-id="1850a-111">Package.json sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="1850a-111">Versioning with package.json</span></span>
<span data-ttu-id="1850a-112">Node.js toobe tooyour aşağıdaki hello ekleyerek kullanılan hello sürümü belirtebilirsiniz **package.json** dosyası:</span><span class="sxs-lookup"><span data-stu-id="1850a-112">You can specify hello version of Node.js toobe used by adding hello following tooyour **package.json** file:</span></span>

    "engines":{"node":version}

<span data-ttu-id="1850a-113">Burada *sürüm* hello belirli bir sürüm numarası toouse değil.</span><span class="sxs-lookup"><span data-stu-id="1850a-113">Where *version* is hello specific version number toouse.</span></span> <span data-ttu-id="1850a-114">Sürüm, daha karmaşık koşulları belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1850a-114">You can specify more complex conditions for version, such as:</span></span>

    "engines":{"node": "0.6.22 || 0.8.x"}

<span data-ttu-id="1850a-115">0.6.22 hello sürümlerinden barındırma ortamı hello kullanılabilir olmadığından, hello yüksek kullanılabilir serisi olacaktır hello 0,8 yerine - 0.8.4 kullanılan sürümü.</span><span class="sxs-lookup"><span data-stu-id="1850a-115">Since 0.6.22 is not one of hello versions available in hello hosting environment, hello highest version of hello 0.8 series that is available will be used instead - 0.8.4.</span></span>

## <a name="versioning-websites-with-app-settings"></a><span data-ttu-id="1850a-116">Uygulama ayarları ile Web siteleri sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="1850a-116">Versioning Websites with App Settings</span></span>
<span data-ttu-id="1850a-117">Merhaba uygulamada bir Web sitesi barındırıyorsanız, hello ortam değişkeni ayarlayabilirsiniz **WEBSITE_NODE_DEFAULT_VERSION** toohello istediğiniz sürümü.</span><span class="sxs-lookup"><span data-stu-id="1850a-117">If you are hosting hello application in a Website, you can set hello environment variable **WEBSITE_NODE_DEFAULT_VERSION** toohello desired version.</span></span>

## <a name="versioning-cloud-services-with-powershell"></a><span data-ttu-id="1850a-118">PowerShell ile sürüm bulut Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="1850a-118">Versioning Cloud Services with PowerShell</span></span>
<span data-ttu-id="1850a-119">Bir bulut hizmeti hello uygulamada barındırma ve Azure PowerShell kullanarak hello uygulama dağıtıyorsanız, hello kullanarak hello varsayılan Node.js sürümünü kılabilirsiniz **kümesi AzureServiceProjectRole** PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="1850a-119">If you are hosting hello application in a Cloud Service, and are deploying hello application using Azure PowerShell, you can override hello default Node.js version by using hello **Set-AzureServiceProjectRole** PowerShell cmdlet.</span></span> <span data-ttu-id="1850a-120">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="1850a-120">For example:</span></span>

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

<span data-ttu-id="1850a-121">Hello deyimi yukarıda Not hello parametreleri büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="1850a-121">Note hello parameters in hello above statement are case-sensitive.</span></span>  <span data-ttu-id="1850a-122">Merhaba doğru Node.js sürümünü hello denetleyerek seçilmiş doğrulayabilirsiniz **motorları** , rolün özelliğinde **package.json**.</span><span class="sxs-lookup"><span data-stu-id="1850a-122">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in your role's **package.json**.</span></span>

<span data-ttu-id="1850a-123">Merhaba de kullanabilirsiniz **Get-AzureServiceProjectRoleRuntime** tooretrieve bulut hizmet olarak barındırılan uygulamalar için kullanılabilir Node.js sürümlerinin bir listesi.</span><span class="sxs-lookup"><span data-stu-id="1850a-123">You can also use hello **Get-AzureServiceProjectRoleRuntime** tooretrieve a list of Node.js versions available for applications hosted as a Cloud Service.</span></span>  <span data-ttu-id="1850a-124">Her zaman bu listede projenizi bağlıdır Node.js hello sürümü olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1850a-124">Always verify hello version of Node.js your project depends on is in this list.</span></span>

## <a name="using-a-custom-version-with-azure-websites"></a><span data-ttu-id="1850a-125">Özel bir sürüm ile Azure Web siteleri kullanma</span><span class="sxs-lookup"><span data-stu-id="1850a-125">Using a custom version with Azure Websites</span></span>
<span data-ttu-id="1850a-126">Azure Node.js birkaç varsayılan sürümü sağlarken toouse varsayılan olarak sağlanmayan bir sürümünü isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1850a-126">While Azure provides several default versions of Node.js, you may want toouse a version that is not provided by default.</span></span> <span data-ttu-id="1850a-127">Uygulamanız bir Azure Web sitesi olarak barındırılıyorsa, bunu hello kullanarak gerçekleştirebilirsiniz **iisnode.yml** dosya.</span><span class="sxs-lookup"><span data-stu-id="1850a-127">If your application is hosted as an Azure Website, you can accomplish this by using hello **iisnode.yml** file.</span></span> <span data-ttu-id="1850a-128">Merhaba aşağıdaki adımlar bir Azure Web sitesi özel bir Node.Js sürümünü kullanarak hello işleminde size rehberlik:</span><span class="sxs-lookup"><span data-stu-id="1850a-128">hello following steps walk through hello process of using a custom version of Node.Js with an Azure Website:</span></span>

1. <span data-ttu-id="1850a-129">Yeni bir dizin oluşturun ve ardından oluşturun bir **server.js** hello dizini içindeki dosya.</span><span class="sxs-lookup"><span data-stu-id="1850a-129">Create a new directory, and then create a **server.js** file within hello directory.</span></span> <span data-ttu-id="1850a-130">Merhaba **server.js** dosya hello şunları içermelidir:</span><span class="sxs-lookup"><span data-stu-id="1850a-130">hello **server.js** file should contain hello following:</span></span>

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    <span data-ttu-id="1850a-131">Bu hello Web sitesine göz atarken kullanılan hello Node.js sürümünü görüntüler.</span><span class="sxs-lookup"><span data-stu-id="1850a-131">This will display hello Node.js version being used when you browse hello website.</span></span>
2. <span data-ttu-id="1850a-132">Yeni Web sitesi ve Not hello hello sitenin adını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1850a-132">Create a new Website and note hello name of hello site.</span></span> <span data-ttu-id="1850a-133">Örneğin, hello aşağıdaki hello kullanır [Azure komut satırı araçları] toocreate adlı yeni bir Azure Web **numaralı**ve ardından hello Web sitesi için Git deposu etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="1850a-133">For example, hello following uses hello [Azure Command-line tools] toocreate a new Azure Website named **mywebsite**, and then enable a Git repository for hello website.</span></span>

        azure site create mywebsite --git
3. <span data-ttu-id="1850a-134">Adlı yeni bir dizin oluşturun **bin** hello içeren hello dizinin alt **server.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="1850a-134">Create a new directory named **bin** as a child of hello directory containing hello **server.js** file.</span></span>
4. <span data-ttu-id="1850a-135">Merhaba belirli sürümünü indirin **node.exe** (Merhaba Windows sürümü) ile uygulamanızı toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="1850a-135">Download hello specific version of **node.exe** (hello Windows version) that you wish toouse with your application.</span></span> <span data-ttu-id="1850a-136">Örneğin, kullanır hello **curl** toodownload sürüm 0.8.1:</span><span class="sxs-lookup"><span data-stu-id="1850a-136">For example, hello following uses **curl** toodownload version 0.8.1:</span></span>

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    <span data-ttu-id="1850a-137">Merhaba Kaydet **node.exe** hello dosyasına **bin** daha önce oluşturduğunuz klasör.</span><span class="sxs-lookup"><span data-stu-id="1850a-137">Save hello **node.exe** file into hello **bin** folder created previously.</span></span>
5. <span data-ttu-id="1850a-138">Oluşturma bir **iisnode.yml** hello aynı dosyayı hello olarak dizin **server.js** dosya ve ardından içerik toohello aşağıdaki hello ekleyin **iisnode.yml** dosyası:</span><span class="sxs-lookup"><span data-stu-id="1850a-138">Create an **iisnode.yml** file in hello same directory as hello **server.js** file, and then add hello following content toohello **iisnode.yml** file:</span></span>

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    <span data-ttu-id="1850a-139">Bu yol hello burada olduğu **node.exe** , Azure Web uygulaması toohello yayımladıktan sonra proje dosyasında bulunan olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1850a-139">This path is where hello **node.exe** file within your project will be located once you have published your application toohello Azure Website.</span></span>
6. <span data-ttu-id="1850a-140">Uygulamanızı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="1850a-140">Publish your application.</span></span> <span data-ttu-id="1850a-141">Örneğin, yeni bir Web sitesi hello--git parametresiyle önceki oluşturduğum olduğundan, hello aşağıdaki komutları hello uygulama dosyaları toomy yerel Git deposu ekleyin ve bunları toohello Web sitesi deposu gönderme:</span><span class="sxs-lookup"><span data-stu-id="1850a-141">For example, since I created a new website with hello --git parameter earlier, hello following commands will add hello application files toomy local Git repository, and then push them toohello website repository:</span></span>

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    <span data-ttu-id="1850a-142">Merhaba uygulaması yayımladıktan sonra hello Web sitesini bir tarayıcıda açın.</span><span class="sxs-lookup"><span data-stu-id="1850a-142">After hello application has published, open hello website in a browser.</span></span> <span data-ttu-id="1850a-143">Belirten iletiyi görmelisiniz "Merhaba Azure çalışan düğümü sürümünden: v0.8.1".</span><span class="sxs-lookup"><span data-stu-id="1850a-143">You should see a message stating "Hello from Azure running node version: v0.8.1".</span></span>

## <a name="next-steps"></a><span data-ttu-id="1850a-144">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="1850a-144">Next Steps</span></span>
<span data-ttu-id="1850a-145">Nasıl toospecify hello Node.js sürümü, uygulamanız tarafından kullanılan anladığınıza göre nasıl çok öğrenin[modüllerle çalışma], [bir Node.js Web sitenizi oluşturup dağıtacak](app-service-web/app-service-web-get-started-nodejs.md), ve [nasıl toouse hello Azure Mac ve Linux için komut satırı araçları].</span><span class="sxs-lookup"><span data-stu-id="1850a-145">Now that you understand how toospecify hello version of Node.js used by your application, learn how too[work with modules], [build and deploy a Node.js Web Site](app-service-web/app-service-web-get-started-nodejs.md), and [How toouse hello Azure Command-Line Tools for Mac and Linux].</span></span>

<span data-ttu-id="1850a-146">Daha fazla bilgi için bkz: Merhaba [Node.js Geliştirici Merkezi](https://azure.microsoft.com/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="1850a-146">For more information, see hello [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/).</span></span>

[nasıl toouse hello Azure Mac ve Linux için komut satırı araçları]:cli-install-nodejs.md
[Azure komut satırı araçları]:cli-install-nodejs.md
[modüllerle çalışma]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
