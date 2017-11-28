---
title: "aaaGuest işletim sistemi ailesi 1 devre dışı bırakma dikkat edin. | Microsoft Docs"
description: "Hello Azure konuk işletim sistemi ailesi 1 kullanımdan oldu ne zaman ve nasıl hakkında bilgi sağlar, etkilenen varsa toodetermine"
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
ms.openlocfilehash: fa8b904c6560dbbe4982c301f818c7a5cbc4eacb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="guest-os-family-1-retirement-notice"></a><span data-ttu-id="d8540-103">Konuk işletim sistemi ailesi 1 kullanımdan kaldırma bildirimi</span><span class="sxs-lookup"><span data-stu-id="d8540-103">Guest OS Family 1 retirement notice</span></span>
<span data-ttu-id="d8540-104">işletim sistemi ailesi 1 Hello bırakma ilk 1 Haziran 2013'te tanıtıldı.</span><span class="sxs-lookup"><span data-stu-id="d8540-104">hello retirement of OS Family 1 was first announced on June 1, 2013.</span></span>

<span data-ttu-id="d8540-105">**2 Eylül 2014** Azure konuk işletim sistemi (konuk işletim sistemi) hello ailesi hello Windows Server 2008 işletim sistemi temelinde, 1.x resmi olarak Çekildi.</span><span class="sxs-lookup"><span data-stu-id="d8540-105">**Sept 2, 2014** hello Azure Guest operating system (Guest OS) Family 1.x, which is based on hello Windows Server 2008 operating system, was officially retired.</span></span> <span data-ttu-id="d8540-106">Tüm denemeleri toodeploy yeni hizmetleri veya ailesi 1'i kullanarak yükseltme varolan Hizmetleri konuk işletim sistemi ailesi 1 kullanımdan o hello bildiren bir hata iletisiyle başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="d8540-106">All attempts toodeploy new services or upgrade existing services using Family 1 will fail with an error message informing you that hello Guest OS Family 1 has been retired.</span></span>

<span data-ttu-id="d8540-107">**3 Kasım 2014** konuk işletim sistemi ailesi 1 için genişletilmiş destek sona erdi ve tam olarak Çekildi.</span><span class="sxs-lookup"><span data-stu-id="d8540-107">**November 3, 2014** Extended support for Guest OS Family 1 ended and it is fully retired.</span></span> <span data-ttu-id="d8540-108">Tüm hizmetler hala ailesi 1 üzerinde etkilenir.</span><span class="sxs-lookup"><span data-stu-id="d8540-108">All services still on Family 1 will be impacted.</span></span> <span data-ttu-id="d8540-109">Biz bu hizmetleri herhangi bir zamanda vermeyebilir.</span><span class="sxs-lookup"><span data-stu-id="d8540-109">We may stop those services at any time.</span></span> <span data-ttu-id="d8540-110">El ile bunları kendiniz yükseltmeniz sürece hizmetlerinizi toorun devam edecek garantisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="d8540-110">There is no guarantee your services will continue toorun unless you manually upgrade them yourself.</span></span>

