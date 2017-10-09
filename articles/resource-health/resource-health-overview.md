---
title: "aaaAzure kaynak sistem durumu genel bakış | Microsoft Docs"
description: "Azure kaynak durumu genel bakış"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 06/01/2016
ms.author: BernardoAMunoz
ms.openlocfilehash: b920241b2f64a0695ba2c32e9ccb0c2c3739986d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-overview"></a><span data-ttu-id="ceb42-103">Azure kaynak sistem durumu genel bakış</span><span class="sxs-lookup"><span data-stu-id="ceb42-103">Azure resource health overview</span></span>
 
<span data-ttu-id="ceb42-104">Kaynak Durumu, bir Azure sorunu kaynaklarınızı etkilediğinde bunu tanılamanıza ve destek almanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ceb42-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="ceb42-105">Merhaba geçerli ve geçmiş kaynaklarınızın sistem durumunu hakkında bilgilendirir ve sorunları azaltmaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ceb42-105">It informs you about hello current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="ceb42-106">Kaynak Durumu, Azure hizmet sorunları ile ilgili yardıma ihtiyacınız olduğunda teknik destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="ceb42-106">Resource health provides technical support when you need help with Azure service issues.</span></span>

<span data-ttu-id="ceb42-107">Oysa [Azure durum](https://status.azure.com) Azure müşterilerine geniş bir dizi etkileyen hizmeti sorunları hakkında bilgilendirir, kaynak durumu hello kaynaklarınızın sistem durumunu içeren bir kişiselleştirilmiş Pano sağlar.</span><span class="sxs-lookup"><span data-stu-id="ceb42-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of hello health of your resources.</span></span> <span data-ttu-id="ceb42-108">Kaynak durumu gösterir, hello sürekli kaynaklarınızı hello kullanılamaz tooAzure hizmet sorunlarını süresi geçti.</span><span class="sxs-lookup"><span data-stu-id="ceb42-108">Resource health shows you all hello times your resources were unavailable in hello past due tooAzure service issues.</span></span> <span data-ttu-id="ceb42-109">Bir SLA ihlal varsa bu, toounderstand basit kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="ceb42-109">This makes it simple for you toounderstand if an SLA was violated.</span></span> 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a><span data-ttu-id="ceb42-110">Bir kaynak olarak kabul ve kaynak sağlıklı olup olmadığını karar nasıl kaynak durumu mu?</span><span class="sxs-lookup"><span data-stu-id="ceb42-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span></span>
<span data-ttu-id="ceb42-111">Örneğin bir Azure hizmeti aracılığıyla Azure Resource Manager tarafından sunulan bir kaynak türünün bir örneği bir kaynaktır: bir sanal makine, bir web uygulaması veya bir SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="ceb42-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span></span>

<span data-ttu-id="ceb42-112">Kaynak durumu üzerinde bir kaynak sağlıklı olup olmadığını hello farklı Azure Hizmetleri tooassess tarafından gösterilen sinyalleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="ceb42-112">Resource health relies on signals emitted by hello different Azure services tooassess if a resource is healthy or not.</span></span> <span data-ttu-id="ceb42-113">Bir kaynak sağlıksız ise, kaynak durumu ek bilgi toodetermine hello hello sorunun kaynağını analiz eder.</span><span class="sxs-lookup"><span data-stu-id="ceb42-113">If a resource is unhealthy, resource health analyzes additional information toodetermine hello source of hello problem.</span></span> <span data-ttu-id="ceb42-114">Ayrıca, Microsoft toofix hello sorunu veya tooaddress hello yapabileceğiniz işlemlerde hello sorununun nedeni ne sürüyor eylemleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ceb42-114">It also identifies actions Microsoft is taking toofix hello issue or what actions you can take tooaddress hello cause of hello problem.</span></span> 

<span data-ttu-id="ceb42-115">Gözden geçirme hello tam kaynak türleri ve sistem durumu denetimleri listesi [Azure kaynak durumu](resource-health-checks-resource-types.md) sistem durumu nasıl değerlendirildiği hakkında ek bilgi.</span><span class="sxs-lookup"><span data-stu-id="ceb42-115">Review hello full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span></span>

## <a name="health-status-provided-by-resource-health"></a><span data-ttu-id="ceb42-116">Kaynak durumu tarafından sağlanan sistem durumu</span><span class="sxs-lookup"><span data-stu-id="ceb42-116">Health status provided by resource health</span></span>
<span data-ttu-id="ceb42-117">bir kaynağın Hello sistem durumlarını izleyen hello biridir:</span><span class="sxs-lookup"><span data-stu-id="ceb42-117">hello health of a resource is one of hello following statuses:</span></span>

### <a name="available"></a><span data-ttu-id="ceb42-118">Kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="ceb42-118">Available</span></span>
<span data-ttu-id="ceb42-119">Merhaba hizmet hello kaynak hello durumunu etkileyen herhangi bir olayı algılamadı.</span><span class="sxs-lookup"><span data-stu-id="ceb42-119">hello service has not detected any events impacting hello health of hello resource.</span></span> <span data-ttu-id="ceb42-120">Burada hello kaynak kurtarıldı Planlanmamış kapalı kalma süresi sırasında hello son durumlarda görürsünüz: 24 saat hello **kısa süre önce kurtarıldıysa** bildirim.</span><span class="sxs-lookup"><span data-stu-id="ceb42-120">In cases where hello resource has recovered from unplanned downtime during hello last 24 hours you will see hello **recently recovered** notification.</span></span>

![Kaynak sistem durumu kullanılabilir sanal makine](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a><span data-ttu-id="ceb42-122">Kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="ceb42-122">Unavailable</span></span>
<span data-ttu-id="ceb42-123">Merhaba hizmeti devam eden platform veya hello kaynak hello sağlığını etkileyen olmayan platform olayı algıladı.</span><span class="sxs-lookup"><span data-stu-id="ceb42-123">hello service has detected an ongoing platform or non-platform event impacting hello health of hello resource.</span></span>

#### <a name="platform-events"></a><span data-ttu-id="ceb42-124">Platform olayları</span><span class="sxs-lookup"><span data-stu-id="ceb42-124">Platform events</span></span>
<span data-ttu-id="ceb42-125">Bu olaylar, birden çok hello Azure altyapı bileşenleri tarafından tetiklenen ve hem planlı bakım gibi zamanlanmış Eylemler ve planlanmamış ana bilgisayar yeniden başlatma gibi beklenmeyen olaylar içerir.</span><span class="sxs-lookup"><span data-stu-id="ceb42-125">These events are triggered by multiple components of hello Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span></span>

<span data-ttu-id="ceb42-126">Kaynak durumu hello olay hello kurtarma işlemi ek ayrıntılar sağlar ve etkin bir Microsoft sözleşmesi destek yüklü olmasa bile, toocontact desteği sağlar.</span><span class="sxs-lookup"><span data-stu-id="ceb42-126">Resource health provides additional details on hello event, hello recovery process and enables you toocontact support even if you don't have an active Microsoft support agreement.</span></span>

![Kaynak durumu kullanılamıyor sanal makine tooplatform olay süresi](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a><span data-ttu-id="ceb42-128">Platform olmayan olaylar</span><span class="sxs-lookup"><span data-stu-id="ceb42-128">Non-Platform events</span></span>
<span data-ttu-id="ceb42-129">Bu olaylar, örneğin bir sanal makineyi durdurmak veya bağlantıları tooa Redis önbelleği hello sayısının ulaşmasını kullanıcılar tarafından gerçekleştirilen eylemler tarafından tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="ceb42-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching hello maximum number of connections tooa Redis Cache.</span></span>

![Kaynak durumu kullanılamıyor sanal makine toonon platform olayı nedeniyle](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a><span data-ttu-id="ceb42-131">Bilinmeyen</span><span class="sxs-lookup"><span data-stu-id="ceb42-131">Unknown</span></span>
<span data-ttu-id="ceb42-132">Bu sistem durumu, kaynak durumu 10 dakikadan bu kaynak hakkındaki bilgileri almadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ceb42-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span></span> <span data-ttu-id="ceb42-133">Bu durum hello kaynak hello durumunun kesin bir gösterge olmamasına karşın, bir sorun giderme işlemi hello önemli veri noktası verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ceb42-133">While this status is not a definitive indication of hello state of hello resource, it is an important data point in hello troubleshooting process:</span></span>
* <span data-ttu-id="ceb42-134">Merhaba kaynak hello kaynak beklenen hello durumu çalışıyorsa, tooAvailable birkaç dakika sonra güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ceb42-134">If hello resource is running as expected hello status of hello resource will update tooAvailable after a few minutes.</span></span>
* <span data-ttu-id="ceb42-135">Merhaba kaynak sorunlarla karşılaşıyorsanız, hello bilinmeyen durumu hello kaynak hello Platform bir olay tarafından etkilenen önerebilir.</span><span class="sxs-lookup"><span data-stu-id="ceb42-135">If you are experiencing problems with hello resource, hello Unknown health status may suggest hello resource is impacted by an event in hello platform.</span></span>

![Kaynak sistem durumu bilinmeyen sanal makine](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a><span data-ttu-id="ceb42-137">Yanlış bir durum raporu</span><span class="sxs-lookup"><span data-stu-id="ceb42-137">Report an incorrect status</span></span>
<span data-ttu-id="ceb42-138">Herhangi bir noktada hello geçerli sistem durumu hatalı olduğunu düşünüyorsanız, bize tıklayarak bildiğiniz **yanlış sistem durumu raporu**.</span><span class="sxs-lookup"><span data-stu-id="ceb42-138">If at any point you believe hello current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span></span> <span data-ttu-id="ceb42-139">Burada bir Azure sorundan etkilenen durumlarda hello kaynak sistem durumu dikey toocontact Destek'ten öneririz.</span><span class="sxs-lookup"><span data-stu-id="ceb42-139">In cases where you are impacted by an Azure problem, we encourage you toocontact support from hello resource health blade.</span></span> 

![Kaynak durumu rapor yanlış durumu](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a><span data-ttu-id="ceb42-141">Geçmiş bilgileri</span><span class="sxs-lookup"><span data-stu-id="ceb42-141">Historical Information</span></span>
<span data-ttu-id="ceb42-142">Geçmiş durumu verilerinin too14 günleri tıklatarak erişebilirsiniz **geçmişini görüntüleme** hello kaynak sistem durumu dikey.</span><span class="sxs-lookup"><span data-stu-id="ceb42-142">You can access up too14 days of historical health data by clicking **View History** in hello Resource health blade.</span></span> 

![Kaynak durumu rapor geçmişi](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a><span data-ttu-id="ceb42-144">Başlarken</span><span class="sxs-lookup"><span data-stu-id="ceb42-144">Getting started</span></span>
<span data-ttu-id="ceb42-145">tooopen bir kaynak için kaynak durumu</span><span class="sxs-lookup"><span data-stu-id="ceb42-145">tooopen Resource health for one resource</span></span>
1.  <span data-ttu-id="ceb42-146">Hello Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ceb42-146">Sign in into hello Azure portal.</span></span>
2.  <span data-ttu-id="ceb42-147">Tooyour kaynak gidin.</span><span class="sxs-lookup"><span data-stu-id="ceb42-147">Navigate tooyour resource.</span></span>
3.  <span data-ttu-id="ceb42-148">Merhaba kaynak menüsünü Hello sol tarafta bulunan **kaynak durumu**.</span><span class="sxs-lookup"><span data-stu-id="ceb42-148">In hello resource menu located in hello left-hand side, click **Resource health**.</span></span>

![Kaynak dikey penceresinden açık kaynak durumu](./media/resource-health-overview/from-resource-blade.png)

<span data-ttu-id="ceb42-150">Kaynak durumu tıklatarak da erişebilirsiniz **daha fazla hizmet**, yazarak **kaynak durumu** filtre metin kutusu tooopen hello içinde **Yardım + Destek** dikey.</span><span class="sxs-lookup"><span data-stu-id="ceb42-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box tooopen hello **Help + Support** blade.</span></span> <span data-ttu-id="ceb42-151">Son olarak tıklatın [ **kaynak durumu**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span><span class="sxs-lookup"><span data-stu-id="ceb42-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span></span>

![Daha fazla hizmetinden açık kaynak durumu](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a><span data-ttu-id="ceb42-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ceb42-153">Next steps</span></span>

<span data-ttu-id="ceb42-154">Bu kaynaklar toolearn kaynak durumu hakkında daha fazla gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="ceb42-154">Check out these resources toolearn more about resource health:</span></span>
-  [<span data-ttu-id="ceb42-155">Kaynak türleri ve sistem durumu denetler Azure kaynak durumu</span><span class="sxs-lookup"><span data-stu-id="ceb42-155">Resource types and health checks in Azure resource health</span></span>](resource-health-checks-resource-types.md)
-  [<span data-ttu-id="ceb42-156">Azure kaynak durumu hakkında sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="ceb42-156">Frequently asked questions about Azure resource health</span></span>](resource-health-faq.md)




