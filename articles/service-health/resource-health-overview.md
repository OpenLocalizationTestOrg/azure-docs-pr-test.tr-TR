---
title: "Azure kaynak sistem durumu genel bakış | Microsoft Docs"
description: "Azure kaynak durumu genel bakış"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/01/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: 040d58a81a9b41fe660e4276d698bf884f90bb6c
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="azure-resource-health-overview"></a><span data-ttu-id="cfaca-103">Azure kaynak sistem durumu genel bakış</span><span class="sxs-lookup"><span data-stu-id="cfaca-103">Azure resource health overview</span></span>
 
<span data-ttu-id="cfaca-104">Kaynak Durumu, bir Azure sorunu kaynaklarınızı etkilediğinde bunu tanılamanıza ve destek almanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="cfaca-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="cfaca-105">Kaynaklarınızın güncel ve geçmiş durumu hakkında bilgiler sağlar ve sorunları azaltmaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="cfaca-105">It informs you about the current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="cfaca-106">Kaynak Durumu, Azure hizmet sorunları ile ilgili yardıma ihtiyacınız olduğunda teknik destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="cfaca-106">Resource health provides technical support when you need help with Azure service issues.</span></span>

<span data-ttu-id="cfaca-107">Oysa [Azure durum](https://status.azure.com) Azure müşterilerine geniş bir dizi etkileyen hizmeti sorunları hakkında bilgilendirir, kaynak durumu kaynaklarınızın sistem durumunu içeren bir kişiselleştirilmiş Pano sağlar.</span><span class="sxs-lookup"><span data-stu-id="cfaca-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of the health of your resources.</span></span> <span data-ttu-id="cfaca-108">Kaynak durumu kaynaklarınızı Azure hizmeti sorunları nedeniyle geçmişte kullanılamaz her zaman gösterir.</span><span class="sxs-lookup"><span data-stu-id="cfaca-108">Resource health shows you all the times your resources were unavailable in the past due to Azure service issues.</span></span> <span data-ttu-id="cfaca-109">Bu, sizin için bir SLA ihlal edildiğini anlamak basit kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="cfaca-109">This makes it simple for you to understand if an SLA was violated.</span></span> 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a><span data-ttu-id="cfaca-110">Bir kaynak olarak kabul ve kaynak sağlıklı olup olmadığını karar nasıl kaynak durumu mu?</span><span class="sxs-lookup"><span data-stu-id="cfaca-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span></span>
<span data-ttu-id="cfaca-111">Örneğin bir Azure hizmeti aracılığıyla Azure Resource Manager tarafından sunulan bir kaynak türünün bir örneği bir kaynaktır: bir sanal makine, bir web uygulaması veya bir SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="cfaca-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span></span>

<span data-ttu-id="cfaca-112">Kaynak durumu sinyalleri üzerinde farklı Azure Hizmetleri tarafından yayılan bir kaynak sağlıklı olup olmadığını değerlendirmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="cfaca-112">Resource health relies on signals emitted by the different Azure services to assess if a resource is healthy or not.</span></span> <span data-ttu-id="cfaca-113">Bir kaynak sağlıksız ise, kaynak durumu sorunun kaynağını belirlemek için ek bilgiler analiz eder.</span><span class="sxs-lookup"><span data-stu-id="cfaca-113">If a resource is unhealthy, resource health analyzes additional information to determine the source of the problem.</span></span> <span data-ttu-id="cfaca-114">Ayrıca Microsoft, sorunu düzeltmek için sürüyor eylemleri tanımlar veya hangi eylemleri sorunun nedenini gidermek için atabileceğiniz.</span><span class="sxs-lookup"><span data-stu-id="cfaca-114">It also identifies actions Microsoft is taking to fix the issue or what actions you can take to address the cause of the problem.</span></span> 

<span data-ttu-id="cfaca-115">Kaynak türleri tam listesini gözden geçirin ve sistem durumu denetler [Azure kaynak durumu](resource-health-checks-resource-types.md) sistem durumu nasıl değerlendirildiği hakkında ek bilgi.</span><span class="sxs-lookup"><span data-stu-id="cfaca-115">Review the full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span></span>

## <a name="health-status-provided-by-resource-health"></a><span data-ttu-id="cfaca-116">Kaynak durumu tarafından sağlanan sistem durumu</span><span class="sxs-lookup"><span data-stu-id="cfaca-116">Health status provided by resource health</span></span>
<span data-ttu-id="cfaca-117">Bir kaynak sistem durumu aşağıdaki durumlardan biri:</span><span class="sxs-lookup"><span data-stu-id="cfaca-117">The health of a resource is one of the following statuses:</span></span>

### <a name="available"></a><span data-ttu-id="cfaca-118">Kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="cfaca-118">Available</span></span>
<span data-ttu-id="cfaca-119">Hizmet kaynak durumunu etkileyen herhangi bir olayı algılamadı.</span><span class="sxs-lookup"><span data-stu-id="cfaca-119">The service has not detected any events impacting the health of the resource.</span></span> <span data-ttu-id="cfaca-120">Burada kaynak kurtarıldı Planlanmamış kapalı kalma süresi son 24 saatte durumlarda görürsünüz **kısa süre önce kurtarıldıysa** bildirim.</span><span class="sxs-lookup"><span data-stu-id="cfaca-120">In cases where the resource has recovered from unplanned downtime during the last 24 hours you will see the **recently recovered** notification.</span></span>

![Kaynak sistem durumu kullanılabilir sanal makine](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a><span data-ttu-id="cfaca-122">Kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="cfaca-122">Unavailable</span></span>
<span data-ttu-id="cfaca-123">Hizmet bir devam eden platform veya kaynak sağlığını etkileyen olmayan platform olayı algıladı.</span><span class="sxs-lookup"><span data-stu-id="cfaca-123">The service has detected an ongoing platform or non-platform event impacting the health of the resource.</span></span>

#### <a name="platform-events"></a><span data-ttu-id="cfaca-124">Platform olayları</span><span class="sxs-lookup"><span data-stu-id="cfaca-124">Platform events</span></span>
<span data-ttu-id="cfaca-125">Bu olaylar, birden çok Azure altyapı bileşenleri tarafından tetiklenen ve hem planlı bakım gibi zamanlanmış Eylemler ve planlanmamış ana bilgisayar yeniden başlatma gibi beklenmeyen olaylar içerir.</span><span class="sxs-lookup"><span data-stu-id="cfaca-125">These events are triggered by multiple components of the Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span></span>

<span data-ttu-id="cfaca-126">Kaynak sistem durumu kurtarma işlemi olayına ek ayrıntılar sağlar ve etkin bir Microsoft sözleşmesi destek yüklü olmasa bile, desteğe başvurun olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="cfaca-126">Resource health provides additional details on the event, the recovery process and enables you to contact support even if you don't have an active Microsoft support agreement.</span></span>

![Kaynak durumu kullanılamıyor sanal makine platform olayı nedeniyle](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a><span data-ttu-id="cfaca-128">Platform olmayan olaylar</span><span class="sxs-lookup"><span data-stu-id="cfaca-128">Non-Platform events</span></span>
<span data-ttu-id="cfaca-129">Bu olaylar, örneğin bir sanal makineyi durdurmak veya bir Redis önbelleğine bağlantı sayısını ulaşmasını kullanıcılar tarafından gerçekleştirilen eylemler tarafından tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="cfaca-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching the maximum number of connections to a Redis Cache.</span></span>

![Kaynak durumu kullanılamıyor sanal makine olmayan platform olayı nedeniyle](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a><span data-ttu-id="cfaca-131">Bilinmeyen</span><span class="sxs-lookup"><span data-stu-id="cfaca-131">Unknown</span></span>
<span data-ttu-id="cfaca-132">Bu sistem durumu, kaynak durumu 10 dakikadan bu kaynak hakkındaki bilgileri almadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="cfaca-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span></span> <span data-ttu-id="cfaca-133">Bu durum, kaynak durumunun kesin bir gösterge olmamasına karşın, bir sorun giderme sürecini önemli veri noktası verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="cfaca-133">While this status is not a definitive indication of the state of the resource, it is an important data point in the troubleshooting process:</span></span>
* <span data-ttu-id="cfaca-134">Kaynak kaynağının durumunu beklendiği gibi çalışıyorsa kullanılabilir için birkaç dakika sonra güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="cfaca-134">If the resource is running as expected the status of the resource will update to Available after a few minutes.</span></span>
* <span data-ttu-id="cfaca-135">Kaynak sorunlarla karşılaşıyorsanız, bilinmeyen sistem durumunu kaynak Platform bir olay tarafından etkilenen önerebilir.</span><span class="sxs-lookup"><span data-stu-id="cfaca-135">If you are experiencing problems with the resource, the Unknown health status may suggest the resource is impacted by an event in the platform.</span></span>

![Kaynak sistem durumu bilinmeyen sanal makine](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a><span data-ttu-id="cfaca-137">Yanlış bir durum raporu</span><span class="sxs-lookup"><span data-stu-id="cfaca-137">Report an incorrect status</span></span>
<span data-ttu-id="cfaca-138">Herhangi bir noktada, geçerli sistem durumunu hatalı olduğunu düşünüyorsanız, bize tıklayarak bilebilir **yanlış sistem durumu raporu**.</span><span class="sxs-lookup"><span data-stu-id="cfaca-138">If at any point you believe the current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span></span> <span data-ttu-id="cfaca-139">Burada bir Azure sorundan etkilenen durumlarda kaynak sistem durumu dikey penceresinden desteği ile iletişim öneririz.</span><span class="sxs-lookup"><span data-stu-id="cfaca-139">In cases where you are impacted by an Azure problem, we encourage you to contact support from the resource health blade.</span></span> 

![Kaynak durumu rapor yanlış durumu](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a><span data-ttu-id="cfaca-141">Geçmiş bilgileri</span><span class="sxs-lookup"><span data-stu-id="cfaca-141">Historical Information</span></span>
<span data-ttu-id="cfaca-142">14 gün geçmiş durumu verilerinin tıklatarak erişebilirsiniz **geçmişini görüntüleme** kaynak sistem durumu dikey.</span><span class="sxs-lookup"><span data-stu-id="cfaca-142">You can access up to 14 days of historical health data by clicking **View History** in the Resource health blade.</span></span> 

![Kaynak durumu rapor geçmişi](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a><span data-ttu-id="cfaca-144">Başlarken</span><span class="sxs-lookup"><span data-stu-id="cfaca-144">Getting started</span></span>
<span data-ttu-id="cfaca-145">Bir kaynak için kaynak durumu açmak için</span><span class="sxs-lookup"><span data-stu-id="cfaca-145">To open Resource health for one resource</span></span>
1.  <span data-ttu-id="cfaca-146">Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="cfaca-146">Sign in into the Azure portal.</span></span>
2.  <span data-ttu-id="cfaca-147">Kaynağınıza gidin.</span><span class="sxs-lookup"><span data-stu-id="cfaca-147">Navigate to your resource.</span></span>
3.  <span data-ttu-id="cfaca-148">Sol tarafta bulunan kaynak menüye tıklayın **kaynak durumu**.</span><span class="sxs-lookup"><span data-stu-id="cfaca-148">In the resource menu located in the left-hand side, click **Resource health**.</span></span>

![Kaynak dikey penceresinden açık kaynak durumu](./media/resource-health-overview/from-resource-blade.png)

<span data-ttu-id="cfaca-150">Kaynak durumu tıklatarak da erişebilirsiniz **daha fazla hizmet**, yazarak **kaynak durumu** açmak için filtre metni kutusuna **Yardım + Destek** dikey.</span><span class="sxs-lookup"><span data-stu-id="cfaca-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box to open the **Help + Support** blade.</span></span> <span data-ttu-id="cfaca-151">Son olarak tıklatın [ **kaynak durumu**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span><span class="sxs-lookup"><span data-stu-id="cfaca-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span></span>

![Daha fazla hizmetinden açık kaynak durumu](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a><span data-ttu-id="cfaca-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cfaca-153">Next steps</span></span>

<span data-ttu-id="cfaca-154">Kaynak durumu hakkında daha fazla bilgi için şu kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="cfaca-154">Check out these resources to learn more about resource health:</span></span>
-  [<span data-ttu-id="cfaca-155">Kaynak türleri ve sistem durumu denetler Azure kaynak durumu</span><span class="sxs-lookup"><span data-stu-id="cfaca-155">Resource types and health checks in Azure resource health</span></span>](resource-health-checks-resource-types.md)
-  [<span data-ttu-id="cfaca-156">Azure kaynak durumu hakkında sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="cfaca-156">Frequently asked questions about Azure resource health</span></span>](resource-health-faq.md)




