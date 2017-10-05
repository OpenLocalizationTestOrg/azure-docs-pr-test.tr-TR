---
title: "Node.js sürümünü belirtme"
description: "Azure Web siteleri ve bulut Hizmetleri tarafından kullanılan Node.js sürümünü belirleme konusunda bilgi edinin"
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
ms.openlocfilehash: 89627e6a877c9f65a5216c55f58f1c707ea25d44
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a><span data-ttu-id="061e4-103">Bir Azure uygulamasında Node.js sürümünü belirtme</span><span class="sxs-lookup"><span data-stu-id="061e4-103">Specifying a Node.js version in an Azure application</span></span>
<span data-ttu-id="061e4-104">Bir Node.js uygulaması barındırdığında, uygulamanızın belirli bir Node.js sürümünü kullandığından emin olmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="061e4-104">When hosting a Node.js application, you may want to ensure that your application uses a specific version of Node.js.</span></span> <span data-ttu-id="061e4-105">Bunu Azure üzerinde barındırılan uygulamalar için yapmanın birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="061e4-105">There are several ways to accomplish this for applications hosted on Azure.</span></span>

## <a name="default-versions"></a><span data-ttu-id="061e4-106">Varsayılan sürümleri</span><span class="sxs-lookup"><span data-stu-id="061e4-106">Default versions</span></span>
<span data-ttu-id="061e4-107">Azure tarafından sağlanan Node.js sürümleri sürekli olarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="061e4-107">The Node.js versions provided by Azure are constantly updated.</span></span> <span data-ttu-id="061e4-108">Aksi belirtilmediği sürece, belirtilen varsayılan sürüm `WEBSITE_NODE_DEFAULT_VERSION` ortam değişkeni kullanılır.</span><span class="sxs-lookup"><span data-stu-id="061e4-108">Unless otherwise specified, the default version that is specified in the `WEBSITE_NODE_DEFAULT_VERSION` environment variable will be used.</span></span> <span data-ttu-id="061e4-109">Bu varsayılan değeri geçersiz kılmak için bu makalenin aşağıdaki bölümlerdeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="061e4-109">To override this default value, follow the steps in following sections of this article</span></span>

> [!NOTE]
> <span data-ttu-id="061e4-110">Azure bulut hizmeti (web veya çalışan rolü) uygulamanızı barındırma ve uygulama dağıttığınız ilk kez ise, Azure Azure üzerinde kullanılabilir varsayılan sürümlerini biriyle eşleşiyorsa, geliştirme ortamınızı yüklediğiniz gibi Node.js aynı sürümünü kullanmayı dener.</span><span class="sxs-lookup"><span data-stu-id="061e4-110">If you are hosting your application in an Azure Cloud Service (web or worker role,) and it is the first time you have deployed the application, Azure will attempt to use the same version of Node.js as you have installed on your development environment if it matches one of the default versions available on Azure.</span></span>
>
>

## <a name="versioning-with-packagejson"></a><span data-ttu-id="061e4-111">Package.json sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="061e4-111">Versioning with package.json</span></span>
<span data-ttu-id="061e4-112">Aşağıdakileri ekleyerek kullanılacak Node.js sürümünü belirtebilirsiniz, **package.json** dosyası:</span><span class="sxs-lookup"><span data-stu-id="061e4-112">You can specify the version of Node.js to be used by adding the following to your **package.json** file:</span></span>

    "engines":{"node":version}

<span data-ttu-id="061e4-113">Burada *sürüm* kullanılacak belirli bir sürüm numarası.</span><span class="sxs-lookup"><span data-stu-id="061e4-113">Where *version* is the specific version number to use.</span></span> <span data-ttu-id="061e4-114">Sürüm, daha karmaşık koşulları belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="061e4-114">You can specify more complex conditions for version, such as:</span></span>

    "engines":{"node": "0.6.22 || 0.8.x"}

<span data-ttu-id="061e4-115">0.6.22 sürümlerinden barındırma ortamında kullanılabilir olmadığından, yüksek kullanılabilir serisi olacaktır 0,8 yerine - 0.8.4 kullanılan sürümü.</span><span class="sxs-lookup"><span data-stu-id="061e4-115">Since 0.6.22 is not one of the versions available in the hosting environment, the highest version of the 0.8 series that is available will be used instead - 0.8.4.</span></span>

## <a name="versioning-websites-with-app-settings"></a><span data-ttu-id="061e4-116">Uygulama ayarları ile Web siteleri sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="061e4-116">Versioning Websites with App Settings</span></span>
<span data-ttu-id="061e4-117">Bir Web uygulamasında barındırıyorsanız, ortam değişkeni ayarlayabilirsiniz **WEBSITE_NODE_DEFAULT_VERSION** istediğiniz sürümü için.</span><span class="sxs-lookup"><span data-stu-id="061e4-117">If you are hosting the application in a Website, you can set the environment variable **WEBSITE_NODE_DEFAULT_VERSION** to the desired version.</span></span>

