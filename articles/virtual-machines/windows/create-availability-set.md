---
title: "aaaCreate VM kullanılabilirlik kümesi Azure'da | Microsoft Docs"
description: "Nasıl toocreate yönetilen bir kullanılabilirlik kümesi veya yönetilmeyen kullanılabilirlik Azure PowerShell kullanarak, sanal makineleriniz için ayarlamak veya portal hello Resource Manager dağıtım modelinde hello öğrenin."
keywords: "Kullanılabilirlik kümesi"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a3db8659-ace8-4e78-8b8c-1e75c04c042c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eadcdfcd28bb2fa21a4647f207b390c33e022ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a>Bir Azure kullanılabilirlik kümesi oluşturarak artış VM kullanılabilirliği 
Kullanılabilirlik kümeleri artıklık tooyour uygulama sağlar. Bir kullanılabilirlik kümesinde iki veya daha fazla sanal makineyi gruplandırmanız önerilir. Bu yapılandırma ya da planlı veya plansız bir bakım olayı sırasında en az bir sanal makine kullanılabilir ve karşılayan hello %99,95 olmasını sağlar Azure SLA. Daha fazla bilgi için bkz: Merhaba [sanal makineler için SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/).

> [!IMPORTANT]
> Sanal makineleri oluşturulmalıdır hello aynı kaynak grubu hello kullanılabilirlik kümesi olarak.
> 

Bir kullanılabilirlik kümesi, VM toobe parçası istiyorsanız toocreate hello kullanılabilirlik gerekir ayarlamak ilk ya da yazarken, ilk VM hello kümesinde oluşturmakta olduğunuz. VM diskleri yönetilen kullanıyorsanız, hello kullanılabilirlik kümesi yönetilen kullanılabilirlik kümesi oluşturulmuş olması gerekir.

