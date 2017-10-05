---
title: "Azure üzerinde bir Windows VM kaynak etiketlemek nasıl | Microsoft Docs"
description: "Azure Resource Manager dağıtım modeli kullanılarak oluşturulmuş bir Windows sanal makinenin etiketleme hakkında bilgi edinin"
services: virtual-machines-windows
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 56d17f45-e4a7-4d84-8022-b40334ae49d2
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2016
ms.author: memccror
ms.openlocfilehash: 5f00c4265cea3db02dbb09a7f81be636a3fdd3d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-tag-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="dde4a-103">Azure'da Windows sanal makine etiketlemek nasıl</span><span class="sxs-lookup"><span data-stu-id="dde4a-103">How to tag a Windows virtual machine in Azure</span></span>
<span data-ttu-id="dde4a-104">Bu makalede Resource Manager dağıtım modeli aracılığıyla Azure'da Windows sanal makine etiketlemek için farklı yollar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="dde4a-104">This article describes different ways to tag a Windows virtual machine in Azure through the Resource Manager deployment model.</span></span> <span data-ttu-id="dde4a-105">Etiketler doğrudan bir kaynağa veya bir kaynak grubu yerleştirilen kullanıcı tanımlı anahtar/değer çiftleridir.</span><span class="sxs-lookup"><span data-stu-id="dde4a-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="dde4a-106">Azure şu anda kaynak ve kaynak grubu başına en fazla 15 etiketlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="dde4a-106">Azure currently supports up to 15 tags per resource and resource group.</span></span> <span data-ttu-id="dde4a-107">Etiketler oluşturma sırasında bir kaynağa yerleştirilmiş veya mevcut bir kaynağı eklendi.</span><span class="sxs-lookup"><span data-stu-id="dde4a-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span></span> <span data-ttu-id="dde4a-108">Etiketler Resource Manager dağıtım modeli yalnızca oluşturulan kaynaklar için desteklendiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="dde4a-108">Please note that tags are supported for resources created via the Resource Manager deployment model only.</span></span> <span data-ttu-id="dde4a-109">Linux sanal makine etiketi istiyorsanız, bkz: [Azure'da bir Linux sanal makine etiketlemek nasıl](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dde4a-109">If you want to tag a Linux virtual machine, see [How to tag a Linux virtual machine in Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a><span data-ttu-id="dde4a-110">PowerShell ile etiketleme</span><span class="sxs-lookup"><span data-stu-id="dde4a-110">Tagging with PowerShell</span></span>
<span data-ttu-id="dde4a-111">Oluşturmak için Ekle ve PowerShell, ayarlamak için ilk gerek aracılığıyla etiketleri silmek, [PowerShell ortam Azure Resource Manager ile][PowerShell environment with Azure Resource Manager].</span><span class="sxs-lookup"><span data-stu-id="dde4a-111">To create, add, and delete tags through PowerShell, you first need to set up your [PowerShell environment with Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span></span> <span data-ttu-id="dde4a-112">Kurulum tamamlandığında, etiketler oluşturma veya kaynak PowerShell yoluyla oluşturulduktan sonra işlem, ağ ve depolama kaynakları yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dde4a-112">Once you have completed the setup, you can place tags on Compute, Network, and Storage resources at creation or after the resource is created via PowerShell.</span></span> <span data-ttu-id="dde4a-113">Bu makalede, görüntüleme ve düzenleme etiketleri sanal makinelerde yerleştirilen hakkında odaklanacaktır.</span><span class="sxs-lookup"><span data-stu-id="dde4a-113">This article will concentrate on viewing/editing tags placed on Virtual Machines.</span></span>

<span data-ttu-id="dde4a-114">İlk olarak, bir sanal makineye üzerinden gidin `Get-AzureRmVM` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="dde4a-114">First, navigate to a Virtual Machine through the `Get-AzureRmVM` cmdlet.</span></span>

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

<span data-ttu-id="dde4a-115">Sanal makineniz etiketleri içeriyorsa, tüm etiketleri, kaynakta sonra görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="dde4a-115">If your Virtual Machine already contains tags, you will then see all the tags on your resource:</span></span>

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

<span data-ttu-id="dde4a-116">PowerShell aracılığıyla etiketler eklemek istiyorsanız, kullanabileceğiniz `Set-AzureRmResource` komutu.</span><span class="sxs-lookup"><span data-stu-id="dde4a-116">If you would like to add tags through PowerShell, you can use the `Set-AzureRmResource` command.</span></span> <span data-ttu-id="dde4a-117">PowerShell aracılığıyla etiketler güncelleştirilirken etiketleri bir bütün olarak güncelleştirilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="dde4a-117">Note when updating tags through PowerShell, tags are updated as a whole.</span></span> <span data-ttu-id="dde4a-118">Bu nedenle etiketleri zaten olan bir kaynağın bir etiket ekliyorsanız, kaynak yerleştirilmesini istediğiniz tüm etiketleri dahil etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="dde4a-118">So if you are adding one tag to a resource that already has tags, you will need to include all the tags that you want to be placed on the resource.</span></span> <span data-ttu-id="dde4a-119">Aşağıda, PowerShell cmdlet'leri aracılığıyla bir kaynağa ek etiketleri eklemeyi örneğidir.</span><span class="sxs-lookup"><span data-stu-id="dde4a-119">Below is an example of how to add additional tags to a resource through PowerShell Cmdlets.</span></span>

<span data-ttu-id="dde4a-120">Bu ilk cmdlet'i tüm getirilen etiketleri ayarlar *MyTestVM* için *$tags* değişken, kullanarak `Get-AzureRmResource` ve `Tags` özelliği.</span><span class="sxs-lookup"><span data-stu-id="dde4a-120">This first cmdlet sets all of the tags placed on *MyTestVM* to the *$tags* variable, using the `Get-AzureRmResource` and `Tags` property.</span></span>

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

<span data-ttu-id="dde4a-121">İkinci komut belirtilen değişkeni için etiketleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="dde4a-121">The second command displays the tags for the given variable.</span></span>

        PS C:\> $tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment

<span data-ttu-id="dde4a-122">Üçüncü komut ek bir etikete ekler *$tags* değişkeni.</span><span class="sxs-lookup"><span data-stu-id="dde4a-122">The third command adds an additional tag to the *$tags* variable.</span></span> <span data-ttu-id="dde4a-123">Kullanımına dikkat edin  **+=**  yeni anahtar/değer çifti eklemek için *$tags* listesi.</span><span class="sxs-lookup"><span data-stu-id="dde4a-123">Note the use of the **+=** to append the new key/value pair to the *$tags* list.</span></span>

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

<span data-ttu-id="dde4a-124">Dördüncü komut tüm tanımlanan etiketleri ayarlar *$tags* verilen kaynağa değişken.</span><span class="sxs-lookup"><span data-stu-id="dde4a-124">The fourth command sets all of the tags defined in the *$tags* variable to the given resource.</span></span> <span data-ttu-id="dde4a-125">Bu durumda, MyTestVM olur.</span><span class="sxs-lookup"><span data-stu-id="dde4a-125">In this case, it is MyTestVM.</span></span>

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

<span data-ttu-id="dde4a-126">Beşinci komut tüm etiketleri kaynaktaki görüntüler.</span><span class="sxs-lookup"><span data-stu-id="dde4a-126">The fifth command displays all of the tags on the resource.</span></span> <span data-ttu-id="dde4a-127">Gördüğünüz gibi *konumu* şimdi bir etiketle olarak tanımlanan *MyLocation* değeri olarak.</span><span class="sxs-lookup"><span data-stu-id="dde4a-127">As you can see, *Location* is now defined as a tag with *MyLocation* as the value.</span></span>

        PS C:\> (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment
        Value        MyLocation
        Name        Location

<span data-ttu-id="dde4a-128">PowerShell aracılığıyla etiketleme hakkında daha fazla bilgi için kullanıma [Azure kaynak cmdlet'leri][Azure Resource Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="dde4a-128">To learn more about tagging through PowerShell, check out the [Azure Resource Cmdlets][Azure Resource Cmdlets].</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="dde4a-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dde4a-129">Next steps</span></span>
* <span data-ttu-id="dde4a-130">Azure kaynaklarınızı etiketleme hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış] [ Azure Resource Manager Overview] ve [etiketleri kullanarak Azure kaynaklarınızı düzenleme][Using Tags to organize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="dde4a-130">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span></span>
* <span data-ttu-id="dde4a-131">Etiketleri kullanımınızı Azure kaynaklarını yönetmek nasıl yardımcı olabileceğini görmek için bkz: [Azure faturanızı anlamak] [ Understanding your Azure Bill] ve [Microsoft Azure kaynak tüketimini Öngörüler elde][Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="dde4a-131">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
