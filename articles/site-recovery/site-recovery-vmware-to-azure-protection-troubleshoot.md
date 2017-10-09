---
title: "aaaTroubleshoot koruma hataları VMware/fiziksel tooAzure | Microsoft Docs"
description: "Bu makalede hello ortak VMware makine çoğaltma hataları ve nasıl tootroubleshoot bunları"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/26/2017
ms.author: asgang
ms.openlocfilehash: b821e9aa2610482ba1900645fb75e75744dc442f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a>Şirket içi VMware/fiziksel sunucu çoğaltma sorunlarını giderme
VMware sanal makineleri veya fiziksel sunucuları Azure Site RECOVERY'yi kullanarak korurken, belirli bir hata iletisi alabilirsiniz. Bazı hello karşılaşılan, sorun giderme adımları tooresolve yanı sıra daha sık karşılaşılan hata iletileri bu makale ayrıntıları bunları.


## <a name="initial-replication-is-stuck-at-0"></a>İlk çoğaltma %0 takıldı
Biz destek karşılaştığınız hello ilk çoğaltma hatalarını kaynak sunucu işlemi sunucu veya işlem sunucusu Azure arasında tooconnectivity sorunları nedeniyle çoğu.
Çoğu durumda, kendi kendini yapabilecekleriniz aşağıda listelenen hello adımları izleyerek bu sorunları giderme.

###<a name="check-hello-following-on-source-machine"></a>Kaynak makinede Hello aşağıdakileri denetleyin
* Kaynak sunucu makine komut satırından Telnet tooping hello işlem sunucusu https bağlantı noktası (varsayılan 9443) ile ağ bağlantısı sorunları veya güvenlik duvarı bağlantı noktası engelleme sorunları varsa toosee gösterildiği gibi kullanın.
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > PING tootest bağlantı kullanmayın, Telnet kullanın.  Telnet yüklü değilse hello adımları listesini izleyen [burada](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)

Sorun hala açamıyor tooconnect gelen bağlantı noktası 9443 hello işlem sunucusu izin ver ve hello olup olmadığını denetleyin çıkar. İşlem sunucusu bu soruna neden olan DMZ olduğu bazı durumlarda açıldı.

* Hizmetin Hello durumunu denetlemek `InMage Scout VX Agent – Sentinel/OutpostStart` hello sorun devam ederse çalıştığından ve onay değilse.   
 
###<a name="check-hello-following-on-process-server"></a>İŞLEM sunucusundaki Hello aşağıdakileri denetleyin

* **İşlem sunucusu veri tooAzure etkin olarak gönderilmesi olmadığını denetleyin** 

İşlem sunucusu makineden hello Görev Yöneticisi'ni (Ctrl-Shift-Esc tuşuna basın) açın. Toohello performans sekmesine gidin ve 'Açık Kaynak İzleyicisi' bağlantısını tıklatın. Kaynak Yöneticisi'nden tooNetwork sekmesine gidin. Cbengine.exe 'Ağ etkinliği işlemlerle' ın büyük miktarda veri (MB) cinsinden etkin olarak gönderme olmadığını denetleyin.

![Çoğaltmayı etkinleştirme](./media/site-recovery-protection-common-errors/cbengine.png)

Aksi halde aşağıda listelenen hello adımları izleyin:

* **İşlem sunucusu mümkün tooconnect Azure Blob olup olmadığını denetle**: seçin ve işlem sunucusu tooAzure depolama blob URL'si bağlantısını cbengine.exe tooview hello 'TCP bağlantılarını' toosee denetleyin.

![Çoğaltmayı etkinleştirme](./media/site-recovery-protection-common-errors/rmonitor.png)

Aksi halde tooControl Masası Git > Hizmetleri denetleyin Hizmetleri aşağıdaki hello hazır ve çalışır olup olmadığını:

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
(Re) Hangi çalışmıyor herhangi bir hizmeti başlatın ve hello sorun hala olup olmadığını kontrol edin.

