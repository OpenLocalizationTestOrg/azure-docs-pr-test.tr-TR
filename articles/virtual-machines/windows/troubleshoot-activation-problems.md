---
title: "aaaTroubleshoot Windows sanal makine etkinleştirme sorunlarını azure'da | Microsoft Docs"
description: "Merhaba sağlar sorun giderme için Azure'da Windows sanal makine etkinleştirme sorunlarını giderme adımları"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 4ebdac66166e80dcd68cd9e2931b30a29ac01eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a>Azure Windows sanal makine etkinleştirme sorunlarını giderme

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Özel bir görüntüden oluşturulan Azure Windows sanal makine (VM) etkinleştirirken sorun varsa, bu belge tootroubleshoot hello sayısındaki sağlanan hello bilgileri kullanabilirsiniz. 

## <a name="symptom"></a>Belirti

Bir Azure Windows VM tooactivate çalıştığınızda bir hata alıyorsunuz ileti örnek aşağıdaki hello benzer:

**Hata: 0xC004F074 hello yazılım LicensingService o hello bilgisayarın etkinleştirilemediğini bildirdi. Hiçbir anahtar ManagementService (KMS) bağlantı kurulamadı. Lütfen ek bilgi için hello uygulama olay günlüğüne bakın.**

## <a name="cause"></a>Nedeni
Genellikle, Azure VM etkinleştirme sorunlar hello Windows VM tarafından yapılandırılmamışsa hello uygun KMS istemci kurulum anahtarı kullanarak veya bir bağlantı sorunu toohello Azure KMS hizmeti (kms.core.windows.net, bağlantı noktası 1668) hello Windows VM sahip oluşur. 

## <a name="solution"></a>Çözüm

>[!NOTE]
>Siteden siteye VPN kullanıyorsanız ve zorlanan tünel, bkz: [kullanım Azure özel yönlendirir zorlamalı tünel ile tooenable KMS etkinleştirmesi](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx). 
>
>ExpressRoute kullanarak ve varsa varsayılan rota yayımlanan bkz [Azure VM ExpressRoute tooactivate başarısız olabilir](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).

### <a name="step-1-configure-hello-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a>1. adım yapılandırma hello uygun KMS istemci kurulum anahtarı (Windows Server 2016 ve Windows Server 2012 R2)

Windows Server 2016 veya Windows Server 2012 R2 özel bir görüntüden oluşturulan VM Hello için hello uygun KMS istemci kurulum anahtarı hello VM için yapılandırmanız gerekir.

Bu adım tooWindows 2012 veya Windows 2008 R2'in geçerli değildir. Yalnızca Windows Server 2016 ve Windows Server 2012 R2 tarafından desteklenen hello Otomasyon sanal makine etkinleştirme (AVMA) özelliği kullanır.

1. Çalıştırma **slmgr.vbs/dlv** yükseltilmiş bir komut isteminde. Merhaba hello çıktısında açıklama değeri denetleyin ve perakende (Perakende kanal) veya toplu (VOLUME_KMSCLIENT) lisans ortamdan oluşturulduğu olup olmadığını belirleyin:
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. Varsa **slmgr.vbs/dlv** komutları tooset hello aşağıdaki hello çalıştırmak, perakende kanal gösterir [KMS istemci kurulum anahtarı](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) hello Windows Server sürümü için kullanılıyorsa ve tooretry etkinleştirme zorla: 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    Örneğin, Windows Server 2016 Datacenter için hello aşağıdaki komutu çalıştırın:

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-hello-connectivity-between-hello-vm-and-azure-kms-service"></a>2. adım hello VM Azure KMS hizmeti arasındaki hello bağlantıyı doğrulayın

1. İndirmeyi ve ayıklamayı hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) aracı tooa yerel klasörde hello değil etkinleştirme VM. 

2. TooStart gidin, Windows PowerShell üzerinde arama, Windows PowerShell sağ tıklayın ve ardından yönetici olarak çalıştır'ı seçin.

