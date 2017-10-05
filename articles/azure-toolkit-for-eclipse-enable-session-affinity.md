---
title: "Eclipse için Azure Araç Seti kullanarak oturum benzeşimi etkinleştir"
description: "Eclipse için Azure Araç Seti kullanarak oturum benzeşimi etkinleştirme hakkında bilgi edinin."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: ab8623d6f9751ed6d71d9a5b1c0d5e939c442862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-session-affinity"></a><span data-ttu-id="f906a-103">Oturum benzeşimi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f906a-103">Enable Session Affinity</span></span>
<span data-ttu-id="f906a-104">Eclipse için Azure araç içinde HTTP oturum benzeşimi ya da "Yapışkan oturumlarına", rollerinizi etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f906a-104">Within the Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span></span> <span data-ttu-id="f906a-105">Aşağıdaki resimde gösterildiği **Yük Dengeleme** oturum benzeşimi özelliğini etkinleştirmek için kullanılan özellikleri iletişim kutusu:</span><span class="sxs-lookup"><span data-stu-id="f906a-105">The following image shows the **Load Balancing** properties dialog used to enable the session affinity feature:</span></span>

![][ic719492]

## <a name="to-enable-session-affinity-for-your-role"></a><span data-ttu-id="f906a-106">Rolünüz için oturum benzeşimi etkinleştirmek için</span><span class="sxs-lookup"><span data-stu-id="f906a-106">To enable session affinity for your role</span></span>
1. <span data-ttu-id="f906a-107">Eclipse'nın Proje Gezgini rolüne sağ tıklayın, **Azure**ve ardından **Yük Dengeleme**.</span><span class="sxs-lookup"><span data-stu-id="f906a-107">Right-click the role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span></span>

2. <span data-ttu-id="f906a-108">İçinde **WorkerRole1 Yük Dengeleme özelliklerini** iletişim:</span><span class="sxs-lookup"><span data-stu-id="f906a-108">In the **Properties for WorkerRole1 Load Balancing** dialog:</span></span>

   <span data-ttu-id="f906a-109">a.</span><span class="sxs-lookup"><span data-stu-id="f906a-109">a.</span></span> <span data-ttu-id="f906a-110">Denetleme **bu rol için HTTP etkinleştirme oturum benzeşimi (Yapışkan oturumları).**</span><span class="sxs-lookup"><span data-stu-id="f906a-110">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span></span>

   <span data-ttu-id="f906a-111">b.</span><span class="sxs-lookup"><span data-stu-id="f906a-111">b.</span></span> <span data-ttu-id="f906a-112">İçin **giriş kullanmak için uç nokta**, örneğin kullanmak için bir giriş uç noktası seçin **http (ortak: 80, özel: 8080)**.</span><span class="sxs-lookup"><span data-stu-id="f906a-112">For **Input endpoint to use**, select an input endpoint to use, for example, **http (public:80, private:8080)**.</span></span> <span data-ttu-id="f906a-113">Uygulamanız bu uç noktası, HTTP uç noktası olarak kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f906a-113">Your application must use this endpoint as its HTTP endpoint.</span></span> <span data-ttu-id="f906a-114">Birden çok uç nokta rolünüz için etkinleştirebilirsiniz, ancak Yapışkan oturumları desteklemek için bunlardan yalnızca birini seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f906a-114">You can enable multiple endpoints for your role, but you can select only one of them to support sticky sessions.</span></span>

   <span data-ttu-id="f906a-115">c.</span><span class="sxs-lookup"><span data-stu-id="f906a-115">c.</span></span> <span data-ttu-id="f906a-116">Uygulamanızı yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f906a-116">Rebuild your application.</span></span>

<span data-ttu-id="f906a-117">Birden fazla rol örneği varsa, etkinleştirildikten sonra belirli bir istemciden gelen HTTP istekleri aynı rol örneği tarafından işlenen devam eder.</span><span class="sxs-lookup"><span data-stu-id="f906a-117">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by the same role instance.</span></span>

