---
title: "Günlük analizi veri çözümde aaaWire | Microsoft Docs"
description: "Kablo verileri birleştirilmiş ağ ve performans OMS aracısının, Operations Manager ve Windows bağlı aracılar dahil olmak üzere bilgisayar verilerdir. Ağ verileri birlikte, günlük veri toohelp ile verilerin bağıntısını."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: fc3d7127-0baa-4772-858a-5ba995d1519b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: banders
ms.openlocfilehash: adafdf98dfbda9d87759643a1a606a84eafd1348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a>Kablo verileri 2.0 (Önizleme) çözümüne günlük analizi

![Kablo verileri simgesi](./media/log-analytics-wire-data/wire-data2-symbol.png)

Kablo verileri Operations Manager, Windows bağlı dahil olmak üzere, OMS aracılarla ve Linux aracılarını bilgisayarlardan birleştirilmiş ağ ve performans verilerini ' dir. Ağ verileri birlikte, diğer günlük veri toohelp ile verilerin bağıntısını.

Ayrıca tooOMS aracıları hello kablo verileri çözüm BT altyapınızın bilgisayarlara yüklemek Microsoft Dependency aracıları kullanır. Bağımlılık aracıları İzleyici ağ gönderilen veriler tooand ağ için bilgisayarlardan düzeyleri 2-3 içinde hello [OSI modeli](https://en.wikipedia.org/wiki/OSI_model), da dahil olmak üzere hello çeşitli protokoller ve bağlantı noktaları kullanılır. Veri tooLog Analytics sonra gönderilen aracıları kullanma.

> [!NOTE]
> Merhaba kablo verileri çözüm toonew çalışma alanları önceki sürümü hello ekleyemezsiniz. Etkin hello özgün kablo verileri çözüm varsa, toouse devam edebilirsiniz. Ancak, toouse kablo verileri 2.0, önce kaldırmalısınız hello özgün sürümü.

Varsayılan olarak, günlük analizi günlüğe kaydedilen veri CPU, bellek, disk ve ağ performans verileri için yerleşik sayaçları toplar. Ağ ve diğer veri toplama gerçekleştirilir gerçek zamanlı alt ağları ve hello bilgisayar tarafından kullanılan uygulama düzeyi protokolleri de dahil olmak üzere her bir aracının için. Merhaba günlükleri sekmesinde hello Ayarları sayfasında diğer performans sayaçları ekleyin.

Kullandıysanız [sFlow](http://www.sflow.org/) veya diğer yazılımlarla [Cisco'nın NetFlow Protokolü](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html)istatistikleri hello ve kablo verileri gördüğünüz veri tanıdık tooyou olacaktır.

Yerleşik günlük arama sorguları hello türlerini bazıları şunlardır:

- Kablo verileri sağlayan aracılar
- Kablo verileri sağlayan aracıların IP adresi
- IP adresleriyle giden iletişimler
- Uygulama protokolleri tarafından gönderilen bayt sayısı
- Bir uygulama hizmeti tarafından gönderilen bayt sayısı
- Farklı protokoller tarafından alınan bayt
- Gönderilen ve IP sürümü tarafından alınan toplam bayt sayısı
- Güvenilir bir şekilde ölçülen bağlantıları için ortalama gecikme süresi
- Bilgisayar başlatan veya alan ağ trafiğinin işler
- Bir işlem için ağ trafiği miktarı

Kablo verileri kullanarak aradığınızda, filtre uygulayabilirsiniz ve Grup veri tooview bilgilerini hello üst aracıları ve üst protokoller. Veya ne zaman görüntüleyebilirsiniz birbirleri ile nasıl için uzun iletilen belirli bilgisayarlara (IP adresleri/MAC adresleri) ve ne kadar veri gönderildiği — temel olarak, arama tabanlı ağ trafiğiyle ilgili meta verileri görüntüleyin.

Meta verileri görüntülediğiniz olduğundan, ancak bunu ayrıntılı sorun giderme için mutlaka kullanışlı değildir. Günlük analizi kablo verileri ağ verilerin tam bir yakalama değil. Bu nedenle, paket düzeyinde ayrıntılı sorun giderme için tasarlanmamıştır. Merhaba Aracısı kullanmanın avantajı Merhaba, tooother koleksiyon yöntemleri karşılaştırıldığında, yok tooinstall gereçlerine sahip, ağ anahtarlarını yeniden yapılandırma ya da karmaşık yapılandırmalar yeniden olduğunu. Kablo verileri yalnızca Aracısı tabanlı — hello Aracısı bir bilgisayara yükleyin ve kendi ağ trafiğini izlemek. Başka bir avantajı, bulut sağlayıcılarının veya barındırma hizmeti sağlayıcısı veya hello kullanıcı hello doku katman burada sahip değil, Microsoft Azure çalışan toomonitor iş yükleri istediğiniz durumdur.

## <a name="connected-sources"></a>Bağlı kaynaklar

Kablo verileri hello Microsoft bağımlılık Aracısı ' verileri alır. Merhaba bağımlılık Aracısı hello OMS aracısı için kendi bağlantıları tooLog Analytics bağlıdır. Bu, bir sunucu OMS Aracısı yüklenir ve ilk yapılandırılmış hello olması gerekir ve ardından hello bağımlılık aracısı yükleyin anlamına gelir. Merhaba aşağıdaki tabloda hello kablo verileri çözümünü destekler hello bağlı kaynakları açıklanmaktadır.

| **Bağlı kaynak** | **Destekleniyor** | **Açıklama** |
| --- | --- | --- |
| Windows aracıları | Evet | Kablo verileri analiz eder ve Windows Aracısı bilgisayarlardan verileri toplar. <br><br> Toplama toohello içinde [OMS Aracısı](log-analytics-windows-agents.md), Windows aracıları hello Microsoft bağımlılık Aracısı gerektirir. Merhaba bkz [desteklenen işletim sistemleri](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) işletim sistemi sürümleri tam bir listesi. |
| Linux aracıları | Evet | Kablo verileri analiz eder ve Linux Aracısı bilgisayarlardan verileri toplar.<br><br> Toplama toohello içinde [OMS Aracısı](log-analytics-linux-agents.md), Linux aracılarını hello Microsoft bağımlılık Aracısı gerektirir. Merhaba bkz [desteklenen işletim sistemleri](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) işletim sistemi sürümleri tam bir listesi. |
| System Center Operations Manager yönetim grubu | Evet | Kablo verileri analiz eder ve Windows ve Linux aracıları bağlı bir veri toplar [System Center Operations Manager yönetim grubu](log-analytics-om-agents.md). <br><br> Merhaba System Center Operations Manager Aracısı bilgisayar tooLog arasında doğrudan bağlantı Analytics gereklidir. Veri hello yönetim grubu tooLog Analytics iletilir. |
| Azure depolama hesabı | Hayır | Hiçbir verilerden gelir kablo verileri Azure depolama biriminden toocollect Aracısı bilgisayarlardan verileri toplar. |

Windows hello Microsoft İzleme Aracısı'nı (MMA) hem System Center Operations Manager hem de günlük analizi toogather tarafından kullanılır ve verileri gönder. Merhaba bağlamı bağlı olarak, hello Aracısı hello System Center Operations Manager Aracısı, OMS Aracısı, günlük analizi Aracısı, MMA veya doğrudan aracı adı verilir. System Center Operations Manager ve günlük analizi hello MMA biraz farklı sürümleri sağlar. Bu sürümleri her tooSystem Center Operations Manager, tooLog Analytics veya tooboth bildirebilirsiniz.

Linux üzerinde hello Linux için OMS aracısının toplar ve veri tooLog Analytics gönderir. Kablo verileri OMS doğrudan aracılarıyla sunucularda veya System Center Operations Manager Yönetim grupları aracılığıyla ekli tooLog Analytics olan sunucular kullanabilirsiniz.

Bu makalede, tooall aracıları olup başvuran Linux veya Windows, bağlı tooa System Center Operations Manager yönetim grubu veya doğrudan tooLog Analytics ifade olup olmadığını hello _OMS Aracısı_. Bağlam için yalnızca gerekli ise hello belirli dağıtım adı hello Aracısı'nın kullanacağız.

Merhaba bağımlılık Aracısı tüm verileri aktarmaz ve herhangi bir değişiklik toofirewalls veya bağlantı noktalarını gerektirmez. Kablo verileri Hello verileri her zaman hello OMS Aracısı tooLog Analytics, ya da doğrudan aktarılan veya hello OMS ağ geçidi kullanarak.

![Aracı diyagramı](./media/log-analytics-wire-data/agents.png)

Bir yönetim grubu bağlı tooLog Analytics System Center Operations Manager kullanıcıyla varsa:

- System Center Operations Manager aracıları hello Internet tooconnect tooLog Analytics erişebiliyorsa ek yapılandırma gerekli değildir.
- System Center Operations Manager aracıları hello Internet günlük analizi erişemediğinde tooconfigure hello OMS ağ geçidi toowork System Center Operations Manager ile gerekir.

Merhaba doğrudan aracı kullanıyorsanız, tooconnect tooLog Analytics veya tooyour OMS ağ geçidi tooconfigure hello OMS Aracısı kendisini gerekir. Merhaba OMS ağ geçidi hello indirebilirsiniz [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).

## <a name="prerequisites"></a>Ön koşullar

- Merhaba gerektirir [Insight and Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) çözümü sunar.
- Hello hello kablo verileri çözüm önceki sürümünü kullanıyorsanız, önce onu kaldırmanız gerekir. Ancak, hello özgün kablo verileri çözüm yakalanan tüm veriler kablo verileri 2.0 ve günlük arama hala mevcut değil.
- Yönetici ayrıcalıkları gerekli tooinstall ya da hello bağımlılık Aracısı kaldırın.
- Merhaba bağımlılık Aracısı, bir 64-bit işletim sistemine sahip bir bilgisayara yüklenmelidir.

### <a name="operating-systems"></a>İşletim sistemleri

Merhaba aşağıdaki bölümlerde hello bağımlılık aracısı için hello desteklenen işletim sistemleri listelenmektedir. Kablo verileri 32-bit mimariler için herhangi bir işletim sistemini desteklemiyor.

#### <a name="windows-server"></a>Windows Server

- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1

#### <a name="windows-desktop"></a>Windows masaüstü

- Windows 10
- Windows 8.1
- Windows 8
- Windows 7

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a>Red Hat Enterprise Linux, CentOS Linux ve Oracle Linux (ile RHEL çekirdek)

- Yalnızca varsayılan ve SMP Linux çekirdek sürümleri desteklenir.
- PAE ve Xen, desteklenmez için tüm Linux dağıtım gibi standart olmayan çekirdek serbest bırakır. Örneğin, bir sistem hello sürüm dizesi ile _2.6.16.21-0.8-xen_ desteklenmiyor.
- Standart çekirdekleri yeniden derlemelerinin dahil olmak üzere özel çekirdekleri desteklenmez.
- CentOSPlus çekirdek desteklenmiyor.
- Oracle kesilemeyen kurumsal çekirdek (UEK), bu makalenin sonraki bölümlerde ele alınmıştır.

#### <a name="red-hat-linux-7"></a>Red Hat Linux 7

| **İşletim sistemi sürümü** | **Çekirdek sürümü** |
| --- | --- |
| 7.0 | 3.10.0-123 |
| 7.1 | 3.10.0-229 |
| 7.2 | 3.10.0-327 |
| 7.3 | 3.10.0-514 |

#### <a name="red-hat-linux-6"></a>Red Hat Linux 6

| **İşletim sistemi sürümü** | **Çekirdek sürümü** |
| --- | --- |
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

| **İşletim sistemi sürümü** | **Çekirdek sürümü** |
| --- | --- |
| 5.8 | 2.6.18-308 |
| 5.9 | 2.6.18-348 |
| 5.10 | 2.6.18-371 |
| 5.11 | 2.6.18-398 <br> 2.6.18-400 <br>2.6.18-402 <br>2.6.18-404 <br>2.6.18-406 <br> 2.6.18-407 <br> 2.6.18-408 <br> 2.6.18-409 <br> 2.6.18-410 <br> 2.6.18-411 <br> 2.6.18-412 <br> 2.6.18-416 <br> 2.6.18-417 <br> 2.6.18-419 |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a>Oracle Enterprise Linux kesilemeyen kurumsal çekirdek ile

#### <a name="oracle-linux-6"></a>Oracle Linux 6

| **İşletim sistemi sürümü** | **Çekirdek sürümü** |
| --- | --- |
| 6.2 | Oracle 2.6.32-300 (UEK R1) |
| 6.3 | Oracle 2.6.39-200 (UEK R2) |
| 6.4 | Oracle 2.6.39-400 (UEK R2) |
| 6.5 | Oracle 2.6.39-400 (UEK R2 i386) |
| 6.6 | Oracle 2.6.39-400 (UEK R2 i386) |

#### <a name="oracle-linux-5"></a>Oracle Linux 5

| **İşletim sistemi sürümü** | **Çekirdek sürümü** |
| --- | --- |
| 5.8 | Oracle 2.6.32-300 (UEK R1) |
| 5.9 | Oracle 2.6.39-300 (UEK R2) |
| 5.10 | Oracle 2.6.39-400 (UEK R2) |
| 5.11 | Oracle 2.6.39-400 (UEK R2) |

#### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

#### <a name="suse-linux-11"></a>SUSE Linux 11

| **İşletim sistemi sürümü** | **Çekirdek sürümü** |
| --- | --- |
| 11 | 2.6.27 |
| 11 SP1 | 2.6.32 |
| 11 SP2 | 3.0.13 |
| 11 SP3 | 3.0.76 |
| 11 SP4 | 3.0.101 |

#### <a name="suse-linux-10"></a>SUSE Linux 10

| **İşletim sistemi sürümü** | **Çekirdek sürümü** |
| --- | --- |
| 10 SP4 | 2.6.16.60 |

#### <a name="dependency-agent-downloads"></a>Bağımlılık Aracısı indirir

| **Dosya** | **İŞLETİM SİSTEMİ** | **Sürüm** | **SHA-256** |
| --- | --- | --- | --- |
| [InstallDependencyAgent Windows.exe](https://aka.ms/dependencyagentwindows) | Windows | 9.0.5 | 73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43 |
| [InstallDependencyAgent Linux64.bin](https://aka.ms/dependencyagentlinux) | Linux | 9.0.5 | A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371 |



## <a name="configuration"></a>Yapılandırma

Aşağıdaki adımları tooconfigure hello kablo verileri çözümü alanlarınızı hello gerçekleştirin.

1. Merhaba etkinlik günlük analizi hello çözümden etkinleştirmek [Azure Market](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) veya açıklanan hello işlemi kullanarak [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).
2. Merhaba bağımlılık Aracısı tooget verilerin istediğiniz her bilgisayara yükleyin. her bilgisayarda bir aracı gerekmeyebilir şekilde hello bağımlılık Aracısı bağlantıları tooimmediate Komşuları olarak izleyebilirsiniz.

### <a name="install-hello-dependency-agent-on-windows"></a>Windows Hello bağımlılık Aracısı yükleme

Yönetici ayrıcalıkları gerekli tooinstall ya da hello aracısını kaldırın.

Merhaba bağımlılık Aracısı InstallDependencyAgent Windows.exe Windows çalıştıran bilgisayarlara yüklenir. Bu yürütülebilir dosya seçenekleri olmadan çalıştırırsanız, tooinstall etkileşimli olarak izleyebileceğiniz bir sihirbazı başlatır.

Windows çalıştıran her bilgisayarda adımları tooinstall hello bağımlılık aracısı aşağıdaki hello kullan:

1. Yükleme hello yönergeleri kullanarak OMS Aracısı hello [bağlanmak Windows bilgisayarları toohello Azure günlük analizi hizmeti](log-analytics-windows-agents.md).
2. Merhaba önceki bölümde Hello bağlantıyı kullanarak hello Windows aracıyı indirin ve çalıştırın komutu aşağıdaki hello kullanarak: InstallDependencyAgent Windows.exe
3. Merhaba Sihirbazı tooinstall hello Aracısı izleyin.
4. Merhaba bağımlılık Aracısı toostart başarısız olursa, ayrıntılı hata bilgileri için hello günlüklerini denetleyin. Windows aracısında %Programfiles%\Microsoft bağımlılık Agent\logs hello günlük dizindir.

#### <a name="windows-command-line"></a>Windows komut satırı

Merhaba tablo tooinstall komut satırından aşağıdaki seçenekleri kullanın. toosee hello kullanarak hello yükleyiciyi çalıştırmak, hello yükleme bayrakları listesini /? aşağıdaki gibi bayrak.

InstallDependencyAgent Windows.exe /?

| **Bayrağı** | **Açıklama** |
| --- | --- |
| <code>/?</code> | Merhaba komut satırı seçeneklerinin listesini alın. |
| <code>/S</code> | Kullanıcı etkileşimi ile sessiz bir yükleme gerçekleştirin. |

Merhaba Windows bağımlılık aracısı için dosyalar varsayılan olarak C:\Program Files\Microsoft bağımlılık Aracısı yerleştirilir.

### <a name="install-hello-dependency-agent-on-linux"></a>Linux'ta Hello bağımlılık Aracısı yükleme

Kök erişimi gerekli tooinstall ya da hello Aracısı yapılandırın.

Merhaba bağımlılık Aracısı InstallDependencyAgent Linux64.bin, kendiliğinden açılan bir ikili içeren bir kabuk betiği aracılığıyla Linux bilgisayarlara yüklenir. Merhaba dosyasını kullanarak çalıştırabilirsiniz _paylaş_ veya ekleme izinleri toohello dosyasının kendisini yürütün.

Adımları tooinstall hello bağımlılık Aracısı her bir Linux bilgisayarda aşağıdaki hello kullan:

1. Yükleme hello yönergeleri kullanarak OMS Aracısı hello [toplamak ve Linux bilgisayarları veri yönetmek](log-analytics-agent-linux.md).
2. Merhaba önceki bölümde Hello bağlantıyı kullanarak hello Linux bağımlılık aracıyı indirin ve ardından komut aşağıdaki hello kullanarak kök olarak yükleyin: Paylaş InstallDependencyAgent Linux64.bin
3. Merhaba bağımlılık Aracısı toostart başarısız olursa, ayrıntılı hata bilgileri için hello günlüklerini denetleyin. Linux aracısında hello günlük dizini:: /var/opt/microsoft/dependency-agent/log.

toosee ile Merhaba hello yükleme programını çalıştırmak, hello yükleme bayrakları listesini `-help` gibi bayrak.

```
InstallDependencyAgent-Linux64.bin -help
```

| **Bayrağı** | **Açıklama** |
| --- | --- |
| <code>-help</code> | Merhaba komut satırı seçeneklerinin listesini alın. |
| <code>-s</code> | Kullanıcı etkileşimi ile sessiz bir yükleme gerçekleştirin. |
| <code>--check</code> | İzinler ve hello işletim sistemi denetle, ancak hello Aracısı yüklemeyin. |

Merhaba bağımlılık aracısı için dosyalar dizinleri izleyen hello yerleştirilir:

| **Dosyaları** | **Konum** |
| --- | --- |
| Çekirdek dosyaları | /OPT/Microsoft/Dependency-Agent |
| Günlük dosyaları | /var/OPT/Microsoft/Dependency-Agent/log |
| Yapılandırma dosyaları | /etc/OPT/Microsoft/Dependency-Agent/config |
| Hizmet yürütülebilir dosyalar | /OPT/Microsoft/Dependency-Agent/bin/Microsoft-Dependency-Agent<br><br>/OPT/Microsoft/Dependency-Agent/bin/Microsoft-Dependency-Agent-Manager |
| İkili depolama dosyaları | /var/OPT/Microsoft/Dependency-Agent/Storage |

### <a name="installation-script-examples"></a>Yükleme komut dosyası örnekleri

tooeasily hello bağımlılık Aracısı pek çok sunucu üzerinde aynı anda dağıtabilir, bir komut dosyası toouse yardımcı olur. Aşağıdaki komut örnekleri toodownload hello kullanın ve Windows ya da Linux hello bağımlılık aracısı yükleyin.

#### <a name="powershell-script-for-windows"></a>Windows PowerShell Betiği

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a>Linux için kabuk komut dosyası

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a>İstenen Durum Yapılandırması

toodeploy hello bağımlılık Aracısı istenen durum yapılandırması hello xPSDesiredStateConfiguration modülü ve biraz kod hello aşağıdaki gibi kullanabilirsiniz:

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install hello Dependency Agent

    xRemoteFile DAPackage

    {

        Uri = &quot;https://aka.ms/dependencyagentwindows&quot;

        DestinationPath = $DAPackageLocalPath

        DependsOn = &quot;[Package]OI&quot;

    }

    xPackage DA

    {

        Ensure=&quot;Present&quot;

        Name = &quot;Dependency Agent&quot;

        Path = $DAPackageLocalPath

        Arguments = '/S'

        ProductId = &quot;&quot;

        InstalledCheckRegKey = &quot;HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent&quot;

        InstalledCheckRegValueName = &quot;DisplayName&quot;

        InstalledCheckRegValueData = &quot;Dependency Agent&quot;

    }

}

```
### <a name="uninstall-hello-dependency-agent"></a>Merhaba bağımlılık aracısı kaldırma

Aşağıdaki bölümlerde toohelp hello bağımlılık aracısı kaldırma hello kullanın.

#### <a name="uninstall-hello-dependency-agent-on-windows"></a>Bağımlılık Aracısı'nı Windows Hello kaldırma

Bir yönetici için hello bağımlılık Aracısı Windows Denetim Masası'ndan kaldırabilirsiniz.

Bir yönetici, %Programfiles%\Microsoft bağımlılık Agent\Uninstall.exe toouninstall hello bağımlılık aracısı olarak da çalıştırabilirsiniz.

#### <a name="uninstall-hello-dependency-agent-on-linux"></a>Merhaba bağımlılık Aracısı'nı Linux kaldırma

Bağımlılık Aracısı'ndan Linux toocompletely kaldırma Merhaba, hello aracı ile otomatik olarak yüklenen bağlayıcı hello ve hello aracının kendisi kaldırmanız gerekir. Hem tek bir komut aşağıdaki hello kullanarak kaldırabilirsiniz:

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a>Yönetim paketleri

Kablo verileri bir günlük analizi çalışma alanındaki etkinleştirildiğinde, 300-KB Yönetim Paketi bu çalışma alanında tooall hello Windows sunucularına gönderilir. System Center Operations Manager aracıları kullanıyorsanız, bir [bağlı yönetim grubu](log-analytics-om-agents.md), hello bağımlılık İzleyicisi Yönetim Paketi System Center Operations Manager'dan dağıtılır. Merhaba aracıları doğrudan bağlıysanız, günlük analizi hello Yönetim Paketi sunar.

Merhaba Yönetim Paketi Microsoft.IntelligencePacks.ApplicationDependencyMonitor olarak adlandırılır. Öğesine yazılır: %Programfiles%\Microsoft izleme Agent\Agent\Health hizmet State\Management paketleri. Merhaba Yönetim Paketi kullanan hello veri kaynağı: % Program files%\Microsoft izleme Agent\Agent\Health hizmet State\Resources&lt;AutoGeneratedID&gt;\ Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.

## <a name="using-hello-solution"></a>Merhaba çözümünü kullanarak

**Yükleme ve yapılandırma hello çözümü**

Bilgi tooinstall aşağıdaki hello kullanın ve hello çözüm yapılandırın.

- Merhaba kablo verileri çözüm Windows Server 2012 R2, Windows 8.1 ve sonraki işletim sistemleri çalıştıran bilgisayarların verilerini alır.
- Tooacquire kablo verileri istediğiniz bilgisayarlarda Microsoft .NET Framework 4.0 veya sonraki sürümü gerekir.
- Açıklanan başlangıç işlemini kullanarak hello kablo verileri çözüm tooyour günlük analizi çalışma Ekle [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md). Başka bir yapılandırma işlemi gerekmez.
- Belirli bir çözüm için tooview kablo verileri istiyorsanız, zaten eklenmiş toohave hello çözüm gerekir tooyour çalışma.

Aracıları yüklü olan ve hello çözüm yükledikten sonra hello kablo verileri 2.0 döşeme çalışma alanında görüntülenir.

> [!NOTE]
> Şu anda hello OMS portalı tooview kablo verileri kullanmanız gerekir. Hello Azure portal tooview kablo verileri kullanamazsınız.

![Kablo verileri döşeme](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-hello-wire-data-20-solution"></a>Merhaba kablo verileri 2.0 çözümünü kullanarak

Merhaba OMS portalında hello tıklatın **kablo verileri 2.0** döşeme tooopen hello kablo verileri Pano. Merhaba Pano aşağıdaki tablonun hello hello Kanatlar içerir. Her dikey penceresinde hello dikey'nın ölçütlerine kapsam ve zaman aralığını belirtilen eşleşen too10 öğeleri listeler. Tıklayarak tüm kayıtları döndüren bir günlük arama çalıştırabilirsiniz **tümünü görmek** hello altındaki hello dikey veya hello dikey penceresi Başlığı tıklatarak.

| **Dikey penceresi** | **Açıklama** |
| --- | --- |
| Ağ trafiğini yakalayan aracılar | Ağ trafiğini yakalayan aracılar Hello sayısını gösterir ve trafiği yakalama hello üst 10 bilgisayarları listeler. Bir günlük Ara Hello numara toorun <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>. Hello listesi toorun bir bilgisayarda yakalanan baytların toplam sayısıdır hello döndüren bir günlük Ara'yı tıklatın. |
| Yerel alt ağları | Aracıları bulunmuş yerel alt ağları Hello sayısını gösterir.  Bir günlük Ara Hello numara toorun <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> , listeleri tüm alt ağlar ile Merhaba her biri gönderilen bayt sayısı. Bir alt ağda hello listesi toorun hello toplam hello alt ağ gönderilen bayt sayısı döndüren bir günlük Ara'yı tıklatın. |
| Uygulama düzeyi protokolleri | Uygulama düzeyi protokolleri Hello sayısını kullanımda, aracıları tarafından bulunan olarak gösterir. Bir günlük Ara Hello numara toorun <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>. Bir protokol toorun hello toplam hello protokolü kullanılarak gönderilen bayt sayısı döndüren bir günlük Ara'yı tıklatın. |

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Kablo verileri Panosu](./media/log-analytics-wire-data/wire-data-dash.png)

Merhaba kullanabilirsiniz **ağ trafiğini yakalayan aracılar** dikey toodetermine ne kadar ağ bant genişliği, bilgisayarlar tarafından tüketilen. Bu dikey kolayca Bul hello yardımcı olabilecek _chattiest_ bilgisayar ortamınızdaki. Bu bilgisayarlar, anormal olarak davranan veya normalden daha fazla ağ kaynaklarını kullanan aşırı yüklenmiş.

![Günlük arama örneği](./media/log-analytics-wire-data/log-search-example01.png)

Benzer şekilde, hello kullanabilirsiniz **yerel alt ağları** dikey toodetermine ne kadar ağ trafiğini, alt ağlar arasında taşıma. Kullanıcıların uygulamaları için kritik alanları geçici alt ağlar genellikle tanımlayın. Bu dikey bu alanlara görünüme sunar.

![Günlük arama örneği](./media/log-analytics-wire-data/log-search-example02.png)

Merhaba **uygulama düzeyi protokolleri** dikey yararlıdır yardımcı olduğundan ne protokolleri kullanımda olduğunu biliyor. Örneğin, SSH toonot, ağ ortamınızda kullanılacak bekleyebilirsiniz. Merhaba dikey penceresinde kullanılabilir bilgilerini görüntüleme hızlı bir şekilde Onayla veya, Beklenti disprove.

![Günlük arama örneği](./media/log-analytics-wire-data/log-search-example03.png)

Bu örnekte, SSH ayrıntıları toosee ayrıntıya hangi bilgisayarların SSH ve diğer birçok iletişim ayrıntılarını kullanıyor olabilir.

![Paylaş arama sonuçları](./media/log-analytics-wire-data/ssh-details.png)

Protokol trafiğini artan veya azalan zamanla varsa yararlı tooknow de olabilir. Bir uygulama tarafından aktarılan veri miktarını Hello artırılması, örneğin, bilincinde olmanız gereken bir şey olması veya dikkate değer bulabileceğiniz emin olabilir.

## <a name="input-data"></a>Giriş verisi

Kablo verileri etkinleştirdiğiniz hello aracıları kullanarak ağ trafiğini hakkındaki meta verileri toplar. Her bir aracının 15 dakikada hakkındaki verileri gönderir.

## <a name="output-data"></a>Çıktı verileri

Türüne sahip bir kayıt _WireData_ her giriş veri türü için oluşturulur. WireData kayıtları, aşağıdaki tablonun hello gösterilen özelliklere sahiptir:

| Özellik | Açıklama |
|---|---|
| Bilgisayar | Burada veri toplanan bilgisayar adı |
| TimeGenerated | Merhaba kayıt zamanı |
| Yerel IP | Merhaba yerel bilgisayarın IP adresi |
| SessionState | Bağlantısı kesilmiş veya bağlı |
| ReceivedBytes | Alınan bayt miktarı |
| ProtocolName | Kullanılan hello ağ protokolü adı |
| İpversion değeri | IP sürümü |
| Yön | Gelen veya giden |
| MaliciousIP | Bilinen kötü amaçlı bir kaynak IP adresi |
| Önem Derecesi | Amaçlı olduğundan kuşkulanılan yazılımın önem derecesi |
| RemoteIPCountry | Ülke / bölge hello uzak IP adresi |
| ManagementGroupName | Merhaba Operations Manager yönetim grubunun adı |
| SourceSystem | Burada veri toplanan kaynak |
| SessionStartTime | Oturum başlangıç saati |
| SessionEndTime | Oturumun bitiş saati |
| LocalSubnet | Burada veri toplanan alt ağ |
| LocalPortNumber | Yerel bağlantı noktası numarası |
| Uzak IP | Merhaba uzak bilgisayar tarafından kullanılan uzak IP adresi |
| RemotePortNumber | Merhaba uzak IP adresi tarafından kullanılan bağlantı noktası numarası |
| SessionID | İki IP adresi arasındaki iletişimi oturumunu tanımlayan benzersiz bir değer |
| SentBytes | Gönderilen bayt sayısı |
| TotalBytes | Toplam oturum sırasında gönderilen bayt sayısı |
| ApplicationProtocol | Kullanılan ağ protokol türü   |
| İşlem kimliği | Windows işlem kimliği |
| İşlem adı | Merhaba işlemin yolu ve dosya adı |
| RemoteIPLongitude | IP boylam değeri |
| RemoteIPLatitude | IP enlem değeri |


## <a name="next-steps"></a>Sonraki adımlar

- [Arama günlüklerini](log-analytics-log-searches.md) tooview ayrıntılı kablo veri arama kaydeder.