3. Sanal makine bu hello toouse hello doğru Azure KMS sunucusunda yapılandırdığınızdan emin olun. toodo Bu, aşağıdaki komutu çalıştırın:
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    Merhaba komutu döndürmelidir: anahtar yönetimi hizmeti makine adı tookms.core.windows.net:1688 başarılı bir şekilde ayarlayın.

4. Bağlantı toohello KMS sunucusuna sahip olmanızı Psping kullanarak doğrulayın. Merhaba Pstools.zip indirme ayıkladığınız toohello klasöre geçin ve hello aşağıdakini çalıştırın:
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  Merhaba ikinci son satırında hello çıktı, gördüğünüz emin olun: gönderilen = 4, alınan = 4, kaybolan = 0 (%0 kayıp).

  Kayıp 0'dan (sıfır) büyük olursa hello VM bağlantı toohello KMS sunucusunda yok. Bu durumda, hello VM olan bir sanal ağ ve özel bir DNS sunucusu belirttiği, bu DNS sunucusuna emin olun mümkün tooresolve kms.core.windows.net olur. Veya kms.core.windows.net gidermek hello DNS sunucusu tooone değiştirin.

  Sanal ağdan tüm DNS sunucularına kaldırırsanız, sanal makineleri Azure'nın iç DNS hizmeti kullandığına dikkat edin. Bu hizmet kms.core.windows.net çözümleyebilir.
  
Ayrıca bu hello Konuk Güvenlik Duvarı'nı etkinleştirme girişimlerini engelleyebilecek bir biçimde yapılandırılmamış doğrulayın.

5. Başarılı bağlantı tookms.core.windows.net doğruladıktan sonra o yükseltilmiş Windows PowerShell isteminde komutu aşağıdaki hello çalıştırın. Bu komut etkinleştirme birden çok kez çalışır.

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

Başarılı bir etkinleştirme hello aşağıdakine benzer bilgiler verir:

**Windows(R), Serverdatacentercore edition (12345678-1234-1234-1234-12345678) etkinleştiriliyor... Ürün başarıyla etkinleştirildi.**

## <a name="faq"></a>SSS 

### <a name="i-created-hello-windows-server-2016-from-azure-marketplace-do-i-need-tooconfigure-kms-key-for-activating-hello-windows-server-2016"></a>Azure Marketi'nden hello Windows Server 2016 oluşturdum. Tooconfigure KMS anahtarı hello Windows Server 2016 etkinleştirmek için gerekiyor mu? 
 
Hayır. Azure Market Hello görüntüde hello uygun KMS istemci kurulum anahtarı zaten yapılandırılmış sahiptir. 

### <a name="does-windows-activation-work-hello-same-way-regardless-if-hello-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a>Merhaba VM veya Azure karma kullanımı Avantajı (HUB) kullanıyorsa, Windows etkinleştirme iş aynı şekilde bakılmaksızın hello mu? 
 
Evet. 
 
### <a name="what-happens-if-windows-activation-period-expires"></a>Windows etkinleştirme süresi dolarsa ne olur? 
 
Hello yetkisiz kullanım süresi dolmuştur ve Windows hala etkin olduğunda, Windows Server 2008 R2 ve sonraki Windows sürümlerini etkinleştirme hakkında ek bildirimleri gösterir. Merhaba masaüstü duvar kağıdı siyah kalır ve Windows Update, güvenlik ve yalnızca kritik güncelleştirmeler, ancak isteğe bağlı değil güncelleştirmeleri yükler. Merhaba bildirimleri bkz hello hello alt kısmına [lisans koşulları](http://technet.microsoft.com/en-us/library/ff793403.aspx) sayfası.   

## <a name="need-help-contact-support"></a>Yardım mı gerekiyor? Desteğe başvurun.
Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) sorunu Çözümlendi hızla tooget.
