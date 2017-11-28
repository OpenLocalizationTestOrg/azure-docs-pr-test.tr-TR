---
title: "Azure RemoteApp kullanarak Azure Otomasyonu'nu yönetme | Microsoft Docs"
description: "Nasıl Azure Otomasyon hizmetine Azure RemoteApp yönetmek için kullanılabilir hakkında bilgi edinin."
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
ms.openlocfilehash: 59ac11f153c0bd74a1106400dbbf5790968b657c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-remoteapp-using-azure-automation"></a><span data-ttu-id="2c7db-103">Azure RemoteApp kullanarak Azure Otomasyonu'nu yönetme</span><span class="sxs-lookup"><span data-stu-id="2c7db-103">Managing Azure RemoteApp using Azure Automation</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2c7db-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="2c7db-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="2c7db-105">Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.</span><span class="sxs-lookup"><span data-stu-id="2c7db-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="2c7db-106">Bu kılavuz Azure Otomasyon hizmetine ve nasıl Azure RemoteApp yönetimini basitleştirmek için kullanılabilmesi için tanıtılacaktır.</span><span class="sxs-lookup"><span data-stu-id="2c7db-106">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of Azure RemoteApp.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="2c7db-107">Azure Otomasyonu Nedir?</span><span class="sxs-lookup"><span data-stu-id="2c7db-107">What is Azure Automation?</span></span>
<span data-ttu-id="2c7db-108">[Azure Otomasyonu](../automation/automation-intro.md) işlem Otomasyonu aracılığıyla bulut yönetimi basitleştirmek için bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="2c7db-108">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="2c7db-109">Azure otomasyonu kullanarak, el ile sık tekrarlanan, uzun süre çalışan ve hataya yatkın görevleri güvenilirlik, verimliliği ve kuruluşunuz için değer süre artırmak için otomatik olarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="2c7db-109">Using Azure Automation, manual, frequently-repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="2c7db-110">Azure Otomasyon gereksinimlerinizi karşılayacak şekilde ölçekler bir yüksek oranda güvenilir ve yüksek oranda kullanılabilir iş akışı yürütme altyapısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="2c7db-110">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="2c7db-111">Tam olarak gerekli görevleri ortaya böylece Azure Otomasyonu'nda işlemleri el ile 3. taraf sistemleri tarafından veya zamanlanan aralıklarla artırılabilir devre dışı.</span><span class="sxs-lookup"><span data-stu-id="2c7db-111">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="2c7db-112">İşlem yükünü azaltmak ve boş BT ve iş değeri Azure Automation'ın otomatik olarak çalıştırılmak üzere bulut yönetim görevlerinizi taşıyarak ekler iş odaklanmak için DevOps personeli.</span><span class="sxs-lookup"><span data-stu-id="2c7db-112">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-remoteapp"></a><span data-ttu-id="2c7db-113">Azure Otomasyonu Azure RemoteApp yönetmenize nasıl yardımcı olabilir?</span><span class="sxs-lookup"><span data-stu-id="2c7db-113">How can Azure Automation help manage Azure RemoteApp?</span></span>
<span data-ttu-id="2c7db-114">RemoteApp yönetilebilir Azure Otomasyonu'nda kullanılabilir PowerShell cmdlet'lerini kullanarak [Azure PowerShell Araçları](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c7db-114">RemoteApp can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="2c7db-115">Böylece tüm RemoteApp yönetim görevlerinizi hizmet içinde gerçekleştirebilirsiniz azure Otomasyonu kutudan çıktığında, bu RemoteApp PowerShell cmdlet'leri vardır.</span><span class="sxs-lookup"><span data-stu-id="2c7db-115">Azure Automation has these RemoteApp PowerShell cmdlets available out of the box, so that you can perform all of your RemoteApp management tasks within the service.</span></span> <span data-ttu-id="2c7db-116">Ayrıca Azure Automation bu cmdlet'leri Azure hizmeti ve 3. taraf sistemi arasında karmaşık görevleri otomatikleştirmek için diğer Azure Hizmetleri için cmdlet'leri ile eşleştirin.</span><span class="sxs-lookup"><span data-stu-id="2c7db-116">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c7db-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2c7db-117">Next steps</span></span>
<span data-ttu-id="2c7db-118">Azure Otomasyonu ve nasıl Azure RemoteApp yönetmek için kullanılmadan öğrendiğinize göre Azure Otomasyonu hakkında daha fazla bilgi edinmek için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="2c7db-118">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure RemoteApp, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="2c7db-119">Azure Otomasyonu bkz [başlama Öğreticisi](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="2c7db-119">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

