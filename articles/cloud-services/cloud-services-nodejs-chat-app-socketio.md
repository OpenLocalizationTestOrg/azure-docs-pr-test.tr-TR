---
title: "Socket.IO kullanarak aaaNode.js uygulaması | Microsoft Docs"
description: "Nasıl bir node.js uygulamasında toouse Socket.IO Azure üzerinde barındırılan öğrenin."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 7f9435e0-7732-4aa1-a4df-ea0e894b847f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 47c6c4a748938959315b880340f41f31faab4ea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a><span data-ttu-id="65d9f-103">Bir Azure bulut hizmeti Socket.IO ile bir Node.js sohbet uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="65d9f-103">Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service</span></span>
<span data-ttu-id="65d9f-104">Socket.IO node.js sunucunuz ve istemcileriniz arasında arasında gerçek zamanlı iletişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="65d9f-104">Socket.IO provides realtime communication between between your node.js server and clients.</span></span> <span data-ttu-id="65d9f-105">Bu öğretici bir yuva barındırma aracılığıyla yol gösterir. G/ç Azure sohbet uygulamaya dayalı.</span><span class="sxs-lookup"><span data-stu-id="65d9f-105">This tutorial will walk you through hosting a socket.IO based chat application on Azure.</span></span> <span data-ttu-id="65d9f-106">Socket.IO ile ilgili daha fazla bilgi için bkz: <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="65d9f-106">For more information on Socket.IO, see <http://socket.io/>.</span></span>

<span data-ttu-id="65d9f-107">Tamamlanan hello uygulamasının ekran görüntüsü aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="65d9f-107">A screenshot of hello completed application is below:</span></span>

![Azure üzerinde barındırılan hello hizmet gösteren bir tarayıcı penceresi][completed-app]  

## <a name="prerequisites"></a><span data-ttu-id="65d9f-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="65d9f-109">Prerequisites</span></span>
<span data-ttu-id="65d9f-110">Ürünler aşağıdaki o hello emin olun ve bu makaledeki yüklü toosuccessfully tam hello örnek sürümleri:</span><span class="sxs-lookup"><span data-stu-id="65d9f-110">Ensure that hello following products and versions are installed toosuccessfully complete hello example in this article:</span></span>

