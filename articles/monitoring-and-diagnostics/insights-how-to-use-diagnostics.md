---
title: "İzleme ve Tanılama, Microsoft Azure | Microsoft Docs"
description: "Azure kaynaklarınız için tanılama ayarlanacağını öğrenin."
author: rboucher
manager: carolz
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: af1947a9-c211-4aa1-8924-880a86240be4
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: b82bb1ab419831e803689edb2a2a7fe256dde5a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-monitoring-and-diagnostics"></a><span data-ttu-id="1194f-103">İzleme ve tanılamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="1194f-103">Enable monitoring and diagnostics</span></span>
<span data-ttu-id="1194f-104">İçinde [Azure Portal](https://portal.azure.com), zengin, sık, izleme ve tanılama veri kaynaklarınızı hakkında yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1194f-104">In the [Azure Portal](https://portal.azure.com), you can configure rich, frequent, monitoring and diagnostics data about your resources.</span></span> <span data-ttu-id="1194f-105">Aynı zamanda [REST API](https://msdn.microsoft.com/library/azure/dn931932.aspx) veya [.NET SDK'sı](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tanılama programlı olarak yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="1194f-105">You can also use the [REST API](https://msdn.microsoft.com/library/azure/dn931932.aspx) or [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) to configure diagnostics programmatically.</span></span>

<span data-ttu-id="1194f-106">Tanılama, izleme ve ölçüm verilerini azure'da tercih ettiğiniz bir Storage hesabına kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="1194f-106">Diagnostics, monitoring and metric data in Azure is saved into a Storage account of your choice.</span></span> <span data-ttu-id="1194f-107">Bu, bir depolama Gezgini'nde, veri, istediğiniz herhangi bir araç Power BI için üçüncü taraf araçları okuma kullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="1194f-107">This allows you to use whatever tooling you want to read the data, from a storage explorer, to Power BI to third-party tooling.</span></span>

## <a name="when-you-create-a-resource"></a><span data-ttu-id="1194f-108">Bir kaynak oluştururken</span><span class="sxs-lookup"><span data-stu-id="1194f-108">When you create a resource</span></span>
<span data-ttu-id="1194f-109">Çoğu Hizmetleri ilk bunları oluşturduğunuzda tanılamayı etkinleştirin izin [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1194f-109">Most services allow you to enable diagnostics when you first create them in the [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="1194f-110">Git **yeni** ve ilgilendiğiniz kaynağı seçin.</span><span class="sxs-lookup"><span data-stu-id="1194f-110">Go to **New** and choose the resource you are interested in.</span></span>
2. <span data-ttu-id="1194f-111">Seçin **isteğe bağlı yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="1194f-111">Select **Optional configuration**.</span></span>
    <span data-ttu-id="1194f-112">![Tanılama dikey penceresi](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)</span><span class="sxs-lookup"><span data-stu-id="1194f-112">![Diagnostics blade](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)</span></span>
3. <span data-ttu-id="1194f-113">Seçin **tanılama**, tıklatıp **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="1194f-113">Select **Diagnostics**, and click **On**.</span></span> <span data-ttu-id="1194f-114">Tanılama kaydedilmesini istediğiniz depolama hesabını seçin gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="1194f-114">You will need to choose the Storage account that you want diagnostics to be saved to.</span></span> <span data-ttu-id="1194f-115">Bir depolama hesabına tanılama gönderdiğinizde, depolama ve işlemler için normal veri ücretleri temel alınarak.</span><span class="sxs-lookup"><span data-stu-id="1194f-115">You’ll be charged normal data rates for storage and transactions when you send diagnostics to a storage account.</span></span>
4. <span data-ttu-id="1194f-116">Tıklatın **Tamam** ve kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1194f-116">Click **OK** and create the resource.</span></span>

## <a name="change-settings-for-an-existing-resource"></a><span data-ttu-id="1194f-117">Mevcut bir kaynağı ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="1194f-117">Change settings for an existing resource</span></span>
<span data-ttu-id="1194f-118">Bir kaynak oluşturmuş ve (veri toplama düzeyi örneğin değiştirmek için) tanılama ayarlarını değiştirmek istiyorsanız, doğrudan Azure portalında yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1194f-118">If you have already created a resource and you want to change the diagnostics settings (to change the level of data collection, for example), you can do that right in the Azure Portal.</span></span>

1. <span data-ttu-id="1194f-119">' A tıklayın ve kaynak Git **ayarları** komutu.</span><span class="sxs-lookup"><span data-stu-id="1194f-119">Go to the resource and click the **Settings** command.</span></span>
2. <span data-ttu-id="1194f-120">Seçin **tanılama**.</span><span class="sxs-lookup"><span data-stu-id="1194f-120">Select **Diagnostics**.</span></span>
3. <span data-ttu-id="1194f-121">**Tanılama** dikey penceresinde tüm olası tanılama ve izleme koleksiyonu veri kaynağı için vardır.</span><span class="sxs-lookup"><span data-stu-id="1194f-121">The **Diagnostics** blade has all of the possible diagnostics and monitoring collection data for that resource.</span></span> <span data-ttu-id="1194f-122">Bazı kaynaklar için de seçebileceğiniz bir **bekletme** verilerin depolama hesabınızdan temizlemek için ilke.</span><span class="sxs-lookup"><span data-stu-id="1194f-122">For some resources you can also choose a **Retention** policy for the data, to clean it up from your storage account.</span></span>
    <span data-ttu-id="1194f-123">![Depolama tanılama](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)</span><span class="sxs-lookup"><span data-stu-id="1194f-123">![Storage diagnostics](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)</span></span>
4. <span data-ttu-id="1194f-124">Ayarlarınızı seçtikten sonra tıklayın **kaydetmek** komutu.</span><span class="sxs-lookup"><span data-stu-id="1194f-124">Once you've chosen your settings, click the **Save** command.</span></span> <span data-ttu-id="1194f-125">İzleme sırasında bu ilk kez etkinleştireceğiniz varsa gösterilmeye verileri için biraz sürebilir.</span><span class="sxs-lookup"><span data-stu-id="1194f-125">It may take a little while for monitoring data to show up if you are enabling it for the first time.</span></span>

### <a name="categories-of-data-collection-for-virtual-machines"></a><span data-ttu-id="1194f-126">Sanal makineler için veri toplama kategorileri</span><span class="sxs-lookup"><span data-stu-id="1194f-126">Categories of data collection for virtual machines</span></span>
<span data-ttu-id="1194f-127">Makinenizin hakkında her zaman en güncel bilgileri yaşayabilirsiniz sanal makineler için tüm ölçümleri ve günlükleri bir dakikalık aralıklarla kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="1194f-127">For virtual machines all metrics and logs will be recorded at one-minute intervals, so you can always have the most up-to-date information about your machine.</span></span>

* <span data-ttu-id="1194f-128">**Temel ölçümleri** : sistem durumu ölçümleri işlemci ve bellek gibi sanal makinenize hakkında</span><span class="sxs-lookup"><span data-stu-id="1194f-128">**Basic metrics** : Health metrics about your virtual machine such as processor and memory</span></span>
* <span data-ttu-id="1194f-129">**Ağ ve web ölçümleri** : ölçümleri ağ bağlantıları ve web hizmetleri hakkında</span><span class="sxs-lookup"><span data-stu-id="1194f-129">**Network and web metrics** : Metrics about your network connections and web services</span></span>
* <span data-ttu-id="1194f-130">**.NET ölçümleri** : ölçümleri, sanal makine üzerinde çalışan .NET ve ASP.NET uygulamaları hakkında</span><span class="sxs-lookup"><span data-stu-id="1194f-130">**.NET metrics** : Metrics about the .NET and ASP.NET applications running on your virtual machine</span></span>
* <span data-ttu-id="1194f-131">**SQL ölçümleri** : Microsoft SQL Hizmeti, kendi performans ölçümleri çalıştırıyorsanız</span><span class="sxs-lookup"><span data-stu-id="1194f-131">**SQL metrics** : If you are running Microsoft SQL Service, its performance metrics</span></span>
* <span data-ttu-id="1194f-132">**Windows olayı uygulama günlükleri** : uygulama kanala gönderilir Windows olayları</span><span class="sxs-lookup"><span data-stu-id="1194f-132">**Windows event application logs** : Windows events that are sent to the application channel</span></span>
* <span data-ttu-id="1194f-133">**Windows olayı sistem günlükleri** : Sistem kanala gönderilir Windows olayları.</span><span class="sxs-lookup"><span data-stu-id="1194f-133">**Windows event system logs** : Windows events that are sent to the system channel.</span></span> <span data-ttu-id="1194f-134">Bu, tüm olayları da içerir [Microsoft Antimalware](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="1194f-134">This also includes all events from [Microsoft Antimalware](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409).</span></span>
* <span data-ttu-id="1194f-135">**Windows olayı güvenlik günlükleri** : güvenlik kanala gönderilir Windows olayları</span><span class="sxs-lookup"><span data-stu-id="1194f-135">**Windows event security logs** : Windows events that are sent to the security channel</span></span>
* <span data-ttu-id="1194f-136">**Tanılama altyapı günlükleri** : hakkında tanılama koleksiyonu altyapı günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="1194f-136">**Diagnostics infrastructure logs** : Logging about the diagnostics collection infrastructure</span></span>
* <span data-ttu-id="1194f-137">**IIS günlüklerini** : IIS sunucunuzu hakkında günlükleri</span><span class="sxs-lookup"><span data-stu-id="1194f-137">**IIS logs** : Logs about your IIS server</span></span>

<span data-ttu-id="1194f-138">Şu anda Linux belirli dağıtımları desteklenmez ve Konuk Aracısı sanal makineye yüklenmesi gerekir, unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1194f-138">Note that at this time certain distributions of Linux are not supported, and, the Guest Agent must be installed on the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1194f-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1194f-139">Next steps</span></span>
* <span data-ttu-id="1194f-140">İşletimsel olaylar gerçekleştiğinde ya da ölçümler bir eşiği aştığında [uyarı bildirimleri alın](insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="1194f-140">[Receive alert notifications](insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="1194f-141">[İzleme hizmeti ölçümleri](insights-how-to-customize-monitoring.md) hizmetinizi kullanılabilir ve yanıt verebilir durumda olduğundan emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="1194f-141">[Monitor service metrics](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
* <span data-ttu-id="1194f-142">[Örnek sayısı otomatik olarak ölçeklendirme](insights-how-to-scale.md) hizmet ölçek talebe dayalı emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="1194f-142">[Scale instance count automatically](insights-how-to-scale.md) to make sure your service scale based on demand.</span></span>
* <span data-ttu-id="1194f-143">[Uygulama performansı izleme](../application-insights/app-insights-azure-web-apps.md) tam olarak kodunuzu bulutta nasıl gerçekleştiriyor anlamak istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="1194f-143">[Monitor application performance](../application-insights/app-insights-azure-web-apps.md) if you want to understand exactly how your code is performing in the cloud.</span></span>
* <span data-ttu-id="1194f-144">[Olayları ve etkinlik günlüğü görüntüle](insights-debugging-with-events.md) hizmetinizi gerçekleştirilmedi her şeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="1194f-144">[View events and activity log](insights-debugging-with-events.md) to learn everything that has happened in your service.</span></span>
* <span data-ttu-id="1194f-145">[Hizmet durumu izleme](insights-service-health.md) Azure performans düşüşünü ya da hizmet kesintilerine yaşandığında öğrenin.</span><span class="sxs-lookup"><span data-stu-id="1194f-145">[Track service health](insights-service-health.md) to find out when Azure has experienced performance degradation or service interruptions.</span></span>

