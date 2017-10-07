---
title: Azure otomasyonu kullanarak VM'ler aaaManage | Microsoft Docs
description: "Kullanılan toomanage hello Azure Otomasyon hizmetine nasıl gerçekleştirilebildiği hakkında ölçekte Azure sanal makineler hakkında bilgi edinin."
services: virtual-machines-windows, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: ce49f83a-f409-42ee-af74-a8ea2caa9ae8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2016
ms.author: timlt
ms.openlocfilehash: bfe7b3a51b6e82bd7cd5b0a83df7226476ed4f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-virtual-machines-using-azure-automation"></a><span data-ttu-id="55610-103">Azure Otomasyonu’nu kullanarak Azure Sanal Makineler’i yönetme</span><span class="sxs-lookup"><span data-stu-id="55610-103">Managing Azure Virtual Machines using Azure Automation</span></span>
<span data-ttu-id="55610-104">Bu kılavuz toohello Azure Otomasyon hizmetine ve nasıl kullanılacağını tanıtır toosimplify Azure sanal makinelerinizi yönetme.</span><span class="sxs-lookup"><span data-stu-id="55610-104">This guide introduces you toohello Azure Automation service and how it can be used toosimplify managing your Azure virtual machines.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="55610-105">Azure Otomasyonu Nedir?</span><span class="sxs-lookup"><span data-stu-id="55610-105">What is Azure Automation?</span></span>
<span data-ttu-id="55610-106">[Azure Otomasyonu](https://azure.microsoft.com/services/automation/) işlem Otomasyonu aracılığıyla bulut yönetimi basitleştirmek için bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="55610-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="55610-107">Azure otomasyonu kullanarak, uzun süre çalışan, el ile hatasız ve sık tekrarlanan görevleri otomatik tooincrease güvenilirlik, verimliliği ve zaman değeri, kuruluşunuz için olabilir.</span><span class="sxs-lookup"><span data-stu-id="55610-107">By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time-to-value for your organization.</span></span>

<span data-ttu-id="55610-108">Azure Otomasyonu, kuruluşunuz büyüdükçe gereksinimlerinizi toomeet ölçeklendirilebilen bir yüksek oranda güvenilir ve yüksek oranda kullanılabilir iş akışı yürütme altyapısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="55610-108">Azure Automation provides a highly reliable and highly available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="55610-109">Tam olarak gerekli görevleri ortaya böylece Azure Otomasyonu'nda işlemleri el ile üçüncü taraf sistemleri tarafından veya zamanlanan aralıklarla artırılabilir devre dışı.</span><span class="sxs-lookup"><span data-stu-id="55610-109">In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="55610-110">Alt işlem yükünü ve boş BT ve DevOps iş değeri, bulut yönetim görevleri otomatik olarak Azure Automation ile çalıştırarak ekler iş toofocus personel.</span><span class="sxs-lookup"><span data-stu-id="55610-110">You can lower operational overhead and free up IT and DevOps staff toofocus on work that adds business value by running your cloud management tasks automatically with Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a><span data-ttu-id="55610-111">Azure Otomasyonu Azure sanal makineleri yönetmenize nasıl yardımcı olabilir?</span><span class="sxs-lookup"><span data-stu-id="55610-111">How can Azure Automation help manage Azure virtual machines?</span></span>
<span data-ttu-id="55610-112">Sanal makineler yönetilen Azure Otomasyonu'nda kullanarak [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="55610-112">Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="55610-113">Tüm sanal makine yönetim görevlerinizi hello hizmet içinde gerçekleştirebilmek için azure Otomasyonu hello Azure PowerShell cmdlet'lerini içerir.</span><span class="sxs-lookup"><span data-stu-id="55610-113">Azure Automation includes hello Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within hello service.</span></span> <span data-ttu-id="55610-114">Diğer Azure Hizmetleri, tooautomate karmaşık görevleri için hello cmdlet'leri hello cmdlet'leriyle Azure automation'da Azure hizmetlerinin ve üçüncü taraf sistemlerde eşleştirin.</span><span class="sxs-lookup"><span data-stu-id="55610-114">You can also pair hello cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and third-party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55610-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="55610-115">Next steps</span></span>
<span data-ttu-id="55610-116">Merhaba öğrendiğinize göre Azure Automation ve kullanılan toomanage nasıl olabilir Azure sanal makineler, daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="55610-116">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure virtual machines, learn more:</span></span>

* [<span data-ttu-id="55610-117">Azure Otomasyonu genel bakış</span><span class="sxs-lookup"><span data-stu-id="55610-117">Azure Automation Overview</span></span>](../../automation/automation-intro.md)
* [<span data-ttu-id="55610-118">İlk runbook’um</span><span class="sxs-lookup"><span data-stu-id="55610-118">My first runbook</span></span>](../../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="55610-119">Azure Otomasyonu öğrenme Haritası</span><span class="sxs-lookup"><span data-stu-id="55610-119">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)

