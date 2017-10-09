---
title: "Azure Web uygulamasına Azure Automation'ı kullanarak aaaManage | Microsoft Docs"
description: "Kullanılan toomanage Azure Web uygulaması'hello Azure Otomasyon hizmetine nasıl olabilir hakkında bilgi edinin."
services: app-service\web, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: c960a44f-f941-401d-afba-a4bc0f0394eb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte
ms.openlocfilehash: 6d80351a2927f26753cfbaead6e1c0c3c94e86e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-web-app-using-azure-automation"></a><span data-ttu-id="4bad4-103">Azure Web uygulamasına Azure Automation'ı kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="4bad4-103">Managing Azure Web App using Azure Automation</span></span>
<span data-ttu-id="4bad4-104">Bu kılavuz toohello Azure Otomasyon hizmetine ve Azure Web uygulaması kullanılan toosimplify yönetimini nasıl çalıştırılabilir tanıtılacaktır.</span><span class="sxs-lookup"><span data-stu-id="4bad4-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure Web App.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="4bad4-105">Azure Otomasyonu Nedir?</span><span class="sxs-lookup"><span data-stu-id="4bad4-105">What is Azure Automation?</span></span>
<span data-ttu-id="4bad4-106">[Azure Otomasyonu](../automation/automation-intro.md) işlem Otomasyonu aracılığıyla bulut yönetimi basitleştirmek için bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="4bad4-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="4bad4-107">Azure otomasyonu kullanarak, el ile yinelenen, uzun süre çalışan ve hataya yatkın görevleri otomatik tooincrease güvenilirlik, verimliliği ve kuruluşunuz için zaman toovalue olabilir.</span><span class="sxs-lookup"><span data-stu-id="4bad4-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="4bad4-108">Azure Otomasyon gereksinimlerinizi toomeet ölçeklendirir bir yüksek oranda güvenilir ve yüksek oranda kullanılabilir iş akışı yürütme altyapısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="4bad4-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="4bad4-109">Tam olarak gerekli görevleri ortaya böylece Azure Otomasyonu'nda işlemleri el ile 3. taraf sistemleri tarafından veya zamanlanan aralıklarla artırılabilir devre dışı.</span><span class="sxs-lookup"><span data-stu-id="4bad4-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="4bad4-110">İşlem yükünü azaltmak ve boş BT ve DevOps personel toofocus iş değeri, bulut yönetim görevleri toobe taşıyarak ekler iş Azure Automation'ın otomatik olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4bad4-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-web-app"></a><span data-ttu-id="4bad4-111">Azure Otomasyonu Azure Web uygulaması yönetmenize nasıl yardımcı olabilir?</span><span class="sxs-lookup"><span data-stu-id="4bad4-111">How can Azure Automation help manage Azure Web App?</span></span>
<span data-ttu-id="4bad4-112">Web uygulaması yönetilebilir Azure Otomasyonu'nda hello kullanılabilir hello PowerShell cmdlet'lerini kullanarak [Azure PowerShell modülleri](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="4bad4-112">Web App can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell modules](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="4bad4-113">Yapabilecekleriniz [Azure Otomasyonu'nda bu Web uygulaması PowerShell cmdlet'lerini yükleyin](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), böylece tüm Web uygulaması yönetim görevlerinizi hello hizmet içinde gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4bad4-113">You can [install these Web App PowerShell cmdlets in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), so that you can perform all of your Web App management tasks within hello service.</span></span> <span data-ttu-id="4bad4-114">Azure Automation bu cmdlet'leri diğer Azure Hizmetleri tooautomate karmaşık görevleri için hello cmdlet'leri ile Azure hizmeti ve 3. taraf sistemi arasında eşleştirin.</span><span class="sxs-lookup"><span data-stu-id="4bad4-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="4bad4-115">Otomasyon ile uygulama hizmetleri yönetmeye ilişkin bazı örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4bad4-115">Here are some examples of managing App Services with Automation:</span></span>

* [<span data-ttu-id="4bad4-116">Web uygulamaları yönetmek için komutlar</span><span class="sxs-lookup"><span data-stu-id="4bad4-116">Scripts for managing Web Apps</span></span>](https://azure.microsoft.com/documentation/scripts/)

## <a name="next-steps"></a><span data-ttu-id="4bad4-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4bad4-117">Next steps</span></span>
<span data-ttu-id="4bad4-118">Artık Azure Automation ve kullanılan toomanage Azure Web uygulaması nasıl olabilir hello temel bilgileri öğrendiğinize göre bu bağlantıları toolearn Azure Otomasyonu hakkında daha fazla izleyin.</span><span class="sxs-lookup"><span data-stu-id="4bad4-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Web App, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="4bad4-119">Hello Azure Otomasyonu bkz [başlangıç Öğreticisi](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="4bad4-119">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

