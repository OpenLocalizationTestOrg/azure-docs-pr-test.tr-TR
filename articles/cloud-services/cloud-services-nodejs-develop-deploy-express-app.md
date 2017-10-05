---
title: "Web uygulaması Express (Node.js) ile | Microsoft Docs"
description: "Bulut hizmeti öğretici oluşturur ve Express modülü kullanmak nasıl gösteren bir öğretici."
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
ms.openlocfilehash: 54b715695e24786ec4e8dfcabefc648d76179c8b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="74f36-103">Bir Azure bulut hizmeti Express kullanarak bir Node.js web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="74f36-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="74f36-104">Node.js işlevselliği en az bir dizi çekirdek çalışma zamanı'nda içerir.</span><span class="sxs-lookup"><span data-stu-id="74f36-104">Node.js includes a minimal set of functionality in the core runtime.</span></span>
<span data-ttu-id="74f36-105">Geliştiriciler 3 taraf modülleri bir Node.js uygulaması geliştirilirken ek işlevsellik sağlamak için çoğunlukla kullanır.</span><span class="sxs-lookup"><span data-stu-id="74f36-105">Developers often use 3rd party modules to provide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="74f36-106">Bu öğreticide kullanarak yeni bir uygulama oluşturacaksınız [Express] [ Express] modül Node.js web uygulamaları oluşturmak için bir MVC çerçevesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="74f36-106">In this tutorial you will create a new application using the [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="74f36-107">Tamamlanmış uygulamanın bir ekran görüntüsü aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="74f36-107">A screenshot of the completed application is below:</span></span>

![Hoş Geldiniz Azure Express'te gösteren bir web tarayıcısı](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="74f36-109">Bir bulut hizmeti projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="74f36-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="74f36-110">'Expressapp' adlı yeni bir bulut hizmeti projesi oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="74f36-110">Perform the following steps to create a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="74f36-111">Gelen **Başlat menüsü** veya **Başlat ekranında**, arama **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="74f36-111">From the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="74f36-112">Son olarak, sağ **Windows PowerShell** seçip **yönetici olarak çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="74f36-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Azure PowerShell simgesi](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="74f36-114">Değiştirme dizinleri **c:\\düğümü** dizin ve adlı yeni bir çözüm oluşturmak için aşağıdaki komutları girin **expressapp** ve adında bir web rolü **WebRole1**:</span><span class="sxs-lookup"><span data-stu-id="74f36-114">Change directories to the **c:\\node** directory and then enter the following commands to create a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="74f36-115">Varsayılan olarak, **Add-AzureNodeWebRole** Node.js daha eski bir sürümü kullanır.</span><span class="sxs-lookup"><span data-stu-id="74f36-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="74f36-116">**Kümesi AzureServiceProjectRole** yukarıdaki ifade v0.10.21 düğümünün kullanmak için Azure bildirir.</span><span class="sxs-lookup"><span data-stu-id="74f36-116">The **Set-AzureServiceProjectRole** statement above instructs Azure to use v0.10.21 of Node.</span></span>  <span data-ttu-id="74f36-117">Parametreleri büyük/küçük harfe duyarlıdır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="74f36-117">Note the parameters are case-sensitive.</span></span>  <span data-ttu-id="74f36-118">Node.js doğru sürümü seçilmiştir denetleyerek doğrulayabilirsiniz **motorları** özelliğinde **WebRole1\package.json**.</span><span class="sxs-lookup"><span data-stu-id="74f36-118">You can verify the correct version of Node.js has been selected by checking the **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="74f36-119">Hızlı yükleme</span><span class="sxs-lookup"><span data-stu-id="74f36-119">Install Express</span></span>
1. <span data-ttu-id="74f36-120">Hızlı Oluşturucu, aşağıdaki komutu gönderdikten yükleyin:</span><span class="sxs-lookup"><span data-stu-id="74f36-120">Install the Express generator by issuing the following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="74f36-121">Npm komutunun çıkışını aşağıdaki sonucu benzer görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="74f36-121">The output of the npm command should look similar to the result below.</span></span> 
   
    ![Windows PowerShell npm çıktısını görüntüleme yükleme express komutu.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="74f36-123">Değiştirme dizinleri **WebRole1** dizin ve yeni bir uygulama oluşturmak için hızlı komutunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="74f36-123">Change directories to the **WebRole1** directory and use the express command to generate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="74f36-124">Önceki uygulamanızı üzerine istenir.</span><span class="sxs-lookup"><span data-stu-id="74f36-124">You will be prompted to overwrite your earlier application.</span></span> <span data-ttu-id="74f36-125">Girin **y** veya **Evet** devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="74f36-125">Enter **y** or **yes** to continue.</span></span> <span data-ttu-id="74f36-126">Express app.js dosya ve uygulamanızı oluşturmak için bir klasör yapısı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="74f36-126">Express will generate the app.js file and a folder structure for building your application.</span></span>
   
    ![Hızlı komut çıktısı](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="74f36-128">Package.json dosyasında tanımlanan ek bağımlılıklar yüklemek için aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="74f36-128">To install additional dependencies defined in the package.json file, enter the following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![Npm çıktısını yükleme komutu](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="74f36-130">Kopyalamak için aşağıdaki komutu kullanın **bin/www** dosya **server.js**.</span><span class="sxs-lookup"><span data-stu-id="74f36-130">Use the following command to copy the **bin/www** file to **server.js**.</span></span> <span data-ttu-id="74f36-131">Bulut hizmeti, bu uygulama için giriş noktası bulabilmesi budur.</span><span class="sxs-lookup"><span data-stu-id="74f36-131">This is so the cloud service can find the entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="74f36-132">Bu komut tamamlandıktan sonra olmalıdır bir **server.js** WebRole1 dizindeki dosyayı.</span><span class="sxs-lookup"><span data-stu-id="74f36-132">After this command completes, you should have a **server.js** file in the WebRole1 directory.</span></span>
5. <span data-ttu-id="74f36-133">Değiştirme **server.js** birini kaldırmak için '.' aşağıdaki satırı karakterlerinden.</span><span class="sxs-lookup"><span data-stu-id="74f36-133">Modify the **server.js** to remove one of the '.' characters from the following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="74f36-134">Bu değişikliği yaptıktan sonra satırı aşağıdaki gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="74f36-134">After making this modification, the line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="74f36-135">Biz dosya taşınmış olduğundan bu değişikliği gerekli değildir (önceki adıyla **bin/www**,) için gerekli uygulama dosyası ile aynı dizinde.</span><span class="sxs-lookup"><span data-stu-id="74f36-135">This change is required since we moved the file (formerly **bin/www**,) to the same directory as the app file being required.</span></span> <span data-ttu-id="74f36-136">Bu değişikliği yaptıktan sonra kaydedin **server.js** dosya.</span><span class="sxs-lookup"><span data-stu-id="74f36-136">After making this change, save the **server.js** file.</span></span>
6. <span data-ttu-id="74f36-137">Uygulama Azure öykünücüsünde çalıştırmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="74f36-137">Use the following command to run the application in the Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Express Hoş Geldiniz içeren bir web sayfası.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-the-view"></a><span data-ttu-id="74f36-139">Görünümü değiştirme</span><span class="sxs-lookup"><span data-stu-id="74f36-139">Modifying the View</span></span>
<span data-ttu-id="74f36-140">Şimdi "Hoş Geldiniz için Express içinde Azure" iletisini görüntülemek için görünümü değiştirin.</span><span class="sxs-lookup"><span data-stu-id="74f36-140">Now modify the view to display the message "Welcome to Express in Azure".</span></span>

1. <span data-ttu-id="74f36-141">İndex.jade dosyayı açmak için aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="74f36-141">Enter the following command to open the index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![İndex.jade dosyasının içeriği.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="74f36-143">Jade Express uygulamaları tarafından kullanılan varsayılan görünüm altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="74f36-143">Jade is the default view engine used by Express applications.</span></span> <span data-ttu-id="74f36-144">Jade görünüm altyapısı hakkında daha fazla bilgi için bkz: [http://jade-lang.com][http://jade-lang.com].</span><span class="sxs-lookup"><span data-stu-id="74f36-144">For more information on the Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="74f36-145">Metnin son satırını ekleyerek değiştirmek **azure'da**.</span><span class="sxs-lookup"><span data-stu-id="74f36-145">Modify the last line of text by appending **in Azure**.</span></span>
   
   ![Son satırı index.jade dosyasını okur: p Hoş Geldiniz için \#{title} Azure'da](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="74f36-147">Dosyayı kaydedin ve Not Defteri'nden çıkın.</span><span class="sxs-lookup"><span data-stu-id="74f36-147">Save the file and exit Notepad.</span></span>
4. <span data-ttu-id="74f36-148">Tarayıcınızı yenileyin ve değişikliklerinizi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="74f36-148">Refresh your browser and you will see your changes.</span></span>
   
   ![Bir tarayıcı penceresi Sayfası'na Hoş Geldiniz Azure Express'te içerir.](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="74f36-150">Uygulamayı test etme sonra kullanın **Stop-AzureEmulator** öykünücü durdurmak için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="74f36-150">After testing the application, use the **Stop-AzureEmulator** cmdlet to stop the emulator.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="74f36-151">Uygulamayı Azure'a yayımlama</span><span class="sxs-lookup"><span data-stu-id="74f36-151">Publishing the Application to Azure</span></span>
<span data-ttu-id="74f36-152">Azure PowerShell penceresinde kullanmak **Publish-AzureServiceProject** bir bulut hizmeti uygulamayı dağıtmak için cmdlet</span><span class="sxs-lookup"><span data-stu-id="74f36-152">In the Azure PowerShell window, use the **Publish-AzureServiceProject** cmdlet to deploy the application to a cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="74f36-153">Dağıtım işlemi tamamlandıktan sonra tarayıcınızı açın ve web sayfasını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="74f36-153">Once the deployment operation completes, your browser will open and display the web page.</span></span>

![Express sayfasını gösteren bir web tarayıcısı.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="74f36-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="74f36-156">Next steps</span></span>
<span data-ttu-id="74f36-157">Daha fazla bilgi için bkz. [Node.js Geliştirici Merkezi](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="74f36-157">For more information, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


