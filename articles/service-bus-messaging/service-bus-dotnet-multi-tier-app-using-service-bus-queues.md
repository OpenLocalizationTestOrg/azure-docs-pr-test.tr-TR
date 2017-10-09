---
title: "Azure Service Bus kullanan aaa.NET çok katmanlı uygulaması | Microsoft Docs"
description: "Yardımcı olan bir .NET Öğreticisi Service Bus kuyrukları toocommunicate katmanları arasında kullanan azure'da çok katmanlı bir uygulama geliştirin."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 485910ff1d3b8b0a709ee14ede32e57cf873829a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a><span data-ttu-id="85402-103">Azure Service Bus kuyruklarını kullanan çok katmanlı .NET uygulaması</span><span class="sxs-lookup"><span data-stu-id="85402-103">.NET multi-tier application using Azure Service Bus queues</span></span>
## <a name="introduction"></a><span data-ttu-id="85402-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="85402-104">Introduction</span></span>
<span data-ttu-id="85402-105">Microsoft Azure, Visual Studio kullanarak kolaydır ve hello .NET için Azure SDK'sı boş için geliştirme.</span><span class="sxs-lookup"><span data-stu-id="85402-105">Developing for Microsoft Azure is easy using Visual Studio and hello free Azure SDK for .NET.</span></span> <span data-ttu-id="85402-106">Bu öğreticide, yerel ortamınızda çalışan birden çok Azure kaynağı kullanan bir uygulama hello adımları toocreate açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="85402-106">This tutorial walks you through hello steps toocreate an application that uses multiple Azure resources running in your local environment.</span></span>

<span data-ttu-id="85402-107">Merhaba şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="85402-107">You will learn hello following:</span></span>

* <span data-ttu-id="85402-108">Nasıl tooenable tek bir Azure geliştirme bilgisayarınıza indirin ve yükleyin.</span><span class="sxs-lookup"><span data-stu-id="85402-108">How tooenable your computer for Azure development with a single download and install.</span></span>
* <span data-ttu-id="85402-109">Nasıl toouse Visual Studio toodevelop Azure için.</span><span class="sxs-lookup"><span data-stu-id="85402-109">How toouse Visual Studio toodevelop for Azure.</span></span>
* <span data-ttu-id="85402-110">Nasıl toocreate web ve çalışan rollerini kullanarak azure'da çok katmanlı bir uygulama.</span><span class="sxs-lookup"><span data-stu-id="85402-110">How toocreate a multi-tier application in Azure using web and worker roles.</span></span>
* <span data-ttu-id="85402-111">Service Bus kuyruklarını kullanan toocommunicate arasında katmanlarını nasıl.</span><span class="sxs-lookup"><span data-stu-id="85402-111">How toocommunicate between tiers using Service Bus queues.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

<span data-ttu-id="85402-112">Bu öğreticide oluşturun ve bir Azure bulut hizmetinde hello çok katmanlı uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="85402-112">In this tutorial you'll build and run hello multi-tier application in an Azure cloud service.</span></span> <span data-ttu-id="85402-113">Merhaba ön uç bir ASP.NET MVC web rolü ve hello arka uç Service Bus kuyruğu kullanan bir alt-rolü.</span><span class="sxs-lookup"><span data-stu-id="85402-113">hello front end is an ASP.NET MVC web role and hello back end is a worker-role that uses a Service Bus queue.</span></span> <span data-ttu-id="85402-114">Oluşturabileceğiniz hello hello ön uç ile dağıtılan tooan Azure Web sitesi bulut hizmeti yerine bir web projesi, aynı çok katmanlı uygulama.</span><span class="sxs-lookup"><span data-stu-id="85402-114">You can create hello same multi-tier application with hello front end as a web project, that is deployed tooan Azure website instead of a cloud service.</span></span> <span data-ttu-id="85402-115">Out hello de deneyebilirsiniz [şirket içi/bulut karma .NET uygulama](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="85402-115">You can also try out hello [.NET on-premises/cloud hybrid application](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span></span>

<span data-ttu-id="85402-116">Merhaba aşağıdaki ekran görüntüsünde tamamlanan hello uygulamayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="85402-116">hello following screen shot shows hello completed application.</span></span>

![][0]

## <a name="scenario-overview-inter-role-communication"></a><span data-ttu-id="85402-117">Senaryoya genel bakış: roller arası iletişim</span><span class="sxs-lookup"><span data-stu-id="85402-117">Scenario overview: inter-role communication</span></span>
<span data-ttu-id="85402-118">toosubmit, hello web rolünde çalışan hello ön uç kullanıcı Arabirimi bileşeninin işlemek için bir sıra hello çalışan rolünde çalışmakta hello orta katman mantığı ile etkileşim kurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="85402-118">toosubmit an order for processing, hello front-end UI component, running in hello web role, must interact with hello middle tier logic running in hello worker role.</span></span> <span data-ttu-id="85402-119">Bu örnek hello hello katmanlar arasında iletişim için Service Bus Mesajlaşma kullanır.</span><span class="sxs-lookup"><span data-stu-id="85402-119">This example uses Service Bus messaging for hello communication between hello tiers.</span></span>

