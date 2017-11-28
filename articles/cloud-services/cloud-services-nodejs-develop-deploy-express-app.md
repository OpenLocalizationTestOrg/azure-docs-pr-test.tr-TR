---
title: aaaWeb Express (Node.js) ile uygulama | Microsoft Docs
description: "Merhaba bulut hizmeti öğretici oluşturur ve nasıl toouse hello Express modülü gösteren bir öğretici."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 24f8e7ef-e90d-4554-9b1e-a9b31d5824e5
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 91921bfbe137eeca9a110d4cb18eb57b46b0060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="f5de6-103">Bir Azure bulut hizmeti Express kullanarak bir Node.js web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5de6-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="f5de6-104">Node.js hello çekirdek çalışma zamanı en az bir işlev kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="f5de6-104">Node.js includes a minimal set of functionality in hello core runtime.</span></span>
<span data-ttu-id="f5de6-105">Geliştiriciler genellikle bir Node.js uygulaması geliştirilirken 3 taraf modülleri tooprovide ek işlevini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f5de6-105">Developers often use 3rd party modules tooprovide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="f5de6-106">Bu öğreticide hello kullanarak yeni bir uygulama oluşturacaksınız [Express] [ Express] modül Node.js web uygulamaları oluşturmak için bir MVC çerçevesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="f5de6-106">In this tutorial you will create a new application using hello [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="f5de6-107">Tamamlanan hello uygulamasının ekran görüntüsü aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f5de6-107">A screenshot of hello completed application is below:</span></span>

