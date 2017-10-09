---
title: "Azure yedekleme hatası sorunlarını giderme: Konuk Aracısı durumu kullanılamıyor | Microsoft Docs"
description: "Belirtiler, nedenleri ve çözümlemeleri, Azure Backup hataları ilgili tooerror: hello VM Aracısı ile iletişim kuramadı"
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
keywords: "Azure yedekleme; VM Aracısı; Ağ bağlantısı;"
ms.assetid: 4b02ffa4-c48e-45f6-8363-73d536be4639
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: genli;markgal;
ms.openlocfilehash: 724c61ba80d0a9ef91a5f8543ae72bb86968881b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-backup-failure-issues-with-agent-andor-extension"></a>Azure yedekleme hatası sorunlarını giderme: aracı ve/veya uzantısı ile ilgili sorunları

Bu makale, yedekleme hataları gidermek sorun giderme adımları toohelp tooproblems VM aracısı ve uzantı ile iletişimi ilgili sağlar.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="vm-agent-unable-toocommunicate-with-azure-backup"></a>VM Aracısı yüklenemiyor toocommunicate Azure yedekleme ile
Kaydolun ve hello Azure Backup hizmeti için bir VM zamanlama sonra yedekleme hello VM Aracısı tootake zaman içinde nokta anlık görüntü ile iletişim kurarak hello iş başlatır. Aşağıdaki koşullar hello birini sırayla tooBackup açabilir tetiklenen, gelen hello anlık görüntüsü engelleyebilir. Sorun giderme adımları sipariş verilen hello içinde aşağıda izleyin ve işlemi yeniden deneyin.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>1. neden: [hello VM sahip Internet erişimi yok](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Neden 2: [hello Aracısı hello VM yüklendi, ancak (Windows VM'ler için) yanıt vermiyor](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>3. neden: [hello VM yüklü hello aracısıdır (Linux VM'ler için) güncel](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>4. neden: [hello anlık görüntü durumu alınamıyor veya anlık görüntü alınamaz](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>5. neden: [hello yedekleme uzantısını tooupdate veya yükleme başarısız](#the-backup-extension-fails-to-update-or-load)

## <a name="snapshot-operation-failed-due-toono-network-connectivity-on-hello-virtual-machine"></a>Anlık görüntü işlemi hello sanal makineye toono ağ bağlantısı nedeniyle başarısız oldu
Kaydolun ve hello Azure Backup hizmeti için bir VM zamanlama sonra yedekleme hello VM backup uzantısı tootake bir nokta zaman snapshot ile iletişim kurarak hello iş başlatır. Aşağıdaki koşullar hello birini sırayla tooBackup açabilir tetiklenen, gelen hello anlık görüntüsü engelleyebilir. Sorun giderme adımları sipariş verilen hello içinde aşağıda izleyin ve işlemi yeniden deneyin.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>1. neden: [hello VM sahip Internet erişimi yok](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Neden 2: [hello anlık görüntü durumu alınamıyor veya anlık görüntü alınamaz](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-3-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>3. neden: [hello yedekleme uzantısını tooupdate veya yükleme başarısız](#the-backup-extension-fails-to-update-or-load)

## <a name="vmsnapshot-extension-operation-failed"></a>VMSnapshot uzantısı işlemi başarısız oldu

Kaydolun ve hello Azure Backup hizmeti için bir VM zamanlama sonra yedekleme hello VM backup uzantısı tootake bir nokta zaman snapshot ile iletişim kurarak hello iş başlatır. Aşağıdaki koşullar hello birini sırayla tooBackup açabilir tetiklenen, gelen hello anlık görüntüsü engelleyebilir. Sorun giderme adımları sipariş verilen hello içinde aşağıda izleyin ve işlemi yeniden deneyin.
##### <a name="cause-1-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>1. neden: [hello anlık görüntü durumu alınamıyor veya anlık görüntü alınamaz](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-2-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Neden 2: [hello yedekleme uzantısını tooupdate veya yükleme başarısız](#the-backup-extension-fails-to-update-or-load)
##### <a name="cause-3-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>3. neden: [hello VM sahip Internet erişimi yok](#the-vm-has-no-internet-access)
##### <a name="cause-4-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>4. neden: [hello Aracısı hello VM yüklendi, ancak (Windows VM'ler için) yanıt vermiyor](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-5-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>5. neden: [hello VM yüklü hello aracısıdır (Linux VM'ler için) güncel](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)

## <a name="unable-tooperform-hello-operation-as-hello-vm-agent-is-not-responsive"></a>Yüklenemiyor tooperform hello işlem olarak hello VM aracısı yanıt vermiyor

Kaydolun ve hello Azure Backup hizmeti için bir VM zamanlama sonra yedekleme hello VM backup uzantısı tootake bir nokta zaman snapshot ile iletişim kurarak hello iş başlatır. Aşağıdaki koşullar hello birini sırayla tooBackup açabilir tetiklenen, gelen hello anlık görüntüsü engelleyebilir. Sorun giderme adımları sipariş verilen hello içinde aşağıda izleyin ve işlemi yeniden deneyin.
##### <a name="cause-1-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>1. neden: [hello Aracısı hello VM yüklendi, ancak (Windows VM'ler için) yanıt vermiyor](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-2-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Neden 2: [hello VM yüklü hello aracısıdır (Linux VM'ler için) güncel](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-3-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>3. neden: [hello VM sahip Internet erişimi yok](#the-vm-has-no-internet-access)

## <a name="backup-failed-with-an-internal-error---please-retry-hello-operation-in-a-few-minutes"></a>Yedekleme bir iç hatayla başarısız oldu - Lütfen hello işlemi birkaç dakika içinde yeniden deneyin

Kaydolun ve hello Azure Backup hizmeti için bir VM zamanlama sonra yedekleme hello VM backup uzantısı tootake bir nokta zaman snapshot ile iletişim kurarak hello iş başlatır. Aşağıdaki koşullar hello birini sırayla tooBackup açabilir tetiklenen, gelen hello anlık görüntüsü engelleyebilir. Sorun giderme adımları sipariş verilen hello içinde aşağıda izleyin ve işlemi yeniden deneyin.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>1. neden: [hello VM sahip Internet erişimi yok](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-agent-installed-in-hello-vm-but-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Neden 2: [hello aracı yanıt vermeyen ancak hello VM (Windows VM'ler için) yüklü](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>3. neden: [hello VM yüklü hello aracısıdır (Linux VM'ler için) güncel](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>4. neden: [hello anlık görüntü durumu alınamıyor veya anlık görüntü alınamaz](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>5. neden: [hello yedekleme uzantısını tooupdate veya yükleme başarısız](#the-backup-extension-fails-to-update-or-load)


## <a name="causes-and-solutions"></a>Nedenler ve çözümler

### <a name="hello-vm-has-no-internet-access"></a>Merhaba VM Internet erişim yok
Merhaba dağıtımı gereksinimi başına hello VM Internet erişimi yok veya erişim toohello Azure altyapı engelleyen kısıtlamalar yerinde var.

toofunction doğru hello yedekleme uzantısı gerektiren bağlantı toohello Azure ortak IP adresleri. Merhaba uzantısını komutları tooan Azure Storage uç noktası (HTTP URL) toomanage hello anlık görüntüleri hello VM gönderir. Merhaba uzantısı genel Internet, sonunda yedekleme başarısız hiçbir erişim toohello varsa.

####  <a name="solution"></a>Çözüm
tooresolve hello sorunu, burada listelenen hello yöntemlerden birini deneyin.
##### <a name="allow-access-toohello-azure-datacenter-ip-ranges"></a>Toohello Azure veri merkezi IP aralıkları erişime izin ver

1. Merhaba elde [Azure veri merkezi IP listesi](https://www.microsoft.com/download/details.aspx?id=41653) tooallow erişimi.
2. Merhaba çalıştırarak Hello IP'leri engellemesini **yeni NetRoute** hello yükseltilmiş bir PowerShell penceresinde Azure VM cmdlet. Merhaba cmdlet'i yönetici olarak çalıştırın.
3. tooallow erişim toohello IP'leri, varsa kuralları toohello ağ güvenlik grubu ekleyin.

##### <a name="create-a-path-for-http-traffic-tooflow"></a>HTTP trafiği tooflow için bir yol oluşturma

1. (Örneğin, bir ağ güvenlik grubu) yerinde ağ kısıtlamalarını varsa, bir HTTP proxy sunucusu tooroute hello trafiği dağıtın.
2. Merhaba HTTP proxy sunucusundan tooallow erişim toohello Internet varsa kuralları toohello ağ güvenlik grubu ekleyin.

VM yedeklemeler için bir HTTP proxy yukarı tooset nasıl görürüm toolearn [Azure sanal makineleri yedeklemek, ortam tooback hazırlama](backup-azure-vms-prepare.md#using-an-http-proxy-for-vm-backups).

Yönetilen diskleri kullanarak durumunda bir ek bağlantı noktası (8443) açarak hello güvenlik duvarlarında gerekebilir.

### <a name="hello-agent-installed-in-hello-vm-but-unresponsive-for-windows-vms"></a>yanıt vermeyen ancak hello VM (Windows VM'ler için) yüklü hello Aracısı

#### <a name="solution"></a>Çözüm
Merhaba VM Aracısı bozulmuş veya hello hizmeti durdurulmuş. Yeniden yükleme hello VM Aracısı hello en son sürümünü alın ve hello iletişimi yeniden yardımcı olacaktır.

1. Doğrulama Windows Konuk Aracısı hizmeti (services.msc) Hizmetleri içinde çalışan sanal makine hello olup olmadığını. Merhaba Windows Konuk Aracısı hizmetini yeniden başlatın ve hello yedekleme başlatmak deneyin<br>
2. hizmetlerinde görünür durumda değilse, programlar ve özellikler Windows Konuk aracısı yüklü olup olmadığını doğrulayın.
4. Programlar ve Özellikler altında mümkün tooview varsa Windows Konuk aracısı kaldırma hello.
5. Merhaba yükleyip [Aracısı MSI en son sürümünü](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Yönetici ayrıcalıkları toocomplete hello yüklemesi gerekir.
6. Ardından mümkün tooview Windows Konuk Aracısı hizmetlerinin Hizmetleri'ndeki olmalıdır
7. "Yedekleme şimdi" Merhaba Portalı'nda tıklayarak üzerinde-isteğe bağlı/geçici bir yedeklemeyi çalıştırmayı deneyin.

Ayrıca, sanal makinenin doğrulayın  **[hello sistemde yüklü .NET 4.5](https://docs.microsoft.com/en-us/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed)**. Merhaba hizmeti ile Merhaba VM Aracısı toocommunicate için gereklidir

### <a name="hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vms"></a>Merhaba VM yüklü hello Aracısı (Linux VM'ler için) güncel değil

#### <a name="solution"></a>Çözüm
Aracı veya uzantı ilgili hataları Linux VM'ler için en güncel olmayan bir VM Aracısı etkileyen sorunları neden olur. tootroubleshoot Bu sorun, şu genel yönergeleri izleyin:

1. Merhaba yönergeleri izleyin [hello Linux VM Aracısı güncelleştirme](../virtual-machines/linux/update-agent.md).

 >[!NOTE]
 >Biz *tavsiye* yalnızca bir dağıtım deposu aracılığıyla hello aracısını güncelleştirin. Doğrudan Github'dan hello aracısı kodu indiriliyor ve güncelleştirmeden önermiyoruz. Merhaba en son aracı dağıtımınız için uygun değilse, yönergeler için dağıtım desteğine başvurun tooinstall onu. Merhaba en son aracı, Git toohello toocheck [Windows Azure Linux Aracısı](https://github.com/Azure/WALinuxAgent/releases) hello GitHub deposunu sayfasında.

2. Bu hello Azure Aracısı hello aşağıdaki komutu çalıştırarak hello VM üzerinde çalıştığından emin olun:`ps -e`

 Merhaba işlem çalışmıyorsa hello aşağıdaki komutları kullanarak yeniden başlatın:

 * Ubuntu için:`service walinuxagent start`
 * Diğer dağıtımlar için:`service waagent start`

3. [Merhaba otomatik yeniden başlatma Aracısı'nı yapılandırma](https://github.com/Azure/WALinuxAgent/wiki/Known-Issues#mitigate_agent_crash).
4. Yeni bir test yedekleme çalıştırın. Merhaba hata devam ederse, lütfen günlükleri hello Müşteri'nin VM'den aşağıdaki hello toplayın:

   * /var/lib/waagent/*.XML
   * /var/log/waagent.log
   * / var/oturum/azure / *

Ayrıntılı günlük kaydı için waagent gerekiyorsa, şu adımları izleyin:

1. Merhaba /etc/waagent.conf dosyasında aşağıdaki satırı hello bulun: **ayrıntılı günlük kaydını etkinleştir (y | n)**
2. Değişiklik hello **Logs.Verbose** değeri  *n*  çok*y*.
3. Merhaba değişikliği kaydetmek ve bu bölümdeki hello önceki adımları izleyerek waagent yeniden başlatın.

### <a name="hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Başlangıç anlık görüntü durum alınamadığı veya anlık görüntü alınamaz
Merhaba VM yedekleme, bir anlık görüntü komutu toohello temel alınan depolama hesabı veren kullanır. Yedekleme, hiçbir erişim toohello depolama hesabı olduğundan veya hello anlık görüntü görevi hello yürütme gecikmesi nedeniyle başarısız olabilir.

#### <a name="solution"></a>Çözüm
Aşağıdaki koşullar hello anlık görüntü görev başarısız olmasına neden olabilir:

| Nedeni | Çözüm |
| --- | --- |
| Merhaba VM yapılandırılmış SQL Server Yedekleme sahiptir. | Varsayılan olarak, hello VM yedekleme Windows Vm'lerinde VSS tam yedekleme çalıştırır. Hangi SQL Server ve SQL Server tabanlı sunucular çalıştırmakta olan VM'ler üzerinde anlık görüntü yürütme gecikmeler oluşabilir yedekleme yapılandırılır.<br><br>Bir yedekleme hata nedeniyle bir anlık görüntü sorun yaşıyorsanız, aşağıdaki kayıt defteri anahtarı hello ayarlayın:<br><br>**[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT] "USEVSSCOPYBACKUP"="TRUE"** |
| RDP Hello VM kapatılmış olduğundan hello VM durumu yanlış bildirilir. | Merhaba VM Uzak Masaüstü Protokolü (RDP) içinde kapatmak, hello portal toodetermine hello VM durumu doğru olup olmadığını denetleyin. Doğru değilse, hello VM hello portalında hello kullanarak kapatmak **kapatma** hello VM Panoda seçeneği. |
| Merhaba aynı bulut hizmeti olan birçok VM'lerin yapılandırılmış hello tooback yukarı aynı anda. | En iyi yöntem toospread olduğu aynı bulut hizmeti hello hello gelen VM'ler için yedekleme zamanlamaları çıkışı. |
| Merhaba VM yüksek CPU veya bellek kullanımı çalışıyor. | Hello VM yüksek CPU kullanımı (yüzde 90) veya yüksek bellek kullanımı çalışıyorsa, hello anlık görüntü görev sıraya alındı ve Gecikmeli ve zaman aşımına uğrar. Bu durumda, bir talep üzerine yedekleme deneyin. |
| Merhaba VM hello konak/doku adresi DHCP'den alamaz. | DHCP hello Iaas VM yedekleme toowork hello Konuk içinde etkinleştirilmesi gerekir.  Merhaba VM hello konak/doku adresi 245 DHCP yanıttan alınamıyor, dosya indirme veya tüm uzantılar çalıştırın. Statik bir özel IP gerekiyorsa, hello platformu ile yapılandırmanız gerekir. Merhaba VM bırakılmalıdır hello etkin içinde DHCP seçeneği. Daha fazla bilgi için bkz: [statik iç özel IP ayarı](../virtual-network/virtual-networks-reserved-private-ip.md). |

### <a name="hello-backup-extension-fails-tooupdate-or-load"></a>Merhaba yedekleme uzantısını tooupdate veya yükleme başarısız
Uzantılar yüklenemiyor çünkü bir anlık görüntü alınamaz yedekleme başarısız olur.

#### <a name="solution"></a>Çözüm

**Windows konuklar için:** hello iaasvmprovider hizmetinin etkin ve bir başlangıç türü doğrulayın *otomatik*. Merhaba hizmet bu şekilde yapılandırılmamışsa, hello sonraki yedekleme başarılı olup olmadığını toodetermine etkinleştirin.

**Linux konuklar için:** doğrula hello en son sürümünü VMSnapshot Linux (Yedekleme tarafından kullanılan hello uzantısı) için olan 1.0.91.0.<br>


Merhaba yedekleme uzantısını tooupdate veya yük yine başarısız olursa hello uzantısı kaldırarak yeniden hello VMSnapshot uzantısı toobe zorlayabilirsiniz. Merhaba sonraki yedekleme girişiminde hello uzantısı yeniden yükleyecektir.

toouninstall Merhaba uzantısı, aşağıdaki hello:

1. Toohello Git [Azure portal](https://portal.azure.com/).
2. Merhaba yedekleme sorunları olan VM bulun.
3. Tıklatın **ayarları**.
4. Tıklatın **uzantıları**.
5. Tıklatın **Vmsnapshot uzantısı**.
6. Tıklatın **kaldırma**.

Bu yordamı hello sonraki yedekleme sırasında yeniden hello uzantısı toobe neden olur.