<span data-ttu-id="85402-120">Hizmet veri yolu kullanarak hello web ve orta katman arasında ileti iki bileşeni birbirinden ayırır.</span><span class="sxs-lookup"><span data-stu-id="85402-120">Using Service Bus messaging between hello web and middle tiers decouples the two components.</span></span> <span data-ttu-id="85402-121">Buna karşılık toodirect (diğer bir deyişle, TCP veya HTTP) Mesajlaşma hello web katmanı bağlanamama toohello orta katman doğrudan; Bunun yerine, iş, birimleri iletileri gibi hizmet güvenilir bir şekilde hello orta katman hazır tooconsume kadar kurtarılmasını ve işlenecekleri Bus hizmetine gönderir.</span><span class="sxs-lookup"><span data-stu-id="85402-121">In contrast toodirect messaging (that is, TCP or HTTP), hello web tier does not connect toohello middle tier directly; instead it pushes units of work, as messages, into Service Bus, which reliably retains them until hello middle tier is ready tooconsume and process them.</span></span>

<span data-ttu-id="85402-122">Hizmet veri yolu sağlayan iki toosupport aracılı Mesajlaşma: sıraları ve konuları.</span><span class="sxs-lookup"><span data-stu-id="85402-122">Service Bus provides two entities toosupport brokered messaging: queues and topics.</span></span> <span data-ttu-id="85402-123">Kuyruklar, her ileti toohello sıra tek bir alıcı tarafından tüketilen gönderilir.</span><span class="sxs-lookup"><span data-stu-id="85402-123">With queues, each message sent toohello queue is consumed by a single receiver.</span></span> <span data-ttu-id="85402-124">Konuları kullanılabilir tooa abonelik hello konuya kaydedilen her yayımlanan ileti yapıldığı hello Yayınla/Abone ol düzenini destekler.</span><span class="sxs-lookup"><span data-stu-id="85402-124">Topics support hello publish/subscribe pattern in which each published message is made available tooa subscription registered with hello topic.</span></span> <span data-ttu-id="85402-125">Her abonelik mantıksal olarak kendi ileti kuyruğunu korur.</span><span class="sxs-lookup"><span data-stu-id="85402-125">Each subscription logically maintains its own queue of messages.</span></span> <span data-ttu-id="85402-126">Abonelikleri hello filtreyle eşleşen gönderilen ileti hello abonelik sıra toothose için hello kümesini sınırlayan filtre kuralları ile de yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="85402-126">Subscriptions can also be configured with filter rules that restrict hello set of messages passed to hello subscription queue toothose that match hello filter.</span></span> <span data-ttu-id="85402-127">Merhaba aşağıdaki örnekte Service Bus kuyrukları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85402-127">hello following example uses Service Bus queues.</span></span>

![][1]

<span data-ttu-id="85402-128">Bu iletişim mekanizması, doğrudan mesajlaşma ile karşılaştırıldığında birçok avantaj sunar:</span><span class="sxs-lookup"><span data-stu-id="85402-128">This communication mechanism has several advantages over direct messaging:</span></span>

* <span data-ttu-id="85402-129">**Zamana bağlı ayırma.**</span><span class="sxs-lookup"><span data-stu-id="85402-129">**Temporal decoupling.**</span></span> <span data-ttu-id="85402-130">Merhaba zaman uyumsuz Mesajlaşma düzeni sayesinde üreticilerin ve tüketicilerin hello çevrimiçi olması gerekmez aynı anda.</span><span class="sxs-lookup"><span data-stu-id="85402-130">With hello asynchronous messaging pattern, producers and consumers need not be online at hello same time.</span></span> <span data-ttu-id="85402-131">Merhaba kullanıcı tarafı almaya hazır olana kadar hizmet veri yolu iletileri güvenilir bir şekilde depolar.</span><span class="sxs-lookup"><span data-stu-id="85402-131">Service Bus reliably stores messages until hello consuming party is ready to receive them.</span></span> <span data-ttu-id="85402-132">Bu, ya da gönüllü, örneğin, Bakım veya tooa bileşen çökmesinden dolayı sistemin tamamını etkilemeden bağlantısı kesilmiş hello dağıtılmış uygulama toobe hello bileşenlerinin sağlar.</span><span class="sxs-lookup"><span data-stu-id="85402-132">This enables hello components of hello distributed application toobe disconnected, either voluntarily, for example, for maintenance, or due tooa component crash, without impacting the system as a whole.</span></span> <span data-ttu-id="85402-133">Ayrıca, uygulama hello hello günün belirli zamanlarında yalnızca çevrimiçi toocome gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="85402-133">Furthermore, hello consuming application might only need toocome online during certain times of hello day.</span></span>
* <span data-ttu-id="85402-134">**Yük dengeleme.**</span><span class="sxs-lookup"><span data-stu-id="85402-134">**Load leveling.**</span></span> <span data-ttu-id="85402-135">Her iş birimi için gerekli hello işleme süresi genellikle sabit durumdayken birçok uygulamada, sistem yükü zaman içinde değişir.</span><span class="sxs-lookup"><span data-stu-id="85402-135">In many applications, system load varies over time, while hello processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="85402-136">Aracılığıyla ileti üreticileri ve tüketicileri bir kuyruk, uygulama (Merhaba çalışan) yalnızca gereksinimlerini toobe tüketen bu hello yoğun yük yerine tooaccommodate ortalama yük sağlanması anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="85402-136">Intermediating message producers and consumers with a queue means that hello consuming application (hello worker) only needs toobe provisioned tooaccommodate average load rather than peak load.</span></span> <span data-ttu-id="85402-137">Merhaba hello sıra derinliği büyüdükçe ve hello gelen Yük hacmi değiştikçe sözleşme.</span><span class="sxs-lookup"><span data-stu-id="85402-137">hello depth of hello queue grows and contracts as hello incoming load varies.</span></span> <span data-ttu-id="85402-138">Bu doğrudan hello altyapı gerekli tooservice hello uygulama yük miktarı bakımından paradan tasarruf eder.</span><span class="sxs-lookup"><span data-stu-id="85402-138">This directly saves money in terms of hello amount of infrastructure required tooservice hello application load.</span></span>
* <span data-ttu-id="85402-139">**Yük dengeleme.**</span><span class="sxs-lookup"><span data-stu-id="85402-139">**Load balancing.**</span></span> <span data-ttu-id="85402-140">Yük arttıkça daha fazla çalışan işlemi hello sıradan tooread eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="85402-140">As load increases, more worker processes can be added tooread from hello queue.</span></span> <span data-ttu-id="85402-141">Her ileti tek hello çalışan işlemleri tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="85402-141">Each message is processed by only one of hello worker processes.</span></span> <span data-ttu-id="85402-142">Ayrıca, çalışan makinelerin işleme gücünü bakımından farklılık gösterse bile iletileri kendi maksimum hızında çeker gibi hello çalışan makinelerin optimum kullanımına bu çekme tabanlı yük dengeleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="85402-142">Furthermore, this pull-based load balancing enables optimal use of hello worker machines even if the worker machines differ in terms of processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="85402-143">Bu desen genellikle hello adlandırılır *rakip tüketici* düzeni.</span><span class="sxs-lookup"><span data-stu-id="85402-143">This pattern is often termed hello *competing consumer* pattern.</span></span>
  
  ![][2]