![Hoş Geldiniz tooExpress Azure'da gösteren bir web tarayıcısı](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="f5de6-109">Bir bulut hizmeti projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5de6-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="f5de6-110">Hello aşağıdaki gerçekleştirme adımları toocreate yeni bir bulut hizmeti projesi 'expressapp' adlı:</span><span class="sxs-lookup"><span data-stu-id="f5de6-110">Perform hello following steps toocreate a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="f5de6-111">Merhaba gelen **Başlat menüsü** veya **Başlat ekranında**, arama **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="f5de6-111">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="f5de6-112">Son olarak, sağ **Windows PowerShell** seçip **yönetici olarak çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="f5de6-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Azure PowerShell simgesi](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="f5de6-114">Değiştirme dizinleri toohello **c:\\düğümü** dizin ve aşağıdaki komutları toocreate adlı yeni bir çözüm hello enter **expressapp** ve adında bir web rolü **WebRole1** :</span><span class="sxs-lookup"><span data-stu-id="f5de6-114">Change directories toohello **c:\\node** directory and then enter hello following commands toocreate a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="f5de6-115">Varsayılan olarak, **Add-AzureNodeWebRole** Node.js daha eski bir sürümü kullanır.</span><span class="sxs-lookup"><span data-stu-id="f5de6-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="f5de6-116">Merhaba **kümesi AzureServiceProjectRole** deyimi yukarıdaki Azure toouse v0.10.21 düğümünün bildirir.</span><span class="sxs-lookup"><span data-stu-id="f5de6-116">hello **Set-AzureServiceProjectRole** statement above instructs Azure toouse v0.10.21 of Node.</span></span>  <span data-ttu-id="f5de6-117">Not hello parametreleri büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="f5de6-117">Note hello parameters are case-sensitive.</span></span>  <span data-ttu-id="f5de6-118">Merhaba doğru Node.js sürümünü hello denetleyerek seçilmiş doğrulayabilirsiniz **motorları** özelliğinde **WebRole1\package.json**.</span><span class="sxs-lookup"><span data-stu-id="f5de6-118">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="f5de6-119">Hızlı yükleme</span><span class="sxs-lookup"><span data-stu-id="f5de6-119">Install Express</span></span>
1. <span data-ttu-id="f5de6-120">Merhaba hızlı Oluşturucu komutu aşağıdaki hello vererek yükleyin:</span><span class="sxs-lookup"><span data-stu-id="f5de6-120">Install hello Express generator by issuing hello following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="f5de6-121">Merhaba hello npm komutunun çıkışını benzer toohello sonuç aşağıdaki gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="f5de6-121">hello output of hello npm command should look similar toohello result below.</span></span> 
   
    ![Windows PowerShell görüntüleme hello çıktısını hello npm express komutu yükleyin.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="f5de6-123">Değiştirme dizinleri toohello **WebRole1** dizin ve kullanım hello express komutu toogenerate yeni bir uygulama:</span><span class="sxs-lookup"><span data-stu-id="f5de6-123">Change directories toohello **WebRole1** directory and use hello express command toogenerate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="f5de6-124">İstendiğinde toooverwrite önceki uygulamanızı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f5de6-124">You will be prompted toooverwrite your earlier application.</span></span> <span data-ttu-id="f5de6-125">Girin **y** veya **Evet** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="f5de6-125">Enter **y** or **yes** toocontinue.</span></span> <span data-ttu-id="f5de6-126">Hızlı Başlangıç app.js dosya ve uygulamanızı oluşturmak için bir klasör yapısı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f5de6-126">Express will generate hello app.js file and a folder structure for building your application.</span></span>
   
    ![Merhaba hello express komutunun çıktısı](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="f5de6-128">Merhaba package.json dosyasında tanımlanan tooinstall ek bağımlılıklar hello aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="f5de6-128">tooinstall additional dependencies defined in hello package.json file, enter hello following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![Merhaba npm Hello çıktısını yükleme komutu](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="f5de6-130">Kullanım hello şu komutu toocopy hello **bin/www** çok dosya**server.js**.</span><span class="sxs-lookup"><span data-stu-id="f5de6-130">Use hello following command toocopy hello **bin/www** file too**server.js**.</span></span> <span data-ttu-id="f5de6-131">Merhaba bulut hizmeti, bu uygulama için hello giriş noktası bulabilmesi budur.</span><span class="sxs-lookup"><span data-stu-id="f5de6-131">This is so hello cloud service can find hello entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="f5de6-132">Bu komut tamamlandıktan sonra olmalıdır bir **server.js** hello WebRole1 dizindeki dosyayı.</span><span class="sxs-lookup"><span data-stu-id="f5de6-132">After this command completes, you should have a **server.js** file in hello WebRole1 directory.</span></span>
5. <span data-ttu-id="f5de6-133">Merhaba değiştirme **server.js** tooremove hello birini '.' hello satır aşağıdaki karakterler.</span><span class="sxs-lookup"><span data-stu-id="f5de6-133">Modify hello **server.js** tooremove one of hello '.' characters from hello following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="f5de6-134">Bu değişikliği yaptıktan sonra hello satırı aşağıdaki gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="f5de6-134">After making this modification, hello line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="f5de6-135">Biz hello dosya taşınmış olduğundan bu değişikliği gerekli değildir (önceki adıyla **bin/www**,) toohello gerektiği hello uygulama dosyası ile aynı dizinde.</span><span class="sxs-lookup"><span data-stu-id="f5de6-135">This change is required since we moved hello file (formerly **bin/www**,) toohello same directory as hello app file being required.</span></span> <span data-ttu-id="f5de6-136">Bu değişikliği yaptıktan sonra hello Kaydet **server.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="f5de6-136">After making this change, save hello **server.js** file.</span></span>
6. <span data-ttu-id="f5de6-137">Komut toorun hello hello Azure öykünücüsü uygulamasında aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="f5de6-137">Use hello following command toorun hello application in hello Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Hoş Geldiniz tooexpress içeren bir web sayfası.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a><span data-ttu-id="f5de6-139">Merhaba görünümü değiştirme</span><span class="sxs-lookup"><span data-stu-id="f5de6-139">Modifying hello View</span></span>
<span data-ttu-id="f5de6-140">Şimdi "Hoş Geldiniz tooExpress Azure" Merhaba iletiyi hello görüntüle toodisplay değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f5de6-140">Now modify hello view toodisplay hello message "Welcome tooExpress in Azure".</span></span>

1. <span data-ttu-id="f5de6-141">Aşağıdaki komut tooopen hello index.jade dosyasına hello girin:</span><span class="sxs-lookup"><span data-stu-id="f5de6-141">Enter hello following command tooopen hello index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![Merhaba index.jade dosyasının içeriğini başlangıç.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="f5de6-143">Jade Express uygulamaları tarafından kullanılan hello varsayılan görünüm altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="f5de6-143">Jade is hello default view engine used by Express applications.</span></span> <span data-ttu-id="f5de6-144">Merhaba Jade görünüm altyapısı hakkında daha fazla bilgi için bkz: [http://jade-lang.com][http://jade-lang.com].</span><span class="sxs-lookup"><span data-stu-id="f5de6-144">For more information on hello Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="f5de6-145">Metnin son satırını Hello ekleyerek değiştirmek **azure'da**.</span><span class="sxs-lookup"><span data-stu-id="f5de6-145">Modify hello last line of text by appending **in Azure**.</span></span>
   
   ![Merhaba son satırında Hello index.jade dosyasını okur: p Hoş Geldiniz çok\#{title} Azure'da](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="f5de6-147">Merhaba dosyayı kaydedip Not Defteri'nden çıkın.</span><span class="sxs-lookup"><span data-stu-id="f5de6-147">Save hello file and exit Notepad.</span></span>
4. <span data-ttu-id="f5de6-148">Tarayıcınızı yenileyin ve değişikliklerinizi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f5de6-148">Refresh your browser and you will see your changes.</span></span>
   
   ![Bir tarayıcı penceresinde hello sayfası Azure Hoş Geldiniz tooExpress içerir.](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="f5de6-150">Sınama hello uygulamadan sonra hello kullan **Stop-AzureEmulator** cmdlet toostop hello öykünücüsü.</span><span class="sxs-lookup"><span data-stu-id="f5de6-150">After testing hello application, use hello **Stop-AzureEmulator** cmdlet toostop hello emulator.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="f5de6-151">Yayımlama hello uygulama tooAzure</span><span class="sxs-lookup"><span data-stu-id="f5de6-151">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="f5de6-152">Hello Azure PowerShell penceresinde hello kullan **Publish-AzureServiceProject** cmdlet toodeploy hello uygulama tooa bulut hizmeti</span><span class="sxs-lookup"><span data-stu-id="f5de6-152">In hello Azure PowerShell window, use hello **Publish-AzureServiceProject** cmdlet toodeploy hello application tooa cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="f5de6-153">Merhaba dağıtım işlemi tamamlandıktan sonra tarayıcınızı açın ve hello web sayfasını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="f5de6-153">Once hello deployment operation completes, your browser will open and display hello web page.</span></span>

![Merhaba Express sayfasını gösteren bir web tarayıcısı.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="f5de6-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f5de6-156">Next steps</span></span>
<span data-ttu-id="f5de6-157">Daha fazla bilgi için bkz: Merhaba [Node.js Geliştirici Merkezi](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="f5de6-157">For more information, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