## <a name="versioning-cloud-services-with-powershell"></a><span data-ttu-id="061e4-118">PowerShell ile sürüm bulut Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="061e4-118">Versioning Cloud Services with PowerShell</span></span>
<span data-ttu-id="061e4-119">Bir bulut hizmet uygulamasında barındırma ve Azure PowerShell kullanarak uygulama dağıtıyorsanız, kullanarak varsayılan Node.js sürümünü kılabilirsiniz **kümesi AzureServiceProjectRole** PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="061e4-119">If you are hosting the application in a Cloud Service, and are deploying the application using Azure PowerShell, you can override the default Node.js version by using the **Set-AzureServiceProjectRole** PowerShell cmdlet.</span></span> <span data-ttu-id="061e4-120">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="061e4-120">For example:</span></span>

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

<span data-ttu-id="061e4-121">Yukarıdaki deyimindeki parametreleri büyük/küçük harfe duyarlıdır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="061e4-121">Note the parameters in the above statement are case-sensitive.</span></span>  <span data-ttu-id="061e4-122">Node.js doğru sürümü seçilmiştir denetleyerek doğrulayabilirsiniz **motorları** , rolün özelliğinde **package.json**.</span><span class="sxs-lookup"><span data-stu-id="061e4-122">You can verify the correct version of Node.js has been selected by checking the **engines** property in your role's **package.json**.</span></span>

<span data-ttu-id="061e4-123">Aynı zamanda **Get-AzureServiceProjectRoleRuntime** bulut hizmet olarak barındırılan uygulamalar için kullanılabilir Node.js sürümlerinin bir listesi alınamadı.</span><span class="sxs-lookup"><span data-stu-id="061e4-123">You can also use the **Get-AzureServiceProjectRoleRuntime** to retrieve a list of Node.js versions available for applications hosted as a Cloud Service.</span></span>  <span data-ttu-id="061e4-124">Her zaman bu listede projenizi bağlıdır Node.js sürümü olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="061e4-124">Always verify the version of Node.js your project depends on is in this list.</span></span>

## <a name="using-a-custom-version-with-azure-websites"></a><span data-ttu-id="061e4-125">Özel bir sürüm ile Azure Web siteleri kullanma</span><span class="sxs-lookup"><span data-stu-id="061e4-125">Using a custom version with Azure Websites</span></span>
<span data-ttu-id="061e4-126">Azure Node.js birkaç varsayılan sürümü sağlarken, varsayılan olarak sağlanmayan bir sürümünü kullanmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="061e4-126">While Azure provides several default versions of Node.js, you may want to use a version that is not provided by default.</span></span> <span data-ttu-id="061e4-127">Uygulamanız bir Azure Web sitesi olarak barındırılıyorsa, bunu kullanarak gerçekleştirebilirsiniz **iisnode.yml** dosya.</span><span class="sxs-lookup"><span data-stu-id="061e4-127">If your application is hosted as an Azure Website, you can accomplish this by using the **iisnode.yml** file.</span></span> <span data-ttu-id="061e4-128">Aşağıdaki adımlar, bir Azure Web sitesi özel bir Node.Js sürümünü kullanarak sürecinde yol:</span><span class="sxs-lookup"><span data-stu-id="061e4-128">The following steps walk through the process of using a custom version of Node.Js with an Azure Website:</span></span>

1. <span data-ttu-id="061e4-129">Yeni bir dizin oluşturun ve ardından oluşturun bir **server.js** dizin içindeki dosya.</span><span class="sxs-lookup"><span data-stu-id="061e4-129">Create a new directory, and then create a **server.js** file within the directory.</span></span> <span data-ttu-id="061e4-130">**Server.js** dosyası şunları içermelidir:</span><span class="sxs-lookup"><span data-stu-id="061e4-130">The **server.js** file should contain the following:</span></span>

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    <span data-ttu-id="061e4-131">Bu Web sitesine göz atarken kullanılan Node.js sürümünü görüntüler.</span><span class="sxs-lookup"><span data-stu-id="061e4-131">This will display the Node.js version being used when you browse the website.</span></span>
2. <span data-ttu-id="061e4-132">Yeni bir Web sitesi oluşturun ve site adını not edin.</span><span class="sxs-lookup"><span data-stu-id="061e4-132">Create a new Website and note the name of the site.</span></span> <span data-ttu-id="061e4-133">Örneğin, aşağıdaki amaçlarla [Azure komut satırı araçları] adlı yeni bir Azure Web oluşturmak için **numaralı**ve Web sitesi için Git deposu etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="061e4-133">For example, the following uses the [Azure Command-line tools] to create a new Azure Website named **mywebsite**, and then enable a Git repository for the website.</span></span>

        azure site create mywebsite --git
