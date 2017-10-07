---
title: aaaCreate StorSimple destek paketi | Microsoft Docs
description: "Nasıl toocreate, şifresini ve StorSimple cihazınız için bir destek paketini Düzenle öğrenin."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: eac76f5f-5db1-4c92-af8c-54053b91e66c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 209aeee50e823fd2ca96ababd1d0cf3ea9cdad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a>Oluşturma ve StorSimple destek paketi yönetme
## <a name="overview"></a>Genel Bakış
Bir StorSimple destek paketi StorSimple cihaz sorunları gidermeye tüm ilgili günlükleri tooassist Microsoft Support toplayan bir kullanımı kolay mekanizmasıdır. Merhaba toplanan günlükleri şifrelenmiş sıkıştırılmış ve.

Bu öğretici, adım adım yönergeler toocreate içerir ve hello destek paketi yönetin.

## <a name="create-and-upload-a-support-package-in-hello-azure-classic-portal"></a>Oluşturma ve hello Klasik Azure portalında bir destek paketi yükleme
Oluşturma ve bir destek paketi toohello Microsoft Support sitesini hello aracılığıyla karşıya **Bakım** hello Klasik Azure portalı hello hizmetinde sayfası.

> [!NOTE]
> Merhaba karşıya yükleme desteği geçiş gerektirir. Destek mühendisinize e-posta iletisinde bu tooyou sağlamalıdır.
> 
> 

Şifrelenmiş ve sıkıştırılmış Destek Paketi (.cab dosyası) oluşturulur ve karşıya yüklenen toohello destek sitesidir. Merhaba destek mühendisine hello destek sitesinden hello sorunu gidermek için bu paketi sonra alabilir.

Merhaba Klasik portal toocreate destek paketi adımlarını izleyerek hello gerçekleştirin.

