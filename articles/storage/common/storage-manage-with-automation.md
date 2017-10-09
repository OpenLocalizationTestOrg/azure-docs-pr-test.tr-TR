---
title: aaaManage Azure depolama Azure otomasyon kullanma
description: "Hello Azure Otomasyon hizmetine ölçekte kullanılan toomanage Azure Storage nasıl olabilir hakkında bilgi edinin."
services: storage, automation
documentationcenter: 
author: jodoglevy
manager: eamono
editor: 
ms.assetid: bac41c39-1d95-46aa-a481-ec17bbb21b40
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: eamono
ms.openlocfilehash: 5edfba1a9ce1f9c81b5bd0889de19099f3d86fc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a><span data-ttu-id="766b8-103">Azure Storage Azure otomasyonu kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="766b8-103">Managing Azure Storage using Azure Automation</span></span>
<span data-ttu-id="766b8-104">Bu kılavuz toohello Azure Otomasyon hizmetine ve Azure Storage BLOB'lar, tablolar ve Kuyruklar kullanılan toosimplify yönetimini nasıl çalıştırılabilir tanıtılacaktır.</span><span class="sxs-lookup"><span data-stu-id="766b8-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure Storage blobs, tables, and queues.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="766b8-105">Azure Otomasyonu Nedir?</span><span class="sxs-lookup"><span data-stu-id="766b8-105">What is Azure Automation?</span></span>
<span data-ttu-id="766b8-106">[Azure Otomasyonu](https://azure.microsoft.com/services/automation/) işlem Otomasyonu aracılığıyla bulut yönetimi basitleştirmek için bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="766b8-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="766b8-107">Azure otomasyonu kullanarak, uzun süre çalışan, el ile hatasız ve sık görevleri otomatik tooincrease güvenilirlik ve verimliliği ve kuruluşunuz için zaman toovalue azaltmak yinelenir.</span><span class="sxs-lookup"><span data-stu-id="766b8-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability and efficiency, and reduce time toovalue for your organization.</span></span>

<span data-ttu-id="766b8-108">Azure Otomasyonu, kuruluşunuz büyüdükçe gereksinimlerinizi toomeet ölçeklendirilebilen bir yüksek oranda güvenilir ve yüksek oranda kullanılabilir iş akışı yürütme altyapısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="766b8-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="766b8-109">Tam olarak gerekli görevleri ortaya böylece Azure Otomasyonu'nda işlemleri el ile 3. taraf sistemleri tarafından veya zamanlanan aralıklarla artırılabilir devre dışı.</span><span class="sxs-lookup"><span data-stu-id="766b8-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="766b8-110">İşletimsel ek yükü azaltmak ve boşaltmak BT / DevOps personel toofocus iş değeri, bulut yönetim görevleri toobe taşıyarak ekler iş Azure Automation'ın otomatik olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="766b8-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-storage"></a><span data-ttu-id="766b8-111">Azure Otomasyonu Azure Storage yönetmenize nasıl yardımcı olabilir?</span><span class="sxs-lookup"><span data-stu-id="766b8-111">How can Azure Automation help manage Azure Storage?</span></span>
<span data-ttu-id="766b8-112">Azure depolama yönetilebilir Azure Otomasyonu'nda kullanılabilir hello PowerShell cmdlet'lerini kullanarak [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="766b8-112">Azure Storage can be managed in Azure Automation by using hello PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="766b8-113">Böylece tüm blob, tablo ve hello hizmet içinde sıra yönetim görevleri gerçekleştirebilir azure Otomasyonu hello kutudan çıktığında, bu depolama PowerShell cmdlet'leri vardır.</span><span class="sxs-lookup"><span data-stu-id="766b8-113">Azure Automation has these Storage PowerShell cmdlets available out of hello box, so that you can perform all of your blob, table, and queue management tasks within hello service.</span></span> <span data-ttu-id="766b8-114">Azure Automation bu cmdlet'leri diğer Azure Hizmetleri, tooautomate karmaşık görevleri için hello cmdlet'leri ile Azure hizmeti ve 3. taraf sistemi arasında eşleştirin.</span><span class="sxs-lookup"><span data-stu-id="766b8-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="766b8-115">Merhaba [Azure Otomasyonu runbook Galerisi](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) Azure Storage diğer Azure Hizmetleri ve 3. taraf sistemi yönetimi otomatikleştirme başlatılan ürün ekibi ve topluluk runbook'lar tooget çeşitli içerir.</span><span class="sxs-lookup"><span data-stu-id="766b8-115">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure Storage, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="766b8-116">Galeri runbook'ları şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="766b8-116">Gallery runbooks include:</span></span>

* [<span data-ttu-id="766b8-117">Azure Storage Bloblarında'de, belirli gün eski kullanarak otomasyon hizmet Kaldır</span><span class="sxs-lookup"><span data-stu-id="766b8-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [<span data-ttu-id="766b8-118">Azure depolama biriminden bir Blob indirin</span><span class="sxs-lookup"><span data-stu-id="766b8-118">Download a Blob from Azure Storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [<span data-ttu-id="766b8-119">Bir bulut hizmetindeki tüm sanal makineleri veya tek bir Azure VM için tüm diskleri yedekleme</span><span class="sxs-lookup"><span data-stu-id="766b8-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a><span data-ttu-id="766b8-120">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="766b8-120">Next Steps</span></span>
<span data-ttu-id="766b8-121">Azure Otomasyonu ve Azure Storage bloblarını kullanılan toomanage, tablolar ve Kuyruklar nasıl çalıştırılabilir hello temel bilgileri öğrendiğinize göre bu bağlantıları toolearn Azure Otomasyonu hakkında daha fazla izleyin.</span><span class="sxs-lookup"><span data-stu-id="766b8-121">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Storage blobs, tables, and queues, follow these links toolearn more about Azure Automation.</span></span>

<span data-ttu-id="766b8-122">Hello Azure Otomasyonu öğretici bkz [oluşturma veya bir Azure Otomasyonu runbook'u içeri aktarma](../../automation/automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="766b8-122">See hello Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../../automation/automation-creating-importing-runbook.md).</span></span>

