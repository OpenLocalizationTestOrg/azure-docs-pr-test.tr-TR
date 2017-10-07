---
title: "Azure depolama hesapları, kapsayıcıları veya VHD'leri sildiğinizde aaaTroubleshoot hataları | Microsoft Docs"
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
ms.openlocfilehash: 77361593e2c924d39aba853e0807dc3188f50e60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a>Azure depolama hesapları, kapsayıcıları veya VHD'leri sildiğinizde hatalarında sorun giderme

Bir Azure depolama hesabı, kapsayıcı ya da sanal sabit disk (VHD) toodelete çalıştığınızda hello hataları alabilirsiniz [Azure portal](https://portal.azure.com). Bu makale bir Azure Resource Manager dağıtım kılavuzu toohelp Çöz hello sorun giderme sağlar.

Bu makalede Azure sorununuzu adresi değil, ziyaret üzerinde Azure forumları hello [MSDN ve yığın taşması](https://azure.microsoft.com/support/forums/). Bu forumlar sorununuzu nakledebilirsiniz veya too@AzureSupport Twitter'da. Ayrıca, size bir Azure destek isteği seçerek dosya **alma desteği** hello üzerinde [Azure Destek](https://azure.microsoft.com/support/options/) site.

## <a name="symptoms"></a>Belirtiler
### <a name="scenario-1"></a>Senaryo 1
Toodelete bir Resource Manager dağıtım depolama hesabında bir VHD çalıştığınızda hello aşağıdaki hata iletisini alıyorsunuz:

**Toodelete blob 'vhds/BlobName.vhd' başarısız oldu. Hata: Yoktur şu anda bir kira hello blob üzerindeki ve hiçbir kiralama kimliği hello istekte belirtildi.**

Bir sanal makine (VM) toodelete çalıştığınız VHD hello üzerinde bir kira olduğundan bu sorun oluşabilir.

### <a name="scenario-2"></a>Senaryo 2
Toodelete bir Resource Manager dağıtım depolama hesabında bir kapsayıcı çalıştığınızda hello aşağıdaki hata iletisini alıyorsunuz:

**Toodelete depolama kapsayıcısı 'VHD'ler' başarısız oldu. Hata: Yoktur şu anda bir kira hello kapsayıcısını ve hiçbir kiralama kimliği hello istekte belirtildi.**

Merhaba kapsayıcı hello kira durumda kilitli bir VHD olduğundan bu sorun oluşabilir.

### <a name="scenario-3"></a>Senaryo 3
Toodelete bir Resource Manager dağıtım depolama hesabında çalıştığınızda hello aşağıdaki hata iletisini alıyorsunuz:

**Toodelete depolama hesabı 'StorageAccountName' başarısız oldu. Hata: hello depolama hesabı kullanımda tooits yapıları nedeniyle silinemiyor.**

Merhaba depolama hesabı hello kira durumda bir VHD içerdiğinden bu sorun oluşabilir.

## <a name="solution"></a>Çözüm 
tooresolve hello ilişkili VM ve bu sorunları hello hello hataya neden olan VHD tanımlamanız gerekir. Ardından, hello VHD Merhaba VM (veri diskleri) gelen detach veya hello hello VHD (işletim sistemi diskler için) kullanarak VM silin. Bu VHD hello hello kira kaldırır ve Silinen toobe sağlar. 

toodo Bu, kullanımı bir yöntem aşağıdaki hello:

### <a name="method-1---use-azure-storage-explorer"></a>Yöntem 1 - kullanım Azure storage Gezgini

### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a>1. adım tanımla hello hello depolama hesabı silinmesini engellemek VHD

1. Merhaba depolama hesabını sildiğinizde, ileti iletişim kutusu hello aşağıdaki gibi alır: 

    ![Merhaba depolama hesabını silme iletisi](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Merhaba denetleyin **Disk URL** tooidentify hello depolama hesabı ve hello engelleyen VHD hello depolama hesabı silin. Dize önce aşağıdaki örneğine hello hello ". blob.core.windows.net" Merhaba depolama hesabı adı ve "SCCM2012-2015-08-28.vhd" Merhaba VHD adı.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-hello-vhd-by-using-azure-storage-explorer"></a>2. adım Delete hello VHD Azure Storage Gezgini kullanarak

1. İndirme ve yükleme hello en son sürümünü [Azure Storage Gezgini](http://storageexplorer.com/). Bu araç, Windows, macOS ve Linux Azure Storage verilerle tooeasily çalışma sağlayan Microsoft bir tek başına uygulamadır.
2. Azure Depolama Gezgini'ni açın ve seçin ![hesabı simgesi](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) Merhaba sol çubuğunda Azure ortamınızı seçin ve ardından oturum açın.

3. Tüm abonelikleri veya toodelete istediğiniz hello depolama hesabını içeren hello abonelik seçin.

    ![Abonelik Ekle](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. Biz hello disk URL daha önce hello alınan toohello depolama hesabı Git **Blob kapsayıcıları** > **VHD'ler** ve delete hello depolama hesabı Merhaba engelleyen VHD arayın.
5. Merhaba VHD bulunursa, hello denetleyin **VM adı** sütun toofind hello bu VHD kullanarak VM.

    ![VM denetleyin](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. Merhaba kira Azure portalını kullanarak VHD hello kaldırın. Daha fazla bilgi için bkz: [hello VHD öğesinden Kaldır hello kira](#remove-the-lease-from-the-vhd). 

7. Toohello Azure Storage Gezgini gidin, hello VHD sağ tıklayın ve ardından Sil'i seçin.

8. Merhaba depolama hesabı silin.

### <a name="method-2---use-azure-portal"></a>Yöntem 2 - Azure portalı 

#### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a>1. adım: hello hello depolama hesabı silinmesini engellemek VHD tanımlayın

1. Merhaba depolama hesabını sildiğinizde, ileti iletişim kutusu hello aşağıdaki gibi alır: 

    ![Merhaba depolama hesabını silme iletisi](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Merhaba denetleyin **Disk URL** tooidentify hello depolama hesabı ve hello engelleyen VHD hello depolama hesabı silin. Dize önce aşağıdaki örneğine hello hello ". blob.core.windows.net" Merhaba depolama hesabı adı ve "SCCM2012-2015-08-28.vhd" Merhaba VHD adı.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. İçinde toohello oturum [Azure portal](https://portal.azure.com).
3. Merhaba Hub menüsünde seçin **tüm kaynakları**. Toohello depolama hesabına gidin ve ardından **BLOB'lar** > **VHD'ler**.

    ![Merhaba depolama hesabı ve vurgulanmış hello "VHD" kapsayıcı hello portalı ekran görüntüsü](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. Merhaba, biz hello disk URL'den daha önce elde edilen VHD bulun. Ardından, VM kullanan belirlemek VHD hello. Genellikle, olan VM hello VHD hello VHD adını kontrol ederek belirleyebilirsiniz:

Resource Manager geliştirme modelini VM

   * İşletim sistemi disk genellikle bu adlandırma kuralını izleyin: VMName-YYYY-AA-GG-HHMMSS.vhd
   * Veri diskleri genellikle bu adlandırma kuralını izleyin: VMName-YYYY-AA-GG-HHMMSS.vhd

VM Klasik geliştirme modeli

   * İşletim sistemi disk genellikle bu adlandırma kuralını izleyin: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd
   * Veri diskleri genellikle bu adlandırma kuralını izleyin: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd

#### <a name="step-2-remove-hello-lease-from-hello-vhd"></a>2. adım: hello kira hello VHD ' kaldırın.

[Merhaba kira VHD hello Kaldır](#remove-the-lease-from-the-vhd)ve hello depolama hesabı silin.

## <a name="what-is-a-lease"></a>Bir kira nedir?
Bir kira kullanılan toocontrol erişim tooa blob (örneğin, bir VHD) olabilecek kilit ' dir. Bir blob kiralanmış olduğunda yalnızca hello kira hello sahipleri hello blob erişebilirsiniz. Bir kira nedenleri aşağıdaki hello için önemlidir:

* Birden çok sahipleri toowrite toohello çalışırsanız veri bozulmasını engeller hello blob hello adresindeki aynı bölümünü aynı anda.
* Merhaba blob bir şey etkin olarak da (örneğin, bir VM) kullanıyorsa, silinen engeller.
* Merhaba depolama hesabı bir şey etkin olarak da (örneğin, bir VM) kullanıyorsa, silinen engeller.

### <a name="remove-hello-lease-from-hello-vhd"></a>Merhaba kira VHD hello Kaldır
Merhaba VHD bir işletim sistemi diski ise, hello VM tooremove hello kira silmeniz gerekir:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba üzerinde **Hub** menüsünde, select **sanal makineleri**.
3. Merhaba VHD hello üzerinde bir kirayı tutan VM seçin.
4. Hiçbir şey etkin şekilde hello sanal makine ve sanal makine artık hello kullandığından emin olun.
5. Merhaba hello üstündeki **VM ayrıntıları** dikey penceresinde, select **silmek**ve ardından **Evet** tooconfirm.
6. Merhaba VM silinmesi gerekir, ancak hello VHD korunabilir. Ancak, hello VHD artık kira üzerinde olmalıdır. Yayımlanan hello kira toobe birkaç dakika sürebilir. kira hello tooverify yayımlanır, çok Git**tüm kaynakları** > **depolama hesabı adı** > **BLOB'lar**  >  **VHD'ler**. Merhaba, **Blob özellikleri** bölmesi, hello **kiralama durum** değeri olmalıdır **kilitli değil**.

Merhaba VHD bir veri diski varsa, hello VHD hello VM tooremove hello kira gelen bağlantısını kesin:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba üzerinde **Hub** menüsünde, select **sanal makineleri**.
3. Merhaba VHD hello üzerinde bir kirayı tutan VM seçin.
4. Seçin **diskleri** hello üzerinde **VM ayrıntıları** dikey.
5. VHD hello üzerinde bir kirayı tutan hello veri diski seçin. VHD bağlı olduğu belirleyebilirsiniz hello VHD hello URL'sini denetleyerek hello disk.
6. Hiçbir şey hello veri diski etkin olarak kullandığını kesin olarak belirleyin.
7. Tıklatın **ayırma** hello üzerinde **Disk ayrıntıları** dikey.
8. Hello disk şimdi VM hello ayrılmış ve hello VHD artık kira üzerinde olmalıdır. Yayımlanan hello kira toobe birkaç dakika sürebilir. kira hello tooverify yayımlanan, çok Git**tüm kaynakları** > **depolama hesabı adı** > **BLOB'lar**  >  **VHD'ler**. Merhaba, **Blob özellikleri** bölmesi, hello **kiralama durum** değeri olmalıdır **kilitli değil**.

## <a name="next-steps"></a>Sonraki adımlar
* [Bir depolama hesabını silme](storage-create-storage-account.md#delete-a-storage-account)
* [Toobreak hello kira blob storage'nın Microsoft Azure (PowerShell) nasıl kilitli](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
