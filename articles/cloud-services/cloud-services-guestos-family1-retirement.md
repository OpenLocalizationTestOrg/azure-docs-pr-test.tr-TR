---
title: "Konuk işletim sistemi ailesi 1 devre dışı bırakma dikkat edin. | Microsoft Docs"
description: "Ne zaman Azure konuk işletim sistemi ailesi 1 kullanımdan oldu ve etkilenip etkilenmediğini belirleme hakkında bilgi sağlar"
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 37b422e9-0713-4a81-a942-f553ef478064
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/21/2017
ms.author: raiye
ms.openlocfilehash: 3178a09dab1cb972a3460d54dc9908fb95cce68b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="guest-os-family-1-retirement-notice"></a><span data-ttu-id="7ea52-103">Konuk işletim sistemi ailesi 1 kullanımdan kaldırma bildirimi</span><span class="sxs-lookup"><span data-stu-id="7ea52-103">Guest OS Family 1 retirement notice</span></span>
<span data-ttu-id="7ea52-104">İşletim sistemi ailesi 1 kullanımdan ilk 1 Haziran 2013'te tanıtıldı.</span><span class="sxs-lookup"><span data-stu-id="7ea52-104">The retirement of OS Family 1 was first announced on June 1, 2013.</span></span>

<span data-ttu-id="7ea52-105">**2 Eylül 2014** Azure konuk işletim sistemi (konuk işletim sistemi) ailesi Windows Server 2008 işletim sistemi temelinde, 1.x resmi olarak Çekildi.</span><span class="sxs-lookup"><span data-stu-id="7ea52-105">**Sept 2, 2014** The Azure Guest operating system (Guest OS) Family 1.x, which is based on the Windows Server 2008 operating system, was officially retired.</span></span> <span data-ttu-id="7ea52-106">Yeni hizmetler dağıtmak veya var olan hizmetleri ailesi 1'i kullanarak yükseltmek için tüm denemeleri konuk işletim sistemi ailesi 1 devre dışı olduğunu bildiren bir hata iletisi ile başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="7ea52-106">All attempts to deploy new services or upgrade existing services using Family 1 will fail with an error message informing you that the Guest OS Family 1 has been retired.</span></span>

<span data-ttu-id="7ea52-107">**3 Kasım 2014** konuk işletim sistemi ailesi 1 için genişletilmiş destek sona erdi ve tam olarak Çekildi.</span><span class="sxs-lookup"><span data-stu-id="7ea52-107">**November 3, 2014** Extended support for Guest OS Family 1 ended and it is fully retired.</span></span> <span data-ttu-id="7ea52-108">Tüm hizmetler hala ailesi 1 üzerinde etkilenir.</span><span class="sxs-lookup"><span data-stu-id="7ea52-108">All services still on Family 1 will be impacted.</span></span> <span data-ttu-id="7ea52-109">Biz bu hizmetleri herhangi bir zamanda vermeyebilir.</span><span class="sxs-lookup"><span data-stu-id="7ea52-109">We may stop those services at any time.</span></span> <span data-ttu-id="7ea52-110">Hizmetlerinizin el ile bunları kendiniz yükseltmeniz sürece çalışmaya devam edecek garantisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="7ea52-110">There is no guarantee your services will continue to run unless you manually upgrade them yourself.</span></span>

