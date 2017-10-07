---
title: bir Windows VM hello Azure portal sorun giderme aaaUse | Microsoft Docs
description: "Azure portal kullanarak bağlanan hello işletim sistemi disk tooa kurtarma VM tootroubleshoot Windows sanal makine sorunlarını Azure nasıl hello öğrenin"
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 396f70338fa39f80bb9adcb9244d3c83f2a233eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a>Bir Windows VM hello işletim sistemi disk tooa kurtarma VM ekleyerek sorun giderme hello Azure portalını kullanma
Azure, Windows sanal makine (VM) önyükleme veya disk bir hatayla karşılaştığında, sorun giderme adımları hello sanal sabit diske kendisini tooperform gerekebilir. Yaygın bir örnek hello VM mümkün tooboot başarıyla engeller başarısız uygulama güncelleştirmesi olacaktır. Bu makale ayrıntıları toouse hello nasıl Azure portal tooconnect, sanal sabit hataları tooanother Windows VM toofix disk sonra özgün VM'yi yeniden oluşturun.

## <a name="recovery-process-overview"></a>Kurtarma işlemine genel bakış
sorun giderme işlemi hello aşağıdaki gibidir:

1. Merhaba sanal sabit diskleri tutmak hello VM karşılaşmadan sorunları, silin.
2. Ekleme ve sorun giderme amacıyla hello sanal sabit disk tooanother Windows VM bağlayın.
3. VM sorun giderme toohello bağlayın. Dosyaları düzenleyin veya herhangi bir aracı toofix sorunları hello özgün sanal sabit disk üzerinde çalıştırın.
4. Çıkarın ve VM sorun giderme hello hello sanal sabit diski kullanımdan çıkarın.
5. Merhaba özgün sanal sabit disk kullanan bir VM oluşturun.


## <a name="determine-boot-issues"></a>Önyükleme sorunlarını belirleme
neden VM'nizi mümkün tooboot doğru değil toodetermine hello önyükleme tanılaması VM ekran inceleyin. Başarısız uygulama güncelleştirme ya da bir temel sanal sabit silindiğinde veya taşındığında disk yaygın bir örnek olacaktır.

Merhaba Portalı'nda, VM seçin ve ardından toohello kaydırın **destek + sorun giderme** bölümü. Tıklatın **önyükleme tanılama** tooview hello ekran görüntüsü. Herhangi bir özel hata iletileri veya hata kodları Not toohelp belirlemek hello VM sorunu neden karşılaşıyor. Merhaba aşağıdaki örnek hizmetleri durdurma bekleniyor VM gösterir:

![Önyükleme tanılaması konsol günlükleri VM görüntüleme](./media/troubleshoot-recovery-disks-portal/screenshot-error.png)

Tıklatarak **ekran** toodownload hello VM ekran yakalama.


## <a name="view-existing-virtual-hard-disk-details"></a>Var olan sanal sabit disk ayrıntılarını görüntüleyin
Sanal sabit disk tooanother VM ekleyebilmek için tooidentify hello adı hello sanal sabit disk (VHD) gerekir. 

Merhaba portalından, bir kaynak grubunu seçin, sonra depolama hesabınızı seçin. Tıklatın **BLOB'lar**, aşağıdaki örneğine hello olarak:

