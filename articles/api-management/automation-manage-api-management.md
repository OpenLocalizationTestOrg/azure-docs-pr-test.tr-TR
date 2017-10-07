---
title: "aaaManage Azure otomasyonu kullanarak Azure API Yönetimi"
description: "Kullanılan toomanage Azure API Management hello Azure Otomasyon hizmetine nasıl olabilir hakkında bilgi edinin."
services: api-management, automation
documentationcenter: 
author: csand-msft
manager: eamono
editor: 
ms.assetid: 2e53c9af-f738-47f8-b1b6-593050a7c51b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 05b8e3cad786fa701feb88f7b6d9629f16686d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-api-management-using-azure-automation"></a><span data-ttu-id="85cc9-103">Azure otomasyonu kullanarak Azure API Management'te yönetme</span><span class="sxs-lookup"><span data-stu-id="85cc9-103">Managing Azure API Management using Azure Automation</span></span>
<span data-ttu-id="85cc9-104">Bu kılavuz toohello Azure Otomasyon hizmetine ve Azure API Management kullanılan toosimplify yönetimini nasıl çalıştırılabilir tanıtılacaktır.</span><span class="sxs-lookup"><span data-stu-id="85cc9-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure API Management.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="85cc9-105">Azure Otomasyonu Nedir?</span><span class="sxs-lookup"><span data-stu-id="85cc9-105">What is Azure Automation?</span></span>
<span data-ttu-id="85cc9-106">[Azure Otomasyonu](https://azure.microsoft.com/services/automation/) işlem Otomasyonu aracılığıyla bulut yönetimi basitleştirmek için bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="85cc9-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="85cc9-107">Azure otomasyonu kullanarak, el ile yinelenen, uzun süre çalışan ve hataya yatkın görevleri otomatik tooincrease güvenilirlik, verimliliği ve kuruluşunuz için zaman toovalue olabilir.</span><span class="sxs-lookup"><span data-stu-id="85cc9-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="85cc9-108">Azure Otomasyon gereksinimlerinizi toomeet ölçeklendirir bir yüksek oranda güvenilir ve yüksek oranda kullanılabilir iş akışı yürütme altyapısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="85cc9-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="85cc9-109">Tam olarak gerekli görevleri ortaya böylece Azure Otomasyonu'nda işlemleri el ile 3. taraf sistemleri tarafından veya zamanlanan aralıklarla artırılabilir devre dışı.</span><span class="sxs-lookup"><span data-stu-id="85cc9-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="85cc9-110">İşlem yükünü azaltmak ve boş BT ve DevOps personel toofocus iş değeri, bulut yönetim görevleri toobe taşıyarak ekler iş Azure Automation'ın otomatik olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="85cc9-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-api-management"></a><span data-ttu-id="85cc9-111">Azure Otomasyonu Azure API Management yönetmenize nasıl yardımcı olabilir?</span><span class="sxs-lookup"><span data-stu-id="85cc9-111">How can Azure Automation help manage Azure API Management?</span></span>
<span data-ttu-id="85cc9-112">API Management yönetilebilir Azure Otomasyonu'nda hello kullanarak [Azure API Yönetimi API için Windows PowerShell cmdlet'leri](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span><span class="sxs-lookup"><span data-stu-id="85cc9-112">API Management can be managed in Azure Automation by using hello [Windows PowerShell cmdlets for Azure API Management API](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span></span> <span data-ttu-id="85cc9-113">Azure Otomasyonu içinde PowerShell iş akışı komut dosyaları tooperform hello cmdlet'leri kullanarak API Management görevlerinizi çoğunu yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85cc9-113">Within Azure Automation you can write PowerShell workflow scripts tooperform many of your API Management tasks using hello cmdlets.</span></span> <span data-ttu-id="85cc9-114">Azure Automation bu cmdlet'leri diğer Azure Hizmetleri, tooautomate karmaşık görevleri için hello cmdlet'leri ile Azure hizmeti ve 3. taraf sistemi arasında eşleştirin.</span><span class="sxs-lookup"><span data-stu-id="85cc9-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="85cc9-115">API Management ile otomasyon kullanma bazı örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="85cc9-115">Here are some examples of using API Management with Automation:</span></span>

* [<span data-ttu-id="85cc9-116">Azure API Management – yedekleme ve geri yükleme için PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="85cc9-116">Azure API Management – Using PowerShell for backup and restore</span></span>](https://blogs.msdn.microsoft.com/katriend/2015/10/02/azure-api-management-using-powershell-for-backup-and-restore/)

## <a name="next-steps"></a><span data-ttu-id="85cc9-117">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="85cc9-117">Next Steps</span></span>
<span data-ttu-id="85cc9-118">Azure Otomasyonu ve kullanılan toomanage Azure API Management nasıl olabilir hello temel bilgileri öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="85cc9-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure API Management, follow these links toolearn more.</span></span>

* <span data-ttu-id="85cc9-119">Hello Azure Otomasyonu bkz [başlama Öğreticisi](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="85cc9-119">See hello Azure Automation [getting started tutorial](../automation/automation-first-runbook-graphical.md).</span></span>

