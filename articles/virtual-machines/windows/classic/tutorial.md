---
title: aaaCreate VM hello Azure portal ile | Microsoft Docs
description: "Bir Windows sanal makine hello Azure portal oluşturun."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a>Windows hello Azure portalı çalıştıran bir sanal makine oluşturma
> [!div class="op_single_selector"]
> * [Azure portal](tutorial.md)
> * [PowerShell: Klasik dağıtım](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Nasıl çok öğrenin[hello Resource Manager dağıtım modelini kullanarak bu adımları uygulamadan](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello kullanarak **Azure portal**.

Bu öğretici şunların nasıl yapıldığını gösterir toocreate Azure Windows hello Azure portalı çalıştıran sanal makine (VM). Örnek olarak bir Windows Server görüntüsü kullanacağız, ancak yalnızca bir Merhaba birçok görüntüleri Azure sunar. Görüntü seçenekleriniz aboneliğinize göre değişir unutmayın. Örneğin, Windows Masaüstü görüntülerini kullanılabilir tooMSDN abone olabilir.

Bu bölümde, nasıl gösterilir toouse hello **Pano** Azure portal tooselect hello ve hello sanal makine oluşturun.

Kullanarak sanal makineleri oluşturabilirsiniz [kendi görüntüleri](createupload-vhd.md). toolearn bu ve diğer yöntemler hakkında bkz [farklı şekillerde toocreate Windows sanal makine](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <a id="createvirtualmachine"></a>Hello sanal makine oluşturma
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[hello Resource Manager dağıtım modeli kullanarak bir VM oluşturma](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello Azure Portalı'nda.
* Toohello sanal makinede oturum açın. Yönergeler için bkz: [tooa sanal Windows Server çalıştıran makinede oturum](connect-logon.md).
* Bir disk toostore veri ekleyin. Boş diskleri ve verileri içeren diskleri ekleyebilirsiniz. Merhaba yönergeler için bkz [bir veri diski tooa Windows hello Klasik dağıtım modeliyle oluşturulan sanal makinenin ekleme](attach-disk.md).