<span data-ttu-id="85402-144">Aşağıdaki bölümlerde hello bu mimariyi uygulayan hello kod ele alınır.</span><span class="sxs-lookup"><span data-stu-id="85402-144">hello following sections discuss hello code that implements this architecture.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="85402-145">Merhaba geliştirme ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="85402-145">Set up hello development environment</span></span>
<span data-ttu-id="85402-146">Azure uygulamalarını geliştirmeye başlamadan önce hello araçları edinin ve geliştirme ortamınızı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="85402-146">Before you can begin developing Azure applications, get hello tools and set up your development environment.</span></span>

1. <span data-ttu-id="85402-147">.NET için SDK hello Hello Azure SDK'sını yüklemek [indirmeler sayfası](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="85402-147">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="85402-148">Merhaba, **.NET** sütun hello sürümünü [Visual Studio](http://www.visualstudio.com) kullanmakta olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="85402-148">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="85402-149">Bu öğretici kullanımda Visual Studio 2015 Hello adımlar, ancak bunlar da Visual Studio 2017 ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="85402-149">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="85402-150">Toorun istenir veya hello yükleyici kaydettiğinizde tıklatın **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="85402-150">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="85402-151">Merhaba, **Web Platformu yükleyicisi**,'ı tıklatın **yüklemek** ve hello yükleme işlemine devam edin.</span><span class="sxs-lookup"><span data-stu-id="85402-151">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="85402-152">Merhaba yüklemesi tamamlandıktan sonra her şeyi olacaktır gerekli toostart toodevelop hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="85402-152">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="85402-153">Merhaba SDK, Visual Studio'da Azure uygulamalarını kolayca geliştirmenize olanak sağlayan araçları içerir.</span><span class="sxs-lookup"><span data-stu-id="85402-153">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="85402-154">Ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="85402-154">Create a namespace</span></span>
<span data-ttu-id="85402-155">Merhaba sonraki adıma toocreate bir hizmet ad alanıdır ve bir paylaşılan erişim imzası (SAS) anahtarı edinin.</span><span class="sxs-lookup"><span data-stu-id="85402-155">hello next step is toocreate a service namespace, and obtain a Shared Access Signature (SAS) key.</span></span> <span data-ttu-id="85402-156">Ad alanı, Service Bus tarafından kullanıma sunulan her uygulama için bir uygulama sınırı sağlar.</span><span class="sxs-lookup"><span data-stu-id="85402-156">A namespace provides an application boundary for each application exposed through Service Bus.</span></span> <span data-ttu-id="85402-157">Bir ad alanı oluşturulduğunda hello sistem tarafından bir SAS anahtarı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="85402-157">A SAS key is generated by hello system when a namespace is created.</span></span> <span data-ttu-id="85402-158">ad alanı ve SAS anahtarı birleşimi Hello Service Bus tooauthenticate erişim tooan uygulamanız için hello kimlik bilgileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="85402-158">hello combination of namespace and SAS key provides hello credentials for Service Bus tooauthenticate access tooan application.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a><span data-ttu-id="85402-159">Web rolü oluşturma</span><span class="sxs-lookup"><span data-stu-id="85402-159">Create a web role</span></span>
<span data-ttu-id="85402-160">Bu bölümde, uygulamanızın ön uç hello oluşturun.</span><span class="sxs-lookup"><span data-stu-id="85402-160">In this section, you build hello front end of your application.</span></span> <span data-ttu-id="85402-161">İlk olarak, uygulamanızın görüntülediği hello sayfaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="85402-161">First, you create hello pages that your application displays.</span></span>
<span data-ttu-id="85402-162">Bundan sonra öğeleri tooa Service Bus kuyruğuna gönderir ve hello kuyruk hakkındaki durum bilgilerini görüntüleyen kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="85402-162">After that, add code that submits items tooa Service Bus queue and displays status information about hello queue.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="85402-163">Başlangıç projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="85402-163">Create hello project</span></span>
1. <span data-ttu-id="85402-164">Yönetici ayrıcalıklarını kullanarak Visual Studio'yu başlatın: sağ hello **Visual Studio** program simgesine ve ardından **yönetici olarak çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="85402-164">Using administrator privileges, start Visual Studio: right-click hello **Visual Studio** program icon, and then click **Run as administrator**.</span></span> <span data-ttu-id="85402-165">Merhaba, bu makalenin sonraki bölümlerinde ele alınan Azure işlem öykünücüsü, Visual Studio'nun yönetici ayrıcalıklarıyla başlatılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="85402-165">hello Azure compute emulator, discussed later in this article, requires that Visual Studio be started with administrator privileges.</span></span>
   
   <span data-ttu-id="85402-166">Visual Studio'da, hello **dosya** menüsünde tıklatın **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="85402-166">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="85402-167">**Yüklü Şablonlar**'da **Visual C#** kısmında **Bulut** seçeneğine ve ardından **Azure Bulut Hizmeti**'ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85402-167">From **Installed Templates**, under **Visual C#**, click **Cloud** and then click **Azure Cloud Service**.</span></span> <span data-ttu-id="85402-168">Ad hello proje **MultiTierApp**.</span><span class="sxs-lookup"><span data-stu-id="85402-168">Name hello project **MultiTierApp**.</span></span> <span data-ttu-id="85402-169">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85402-169">Then click **OK**.</span></span>
   
   ![][9]