3. <span data-ttu-id="061e4-134">Adlı yeni bir dizin oluşturun **bin** dizin içeren bir alt olarak **server.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="061e4-134">Create a new directory named **bin** as a child of the directory containing the **server.js** file.</span></span>
4. <span data-ttu-id="061e4-135">Belirli sürümünü indirin **node.exe** (Windows sürümü), uygulamanız ile kullanmak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="061e4-135">Download the specific version of **node.exe** (the Windows version) that you wish to use with your application.</span></span> <span data-ttu-id="061e4-136">Örneğin, aşağıdaki amaçlarla **curl** 0.8.1 sürümü karşıdan yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="061e4-136">For example, the following uses **curl** to download version 0.8.1:</span></span>

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    <span data-ttu-id="061e4-137">Kaydet **node.exe** içine dosya **bin** daha önce oluşturduğunuz klasör.</span><span class="sxs-lookup"><span data-stu-id="061e4-137">Save the **node.exe** file into the **bin** folder created previously.</span></span>
5. <span data-ttu-id="061e4-138">Oluşturma bir **iisnode.yml** aynı dizinde dosya **server.js** dosya ve ardından aşağıdaki içeriği ekleyin **iisnode.yml** dosyası:</span><span class="sxs-lookup"><span data-stu-id="061e4-138">Create an **iisnode.yml** file in the same directory as the **server.js** file, and then add the following content to the **iisnode.yml** file:</span></span>

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    <span data-ttu-id="061e4-139">Bu yol yerdir **node.exe** Azure Web uygulamanıza yayımladıktan sonra proje dosyasında bulunan olacaktır.</span><span class="sxs-lookup"><span data-stu-id="061e4-139">This path is where the **node.exe** file within your project will be located once you have published your application to the Azure Website.</span></span>
6. <span data-ttu-id="061e4-140">Uygulamanızı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="061e4-140">Publish your application.</span></span> <span data-ttu-id="061e4-141">Örneğin, yeni bir Web sitesi--git parametresiyle önceki oluşturduğum olduğundan, aşağıdaki komutları uygulama dosyalarını my yerel Git deposu ekleyin ve bunları Web sitesi depoya gönderme:</span><span class="sxs-lookup"><span data-stu-id="061e4-141">For example, since I created a new website with the --git parameter earlier, the following commands will add the application files to my local Git repository, and then push them to the website repository:</span></span>

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    <span data-ttu-id="061e4-142">Uygulama yayımladıktan sonra Web sitesini bir tarayıcıda açın.</span><span class="sxs-lookup"><span data-stu-id="061e4-142">After the application has published, open the website in a browser.</span></span> <span data-ttu-id="061e4-143">Belirten iletiyi görmelisiniz "Merhaba Azure çalışan düğümü sürümünden: v0.8.1".</span><span class="sxs-lookup"><span data-stu-id="061e4-143">You should see a message stating "Hello from Azure running node version: v0.8.1".</span></span>

## <a name="next-steps"></a><span data-ttu-id="061e4-144">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="061e4-144">Next Steps</span></span>
<span data-ttu-id="061e4-145">Uygulamanız tarafından kullanılan Node.js sürümünü belirtin, öğrenme yapacağınızı anladığınıza göre nasıl [modüllerle çalışma], [bir Node.js Web sitenizi oluşturup dağıtacak](app-service-web/app-service-web-get-started-nodejs.md), ve [Mac ve Linux için Azure komut satırı araçları kullanmak üzere nasıl].</span><span class="sxs-lookup"><span data-stu-id="061e4-145">Now that you understand how to specify the version of Node.js used by your application, learn how to [work with modules], [build and deploy a Node.js Web Site](app-service-web/app-service-web-get-started-nodejs.md), and [How to use the Azure Command-Line Tools for Mac and Linux].</span></span>

<span data-ttu-id="061e4-146">Daha fazla bilgi için bkz. [Node.js Geliştirici Merkezi](https://azure.microsoft.com/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="061e4-146">For more information, see the [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/).</span></span>

<span data-ttu-id="061e4-147">[Mac ve Linux için Azure komut satırı araçları kullanmak üzere nasıl]:cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="061e4-147">[How to use the Azure Command-Line Tools for Mac and Linux]:cli-install-nodejs.md</span></span>
<span data-ttu-id="061e4-148">[Azure komut satırı araçları]:cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="061e4-148">[Azure Command-line tools]:cli-install-nodejs.md</span></span>
<span data-ttu-id="061e4-149">[modüllerle çalışma]: nodejs-use-node-modules-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="061e4-149">[work with modules]: nodejs-use-node-modules-azure-apps.md</span></span>
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
