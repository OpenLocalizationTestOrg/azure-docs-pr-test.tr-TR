---
title: "Eclipse için Azure Araç Seti hello aaaEnable oturum benzeşimi kullanma"
description: "Nasıl tooenable oturum benzeşimi kullanılarak izin ver hello Eclipse için Azure Araç Seti öğrenin."
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
ms.openlocfilehash: 523e728c58bda95e7af4b242e831694eb6d75cb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-session-affinity"></a><span data-ttu-id="10817-103">Oturum benzeşimi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="10817-103">Enable Session Affinity</span></span>
<span data-ttu-id="10817-104">Eclipse için Azure Araç Seti Hello içinde HTTP oturum benzeşimi ya da "Yapışkan oturumlarına", rollerinizi etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10817-104">Within hello Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span></span> <span data-ttu-id="10817-105">Merhaba aşağıdaki resimde gösterilmiştir hello **Yük Dengeleme** özellikler kullanılan iletişim tooenable hello oturum benzeşimi özelliğini:</span><span class="sxs-lookup"><span data-stu-id="10817-105">hello following image shows hello **Load Balancing** properties dialog used tooenable hello session affinity feature:</span></span>

![][ic719492]

## <a name="tooenable-session-affinity-for-your-role"></a><span data-ttu-id="10817-106">tooenable oturum benzeşimi rolünüz için</span><span class="sxs-lookup"><span data-stu-id="10817-106">tooenable session affinity for your role</span></span>
1. <span data-ttu-id="10817-107">Merhaba rol Eclipse'nın Proje Gezgini'nde sağ tıklayın, **Azure**ve ardından **Yük Dengeleme**.</span><span class="sxs-lookup"><span data-stu-id="10817-107">Right-click hello role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span></span>

2. <span data-ttu-id="10817-108">Merhaba, **WorkerRole1 Yük Dengeleme özelliklerini** iletişim:</span><span class="sxs-lookup"><span data-stu-id="10817-108">In hello **Properties for WorkerRole1 Load Balancing** dialog:</span></span>

   <span data-ttu-id="10817-109">a.</span><span class="sxs-lookup"><span data-stu-id="10817-109">a.</span></span> <span data-ttu-id="10817-110">Denetleme **bu rol için HTTP etkinleştirme oturum benzeşimi (Yapışkan oturumları).**</span><span class="sxs-lookup"><span data-stu-id="10817-110">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span></span>

   <span data-ttu-id="10817-111">b.</span><span class="sxs-lookup"><span data-stu-id="10817-111">b.</span></span> <span data-ttu-id="10817-112">İçin **giriş uç noktası toouse**, örneğin, bir giriş uç noktası toouse seçin **http (ortak: 80, özel: 8080)**.</span><span class="sxs-lookup"><span data-stu-id="10817-112">For **Input endpoint toouse**, select an input endpoint toouse, for example, **http (public:80, private:8080)**.</span></span> <span data-ttu-id="10817-113">Uygulamanız bu uç noktası, HTTP uç noktası olarak kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="10817-113">Your application must use this endpoint as its HTTP endpoint.</span></span> <span data-ttu-id="10817-114">Birden çok uç nokta rolünüz için etkinleştirebilirsiniz, ancak yalnızca bunlardan birinin toosupport seçebilirsiniz Yapışkan oturumları.</span><span class="sxs-lookup"><span data-stu-id="10817-114">You can enable multiple endpoints for your role, but you can select only one of them toosupport sticky sessions.</span></span>

   <span data-ttu-id="10817-115">c.</span><span class="sxs-lookup"><span data-stu-id="10817-115">c.</span></span> <span data-ttu-id="10817-116">Uygulamanızı yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="10817-116">Rebuild your application.</span></span>

<span data-ttu-id="10817-117">Birden fazla rol örneği varsa, etkinleştirildikten sonra belirli bir istemciden gelen HTTP istekleri aynı hello tarafından işlenen devam edecek rol örneği.</span><span class="sxs-lookup"><span data-stu-id="10817-117">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by hello same role instance.</span></span>