Oluşturma ve kullanılabilirlik kümelerini kullanma hakkında daha fazla bilgi için bkz: [hello sanal makinelerin kullanılabilirliğini yönetme](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="use-hello-portal-toocreate-an-availability-set-before-creating-your-vms"></a>Merhaba portal toocreate kullanılabilirlik kümesi, sanal makineleri oluşturmadan önce kullanın
1. Merhaba hub menüsünde tıklatın **Gözat** seçip **kullanılabilirlik kümeleri**.
2. Merhaba üzerinde **kullanılabilirlik kümeleri dikey**, tıklatın **Ekle**.
   
    ![Merhaba gösteren ekran görüntüsü yeni bir kullanılabilirlik kümesi oluşturmak için düğmesi ekleyin.](./media/create-availability-set/add-availability-set.png)
3. Merhaba üzerinde **kullanılabilirlik kümesi oluştur** dikey penceresinde, kümeniz için tam hello bilgileri.
   
    ![Ekran görüntüsü gösterildiği tooenter toocreate hello kullanılabilirlik gereksinim duyduğunuz bilgileri hello ayarlayın.](./media/create-availability-set/create-availability-set.png)
   
   * **Ad** -hello adı, sayı, harf, nokta, alt çizgi ve tire oluşan 1-80 karakter olmalıdır. Merhaba ilk karakteri bir harf veya sayı olması gerekir. Merhaba son karakter bir harf, sayı veya alt çizgi olmalıdır.
   * **Hata etki alanları** -hata etki alanlarını tanımlayın hello Grup sanal makinelerin, ortak bir güç kaynağı ve ağ anahtarını paylaşır. Varsayılan olarak, hello VM'ler toothree hata etki alanları arasında ayrılır ve değiştirilen toobetween 1 ve 3 olabilir.
   * **Güncelleme etki alanları** - beş güncelleştirme etki alanları, varsayılan olarak atanır ve bu toobetween 1 ve 20 ayarlanabilir. Güncelleme etki alanına belirtmek sanal makineler ve hello yeniden temel alınan fiziksel donanım grupları aynı anda. Örneğin, beş güncelleştirme beşten fazla sanal makine bir tek kullanılabilirlik kümesi içinde hello altıncı sanal makine yapılandırıldığında etki alanları, yerleştirilir hello hello ilk sanal makineye aynı güncelleştirme etki hello seventh içinde belirtirseniz, aynı hello UD hello ikinci sanal makine vb. olarak. Merhaba yeniden başlatmalar Hello sırasını sıralı değil, ancak aynı anda yalnızca tek bir güncelleştirme etki alanı yeniden başlatılacak.
   * **Abonelik** -birden fazla varsa hello abonelik toouse seçin.
   * **Kaynak grubu** -hello okunu ve bir kaynak grubu hello seçerek varolan bir kaynak grubu açılan menüsünü seçin. Ayrıca, bir ad yazarak yeni bir kaynak grubu oluşturabilirsiniz. Merhaba adı aşağıdaki karakterleri hello birini içerebilir: harf, sayı, nokta, tire, alt çizgi ve açma veya kapatma parantezi. Merhaba ad bir nokta ile bitemez. Merhaba VM'ler hello kullanılabilirlik grubundaki tümüne hello oluşturulan toobe ihtiyaç hello kullanılabilirlik kümesi ile aynı kaynak grubunda.
   * **Konum** -hello açılan listeden bir konum seçin.
   * **Yönetilen** - seçin *Evet* toocreate yönetilen kullanılabilirlik toouse yönetilen diskler için depolama kullanan sanal makineler ile ayarlayın. Seçin **Hayır** hello hello ayarlanır VM'ler bir depolama hesabında yönetilmeyen diskler kullanıyorsanız.
   
4. Merhaba bilgi girmeyi tamamladığınızda, tıklatın **oluşturma**. 

## <a name="use-hello-portal-toocreate-a-virtual-machine-and-an-availability-set-at-hello-same-time"></a>Bir sanal makine ve bir kullanılabilirlik kümesi hello aynı hello portal toocreate kullanma zamanı
Merhaba portal kullanarak yeni bir VM oluşturuyorsanız, yeni bir kullanılabilirlik hello oluştururken Merhaba VM kümesi de oluşturabilirsiniz hello kümesindeki ilk VM. VM için toouse yönetilen diskleri seçerseniz, bir yönetilen kullanılabilirlik kümesi oluşturulur.

![Yeni bir kullanılabilirlik hello VM oluştururken kümesi oluşturmak için başlangıç işlemini gösteren ekran görüntüsü.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-tooan-existing-availability-set-in-hello-portal"></a>Merhaba Portalı'nda bir yeni VM tooan varolan kullanılabilirlik kümesi Ekle
Hello kümesinde ait, içinde oluşturduğunuzdan emin olun, oluşturduğunuz her ek VM için aynı hello **kaynak grubu** ve ardından adım 3'te mevcut kullanılabilirlik seçin hello. 

![Tooselect varolan kullanılabilirlik toouse VM için nasıl ayarlanacağını gösteren ekran görüntüsü.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-toocreate-an-availability-set"></a>PowerShell toocreate kullanılabilirlik kullanmak ayarlayın
Bu örnek, kullanılabilirlik adlandırılmış kümesi oluşturur **myAvailabilitySet** hello içinde **myResourceGroup** hello kaynak grubunda **Batı ABD** konumu. Bu hello oluşturmadan önce bitti toobe gereken hello ayarlanır ilk VM.

Başlamadan önce hello hello AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun. Çalıştırma hello komut tooinstall onu.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).


Vm'leriniz için yönetilen diskler kullanıyorsanız yazın:

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

Vm'leriniz için kendi depolama hesapları kullanıyorsanız yazın:

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

Daha fazla bilgi için bkz: [yeni AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).

## <a name="troubleshooting"></a>Sorun giderme
* Oluşturduğunuzda istediğiniz hello kullanılabilirlik kümesini hello portal hello aşağı açılan listesinde, yoksa bir VM, farklı bir kaynak grubu içinde oluşturduktan. Merhaba kaynak grubu, kullanılabilirlik için ayarlayın, Git toohello hub menüsünde ve Gözat'ı tıklatın bilmiyorsanız > kullanılabilirlik kümeleri, kullanılabilirlik listesini ayarlar ve hangi kaynak grupları ait oldukları toosee.

## <a name="next-steps"></a>Sonraki adımlar
Ek depolama alanı tooyour VM ek ekleyerek [veri diski](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

