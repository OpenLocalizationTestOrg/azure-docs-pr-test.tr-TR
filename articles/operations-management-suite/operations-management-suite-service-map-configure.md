---
title: "Operations Management Suite hizmet eşlemesinde aaaConfigure | Microsoft Docs"
description: "Linux sistemleri ve haritalar Hizmetleri arasındaki iletişimi hello ve hizmet Haritası Windows uygulama bileşenleri otomatik olarak bulur bir Operations Management Suite çözümüdür. Bu makalede hizmet Haritası ortamınıza dağıtmak ve çeşitli senaryolarda içinde kullanma ile ilgili ayrıntıları sağlar."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: d3d66b45-9874-4aad-9c00-124734944b2e
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/18/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: 3127f4440f2886370f8ff617c405c6d70a926eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-service-map-in-operations-management-suite"></a>Operations Management Suite içinde hizmet Haritası yapılandırın
Hizmet eşlemesi sistemlerde, Windows ve Linux uygulama bileşenleri otomatik olarak bulur ve Hizmetleri arasındaki iletişimi eşlemeleri hello. Sunucularınızın siz bunları--Kritik hizmetler sunan birbirine bağlı sistemler olarak düşündüğünüz tooview kullanabilirsiniz. Hizmet eşlemesi gerekli, bir aracı yüklemesini dışındaki herhangi bir yapılandırma TCP bağlı mimarisiyle boyunca sunucuları, işlemleri ve bağlantı noktaları arasındaki bağlantıları gösterir.

Bu makalede hizmet Haritası ve ekleme aracıları yapılandırma ayrıntılarını hello açıklanmaktadır. Hizmet eşlemesi kullanarak hakkında daha fazla bilgi için bkz: [Operations Management Suite hello hizmet Haritası çözümü kullanan](operations-management-suite-service-map.md).

