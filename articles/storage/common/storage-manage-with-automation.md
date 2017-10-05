---
title: "Azure Storage Azure otomasyonu kullanarak yönetme"
description: "Nasıl Azure Otomasyon hizmetine ölçekte Azure depolamayı yönetmek için kullanılabilir hakkında bilgi edinin."
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
ms.openlocfilehash: 4649e42a628307e15f8b067503e4e8e13f16f1af
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a><span data-ttu-id="ece9c-103">Azure Storage Azure otomasyonu kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="ece9c-103">Managing Azure Storage using Azure Automation</span></span>
<span data-ttu-id="ece9c-104">Bu kılavuz Azure Otomasyon hizmetine ve nasıl bu Azure depolama BLOB'lar, tablolar ve Kuyruklar yönetimini kolaylaştırmak için kullanılabilir tanıtılacaktır.</span><span class="sxs-lookup"><span data-stu-id="ece9c-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure Storage blobs, tables, and queues.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="ece9c-105">Azure Otomasyonu Nedir?</span><span class="sxs-lookup"><span data-stu-id="ece9c-105">What is Azure Automation?</span></span>
<span data-ttu-id="ece9c-106">[Azure Otomasyonu](https://azure.microsoft.com/services/automation/) işlem Otomasyonu aracılığıyla bulut yönetimi basitleştirmek için bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="ece9c-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="ece9c-107">Azure otomasyonu kullanarak, uzun süre çalışan, el ile hatasız ve sık tekrarlanan görevleri, güvenilirlik ve verimliliği artırmak için otomatik ve kuruluşunuz için değerine süresini azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="ece9c-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability and efficiency, and reduce time to value for your organization.</span></span>

<span data-ttu-id="ece9c-108">Azure Otomasyonu, kuruluşunuz büyüdükçe gereksinimlerinizi karşılayacak şekilde ölçekler bir yüksek oranda güvenilir ve yüksek oranda kullanılabilir iş akışı yürütme altyapısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="ece9c-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="ece9c-109">Tam olarak gerekli görevleri ortaya böylece Azure Otomasyonu'nda işlemleri el ile 3. taraf sistemleri tarafından veya zamanlanan aralıklarla artırılabilir devre dışı.</span><span class="sxs-lookup"><span data-stu-id="ece9c-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="ece9c-110">İşletimsel ek yükü azaltmak ve boşaltmak BT / iş ekler çalışmaları odaklanmaya DevOps personel değer Azure Automation'ın otomatik olarak çalıştırılmak üzere bulut yönetim görevlerinizi taşıyarak.</span><span class="sxs-lookup"><span data-stu-id="ece9c-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-storage"></a><span data-ttu-id="ece9c-111">Azure Otomasyonu Azure Storage yönetmenize nasıl yardımcı olabilir?</span><span class="sxs-lookup"><span data-stu-id="ece9c-111">How can Azure Automation help manage Azure Storage?</span></span>
<span data-ttu-id="ece9c-112">Azure depolama yönetilebilir Azure Otomasyonu'nda kullanılabilir PowerShell cmdlet'lerini kullanarak [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="ece9c-112">Azure Storage can be managed in Azure Automation by using the PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="ece9c-113">Böylece tüm blob, tablo ve hizmet içinde sıra yönetim görevleri gerçekleştirebilir azure Otomasyonu kutudan çıktığında, bu depolama PowerShell cmdlet'leri vardır.</span><span class="sxs-lookup"><span data-stu-id="ece9c-113">Azure Automation has these Storage PowerShell cmdlets available out of the box, so that you can perform all of your blob, table, and queue management tasks within the service.</span></span> <span data-ttu-id="ece9c-114">Ayrıca Azure Automation bu cmdlet'leri Azure hizmeti ve 3. taraf sistemi arasında karmaşık görevleri otomatikleştirmek için diğer Azure Hizmetleri için cmdlet'leri ile eşleştirin.</span><span class="sxs-lookup"><span data-stu-id="ece9c-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="ece9c-115">[Azure Otomasyonu runbook Galerisi](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) Azure Storage diğer Azure Hizmetleri ve 3. taraf sistemi yönetimi otomatikleştirme başlamak için ürün ekibi ve topluluk runbook'lar çeşitli içerir.</span><span class="sxs-lookup"><span data-stu-id="ece9c-115">The [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks to get started automating management of Azure Storage, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="ece9c-116">Galeri runbook'ları şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="ece9c-116">Gallery runbooks include:</span></span>

* [<span data-ttu-id="ece9c-117">Azure Storage Bloblarında'de, belirli gün eski kullanarak otomasyon hizmet Kaldır</span><span class="sxs-lookup"><span data-stu-id="ece9c-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [<span data-ttu-id="ece9c-118">Azure depolama biriminden bir Blob indirin</span><span class="sxs-lookup"><span data-stu-id="ece9c-118">Download a Blob from Azure Storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [<span data-ttu-id="ece9c-119">Bir bulut hizmetindeki tüm sanal makineleri veya tek bir Azure VM için tüm diskleri yedekleme</span><span class="sxs-lookup"><span data-stu-id="ece9c-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a><span data-ttu-id="ece9c-120">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="ece9c-120">Next Steps</span></span>
<span data-ttu-id="ece9c-121">Azure Otomasyonu ve nasıl Azure Storage BLOB'lar, tablolar ve Kuyruklar yönetmek için kullanılmadan öğrendiğinize göre Azure Otomasyonu hakkında daha fazla bilgi için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="ece9c-121">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Storage blobs, tables, and queues, follow these links to learn more about Azure Automation.</span></span>

<span data-ttu-id="ece9c-122">Azure Otomasyonu öğretici bkz [oluşturma veya bir Azure Otomasyonu runbook'u içeri aktarma](../../automation/automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="ece9c-122">See the Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../../automation/automation-creating-importing-runbook.md).</span></span>

