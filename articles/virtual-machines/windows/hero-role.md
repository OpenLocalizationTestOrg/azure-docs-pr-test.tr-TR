---
title: ilk Windows VM'nizi IIS'de aaaInstall | Microsoft Docs
description: "Denemeler ile ilk Windows sanal makine IIS yükleyerek ve 80 numaralı bağlantı noktasını kullanarak açma hello Azure portalı."
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6334ea45-db6b-4e08-abb5-1f98927ebc34
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cynthn
ms.openlocfilehash: 7cfed6197df058c4569d111ee88961da7c6fe0b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a>Windows VM üzerinde bir rolü yüklemeye denemeler
İlk sanal makine (VM) ve çalışan olduktan sonra tooinstalling yazılım ve hizmetlerinin taşıyabilirsiniz. Bu öğreticide, biz toouse Sunucu Yöneticisi'ni hello Windows Server VM tooinstall IIS üzerinde adımıdır. Ardından, hello Azure portal tooopen bağlantı noktası 80 tooIIS trafiği kullanarak ağ güvenlik grubu (NSG) oluşturacağız. 

İlk VM oluşturmadıysanız, size geri çok tamamlamalıdır[hello Azure portalında, ilk Windows sanal makine oluşturma](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Bu öğretici ile devam etmeden önce.

## <a name="make-sure-hello-vm-is-running"></a>VM'nin çalıştığından emin hello olun
1. Açık hello [Azure portal](https://portal.azure.com).
2. Merhaba hub menüsünde **sanal makineleri**. Merhaba sanal makine hello listeden seçin.
3. Merhaba durumundaysa **durduruldu (Deallocated)**, hello tıklatın **Başlat** hello düğmesinde **Essentials** hello VM dikey. Merhaba durumundaysa **çalıştıran**, üzerinde toohello sonraki adıma geçebilirsiniz.

## <a name="connect-toohello-virtual-machine-and-sign-in"></a>Toohello sanal makineye bağlanın ve oturum açın
1. Merhaba hub menüsünde **sanal makineleri**. Merhaba sanal makine hello listeden seçin.
2. Merhaba sanal makine için Hello dikey penceresinde **Bağlan**. Bu oluşturur ve bir kısayol tooconnect tooyour makine gibi bir Uzak Masaüstü Protokolü dosyasını (.rdp dosyası) indirir. Kolay erişim için toosave hello dosya tooyour Masaüstü isteyebilirsiniz. **Açık** bu dosya tooconnect tooyour VM.
   
    ![Hello Azure portal gösteren ekran görüntüsü nasıl tooconnect tooyour VM](./media/hero-role/connect.png)
3. Bir uyarı almak bu hello .rdp bilinmeyen bir yayımcıdan değil. Bu normaldir. Merhaba Uzak Masaüstü penceresinde **Bağlan** toocontinue.
   
    ![Bilinmeyen yayımcıya ilişkin uyarı ekran görüntüsü](./media/hero-role/rdp-warn.png)
4. Merhaba Windows Güvenlik penceresinde türü hello kullanıcı adı ve parola oluşturduğunuz sırada oluşturduğunuz hello yerel hesap için VM hello. Merhaba kullanıcı adı olarak girilir *vmname*&#92; *Kullanıcı adı*, ardından **Tamam**.
   
    ![Merhaba VM adı, kullanıcı adı ve parola girme ekran görüntüsü](./media/hero-role/credentials.png)
5. Bir uyarı almak bu hello sertifika doğrulanamıyor. Bu normaldir. Tıklatın **Evet** tooverify hello hello sanal makine kimliğini ve oturum açmayı tamamlayın.
   
   ![Bir ileti gösteren ekran görüntüsü hello hello VM kimliğini doğrulamaya ilişkin](./media/hero-role/cert-warning.png)

Tooconnect çalıştığınızda tootrouble içinde çalıştırırsanız, bkz: [sorun giderme Uzak Masaüstü bağlantıları tooa Windows tabanlı Azure sanal makine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="install-iis-on-your-vm"></a>Sanal makinenize IIS yükleme
Toohello VM kaydedilir, böylece daha deneyebilirsiniz biz sunucu rolünü yükler.

1. Henüz açık değilse **Sunucu Yöneticisi**’ni açın. Merhaba tıklatın **Başlat** menüsüne ve ardından **Sunucu Yöneticisi'ni**.
2. İçinde **Sunucu Yöneticisi'ni**seçin **yerel sunucu** hello sol bölmesinden. 
3. Merhaba menüde seçin **Yönet** > **rol ve Özellik Ekle**.
4. Merhaba eklemek rol ve özellik Sihirbazı'nda hello **yükleme türü** sayfasında, **rol tabanlı veya özellik tabanlı yükleme**ve ardından **sonraki**.
   
    ![Ekran gösteren hello Ekle roller ve Özellikler Sihirbazı sekmesinde yükleme türü](./media/hero-role/role-wizard.png)
5. Merhaba sunucu havuzundan Hello VM seçin ve tıklatın **sonraki**.
6. Merhaba üzerinde **sunucu rolleri** sayfasında, **Web sunucusu (IIS)**.
   
    ![Ekran gösteren hello Ekle roller ve Özellikler Sihirbazı sekmesini sunucu rolleri için](./media/hero-role/add-iis.png)
7. ISS'nin ihtiyaç duyduğu özellikleri ekleme hakkında açılır Hello içinde olduğundan emin olun **yönetim araçlarını dahil** seçilir ve ardından **Özellik Ekle**. Merhaba açılır kapandığında tıklatın **sonraki** hello Sihirbazı'nda.
   
    ![Merhaba IIS rolü ekleme açılır tooconfirm gösteren ekran görüntüsü](./media/hero-role/confirm-add-feature.png)
8. Merhaba özellikleri sayfasında, tıklatın **sonraki**.
9. Merhaba üzerinde **Web sunucusu rolü (IIS)** sayfasında, **sonraki**. 
10. Merhaba üzerinde **rol hizmetlerini** sayfasında, **sonraki**. 
11. Merhaba üzerinde **onay** sayfasında, **yükleme**. 
12. Merhaba yüklemesi tamamlandıktan sonra tıklatın **Kapat** hello Sihirbazı.

## <a name="open-port-80"></a>Bağlantı noktası 80'i açın
Bağlantı noktası 80 üzerinden gelen trafik, VM tooaccept sırada, tooadd bir gelen kuralı toohello ağ güvenlik grubu gerekir. 

1. Açık hello [Azure portal](https://portal.azure.com).
2. İçinde **sanal makineleri** hello oluşturduğunuz VM seçin.
3. Merhaba sanal makine ayarlarında seçin **ağ arabirimleri** ve ardından var olan ağ arabirimi seçin hello.
   
    ![Ağ arabirimleri hello Hello sanal makine ayarı gösteren ekran görüntüsü](./media/hero-role/network-interface.png)
4. İçinde **Essentials** hello hello ağ arabirimi için tıklatın **ağ güvenlik grubu**.
   
    ![Merhaba temel parçalar bölümünde hello ağ arabirimi için gösteren ekran görüntüsü](./media/hero-role/select-nsg.png)
5. Merhaba, **Essentials** dikey penceresinde hello NSG için gelen kuralı için bir var olan varsayılan olmalıdır **varsayılan izin rdp** olanak sağlayan toolog toohello VM. Başka bir gelen kuralı tooallow IIS trafiği ekleyeceksiniz. **Gelen güvenlik kuralı**’na tıklayın.
   
    ![Merhaba temel parçalar bölümünde hello NSG için gösteren ekran görüntüsü](./media/hero-role/inbound.png)
6. **Gelen güvenlik kuralları** bölümünde **Ekle**’ye tıklayın.
   
    ![Güvenlik kuralı Hello düğmesi tooadd gösteren ekran görüntüsü](./media/hero-role/add-rule.png)
7. **Gelen güvenlik kuralları** bölümünde **Ekle**’ye tıklayın. Tür **80** hello bağlantı noktası aralığı ve emin olun **izin** seçilir. İşiniz bittiğinde **Tamam**’a tıklayın.
   
    ![Güvenlik kuralı Hello düğmesi tooadd gösteren ekran görüntüsü](./media/hero-role/port-80.png)

Nsg'ler, gelen ve giden kuralları hakkında daha fazla bilgi için bkz: [izin dış erişim tooyour VM kullanarak hello Azure portalı](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="connect-toohello-default-iis-website"></a>Toohello varsayılan IIS Web sitesini Bağlan
1. Hello Azure portal'ı tıklatın **sanal makineleri** ve VM'yi seçin.
2. Merhaba, **Essentials** dikey penceresinde, kopyalama, **genel IP adresi**.
   
    ![Burada toofind hello VM genel IP adresini gösteren ekran görüntüsü](./media/hero-role/ipaddress.png)
3. Bir tarayıcı açın ve bu gibi ortak IP adresi hello adres çubuğunda yazın: http://<publicIPaddress> tıklatıp **Enter** toogo toothat adresi.
4. Tarayıcınız hello varsayılan IIS web sayfası açmanız gerekir. Şuna benzer:
   
    ![Bir tarayıcıda hangi hello varsayılan IIS sayfasını gösteren ekran görüntüsü gibi görünüyor](./media/hero-role/iis-default.png)

## <a name="next-steps"></a>Sonraki adımlar
* De deneyimleyebilirsiniz [bir veri diski eklemeyi](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour sanal makine. Veri diskleri sanal makineniz için daha fazla depolama alanı sağlar.