## <a name="dependency-agent-downloads"></a>Bağımlılık Aracısı indirir
| Dosya | İşletim Sistemi | Sürüm | SHA-256 |
|:--|:--|:--|:--|
| [InstallDependencyAgent Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |


## <a name="connected-sources"></a>Bağlı kaynaklar
Hizmet eşlemesi hello Microsoft bağımlılık Aracısı ' verileri alır. Merhaba bağımlılık Aracısı hello OMS aracısı için kendi bağlantıları tooOperations yönetim paketine bağlıdır. Başka bir deyişle, bir sunucu OMS Aracısı yüklenir ve ilk ve bağımlılık aracısı yüklü hello yapılandırılmış hello olması gerekir. Merhaba aşağıdaki tabloda hello hizmet Haritası çözümünü destekler hello bağlı kaynakları açıklanmaktadır.

| Bağlı kaynak | Destekleniyor | Açıklama |
|:--|:--|:--|
| Windows aracıları | Evet | Hizmet eşlemesi analiz eder ve Windows Aracısı bilgisayarlardan verileri toplar. <br><br>Toplama toohello içinde [OMS Aracısı](../log-analytics/log-analytics-windows-agents.md), Windows aracıları hello Microsoft bağımlılık Aracısı gerektirir. Merhaba bkz [desteklenen işletim sistemleri](#supported-operating-systems) işletim sistemi sürümleri tam bir listesi. |
| Linux aracıları | Evet | Hizmet eşlemesi analiz eder ve Linux Aracısı bilgisayarlardan verileri toplar. <br><br>Toplama toohello içinde [OMS Aracısı](../log-analytics/log-analytics-linux-agents.md), Linux aracılarını hello Microsoft bağımlılık Aracısı gerektirir. Merhaba bkz [desteklenen işletim sistemleri](#supported-operating-systems) işletim sistemi sürümleri tam bir listesi. |
| System Center Operations Manager yönetim grubu | Evet | Hizmet eşlemesi Windows ve Linux aracıları bağlı bir veri toplar ve analiz eder [System Center Operations Manager yönetim grubu](../log-analytics/log-analytics-om-agents.md). <br><br>Merhaba System Center Operations Manager Aracısı bilgisayar tooOperations arasında doğrudan bağlantı Yönetim Paketi gereklidir. Veri hello yönetim grubu toohello Operations Management Suite depodan iletilir.|
| Azure depolama hesabı | Hayır | Hiçbir verilerden nedenle hizmet eşlemesi toocollect Azure depolama biriminden Aracısı bilgisayarlardan verileri toplar. |

Hizmet eşlemesi yalnızca 64-bit platformları destekler.

Windows hello Microsoft İzleme Aracısı'nı (MMA) hem System Center Operations Manager ve Operations Management Suite toogather hem de izleme verileri gönder tarafından kullanılır. (Bu aracı hello System Center Operations Manager Aracısı, OMS Aracısı, günlük analizi Aracısı, MMA veya doğrudan Aracısı hello bağlam bağlı olarak adlandırılır.) System Center Operations Manager ve Operations Management Suite hello MMA farklı hello kutu sürümleri sağlar. Bu sürümleri her tooSystem Center Operations Manager, tooOperations Management Suite veya tooboth bildirebilirsiniz.  

Linux üzerinde Linux toplar ve veri tooOperations Management Suite izleme gönderir için OMS aracısının hello. Hizmet eşlemesi OMS doğrudan aracılarıyla sunucularda veya System Center Operations Manager Yönetim grupları aracılığıyla ekli tooOperations Management Suite olan sunucular kullanabilirsiniz.  

Bu makalede, biz tooall aracıları--olup başvurmak Linux veya Windows olup olmadığını bağlı tooa System Center Operations Manager yönetim grubu veya doğrudan tooOperations Management Suite--"OMS Aracısı" Merhaba gibi Bağlam için yalnızca gerekli ise hello belirli dağıtım adı hello Aracısı'nın kullanacağız.

Merhaba hizmet Haritası Aracısı tüm verileri aktarmaz ve herhangi bir değişiklik toofirewalls veya bağlantı noktalarını gerektirmez. Hizmet eşlemesi Hello verilerde hello OMS Aracısı tooOperations Yönetim Paketi tarafından her zaman doğrudan veya hello OMS ağ geçidi üzerinden aktarılır.

![Hizmet eşlemesi aracıları](media/oms-service-map/agents.png)

Bir yönetim grubu bağlı tooOperations Management Suite ile System Center Operations Manager müşteri varsa:

- System Center Operations Manager aracıları hello Internet tooconnect tooOperations Management Suite erişebiliyorsanız, ek yapılandırma gereklidir.  
- System Center Operations Manager aracıları Operations Management Suite hello Internet erişemiyorsanız tooconfigure hello OMS ağ geçidi toowork System Center Operations Manager ile gerekir.
  
Merhaba OMS doğrudan aracı kullanıyorsanız, tooconnect tooOperations Management Suite veya tooyour OMS ağ geçidi tooconfigure hello OMS Aracısı kendisini gerekir. Merhaba OMS ağ geçidi hello indirilebilir [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).

### <a name="management-packs"></a>Yönetim paketleri
Hizmet eşlemesi bir Operations Management Suite çalışma alanı içinde etkinleştirildiğinde, 300-KB Yönetim Paketi bu çalışma alanında tooall hello Windows sunucuları gönderilir. System Center Operations Manager aracıları kullanıyorsanız, bir [bağlı yönetim grubu](../log-analytics/log-analytics-om-agents.md), hello hizmet Haritası Yönetim Paketi System Center Operations Manager'dan dağıtılır. Merhaba aracıları doğrudan bağlıysanız, Operations Management Suite hello Yönetim Paketi sunar.

Merhaba Yönetim Paketi Microsoft.IntelligencePacks.ApplicationDependencyMonitor olarak adlandırılır. Buna ait yazılı too%Programfiles%\Microsoft izleme Agent\Agent\Health hizmet State\Management Packs\. Merhaba hello Yönetim Paketi kullanan veri kaynağı olan % Program files%\Microsoft izleme Agent\Agent\Health hizmet State\Resources\<AutoGeneratedID > \ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.

## <a name="installation"></a>Yükleme
### <a name="install-hello-dependency-agent-on-microsoft-windows"></a>Microsoft Windows Hello bağımlılık Aracısı yükleme
Yönetici ayrıcalıkları gerekli tooinstall ya da hello aracısını kaldırın.

Merhaba bağımlılık Aracısı InstallDependencyAgent Windows.exe üzerinden Windows bilgisayarlara yüklenir. Bu yürütülebilir dosya seçenekleri olmadan çalıştırırsanız, tooinstall etkileşimli olarak izleyebileceğiniz bir sihirbazı başlatır.  

Adımları tooinstall hello bağımlılık Aracısı her Windows bilgisayarda aşağıdaki hello kullan:

1.  Yükleme hello yönergeleri kullanarak OMS Aracısı hello [bağlanmak Windows bilgisayarları toohello Azure günlük analizi hizmeti](../log-analytics/log-analytics-windows-agents.md).
2.  Merhaba Windows Aracısı'nı indirin ve çalıştırın komutu aşağıdaki hello kullanarak: <br>`InstallDependencyAgent-Windows.exe`
3.  Merhaba Sihirbazı tooinstall hello Aracısı izleyin.
4.  Merhaba bağımlılık Aracısı toostart başarısız olursa, ayrıntılı hata bilgileri için hello günlüklerini denetleyin. Windows aracısında %Programfiles%\Microsoft bağımlılık Agent\logs hello günlük dizindir. 

#### <a name="windows-command-line"></a>Windows komut satırı
Merhaba tablo tooinstall komut satırından aşağıdaki seçenekleri kullanın. toosee hello kullanarak hello yükleyiciyi çalıştırmak, hello yükleme bayrakları listesini /? aşağıdaki gibi bayrak.

    InstallDependencyAgent-Windows.exe /?

| Bayrağı | Açıklama |
|:--|:--|
| /? | Merhaba komut satırı seçeneklerinin listesini alın. |
| / S | Kullanıcı etkileşimi ile sessiz bir yükleme gerçekleştirin. |

Merhaba Windows bağımlılık aracısı için dosyalar varsayılan olarak C:\Program Files\Microsoft bağımlılık Aracısı yerleştirilir.

### <a name="install-hello-dependency-agent-on-linux"></a>Linux'ta Hello bağımlılık Aracısı yükleme
Kök erişimi gerekli tooinstall ya da hello Aracısı yapılandırın.

Merhaba bağımlılık Aracısı InstallDependencyAgent Linux64.bin, kendiliğinden açılan bir ikili içeren bir kabuk betiği aracılığıyla Linux bilgisayarlara yüklenir. Merhaba Paylaş kullanarak dosyasını çalıştırın ya da eklemek izinleri toohello dosyasının kendisini yürütün.
 
Adımları tooinstall hello bağımlılık Aracısı her bir Linux bilgisayarda aşağıdaki hello kullan:

1.  Yükleme hello yönergeleri kullanarak OMS Aracısı hello [toplamak ve Linux bilgisayarları veri yönetmek](https://technet.microsoft.com/library/mt622052.aspx).
2.  Merhaba Linux bağımlılık Aracısı, komutu aşağıdaki hello kullanarak kök olarak yükleyin:<br>`sh InstallDependencyAgent-Linux64.bin`
3.  Merhaba bağımlılık Aracısı toostart başarısız olursa, ayrıntılı hata bilgileri için hello günlüklerini denetleyin. Linux aracısında /var/opt/microsoft/dependency-agent/log hello günlük dizindir.

toosee ile Merhaba yükleme programını çalıştırmak, hello yükleme bayrakları listesini hello - Yardım bayrağı gibi.

    InstallDependencyAgent-Linux64.bin -help

| Bayrağı | Açıklama |
|:--|:--|
| -Yardım | Merhaba komut satırı seçeneklerinin listesini alın. |
| -s | Kullanıcı etkileşimi ile sessiz bir yükleme gerçekleştirin. |
| --denetleyin | İzinler ve hello işletim sistemi denetle, ancak hello Aracısı yüklemeyin. |

Merhaba bağımlılık aracısı için dosyalar dizinleri izleyen hello yerleştirilir:

| Dosyalar | Konum |
|:--|:--|
| Çekirdek dosyaları | /OPT/Microsoft/Dependency-Agent |
| Günlük dosyaları | /var/OPT/Microsoft/Dependency-Agent/log |
| Yapılandırma dosyaları | /etc/OPT/Microsoft/Dependency-Agent/config |
| Hizmet yürütülebilir dosyalar | /OPT/Microsoft/Dependency-Agent/bin/Microsoft-Dependency-Agent<br>/OPT/Microsoft/Dependency-Agent/bin/Microsoft-Dependency-Agent-Manager |
| İkili depolama dosyaları | /var/OPT/Microsoft/Dependency-Agent/Storage |

## <a name="installation-script-examples"></a>Yükleme komut dosyası örnekleri
tooeasily hello bağımlılık Aracısı pek çok sunucu üzerinde aynı anda dağıtabilir, bir komut dosyası toouse yardımcı olur. Aşağıdaki komut örnekleri toodownload hello kullanın ve Windows ya da Linux hello bağımlılık aracısı yükleyin.

### <a name="powershell-script-for-windows"></a>Windows PowerShell Betiği
```PowerShell
Invoke-WebRequest "https://aka.ms/dependencyagentwindows" -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S
```

### <a name="shell-script-for-linux"></a>Linux için kabuk komut dosyası
```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
sh InstallDependencyAgent-Linux64.bin -s
```

## <a name="desired-state-configuration"></a>İstenen Durum Yapılandırması
toodeploy hello bağımlılık Aracısı istenen durum yapılandırması hello xPSDesiredStateConfiguration modülü ve biraz kod hello aşağıdaki gibi kullanabilirsiniz:
```
configuration ServiceMap {

Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = "C:\InstallDependencyAgent-Windows.exe"

Node localhost
{ 
    # Download and install hello Dependency Agent
    xRemoteFile DAPackage 
    {
        Uri = "https://aka.ms/dependencyagentwindows"
        DestinationPath = $DAPackageLocalPath
    }

    xPackage DA
    {
        Ensure="Present"
        Name = "Dependency Agent"
        Path = $DAPackageLocalPath
        Arguments = '/S'
        ProductId = ""
        InstalledCheckRegKey = "HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent"
        InstalledCheckRegValueName = "DisplayName"
        InstalledCheckRegValueData = "Dependency Agent"
        DependsOn = "[xRemoteFile]DAPackage"
    }
  }
}
```

## <a name="uninstallation"></a>Kaldırma
### <a name="uninstall-hello-dependency-agent-on-windows"></a>Bağımlılık Aracısı'nı Windows Hello kaldırma
Bir yönetici için hello bağımlılık Aracısı Windows Denetim Masası'ndan kaldırabilirsiniz.

Bir yönetici, %Programfiles%\Microsoft bağımlılık Agent\Uninstall.exe toouninstall hello bağımlılık aracısı olarak da çalıştırabilirsiniz.

### <a name="uninstall-hello-dependency-agent-on-linux"></a>Merhaba bağımlılık Aracısı'nı Linux kaldırma
Bağımlılık Aracısı'ndan Linux toocompletely kaldırma Merhaba, hello aracı ile otomatik olarak yüklenen bağlayıcı hello ve hello aracının kendisi kaldırmanız gerekir. Hem tek bir komut aşağıdaki hello kullanarak kaldırabilirsiniz:

    rpm -e dependency-agent dependency-agent-connector

## <a name="troubleshooting"></a>Sorun giderme
Yükleme veya hizmet Haritası çalıştıran herhangi bir sorun varsa, bu bölümde, yardımcı olabilir. Sorununuzu hala çözümleyemiyorsa, lütfen Microsoft Support başvurun.

### <a name="dependency-agent-installation-problems"></a>Bağımlılık Aracısı yükleme sorunları
#### <a name="installer-asks-for-a-reboot"></a>Yeniden başlatma için yükleyici sorar
Merhaba bağımlılık Aracısı *genellikle* yükleme veya kaldırma işlemi sırasında yeniden başlatma gerektirmez. Ancak, bazı nadir durumlarda, Windows Server yükleme ile bir yeniden başlatma toocontinue gerektirir. Bu, bağımlılık, genellikle Microsoft Visual C++ yeniden dağıtılabilir, hello kilitli bir dosyayı nedeniyle yeniden başlatma gerektiren ortaya çıkar.

#### <a name="message-unable-tooinstall-dependency-agent-visual-studio-runtime-libraries-failed-tooinstall-code--codenumber-appears"></a>İleti "oluşturulamıyor tooinstall bağımlılık aracısı: Visual Studio çalışma zamanı kitaplıkları tooinstall başarısız oldu (kod [code_number] =)" görüntülenir

Merhaba Microsoft bağımlılık Aracısı hello Microsoft Visual Studio çalışma zamanı kitaplıkları üzerinde oluşturulmuştur. Merhaba kitaplıkları yükleme sırasında bir sorun varsa bir ileti alırsınız. 

Merhaba çalışma zamanı kitaplığı yükleyicileri günlükleri hello %LOCALAPPDATA%\temp klasöründe oluşturun. Merhaba dosyasıdır dd_vcredist_arch_yyyymmddhhmmss.log, burada *arch* "x86" veya "amd64" ve *YYYYMMDD'nin* hello tarih ve saate hello günlük ne zaman oluşturulduğu (24 saat cinsinden). Merhaba günlük yükleme engelleme hello sorun hakkında ayrıntılar sağlar.

Yararlı tooinstall hello olabilir [son çalışma zamanı kitaplıkları](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) kendiniz ilk.

Merhaba aşağıdaki tabloda kod numaraları ve önerilen çözümler listelenmektedir.

| Kod | Açıklama | Çözüm |
|:--|:--|:--|
| 0x17 | Merhaba kitaplığı yükleyicinin yüklenmemiştir bir Windows güncelleştirmesi gerekir. | Merhaba en son kitaplığı yükleyici günlüğüne bakın.<br><br>Bir referans varsa "Windows8.1-KB2999226-x64.msu" bir çizgiyle çok izlenir "hata 0x80240017: başarısız tooexecute MSU paket," Merhaba Önkoşullar tooinstall KB2999226 yok. Merhaba önkoşullar bölümünde Hello yönergeleri [Windows Evrensel C çalışma zamanı](https://support.microsoft.com/kb/2999226). Toorun Windows Update ihtiyacınız ve birden çok kez sipariş tooinstall hello önkoşulları yeniden başlatın.<br><br>Merhaba Microsoft bağımlılık Aracısı yükleyiciyi yeniden çalıştırın. |

### <a name="post-installation-issues"></a>Yükleme sonrası sorunları
#### <a name="server-doesnt-appear-in-service-map"></a>Sunucu hizmet eşlemesinde görünmüyor
Bağımlılık Aracısı yükleme başarılı oldu, ancak sunucunuzun hello hizmet Haritası çözüm görmüyorum varsa:
* Merhaba bağımlılık Aracısı başarıyla yüklenir? Bu, hello hizmetini yüklediyseniz toosee denetleniyor ve çalıştırarak doğrulayabilirsiniz.<br><br>
**Windows**: "Microsoft Dependency Aracısı" adlı hello hizmeti için Ara<br>
**Linux**: işlemin "microsoft-bağımlılık-agent." Merhaba arayın

* Merhaba üzerinde olduğunuz [ücretsiz fiyatlandırma katmanı Operations Management Suite/Log Analytics,](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)? hello ücretsiz planı toofive benzersiz hizmet Haritası sunucuları için sağlar. Merhaba önceki beş artık gönderme olsa bile veri herhangi bir sonraki sunucu hizmet eşlemesinde görünmez.

* Sunucu gönderen günlük ve performans verileri tooOperations Management Suite nedir? TooLog arama gidin ve bilgisayarınız için sorgu aşağıdaki hello çalıştırın: 

        * Computer="<your computer name here>" | measure count() by Type
        
  Merhaba sonuçlarında olayları çeşitli mı aldınız? Merhaba veri son mi? Öyleyse, OMS Aracısı doğru işletim ve hello Operations Management Suite hizmeti ile iletişim. Değilse, sunucunuzdaki hello OMS Aracısı kontrol edin: [OMS Aracısı Windows için sorun giderme](https://support.microsoft.com/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues) veya [Linux sorun giderme için OMS aracısının](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md).

#### <a name="server-appears-in-service-map-but-has-no-processes"></a>Sunucu hizmet eşlemesinde görünür ancak hiçbir işlem var
Hizmet eşlemesi sunucunuzun bakın, ancak bu hello gösteren hiçbir işlem veya bağlantı veri varsa bağımlılık aracısı yüklü olduğundan ve çalıştığından, ancak hello çekirdek sürücüsü yüklenmeyen. 

Merhaba C:\Program Files\Microsoft bağımlılık Agent\logs\wrapper.log dosyası (Windows) veya /var/opt/microsoft/dependency-agent/log/service.log dosyası (Linux) denetleyin. Merhaba son satırları hello dosyasının hello çekirdek neden yüklenmeyen belirtmeniz gerekir. Örneğin, çekirdek güncelleştirdiyseniz hello çekirdek Linux'ta desteklenmeyebilir.

## <a name="data-collection"></a>Veri toplama
Her aracı tootransmit kabaca bekleyebilirsiniz 25 MB günde nasıl sistemi bağımlılıkları karmaşıktır bağlı olarak. Her bir aracının 15 dakikada hizmet Haritası bağımlılık verileri gönderir.  

Merhaba bağımlılık Aracısı genellikle sistem belleğinin yüzde 0,1 ve sistem CPU yüzdesi 0,1 tüketir.

## <a name="supported-azure-regions"></a>Desteklenen Azure bölgeleri
Hizmet eşlemesi Azure bölgeleri aşağıdaki hello şu anda kullanılabilir değil:
- Doğu ABD
- Batı Avrupa
- Batı Orta ABD


## <a name="supported-operating-systems"></a>Desteklenen işletim sistemleri
Merhaba aşağıdaki bölümlerde hello bağımlılık aracısı için hello desteklenen işletim sistemleri listelenmektedir. Hizmet eşlemesi 32-bit mimariler için herhangi bir işletim sistemini desteklemiyor.

### <a name="windows-server"></a>Windows Server
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1

### <a name="windows-desktop"></a>Windows masaüstü
- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux, CentOS Linux ve Oracle Linux (ile RHEL çekirdek)
- Yalnızca varsayılan ve SMP Linux çekirdek sürümleri desteklenir.
- PAE ve Xen, desteklenmez için tüm Linux dağıtım gibi standart olmayan çekirdek serbest bırakır. Örneğin, "2.6.16.21-0.8-xen" Merhaba sürüm dizesi sistemiyle desteklenmiyor.
- Standart çekirdekleri yeniden derlemelerinin dahil olmak üzere özel çekirdekleri desteklenmez.
- CentOSPlus çekirdek desteklenmiyor.
- Oracle kesilemeyen kurumsal çekirdek (UEK), bu makalenin sonraki bölümlerde ele alınmıştır.


#### <a name="red-hat-linux-7"></a>Red Hat Linux 7
| İşletim sistemi sürümü | Çekirdek sürümü |
|:--|:--|
| 7.0 | 3.10.0-123 |
| 7.1 | 3.10.0-229 |
| 7.2 | 3.10.0-327 |
| 7.3 | 3.10.0-514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6
| İşletim sistemi sürümü | Çekirdek sürümü |
|:--|:--|
| 6.0 | 2.6.32-71 |
| 6.1 | 2.6.32-131 |
| 6.2 | 2.6.32-220 |
| 6.3 | 2.6.32-279 |
| 6.4 | 2.6.32-358 |
| 6.5 | 2.6.32-431 |
| 6.6 | 2.6.32-504 |
| 6.7 | 2.6.32-573 |
| 6.8 | 2.6.32-642 |

#### <a name="red-hat-linux-5"></a>Red Hat Linux 5
| İşletim sistemi sürümü | Çekirdek sürümü |
|:--|:--|
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398<br>2.6.18-400<br>2.6.18-402<br>2.6.18-404<br>2.6.18-406<br>2.6.18-407<br>2.6.18-408<br>2.6.18-409<br>2.6.18-410<br>2.6.18-411<br>2.6.18-412<br>2.6.18-416<br>2.6.18-417<br>2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Oracle Enterprise Linux kesilemeyen kurumsal çekirdek ile

#### <a name="oracle-linux-6"></a>Oracle Linux 6
| İşletim sistemi sürümü | Çekirdek sürümü
|:--|:--|
| 6.2 | Oracle 2.6.32-300 (UEK R1) |
| 6.3 | Oracle 2.6.39-200 (UEK R2) |
| 6.4 | Oracle 2.6.39-400 (UEK R2) |
| 6.5 | Oracle 2.6.39-400 (UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400 (UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| İşletim sistemi sürümü | Çekirdek sürümü
|:--|:--|
| 5.8 | Oracle 2.6.32-300 (UEK R1) |
| 5.9 | Oracle 2.6.39-300 (UEK R2) |
| 5.10 | Oracle 2.6.39-400 (UEK R2) |
| 5.11 | Oracle 2.6.39-400 (UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11
| İşletim sistemi sürümü | Çekirdek sürümü
|:--|:--|
| 11 | 2.6.27 |
| 11 SP1 | 2.6.32 |
| 11 SP2 | 3.0.13 |
| 11 SP3 | 3.0.76 |
| 11 SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10
| İşletim sistemi sürümü | Çekirdek sürümü
|:--|:--|
| 10 SP4 | 2.6.16.60 |

## <a name="diagnostic-and-usage-data"></a>Tanılama ve kullanım verileri
Microsoft otomatik olarak hello hizmet Haritası hizmet kullanımınız vasıtasıyla kullanım ve performans verilerini toplar. Microsoft hello kalite, güvenlik ve hello hizmet Haritası hizmet bütünlüğünü geliştirmek ve bu verileri tooprovide kullanır. Veriler, işletim sistemi ve sürümü gibi yazılımınızın hello yapılandırma hakkında bilgi içerir. Ayrıca IP adresi, DNS adı ve iş istasyonu adı sipariş tooprovide doğru ve etkili sorun giderme özellikleri içerir. Ad, adres veya diğer kişi bilgilerini toplamaz.

Veri toplama ve kullanım hakkında daha fazla bilgi için bkz: Merhaba [Microsoft Online Services gizlilik bildirimi](https://go.microsoft.com/fwlink/?LinkId=512132).



## <a name="next-steps"></a>Sonraki adımlar
- Nasıl çok öğrenin[hizmet eşlemesi kullanmak](operations-management-suite-service-map.md) sonra dağıtılan ve yapılandırılmış.
