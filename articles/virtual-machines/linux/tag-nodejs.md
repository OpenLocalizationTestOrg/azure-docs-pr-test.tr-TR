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
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a>Nasıl tootag azure'da bir Linux sanal makine
Bu makalede farklı şekillerde tootag Linux sanal makine azure'da hello Resource Manager dağıtım modeli üzerinden açıklanmaktadır. Etiketler doğrudan bir kaynağa veya bir kaynak grubu yerleştirilen kullanıcı tanımlı anahtar/değer çiftleridir. Azure şu anda'kaynak ve kaynak grubu başına too15 etiketlerini destekler. Etiketleri hello oluşturma sırasında bir kaynakta yerleştirilebilir veya tooan mevcut kaynak eklendi. Lütfen unutmayın, etiketleri hello Resource Manager dağıtım modeli yalnızca oluşturulan kaynaklar için desteklenir.

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a>Azure CLI ile etiketleme
toobegin, [hello Azure CLI yükleyip](../../xplat-cli-azure-resource-manager.md) ve Kaynak Yöneticisi modunda olduğundan emin olun (`azure config mode arm`).

Bir verilen hello etiketleri de dahil olmak üzere, bu komutu kullanma için sanal makine, tüm özelliklerini görüntüleyebilirsiniz:

        azure vm show -g MyResourceGroup -n MyTestVM

tooadd hello Azure CLI aracılığıyla yeni bir VM etiket, kullanabileceğiniz hello `azure vm set` hello tag parametresini birlikte komutu **-t**:

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

tooremove tüm etiketleri, hello kullanabilirsiniz **– T** hello parametresinde `azure vm set` komutu.

        azure vm set – g MyResourceGroup –n MyTestVM -T


Etiketler tooour kaynakları Azure CLI uyguladığınız ve Portal hello göre bir hello kullanım ayrıntılarını toosee hello etiketleri hello fatura Portalı'nda bakalım.

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>Sonraki adımlar
* Azure kaynaklarınızı etiketleme hakkında daha fazla toolearn bkz [Azure Resource Manager'a genel bakış] [ Azure Resource Manager Overview] ve [etiketleri kullanarak tooorganize Azure kaynaklarınızı] [ Using Tags tooorganize your Azure Resources].
* Etiketler, Azure kaynak kullanımınızı yönetmenize yardımcı olabilir nasıl toosee bkz [Azure faturanızı anlamak] [ Understanding your Azure Bill] ve [Microsoft Azure kaynak tüketimini Öngörüler elde] [Gain insights into your Microsoft Azure resource consumption].

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
