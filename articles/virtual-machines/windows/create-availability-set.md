---
title: "Azure üzerinde ayarlanmış bir VM kullanılabilirlik oluştur | Microsoft Docs"
description: "Yönetilen kullanılabilirlik kümesi veya yönetilmeyen kullanılabilirlik Azure PowerShell veya portal Resource Manager dağıtım modelinde kullanarak, sanal makineleriniz kümesi oluşturmayı öğrenin."
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
ms.openlocfilehash: e813ade8e105169f21138ed8a8eafda1ff39f42e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a>Bir Azure kullanılabilirlik kümesi oluşturarak artış VM kullanılabilirliği 
Kullanılabilirlik kümeleri, uygulamanız için artıklık sağlar. Bir kullanılabilirlik kümesinde iki veya daha fazla sanal makineyi gruplandırmanız önerilir. Bu yapılandırma ya da planlı veya plansız bir bakım olayı sırasında en az bir sanal makinenin kullanılabilir durumda olmasını ve %99,95 karşıladığından emin sağlar Azure SLA. Daha fazla bilgi için bkz. [Sanal Makineler için SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/).

> [!IMPORTANT]
> Sanal makineleri kullanılabilirlik kümesi ile aynı kaynak grubunda oluşturulması gerekir.
> 

Bir kullanılabilirlik kümesinin parçası olarak, VM istiyorsanız, önce ayarlamanız kullanılabilirlik oluşturmanız gerekir veya kümesindeki ilk VM oluştururken. VM diskleri yönetilen kullanıyorsanız, kullanılabilirlik kümesi yönetilen kullanılabilirlik kümesi oluşturulmuş olması gerekir.

Oluşturma ve kullanılabilirlik kümelerini kullanma hakkında daha fazla bilgi için bkz: [sanal makinelerin kullanılabilirliğini yönetme](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="use-the-portal-to-create-an-availability-set-before-creating-your-vms"></a>Kullanılabilirlik kümesi, sanal makineleri oluşturmadan önce oluşturmak üzere portalı kullanın
1. Hub menüsünde tıklatın **Gözat** seçip **kullanılabilirlik kümeleri**.
2. Üzerinde **kullanılabilirlik kümeleri dikey**, tıklatın **Ekle**.
   
    ![Yeni kullanılabilirlik oluşturmak için Ekle düğmesini gösteren ekran görüntüsü ayarlayın.](./media/create-availability-set/add-availability-set.png)
3. Üzerinde **kullanılabilirlik kümesi oluştur** dikey penceresinde, kümeniz için bilgileri tamamlayın.
   
    ![Kullanılabilirlik kümesi oluşturmak için girmenize gerek bilgileri gösteren ekran görüntüsü.](./media/create-availability-set/create-availability-set.png)
   
   * **Ad** -ad rakam, harf, nokta, alt çizgi ve tire oluşan 1-80 karakterden uzun olmalıdır. İlk karakteri bir harf veya sayı olması gerekir. Son karakter bir harf, sayı veya alt çizgi olmalıdır.
   * **Hata etki alanları** -hata etki alanlarını tanımlayın ortak bir güç kaynağı ve ağ anahtarı paylaşmak sanal makineler grubudur. Varsayılan olarak, sanal makineleri en çok üç hata etki alanlarında ayrılır ve 1 ile 3 arasında değiştirilebilir.
   * **Güncelleme etki alanları** - beş güncelleştirme etki alanları, varsayılan olarak atanır ve bu 1 ve 20 arasında ayarlanabilir. Güncelleme etki alanına sanal makineler ve aynı anda yeniden temel alınan fiziksel donanım grupları belirtin. Örneğin, beşten fazla sanal makine kullanılabilirlik tek bir kümesi içinde yapılandırıldığında beş güncelleme etki alanları, belirtirseniz, altıncı sanal makine ilk sanal makineye aynı UD ikinci sanal makine olarak yedinci aynı güncelleştirme etki yerleştirilir ve benzeri. Yeniden başlatma sırasını sıralı değil, ancak aynı anda yalnızca tek bir güncelleştirme etki alanı yeniden başlatılacak.
   * **Abonelik** -birden fazla varsa, kullanılacak aboneliği seçin.
   * **Kaynak grubu** -oka tıklayarak ve aşağı açılan listeden bir kaynak grubu seçerek varolan bir kaynak grubu seçin. Ayrıca, bir ad yazarak yeni bir kaynak grubu oluşturabilirsiniz. Ad aşağıdaki karakterlerden herhangi birini içerebilir: harf, sayı, nokta, tire, alt çizgi ve açma veya kapatma parantezi. Ad bir nokta ile bitemez. Tüm sanal makineleri kullanılabilirlik grubundaki kullanılabilirlik kümesi ile aynı kaynak grubunda oluşturulması gerekir.
   * **Konum** -açılan listeden bir konum seçin.
   * **Yönetilen** - seçin *Evet* yönetilen diskler için depolama kullanan sanal makineler ile kullanmak üzere ayarlanmış yönetilen bir kullanılabilirlik oluşturmak için. Seçin **Hayır** kümesinde olacak VM'ler yönetilmeyen diskler bir depolama hesabı kullanıyorsanız.
   
4. İşiniz bittiğinde bilgileri girerek, tıklatın **oluşturma**. 

## <a name="use-the-portal-to-create-a-virtual-machine-and-an-availability-set-at-the-same-time"></a>Bir sanal makine ve kullanılabilirlik aynı anda kümesi oluşturmak üzere portalı kullanın
Portalı'nı kullanarak yeni bir VM oluşturuyorsanız, yeni bir kullanılabilirlik kümesinde ilk VM oluştururken VM için kümesi de oluşturabilirsiniz. VM için yönetilen diskleri kullanmayı seçerseniz, bir yönetilen kullanılabilirlik kümesi oluşturulur.

![Yeni bir kullanılabilirlik VM oluştururken kümesi oluşturmayı gösteren ekran görüntüsü.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-to-an-existing-availability-set-in-the-portal"></a>Var olan kullanılabilirlik kümesi Portalı'nda yeni bir VM ekleme
Kümeye ait olan, oluşturduğunuz her ek VM için onu aynı oluşturduğunuzdan emin olun **kaynak grubu** ve var olan kullanılabilirlik adım 3'te kümesini seçin. 

![VM için kullanmak üzere bir var olan kullanılabilirlik kümesi seçme gösteren ekran görüntüsü.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-to-create-an-availability-set"></a>Bir kullanılabilirlik kümesi oluşturmak için PowerShell kullanın
Bu örnek, kullanılabilirlik adlandırılmış kümesi oluşturur **myAvailabilitySet** içinde **myResourceGroup** kaynak grubunda **Batı ABD** konumu. Bu kümede yer alacak ilk VM oluşturmadan önce yapılmalıdır.

Başlamadan önce AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun. Yüklemek için aşağıdaki komutu çalıştırın.

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
* Portal aşağı açılan listesinde, istediğiniz kullanılabilirlik kümesi değilse, bir VM oluştururken farklı kaynak grubunda oluşturduğunuz. Kaynak grubu, kullanılabilirlik için ayarlayın, hub menüsüne gidin ve Gözat'ı bilmiyorsanız > kullanılabilirlik kümeleri, kullanılabilirlik kümeleri ve hangi listesini görmek için kaynak gruplarını ait oldukları.

## <a name="next-steps"></a>Sonraki adımlar
Ek depolama alanı, VM için ek bir ekleyerek [veri diski](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