* **İşlem sunucusu bağlantı noktası 443 aracılığıyla mümkün tooconnect tooAzure genel IP adresi olup olmadığını denetleyin**

Açık gelen son CBEngineCurr.errlog hello `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` arayın ve: 443 ve bağlantı girişimi başarısız oldu.

![Çoğaltmayı etkinleştirme](./media/site-recovery-protection-common-errors/logdetails1.png)

Sorun varsa, telnet tooping işlem sunucusu komut satırından kullanmak hello CBEngineCurr.currLog bulundu (içinde görüntünün üzerinde maskelenmiş) Azure genel IP adresinizin 443 numaralı bağlantı noktasını kullanarak.

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
%S tooconnect varsa, hello erişim sorununu son toofirewall veya sonraki adımda açıklandığı gibi Proxy sonra kontrol edin.


* **IP adresi tabanlı Güvenlik Duvarı'nı işlem sunucusu engellemediğini varsa erişimi denetleme**: hello sunucuda bir IP adresi tabanlı güvenlik duvarı kuralları kullanıyorsanız, hello tam listesi Microsoft Azure veri merkezi IP aralıkları indirme [burada ](https://www.microsoft.com/download/details.aspx?id=41653) ve iletişim tooAzure (ve hello HTTPS (443 numaralı) bağlantı noktası) sağlarlar tooyour güvenlik duvarı yapılandırması tooensure ekleyin.  IP adres aralıklarını hello aboneliğinizin Azure bölgesi ve Batı ABD (erişim denetimi ve kimlik yönetimi için kullanılan) izin verir.

* **İşlem sunucusu URL'si tabanlı güvenlik duvarının erişimi engellemediğini varsa denetleyin**: hello sunucuda temel URL güvenlik duvarı kuralları kullanıyorsanız, aşağıdaki URL'lere hello toofirewall yapılandırma eklenir olduğundan emin olun. 
     
  `*.accesscontrol.windows.net:` Erişim denetimi ve kimlik yönetimi için kullanılır

  `*.backup.windowsazure.com:` Çoğaltma veri aktarımı ve düzenlemesi için kullanılır

  `*.blob.core.windows.net:`Erişim toohello için kullanılan veri depolayan bir depolama hesabı çoğaltılan

  `*.hypervrecoverymanager.windowsazure.com:` Çoğaltma yönetimi işlemleri ve düzenleme için kullanılır

  `time.nist.gov`ve `time.windows.com`: toocheck zaman eşitleme sistem genel zaman arasında kullanılır.

URL'ler için **Azure Bulutu**:

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* **İşlem sunucusundaki proxy ayarlarını erişim engellemediğinden varsa denetleyin**.  Bir Proxy sunucu kullanıyorsanız, hello DNS sunucusu tarafından hello proxy sunucu adı çözülürken emin olun.
toocheck yapılandırma sunucusu Kurulum hello sırasında sağlanan. Tooregistry anahtar gidin

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

Şimdi aynı ayarları Azure Site Recovery aracı toosend verilerini tarafından kullanılmakta olan bu hello emin olun.
Arama Microsoft Azure yedekleme 

![Çoğaltmayı etkinleştirme](./media/site-recovery-protection-common-errors/mab.png)

Bunu açıp eylemini tıklatın > özelliklerini değiştir. Proxy yapılandırma sekmesi altında hello kayıt defteri ayarları tarafından gösterildiği gibi aynı olması gerekir hello proxy adresi görmeniz gerekir. Aksi durumda, lütfen toohello değiştirin aynı adres.

![Çoğaltmayı etkinleştirme](./media/site-recovery-protection-common-errors/mabproxy.png)

* **Bant genişliği azaltma işlemi sunucu üzerinde sınırlı değildir, denetleme**: hello bant genişliğini artırmak ve hello sorun hala olup olmadığını kontrol edin.

##<a name="next-steps"></a>Sonraki adımlar
Daha fazla yardıma gereksinim duyarsanız, sorgunuzu çok sonrası[ASR Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr). Etkin bir topluluk sahibiz ve bizim mühendisleri birini mümkün tooassist olacaktır.
