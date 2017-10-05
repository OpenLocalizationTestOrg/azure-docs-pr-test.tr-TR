---
title: "Bir Azure Linux sanal makine etiketlemek nasıl | Microsoft Docs"
description: "Azure Resource Manager dağıtım modeli kullanılarak oluşturulmuş bir Azure Linux sanal makinenin etiketleme hakkında bilgi edinin."
services: virtual-machines-linux
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: memccror
ms.openlocfilehash: da3ff0de2a5d6ac8994b7c16b758f976228a53b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-tag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="55d75-103">Azure'da bir Linux sanal makine etiketlemek nasıl</span><span class="sxs-lookup"><span data-stu-id="55d75-103">How to tag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="55d75-104">Bu makalede Resource Manager dağıtım modeli aracılığıyla Azure'da bir Linux sanal makine etiketlemek için farklı yollar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="55d75-104">This article describes different ways to tag a Linux virtual machine in Azure through the Resource Manager deployment model.</span></span> <span data-ttu-id="55d75-105">Etiketler doğrudan bir kaynağa veya bir kaynak grubu yerleştirilen kullanıcı tanımlı anahtar/değer çiftleridir.</span><span class="sxs-lookup"><span data-stu-id="55d75-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="55d75-106">Azure şu anda kaynak ve kaynak grubu başına en fazla 15 etiketlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="55d75-106">Azure currently supports up to 15 tags per resource and resource group.</span></span> <span data-ttu-id="55d75-107">Etiketler oluşturma sırasında bir kaynağa yerleştirilmiş veya mevcut bir kaynağı eklendi.</span><span class="sxs-lookup"><span data-stu-id="55d75-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span></span> <span data-ttu-id="55d75-108">Lütfen unutmayın, Resource Manager dağıtım modeli yalnızca oluşturulan kaynaklar için etiketler desteklenir.</span><span class="sxs-lookup"><span data-stu-id="55d75-108">Please note, tags are supported for resources created via the Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="55d75-109">Azure CLI ile etiketleme</span><span class="sxs-lookup"><span data-stu-id="55d75-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="55d75-110">Başlamak için en son gereksinim [Azure CLI 2.0 (Önizleme)](/cli/azure/install-az-cli2) yüklü ve bir Azure hesabı kullanarak oturum açmış [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="55d75-110">To begin, you need the latest [Azure CLI 2.0 (Preview)](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="55d75-111">Bu adımları [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ile de gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55d75-111">You can also perform these steps with the [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="55d75-112">Bir verilen etiketleri de dahil olmak üzere bu komutu kullanarak sanal makine için tüm özelliklerini görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="55d75-112">You can view all properties for a given Virtual Machine, including the tags, using this command:</span></span>

        az vm show --resource-group MyResourceGroup --name MyTestVM

<span data-ttu-id="55d75-113">Azure CLI aracılığıyla yeni bir VM etiket eklemek için kullanabileceğiniz `azure vm update` tag parametresini birlikte komutu **--ayarlama**:</span><span class="sxs-lookup"><span data-stu-id="55d75-113">To add a new VM tag through the Azure CLI, you can use the `azure vm update` command along with the tag parameter **--set**:</span></span>

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

<span data-ttu-id="55d75-114">Etiketleri kaldırmak için kullanabileceğiniz **--kaldırmak** parametresinde `azure vm update` komutu.</span><span class="sxs-lookup"><span data-stu-id="55d75-114">To remove tags, you can use the **--remove** parameter in the `azure vm update` command.</span></span>

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


<span data-ttu-id="55d75-115">Etiketler KAYNAKLARIMIZI Azure CLI ve Portal için uyguladıysanız, fatura portalı etiketlerinde görmek için kullanım ayrıntılarını bir göz atalım.</span><span class="sxs-lookup"><span data-stu-id="55d75-115">Now that we have applied tags to our resources Azure CLI and the Portal, let’s take a look at the usage details to see the tags in the billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="55d75-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="55d75-116">Next steps</span></span>
* <span data-ttu-id="55d75-117">Azure kaynaklarınızı etiketleme hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış] [ Azure Resource Manager Overview] ve [etiketleri kullanarak Azure kaynaklarınızı düzenleme][Using Tags to organize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="55d75-117">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span></span>
* <span data-ttu-id="55d75-118">Etiketleri kullanımınızı Azure kaynaklarını yönetmek nasıl yardımcı olabileceğini görmek için bkz: [Azure faturanızı anlamak] [ Understanding your Azure Bill] ve [Microsoft Azure kaynak tüketimini Öngörüler elde][Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="55d75-118">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
