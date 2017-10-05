---
title: "Azure depolama hesapları, kapsayıcıları veya VHD'leri sildiğinizde hatalarında sorun giderme | Microsoft Docs"
description: "Azure depolama hesapları, kapsayıcıları veya VHD'leri sildiğinizde hatalarında sorun giderme"
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 11944dd38b1cc30106c0b76a108480c018ca39d4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a>Azure depolama hesapları, kapsayıcıları veya VHD'leri sildiğinizde hatalarında sorun giderme

Bir Azure depolama hesabı, kapsayıcı ya da sanal sabit disk (VHD) silmeye çalıştığınızda, hatalar alabilirsiniz [Azure portal](https://portal.azure.com). Bu makalede Azure Resource Manager dağıtımında sorunu gidermek için sorun giderme kılavuzu verilmiştir.

Bu makalede Azure sorununuzu adresi değil, üzerinde Azure forumları ziyaret [MSDN ve yığın taşması](https://azure.microsoft.com/support/forums/). Bu forumları veya çok sorununuzu nakledebilirsiniz @AzureSupport Twitter'da. Ayrıca, size bir Azure destek isteği seçerek dosya **alma desteği** üzerinde [Azure Destek](https://azure.microsoft.com/support/options/) site.

## <a name="symptoms"></a>Belirtiler
### <a name="scenario-1"></a>Senaryo 1
Resource Manager dağıtım depolama hesabında bir VHD silmeye çalıştığınızda, aşağıdaki hata iletisini alıyorsunuz:

**BLOB 'vhds/BlobName.vhd' silinemedi. Hata: Yoktur şu anda bir kira blob üzerindeki ve istekte hiçbir kiralama kimliği belirtildi.**

Bir sanal makine (VM), silmeyi denediğiniz VHD üzerinde bir kira olduğundan bu sorun oluşabilir.

### <a name="scenario-2"></a>Senaryo 2
Resource Manager dağıtım depolama hesabında bir kapsayıcı silmeye çalıştığınızda, aşağıdaki hata iletisini alıyorsunuz:

**Depolama kapsayıcısı 'VHD'ler' silinemedi. Hata: Yoktur şu anda bir kira kapsayıcısını ve istekte hiçbir kiralama kimliği belirtildi.**

Kapsayıcı kira durumda kilitli bir VHD olduğundan bu sorun oluşabilir.

### <a name="scenario-3"></a>Senaryo 3
Resource Manager dağıtım bir depolama hesabını silmeye çalıştığınızda, aşağıdaki hata iletisini alıyorsunuz:

**Depolama hesabı 'StorageAccountName' silinemedi. Hata: Depolama hesabına ait yapıtlar kullanımda nedeniyle silinemiyor.**

Depolama hesabı kira durumuna sahip bir VHD içerdiğinden bu sorun oluşabilir.

## <a name="solution"></a>Çözüm 
Bu sorunları gidermek için hataya neden olan VHD ve ilişkili VM tanımlamanız gerekir. Ardından, VM (için veri diskleri) VHD'den detach veya VHD (işletim sistemi diskler için) kullanarak VM silin. Bu kira VHD'den kaldırır ve silinmesine izin verir. 

Bunu yapmak için aşağıdaki yöntemlerden birini kullanın:

### <a name="method-1---use-azure-storage-explorer"></a>Yöntem 1 - kullanım Azure storage Gezgini

### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a>Adım 1 depolama hesabı silinmesini engellemek VHD tanımlayın

1. Depolama hesabı sildiğinizde, ileti iletişim kutusu aşağıdaki gibi alır: 

    ![Depolama hesabını silme iletisi](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Denetleme **Disk URL** depolama belirlemek için hesap ve engelleyen VHD depolama hesabını silme. Aşağıdaki örnekte, dize önce ". blob.core.windows.net" depolama hesabı adı ve "SCCM2012-2015-08-28.vhd" VHD adı.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-the-vhd-by-using-azure-storage-explorer"></a>2. adım, Azure Storage Gezgini kullanarak VHD silme

1. En son sürümünü karşıdan yükleyip [Azure Storage Gezgini](http://storageexplorer.com/). Bu araç, Windows, macOS ve Linux Azure Storage ile kolayca çalışmanızı sağlayan Microsoft bir tek başına uygulamadır.
2. Azure Depolama Gezgini'ni açın ve seçin ![hesabı simgesi](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) Sol çubuğunda, Azure ortamınıza seçin ve ardından oturum açın.

3. Tüm abonelikleri veya silmek istediğiniz depolama hesabını içeren bir abonelik seçin.

    ![Abonelik Ekle](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. Biz disk URL'den daha önce edindiğiniz depolama hesabı gidin **Blob kapsayıcıları** > **VHD'ler** ve arama engelleyen VHD için depolama hesabı silin.
5. VHD bulunursa, denetleme **VM adı** bu VHD kullanarak VM bulmak için sütun.

    ![VM denetleyin](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. Kira VHD'den Azure portalını kullanarak kaldırın. Daha fazla bilgi için bkz: [kira VHD'den kaldırmak](#remove-the-lease-from-the-vhd). 

7. Azure depolama Gezgini'ne gidin, VHD'yi sağ tıklayın ve ardından Sil'i seçin.

8. Depolama hesabını silin.

### <a name="method-2---use-azure-portal"></a>Yöntem 2 - Azure portalı 

#### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a>1. adım: depolama hesabı silinmesini engellemek VHD tanımlayın

1. Depolama hesabı sildiğinizde, ileti iletişim kutusu aşağıdaki gibi alır: 

    ![Depolama hesabını silme iletisi](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Denetleme **Disk URL** depolama belirlemek için hesap ve engelleyen VHD depolama hesabını silme. Aşağıdaki örnekte, dize önce ". blob.core.windows.net" depolama hesabı adı ve "SCCM2012-2015-08-28.vhd" VHD adı.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. [Azure Portal](https://portal.azure.com) oturum açın.
3. Hub menüsünde seçin **tüm kaynakları**. Depolama hesabına gidin ve ardından **BLOB'lar** > **VHD'ler**.

    ![Depolama hesabı ve vurgulanmış "VHD" kapsayıcı portalı ekran görüntüsü](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. Biz disk URL'den daha önce edindiğiniz VHD'yi bulun. Ardından, VM kullanan belirlemek VHD. Genellikle, VHD adını kontrol ederek VHD VM tutan belirleyebilirsiniz:

Resource Manager geliştirme modelini VM

   * İşletim sistemi disk genellikle bu adlandırma kuralını izleyin: VMName-YYYY-AA-GG-HHMMSS.vhd
   * Veri diskleri genellikle bu adlandırma kuralını izleyin: VMName-YYYY-AA-GG-HHMMSS.vhd

VM Klasik geliştirme modeli

   * İşletim sistemi disk genellikle bu adlandırma kuralını izleyin: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd
   * Veri diskleri genellikle bu adlandırma kuralını izleyin: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd

#### <a name="step-2-remove-the-lease-from-the-vhd"></a>2. adım: kira VHD'den kaldırın.

[Kira VHD'den kaldırmak](#remove-the-lease-from-the-vhd)ve ardından depolama hesabını silin.

## <a name="what-is-a-lease"></a>Bir kira nedir?
Bir kira blob'u (örneğin, bir VHD) erişimi denetlemek için kullanılan bir kilit ' dir. Bir blob kiralanmış yalnızca kira sahipleri blob erişebilirsiniz. Bir kira aşağıdaki nedenlerle önemlidir:

* Aynı anda blob aynı bölümüne yazmak birden çok sahipleri denerseniz, veri bozulmasını engeller.
* Blob bir şey etkin olarak da (örneğin, bir VM) kullanıyorsa, silinen engeller.
* Depolama hesabı bir şey etkin olarak da (örneğin, bir VM) kullanıyorsa, silinen engeller.

### <a name="remove-the-lease-from-the-vhd"></a>Kira VHD'den Kaldır
VHD bir işletim sistemi diski ise, kira kaldırmak için VM silmeniz gerekir:

1. [Azure Portal](https://portal.azure.com) oturum açın.
2. Üzerinde **Hub** menüsünde, select **sanal makineleri**.
3. VHD bir kirayı tutan VM'yi seçin.
4. Hiçbir şey etkin olarak sanal makinenin kullandığından emin olun ve sanal makine artık gerekir.
5. Üstündeki **VM ayrıntıları** dikey penceresinde, select **silmek**ve ardından **Evet** onaylamak için.
6. VM silinmesi gerekir, ancak VHD korunabilir. Ancak, VHD'yi artık kira üzerinde olmalıdır. Yayımlanacak kira için birkaç dakika sürebilir. Kira serbest olduğunu doğrulamak için Git **tüm kaynakları** > **depolama hesabı adı** > **BLOB'lar**  >   **VHD'ler**. İçinde **Blob özellikleri** bölmesinde **kiralama durum** değeri olmalıdır **kilitli değil**.

VHD bir veri diski varsa, kira kaldırmak için VM VHD'den bağlantısını kesin:

1. [Azure Portal](https://portal.azure.com) oturum açın.
2. Üzerinde **Hub** menüsünde, select **sanal makineleri**.
3. VHD bir kirayı tutan VM'yi seçin.
4. Seçin **diskleri** üzerinde **VM ayrıntıları** dikey.
5. VHD bir kirayı tutan veri diski seçin. VHD bağlı olduğu belirleyebilirsiniz VHD URL'sini denetleyerek disk.
6. Hiçbir şey veri diski etkin olarak kullandığını kesin olarak belirleyin.
7. Tıklatın **ayırma** üzerinde **Disk ayrıntıları** dikey.
8. Diski artık sanal makineden ayrılmış ve VHD artık kira üzerinde sahip olmalıdır. Yayımlanacak kira için birkaç dakika sürebilir. Kiralamasının serbest bırakıldığını doğrulamak için Git **tüm kaynakları** > **depolama hesabı adı** > **BLOB'lar**  >  **VHD'ler**. İçinde **Blob özellikleri** bölmesinde **kiralama durum** değeri olmalıdır **kilitli değil**.

## <a name="next-steps"></a>Sonraki adımlar
* [Bir depolama hesabını silme](storage-create-storage-account.md#delete-a-storage-account)
* [Microsoft Azure (PowerShell) kilitli kira blob storage'nın nasıl](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
