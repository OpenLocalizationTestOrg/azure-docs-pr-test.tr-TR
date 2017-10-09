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
ms.openlocfilehash: 0e99ea66a87b7e00eb21a2f72dd2bce8673778dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="4d115-103">Nasıl tootag azure'da bir Linux sanal makine</span><span class="sxs-lookup"><span data-stu-id="4d115-103">How tootag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="4d115-104">Bu makalede farklı şekillerde tootag Linux sanal makine azure'da hello Resource Manager dağıtım modeli üzerinden açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4d115-104">This article describes different ways tootag a Linux virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="4d115-105">Etiketler doğrudan bir kaynağa veya bir kaynak grubu yerleştirilen kullanıcı tanımlı anahtar/değer çiftleridir.</span><span class="sxs-lookup"><span data-stu-id="4d115-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="4d115-106">Azure şu anda'kaynak ve kaynak grubu başına too15 etiketlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="4d115-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="4d115-107">Etiketleri hello oluşturma sırasında bir kaynakta yerleştirilebilir veya tooan mevcut kaynak eklendi.</span><span class="sxs-lookup"><span data-stu-id="4d115-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="4d115-108">Lütfen unutmayın, etiketleri hello Resource Manager dağıtım modeli yalnızca oluşturulan kaynaklar için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="4d115-108">Please note, tags are supported for resources created via hello Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="4d115-109">Azure CLI ile etiketleme</span><span class="sxs-lookup"><span data-stu-id="4d115-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="4d115-110">toobegin, [hello Azure CLI yükleyip](../../xplat-cli-azure-resource-manager.md) ve Kaynak Yöneticisi modunda olduğundan emin olun (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="4d115-110">toobegin, [install and configure hello Azure CLI](../../xplat-cli-azure-resource-manager.md) and make sure you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="4d115-111">Bir verilen hello etiketleri de dahil olmak üzere, bu komutu kullanma için sanal makine, tüm özelliklerini görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4d115-111">You can view all properties for a given Virtual Machine, including hello tags, using this command:</span></span>

        azure vm show -g MyResourceGroup -n MyTestVM

<span data-ttu-id="4d115-112">tooadd hello Azure CLI aracılığıyla yeni bir VM etiket, kullanabileceğiniz hello `azure vm set` hello tag parametresini birlikte komutu **-t**:</span><span class="sxs-lookup"><span data-stu-id="4d115-112">tooadd a new VM tag through hello Azure CLI, you can use hello `azure vm set` command along with hello tag parameter **-t**:</span></span>

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

<span data-ttu-id="4d115-113">tooremove tüm etiketleri, hello kullanabilirsiniz **– T** hello parametresinde `azure vm set` komutu.</span><span class="sxs-lookup"><span data-stu-id="4d115-113">tooremove all tags, you can use hello **–T** parameter in hello `azure vm set` command.</span></span>

        azure vm set – g MyResourceGroup –n MyTestVM -T


<span data-ttu-id="4d115-114">Etiketler tooour kaynakları Azure CLI uyguladığınız ve Portal hello göre bir hello kullanım ayrıntılarını toosee hello etiketleri hello fatura Portalı'nda bakalım.</span><span class="sxs-lookup"><span data-stu-id="4d115-114">Now that we have applied tags tooour resources Azure CLI and hello Portal, let’s take a look at hello usage details toosee hello tags in hello billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="4d115-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4d115-115">Next steps</span></span>
* <span data-ttu-id="4d115-116">Azure kaynaklarınızı etiketleme hakkında daha fazla toolearn bkz [Azure Resource Manager'a genel bakış] [ Azure Resource Manager Overview] ve [etiketleri kullanarak tooorganize Azure kaynaklarınızı] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="4d115-116">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="4d115-117">Etiketler, Azure kaynak kullanımınızı yönetmenize yardımcı olabilir nasıl toosee bkz [Azure faturanızı anlamak] [ Understanding your Azure Bill] ve [Microsoft Azure kaynak tüketimini Öngörüler elde] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="4d115-117">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