<span data-ttu-id="f906a-118">Eclipse Araç Seti Bu uygulama isteği yönlendirme (ARR) her rolü örneklerinizi adlı özel bir IIS Modülü yükleyerek sağlar.</span><span class="sxs-lookup"><span data-stu-id="f906a-118">The Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span></span> <span data-ttu-id="f906a-119">ARR, HTTP isteklerini uygun rol örneği yeniden yönlendirmeler.</span><span class="sxs-lookup"><span data-stu-id="f906a-119">ARR reroutes HTTP requests to the appropriate role instance.</span></span> <span data-ttu-id="f906a-120">Gelen HTTP trafiği için ARR yazılım ilk yönlendirilmesi Araç Seti seçili uç noktası otomatik olarak yeniden yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="f906a-120">The toolkit automatically reconfigures the selected endpoint so that the incoming HTTP traffic is first routed to the ARR software.</span></span> <span data-ttu-id="f906a-121">Araç Seti ayrıca yeni bir iç uç noktası oluşturan Java sunucunuz dinlemek üzere yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="f906a-121">The toolkit also creates a new internal endpoint that your Java server is configured to listen to.</span></span> <span data-ttu-id="f906a-122">Uygun rol örneği HTTP trafiği yeniden yönlendirebilir için ARR tarafından kullanılan uç noktayla olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="f906a-122">That is the endpoint used by ARR to reroute the HTTP traffic to the appropriate role instance.</span></span> <span data-ttu-id="f906a-123">Bu şekilde, her rol örneği çok örnekli dağıtımınızdaki Yapışkan oturumları etkinleştirme için ters proxy tüm diğer örnekleri, işlevi görür.</span><span class="sxs-lookup"><span data-stu-id="f906a-123">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all the other instances, enabling sticky sessions.</span></span>

## <a name="notes-about-session-affinity"></a><span data-ttu-id="f906a-124">Oturum benzeşimi ile ilgili notlar</span><span class="sxs-lookup"><span data-stu-id="f906a-124">Notes about session affinity</span></span>
* <span data-ttu-id="f906a-125">Oturum benzeşimi işlem öykünücüsü çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="f906a-125">Session affinity does not work in the compute emulator.</span></span> <span data-ttu-id="f906a-126">Ayarları ile derleme işleminin engellemeden işlem öykünücüsü uygulanabilir veya öykünücüsü yürütme işlem, ancak özellik işlem öykünücüsü içinde çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="f906a-126">The settings can be applied in the compute emulator without interfering with your build process or compute emulator execution, but the feature itself does not function within the compute emulator.</span></span>

* <span data-ttu-id="f906a-127">Oturum benzeşimi etkinleştirme Azure, dağıtımınızdaki tarafından ek yazılım indirilir ve hizmetinizi Azure bulutunda başlatıldığında rolü örneklerinizi yüklü olarak kapladığı disk alanı miktarında artış neden olur.</span><span class="sxs-lookup"><span data-stu-id="f906a-127">Enabling session affinity will result in an increase in the amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in the Azure cloud.</span></span>

* <span data-ttu-id="f906a-128">Her rol başlatmak için daha uzun sürer.</span><span class="sxs-lookup"><span data-stu-id="f906a-128">The time to initialize each role will take longer.</span></span>

* <span data-ttu-id="f906a-129">Yukarıda belirtildiği gibi trafik rerouter çalışması için dahili uç noktayı, eklenir.</span><span class="sxs-lookup"><span data-stu-id="f906a-129">An internal endpoint, to function as a traffic rerouter as mentioned above, will be added.</span></span>


## <a name="see-also"></a><span data-ttu-id="f906a-130">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f906a-130">See Also</span></span>
<span data-ttu-id="f906a-131">[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f906a-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="f906a-132">[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f906a-132">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="f906a-133">[Eclipse için Azure araç setini yükleme][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f906a-133">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="f906a-134">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="f906a-134">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How to Maintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
