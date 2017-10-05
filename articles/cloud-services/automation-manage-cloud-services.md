---
title: "Azure otomasyonu kullanarak Azure Cloud Services yönetme | Microsoft Docs"
description: "Nasıl Azure Otomasyon hizmetine ölçekte Azure bulut hizmetlerini yönetmek için kullanılabilir hakkında bilgi edinin."
services: cloud-services, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: 3789810a-2892-4eef-bf29-c781c1b5af48
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2016
ms.author: timlt
ms.openlocfilehash: 6b5acac1b8647c324988c316cd5602b3dba98a1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a><span data-ttu-id="8e902-103">Azure otomasyonu kullanarak Azure Cloud Services yönetme</span><span class="sxs-lookup"><span data-stu-id="8e902-103">Managing Azure Cloud Services using Azure Automation</span></span>
<span data-ttu-id="8e902-104">Bu kılavuz Azure Otomasyon hizmetine ve nasıl Azure bulut hizmetlerinizi yönetimini basitleştirmek için kullanılabilmesi için tanıtılacaktır.</span><span class="sxs-lookup"><span data-stu-id="8e902-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure cloud services.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="8e902-105">Azure Otomasyonu Nedir?</span><span class="sxs-lookup"><span data-stu-id="8e902-105">What is Azure Automation?</span></span>
<span data-ttu-id="8e902-106">[Azure Otomasyonu](https://azure.microsoft.com/services/automation/) işlem Otomasyonu aracılığıyla bulut yönetimi basitleştirmek için bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="8e902-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="8e902-107">Azure otomasyonu kullanarak, uzun süre çalışan, el ile hatasız ve sık tekrarlanan görevleri güvenilirlik, verimliliği ve kuruluşunuz için değer süre artırmak için otomatik olarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="8e902-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="8e902-108">Azure Otomasyonu, kuruluşunuz büyüdükçe gereksinimlerinizi karşılayacak şekilde ölçekler bir yüksek oranda güvenilir ve yüksek oranda kullanılabilir iş akışı yürütme altyapısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="8e902-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="8e902-109">Tam olarak gerekli görevleri ortaya böylece Azure Otomasyonu'nda işlemleri el ile 3. taraf sistemleri tarafından veya zamanlanan aralıklarla artırılabilir devre dışı.</span><span class="sxs-lookup"><span data-stu-id="8e902-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="8e902-110">İşletimsel ek yükü azaltmak ve boşaltmak BT / iş ekler çalışmaları odaklanmaya DevOps personel değer Azure Automation'ın otomatik olarak çalıştırılmak üzere bulut yönetim görevlerinizi taşıyarak.</span><span class="sxs-lookup"><span data-stu-id="8e902-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a><span data-ttu-id="8e902-111">Azure Otomasyonu Azure bulut hizmetlerini yönetmenize nasıl yardımcı olabilir?</span><span class="sxs-lookup"><span data-stu-id="8e902-111">How can Azure Automation help manage Azure cloud services?</span></span>
<span data-ttu-id="8e902-112">Azure bulut hizmetlerine yönetilebilir Azure Otomasyonu'nda kullanılabilir PowerShell cmdlet'lerini kullanarak [Azure PowerShell Araçları](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="8e902-112">Azure cloud services can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="8e902-113">Böylece tüm hizmet içinde bulut Hizmeti Yönetim görevlerinizi gerçekleştirmek azure Otomasyonu kutudan çıktığında, bu bulut hizmeti PowerShell cmdlet'leri kullanılabilir olur.</span><span class="sxs-lookup"><span data-stu-id="8e902-113">Azure Automation has these cloud service PowerShell cmdlets available out of the box, so that you can perform all of your cloud service management tasks within the service.</span></span> <span data-ttu-id="8e902-114">Ayrıca Azure Automation bu cmdlet'leri Azure hizmeti ve 3. taraf sistemi arasında karmaşık görevleri otomatikleştirmek için diğer Azure Hizmetleri için cmdlet'leri ile eşleştirin.</span><span class="sxs-lookup"><span data-stu-id="8e902-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="8e902-115">Azure Otomasyonu, Azure bulut hizmetlerini yönetmek için bazı örnek kullanımları şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="8e902-115">Some example uses of Azure Automation to manage Azure Cloud Services include:</span></span>

* [<span data-ttu-id="8e902-116">Bir bulut cscfg veya cspkg Azure Blob depolama alanına güncelleştirildiğinde hizmetin sürekli dağıtımı</span><span class="sxs-lookup"><span data-stu-id="8e902-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [<span data-ttu-id="8e902-117">Bulut hizmeti örnekleri paralel, bir seferde bir yükseltme etki alanı yeniden başlatılıyor</span><span class="sxs-lookup"><span data-stu-id="8e902-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a><span data-ttu-id="8e902-118">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="8e902-118">Next Steps</span></span>
<span data-ttu-id="8e902-119">Azure Otomasyonu ve nasıl Azure bulut hizmetlerini yönetmek için kullanılmadan öğrendiğinize göre Azure Otomasyonu hakkında daha fazla bilgi edinmek için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="8e902-119">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure cloud services, follow these links to learn more about Azure Automation.</span></span>

* [<span data-ttu-id="8e902-120">Azure Otomasyonu genel bakış</span><span class="sxs-lookup"><span data-stu-id="8e902-120">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="8e902-121">İlk runbook’um</span><span class="sxs-lookup"><span data-stu-id="8e902-121">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="8e902-122">Azure Otomasyonu öğrenme Haritası</span><span class="sxs-lookup"><span data-stu-id="8e902-122">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