<span data-ttu-id="10817-118">Merhaba Eclipse Araç Seti Bu uygulama isteği yönlendirme (ARR) her rolü örneklerinizi adlı özel bir IIS Modülü yükleyerek sağlar.</span><span class="sxs-lookup"><span data-stu-id="10817-118">hello Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span></span> <span data-ttu-id="10817-119">ARR, HTTP isteklerini toohello uygun rol örneği yeniden yönlendirmeler.</span><span class="sxs-lookup"><span data-stu-id="10817-119">ARR reroutes HTTP requests toohello appropriate role instance.</span></span> <span data-ttu-id="10817-120">Böylece Hello gelen HTTP trafiği ilk yönlendirilmiş toohello ARR yazılım hello Araç Seti seçili hello uç noktası otomatik olarak yeniden yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="10817-120">hello toolkit automatically reconfigures hello selected endpoint so that hello incoming HTTP traffic is first routed toohello ARR software.</span></span> <span data-ttu-id="10817-121">Merhaba Araç Seti ayrıca Java sunucunuz için yapılandırılmış toolisten olan yeni bir iç uç noktası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="10817-121">hello toolkit also creates a new internal endpoint that your Java server is configured toolisten to.</span></span> <span data-ttu-id="10817-122">ARR tooreroute hello HTTP trafiği toohello uygun rol örneği tarafından kullanılan hello endpoint olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="10817-122">That is hello endpoint used by ARR tooreroute hello HTTP traffic toohello appropriate role instance.</span></span> <span data-ttu-id="10817-123">Tümü için ters proxy hello gibi diğer örnekleri Yapışkan oturumları etkinleştirme bu şekilde, her rol örneği çok örnekli dağıtımınızdaki işlevi görür.</span><span class="sxs-lookup"><span data-stu-id="10817-123">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all hello other instances, enabling sticky sessions.</span></span>

## <a name="notes-about-session-affinity"></a><span data-ttu-id="10817-124">Oturum benzeşimi ile ilgili notlar</span><span class="sxs-lookup"><span data-stu-id="10817-124">Notes about session affinity</span></span>
* <span data-ttu-id="10817-125">Oturum benzeşimi hello işlem öykünücüsü çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="10817-125">Session affinity does not work in hello compute emulator.</span></span> <span data-ttu-id="10817-126">Hello ayarları hello işlem öykünücüsü yapı işleminizin engellemeden uygulanabilir veya öykünücü yürütme işlem, ancak hello özelliğe hello işlem öykünücüsü içinde çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="10817-126">hello settings can be applied in hello compute emulator without interfering with your build process or compute emulator execution, but hello feature itself does not function within hello compute emulator.</span></span>

* <span data-ttu-id="10817-127">Oturum benzeşimi etkinleştirme hello Azure, dağıtımınızdaki tarafından ek yazılım indirilir ve hello Azure bulut hizmetinize başlatıldığında rolü örneklerinizi yüklü olarak kapladığı disk alanı miktarını artış neden olur.</span><span class="sxs-lookup"><span data-stu-id="10817-127">Enabling session affinity will result in an increase in hello amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in hello Azure cloud.</span></span>

* <span data-ttu-id="10817-128">Başlangıç saati tooinitialize her rol daha uzun sürer.</span><span class="sxs-lookup"><span data-stu-id="10817-128">hello time tooinitialize each role will take longer.</span></span>

* <span data-ttu-id="10817-129">İç uç nokta, toofunction, yukarıda belirtildiği gibi bir trafik rerouter olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="10817-129">An internal endpoint, toofunction as a traffic rerouter as mentioned above, will be added.</span></span>


## <a name="see-also"></a><span data-ttu-id="10817-130">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="10817-130">See Also</span></span>
<span data-ttu-id="10817-131">[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="10817-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="10817-132">[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="10817-132">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="10817-133">[Yükleme hello Eclipse için Azure Araç Seti][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="10817-133">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="10817-134">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="10817-134">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How tooMaintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