3. <span data-ttu-id="85402-170">**.NET Framework 4.5** rollerinden **ASP.NET Web Rolü**'ne çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85402-170">From **.NET Framework 4.5** roles, double-click **ASP.NET Web Role**.</span></span>
   
   ![][10]
4. <span data-ttu-id="85402-171">Üzerine gelerek **WebRole1** altında **Azure bulut hizmeti çözümü**hello kalem simgesine tıklayın ve hello web rolü çok yeniden adlandırma**FrontendWebRole**.</span><span class="sxs-lookup"><span data-stu-id="85402-171">Hover over **WebRole1** under **Azure Cloud Service solution**, click hello pencil icon, and rename hello web role too**FrontendWebRole**.</span></span> <span data-ttu-id="85402-172">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85402-172">Then click **OK**.</span></span> <span data-ttu-id="85402-173">("Frontend" öğesini "FrontEnd" olarak değil de küçük 'e' ile yazdığınızdan emin olun.)</span><span class="sxs-lookup"><span data-stu-id="85402-173">(Make sure you enter "Frontend" with a lower-case 'e,' not "FrontEnd".)</span></span>
   
   ![][11]
5. <span data-ttu-id="85402-174">Merhaba gelen **yeni ASP.NET projesi** iletişim kutusunda hello **bir şablon seçin** tıklatın **MVC**.</span><span class="sxs-lookup"><span data-stu-id="85402-174">From hello **New ASP.NET Project** dialog box, in hello **Select a template** list, click **MVC**.</span></span>
   
   ![][12]
6. <span data-ttu-id="85402-175">Merhaba yine de **yeni ASP.NET projesi** iletişim kutusunda, hello **kimlik doğrulamayı Değiştir** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="85402-175">Still in hello **New ASP.NET Project** dialog box, click hello **Change Authentication** button.</span></span> <span data-ttu-id="85402-176">Merhaba, **kimlik doğrulamayı Değiştir** iletişim kutusu, tıklatın **doğrulaması yok**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="85402-176">In hello **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span> <span data-ttu-id="85402-177">Bu öğreticide kullanıcının oturum açmasını gerektirmeyen bir uygulamayı dağıtıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="85402-177">For this tutorial, you're deploying an app that doesn't need a user login.</span></span>
   
    ![][16]
