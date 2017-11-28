---
title: Azure otomasyonu kullanarak Azure Cloud Services aaaManage | Microsoft Docs
description: "Hello Azure Otomasyon hizmetine ölçekte kullanılan toomanage Azure bulut hizmetlerine nasıl olabilir hakkında bilgi edinin."
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
ms.openlocfilehash: 8e920fb94955466bfec71cc332444f5f0ee497a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a><span data-ttu-id="4bacd-103">Azure otomasyonu kullanarak Azure Cloud Services yönetme</span><span class="sxs-lookup"><span data-stu-id="4bacd-103">Managing Azure Cloud Services using Azure Automation</span></span>
<span data-ttu-id="4bacd-104">Bu kılavuz toohello Azure Otomasyon hizmetine ve Azure bulut hizmetlerinizi kullanılan toosimplify yönetimini nasıl çalıştırılabilir tanıtılacaktır.</span><span class="sxs-lookup"><span data-stu-id="4bacd-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure cloud services.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="4bacd-105">Azure Otomasyonu Nedir?</span><span class="sxs-lookup"><span data-stu-id="4bacd-105">What is Azure Automation?</span></span>
<span data-ttu-id="4bacd-106">[Azure Otomasyonu](https://azure.microsoft.com/services/automation/) işlem Otomasyonu aracılığıyla bulut yönetimi basitleştirmek için bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="4bacd-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="4bacd-107">Azure otomasyonu kullanarak, uzun süre çalışan, el ile hatasız ve sık tekrarlanan görevleri otomatik tooincrease güvenilirlik, verimliliği ve kuruluşunuz için zaman toovalue olabilir.</span><span class="sxs-lookup"><span data-stu-id="4bacd-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="4bacd-108">Azure Otomasyonu, kuruluşunuz büyüdükçe gereksinimlerinizi toomeet ölçeklendirilebilen bir yüksek oranda güvenilir ve yüksek oranda kullanılabilir iş akışı yürütme altyapısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="4bacd-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="4bacd-109">Tam olarak gerekli görevleri ortaya böylece Azure Otomasyonu'nda işlemleri el ile 3. taraf sistemleri tarafından veya zamanlanan aralıklarla artırılabilir devre dışı.</span><span class="sxs-lookup"><span data-stu-id="4bacd-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="4bacd-110">İşletimsel ek yükü azaltmak ve boşaltmak BT / DevOps personel toofocus iş değeri, bulut yönetim görevleri toobe taşıyarak ekler iş Azure Automation'ın otomatik olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4bacd-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a><span data-ttu-id="4bacd-111">Azure Otomasyonu Azure bulut hizmetlerini yönetmenize nasıl yardımcı olabilir?</span><span class="sxs-lookup"><span data-stu-id="4bacd-111">How can Azure Automation help manage Azure cloud services?</span></span>
<span data-ttu-id="4bacd-112">Azure bulut hizmetlerine yönetilebilir Azure Otomasyonu'nda hello kullanılabilir hello PowerShell cmdlet'lerini kullanarak [Azure PowerShell Araçları](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="4bacd-112">Azure cloud services can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="4bacd-113">Böylece tüm bulut Hizmeti Yönetim görevlerinizi hello hizmet içinde gerçekleştirebilirsiniz azure Otomasyonu hello kutudan çıktığında, bu bulut hizmeti PowerShell cmdlet'leri kullanılabilir sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4bacd-113">Azure Automation has these cloud service PowerShell cmdlets available out of hello box, so that you can perform all of your cloud service management tasks within hello service.</span></span> <span data-ttu-id="4bacd-114">Azure Automation bu cmdlet'leri diğer Azure Hizmetleri, tooautomate karmaşık görevleri için hello cmdlet'leri ile Azure hizmeti ve 3. taraf sistemi arasında eşleştirin.</span><span class="sxs-lookup"><span data-stu-id="4bacd-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="4bacd-115">Bazı örnek Azure Cloud Services dahil Azure Otomasyonu toomanage kullanır:</span><span class="sxs-lookup"><span data-stu-id="4bacd-115">Some example uses of Azure Automation toomanage Azure Cloud Services include:</span></span>

* [<span data-ttu-id="4bacd-116">Bir bulut cscfg veya cspkg Azure Blob depolama alanına güncelleştirildiğinde hizmetin sürekli dağıtımı</span><span class="sxs-lookup"><span data-stu-id="4bacd-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [<span data-ttu-id="4bacd-117">Bulut hizmeti örnekleri paralel, bir seferde bir yükseltme etki alanı yeniden başlatılıyor</span><span class="sxs-lookup"><span data-stu-id="4bacd-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a><span data-ttu-id="4bacd-118">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="4bacd-118">Next Steps</span></span>
<span data-ttu-id="4bacd-119">Azure Otomasyonu ve nasıl kullanılan toomanage Azure bulut Hizmetleri olabilir hello temel bilgileri öğrendiğinize göre bu bağlantıları toolearn Azure Otomasyonu hakkında daha fazla izleyin.</span><span class="sxs-lookup"><span data-stu-id="4bacd-119">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure cloud services, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="4bacd-120">Azure Otomasyonu genel bakış</span><span class="sxs-lookup"><span data-stu-id="4bacd-120">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="4bacd-121">İlk runbook’um</span><span class="sxs-lookup"><span data-stu-id="4bacd-121">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="4bacd-122">Azure Otomasyonu öğrenme Haritası</span><span class="sxs-lookup"><span data-stu-id="4bacd-122">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