<span data-ttu-id="7ea52-111">Ek sorularınız varsa, ziyaret [Cloud Services forumlarında](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) veya [Azure desteğine başvurun](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="7ea52-111">If you have additional questions, visit the [Cloud Services Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) or [contact Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="are-you-affected"></a><span data-ttu-id="7ea52-112">Etkilenen?</span><span class="sxs-lookup"><span data-stu-id="7ea52-112">Are you affected?</span></span>
<span data-ttu-id="7ea52-113">Aşağıdakilerden herhangi biri geçerliyse, bulut hizmetlerinize etkilenir:</span><span class="sxs-lookup"><span data-stu-id="7ea52-113">Your Cloud Services are affected if any one of the following applies:</span></span>

1. <span data-ttu-id="7ea52-114">Değerine sahip "osFamily"1"bulut hizmetiniz için ServiceConfiguration.cscfg dosyasında açıkça belirtilen =.</span><span class="sxs-lookup"><span data-stu-id="7ea52-114">You have a value of "osFamily = "1" explicitly specified in the ServiceConfiguration.cscfg file for your Cloud Service.</span></span>
2. <span data-ttu-id="7ea52-115">Açıkça bulut hizmetiniz için ServiceConfiguration.cscfg dosyasında belirtilen osFamily için bir değere sahip değil.</span><span class="sxs-lookup"><span data-stu-id="7ea52-115">You do not have a value for osFamily explicitly specified in the ServiceConfiguration.cscfg file for your Cloud Service.</span></span> <span data-ttu-id="7ea52-116">Şu anda, bu durumda varsayılan değerini "1" sistemi kullanır.</span><span class="sxs-lookup"><span data-stu-id="7ea52-116">Currently, the system uses the default value of "1" in this case.</span></span>
3. <span data-ttu-id="7ea52-117">Azure portalı ve konuk işletim sistemi ailesi değer "Windows sunucusu 2008" olarak listelenir.</span><span class="sxs-lookup"><span data-stu-id="7ea52-117">The Azure portal lists your Guest Operating System family value as "Windows Server 2008".</span></span>

<span data-ttu-id="7ea52-118">Yapmanız gerekenler rağmen bulut hizmetlerinizi, hangi işletim sistemi ailesi çalıştığı bulmak için aşağıdaki komut dosyası Azure PowerShell'de çalıştırabilirsiniz [Azure PowerShell ayarlamak](/powershell/azureps-cmdlets-docs) ilk.</span><span class="sxs-lookup"><span data-stu-id="7ea52-118">To find which of your cloud services are running which OS Family, you can run the following script in Azure PowerShell, though you must [set up Azure PowerShell](/powershell/azureps-cmdlets-docs) first.</span></span> <span data-ttu-id="7ea52-119">Komut dosyası hakkında daha fazla bilgi için bkz: [Azure konuk işletim sistemi ailesi 1 son, ömrü: Haziran 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ea52-119">For more information on the script, see [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span></span>

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

<span data-ttu-id="7ea52-120">Betik çıkışında osFamily sütun boş veya "1" içeriyorsa, bulut hizmetlerinize işletim sistemi ailesi 1 kullanımdan tarafından etkilenir.</span><span class="sxs-lookup"><span data-stu-id="7ea52-120">Your cloud services will be impacted by OS Family 1 retirement if the osFamily column in the script output is empty or contains a "1".</span></span>

## <a name="recommendations-if-you-are-affected"></a><span data-ttu-id="7ea52-121">Etkilenen varsa önerileri</span><span class="sxs-lookup"><span data-stu-id="7ea52-121">Recommendations if you are affected</span></span>
<span data-ttu-id="7ea52-122">Bulut hizmeti rollerinizi desteklenen konuk işletim sistemi ailelerinin birine geçirmek öneririz:</span><span class="sxs-lookup"><span data-stu-id="7ea52-122">We recommend you migrate your Cloud Service roles to one of the supported Guest OS Families:</span></span>

<span data-ttu-id="7ea52-123">**Konuk işletim sistemi ailesi 4.x** -Windows Server 2012 R2 *(önerilir)*</span><span class="sxs-lookup"><span data-stu-id="7ea52-123">**Guest OS family 4.x** - Windows Server 2012 R2 *(recommended)*</span></span>

1. <span data-ttu-id="7ea52-124">Uygulamanız .NET framework 4.0, 4.5 veya 4.5.1 SDK 2.1 veya üzeri kullandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="7ea52-124">Ensure that your application is using SDK 2.1 or later with .NET framework 4.0, 4.5 or 4.5.1.</span></span>
2. <span data-ttu-id="7ea52-125">"4" için osFamily özniteliği ServiceConfiguration.cscfg dosyasında ayarlanan ve bulut hizmeti yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="7ea52-125">Set the osFamily attribute to “4” in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="7ea52-126">**Konuk işletim sistemi ailesi 3.x** -Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="7ea52-126">**Guest OS family 3.x** - Windows Server 2012</span></span>

1. <span data-ttu-id="7ea52-127">Uygulamanız .NET framework 4.0 veya 4.5 ile SDK 1.8 veya sonraki sürümünü kullandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="7ea52-127">Ensure that your application is using SDK 1.8 or later with .NET framework 4.0 or 4.5.</span></span>
2. <span data-ttu-id="7ea52-128">"3" osFamily özniteliği ServiceConfiguration.cscfg dosyasında ayarlanan ve bulut hizmeti yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="7ea52-128">Set the osFamily attribute to “3” in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="7ea52-129">**Konuk işletim sistemi ailesi 2.x** -Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="7ea52-129">**Guest OS family 2.x** - Windows Server 2008 R2</span></span>

1. <span data-ttu-id="7ea52-130">Uygulamanızı SDK 1.3 kullandığından emin olun ve yukarıdaki .NET framework 3.5 veya 4.0 ile.</span><span class="sxs-lookup"><span data-stu-id="7ea52-130">Ensure that your application is using SDK 1.3 and above with .NET framework 3.5 or 4.0.</span></span>
2. <span data-ttu-id="7ea52-131">"2" osFamily özniteliği ServiceConfiguration.cscfg dosyasında ayarlanan ve bulut hizmeti yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="7ea52-131">Set the osFamily attribute to "2" in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a><span data-ttu-id="7ea52-132">3 Kas 2014 konuk işletim sistemi ailesi 1 için genişletilmiş destek sona erdi</span><span class="sxs-lookup"><span data-stu-id="7ea52-132">Extended Support for Guest OS Family 1 ended Nov 3, 2014</span></span>
<span data-ttu-id="7ea52-133">Bulut Hizmetleri konuk işletim sistemi ailesinde 1 artık desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="7ea52-133">Cloud services on Guest OS family 1 are no longer supported.</span></span> <span data-ttu-id="7ea52-134">Mümkün olan en kısa sürede hizmet kesintisi yaşamamak için ailesi 1 geçirin.</span><span class="sxs-lookup"><span data-stu-id="7ea52-134">Migrate off family 1 as soon as possible to avoid service disruption.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="7ea52-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7ea52-135">Next steps</span></span>
<span data-ttu-id="7ea52-136">En son gözden [konuk işletim sistemi sürümleri](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="7ea52-136">Review the latest [Guest OS releases](cloud-services-guestos-update-matrix.md).</span></span>
