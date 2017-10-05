---
title: "Bir Linux VM için bir veri diski ekleme | Microsoft Docs"
description: "Bir Linux VM Resource Manager dağıtım modelini kullanarak Azure portalında yeni veya var olan veri diski ekleme yapma."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 1599ee241c3d9fb3623ebd89ae30f2795cae1930
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-attach-a-data-disk-to-a-linux-vm-in-the-azure-portal"></a>Nasıl bir Linux VM Azure portalında bir veri diski ekleme
Bu makalede Azure portalı üzerinden Linux sanal makine için yeni ve mevcut diskleri ekleme gösterilmiştir. Ayrıca [bir Windows VM Azure portalında bir veri diski ekleme](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Azure diskleri yönetilen veya yönetilmeyen diskler kullanmayı da tercih edebilirsiniz. Yönetilen diskleri Azure platformu tarafından işlenir ve hazırlık veya konum depolamaya gerektirmez. Yönetilmeyen diskler bir depolama hesabı gerektirir ve bazı [kotalar ve uygulama sınırlar](../../azure-subscription-service-limits.md#storage-limits). Azure Yönetilen Diskler hakkında daha fazla bilgi için bkz. [Azure Yönetilen Disklere genel bakış](../windows/managed-disks-overview.md).

VM'nize diskleri eklemeden önce bu ipuçlarını gözden geçirin:

* Sanal makinenin boyutunu, iliştirebilirsiniz kaç tane veri diskleri denetler. Ayrıntılar için bkz [sanal makineler için Boyutlar](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Premium depolama kullanmak için DS serisi veya GS serisi bir sanal makine gerekir. Bu sanal makinelerle Premium ve standart diskler kullanabilirsiniz. Premium depolama belirli bölgelerde kullanılabilir. Ayrıntılar için bkz [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Sanal makinelere bağlı diskler Azure'da depolanan gerçekte .vhd dosyalarıdır. Ayrıntılar için bkz [diskler ve sanal makineler için VHD'ler hakkında](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="find-the-virtual-machine"></a>Sanal makine bulunamadı
1. [Azure Portal](https://portal.azure.com/) oturum açın.
2. Hub menüsünde, **Virtual Machines**’e tıklayın.
3. Listeden sanal makineyi seçin.
4. Sanal makineleri dikey penceresinde de **Essentials**, tıklatın **diskleri**.
   
    ![Disk Ayarları'nı açın](./media/attach-disk-portal/find-disk-settings.png)

Ya da eklemek için aşağıdaki yönergeleri tarafından devam bir [yönetilen disk](#use-azure-managed-disks) veya [yönetilmeyen disk](#use-unmanaged-disks).

## <a name="use-azure-managed-disks"></a>Azure yönetilen diskleri kullanın

### <a name="attach-a-new-disk"></a>Yeni bir diski kullanıma açın

1. Üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.
2. Aşağı açılan menüsüne tıklayın **adı** seçip **oluşturma disk**:

    ![Azure oluşturmak yönetilen disk](./media/attach-disk-portal/create-new-md.png)

3. Yönetilen disk için bir ad girin. Varsayılan ayarları gözden geçirin, gerektiği gibi güncelleştirin ve ardından **oluşturma**.
   
   ![Disk ayarlarını gözden geçirin](./media/attach-disk-portal/create-new-md-settings.png)

4. Tıklatın **kaydetmek** yönetilen disk oluşturmak ve VM yapılandırmasını güncelleştirmek için:

   ![Yeni Azure diski yönetilen Kaydet](./media/attach-disk-portal/confirm-create-new-md.png)

5. Azure disk oluşturur ve sanal makineye iliştirir sonra yeni disk sanal makinenin disk ayarları altında listelenen **veri diskleri**. Yönetilen diskleri en üst düzey bir kaynak olduğundan, diskin kaynak grubu kökünde görünür:

   ![Kaynak grubundaki yönetilen Azure Disk](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a>Var olan bir diski ekleme
1. Üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.
2. Aşağı açılan menüsüne tıklayın **adı** Azure aboneliğinize erişilebilir olan yönetilen disklerin listesini görüntülemek için. Yönetilen bir disk eklemek için seçin:

   ![Yönetilen mevcut Azure diski ekleme](./media/attach-disk-portal/select-existing-md.png)

3. Tıklatın **kaydetmek** mevcut yönetilen diski ekleyin ve VM yapılandırmasını güncelleştirmek için:
   
   ![Azure yönetilen diski güncelleştirmelerini kaydedin](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. Azure disk sanal makineye iliştirir sonra sanal makinenin disk ayarları altında listelenen **veri diskleri**.

## <a name="use-unmanaged-disks"></a>Yönetilmeyen diskleri kullanın

### <a name="attach-a-new-disk"></a>Yeni bir diski kullanıma açın

1. Üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.
2. Varsayılan ayarları gözden geçirin, gerektiği gibi güncelleştirin ve ardından **Tamam**.
   
   ![Disk ayarlarını gözden geçirin](./media/attach-disk-portal/attach-new.png)
3. Azure disk oluşturur ve sanal makineye iliştirir sonra yeni disk sanal makinenin disk ayarları altında listelenen **veri diskleri**.

### <a name="attach-an-existing-disk"></a>Var olan bir diski ekleme
1. Üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.
2. Altında **varolan bir diski İlişti**, tıklatın **VHD dosyasını**.
   
   ![Varolan bir diski kullanıma açın](./media/attach-disk-portal/attach-existing.png)
3. Altında **depolama hesapları**, .vhd dosyası tutan kapsayıcı ve hesabı seçin.
   
   ![VHD konumunu bulma](./media/attach-disk-portal/find-storage-container.png)
4. .Vhd dosyasını seçin.
5. Altında **varolan bir diski İlişti**, seçtiğiniz dosya altında listelenen **VHD dosyasını**. **Tamam** düğmesine tıklayın.
6. Azure disk sanal makineye iliştirir sonra sanal makinenin disk ayarları altında listelenen **veri diskleri**.


## <a name="next-steps"></a>Sonraki adımlar
Disk eklendikten sonra kullanım için hazırlamanız gerekir. Daha fazla bilgi için bkz: [nasıl yapılır: Linux yeni bir veri diski başlatma](add-disk.md).
