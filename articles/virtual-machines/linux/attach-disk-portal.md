---
title: bir veri diski tooa Linux VM aaaAttach | Microsoft Docs
description: "Nasıl tooattach yeni veya var olan veri diski tooa Linux VM Azure portal kullanarak hello Resource Manager dağıtım modeli hello."
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
ms.openlocfilehash: 069c3c6f5e71a8c495342e6d0c6f3d92c4ed5053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-vm-in-hello-azure-portal"></a>Nasıl tooattach bir veri diski hello Azure portal'ın tooa Linux VM
Bu makalede nasıl tooattach hem yeni hem de mevcut hello Azure portal aracılığıyla tooa Linux sanal makine disklerini gösterilmektedir. Ayrıca [hello Azure portal'ın bir veri diski tooa Windows VM ekleme](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Toouse yönetilen ya da Azure diskleri seçin veya yönetilmeyen diskler. Yönetilen diskleri hello Azure platformu tarafından işlenir ve hazırlık veya konumu toostore gerektirmeyen bunları. Yönetilmeyen diskler bir depolama hesabı gerektirir ve bazı [kotalar ve uygulama sınırlar](../../azure-subscription-service-limits.md#storage-limits). Azure Yönetilen Diskler hakkında daha fazla bilgi için bkz. [Azure Yönetilen Disklere genel bakış](../windows/managed-disks-overview.md).

Diskleri tooyour VM eklemeden önce bu ipuçlarını gözden geçirin:

* Merhaba boyutunu hello sanal makine, iliştirebilirsiniz kaç tane veri diskleri denetler. Ayrıntılar için bkz [sanal makineler için Boyutlar](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Premium depolama toouse, DS serisi veya GS serisi bir sanal makine gerekir. Bu sanal makinelerle Premium ve standart diskler kullanabilirsiniz. Premium depolama belirli bölgelerde kullanılabilir. Ayrıntılar için bkz [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Diskleri ekli toovirtual makineleri Azure'da depolanan gerçekte .vhd dosyalarıdır. Ayrıntılar için bkz [diskler ve sanal makineler için VHD'ler hakkında](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="find-hello-virtual-machine"></a>Merhaba sanal makine bulunamadı
1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Merhaba Hub menüsünde **sanal makineleri**.
3. Merhaba sanal makine hello listeden seçin.
4. toohello sanal makineleri dikey penceresinde de **Essentials**, tıklatın **diskleri**.
   
    ![Disk Ayarları'nı açın](./media/attach-disk-portal/find-disk-settings.png)

Ya da eklemek için aşağıdaki yönergeleri tarafından devam bir [yönetilen disk](#use-azure-managed-disks) veya [yönetilmeyen disk](#use-unmanaged-disks).

## <a name="use-azure-managed-disks"></a>Azure yönetilen diskleri kullanın

### <a name="attach-a-new-disk"></a>Yeni bir diski kullanıma açın

1. Merhaba üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.
2. Merhaba açılan menüsüne tıklayın **adı** seçip **oluşturma disk**:

    ![Azure oluşturmak yönetilen disk](./media/attach-disk-portal/create-new-md.png)

3. Yönetilen disk için bir ad girin. Merhaba varsayılan ayarları gözden geçirin, gerektiği gibi güncelleştirin ve ardından **oluşturma**.
   
   ![Disk ayarlarını gözden geçirin](./media/attach-disk-portal/create-new-md-settings.png)

4. Tıklatın **kaydetmek** toocreate hello yönetilen disk ve güncelleştirme hello VM yapılandırması:

   ![Yeni Azure diski yönetilen Kaydet](./media/attach-disk-portal/confirm-create-new-md.png)

5. Azure hello disk oluşturur ve toohello sanal makineye iliştirir sonra hello yeni disk hello sanal makinenin disk ayarları altında listelenen **veri diskleri**. Yönetilen diskleri en üst düzey bir kaynak olduğundan, hello disk hello hello kaynak grubu kökünde görüntülenir:

   ![Kaynak grubundaki yönetilen Azure Disk](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a>Var olan bir diski ekleme
1. Merhaba üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.
2. Merhaba açılan menüsüne tıklayın **adı** tooview varolan listesini yönetilen diskleri erişilebilir tooyour Azure aboneliği. Select hello disk tooattach yönetilen:

   ![Yönetilen mevcut Azure diski ekleme](./media/attach-disk-portal/select-existing-md.png)

3. Tıklatın **kaydetmek** tooattach hello varolan yönetilen disk ve güncelleştirme hello VM yapılandırması:
   
   ![Azure yönetilen diski güncelleştirmelerini kaydedin](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. Disk toohello sanal makine Azure ekler hello sonra hello sanal makinenin disk ayarları altında listelenen **veri diskleri**.

## <a name="use-unmanaged-disks"></a>Yönetilmeyen diskleri kullanın

### <a name="attach-a-new-disk"></a>Yeni bir diski kullanıma açın

1. Merhaba üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.
2. Merhaba varsayılan ayarları gözden geçirin, gerektiği gibi güncelleştirin ve ardından **Tamam**.
   
   ![Disk ayarlarını gözden geçirin](./media/attach-disk-portal/attach-new.png)
3. Azure hello disk oluşturur ve toohello sanal makineye iliştirir sonra hello yeni disk hello sanal makinenin disk ayarları altında listelenen **veri diskleri**.

### <a name="attach-an-existing-disk"></a>Var olan bir diski ekleme
1. Merhaba üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.
2. Altında **varolan bir diski İlişti**, tıklatın **VHD dosyasını**.
   
   ![Varolan bir diski kullanıma açın](./media/attach-disk-portal/attach-existing.png)
3. Altında **depolama hesapları**, hello hesabınızı ve hello .vhd dosyası tutan kapsayıcı.
   
   ![VHD konumunu bulma](./media/attach-disk-portal/find-storage-container.png)
4. Merhaba .vhd dosyasını seçin.
5. Altında **varolan bir diski İlişti**, seçtiğiniz hello dosya altında listelenen **VHD dosyasını**. **Tamam** düğmesine tıklayın.
6. Disk toohello sanal makine Azure ekler hello sonra hello sanal makinenin disk ayarları altında listelenen **veri diskleri**.


## <a name="next-steps"></a>Sonraki adımlar
Merhaba disk eklendikten sonra tooprepare gereksinim için kullanın. Daha fazla bilgi için bkz: [nasıl yapılır: Linux yeni bir veri diski başlatma](add-disk.md).
