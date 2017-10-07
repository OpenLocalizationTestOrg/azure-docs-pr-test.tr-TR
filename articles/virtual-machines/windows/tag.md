---
title: aaaHow tootag Azure Windows VM kaynak | Microsoft Docs
description: "Azure'da hello Resource Manager dağıtım modeli kullanarak oluşturulan Windows sanal makine etiketleme hakkında bilgi edinin"
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
ms.openlocfilehash: 160416ddc35998b3c98c6e579668a6a5eb6de6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="b2198-103">Nasıl tootag azure'da Windows sanal makine</span><span class="sxs-lookup"><span data-stu-id="b2198-103">How tootag a Windows virtual machine in Azure</span></span>
<span data-ttu-id="b2198-104">Bu makalede farklı şekillerde tootag hello Resource Manager dağıtım modeli üzerinden Windows sanal makine azure'da açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b2198-104">This article describes different ways tootag a Windows virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="b2198-105">Etiketler doğrudan bir kaynağa veya bir kaynak grubu yerleştirilen kullanıcı tanımlı anahtar/değer çiftleridir.</span><span class="sxs-lookup"><span data-stu-id="b2198-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="b2198-106">Azure şu anda'kaynak ve kaynak grubu başına too15 etiketlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="b2198-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="b2198-107">Etiketleri hello oluşturma sırasında bir kaynakta yerleştirilebilir veya tooan mevcut kaynak eklendi.</span><span class="sxs-lookup"><span data-stu-id="b2198-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="b2198-108">Etiketler hello Resource Manager dağıtım modeli yalnızca oluşturulan kaynaklar için desteklendiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b2198-108">Please note that tags are supported for resources created via hello Resource Manager deployment model only.</span></span> <span data-ttu-id="b2198-109">Linux sanal makine tootag istiyorsanız, bkz: [nasıl tootag azure'da bir Linux sanal makine](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2198-109">If you want tootag a Linux virtual machine, see [How tootag a Linux virtual machine in Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a><span data-ttu-id="b2198-110">PowerShell ile etiketleme</span><span class="sxs-lookup"><span data-stu-id="b2198-110">Tagging with PowerShell</span></span>
<span data-ttu-id="b2198-111">toocreate, ekleme ve PowerShell aracılığıyla etiketleri silme, Yukarı önce tooset gerekir, [PowerShell ortam Azure Resource Manager ile][PowerShell environment with Azure Resource Manager].</span><span class="sxs-lookup"><span data-stu-id="b2198-111">toocreate, add, and delete tags through PowerShell, you first need tooset up your [PowerShell environment with Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span></span> <span data-ttu-id="b2198-112">Merhaba Kurulum tamamlandığında, etiketler oluşturma veya hello kaynak PowerShell yoluyla oluşturulduktan sonra işlem, ağ ve depolama kaynakları yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2198-112">Once you have completed hello setup, you can place tags on Compute, Network, and Storage resources at creation or after hello resource is created via PowerShell.</span></span> <span data-ttu-id="b2198-113">Bu makalede, görüntüleme ve düzenleme etiketleri sanal makinelerde yerleştirilen hakkında odaklanacaktır.</span><span class="sxs-lookup"><span data-stu-id="b2198-113">This article will concentrate on viewing/editing tags placed on Virtual Machines.</span></span>

<span data-ttu-id="b2198-114">İlk olarak, hello aracılığıyla sanal makine tooa gidin `Get-AzureRmVM` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="b2198-114">First, navigate tooa Virtual Machine through hello `Get-AzureRmVM` cmdlet.</span></span>

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

<span data-ttu-id="b2198-115">Sanal makineniz etiketleri içeriyorsa, tüm hello etiketleri, kaynakta sonra görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="b2198-115">If your Virtual Machine already contains tags, you will then see all hello tags on your resource:</span></span>

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

<span data-ttu-id="b2198-116">PowerShell aracılığıyla tooadd etiketleri isterseniz hello kullanabilirsiniz `Set-AzureRmResource` komutu.</span><span class="sxs-lookup"><span data-stu-id="b2198-116">If you would like tooadd tags through PowerShell, you can use hello `Set-AzureRmResource` command.</span></span> <span data-ttu-id="b2198-117">PowerShell aracılığıyla etiketler güncelleştirilirken etiketleri bir bütün olarak güncelleştirilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b2198-117">Note when updating tags through PowerShell, tags are updated as a whole.</span></span> <span data-ttu-id="b2198-118">Bu nedenle etiketleri zaten olan bir etiketi tooa kaynak ekliyorsanız, hello kaynakta yerleştirilen toobe istediğiniz tüm hello etiketleri tooinclude gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2198-118">So if you are adding one tag tooa resource that already has tags, you will need tooinclude all hello tags that you want toobe placed on hello resource.</span></span> <span data-ttu-id="b2198-119">Aşağıda nasıl tooadd ek PowerShell cmdlet'leri aracılığıyla tooa kaynak etiketler, bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b2198-119">Below is an example of how tooadd additional tags tooa resource through PowerShell Cmdlets.</span></span>

<span data-ttu-id="b2198-120">Bu ilk cmdlet'i tüm getirilen hello etiketlerin ayarlar *MyTestVM* toohello *$tags* hello kullanarak değişken `Get-AzureRmResource` ve `Tags` özelliği.</span><span class="sxs-lookup"><span data-stu-id="b2198-120">This first cmdlet sets all of hello tags placed on *MyTestVM* toohello *$tags* variable, using hello `Get-AzureRmResource` and `Tags` property.</span></span>

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

<span data-ttu-id="b2198-121">Merhaba ikinci komutu değişkeni verilen hello hello etiketleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b2198-121">hello second command displays hello tags for hello given variable.</span></span>

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

<span data-ttu-id="b2198-122">Merhaba üçüncü komut ekler ek etiketi toohello *$tags* değişkeni.</span><span class="sxs-lookup"><span data-stu-id="b2198-122">hello third command adds an additional tag toohello *$tags* variable.</span></span> <span data-ttu-id="b2198-123">Not hello hello  **+=**  tooappend hello yeni anahtar/değer çifti toohello *$tags* listesi.</span><span class="sxs-lookup"><span data-stu-id="b2198-123">Note hello use of hello **+=** tooappend hello new key/value pair toohello *$tags* list.</span></span>

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

<span data-ttu-id="b2198-124">Merhaba dördüncü komut hello etiketleri hello tanımlanan tüm ayarlar *$tags* kaynak verilen değişken toohello.</span><span class="sxs-lookup"><span data-stu-id="b2198-124">hello fourth command sets all of hello tags defined in hello *$tags* variable toohello given resource.</span></span> <span data-ttu-id="b2198-125">Bu durumda, MyTestVM olur.</span><span class="sxs-lookup"><span data-stu-id="b2198-125">In this case, it is MyTestVM.</span></span>

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

<span data-ttu-id="b2198-126">Merhaba beşinci komut tüm hello etiketlerin hello kaynakta görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b2198-126">hello fifth command displays all of hello tags on hello resource.</span></span> <span data-ttu-id="b2198-127">Gördüğünüz gibi *konumu* şimdi bir etiketle olarak tanımlanan *MyLocation* hello değeri olarak.</span><span class="sxs-lookup"><span data-stu-id="b2198-127">As you can see, *Location* is now defined as a tag with *MyLocation* as hello value.</span></span>

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

<span data-ttu-id="b2198-128">hakkında daha fazla bilgi toolearn PowerShell aracılığıyla etiketlemeyi hello denetle [Azure kaynak cmdlet'leri][Azure Resource Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="b2198-128">toolearn more about tagging through PowerShell, check out hello [Azure Resource Cmdlets][Azure Resource Cmdlets].</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="b2198-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b2198-129">Next steps</span></span>
* <span data-ttu-id="b2198-130">Azure kaynaklarınızı etiketleme hakkında daha fazla toolearn bkz [Azure Resource Manager'a genel bakış] [ Azure Resource Manager Overview] ve [etiketleri kullanarak tooorganize Azure kaynaklarınızı] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="b2198-130">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="b2198-131">Etiketler, Azure kaynak kullanımınızı yönetmenize yardımcı olabilir nasıl toosee bkz [Azure faturanızı anlamak] [ Understanding your Azure Bill] ve [Microsoft Azure kaynak tüketimini Öngörüler elde] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="b2198-131">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