#### <a name="toocreate-a-support-package-in-hello-azure-classic-portal"></a>toocreate hello Klasik Azure portalında bir destek paketi
1. Seçin **aygıtları** > **Bakım**.
2. Merhaba, **destek paketi** bölümünde, select **oluşturma ve karşıya yükleme destek paketi**.
3. Merhaba, **oluşturma ve karşıya yükleme destek paketi** iletişim kutusunda, aşağıdaki hello:
   
    ![Destek Paketi Oluştur](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * Merhaba, **destek geçiş** metin kutusuna, hello geçiş anahtarı girin. Microsoft destek mühendisinize bu geçiş tooyou e-posta göndermesi gerekir.
   * Merhaba onay kutusunu tooprovide izin tooautomatically karşıya yükleme hello destek paketi toohello Microsoft Support sitesini seçin.
   * Merhaba onay simgesine tıklayın ![Onay simgesi](./media/storsimple-create-manage-support-package/IC740895.png).

## <a name="manually-create-a-support-package"></a>El ile bir destek paketi oluştur
Bazı durumlarda, gerekir toomanually StorSimple için Windows PowerShell üzerinden hello destek paketi oluşturun. Örneğin:

* Tooremove hassas bilgileri, günlüğünden gerekirse Microsoft Support önceki toosharing dosyaları.
* Merhaba paket tooconnectivity sorunları nedeniyle karşıya zorluk yaşıyorsanız.

E-posta Microsoft Support el ile oluşturulan destek paketinizi paylaşabilirsiniz. StorSimple için Windows PowerShell desteği paketinde adımları toocreate aşağıdaki hello gerçekleştirin.

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a>toocreate StorSimple için Windows PowerShell desteği paketinde
1. toostart tooconnect tooyour StorSimple cihazı kullandığı hello uzak bilgisayarda yönetici olarak Windows PowerShell oturumu bir hello aşağıdaki komutu girin:
   
    `Start PowerShell`
2. Merhaba Windows PowerShell oturumunda toohello Cihazınızı SSAdmin konsoluna Bağlan:
   
   * Merhaba komut isteminde girin:
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * Açılan hello iletişim kutusunda, cihaz Yönetici parolanızı girin. Merhaba varsayılan paroladır:
     
      `Password1`
     
      ![PowerShell kimlik bilgisi iletişim kutusu](./media/storsimple-create-manage-support-package/IC740962.png)
   * **Tamam**’ı seçin.
   * Merhaba komut isteminde girin:
     
      `Enter-PSSession $MS`
3. Açılır hello oturumunda hello uygun komutu girin.
   
   * Parola korumalı ağ paylaşımları için girin:
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       (Merhaba destek paketi şifrelendiğinden) bir parola, bir yol toohello ağ paylaşılan klasörüne ve bir şifreleme parolası istenir. Bir destek paketi sonra hello belirtilen klasörde oluşturulur.
   * Parola korumalı olmayan paylaşımlar için hello gerekmez `-Credential` parametresi. Merhaba aşağıdakileri girin:
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       Merhaba destek paketi hem denetleyicileri hello belirtilen ağ paylaşılan klasöründe oluşturulur. Bu sorun giderme için tooMicrosoft destek gönderilebilecek bir şifrelenmiş ve sıkıştırılmış dosyasıdır. Daha fazla bilgi için bkz: [Microsoft Destek birimine başvurun](storsimple-contact-microsoft-support.md).

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a>Merhaba verme HcsSupportPackage cmdlet parametreleri
Şu parametreler hello verme HcsSupportPackage cmdlet ile Merhaba kullanabilirsiniz.

| Parametre | Gerekli/isteğe bağlı | Açıklama |
| --- | --- | --- |
| `-Path` |Gerekli |Merhaba ağ paylaşılan klasörüne hangi hello destek paketi yerleştirilir tooprovide hello konumu kullanın. |
| `-EncryptionPassphrase` |Gerekli |Kullanım tooprovide parola toohelp hello destek paketi şifreleyin. |
| `-Credential` |İsteğe bağlı |Toosupply erişim kimlik bilgileri hello ağ paylaşılan klasör için kullanın. |
| `-Force` |İsteğe bağlı |Tooskip hello şifreleme parolası onayı adımını kullanın. |
| `-PackageTag` |İsteğe bağlı |Bir dizini altında toospecify kullanmak *yol* hangi hello destek paketi yerleştirilir. Merhaba varsayılandır [aygıt adı]-[geçerli tarih ve time:yyyy-MM-dd-HH-mm-ss]. |
| `-Scope` |İsteğe bağlı |Olarak belirttiğiniz **küme** (varsayılan) toocreate hem denetleyicileri için bir destek paketi. Yalnızca hello geçerli denetleyici için bir paket toocreate istiyorsanız belirtin **denetleyicisi**. |

## <a name="edit-a-support-package"></a>Destek paketini Düzenle
Bir destek paketi oluşturduktan sonra tooedit hello paket tooremove hassas bilgileri gerekebilir. Bu, birim adları, cihaz IP adresleri ve hello günlük dosyalarındaki yedek adları içerebilir.

> [!IMPORTANT]
> Yalnızca StorSimple için Windows PowerShell aracılığıyla oluşturulan bir destek paketi düzenleyebilirsiniz. Merhaba StorSimple Yöneticisi hizmetiyle Klasik Azure portalında oluşturulan bir paket düzenleyemezsiniz.
> 
> 

tooedit hello Microsoft Support sitesini üzerinde karşıya yüklemeden önce bir destek paketi ilk hello destek paketi şifresini, hello dosyaları düzenleyin ve yeniden şifrelemek. Merhaba aşağıdaki adımları gerçekleştirin.

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a>tooedit StorSimple için Windows PowerShell desteği paketinde
1. Açıklandığı gibi daha önce bir destek paketi oluştur [toocreate StorSimple için Windows PowerShell desteği paketinde](#to-create-a-support-package-in-windows-powershell-for-storsimple).
2. [Karşıdan yükleme Hello komut](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) istemciniz yerel olarak.
3. Merhaba Windows PowerShell modülünü içeri aktarın. Merhaba yolu toohello yerel klasör hello betiği indirildi belirtin. tooimport hello modülü girin:
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. Tüm hello dosyalar *.aes* sıkıştırılmış ve şifrelenmiş dosyalar. toodecompress ve şifre çözme dosyaları girin:
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    Hello gerçek dosya uzantıları için tüm hello dosyaları şimdi görüntülenen unutmayın.
   
    ![Destek paketini Düzenle](./media/storsimple-create-manage-support-package/IC750706.png)
5. Merhaba şifreleme parolası istendiğinde hello destek paketi oluştururken kullandığınız hello parola girin.
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. Merhaba günlük dosyalarını içeren toohello klasörüne göz atın. Merhaba günlük dosyalarının şimdi sıkıştırması açılmış ve şifresi çünkü bunlar özgün dosya uzantılarını sahip olur. Bu dosyaları tooremove birim adları ve cihaz IP adresleri gibi herhangi bir müşteriye özgü bilgisi değiştirin ve hello dosyalarını kaydedin.
7. Kapat hello dosyaları toocompress gzip ile bunları ve AES 256 ile şifreleyebilirsiniz. Bu hız ve hello destek paketi bir ağ üzerinden aktarılması güvenliği içindir. toocompress ve dosyaları şifrelemek, hello aşağıdakileri girin:
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Destek paketini Düzenle](./media/storsimple-create-manage-support-package/IC750707.png)
8. İstendiğinde, bir şifreleme parolası hello değiştirilmiş destek paketi için belirtin.
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. Microsoft istendiğinde Support paylaşmanızı sağlayan hello yeni parolayı not ettiğinizden.

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a>Örnek: parola korumalı bir paylaşılan bir destek paketi dosyalarını düzenleme
Aşağıdaki örneğine hello nasıl toodecrypt, düzenlemek ve bir destek paketi yeniden şifrele gösterir.

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[kullanma desteği paketler ve cihaz oturum tootroubleshoot aygıt dağıtımınızı](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).
* Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

