---
title: "Azure otomasyonu kullanarak sanal makineleri yönetme | Microsoft Docs"
description: "Nasıl Azure Otomasyon hizmetine ölçekte Azure sanal makineleri yönetmek için kullanılabilir hakkında bilgi edinin."
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
ms.openlocfilehash: 15653c5d653ae538bdb66eaf0daee12c35858b45
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-virtual-machines-using-azure-automation"></a><span data-ttu-id="20891-103">Azure Otomasyonu’nu kullanarak Azure Sanal Makineler’i yönetme</span><span class="sxs-lookup"><span data-stu-id="20891-103">Managing Azure Virtual Machines using Azure Automation</span></span>
<span data-ttu-id="20891-104">Bu kılavuz size Azure Otomasyon hizmetine ve nasıl bu Azure sanal makinelerinizi yönetimini kolaylaştırmak için kullanılabilir tanıtır.</span><span class="sxs-lookup"><span data-stu-id="20891-104">This guide introduces you to the Azure Automation service and how it can be used to simplify managing your Azure virtual machines.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="20891-105">Azure Otomasyonu Nedir?</span><span class="sxs-lookup"><span data-stu-id="20891-105">What is Azure Automation?</span></span>
<span data-ttu-id="20891-106">[Azure Otomasyonu](https://azure.microsoft.com/services/automation/) işlem Otomasyonu aracılığıyla bulut yönetimi basitleştirmek için bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="20891-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="20891-107">Azure otomasyonu kullanarak, uzun süre çalışan, el ile hatasız ve sık tekrarlanan görevleri güvenilirlik, verimliliği ve zaman değeri, kuruluşunuz için artırmak için otomatik olarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="20891-107">By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time-to-value for your organization.</span></span>

<span data-ttu-id="20891-108">Azure Otomasyonu, kuruluşunuz büyüdükçe gereksinimlerinizi karşılayacak şekilde ölçekler bir yüksek oranda güvenilir ve yüksek oranda kullanılabilir iş akışı yürütme altyapısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="20891-108">Azure Automation provides a highly reliable and highly available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="20891-109">Tam olarak gerekli görevleri ortaya böylece Azure Otomasyonu'nda işlemleri el ile üçüncü taraf sistemleri tarafından veya zamanlanan aralıklarla artırılabilir devre dışı.</span><span class="sxs-lookup"><span data-stu-id="20891-109">In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="20891-110">Alt işlem yükünü ve boş BT ve iş değeri, bulut yönetim görevleri otomatik olarak Azure Automation ile çalıştırarak ekler iş odaklanmak için DevOps personeli.</span><span class="sxs-lookup"><span data-stu-id="20891-110">You can lower operational overhead and free up IT and DevOps staff to focus on work that adds business value by running your cloud management tasks automatically with Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a><span data-ttu-id="20891-111">Azure Otomasyonu Azure sanal makineleri yönetmenize nasıl yardımcı olabilir?</span><span class="sxs-lookup"><span data-stu-id="20891-111">How can Azure Automation help manage Azure virtual machines?</span></span>
<span data-ttu-id="20891-112">Sanal makineler yönetilen Azure Otomasyonu'nda kullanarak [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="20891-112">Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="20891-113">Tüm hizmet içinde sanal makine yönetim görevlerinizi gerçekleştirmek için azure Otomasyonu Azure PowerShell cmdlet'lerini içerir.</span><span class="sxs-lookup"><span data-stu-id="20891-113">Azure Automation includes the Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within the service.</span></span> <span data-ttu-id="20891-114">Ayrıca Azure Automation cmdlet'leri Azure hizmetlerinin ve üçüncü taraf sistemlerde karmaşık görevleri otomatikleştirmek için diğer Azure Hizmetleri için cmdlet'leri ile eşleştirin.</span><span class="sxs-lookup"><span data-stu-id="20891-114">You can also pair the cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and third-party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20891-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="20891-115">Next steps</span></span>
<span data-ttu-id="20891-116">Azure Otomasyonu ve nasıl Azure sanal makineleri yönetmek için kullanılmadan öğrendiğinize göre daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="20891-116">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure virtual machines, learn more:</span></span>

* [<span data-ttu-id="20891-117">Azure Otomasyonu genel bakış</span><span class="sxs-lookup"><span data-stu-id="20891-117">Azure Automation Overview</span></span>](../../automation/automation-intro.md)
* [<span data-ttu-id="20891-118">İlk runbook’um</span><span class="sxs-lookup"><span data-stu-id="20891-118">My first runbook</span></span>](../../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="20891-119">Azure Otomasyonu öğrenme Haritası</span><span class="sxs-lookup"><span data-stu-id="20891-119">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)

