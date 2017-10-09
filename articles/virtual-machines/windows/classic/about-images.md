---
title: "Windows sanal makineler için aaaAbout görüntüleri | Microsoft Docs"
description: "Görüntüleri azure'da Windows sanal makinelerle kullanılma hakkında bilgi edinin."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cynthn
ms.openlocfilehash: c7cfa1d018a5e99d5b68f559ec9ae1f14e4dec8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="about-images-for-windows-virtual-machines"></a>Windows sanal makineler için görüntüler hakkında
> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Bulma ve hello Resource Manager modelinde görüntüleri kullanma hakkında daha fazla bilgi için bkz: [burada](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a>İmajlarla çalışma

Hello Azure PowerShell modülü ve hello Azure portal toomanage hello görüntüleri kullanılabilir tooyour Azure aboneliği kullanabilirsiniz. Hello Azure PowerShell modülü, tam olarak ne saptayabilirler şekilde daha fazla komut seçenekleri sağlar toosee istediğiniz ya da yapın. Hello Azure portal GUI hello gündelik yönetim görevlerinin çoğunu sağlar.

Hello Azure PowerShell modülünü kullanan bazı örnekler şunlardır.

* **Tüm görüntüleri alma**:`Get-AzureVMImage`geçerli aboneliğinizdeki kullanılabilir tüm hello görüntüleri listesini döndürür: görüntüleri ve Azure veya iş ortakları tarafından sağlanan. Merhaba sonuç listesi büyük olabilir. sonraki örneklerde nasıl hello tooget daha kısa bir liste.
* **Görüntü aileleri alma**:`Get-AzureVMImage | select ImageFamily` dizeleri göstererek görüntü aileleri listesini alır **ImageFamily** özelliği.
* **Belirli bir ailesinde tüm görüntüleri alma**:`Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`
* **VM görüntüleri Bul**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` yalnızca tooVM görüntülerini uygular hello DataDiskConfiguration özelliği filtreleyerek Bu cmdlet'i çalışır. Bu örnek ayrıca etiket ve resim hello çıktı tooonly hello adı filtreler.
* **Genelleştirilmiş bir yansıma Kaydet**:`Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`
* **Özel bir yansıma Kaydet**:`Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`

  > [!TIP]
  > Merhaba OSState parametresi gerekli toocreate hello işletim sistemi diski içerir ve veri diskleri ekli bir VM görüntüsü ' dir. Merhaba parametreyi kullanmazsanız hello cmdlet'i bir işletim sistemi görüntüsü oluşturur. Merhaba hello parametresinin değerini gösterir hello görüntü genelleştirilmiş veya özelleştirilmiş olup olmadığını dayalı hello işletim sistemi diski yeniden kullanılmak üzere hazırlanmıştır olup olmadığı.

* **Bir görüntü Sil**:`Remove-AzureVMImage –ImageName "MyOldVmImage"`

## <a name="next-steps"></a>Sonraki Adımlar
Ayrıca [hello Azure portal kullanarak bir Windows makinesine oluşturma](tutorial.md).
