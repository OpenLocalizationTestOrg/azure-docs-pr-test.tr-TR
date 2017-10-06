---
title: "aaaAzure Automation DSC genel bakış | Microsoft Docs"
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
ms.openlocfilehash: 5b8e5104c7b5bed848c015ac26a8b7d1f5b24de9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-dsc-overview"></a><span data-ttu-id="df85b-104">Azure Otomasyonu DSC genel bakış</span><span class="sxs-lookup"><span data-stu-id="df85b-104">Azure Automation DSC Overview</span></span>

<span data-ttu-id="df85b-105">Azure Otomasyonu DSC, toowrite sağlayan bir Azure hizmetidir, yönetmek ve PowerShell istenen durum yapılandırması (DSC) derlemek [yapılandırmaları](https://msdn.microsoft.com/powershell/dsc/configurations), içeri aktarma [DSC kaynakları](https://msdn.microsoft.com/powershell/dsc/resources)ve atayın Merhaba bulutta tüm yapılandırmaları tootarget düğümleri.</span><span class="sxs-lookup"><span data-stu-id="df85b-105">Azure Automation DSC is an Azure service that allows you toowrite, manage, and compile PowerShell Desired State Configuration (DSC) [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), import [DSC Resources](https://msdn.microsoft.com/powershell/dsc/resources), and assign configurations tootarget nodes, all in hello cloud.</span></span>

## <a name="why-use-azure-automation-dsc"></a><span data-ttu-id="df85b-106">Azure Otomasyonu DSC neden kullanılır?</span><span class="sxs-lookup"><span data-stu-id="df85b-106">Why use Azure Automation DSC</span></span>

<span data-ttu-id="df85b-107">Azure Otomasyonu DSC Azure dışında DSC kullanarak birkaç avantajı sağlar.</span><span class="sxs-lookup"><span data-stu-id="df85b-107">Azure Automation DSC provides several advantages over using DSC outside of Azure.</span></span>

### <a name="built-in-pull-server"></a><span data-ttu-id="df85b-108">Yerleşik çekme sunucu</span><span class="sxs-lookup"><span data-stu-id="df85b-108">Built-in pull server</span></span>

<span data-ttu-id="df85b-109">Azure Automation'ın sağladığı bir [DSC istek sunucusuyla](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) hedef düğümleri otomatik olarak yapılandırmaları alması için bunları istenen toohello durumu uygun ve uyumlulukları hakkında rapor.</span><span class="sxs-lookup"><span data-stu-id="df85b-109">Azure Automation provides a [DSC pull server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) so that target nodes automatically receive configurations, conform toohello desired state, and report back on their compliance.</span></span>
<span data-ttu-id="df85b-110">Azure Otomasyonu Hello yerleşik çekme sunucusunda yukarı hello gerek tooset ortadan kaldırır ve kendi çekme sunucunuz.</span><span class="sxs-lookup"><span data-stu-id="df85b-110">hello built-in pull server in Azure Automation eliminates hello need tooset up and maintain your own pull server.</span></span>
<span data-ttu-id="df85b-111">Azure Otomasyonu sanal veya fiziksel Windows veya Linux makineler, hello Bulut veya şirket içi hedefleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df85b-111">Azure Automation can target virtual or physical Windows or Linux machines, in hello cloud or on-premises.</span></span>

### <a name="management-of-all-your-dsc-artifacts"></a><span data-ttu-id="df85b-112">Tüm DSC yapıları Yönetimi</span><span class="sxs-lookup"><span data-stu-id="df85b-112">Management of all your DSC artifacts</span></span>

<span data-ttu-id="df85b-113">Azure Otomasyonu DSC getirir aynı yönetim katmanı çok hello[PowerShell istenen durum Yapılandırması](https://msdn.microsoft.com/powershell/dsc/overview) gibi Azure Otomasyonu PowerShell komut dosyası için sunar.</span><span class="sxs-lookup"><span data-stu-id="df85b-113">Azure Automation DSC brings hello same management layer too[PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) as Azure Automation offers for PowerShell scripting.</span></span>

<span data-ttu-id="df85b-114">Hello Azure portal veya PowerShell, tüm, DSC yapılandırmalarını, kaynak ve hedef düğümleri yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df85b-114">From hello Azure portal, or from PowerShell, you can manage all your DSC configurations, resources, and target nodes.</span></span>

![Hello Azure Otomasyonu dikey penceresi ekran görüntüsü](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a><span data-ttu-id="df85b-116">Günlük analizi raporlama verilerini alma</span><span class="sxs-lookup"><span data-stu-id="df85b-116">Import reporting data into Log Analytics</span></span>

<span data-ttu-id="df85b-117">Azure Otomasyonu DSC'ye yönetilen düğümler ayrıntılı raporlama durum veri toohello yerleşik çekme sunucusuna gönderir.</span><span class="sxs-lookup"><span data-stu-id="df85b-117">Nodes that are managed with Azure Automation DSC send detailed reporting status data toohello built-in pull server.</span></span>
<span data-ttu-id="df85b-118">Bu veri tooyour Microsoft Operations Management Suite (OMS) günlük analizi çalışma alanı Azure Otomasyonu DSC toosend yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df85b-118">You can configure Azure Automation DSC toosend this data tooyour Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>
<span data-ttu-id="df85b-119">toosend DSC durum veri tooyour günlük analizi çalışma alanı, nasıl görürüm toolearn [İleri Azure Otomasyonu veri tooOMS günlük analizi raporlama DSC](automation-dsc-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="df85b-119">toolearn how toosend DSC status data tooyour Log Analytics workspace, see [Forward Azure Automation DSC reporting data tooOMS Log Analytics](automation-dsc-diagnostics.md).</span></span>

## <a name="introduction-video"></a><span data-ttu-id="df85b-120">Tanıtım videosu</span><span class="sxs-lookup"><span data-stu-id="df85b-120">Introduction video</span></span>

<span data-ttu-id="df85b-121">Tooreading izlemeyi mi tercih ediyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="df85b-121">Prefer watching tooreading?</span></span> <span data-ttu-id="df85b-122">Mayıs 2015, ne zaman Azure Otomasyonu DSC ilk duyurulan video aşağıdaki hello göz vardır.</span><span class="sxs-lookup"><span data-stu-id="df85b-122">Have a look at hello following video from May 2015, when Azure Automation DSC was first announced.</span></span>

>[!NOTE]
><span data-ttu-id="df85b-123">Merhaba kavramları ve bu videoda ele alınan ömrünü doğru olsa da, bu videonun kaydedilmesinden sonra Azure Otomasyonu DSC değişmiştir.</span><span class="sxs-lookup"><span data-stu-id="df85b-123">While hello concepts and life cycle discussed in this video are correct, Azure Automation DSC has progressed a lot since this video was recorded.</span></span>
><span data-ttu-id="df85b-124">Genel kullanıma sunulmuştur, hello Azure portal çok daha geniş bir kullanıcı Arabirimine sahiptir ve birçok ek özellikleri desteklemektedir.</span><span class="sxs-lookup"><span data-stu-id="df85b-124">It is now generally available, has a much more extensive UI in hello Azure portal, and supports many additional capabilities.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a><span data-ttu-id="df85b-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="df85b-125">Next steps</span></span>

* <span data-ttu-id="df85b-126">Azure Otomasyonu DSC'ye tooonboard düğümleri toobe yönetilen nasıl toolearn bakın [Azure Otomasyonu DSC tarafından Yönetim için hazırlama makineler](automation-dsc-onboarding.md)</span><span class="sxs-lookup"><span data-stu-id="df85b-126">toolearn how tooonboard nodes toobe managed with Azure Automation DSC, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span>
* <span data-ttu-id="df85b-127">Azure Automation DSC kullanmaya tooget bakın [Azure Otomasyonu DSC ile çalışmaya başlama](automation-dsc-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="df85b-127">tooget started using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="df85b-128">toolearn tootarget düğümleri atayabilirsiniz bir DSC yapılandırmaları derleme hakkında bkz [Azure Otomasyonu DSC yapılandırmalarında derleme](automation-dsc-compile.md)</span><span class="sxs-lookup"><span data-stu-id="df85b-128">toolearn about compiling DSC configurations so that you can assign them tootarget nodes, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md)</span></span>
* <span data-ttu-id="df85b-129">Azure Otomasyonu DSC için PowerShell cmdlet başvuru için bkz: [Azure Otomasyonu DSC cmdlet'leri](/powershell/module/azurerm.automation/#automation)</span><span class="sxs-lookup"><span data-stu-id="df85b-129">For PowerShell cmdlet reference for Azure Automation DSC, see [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
* <span data-ttu-id="df85b-130">Fiyatlandırma bilgileri için bkz: [Azure Otomasyonu DSC fiyatlandırma](https://azure.microsoft.com/pricing/details/automation/)</span><span class="sxs-lookup"><span data-stu-id="df85b-130">For pricing information, see [Azure Automation DSC pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
* <span data-ttu-id="df85b-131">toosee sürekli dağıtım ardışık düzeninde, Azure Automation DSC kullanmaya ilişkin bir örnek görmek [sürekli dağıtım tooIaaS VM'ler kullanarak Azure Otomasyonu DSC ve Chocolatey](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="df85b-131">toosee an example of using Azure Automation DSC in a continuous deployment pipeline, see  [Continuous Deployment tooIaaS VMs Using Azure Automation DSC and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>
