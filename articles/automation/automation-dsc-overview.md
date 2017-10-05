---
title: "Azure Otomasyonu DSC genel bakış | Microsoft Docs"
description: "Bir genel bakış, Azure Otomasyonu istenen durum yapılandırması (DSC), koşulları ve bilinen sorunlar"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "PowerShell dsc, istenen durum yapılandırması, powershell dsc azure"
ms.assetid: fd40cb68-c1a6-48c3-bba2-710b607d1555
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 468321fa6863d78bc0d179fbe5c2ed6195040d50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-dsc-overview"></a><span data-ttu-id="8c674-104">Azure Otomasyonu DSC genel bakış</span><span class="sxs-lookup"><span data-stu-id="8c674-104">Azure Automation DSC Overview</span></span>

<span data-ttu-id="8c674-105">Azure Otomasyonu DSC, yazma, yönetmek ve PowerShell istenen durum yapılandırması (DSC) derlemek için sağlayan bir Azure hizmetidir [yapılandırmaları](https://msdn.microsoft.com/powershell/dsc/configurations), içeri aktarma [DSC kaynakları](https://msdn.microsoft.com/powershell/dsc/resources)ve tüm bulutta hedef düğümleri yapılandırmaları atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c674-105">Azure Automation DSC is an Azure service that allows you to write, manage, and compile PowerShell Desired State Configuration (DSC) [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), import [DSC Resources](https://msdn.microsoft.com/powershell/dsc/resources), and assign configurations to target nodes, all in the cloud.</span></span>

## <a name="why-use-azure-automation-dsc"></a><span data-ttu-id="8c674-106">Azure Otomasyonu DSC neden kullanılır?</span><span class="sxs-lookup"><span data-stu-id="8c674-106">Why use Azure Automation DSC</span></span>

<span data-ttu-id="8c674-107">Azure Otomasyonu DSC Azure dışında DSC kullanarak birkaç avantajı sağlar.</span><span class="sxs-lookup"><span data-stu-id="8c674-107">Azure Automation DSC provides several advantages over using DSC outside of Azure.</span></span>

### <a name="built-in-pull-server"></a><span data-ttu-id="8c674-108">Yerleşik çekme sunucu</span><span class="sxs-lookup"><span data-stu-id="8c674-108">Built-in pull server</span></span>

<span data-ttu-id="8c674-109">Azure Automation'ın sağladığı bir [DSC istek sunucusuyla](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) hedef düğümleri otomatik olarak yapılandırmaları alması için bunları, belirtilen istenen duruma uyumlu ve uyumlulukları hakkında rapor.</span><span class="sxs-lookup"><span data-stu-id="8c674-109">Azure Automation provides a [DSC pull server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) so that target nodes automatically receive configurations, conform to the desired state, and report back on their compliance.</span></span>
<span data-ttu-id="8c674-110">Yerleşik çekme sunucunun Azure Automation ayarlama ve kendi çekme sunucunuz gereğini ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="8c674-110">The built-in pull server in Azure Automation eliminates the need to set up and maintain your own pull server.</span></span>
<span data-ttu-id="8c674-111">Azure Otomasyonu sanal veya fiziksel Windows veya Linux makineler, bulutta veya şirket içi hedefleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c674-111">Azure Automation can target virtual or physical Windows or Linux machines, in the cloud or on-premises.</span></span>

### <a name="management-of-all-your-dsc-artifacts"></a><span data-ttu-id="8c674-112">Tüm DSC yapıları Yönetimi</span><span class="sxs-lookup"><span data-stu-id="8c674-112">Management of all your DSC artifacts</span></span>

<span data-ttu-id="8c674-113">Azure Otomasyonu DSC aynı yönetim katmanı getirir [PowerShell istenen durum Yapılandırması](https://msdn.microsoft.com/powershell/dsc/overview) gibi Azure Otomasyonu PowerShell komut dosyası için sunar.</span><span class="sxs-lookup"><span data-stu-id="8c674-113">Azure Automation DSC brings the same management layer to [PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) as Azure Automation offers for PowerShell scripting.</span></span>

<span data-ttu-id="8c674-114">Azure portal veya PowerShell, tüm, DSC yapılandırmalarını, kaynak ve hedef düğümleri yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c674-114">From the Azure portal, or from PowerShell, you can manage all your DSC configurations, resources, and target nodes.</span></span>

![Azure Otomasyonu dikey penceresi ekran görüntüsü](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a><span data-ttu-id="8c674-116">Günlük analizi raporlama verilerini alma</span><span class="sxs-lookup"><span data-stu-id="8c674-116">Import reporting data into Log Analytics</span></span>

<span data-ttu-id="8c674-117">Azure Otomasyonu DSC'ye yönetilen düğümler ayrıntılı raporlama Durum verilerini yerleşik çekme sunucusuna gönderir.</span><span class="sxs-lookup"><span data-stu-id="8c674-117">Nodes that are managed with Azure Automation DSC send detailed reporting status data to the built-in pull server.</span></span>
<span data-ttu-id="8c674-118">Bu veriler, Microsoft Operations Management Suite (OMS) günlük analizi çalışma alanına göndermek için Azure Otomasyonu DSC yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c674-118">You can configure Azure Automation DSC to send this data to your Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>
<span data-ttu-id="8c674-119">Günlük analizi çalışma alanına DSC Durum verilerini gönderme hakkında bilgi edinmek için bkz: [İleri Azure Otomasyonu OMS günlük analizi veri raporlama DSC](automation-dsc-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="8c674-119">To learn how to send DSC status data to your Log Analytics workspace, see [Forward Azure Automation DSC reporting data to OMS Log Analytics](automation-dsc-diagnostics.md).</span></span>

## <a name="introduction-video"></a><span data-ttu-id="8c674-120">Tanıtım videosu</span><span class="sxs-lookup"><span data-stu-id="8c674-120">Introduction video</span></span>

<span data-ttu-id="8c674-121">Okumak yerine izlemeyi mi tercih ediyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="8c674-121">Prefer watching to reading?</span></span> <span data-ttu-id="8c674-122">Aşağıdaki video Mayıs 2015, ne zaman Azure Otomasyonu DSC ilk duyurulan göz vardır.</span><span class="sxs-lookup"><span data-stu-id="8c674-122">Have a look at the following video from May 2015, when Azure Automation DSC was first announced.</span></span>

>[!NOTE]
><span data-ttu-id="8c674-123">Kavramlar ve bu videoda ele alınan ömrünü doğru olsa da, bu videonun kaydedilmesinden sonra Azure Otomasyonu DSC değişmiştir.</span><span class="sxs-lookup"><span data-stu-id="8c674-123">While the concepts and life cycle discussed in this video are correct, Azure Automation DSC has progressed a lot since this video was recorded.</span></span>
><span data-ttu-id="8c674-124">Genel kullanıma sunulmuştur, Azure Portal'da daha geniş bir kullanıcı Arabirimine sahiptir ve birçok ek özellikleri desteklemektedir.</span><span class="sxs-lookup"><span data-stu-id="8c674-124">It is now generally available, has a much more extensive UI in the Azure portal, and supports many additional capabilities.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a><span data-ttu-id="8c674-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8c674-125">Next steps</span></span>

* <span data-ttu-id="8c674-126">Bilgi edinmek için nasıl Azure Otomasyonu DSC'ye yönetilecek yerleşik düğümleri için bkz: [Azure Otomasyonu DSC tarafından Yönetim için hazırlama makineler](automation-dsc-onboarding.md)</span><span class="sxs-lookup"><span data-stu-id="8c674-126">To learn how to onboard nodes to be managed with Azure Automation DSC, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span>
* <span data-ttu-id="8c674-127">Azure Automation DSC kullanmaya başlamak için bkz: [Azure Otomasyonu DSC ile çalışmaya başlama](automation-dsc-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="8c674-127">To get started using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="8c674-128">Böylece hedef düğümleri atayabilirsiniz DSC yapılandırmaları derleme hakkında bilgi edinmek için [Azure Otomasyonu DSC yapılandırmalarında derleme](automation-dsc-compile.md)</span><span class="sxs-lookup"><span data-stu-id="8c674-128">To learn about compiling DSC configurations so that you can assign them to target nodes, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md)</span></span>
* <span data-ttu-id="8c674-129">Azure Otomasyonu DSC için PowerShell cmdlet başvuru için bkz: [Azure Otomasyonu DSC cmdlet'leri](/powershell/module/azurerm.automation/#automation)</span><span class="sxs-lookup"><span data-stu-id="8c674-129">For PowerShell cmdlet reference for Azure Automation DSC, see [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
* <span data-ttu-id="8c674-130">Fiyatlandırma bilgileri için bkz: [Azure Otomasyonu DSC fiyatlandırma](https://azure.microsoft.com/pricing/details/automation/)</span><span class="sxs-lookup"><span data-stu-id="8c674-130">For pricing information, see [Azure Automation DSC pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
* <span data-ttu-id="8c674-131">Sürekli dağıtım ardışık düzeninde Azure Automation DSC kullanmaya ilişkin bir örnek görmek için bkz: [Iaas VM'ler kullanarak Azure Otomasyonu DSC ve Chocolatey sürekli dağıtım](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="8c674-131">To see an example of using Azure Automation DSC in a continuous deployment pipeline, see  [Continuous Deployment to IaaS VMs Using Azure Automation DSC and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>