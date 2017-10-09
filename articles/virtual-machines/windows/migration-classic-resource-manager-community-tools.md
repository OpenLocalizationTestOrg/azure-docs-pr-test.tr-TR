---
title: "aaaCommunity araçları - taşıma Klasik kaynakları tooAzure Resource Manager | Microsoft Docs"
description: "Merhaba topluluk toohelp tarafından sağlanan Bu makale kataloglar hello araçları Iaas kaynaklarına Klasik toohello Azure Resource Manager dağıtım modelinden geçirin."
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
ms.openlocfilehash: 67d5624a14d12a2d9eb46eb12aef461b706d4589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="community-tools-toomigrate-iaas-resources-from-classic-tooazure-resource-manager"></a><span data-ttu-id="98672-103">Topluluk toomigrate Iaas kaynaklardan Klasik tooAzure Kaynak Yöneticisi Araçları</span><span class="sxs-lookup"><span data-stu-id="98672-103">Community tools toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>
<span data-ttu-id="98672-104">Klasik toohello Azure Resource Manager dağıtım modeli Iaas kaynaklardan geçişini ile Merhaba topluluk tooassist tarafından sağlanmış olan bu makale kataloglar hello araçları.</span><span class="sxs-lookup"><span data-stu-id="98672-104">This article catalogs hello tools that have been provided by hello community tooassist with migration of IaaS resources from classic toohello Azure Resource Manager deployment model.</span></span>

> [!NOTE]
> <span data-ttu-id="98672-105">Bu araçları tarafından Microsoft Support resmi olarak desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="98672-105">These tools are not officially supported by Microsoft Support.</span></span> <span data-ttu-id="98672-106">Bu nedenle Github'da kaynaklanan açık ve mutluluk tooaccept PRs düzeltmeler veya ek senaryoları için çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="98672-106">Therefore they are open sourced on GitHub and we're happy tooaccept PRs for fixes or additional scenarios.</span></span> <span data-ttu-id="98672-107">bir sorun tooreport özelliği GitHub sorunları hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="98672-107">tooreport an issue, use hello GitHub issues feature.</span></span>
> 
> <span data-ttu-id="98672-108">Bu araçların geçiş kapalı kalma süresi Klasik sanal makineniz için neden olur.</span><span class="sxs-lookup"><span data-stu-id="98672-108">Migrating with these tools will cause downtime for your classic Virtual Machine.</span></span> <span data-ttu-id="98672-109">Desteklenen platform geçiş için arıyorsanız, ziyaret edin</span><span class="sxs-lookup"><span data-stu-id="98672-109">If you're looking for platform supported migration, visit</span></span> 
> 
>   * [<span data-ttu-id="98672-110">Klasik tooAzure Kaynak Yöneticisi yığını Iaas kaynaklardan desteklenen platform geçişi</span><span class="sxs-lookup"><span data-stu-id="98672-110">Platform supported migration of IaaS resources from Classic tooAzure Resource Manager stack</span></span>](migration-classic-resource-manager-overview.md)
>   * [<span data-ttu-id="98672-111">Klasik tooAzure Kaynak Yöneticisi geçişini teknik derinlemesine platformunda desteklenir</span><span class="sxs-lookup"><span data-stu-id="98672-111">Technical Deep Dive on Platform supported migration from Classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md)
>   * [<span data-ttu-id="98672-112">Iaas kaynaklarını Klasik tooAzure Azure PowerShell kullanarak Kaynak Yöneticisi ' geçirme</span><span class="sxs-lookup"><span data-stu-id="98672-112">Migrate IaaS resources from Classic tooAzure Resource Manager using Azure PowerShell</span></span>](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a><span data-ttu-id="98672-113">AsmMetadataParser</span><span class="sxs-lookup"><span data-stu-id="98672-113">AsmMetadataParser</span></span>
<span data-ttu-id="98672-114">Bu, Azure Hizmet Yönetimi tooAzure Resource Manager enterprise kümesinden bir parçası olarak oluşturulan yardımcı Araçlar koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="98672-114">This is a collection of helper tools created as part of enterprise migrations from Azure Service Management tooAzure Resource Manager.</span></span> <span data-ttu-id="98672-115">Bu araç, tooreplicate sağlar ve üretim aboneliğinizi hello geçiş çalıştırmadan önce sorunları Iron geçiş test etmek için kullanılabilir başka bir aboneliği yapınıza.</span><span class="sxs-lookup"><span data-stu-id="98672-115">This tool allows you tooreplicate your infrastructure into another subscription which can be used for testing migration and iron out any issues before running hello migration on your Production subscription.</span></span>

[<span data-ttu-id="98672-116">Bağlantı toohello aracı belgeleri</span><span class="sxs-lookup"><span data-stu-id="98672-116">Link toohello tool documentation</span></span>](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a><span data-ttu-id="98672-117">migAz</span><span class="sxs-lookup"><span data-stu-id="98672-117">migAz</span></span>
<span data-ttu-id="98672-118">migAz ek seçeneği toomigrate eksiksiz classic Iaas kaynaklar tooAzure Kaynak Yöneticisi Iaas kaynaklar ' dir.</span><span class="sxs-lookup"><span data-stu-id="98672-118">migAz is an additional option toomigrate a complete set of classic IaaS resources tooAzure Resource Manager IaaS resources.</span></span> <span data-ttu-id="98672-119">Merhaba geçiş hello içinde aynı oluşabilir abonelik ya da farklı Aboneliklerde ve abonelik türleri arasında (örn: CSP abonelikler).</span><span class="sxs-lookup"><span data-stu-id="98672-119">hello migration can occur within hello same subscription or between different subscriptions and subscription types (ex: CSP subscriptions).</span></span>

[<span data-ttu-id="98672-120">Bağlantı toohello aracı belgeleri</span><span class="sxs-lookup"><span data-stu-id="98672-120">Link toohello tool documentation</span></span>](https://github.com/Azure/migAz)

## <a name="next-steps"></a><span data-ttu-id="98672-121">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="98672-121">Next Steps</span></span>

* [<span data-ttu-id="98672-122">Klasik tooAzure Resource Manager Iaas kaynaklardan platform desteklenen geçişini genel bakış</span><span class="sxs-lookup"><span data-stu-id="98672-122">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="98672-123">Teknik ya ilişkin ayrıntılar platform desteklenen geçiş Klasik tooAzure Kaynak Yöneticisi'nden</span><span class="sxs-lookup"><span data-stu-id="98672-123">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="98672-124">Iaas kaynaklardan Klasik tooAzure Kaynak Yöneticisi geçişini planlama</span><span class="sxs-lookup"><span data-stu-id="98672-124">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="98672-125">Klasik tooAzure Resource Manager PowerShell toomigrate Iaas kaynakları kullanın</span><span class="sxs-lookup"><span data-stu-id="98672-125">Use PowerShell toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="98672-126">CLI toomigrate Iaas kaynaklarına Klasik tooAzure Kaynak Yöneticisi'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="98672-126">Use CLI toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="98672-127">En sık karşılaşılan geçiş hatalarını gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="98672-127">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="98672-128">Gözden geçirme hello en sık Klasik tooAzure Kaynak Yöneticisi geçirme Iaas kaynaklardan hakkında sorular</span><span class="sxs-lookup"><span data-stu-id="98672-128">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

