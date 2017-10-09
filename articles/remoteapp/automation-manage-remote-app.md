---
title: Azure RemoteApp kullanarak Azure Otomasyonu'nu aaaManage | Microsoft Docs
description: "Kullanılan toomanage Azure RemoteApp hello Azure Otomasyon hizmetine nasıl olabilir hakkında bilgi edinin."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 589f01ef-f9c1-4e7b-a040-1b46862d3544
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: magoedte;csand
ms.openlocfilehash: a4cb23e292c797256e971acb3b363b025f140f16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-remoteapp-using-azure-automation"></a><span data-ttu-id="902c3-103">Azure RemoteApp kullanarak Azure Otomasyonu'nu yönetme</span><span class="sxs-lookup"><span data-stu-id="902c3-103">Managing Azure RemoteApp using Azure Automation</span></span>
> [!IMPORTANT]
> <span data-ttu-id="902c3-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="902c3-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="902c3-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="902c3-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="902c3-106">Bu kılavuz toohello Azure Otomasyon hizmetine ve Azure RemoteApp kullanılan toosimplify yönetimini nasıl çalıştırılabilir tanıtılacaktır.</span><span class="sxs-lookup"><span data-stu-id="902c3-106">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure RemoteApp.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="902c3-107">Azure Otomasyonu Nedir?</span><span class="sxs-lookup"><span data-stu-id="902c3-107">What is Azure Automation?</span></span>
<span data-ttu-id="902c3-108">[Azure Otomasyonu](../automation/automation-intro.md) işlem Otomasyonu aracılığıyla bulut yönetimi basitleştirmek için bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="902c3-108">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="902c3-109">Azure otomasyonu kullanarak, el ile sık tekrarlanan, uzun süre çalışan ve hataya yatkın görevleri otomatik tooincrease güvenilirlik, verimliliği ve kuruluşunuz için zaman toovalue olabilir.</span><span class="sxs-lookup"><span data-stu-id="902c3-109">Using Azure Automation, manual, frequently-repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="902c3-110">Azure Otomasyon gereksinimlerinizi toomeet ölçeklendirir bir yüksek oranda güvenilir ve yüksek oranda kullanılabilir iş akışı yürütme altyapısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="902c3-110">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="902c3-111">Tam olarak gerekli görevleri ortaya böylece Azure Otomasyonu'nda işlemleri el ile 3. taraf sistemleri tarafından veya zamanlanan aralıklarla artırılabilir devre dışı.</span><span class="sxs-lookup"><span data-stu-id="902c3-111">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="902c3-112">İşlem yükünü azaltmak ve boş BT ve DevOps personel toofocus iş değeri, bulut yönetim görevleri toobe taşıyarak ekler iş Azure Automation'ın otomatik olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="902c3-112">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-remoteapp"></a><span data-ttu-id="902c3-113">Azure Otomasyonu Azure RemoteApp yönetmenize nasıl yardımcı olabilir?</span><span class="sxs-lookup"><span data-stu-id="902c3-113">How can Azure Automation help manage Azure RemoteApp?</span></span>
<span data-ttu-id="902c3-114">RemoteApp yönetilebilir Azure Otomasyonu'nda hello kullanılabilir hello PowerShell cmdlet'lerini kullanarak [Azure PowerShell Araçları](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="902c3-114">RemoteApp can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="902c3-115">Böylece tüm RemoteApp yönetim görevlerinizi hello hizmet içinde gerçekleştirebilirsiniz azure Otomasyonu hello kutudan çıktığında, bu RemoteApp PowerShell cmdlet'leri vardır.</span><span class="sxs-lookup"><span data-stu-id="902c3-115">Azure Automation has these RemoteApp PowerShell cmdlets available out of hello box, so that you can perform all of your RemoteApp management tasks within hello service.</span></span> <span data-ttu-id="902c3-116">Azure Automation bu cmdlet'leri diğer Azure Hizmetleri, tooautomate karmaşık görevleri için hello cmdlet'leri ile Azure hizmeti ve 3. taraf sistemi arasında eşleştirin.</span><span class="sxs-lookup"><span data-stu-id="902c3-116">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="902c3-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="902c3-117">Next steps</span></span>
<span data-ttu-id="902c3-118">Artık Azure Automation ve kullanılan toomanage Azure RemoteApp nasıl olabilir hello temel bilgileri öğrendiğinize göre bu bağlantıları toolearn Azure Otomasyonu hakkında daha fazla izleyin.</span><span class="sxs-lookup"><span data-stu-id="902c3-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure RemoteApp, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="902c3-119">Hello Azure Otomasyonu bkz [başlangıç Öğreticisi](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="902c3-119">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

