---
title: aaaHow toouse PerfInsights Microsoft Azure | Microsoft Docs
description: "Öğrenir nasıl toouse PerfInsights tootroubleshoot Windows VM performans sorunlarını."
services: virtual-machines-windows'
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: genli
ms.openlocfilehash: f23ff7708c0c63bd02674b1bdc07753e8a89d9be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-perfinsights"></a>Nasıl toouse PerfInsights 

[PerfInsights](http://aka.ms/perfinsightsdownload) yararlı tanılama bilgileri toplar, g/ç yoğun yüklerini çalışır ve bir analiz raporu toohelp sağlar otomatik bir betik Microsoft Azure Windows VM performans sorunlarını giderme değil. 

VM performans sorunları için Microsoft ile bir destek bileti açmadan önce bu betik çalıştırmanızı öneririz.

## <a name="supported-troubleshooting-scenarios"></a>Sorun giderme senaryoları desteklenir

PerfInsights toplamak ve benzersiz senaryolarına gruplandırılır birkaç tür bilgiyi analiz edin.

### <a name="collect-disk-configuration"></a>Disk yapılandırmasını Topla 

Bu senaryo hello disk yapılandırması ve aşağıdaki öğelerindeki hello dahil olmak üzere diğer önemli bilgileri toplar:

-   Olay günlükleri

-   Tüm gelen ve giden bağlantıları için ağ durumu

-   Ağ ve güvenlik duvarı yapılandırma ayarları

-   Merhaba sistem üzerinde çalışmakta olan tüm uygulamalar için görev listesi

-   Bilgi dosyası msinfo32 hello sanal makine (VM) tarafından oluşturulan

-   Microsoft SQL Server veritabanı yapılandırma ayarlarını (Merhaba VM SQL Server çalıştıran bir sunucu belirlenirse)

-   Depolama güvenilirlik sayaçları

-   Önemli Windows düzeltmeleri

-   Yüklü filtre sürücüleri

Bu edilgen hello sistem etkileyen döndürmemelidir bilgi koleksiyonudur. 

>[!Note]
>Bu senaryoda her senaryoları aşağıdaki hello otomatik olarak dahil edilir.

### <a name="benchmarkstorage-performance-test"></a>Kıyaslama/depolama performans testi

Bu senaryo hello çalıştıran [diskspd](https://github.com/Microsoft/diskspd) olan tüm sürücüleri toohello VM ekli için Kıyaslama test (IOPS ve MB/sn). 

> [!Note]
> Bu senaryo hello sistem etkileyebilir ve canlı üretim sisteminde çalıştırılması gerekir. Gerekirse, bu senaryo bir adanmış bakım penceresi tooavoid içinde herhangi bir sorun çalıştırın. Bir izleme veya Kıyaslama test tarafından neden iş yükünün artmasına VM hello performansını olumsuz etkileyebilir.
>

### <a name="general-vm-slow-analysis"></a>Genel VM yavaş çözümleme 

Bu senaryo çalıştıran bir [performans sayacı](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) hello Generalcounters.txt dosyasında belirtilen hello sayaçları kullanarak izleme. Merhaba VM SQL Server çalıştıran bir sunucu belirlenirse, bir performans sayacı izlemesi hello Sqlcounters.txt dosyasında bulunan hello sayaçlarını kullanarak çalıştırır. Ayrıca, performans tanılama verilerini içerir.

### <a name="vm-slow-analysis-and-benchmark"></a>VM yavaş çözümleme ve Kıyaslama

Bu senaryo çalıştıran bir [performans sayacı](https://msdn.microsoft.com/library/windows/desktop/aa373083(v=vs.85).aspx) tarafından izlenen izleme bir [diskspd](https://github.com/Microsoft/diskspd) Kıyaslama test. 

> [!Note]
> Bu senaryo hello sistem etkileyebilir ve canlı üretim sisteminde çalıştırılması gerekir. Gerekirse, bu senaryo bir adanmış bakım penceresi tooavoid içinde herhangi bir sorun çalıştırın. Bir izleme veya Kıyaslama test tarafından neden iş yükünün artmasına VM hello performansını olumsuz etkileyebilir.
>

### <a name="azure-files-analysis"></a>Azure dosyaları çözümleme 

Bu senaryo, bir özel performans sayacı yakalama ağ izleme ile birlikte çalışır. Yakalama tüm hello "SMB istemci paylaşımları" sayaçlar içerir. Merhaba, hello yakalama parçası olan bazı anahtar SMB istemci paylaşımı performans sayaçları verilmiştir:

| **Tür**     | **SMB istemci paylaşımları sayacı** |
|--------------|-------------------------------|
| IOPS         | Veri isteği/sn             |
|              | Okuma isteği/sn             |
|              | Yazma İsteği/sn            |
| Gecikme süresi      | Ortalama sn/veri isteği         |
|              | Ortalama sn/Okuma                 |
|              | Ortalama sn/yazma                |
| G/ç boyutu      | Ort. Bayt/veri isteği       |
|              | Ort. Okunan bayt               |
|              | Ort. Bayt/yazma              |
| Aktarım hızı   | Veri bayt/sn                |
|              | Okuma Bayt/sn                |
|              | Yazma Bayt/sn               |
| Sırası uzunluğu | Ort. Okuma sırası uzunluğu        |
|              | Ort. Kuyruk uzunluğu yazma       |
|              | Ort. Veri sırası uzunluğu        |

### <a name="custom-configuration"></a>Özel yapılandırma 

Özel yapılandırma çalıştırdığınızda, kaç tane farklı izlemeleri seçili bağlı olarak tüm izlemeleri (Performans Tanılama, performans sayacı, XPerf'in, ağ, storport) paralel olarak çalışıyor. İzleme tamamlandıktan sonra seçiliyse hello aracı hello diskspd Kıyaslama çalışır. 

> [!Note]
> Bu senaryo hello sistem etkileyebilir ve canlı üretim sisteminde çalıştırılması gerekir. Gerekirse, bu senaryo bir adanmış bakım penceresi tooavoid içinde herhangi bir sorun çalıştırın. Bir izleme veya Kıyaslama test tarafından neden iş yükünün artmasına VM hello performansını olumsuz etkileyebilir.
>

## <a name="what-kind-of-information-is-collected-by-hello-script"></a>Hangi bilgilerin iletildiği hello komut dosyası tarafından toplanır?

Yapılandırma bilgilerini Windows VM, disk veya depolama havuzları, performans sayaçlarını, günlükleri ve çeşitli izlemeleri kullanılan hello performans senaryoyu bağlı olarak toplanır:

|Toplanan veriler                              |  |  | Performans senaryoları |  |  | |
|----------------------------------|----------------------------|------------------------------------|--------------------------|--------------------------------|----------------------|----------------------|
|                              | Disk yapılandırması Topla | Kıyaslama/depolama performans testi | Genel VM yavaş çözümleme | VM yavaş çözümleme ve Kıyaslama | Azure dosyaları çözümleme | Özel yapılandırma |
| Olay günlükleri bilgileri      | Evet                        | Evet                                | Evet                      | Evet                            | Evet                  | Evet                  |
| Sistem bilgileri               | Evet                        | Evet                                | Evet                      | Evet                            | Evet                  | Evet                  |
| Birim eşleme                       | Evet                        | Evet                                | Evet                      | Evet                            | Evet                  | Evet                  |
| Disk eşleme                         | Evet                        | Evet                                | Evet                      | Evet                            | Evet                  | Evet                  |
| Çalışan görevleri                    | Evet                        | Evet                                | Evet                      | Evet                            | Evet                  | Evet                  |
| Depolama güvenilirlik sayaçları     | Evet                        | Evet                                | Evet                      | Evet                            | Evet                  | Evet                  |
| Depolama birimi bilgileri              | Evet                        | Evet                                | Evet                      | Evet                            | Evet                  | Evet                  |
| Fsutil çıktı                    | Evet                        | Evet                                | Evet                      | Evet                            | Evet                  | Evet                  |
| Filtre sürücüsü bilgileri               | Evet                        | Evet                                | Evet                      | Evet                            | Evet                  | Evet                  |
| Netstat çıktı                   | Evet                        | Evet                                | Evet                      | Evet                            | Evet                  | Evet                  |
| Ağ yapılandırması            | Evet                        | Evet                                | Evet                      | Evet                            | Evet                  | Evet                  |
| Güvenlik duvarı yapılandırması           | Evet                        | Evet                                | Evet                      | Evet                            | Evet                  | Evet                  |
| SQL Server yapılandırma         | Evet                        | Evet                                | Evet                      | Evet                            | Evet                  | Evet                  |
| Performans Tanılama izlemelerini * |                            |                                    | Evet                      |                                |                      | Evet                  |
| Performans sayacı izleme **     |                            |                                    |                          |                                |                      | Evet                  |
| SMB sayaç izleme **             |                            |                                    |                          |                                | Evet                  |                      |
| SQL Server sayaç izleme **      |                            |                                    |                          |                                |                      | Evet                  |
| XPerf'in izleme                      |                            |                                    |                          |                                |                      | Evet                  |
| StorPort izleme                   |                            |                                    |                          |                                |                      | Evet                  |
| Ağ izleme                    |                            |                                    |                          |                                | Evet                  | Evet                  |
| Diskspd Kıyaslama izleme ***      |                            | Evet                                |                          | Evet                            |                      |                      |
|       |                            |                         |                                                   |                      |                      |

### <a name="performance-diagnostics-trace-"></a>Performans Tanılama izleme (*)

Bir kural tabanlı altyapısı hello arka plan toocollect verilerde çalışır ve devam eden performans sorunlarını tanılamanıza. Kuralları aşağıdaki hello şu anda desteklenir:

- HighCpuUsage kuralı: yüksek CPU kullanım dönemlerini algılar ve bu dönemlerde hello üst CPU kullanımı tüketicileri gösterir.
- HighDiskUsage kuralı: yüksek disk kullanım dönemlerini fiziksel disklerdeki algılar ve hello üst disk kullanımı tüketicileri bu dönemlerde gösterir.
- HighResolutionDiskMetric kuralı: IOPS, üretilen iş ve g/ç gecikmesi ölçümleri her fiziksel disk için 50 milisaniye başına gösterir. Bu nokta azaltma diski tanımlamak tooquickly yardımcı olur.
- HighMemoryUsage kuralı: yüksek bellek kullanım dönemlerini algılar ve hello üst bellek kullanımı tüketicileri bu dönemlerde gösterir.

> [!NOTE] 
> Şu anda hello .NET Framework 3.5 dahil Windows sürümleri veya sonraki sürümler desteklenir.

### <a name="performance-counter-trace-"></a>Performans sayacı izleme (*)

Performans sayaçlarını izleyerek hello toplar:

- \Process, \Processor, \Memory, \Thread, \PhysicalDisk, \LogicalDisk
- \Cache\Dirty sayfaları, \Cache\Lazy diske yazma/sn, \Server\Pool belleği olmayan havuz, hataları, disk belleğine alınan \Server\Pool hataları
- Seçili sayaçları \Network arabirimi, \IPv4\Datagrams, \IPv6\Datagrams, \TCPv4\Segments, \TCPv6\Segments, \Network bağdaştırıcısı, \WFPv4\Packets, \WFPv6\Packets, \UDPv4\Datagrams, \UDPv6\Datagrams, \TCPv4\Connection, \TCPv6\Connection, \Network QoS Policy\Packets, altında \Per \Microsoft Winsock BSP işlemci ağ arabirimi kartı etkinliği

#### <a name="for-sql-server-instances"></a>SQL Server örnekleri için
- \SQL sunucu: arabellek Yöneticisi, \SQLServer:Resource havuzu istatistikleri, \SQLServer:SQL Statistics\
- \SQLServer:Locks, \SQLServer:General, istatistikleri
- \SQLServer:Access yöntemleri

#### <a name="for-azure-files"></a>Azure dosyaları
\SMB istemci paylaşımları

### <a name="diskspd-benchmark-trace-"></a>Diskspd Kıyaslama izleme (*)
Diskspd g/ç iş yükü testleri [işletim sistemi diski (yazma) ve havuzu sürücüler (okuma/yazma)]

## <a name="run-hello-perfinsights-on-your-vm"></a>Merhaba PerfInsights, VM üzerinde çalışan

### <a name="what-do-i-have-tooknow-before-i-run-hello-script"></a>Merhaba betiği çalıştırmadan önce ne ı tooknow var mı? 

**Komut dosyası gereksinimleri**

1.  Bu komut dosyası hello hello performans sorunu olan VM üzerinde çalıştırmanız gerekir. 

2.  Merhaba aşağıdaki işletim sistemleri desteklenir: Windows Server 2008 R2, 2012, 2012 R2'de, 2016; Windows 8.1 ve Windows 10.

**Sanal makineleri üretim hello komut çalıştırdığınızda olası sorunlar:**

1.  XPerf'in veya DiskSpd kullanarak yapılandırılan hello "Kıyaslama" veya "Özel" senaryo ile birlikte kullanıldığında hello betik olumsuz hello VM hello performansını etkileyebilir. Bir üretim ortamında hello komut çalıştırdığınızda dikkatli olun.

2.  Merhaba komut DiskSpd kullanarak yapılandırılan hello "Kıyaslama" veya "Özel" senaryo ile birlikte kullandığınızda, başka bir arka plan etkinliği hello g/ç iş yükü test hello disklerde işlemini uğratan emin olun.

3.  Varsayılan olarak, hello betik hello geçici depolama sürücüsü toocollect verileri kullanır. Uzun bir süre boyunca etkin kalır izleme, toplanan veri miktarını hello ilgili olabilir. Bu, bu nedenle bu sürücüde güvenen herhangi bir uygulama etkileyen hello geçici disk alanı hello kullanılabilirliğini azaltabilir.

### <a name="how-do-i-run-perfinsights"></a>PerfInsights nasıl çalışır? 

toorun Merhaba komut dosyası, şu adımları izleyin:

1. Karşıdan [PerfInsights.zip](http://aka.ms/perfinsightsdownload).

2. Merhaba PerfInsights.zip dosya engellemesini. Bu, sağ hello PerfInsights.zip dosya toodo seçin **özellikleri**. Merhaba, **genel** sekmesine **Engellemeyi Kaldır** ve ardından **Tamam**. Bu ek güvenlik ister olmadan hello komut dosyasını çalıştırır emin olmanızı sağlar.  

    ![Merhaba zip dosyası kilidini aç](media/how-to-use-perfInsights/unlock-file.png)

3.  (Varsayılan olarak, genellikle hello D sürücüsü), geçici sürücüsüne sıkıştırılmış hello PerfInsights.zip dosyasını genişletin. Merhaba sıkıştırılmış dosyayı hello aşağıdakileri içermesi gereken dosyalar ve klasörler:

    ![Merhaba zip klasöründeki dosyaları](media/how-to-use-perfInsights/file-folder.png)

4.  Windows PowerShell'i yönetici olarak açın ve ardından hello PerfInsights.ps1 komut dosyasını çalıştırın.

    ```
    cd <hello path of PerfInsights folder >
    Powershell.exe -ExecutionPolicy UnRestricted -NoProfile -File .\\PerfInsights.ps1
    ```

    "Y" tooenter olabilir misiniz tooif toochange hello yürütme İlkesi istediğiniz tooconfirm sorulan.

    Merhaba sorumluluk reddi iletişim kutusunda hello seçeneği tooshare tanılama bilgilerini Microsoft Support verilir. Ayrıca toohello lisans sözleşmesi toocontinue onaylaması gerekir. Seçimlerinizi yapın ve ardından **komut dosyasını Çalıştır**.

    ![Vazgeçme kutusu](media/how-to-use-perfInsights/disclaimer.png)

5.  (Bizim istatistiklerini budur) hello komut çalıştırdığınızda, varsa hello olay numarasını gönderin. Ardından **Tamam**.
    
    ![Destek kimliği girin](media/how-to-use-perfInsights/enter-support-number.png)

6.  Geçici depolama sürücüsünü seçin. Merhaba betik otomatik-hello hello sürücünün harfini algılayabilir. Bu aşamada herhangi bir sorun meydana gelirse, olabilir tooselect hello sürücü istenir (Merhaba varsayılan sürücüdür D). Oluşturulan günlüklerin burada hello günlüğünde depolanan\_koleksiyon klasörü. Girin ya da hello sürücü harfini kabul edin sonra seçeneğini **Tamam**.

    ![Sürücü girin](media/how-to-use-perfInsights/enter-drive.png)

7.  Bir sorun giderme senaryosu listesi sağlanan hello seçin.

       ![Destek senaryoları seçin](media/how-to-use-perfInsights/select-scenarios.png)

8.  PerfInsights kullanıcı Arabirimi olmadan da çalıştırabilirsiniz.

    Merhaba aşağıdaki çalıştırır hello "Genel VM yavaş analiz UI istemi olmadan senaryo sorun giderme" komutunu veya 30 saniye verilerini yakalama. Tooconsent toohello ister aynı sorumluluk reddi ve 4. adımda anlatılan EULA'sı.

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30"

    Sessiz modda PerfInsights toorun istiyorsanız kullanın **- AcceptDisclaimerAndShareDiagnostics** parametresi. Örneğin, komutu aşağıdaki hello kullan:

        powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -NoGui -Scenario vmslow -TracingDuration 30 -AcceptDisclaimerAndShareDiagnostics"

### <a name="how-do-i-troubleshoot-issues-while-running-hello-script"></a>Sorunları hello komut dosyası çalıştırılırken nasıl gidermek?

Merhaba betik sonlandırılırsa ile birlikte hello komut dosyasını çalıştırarak tutarsız bir duruma temizleyebilirsiniz - temizleme anahtar şu şekilde hello:

    powershell.exe -ExecutionPolicy UnRestricted -NoProfile -Command ".\\PerfInsights.ps1 -Cleanup"

Merhaba otomatik algılanmasını hello geçici sürücü sırasında herhangi bir sorun meydana gelirse, olabilir tooselect hello sürücü istenir (Merhaba varsayılan sürücüdür D).

![Sürücü girin](media/how-to-use-perfInsights/enter-drive.png)

Merhaba betik hello yardımcı program araçları kaldırır ve geçici klasör kaldırır.

### <a name="troubleshooting-other-script-issues"></a>Diğer komut dosyası sorunlarını giderme 

Merhaba komut çalıştırdığınızda herhangi bir sorun oluşursa, Ctrl + C toointerrupt hello komut dosyası yürütme tuşuna basın. tooremove geçici nesneler hello "anormal şekilde sonlanmasından sonra temizleme" bölümüne bakın.

Birkaç denemeden sonra bile tooexperience komut dosyası hatası devam ederseniz, "hata ayıklama modunda" Merhaba betik çalıştırmak hello kullanarak öneririz "-Debug" Başlangıçta parametre seçeneği.

Hello hatası, kopyalama hello tam çıktısı hello PowerShell konsolunda oluşur ve size yardım toohello Microsoft Support aracı gönderme sonra toohelp hello sorun giderin.

### <a name="how-do-i-run-hello-script-in-custom-configuration-mode"></a>Özel yapılandırma modunda nasıl hello betik çalıştırılsın mı?

Merhaba seçerek **özel** yapılandırma, paralel (kullanın Shift toomulti-seçin) birkaç izlemeleri etkinleştirebilirsiniz:

![senaryoları seçin](media/how-to-use-perfInsights/select-scenario.png)

Merhaba tanıları seçtiğinizde, performans sayacı izleme, XPerf'in izleme, ağ izleme veya Storport izleme senaryoları hello iletişim kutularındaki hello yönergeleri izleyin ve tooreproduce hello yavaş performans sorunu hello izlemeleri başlattıktan sonra deneyin.

iletişim kutusu aşağıdaki Merhaba, bir izleme başlatmanızı sağlar:

![Start-izleme](media/how-to-use-perfInsights/start-trace-message.png)

toostop hello izlemeleri, ikinci bir iletişim kutusu tooconfirm hello komut sahip.

![İzlemeyi Durdur](media/how-to-use-perfInsights/stop-trace-message.png)
![İzlemeyi Durdur](media/how-to-use-perfInsights/ok-trace-message.png)

Ne zaman, izlemeleri hello veya işlemler tamamlanır, D: içinde yeni bir dosya oluşturulur\\günlük\_koleksiyonu (veya hello geçici sürücü) adlandırılan **CollectedData\_yyyy-aa-gg\_hh\_mm \_ss.zip.** Bu dosya toohello destek aracı analiz için gönderebilirsiniz.

## <a name="review-hello-diagnostics-report-created-by-perfinsights"></a>PerfInsights tarafından oluşturulan hello tanılama raporu gözden geçirin

Merhaba içinde **CollectedData\_yyyy-aa-gg\_hh\_mm\_ss.zip dosya** PerfInsights tarafından oluşturulan, hello bulgularını, ayrıntılı bir HTML raporu bulabilirsiniz PerfInsights. tooreview Merhaba raporu, hello genişletin **CollectedData\_yyyy-aa-gg\_hh\_mm\_ss.zip** dosya ve hello açın **PerfInsights raporu.HTML**dosya.

Select hello **bulgularını** sekmesi.

![Sekme Bul](media/how-to-use-perfInsights/findingtab.png)

**Notlar**

-   Kırmızı iletilerinde performans sorunlarına neden olabilir yapılandırma ilgili bilinen sorunlardır.

-   Sarı iletilerinde mutlaka performans sorunlarına neden olmaz en iyi olmayan yapılandırmalar temsil uyarılar var.

-   Mavi iletileri yalnızca bilgilendirici deyimleri edilir.

Daha ayrıntılı bilgiler hello bulgularını ve nasıl bunlar hello performans ya da performans için iyileştirilmiş yapılandırmaları için en iyi uygulamaları etkileyebilir hakkında gözden geçirme hello HTTP bağlantıları için kırmızı tooget tüm hata iletileri.

### <a name="disk-configuration-tab"></a>Disk yapılandırma sekmesi

Merhaba **genel bakış** bölümü hello depolama yapılandırmasının Diskpart ve depolama alanları bilgileri de dahil olmak üzere, farklı görünümleri görüntüler

Merhaba **DiskMap** ve **VolumeMap** bölümlerde çift açısı nasıl mantıksal birimler ve fiziksel diskleri olan diğer ilgili tooeach.

Hello PhysicalDisk perspektif (DiskMap), hello tablo hello disk üzerinde çalışan tüm mantıksal birimleri gösterir. Aşağıdaki örneğine hello PhysicalDrive2 birden çok bölüm (J ve Y) oluşturulan 2 mantıksal birimler çalıştırır:

![Veri sekmesi](media/how-to-use-perfInsights/disktab.png)

Merhaba birim perspektif içinde (*VolumeMap*), hello tablolarda her bir mantıksal birim altındaki tüm hello fiziksel diskleri gösterilmektedir. RAID/dinamik diskler için dikkat edin, mantıksal birimi birden fazla fiziksel diske bağlı çalışabilir. Örnek aşağıdaki hello içinde *C:\\bağlama* olduğu olarak yapılandırılan bir mountpoint *SpannedDisk* PhysicalDisks üzerinde \#2 ve \#3:

![Birim sekmesi](media/how-to-use-perfInsights/volumetab.png)

### <a name="sql-server-tab"></a>SQL Server sekmesi

Merhaba hedef VM hiç SQL Server örneği barındırıyorsa, ek bir sekme adlı hello raporunda görürsünüz **SQL Server**:

![SQL sekmesi](media/how-to-use-perfInsights/sqltab.png)

Bu bölüm, her hello SQL Server örneklerinin hello VM üzerinde barındırılan bir "Genel" ve ek alt sekme içerir.

Merhaba "Genel bakış" bölümüne çalıştıran ve veri dosyalarını ve işlem günlüğü dosyalarını bir karışımını içeren tüm hello fiziksel diskleri (sistem ve veri diskleri) özetler yararlı bir tablo içeriyor.

Örneğin, aşağıdaki hello içinde *PhysicalDrive0* (Merhaba C sürücüsü çalıştıran) görüntülenen her ikisi de hello çünkü *modeldev* ve *modellog* dosyaları hello C sürücüsünde bulunur ve farklı türde olan (veri dosyası ve işlem günlüğü gibi sırasıyla):

![ILogInformation](media/how-to-use-perfInsights/loginfo.png)

Merhaba SQL Server örneği özgü sekmeler hello seçilen örnek hakkındaki temel bilgileri görüntüleyen genel bir bölüm ve ayarları, yapılandırmaları ve kullanıcı seçenekleri de dahil olmak üzere Gelişmiş bilgi için ek bölümler içerir.

## <a name="references-toohello-external-tools-used"></a>Kullanılan toohello dış araçları başvurur

### <a name="diskspd"></a>Diskspd

DISKSPD bir depolama yük oluşturucuyu ve performans testi ekiplerinden hello Windows ve Windows Server ve bulut sunucu altyapısı mühendislik aracıdır. Daha fazla bilgi için bkz: [Diskspd](https://github.com/Microsoft/diskspd).

### <a name="xperf"></a>XPerf'in

XPerf'in bir komut satırı aracı toocapture izlemeleri hello Windows Performans araçları Seti olur.

Daha fazla bilgi için bkz: [Windows Performans Araç Seti – XPerf'in](https://blogs.msdn.microsoft.com/ntdebugging/2008/04/03/windows-performance-toolkit-xperf/).

## <a name="next-steps"></a>Sonraki Adımlar

### <a name="upload-diagnostics-logs-and-reports-toomicrosoft-support-for-further-review"></a>Karşıya yükleme tanılama günlüklerini ve daha fazla inceleme için destek tooMicrosoft raporları

Merhaba Microsoft Support personeli ile çalışırken, sorun giderme işlemi PerfInsights tooassist hello tarafından oluşturulan istenen tootransmit hello çıktı olabilir.

Merhaba destek aracı DTM çalışma alanı sizin için oluşturur ve bir bağlantı toohello [DTM portal (https://filetransfer.support.microsoft.com/EFTClient/Account/Login.htm) ve bir benzersiz bir kullanıcı kimliği ve parolası. içeren bir e-posta iletisi alırsınız

Bu iletinin gönderildiği **CTS otomatik tanılama Hizmetleri** (ctsadiag@microsoft.com).

![Merhaba ileti örneği](media/how-to-use-perfInsights/supportemail.png)

Ek güvenlik için parolanızı gerekli toochange olacaktır ilk kullanın.

İçinde tooDTM açtıktan sonra bir iletişim kutusu tooupload hello bulacaksınız **CollectedData\_yyyy-aa-gg\_hh\_mm\_ss.zip** PerfInsights tarafından toplanan dosya.