<span data-ttu-id="d8540-111">Ek sorularınız varsa, hello ziyaret [Cloud Services forumlarında](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) veya [Azure desteğine başvurun](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="d8540-111">If you have additional questions, visit hello [Cloud Services Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) or [contact Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="are-you-affected"></a><span data-ttu-id="d8540-112">Etkilenen?</span><span class="sxs-lookup"><span data-stu-id="d8540-112">Are you affected?</span></span>
<span data-ttu-id="d8540-113">Merhaba aşağıdakilerden herhangi biri geçerliyse, bulut hizmetlerinize etkilenir:</span><span class="sxs-lookup"><span data-stu-id="d8540-113">Your Cloud Services are affected if any one of hello following applies:</span></span>

1. <span data-ttu-id="d8540-114">Değerine sahip "osFamily"1"Merhaba ServiceConfiguration.cscfg dosyasında bulut hizmetiniz için açıkça belirtilen =.</span><span class="sxs-lookup"><span data-stu-id="d8540-114">You have a value of "osFamily = "1" explicitly specified in hello ServiceConfiguration.cscfg file for your Cloud Service.</span></span>
2. <span data-ttu-id="d8540-115">Bulut hizmetiniz için açıkça hello ServiceConfiguration.cscfg dosyasında belirtilen osFamily için bir değere sahip değil.</span><span class="sxs-lookup"><span data-stu-id="d8540-115">You do not have a value for osFamily explicitly specified in hello ServiceConfiguration.cscfg file for your Cloud Service.</span></span> <span data-ttu-id="d8540-116">Şu anda, bu durumda hello varsayılan değerini "1" Merhaba sistemi kullanır.</span><span class="sxs-lookup"><span data-stu-id="d8540-116">Currently, hello system uses hello default value of "1" in this case.</span></span>
3. <span data-ttu-id="d8540-117">Hello Azure portal ve konuk işletim sistemi ailesi değer "Windows sunucusu 2008" olarak listelenir.</span><span class="sxs-lookup"><span data-stu-id="d8540-117">hello Azure portal lists your Guest Operating System family value as "Windows Server 2008".</span></span>

<span data-ttu-id="d8540-118">hangi bulut hizmetlerinizi hangi işletim sistemi ailesi çalıştıran toofind çalıştırabilirsiniz Azure PowerShell Betiği aşağıdaki hello gerekir ancak [Azure PowerShell ayarlamak](/powershell/azureps-cmdlets-docs) ilk.</span><span class="sxs-lookup"><span data-stu-id="d8540-118">toofind which of your cloud services are running which OS Family, you can run hello following script in Azure PowerShell, though you must [set up Azure PowerShell](/powershell/azureps-cmdlets-docs) first.</span></span> <span data-ttu-id="d8540-119">Merhaba komut dosyası hakkında daha fazla bilgi için bkz: [Azure konuk işletim sistemi ailesi 1 son, ömrü: Haziran 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8540-119">For more information on hello script, see [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span></span>

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

<span data-ttu-id="d8540-120">Merhaba osFamily sütun hello betik çıkışında boş veya "1" içeriyorsa, bulut hizmetlerinize işletim sistemi ailesi 1 kullanımdan tarafından etkilenir.</span><span class="sxs-lookup"><span data-stu-id="d8540-120">Your cloud services will be impacted by OS Family 1 retirement if hello osFamily column in hello script output is empty or contains a "1".</span></span>

## <a name="recommendations-if-you-are-affected"></a><span data-ttu-id="d8540-121">Etkilenen varsa önerileri</span><span class="sxs-lookup"><span data-stu-id="d8540-121">Recommendations if you are affected</span></span>
<span data-ttu-id="d8540-122">Bulut hizmeti rolleri tooone hello desteklenen konuk işletim sistemi ailelerinin geçirmek öneririz:</span><span class="sxs-lookup"><span data-stu-id="d8540-122">We recommend you migrate your Cloud Service roles tooone of hello supported Guest OS Families:</span></span>

<span data-ttu-id="d8540-123">**Konuk işletim sistemi ailesi 4.x** -Windows Server 2012 R2 *(önerilir)*</span><span class="sxs-lookup"><span data-stu-id="d8540-123">**Guest OS family 4.x** - Windows Server 2012 R2 *(recommended)*</span></span>

1. <span data-ttu-id="d8540-124">Uygulamanız .NET framework 4.0, 4.5 veya 4.5.1 SDK 2.1 veya üzeri kullandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="d8540-124">Ensure that your application is using SDK 2.1 or later with .NET framework 4.0, 4.5 or 4.5.1.</span></span>
2. <span data-ttu-id="d8540-125">Merhaba osFamily özniteliği "4" çok içinde hello ServiceConfiguration.cscfg dosyası ayarlayın ve bulut hizmeti yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d8540-125">Set hello osFamily attribute too“4” in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="d8540-126">**Konuk işletim sistemi ailesi 3.x** -Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="d8540-126">**Guest OS family 3.x** - Windows Server 2012</span></span>

1. <span data-ttu-id="d8540-127">Uygulamanız .NET framework 4.0 veya 4.5 ile SDK 1.8 veya sonraki sürümünü kullandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="d8540-127">Ensure that your application is using SDK 1.8 or later with .NET framework 4.0 or 4.5.</span></span>
2. <span data-ttu-id="d8540-128">Merhaba osFamily özniteliği "3" çok içinde hello ServiceConfiguration.cscfg dosyası ayarlayın ve bulut hizmeti yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d8540-128">Set hello osFamily attribute too“3” in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="d8540-129">**Konuk işletim sistemi ailesi 2.x** -Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="d8540-129">**Guest OS family 2.x** - Windows Server 2008 R2</span></span>

1. <span data-ttu-id="d8540-130">Uygulamanızı SDK 1.3 kullandığından emin olun ve yukarıdaki .NET framework 3.5 veya 4.0 ile.</span><span class="sxs-lookup"><span data-stu-id="d8540-130">Ensure that your application is using SDK 1.3 and above with .NET framework 3.5 or 4.0.</span></span>
2. <span data-ttu-id="d8540-131">Merhaba osFamily özniteliği "2" çok içinde hello ServiceConfiguration.cscfg dosyası ayarlayın ve bulut hizmeti yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d8540-131">Set hello osFamily attribute too"2" in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a><span data-ttu-id="d8540-132">3 Kas 2014 konuk işletim sistemi ailesi 1 için genişletilmiş destek sona erdi</span><span class="sxs-lookup"><span data-stu-id="d8540-132">Extended Support for Guest OS Family 1 ended Nov 3, 2014</span></span>
<span data-ttu-id="d8540-133">Bulut Hizmetleri konuk işletim sistemi ailesinde 1 artık desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="d8540-133">Cloud services on Guest OS family 1 are no longer supported.</span></span> <span data-ttu-id="d8540-134">Engellemeyi olası tooavoid hizmet hemen ailesi 1 geçirin.</span><span class="sxs-lookup"><span data-stu-id="d8540-134">Migrate off family 1 as soon as possible tooavoid service disruption.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d8540-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d8540-135">Next steps</span></span>
<span data-ttu-id="d8540-136">Gözden geçirme hello son [konuk işletim sistemi sürümleri](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="d8540-136">Review hello latest [Guest OS releases](cloud-services-guestos-update-matrix.md).</span></span>
