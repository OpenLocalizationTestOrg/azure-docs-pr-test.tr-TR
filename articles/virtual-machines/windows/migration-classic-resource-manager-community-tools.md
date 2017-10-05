---
title: "Topluluk araçları - Klasik kaynakları taşıma için Azure Resource Manager | Microsoft Docs"
description: "Bu makalede, Iaas kaynaklarına Klasikten Azure Resource Manager dağıtım modeline geçiş yardımcı olmak için topluluk tarafından sağlanan araçları kataloglar."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 228b697b-3950-49f5-84bb-283bb56621b1
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: d3fc0246088eddeb345bea0ffbd2c5247b218006
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="community-tools-to-migrate-iaas-resources-from-classic-to-azure-resource-manager"></a><span data-ttu-id="35fbd-103">IaaS kaynaklarını klasik modelden Azure Resource Manager’a geçirmeye yönelik topluluk araçları</span><span class="sxs-lookup"><span data-stu-id="35fbd-103">Community tools to migrate IaaS resources from classic to Azure Resource Manager</span></span>
<span data-ttu-id="35fbd-104">Bu makalede Klasik Iaas kaynaklardan Azure Resource Manager dağıtım modeline geçiş ile yardımcı olmak üzere topluluk tarafından sağlanan araçları kataloglar.</span><span class="sxs-lookup"><span data-stu-id="35fbd-104">This article catalogs the tools that have been provided by the community to assist with migration of IaaS resources from classic to the Azure Resource Manager deployment model.</span></span>

> [!NOTE]
> <span data-ttu-id="35fbd-105">Bu araçları tarafından Microsoft Support resmi olarak desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="35fbd-105">These tools are not officially supported by Microsoft Support.</span></span> <span data-ttu-id="35fbd-106">Bu nedenle Github'da kaynaklanan açık ve düzeltmeleri veya İlave Senaryolar PRs kabul mutluluk çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="35fbd-106">Therefore they are open sourced on GitHub and we're happy to accept PRs for fixes or additional scenarios.</span></span> <span data-ttu-id="35fbd-107">Bir sorunu bildirmek için GitHub sorunları özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="35fbd-107">To report an issue, use the GitHub issues feature.</span></span>
> 
> <span data-ttu-id="35fbd-108">Bu araçların geçiş kapalı kalma süresi Klasik sanal makineniz için neden olur.</span><span class="sxs-lookup"><span data-stu-id="35fbd-108">Migrating with these tools will cause downtime for your classic Virtual Machine.</span></span> <span data-ttu-id="35fbd-109">Desteklenen platform geçiş için arıyorsanız, ziyaret edin</span><span class="sxs-lookup"><span data-stu-id="35fbd-109">If you're looking for platform supported migration, visit</span></span> 
> 
>   * [<span data-ttu-id="35fbd-110">Klasik Iaas kaynaklardan Azure Resource Manager yığınına desteklenen platform geçişi</span><span class="sxs-lookup"><span data-stu-id="35fbd-110">Platform supported migration of IaaS resources from Classic to Azure Resource Manager stack</span></span>](migration-classic-resource-manager-overview.md)
>   * [<span data-ttu-id="35fbd-111">Teknik derinlemesine platformunda geçiş Klasik Azure Resource Manager için desteklenen</span><span class="sxs-lookup"><span data-stu-id="35fbd-111">Technical Deep Dive on Platform supported migration from Classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md)
>   * [<span data-ttu-id="35fbd-112">Iaas kaynaklarını Klasikten Azure Resource Manager'da Azure PowerShell kullanarak geçirme</span><span class="sxs-lookup"><span data-stu-id="35fbd-112">Migrate IaaS resources from Classic to Azure Resource Manager using Azure PowerShell</span></span>](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a><span data-ttu-id="35fbd-113">AsmMetadataParser</span><span class="sxs-lookup"><span data-stu-id="35fbd-113">AsmMetadataParser</span></span>
<span data-ttu-id="35fbd-114">Bu, Kurumsal geçişleri için Azure Resource Manager Azure Hizmet Yönetimi'nden bir parçası olarak oluşturulan yardımcı Araçlar koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="35fbd-114">This is a collection of helper tools created as part of enterprise migrations from Azure Service Management to Azure Resource Manager.</span></span> <span data-ttu-id="35fbd-115">Bu araç, geçiş ve sorunları çıkışı Demir geçiş üretim aboneliğinizi çalıştırmadan önce test etmek için kullanılan başka bir aboneliğe altyapınızı çoğaltmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="35fbd-115">This tool allows you to replicate your infrastructure into another subscription which can be used for testing migration and iron out any issues before running the migration on your Production subscription.</span></span>

[<span data-ttu-id="35fbd-116">Aracı belgeleri için bağlantı</span><span class="sxs-lookup"><span data-stu-id="35fbd-116">Link to the tool documentation</span></span>](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a><span data-ttu-id="35fbd-117">migAz</span><span class="sxs-lookup"><span data-stu-id="35fbd-117">migAz</span></span>
<span data-ttu-id="35fbd-118">migAz eksiksiz classic Iaas kaynakların Azure Resource Manager Iaas kaynaklarına geçirmek için ek bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="35fbd-118">migAz is an additional option to migrate a complete set of classic IaaS resources to Azure Resource Manager IaaS resources.</span></span> <span data-ttu-id="35fbd-119">Geçiş aynı abonelik içindeki ya da farklı Aboneliklerde ve abonelik türleri arasında oluşabilir (örn: CSP abonelikler).</span><span class="sxs-lookup"><span data-stu-id="35fbd-119">The migration can occur within the same subscription or between different subscriptions and subscription types (ex: CSP subscriptions).</span></span>

[<span data-ttu-id="35fbd-120">Aracı belgeleri için bağlantı</span><span class="sxs-lookup"><span data-stu-id="35fbd-120">Link to the tool documentation</span></span>](https://github.com/Azure/migAz)

## <a name="next-steps"></a><span data-ttu-id="35fbd-121">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="35fbd-121">Next Steps</span></span>

* [<span data-ttu-id="35fbd-122">Platform desteklenen geçişi Iaas Klasik kaynaklardan Azure Resource Manager'a genel bakış</span><span class="sxs-lookup"><span data-stu-id="35fbd-122">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="35fbd-123">Teknik ya ilişkin ayrıntılar platform desteklenen geçiş Klasik'ten Azure Kaynak Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="35fbd-123">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="35fbd-124">IaaS kaynaklarının Klasik’ten Azure Resource Manager’a geçişini planlama</span><span class="sxs-lookup"><span data-stu-id="35fbd-124">Planning for migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="35fbd-125">Iaas kaynaklarına Klasikten Azure Resource Manager geçirmek için PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="35fbd-125">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="35fbd-126">Iaas kaynaklarına Klasikten Azure Resource Manager geçirmek için CLI kullanın</span><span class="sxs-lookup"><span data-stu-id="35fbd-126">Use CLI to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="35fbd-127">En sık karşılaşılan geçiş hatalarını gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="35fbd-127">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="35fbd-128">Gözden geçirme Iaas kaynaklardan Klasik Azure Kaynak Yöneticisi hakkında en sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="35fbd-128">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