* <span data-ttu-id="65d9f-111">[Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)'yu yükleme</span><span class="sxs-lookup"><span data-stu-id="65d9f-111">Install [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span></span>
* <span data-ttu-id="65d9f-112">[Node.js](https://nodejs.org/download/)’yi yükleme</span><span class="sxs-lookup"><span data-stu-id="65d9f-112">Install [Node.js](https://nodejs.org/download/)</span></span>
* <span data-ttu-id="65d9f-113">Yükleme [Python sürümü 2.7.10](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="65d9f-113">Install [Python version 2.7.10](https://www.python.org/)</span></span>

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="65d9f-114">Bir bulut hizmeti projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="65d9f-114">Create a Cloud Service Project</span></span>
<span data-ttu-id="65d9f-115">Merhaba aşağıdaki adımları Merhaba Socket.IO uygulaması barındıracak hello bulut hizmeti projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="65d9f-115">hello following steps create hello cloud service project that will host hello Socket.IO application.</span></span>

1. <span data-ttu-id="65d9f-116">Merhaba gelen **Başlat menüsü** veya **Başlat ekranında**, arama **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="65d9f-116">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="65d9f-117">Son olarak, sağ **Windows PowerShell** seçip **yönetici olarak çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="65d9f-117">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Azure PowerShell simgesi][powershell-menu]
2. <span data-ttu-id="65d9f-119">Adlı bir dizin oluşturun **c:\\düğümü**.</span><span class="sxs-lookup"><span data-stu-id="65d9f-119">Create a directory called **c:\\node**.</span></span> 
   
        PS C:\> md node
3. <span data-ttu-id="65d9f-120">Değiştirme dizinleri toohello **c:\\düğümü** dizini</span><span class="sxs-lookup"><span data-stu-id="65d9f-120">Change directories toohello **c:\\node** directory</span></span>
   
        PS C:\> cd node
4. <span data-ttu-id="65d9f-121">Aşağıdaki komutları toocreate adlı yeni bir çözüm hello girin **chatapp** ve adlı çalışan rolü **WorkerRole1**:</span><span class="sxs-lookup"><span data-stu-id="65d9f-121">Enter hello following commands toocreate a new solution named **chatapp** and a worker role named **WorkerRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    <span data-ttu-id="65d9f-122">Yanıt aşağıdaki hello görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="65d9f-122">You will see hello following response:</span></span>
   
    ![Merhaba yeni-azureservice ve ekleme azurenodeworkerrolecmdlets Hello çıktısı](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a><span data-ttu-id="65d9f-124">Merhaba sohbet örnek indirme</span><span class="sxs-lookup"><span data-stu-id="65d9f-124">Download hello Chat Example</span></span>
<span data-ttu-id="65d9f-125">Bu proje için hello sohbet hello örnekten kullanacağız [Socket.IO GitHub deposunu].</span><span class="sxs-lookup"><span data-stu-id="65d9f-125">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="65d9f-126">Aşağıdaki adımları toodownload hello örneğine hello gerçekleştirmek ve daha önce oluşturduğunuz toohello proje ekleyin.</span><span class="sxs-lookup"><span data-stu-id="65d9f-126">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="65d9f-127">Hello kullanarak hello deposu yerel bir kopyasını oluşturma **kopya** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="65d9f-127">Create a local copy of hello repository by using hello **Clone** button.</span></span> <span data-ttu-id="65d9f-128">Merhaba de kullanabilir **ZIP** düğmesini toodownload hello projesi.</span><span class="sxs-lookup"><span data-stu-id="65d9f-128">You may also use hello **ZIP** button toodownload hello project.</span></span>
   
   ![Bir tarayıcı penceresinde hello ZIP indirme simge vurgulanmış ile https://github.com/LearnBoost/Socket.io/Tree/master/examples/Chat, görüntüleme][chat-example-view]
2. <span data-ttu-id="65d9f-130">Hello gelmesini kadar hello yerel deposu hello dizin yapısını gidin **örnekler\\sohbet** dizin.</span><span class="sxs-lookup"><span data-stu-id="65d9f-130">Navigate hello directory structure of hello local repository until you arrive at hello **examples\\chat** directory.</span></span> <span data-ttu-id="65d9f-131">Bu dizin toothe Hello içeriğini kopyalayın **C:\\düğümü\\chatapp\\WorkerRole1** daha önce oluşturduğunuz dizin.</span><span class="sxs-lookup"><span data-stu-id="65d9f-131">Copy hello contents of this directory toothe **C:\\node\\chatapp\\WorkerRole1** directory created earlier.</span></span>
   
   ![Merhaba örnekler Hello içeriğini görüntüleme explorer\\hello arşivinden ayıklanan sohbet dizini][chat-contents]
   
   <span data-ttu-id="65d9f-133">Merhaba vurgulanan hello ekran görüntüsü yukarıdaki hello kopyalanan hello dosya öğeleridir **örnekler\\sohbet** dizini</span><span class="sxs-lookup"><span data-stu-id="65d9f-133">hello highlighted items in hello screenshot above are hello files copied from hello **examples\\chat** directory</span></span>
3. <span data-ttu-id="65d9f-134">Merhaba, **C:\\düğümü\\chatapp\\WorkerRole1** dizin, delete hello **server.js** dosya ve hello yeniden adlandırma **app.js**çok dosya**server.js**.</span><span class="sxs-lookup"><span data-stu-id="65d9f-134">In hello **C:\\node\\chatapp\\WorkerRole1** directory, delete hello **server.js** file, and then rename hello **app.js** file too**server.js**.</span></span> <span data-ttu-id="65d9f-135">Bu hello varsayılan kaldırır **server.js** hello tarafından daha önce oluşturduğunuz dosya **Ekle AzureNodeWorkerRole** cmdlet'i ve Merhaba uygulaması ile dosya değiştirir hello sohbet örnek.</span><span class="sxs-lookup"><span data-stu-id="65d9f-135">This removes hello default **server.js** file created previously by hello **Add-AzureNodeWorkerRole** cmdlet and replaces it with hello application file from hello chat example.</span></span>

### <a name="modify-serverjs-and-install-modules"></a><span data-ttu-id="65d9f-136">Server.js değiştirmek ve modülleri yükleme</span><span class="sxs-lookup"><span data-stu-id="65d9f-136">Modify Server.js and Install Modules</span></span>
<span data-ttu-id="65d9f-137">Sınama hello uygulamada önce hello Azure öykünücüsü, biz bazı küçük değişiklikler yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="65d9f-137">Before testing hello application in hello Azure emulator, we must make some minor modifications.</span></span> <span data-ttu-id="65d9f-138">Aşağıdaki adımları toothe server.js dosyasına hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="65d9f-138">Perform hello following steps toothe server.js file:</span></span>

1. <span data-ttu-id="65d9f-139">Açık hello **server.js** Visual Studio veya herhangi bir metin düzenleyicisi dosyası.</span><span class="sxs-lookup"><span data-stu-id="65d9f-139">Open hello **server.js** file in Visual Studio or any text editor.</span></span>
2. <span data-ttu-id="65d9f-140">Hello bulur **modülü bağımlılıkları** bölümünde hello server.js başında ve hello satırını içeren değiştirme **SIO require('.. = //.. lib//Socket.io')** çok**SIO require('socket.io') =** aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="65d9f-140">Find hello **Module dependencies** section at hello beginning of server.js and change hello line containing **sio = require('..//..//lib//socket.io')** too**sio = require('socket.io')** as shown below:</span></span>
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. <span data-ttu-id="65d9f-141">Merhaba doğru bağlantı noktası üzerinde dinleyen tooensure hello uygulama, Not Defteri veya tercih ettiğiniz Düzenleyicisi server.js açın ve ardından değiştirerek aşağıdaki satırı değiştirin **3000** ile **process.env.port** gösterildiği gibi Aşağıda:</span><span class="sxs-lookup"><span data-stu-id="65d9f-141">tooensure hello application listens on hello correct port, open server.js in Notepad or your favorite editor, and then change the following line by replacing **3000** with **process.env.port** as shown below:</span></span>
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

<span data-ttu-id="65d9f-142">Merhaba değişiklikleri çok kaydetme sonra**server.js**, gerekli modüllerini yüklemek için aşağıdaki adımları hello kullanın ve Azure öykünücüsünde hello uygulamayı test etme:</span><span class="sxs-lookup"><span data-stu-id="65d9f-142">After saving hello changes too**server.js**, use hello following steps to install required modules, and then test hello application in the Azure emulator:</span></span>

1. <span data-ttu-id="65d9f-143">Kullanarak **Azure PowerShell**, dizinleri toohello değiştirme **C:\\düğümü\\chatapp\\WorkerRole1** komutu tooinstall hello aşağıdaki dizin ve kullanım hello Bu uygulama tarafından istenen modüller:</span><span class="sxs-lookup"><span data-stu-id="65d9f-143">Using **Azure PowerShell**, change directories toohello **C:\\node\\chatapp\\WorkerRole1** directory and use hello following command tooinstall hello modules required by this application:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   <span data-ttu-id="65d9f-144">Bu hello package.json dosyasında listelenen hello modüllerini yükler.</span><span class="sxs-lookup"><span data-stu-id="65d9f-144">This will install hello modules listed in hello package.json file.</span></span> <span data-ttu-id="65d9f-145">Merhaba komutu tamamlandığında, çıkış benzer toothe aşağıdaki görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="65d9f-145">After hello command completes, you should see output similar toothe following:</span></span>
   
   ![Merhaba npm Hello çıktısını yükleme komutu][The-output-of-the-npm-install-command]
2. <span data-ttu-id="65d9f-147">Bu örnekte, ilk olarak hello Socket.IO GitHub deposunu bir parçası olan ve doğrudan hello Socket.IO kitaplığı göreli yolu tarafından başvurulan olduğundan, biz komutu aşağıdaki hello vererek yüklemeniz gerekir böylece Socket.IO hello package.json dosyasında başvurulmadı:</span><span class="sxs-lookup"><span data-stu-id="65d9f-147">Since this example was originally a part of hello Socket.IO GitHub repository, and directly referenced hello Socket.IO library by relative path, Socket.IO was not referenced in hello package.json file, so we must install it by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a><span data-ttu-id="65d9f-148">Test etme ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="65d9f-148">Test and Deploy</span></span>
1. <span data-ttu-id="65d9f-149">Merhaba öykünücüsü komutu aşağıdaki hello vererek başlatın:</span><span class="sxs-lookup"><span data-stu-id="65d9f-149">Launch hello emulator by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > <span data-ttu-id="65d9f-150">Öykünücü, örneğin başlatma sorunlar karşılaşırsanız.: Başlangıç AzureEmulator: beklenmeyen bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="65d9f-150">If you encounter issues with launching emulator, eg.: Start-AzureEmulator : An unexpected failure occurred.</span></span>  <span data-ttu-id="65d9f-151">Ayrıntılar: Karşılaştı hello Faulted durumunda olduğundan System.ServiceModel.Channels.ServiceChannel, bir beklenmeyen bir hata hello iletişim nesnesi iletişimi için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="65d9f-151">Details: Encountered an unexpected error hello communication object,  System.ServiceModel.Channels.ServiceChannel, cannot be used for communication because it is in hello Faulted state.</span></span>
   
      <span data-ttu-id="65d9f-152">AzureAuthoringTools v 2.7.1 ve AzureComputeEmulator v 2.7 yeniden - o eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="65d9f-152">reinstall AzureAuthoringTools v 2.7.1 and AzureComputeEmulator v 2.7 - make sure that version matches.</span></span>
   >
   >


2. <span data-ttu-id="65d9f-153">Bir tarayıcı açın ve çok gidin**http://127.0.0.1**.</span><span class="sxs-lookup"><span data-stu-id="65d9f-153">Open a browser and navigate too**http://127.0.0.1**.</span></span>
3. <span data-ttu-id="65d9f-154">Merhaba tarayıcı penceresi açıldığında, takma ad girin ve ardından ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="65d9f-154">When hello browser window opens, enter a nickname and then hit enter.</span></span>
   <span data-ttu-id="65d9f-155">Bu, toopost iletileri belirli bir takma olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="65d9f-155">This will allow you toopost messages as a specific nickname.</span></span> <span data-ttu-id="65d9f-156">tootest çok kullanıcı işlevselliği, aynı URL'yi kullanarak ek tarayıcı pencerelerini açın ve farklı takma adlar girin.</span><span class="sxs-lookup"><span data-stu-id="65d9f-156">tootest multi-user functionality, open additional browser windows using the same URL and enter different nicknames.</span></span>
   
   ![İki tarayıcı pencerelerini Kullanıcı1 ve kullanıcı2 sohbet iletileri görüntüleme](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. <span data-ttu-id="65d9f-158">Sınama hello uygulamadan sonra aşağıdaki komutu gönderdikten hello öykünücüsü durdurun:</span><span class="sxs-lookup"><span data-stu-id="65d9f-158">After testing hello application, stop hello emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. <span data-ttu-id="65d9f-159">toodeploy hello uygulama tooAzure, kullanım **Publish-AzureServiceProject** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="65d9f-159">toodeploy hello application tooAzure, use the **Publish-AzureServiceProject** cmdlet.</span></span> <span data-ttu-id="65d9f-160">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="65d9f-160">For example:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > <span data-ttu-id="65d9f-161">Emin toouse benzersiz bir ad olmalıdır, aksi takdirde hello yayımlama işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="65d9f-161">Be sure toouse a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="65d9f-162">Merhaba dağıtım tamamlandıktan sonra hello tarayıcısı açın ve dağıtılmış toohello hizmet gidin.</span><span class="sxs-lookup"><span data-stu-id="65d9f-162">After hello deployment has completed, hello browser will open and navigate toohello deployed service.</span></span>
   > 
   > <span data-ttu-id="65d9f-163">Abonelik adı içeri hello yok Bu hello sağlanan belirten bir hata alırsanız, yayımlama profili, indirin ve tooAzure dağıtmadan önce aboneliğinizin hello yayımlama profilini içeri aktarma.</span><span class="sxs-lookup"><span data-stu-id="65d9f-163">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="65d9f-164">Merhaba bkz **hello uygulama tooAzure dağıtma** bölümünü [derleme ve bir Node.js uygulaması tooan Azure bulut hizmeti dağıtma](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="65d9f-164">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 
   
   ![Azure üzerinde barındırılan hello hizmet gösteren bir tarayıcı penceresi][completed-app]
   
   > [!NOTE]
   > <span data-ttu-id="65d9f-166">Abonelik adı içeri hello yok Bu hello sağlanan belirten bir hata alırsanız, yayımlama profili, indirin ve tooAzure dağıtmadan önce aboneliğinizin hello yayımlama profilini içeri aktarma.</span><span class="sxs-lookup"><span data-stu-id="65d9f-166">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="65d9f-167">Merhaba bkz **hello uygulama tooAzure dağıtma** bölümünü [derleme ve bir Node.js uygulaması tooan Azure bulut hizmeti dağıtma](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="65d9f-167">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 

<span data-ttu-id="65d9f-168">Uygulamanız artık Azure üzerinde çalışan ve Sohbet iletilerini Socket.IO kullanarak farklı istemciler arasında geçiş.</span><span class="sxs-lookup"><span data-stu-id="65d9f-168">Your application is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

> [!NOTE]
> <span data-ttu-id="65d9f-169">Kolaylık olması için bu kullanıcıları bağlı toohello arasında sınırlı toochatting örnektir aynı örneği.</span><span class="sxs-lookup"><span data-stu-id="65d9f-169">For simplicity, this sample is limited toochatting between users connected toohello same instance.</span></span> <span data-ttu-id="65d9f-170">Bu iki çalışan rolü örnekleri hello bulut hizmeti oluşturur, kullanıcılar yalnızca mümkün olacaktır başkalarıyla toochat bağlı toohello aynı çalışan rolü örneği.</span><span class="sxs-lookup"><span data-stu-id="65d9f-170">This means that if hello cloud service creates two worker role instances, users will only be able toochat with others connected toohello same worker role instance.</span></span> <span data-ttu-id="65d9f-171">tooscale hello uygulama toowork birden fazla rol örneği ile Service Bus tooshare hello Socket.IO deposu durumu gibi bir teknoloji örneklerinde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65d9f-171">tooscale hello application toowork with multiple role instances, you could use a technology like Service Bus tooshare hello Socket.IO store state across instances.</span></span> <span data-ttu-id="65d9f-172">Merhaba hello Service Bus kuyrukları ve konularından kullanım örnekleri örnekler için bkz [Node.js GitHub deposunu için Azure SDK](https://github.com/WindowsAzure/azure-sdk-for-node).</span><span class="sxs-lookup"><span data-stu-id="65d9f-172">For examples, see hello Service Bus Queues and Topics usage samples in hello [Azure SDK for Node.js GitHub repository](https://github.com/WindowsAzure/azure-sdk-for-node).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="65d9f-173">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="65d9f-173">Next steps</span></span>
<span data-ttu-id="65d9f-174">Bu öğreticide nasıl toocreate bir temel sohbet uygulaması bir Azure bulut hizmetinde barındırılan öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="65d9f-174">In this tutorial you learned how toocreate a basic chat application hosted in an Azure Cloud Service.</span></span> <span data-ttu-id="65d9f-175">toolearn nasıl toohost bu uygulamayı bir Azure Web sitesinde bkz [bir Azure Web sitesinde Socket.IO ile bir Node.js sohbet uygulaması derleme][chatwebsite].</span><span class="sxs-lookup"><span data-stu-id="65d9f-175">toolearn how toohost this application in an Azure Website, see [Build a Node.js Chat Application with Socket.IO on an Azure Web Site][chatwebsite].</span></span>

<span data-ttu-id="65d9f-176">Daha fazla bilgi için hello Ayrıca bkz. [Node.js Geliştirici Merkezi](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="65d9f-176">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Socket.IO GitHub deposunu]: https://github.com/LearnBoost/socket.io/tree/0.9.14
[Azure Considerations]: #windowsazureconsiderations
[Hosting hello Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