7. <span data-ttu-id="85402-178">Merhaba edilene **yeni ASP.NET projesi** iletişim kutusu, tıklatın **Tamam** toocreate hello projesi.</span><span class="sxs-lookup"><span data-stu-id="85402-178">Back in hello **New ASP.NET Project** dialog box, click **OK** toocreate hello project.</span></span>
8. <span data-ttu-id="85402-179">İçinde **Çözüm Gezgini**, hello içinde **FrontendWebRole** projesinde **başvuruları**, ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="85402-179">In **Solution Explorer**, in hello **FrontendWebRole** project, right-click **References**, then click **Manage NuGet Packages**.</span></span>
9. <span data-ttu-id="85402-180">Merhaba tıklatın **Gözat** sekmesini ve ardından arama `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="85402-180">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="85402-181">Select hello **WindowsAzure.ServiceBus** paketini, tıklatın **yükleme**ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="85402-181">Select hello **WindowsAzure.ServiceBus** package, click **Install**, and accept hello terms of use.</span></span>
   
   ![][13]
   
   <span data-ttu-id="85402-182">Bu hello gerekli istemci derlemelerine başvuru oluşturulduğunu ve bazı yeni kod dosyaları eklendiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="85402-182">Note that hello required client assemblies are now referenced and some new code files have been added.</span></span>
10. <span data-ttu-id="85402-183">**Çözüm Gezgini**'nde, **Modeller**'e sağ tıklayın ve ardından **Ekle** ile **Sınıf** seçeneklerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85402-183">In **Solution Explorer**, right-click **Models** and click **Add**, then click **Class**.</span></span> <span data-ttu-id="85402-184">Merhaba, **adı** kutusu, tür hello adı **OnlineOrder.cs**.</span><span class="sxs-lookup"><span data-stu-id="85402-184">In hello **Name** box, type hello name **OnlineOrder.cs**.</span></span> <span data-ttu-id="85402-185">Daha sonra **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85402-185">Then click **Add**.</span></span>

### <a name="write-hello-code-for-your-web-role"></a><span data-ttu-id="85402-186">Merhaba web rolünüz için kod yazma</span><span class="sxs-lookup"><span data-stu-id="85402-186">Write hello code for your web role</span></span>
<span data-ttu-id="85402-187">Bu bölümde, uygulamanızın görüntülediği çeşitli sayfalar hello oluşturun.</span><span class="sxs-lookup"><span data-stu-id="85402-187">In this section, you create hello various pages that your application displays.</span></span>

1. <span data-ttu-id="85402-188">Merhaba OnlineOrder.cs dosyasında Visual Studio, var olan ad alanı tanımını koddan hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="85402-188">In hello OnlineOrder.cs file in Visual Studio, replace the existing namespace definition with hello following code:</span></span>
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. <span data-ttu-id="85402-189">**Çözüm Gezgini**'nde **Controllers\HomeController.cs** öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85402-189">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span> <span data-ttu-id="85402-190">Merhaba aşağıdakileri ekleyin **kullanarak** deyimleri hello hello üstündeki dosya, yeni oluşturduğunuz, Service Bus hizmetinin yanı sıra modelin tooinclude hello ad alanları.</span><span class="sxs-lookup"><span data-stu-id="85402-190">Add hello following **using** statements at hello top of hello file tooinclude hello namespaces for the model you just created, as well as Service Bus.</span></span>
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. <span data-ttu-id="85402-191">Ayrıca hello HomeController.cs dosyasında Visual Studio, var olan ad alanı tanımını koddan hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="85402-191">Also in hello HomeController.cs file in Visual Studio, replace the existing namespace definition with hello following code.</span></span> <span data-ttu-id="85402-192">Bu kod öğeleri toohello sırasının hello gönderimi işlenmesine yönelik yöntemler içerir.</span><span class="sxs-lookup"><span data-stu-id="85402-192">This code contains methods for handling hello submission of items toohello queue.</span></span>
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect tooSubmit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for hello submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from hello submission
           // form.
           [HttpPost]
           // Attribute toohelp prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting tooqueue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. <span data-ttu-id="85402-193">Merhaba gelen **yapı** menüsünde tıklatın **yapı çözümü** tootest hello çalışmanızın o ana kadarki doğruluğunu.</span><span class="sxs-lookup"><span data-stu-id="85402-193">From hello **Build** menu, click **Build Solution** tootest hello accuracy of your work so far.</span></span>
5. <span data-ttu-id="85402-194">Şimdi, hello hello görünümünü oluşturmak `Submit()` daha önce oluşturduğunuz yöntemi.</span><span class="sxs-lookup"><span data-stu-id="85402-194">Now, create hello view for hello `Submit()` method you created earlier.</span></span> <span data-ttu-id="85402-195">İçinde Hello sağ `Submit()` yöntemi (Merhaba aşırı yüklemesini `Submit()` parametre almayan) ve ardından **Görünüm Ekle**.</span><span class="sxs-lookup"><span data-stu-id="85402-195">Right-click within hello `Submit()` method (hello overload of `Submit()` that takes no parameters), and then choose **Add View**.</span></span>
   
   ![][14]
6. <span data-ttu-id="85402-196">Merhaba görünümü oluşturmak için bir iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="85402-196">A dialog box appears for creating hello view.</span></span> <span data-ttu-id="85402-197">Merhaba, **şablonu** listesinde, seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="85402-197">In hello **Template** list, choose **Create**.</span></span> <span data-ttu-id="85402-198">Merhaba, **Model sınıfı** hello tıklatın **OnlineOrder** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="85402-198">In hello **Model class** list, click hello **OnlineOrder** class.</span></span>
   
   ![][15]
7. <span data-ttu-id="85402-199">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85402-199">Click **Add**.</span></span>
8. <span data-ttu-id="85402-200">Şimdi, uygulamanızın görüntülenen hello adını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="85402-200">Now, change hello displayed name of your application.</span></span> <span data-ttu-id="85402-201">İçinde **Çözüm Gezgini**, çift **görünümler/paylaşılan\\_Layout.cshtml** tooopen dosya hello Visual Studio düzenleyicisinde içinde.</span><span class="sxs-lookup"><span data-stu-id="85402-201">In **Solution Explorer**, double-click the **Views\Shared\\_Layout.cshtml** file tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="85402-202">**My ASP.NET Application** uygulamasının tüm örneklerini **LITWARE's Products** olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="85402-202">Replace all occurrences of **My ASP.NET Application** with **LITWARE'S Products**.</span></span>
10. <span data-ttu-id="85402-203">Merhaba kaldırmak **giriş**, **hakkında**, ve **kişi** bağlantılar.</span><span class="sxs-lookup"><span data-stu-id="85402-203">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="85402-204">Merhaba vurgulanmış kodu silme:</span><span class="sxs-lookup"><span data-stu-id="85402-204">Delete hello highlighted code:</span></span>
    
    ![][28]
11. <span data-ttu-id="85402-205">Son olarak, hello gönderme sayfası tooinclude hello sırası hakkında bazı bilgiler değiştirin.</span><span class="sxs-lookup"><span data-stu-id="85402-205">Finally, modify hello submission page tooinclude some information about hello queue.</span></span> <span data-ttu-id="85402-206">İçinde **Çözüm Gezgini**, çift **Views\Home\Submit.cshtml** tooopen dosya hello Visual Studio düzenleyicisinde içinde.</span><span class="sxs-lookup"><span data-stu-id="85402-206">In **Solution Explorer**, double-click the **Views\Home\Submit.cshtml** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="85402-207">Satır sonlarında aşağıdaki hello eklemek `<h2>Submit</h2>`.</span><span class="sxs-lookup"><span data-stu-id="85402-207">Add hello following line after `<h2>Submit</h2>`.</span></span> <span data-ttu-id="85402-208">Şimdilik, hello `ViewBag.MessageCount` boş.</span><span class="sxs-lookup"><span data-stu-id="85402-208">For now, hello `ViewBag.MessageCount` is empty.</span></span> <span data-ttu-id="85402-209">Bu alanı daha sonra dolduracaksınız.</span><span class="sxs-lookup"><span data-stu-id="85402-209">You will populate it later.</span></span>
    
    ```html
    <p>Current number of orders in queue waiting toobe processed: @ViewBag.MessageCount</p>
    ```
12. <span data-ttu-id="85402-210">Şu anda kullanıcı arabiriminizi uyguladınız.</span><span class="sxs-lookup"><span data-stu-id="85402-210">You now have implemented your UI.</span></span> <span data-ttu-id="85402-211">Basabilirsiniz **F5** toorun uygulamanız ve istediğiniz gibi göründüğünü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="85402-211">You can press **F5** toorun your application and confirm that it looks as expected.</span></span>
    
    ![][17]

### <a name="write-hello-code-for-submitting-items-tooa-service-bus-queue"></a><span data-ttu-id="85402-212">Öğeleri tooa Service Bus kuyruğuna göndermek için hello kod yazma</span><span class="sxs-lookup"><span data-stu-id="85402-212">Write hello code for submitting items tooa Service Bus queue</span></span>
<span data-ttu-id="85402-213">Şimdi, öğeleri tooa sıraya göndermek için kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="85402-213">Now, add code for submitting items tooa queue.</span></span> <span data-ttu-id="85402-214">İlk olarak, Service Bus kuyruğunuzun bağlantı bilgilerini içeren bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="85402-214">First, you create a class that contains your Service Bus queue connection information.</span></span> <span data-ttu-id="85402-215">Ardından, bağlantınızı Global.aspx.cs üzerinden başlatın.</span><span class="sxs-lookup"><span data-stu-id="85402-215">Then, initialize your connection from Global.aspx.cs.</span></span> <span data-ttu-id="85402-216">Son olarak, daha önce HomeController.cs tooactually gönderme öğeleri tooa Service Bus sırada oluşturduğunuz hello gönderme kodunu güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="85402-216">Finally, update hello submission code you created earlier in HomeController.cs tooactually submit items tooa Service Bus queue.</span></span>

1. <span data-ttu-id="85402-217">İçinde **Çözüm Gezgini**, sağ **FrontendWebRole** (sağ hello proje, hello rolü değil).</span><span class="sxs-lookup"><span data-stu-id="85402-217">In **Solution Explorer**, right-click **FrontendWebRole** (right-click hello project, not hello role).</span></span> <span data-ttu-id="85402-218">**Ekle** seçeneğine ve ardından **Sınıf**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85402-218">Click **Add**, and then click **Class**.</span></span>
2. <span data-ttu-id="85402-219">Ad hello sınıfı **QueueConnector.cs**.</span><span class="sxs-lookup"><span data-stu-id="85402-219">Name hello class **QueueConnector.cs**.</span></span> <span data-ttu-id="85402-220">Tıklatın **Ekle** toocreate hello sınıfı.</span><span class="sxs-lookup"><span data-stu-id="85402-220">Click **Add** toocreate hello class.</span></span>
3. <span data-ttu-id="85402-221">Şimdi, hello bağlantı bilgilerini yalıtan ve hello bağlantı tooa Service Bus kuyruğuna başlatan kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="85402-221">Now, add code that encapsulates hello connection information and initializes hello connection tooa Service Bus queue.</span></span> <span data-ttu-id="85402-222">QueueConnector.cs tüm içeriğini Hello koddan hello ile değiştirin ve için değerleri girin `your Service Bus namespace` (ad alanı adınız) ve `yourKey`, hello olduğu **birincil anahtar** hello Azure ' daha önce edindiğiniz Portal.</span><span class="sxs-lookup"><span data-stu-id="85402-222">Replace hello entire contents of QueueConnector.cs with hello following code, and enter values for `your Service Bus namespace` (your namespace name) and `yourKey`, which is hello **primary key** you previously obtained from hello Azure portal.</span></span>
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from hello portal.
           public const string Namespace = "your Service Bus namespace";
   
           // hello name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create hello namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http toobe friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create hello namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create hello queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client toohello queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. <span data-ttu-id="85402-223">Şimdi **Başlat** yönteminizin çağrıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="85402-223">Now, ensure that your **Initialize** method gets called.</span></span> <span data-ttu-id="85402-224">**Çözüm Gezgini**'nde **Global.asax\Global.asax.cs** öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85402-224">In **Solution Explorer**, double-click **Global.asax\Global.asax.cs**.</span></span>
5. <span data-ttu-id="85402-225">Aşağıdaki kod hello hello sonunda hello eklemek **Application_Start** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="85402-225">Add hello following line of code at hello end of hello **Application_Start** method.</span></span>
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. <span data-ttu-id="85402-226">Son olarak, öğeleri toohello sıraya göndermek için daha önce oluşturduğunuz hello web kodunu güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="85402-226">Finally, update hello web code you created earlier, to submit items toohello queue.</span></span> <span data-ttu-id="85402-227">**Çözüm Gezgini**'nde **Controllers\HomeController.cs** öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85402-227">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span>
7. <span data-ttu-id="85402-228">Güncelleştirme hello `Submit()` yöntemini (parametre almayan hello aşırı yük) aşağıdaki gibi tooget selamlama iletisine saymak hello sırası.</span><span class="sxs-lookup"><span data-stu-id="85402-228">Update hello `Submit()` method (hello overload that takes no parameters) as follows tooget hello message count for hello queue.</span></span>
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you tooperform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get hello queue, and obtain hello message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. <span data-ttu-id="85402-229">Güncelleştirme hello `Submit(OnlineOrder order)` yöntemi (bir parametre alan hello aşırı yük) aşağıdaki gibi toosubmit sipariş bilgilerini toohello sırası.</span><span class="sxs-lookup"><span data-stu-id="85402-229">Update hello `Submit(OnlineOrder order)` method (hello overload that takes one parameter) as follows toosubmit order information toohello queue.</span></span>
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from hello order.
           var message = new BrokeredMessage(order);
   
           // Submit hello order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. <span data-ttu-id="85402-230">Şimdi hello uygulamayı tekrar çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85402-230">You can now run hello application again.</span></span> <span data-ttu-id="85402-231">Bir sipariş göndermek her zaman hello ileti sayısı da artar.</span><span class="sxs-lookup"><span data-stu-id="85402-231">Each time you submit an order, hello message count increases.</span></span>
   
   ![][18]

## <a name="create-hello-worker-role"></a><span data-ttu-id="85402-232">Merhaba çalışan rolü oluşturma</span><span class="sxs-lookup"><span data-stu-id="85402-232">Create hello worker role</span></span>
<span data-ttu-id="85402-233">Şimdi hello sipariş gönderimlerini işleyen hello çalışan rolü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="85402-233">You will now create hello worker role that processes hello order submissions.</span></span> <span data-ttu-id="85402-234">Bu örnek hello kullanır **Service Bus kuyruğu içeren çalışan rolü** Visual Studio Proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="85402-234">This example uses hello **Worker Role with Service Bus Queue** Visual Studio project template.</span></span> <span data-ttu-id="85402-235">Merhaba gerekli kimlik bilgileri zaten hello portaldan almıştınız.</span><span class="sxs-lookup"><span data-stu-id="85402-235">You already obtained hello required credentials from hello portal.</span></span>

1. <span data-ttu-id="85402-236">Visual Studio tooyour Azure hesabı bağladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="85402-236">Make sure you have connected Visual Studio tooyour Azure account.</span></span>
2. <span data-ttu-id="85402-237">Visual Studio'da içinde **Çözüm Gezgini** sağ **rolleri** hello altında bir klasör **MultiTierApp** projesi.</span><span class="sxs-lookup"><span data-stu-id="85402-237">In Visual Studio, in **Solution Explorer** right-click the **Roles** folder under hello **MultiTierApp** project.</span></span>
3. <span data-ttu-id="85402-238">**Ekle**'ye ve ardından **Yeni Çalışan Rolü Projesi**'ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85402-238">Click **Add**, and then click **New Worker Role Project**.</span></span> <span data-ttu-id="85402-239">Merhaba **yeni rol projesi Ekle** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="85402-239">hello **Add New Role Project** dialog box appears.</span></span>
   
   ![][26]
4. <span data-ttu-id="85402-240">Merhaba, **yeni rol projesi Ekle** iletişim kutusu, tıklatın **Service Bus kuyruğu içeren çalışan rolü**.</span><span class="sxs-lookup"><span data-stu-id="85402-240">In hello **Add New Role Project** dialog box, click **Worker Role with Service Bus Queue**.</span></span>
   
   ![][23]
5. <span data-ttu-id="85402-241">Merhaba, **adı** kutusu, ad hello proje **OrderProcessingRole**.</span><span class="sxs-lookup"><span data-stu-id="85402-241">In hello **Name** box, name hello project **OrderProcessingRole**.</span></span> <span data-ttu-id="85402-242">Daha sonra **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85402-242">Then click **Add**.</span></span>
6. <span data-ttu-id="85402-243">Merhaba "Service Bus ad alanı oluşturma" bölümünde toohello Pano 9. adımında elde ettiğiniz hello bağlantı dizesini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="85402-243">Copy hello connection string that you obtained in step 9 of hello "Create a Service Bus namespace" section toohello clipboard.</span></span>
7. <span data-ttu-id="85402-244">İçinde **Çözüm Gezgini**, sağ hello **OrderProcessingRole** 5. adımda oluşturduğunuz (, sağ emin olun **OrderProcessingRole** altında**Rolleri**, ve sınıf hello değil).</span><span class="sxs-lookup"><span data-stu-id="85402-244">In **Solution Explorer**, right-click hello **OrderProcessingRole** you created in step 5 (make sure that you right-click **OrderProcessingRole** under **Roles**, and not hello class).</span></span> <span data-ttu-id="85402-245">Daha sonra **Özellikler**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85402-245">Then click **Properties**.</span></span>
8. <span data-ttu-id="85402-246">Merhaba üzerinde **ayarları** hello sekmesinde **özellikleri** iletişim kutusunda hello içinde **değeri** kutusunun **Microsoft.ServiceBus.ConnectionString**ve 6. adımda kopyaladığınız hello uç nokta değerini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="85402-246">On hello **Settings** tab of hello **Properties** dialog box, click inside hello **Value** box for **Microsoft.ServiceBus.ConnectionString**, and then paste hello endpoint value you copied in step 6.</span></span>
   
   ![][25]
9. <span data-ttu-id="85402-247">Oluşturma bir **OnlineOrder** hello sıradan işlemek gibi toorepresent hello siparişleri sınıfı.</span><span class="sxs-lookup"><span data-stu-id="85402-247">Create an **OnlineOrder** class toorepresent hello orders as you process them from hello queue.</span></span> <span data-ttu-id="85402-248">Önceden oluşturduğunuz bir sınıfı yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85402-248">You can reuse a class you have already created.</span></span> <span data-ttu-id="85402-249">İçinde **Çözüm Gezgini**, sağ hello **OrderProcessingRole** sınıfı (sağ hello sınıf simgesi, hello rolü değil).</span><span class="sxs-lookup"><span data-stu-id="85402-249">In **Solution Explorer**, right-click hello **OrderProcessingRole** class (right-click hello class icon, not hello role).</span></span> <span data-ttu-id="85402-250">**Ekle**'ye ve **Var Olan Öğe**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85402-250">Click **Add**, then click **Existing Item**.</span></span>
10. <span data-ttu-id="85402-251">Toohello alt klasör için Gözat **FrontendWebRole\Models**, çift tıklayın ve ardından **OnlineOrder.cs** tooadd, toothis projesi.</span><span class="sxs-lookup"><span data-stu-id="85402-251">Browse toohello subfolder for **FrontendWebRole\Models**, and then double-click **OnlineOrder.cs** tooadd it toothis project.</span></span>
11. <span data-ttu-id="85402-252">İçinde **WorkerRole.cs**, hello hello değerini değiştirme **QueueName** değişkeni `"ProcessingQueue"` çok`"OrdersQueue"` hello kod aşağıdaki gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="85402-252">In **WorkerRole.cs**, change hello value of hello **QueueName** variable from `"ProcessingQueue"` too`"OrdersQueue"` as shown in hello following code.</span></span>
    
    ```csharp
    // hello name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. <span data-ttu-id="85402-253">Merhaba aşağıdakileri ekleyin hello'hello WorkerRole.cs dosyasının üst kısmında deyimiyle.</span><span class="sxs-lookup"><span data-stu-id="85402-253">Add hello following using statement at hello top of hello WorkerRole.cs file.</span></span>
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. <span data-ttu-id="85402-254">Merhaba, `Run()` işlevinde hello `OnMessage()` çağrısı, hello hello içeriğini değiştirin `try` yan tümcesiyle birlikte koddan hello.</span><span class="sxs-lookup"><span data-stu-id="85402-254">In hello `Run()` function, inside hello `OnMessage()` call, replace hello contents of hello `try` clause with hello following code.</span></span>
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View hello message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. <span data-ttu-id="85402-255">Merhaba uygulaması tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="85402-255">You have completed hello application.</span></span> <span data-ttu-id="85402-256">Çözüm Gezgini'nde hello MultiTierApp projesine sağ tıklayarak hello tam uygulama sınayabilirsiniz seçme **başlangıç projesi olarak ayarla**ve F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="85402-256">You can test hello full application by right-clicking hello MultiTierApp project in Solution Explorer, selecting **Set as Startup Project**, and then pressing F5.</span></span> <span data-ttu-id="85402-257">Merhaba çalışan rolü öğeleri hello sırasından işler ve bunları tamamlanmış olarak işaretler olduğundan ileti sayısında artış olmayacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="85402-257">Note that the message count does not increment, because hello worker role processes items from hello queue and marks them as complete.</span></span> <span data-ttu-id="85402-258">Hello Azure işlem öykünücüsü kullanıcı Arabiriminde görüntüleyerek çalışan rolünüzün izleme çıktısını hello görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85402-258">You can see hello trace output of your worker role by viewing hello Azure Compute Emulator UI.</span></span> <span data-ttu-id="85402-259">Merhaba bildirim alanı görev çubuğunuzdaki hello öykünücü simgesine sağ tıklayıp seçerek bunu yapabilirsiniz **Göster işlem öykünücüsü kullanıcı Arabiriminde**.</span><span class="sxs-lookup"><span data-stu-id="85402-259">You can do this by right-clicking hello emulator icon in hello notification area of your taskbar and selecting **Show Compute Emulator UI**.</span></span>
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a><span data-ttu-id="85402-260">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="85402-260">Next steps</span></span>
<span data-ttu-id="85402-261">Service Bus hakkında daha fazla toolearn kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="85402-261">toolearn more about Service Bus, see hello following resources:</span></span>  

