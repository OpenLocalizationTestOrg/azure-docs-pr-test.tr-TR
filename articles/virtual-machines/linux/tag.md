---
title: aaaHow tootag Azure Linux sanal makine | Microsoft Docs
description: "Azure'da hello Resource Manager dağıtım modeli kullanarak oluşturulmuş bir Azure Linux sanal makinenin etiketleme hakkında bilgi edinin."
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
ms.openlocfilehash: 456b226af4495c3b446cb79c99cf9494dde9fca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="a6bc0-103">Nasıl tootag azure'da bir Linux sanal makine</span><span class="sxs-lookup"><span data-stu-id="a6bc0-103">How tootag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="a6bc0-104">Bu makalede farklı şekillerde tootag Linux sanal makine azure'da hello Resource Manager dağıtım modeli üzerinden açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a6bc0-104">This article describes different ways tootag a Linux virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="a6bc0-105">Etiketler doğrudan bir kaynağa veya bir kaynak grubu yerleştirilen kullanıcı tanımlı anahtar/değer çiftleridir.</span><span class="sxs-lookup"><span data-stu-id="a6bc0-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="a6bc0-106">Azure şu anda'kaynak ve kaynak grubu başına too15 etiketlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="a6bc0-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="a6bc0-107">Etiketleri hello oluşturma sırasında bir kaynakta yerleştirilebilir veya tooan mevcut kaynak eklendi.</span><span class="sxs-lookup"><span data-stu-id="a6bc0-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="a6bc0-108">Lütfen unutmayın, etiketleri hello Resource Manager dağıtım modeli yalnızca oluşturulan kaynaklar için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a6bc0-108">Please note, tags are supported for resources created via hello Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="a6bc0-109">Azure CLI ile etiketleme</span><span class="sxs-lookup"><span data-stu-id="a6bc0-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="a6bc0-110">toobegin, gereksinim duyduğunuz hello son [Azure CLI 2.0 (Önizleme)](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="a6bc0-110">toobegin, you need hello latest [Azure CLI 2.0 (Preview)](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="a6bc0-111">Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6bc0-111">You can also perform these steps with hello [Azure CLI 1.0](tag-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="a6bc0-112">Bir verilen hello etiketleri de dahil olmak üzere, bu komutu kullanma için sanal makine, tüm özelliklerini görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a6bc0-112">You can view all properties for a given Virtual Machine, including hello tags, using this command:</span></span>

        az vm show --resource-group MyResourceGroup --name MyTestVM

<span data-ttu-id="a6bc0-113">tooadd hello Azure CLI aracılığıyla yeni bir VM etiket, kullanabileceğiniz hello `azure vm update` hello tag parametresini birlikte komutu **--ayarlama**:</span><span class="sxs-lookup"><span data-stu-id="a6bc0-113">tooadd a new VM tag through hello Azure CLI, you can use hello `azure vm update` command along with hello tag parameter **--set**:</span></span>

        az vm update --resource-group MyResourceGroup --name MyTestVM –-set tags.myNewTagName1=myNewTagValue1 tags.myNewTagName2=myNewTagValue2

<span data-ttu-id="a6bc0-114">tooremove etiketleri hello kullanabilir **--kaldırmak** hello parametresinde `azure vm update` komutu.</span><span class="sxs-lookup"><span data-stu-id="a6bc0-114">tooremove tags, you can use hello **--remove** parameter in hello `azure vm update` command.</span></span>

        az vm update –-resource-group MyResourceGroup –-name MyTestVM --remove tags.myNewTagName1


<span data-ttu-id="a6bc0-115">Etiketler tooour kaynakları Azure CLI uyguladığınız ve Portal hello göre bir hello kullanım ayrıntılarını toosee hello etiketleri hello fatura Portalı'nda bakalım.</span><span class="sxs-lookup"><span data-stu-id="a6bc0-115">Now that we have applied tags tooour resources Azure CLI and hello Portal, let’s take a look at hello usage details toosee hello tags in hello billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="a6bc0-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a6bc0-116">Next steps</span></span>
* <span data-ttu-id="a6bc0-117">Azure kaynaklarınızı etiketleme hakkında daha fazla toolearn bkz [Azure Resource Manager'a genel bakış] [ Azure Resource Manager Overview] ve [etiketleri kullanarak tooorganize Azure kaynaklarınızı] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="a6bc0-117">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="a6bc0-118">Etiketler, Azure kaynak kullanımınızı yönetmenize yardımcı olabilir nasıl toosee bkz [Azure faturanızı anlamak] [ Understanding your Azure Bill] ve [Microsoft Azure kaynak tüketimini Öngörüler elde] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="a6bc0-118">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