![Depolama BLOB'ları seçin](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

Adlı bir kapsayıcıya sahip genellikle **VHD'ler** sanal sabit disklerinizi depolar. Merhaba kapsayıcı tooview sanal sabit disklerin listesini seçin. Not Merhaba, VHD adını (Merhaba önekidir genellikle VM hello adı):

![Depolama kapsayıcısı VHD tanımlayın](./media/troubleshoot-recovery-disks-portal/storage-container.png)

Merhaba listeden, varolan bir sanal sabit diski seçin ve hello URL'sini kullanmak için aşağıdaki adımları hello kopyalayın:

![Var olan sanal sabit disk URL'sini Kopyala](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a>Var olan VM silme
Sanal sabit diskler ve sanal makineler Azure'da iki ayrı kaynaktır. Bir sanal sabit disk hello işletim sisteminin kendisi, uygulamalar ve yapılandırmalar depolandığı ' dir. Merhaba VM kendisini hello boyutunu veya konumunu tanımlar ve bir sanal sabit disk veya sanal ağ arabirim kartı (NIC) gibi kaynakları başvuran meta verilerdir. Her sanal sabit diske bağlı olduğunda atanmış bir kira sahip tooa VM. Veri diskleri bağlı ve hatta hello VM çalışırken ayrılmış olsa da, hello VM kaynak silinmedikçe hello işletim sistemi diski ayrılamıyor. Bu VM durduruldu ve deallocated durumda olduğunda bile hello kira tooassociate hello işletim sistemi diski bir VM ile devam eder.

İlk adım toorecover hello VM toodelete hello VM kendisini kaynaktır. Silme hello VM hello sanal sabit diskleri depolama hesabınızdaki bırakır. Merhaba, VM silinmiş sonra hello sanal sabit disk tooanother VM tootroubleshoot ekleme ve hello hataları çözümleyin.

Hello Portalı'nda, VM seçin ve ardından **silmek**:

![VM önyükleme tanılama önyükleme hatası gösteren ekran görüntüsü](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

Merhaba VM hello sanal sabit disk tooanother VM eklemeden önce silme tamamlanana kadar bekleyin. Merhaba kira hello sanal sabit diskte hello VM ile ilişkilendiren hello sanal sabit disk tooanother VM iliştirebilirsiniz önce yayınlanan toobe gerekir.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Var olan sanal sabit disk tooanother VM ekleme
Sonraki birkaç adımda için Merhaba, sorun giderme amacıyla başka bir VM kullanın. VM toobe mümkün toobrowse sorun giderme hello varolan sanal sabit disk toothis ekleme ve hello diskin içeriği düzenleyin. Bu işlem toocorrect sağlar herhangi bir yapılandırma hataları veya gözden geçirme ek uygulama veya sistem günlük dosyaları, örneğin. Seçin veya sorun giderme amacıyla başka bir VM toouse oluşturun.

1. Merhaba portalından, bir kaynak grubunu seçin, sonra sorun giderme VM'yi seçin. Seçin **diskleri** ve ardından **Attach varolan**:

    ![Merhaba Portalı'nda mevcut diski kullanıma açın](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. tooselect, mevcut sanal sabit diski tıklatın **VHD dosyasını**:

    ![Mevcut bir VHD'ye göz atma](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. Depolama hesabı ve kapsayıcı seçip, varolan bir VHD'Yİ'ı tıklatın. Merhaba tıklatın **seçin** tooconfirm tercih ettiğiniz düğmesi:

    ![Mevcut VHD’nizi seçme](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. Artık seçili, VHD ile tıklatın **Tamam** tooattach hello varolan bir sanal sabit disk:

    ![Varolan bir sanal sabit diski ekleme onaylayın](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. Birkaç saniye sonra hello **diskleri** bölmesi, VM için varolan bir sanal sabit bir veri diski bağlı disk listeler:

    ![Veri diski olarak bağlı olan sanal sabit disk](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a>Merhaba bağlı veri diski bağlama

1. Uzak Masaüstü Bağlantısı tooyour VM açın. Hello Portalı'nda VM seçin ve tıklatın **Bağlan**. Merhaba RDP bağlantı dosyasını indirip açın. Kimlik bilgileri toolog tooyour VM aşağıdaki gibi girin:

    ![Tooyour Uzak Masaüstü kullanarak VM oturum](./media/troubleshoot-recovery-disks-portal/open-remote-desktop.png)

2. Açık **Sunucu Yöneticisi'ni**seçeneğini belirleyip **dosya ve depolama hizmetleri**. 

    ![Dosya ve depolama hizmetleri Sunucu Yöneticisi içinde seçin](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

3. Merhaba veri diski otomatik olarak algılandı ve bağlı. toosee hello listesini bağlı diskler, select **diskleri**. Merhaba sürücü harfi dahil olmak üzere, veri diski tooview birim bilgilerinizi seçebilirsiniz. Merhaba gösterir hello bağlı veri diski örnek ve kullanarak **F:**:

    ![Bağlı disk ve birim bilgileri Sunucu Yöneticisi'nde](./media/troubleshoot-recovery-disks-portal/server-manager-disk-attached.png)


## <a name="fix-issues-on-original-virtual-hard-disk"></a>Özgün sanal sabit diskinde ilgili sorunları giderme
Merhaba varolan bir sanal sabit takılı diski ile tüm bakım ve sorun giderme adımları gereken şekilde artık gerçekleştirebilirsiniz. Merhaba sorunlar ele sonra aşağıdaki adımları hello ile devam edin.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Çıkarın ve özgün sanal sabit disk ayırma
Hatalarınızı çözüldükten sonra hello varolan sanal sabit diskten, sorun giderme VM ayırma. VM sorun giderme hello sanal sabit disk toohello ekleme hello kira serbest kadar herhangi bir VM ile sanal sabit disk kullanamazsınız.

1. Merhaba RDP oturumu tooyour VM, açık **Sunucu Yöneticisi'ni**seçeneğini belirleyip **dosya ve depolama hizmetleri**:

    ![Sunucu Yöneticisi'nde dosya ve depolama hizmetleri seçin](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

2. Seçin **diskleri** ve veri diskinizi seçin. Veri diskinizi sağ tıklatın ve seçin **Çevrimdışına Al**:

    ![Sunucu Yöneticisi'nde çevrimdışı olarak Hello veri diski ayarlayın](./media/troubleshoot-recovery-disks-portal/server-manager-set-disk-offline.png)

3. Şimdi hello VM hello sanal sabit diski kullanımdan çıkarın. Hello Azure portal, VM seçin ve tıklatın **diskleri**. Varolan bir sanal sabit diski seçin ve ardından **ayırma**:

    ![Varolan bir sanal sabit disk ayırma](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    Merhaba VM başarıyla hello veri diski devam etmeden önce ayrılmış kadar bekleyin.

## <a name="create-vm-from-original-hard-disk"></a>Özgün sabit diskten VM oluşturma
bir VM, özgün sanal sabit diskten toocreate kullanmak [bu Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet). Merhaba şablon hello VHD URL'si hello gelen kullanarak mevcut sanal ağda, bir VM dağıtır önceki komutu. Merhaba tıklatın **tooAzure dağıtmak** gibi düğmesi:

![Github'dan şablondan VM dağıtma](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

Merhaba şablon dağıtımı için Azure portal hello yüklenir. Yeni VM ve mevcut Azure kaynaklarını Hello adlarını girin ve hello URL tooyour varolan bir sanal sabit diski yapıştırın. toobegin hello dağıtım tıklatın **satın alma**:

![VM şablonu dağıtma](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a>Önyükleme tanılaması yeniden etkinleştirin
Merhaba varolan sanal sabit diskten VM'nizi oluşturduğunuzda, önyükleme tanılaması otomatik olarak etkinleştirilmemiş olabilir. toocheck önyükleme tanılaması durumunu hello ve hello Portalı'nda, VM seçin gerekirse açın. Altında **izleme**, tıklatın **tanılama ayarları**. Merhaba durum olduğundan emin olun **üzerinde**, ve onay işareti sonraki çok hello**önyükleme tanılama** seçilir. Herhangi bir değişiklik yaparsanız, tıklatın **kaydetmek**:

![Önyükleme tanılaması ayarları güncelleştirme](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a>Sonraki adımlar
Tooyour VM bağlantı sorunları yaşıyorsanız, bkz: [sorun giderme RDP bağlantıları tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). VM üzerinde çalışan uygulamalara erişim sorunları için bkz: [Windows VM üzerinde uygulama bağlantı sorunlarını giderme](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Kaynak Yöneticisi'ni kullanma hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).