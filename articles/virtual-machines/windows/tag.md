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
# <a name="how-tootag-a-windows-virtual-machine-in-azure"></a>Nasıl tootag azure'da Windows sanal makine
Bu makalede farklı şekillerde tootag hello Resource Manager dağıtım modeli üzerinden Windows sanal makine azure'da açıklanmaktadır. Etiketler doğrudan bir kaynağa veya bir kaynak grubu yerleştirilen kullanıcı tanımlı anahtar/değer çiftleridir. Azure şu anda'kaynak ve kaynak grubu başına too15 etiketlerini destekler. Etiketleri hello oluşturma sırasında bir kaynakta yerleştirilebilir veya tooan mevcut kaynak eklendi. Etiketler hello Resource Manager dağıtım modeli yalnızca oluşturulan kaynaklar için desteklendiğini unutmayın. Linux sanal makine tootag istiyorsanız, bkz: [nasıl tootag azure'da bir Linux sanal makine](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a>PowerShell ile etiketleme
toocreate, ekleme ve PowerShell aracılığıyla etiketleri silme, Yukarı önce tooset gerekir, [PowerShell ortam Azure Resource Manager ile][PowerShell environment with Azure Resource Manager]. Merhaba Kurulum tamamlandığında, etiketler oluşturma veya hello kaynak PowerShell yoluyla oluşturulduktan sonra işlem, ağ ve depolama kaynakları yerleştirebilirsiniz. Bu makalede, görüntüleme ve düzenleme etiketleri sanal makinelerde yerleştirilen hakkında odaklanacaktır.

İlk olarak, hello aracılığıyla sanal makine tooa gidin `Get-AzureRmVM` cmdlet'i.

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

Sanal makineniz etiketleri içeriyorsa, tüm hello etiketleri, kaynakta sonra görürsünüz:

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

PowerShell aracılığıyla tooadd etiketleri isterseniz hello kullanabilirsiniz `Set-AzureRmResource` komutu. PowerShell aracılığıyla etiketler güncelleştirilirken etiketleri bir bütün olarak güncelleştirilir unutmayın. Bu nedenle etiketleri zaten olan bir etiketi tooa kaynak ekliyorsanız, hello kaynakta yerleştirilen toobe istediğiniz tüm hello etiketleri tooinclude gerekir. Aşağıda nasıl tooadd ek PowerShell cmdlet'leri aracılığıyla tooa kaynak etiketler, bir örnek verilmiştir.

Bu ilk cmdlet'i tüm getirilen hello etiketlerin ayarlar *MyTestVM* toohello *$tags* hello kullanarak değişken `Get-AzureRmResource` ve `Tags` özelliği.

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

Merhaba ikinci komutu değişkeni verilen hello hello etiketleri görüntüler.

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

Merhaba üçüncü komut ekler ek etiketi toohello *$tags* değişkeni. Not hello hello  **+=**  tooappend hello yeni anahtar/değer çifti toohello *$tags* listesi.

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

Merhaba dördüncü komut hello etiketleri hello tanımlanan tüm ayarlar *$tags* kaynak verilen değişken toohello. Bu durumda, MyTestVM olur.

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

Merhaba beşinci komut tüm hello etiketlerin hello kaynakta görüntüler. Gördüğünüz gibi *konumu* şimdi bir etiketle olarak tanımlanan *MyLocation* hello değeri olarak.

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

hakkında daha fazla bilgi toolearn PowerShell aracılığıyla etiketlemeyi hello denetle [Azure kaynak cmdlet'leri][Azure Resource Cmdlets].

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>Sonraki adımlar
* Azure kaynaklarınızı etiketleme hakkında daha fazla toolearn bkz [Azure Resource Manager'a genel bakış] [ Azure Resource Manager Overview] ve [etiketleri kullanarak tooorganize Azure kaynaklarınızı] [ Using Tags tooorganize your Azure Resources].
* Etiketler, Azure kaynak kullanımınızı yönetmenize yardımcı olabilir nasıl toosee bkz [Azure faturanızı anlamak] [ Understanding your Azure Bill] ve [Microsoft Azure kaynak tüketimini Öngörüler elde] [Gain insights into your Microsoft Azure resource consumption].

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