* <span data-ttu-id="85402-262">[Azure Service Bus belgeleri][sbdocs]</span><span class="sxs-lookup"><span data-stu-id="85402-262">[Azure Service Bus documentation][sbdocs]</span></span>  
* <span data-ttu-id="85402-263">[Service Bus hizmet sayfası][sbacom]</span><span class="sxs-lookup"><span data-stu-id="85402-263">[Service Bus service page][sbacom]</span></span>  
* <span data-ttu-id="85402-264">[Nasıl tooUse hizmet veri yolu kuyrukları][sbacomqhowto]</span><span class="sxs-lookup"><span data-stu-id="85402-264">[How tooUse Service Bus Queues][sbacomqhowto]</span></span>  

<span data-ttu-id="85402-265">çok katmanlı senaryoları hakkında daha fazla toolearn bakın:</span><span class="sxs-lookup"><span data-stu-id="85402-265">toolearn more about multi-tier scenarios, see:</span></span>  

* <span data-ttu-id="85402-266">[Depolama Tabloları, Kuyruklar ve Blob'ların Kullanıldığı .NET Çok Katmanlı Uygulaması][mutitierstorage]</span><span class="sxs-lookup"><span data-stu-id="85402-266">[.NET Multi-Tier Application Using Storage Tables, Queues, and Blobs][mutitierstorage]</span></span>  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36
