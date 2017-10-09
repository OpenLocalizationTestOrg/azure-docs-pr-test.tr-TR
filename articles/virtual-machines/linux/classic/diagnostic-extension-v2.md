---
title: "bir Linux VM VM uzantısı ile aaaMonitoring | Microsoft Docs"
description: "Toouse nasıl hello Linux tanılama uzantısını toomonitor hello performans ve Tanılama verileri azure'da bir Linux VM öğrenin."
services: virtual-machines-linux
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f54a11c5-5a0e-40ff-af6c-e60bd464058b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: Ning
ms.openlocfilehash: cf7bfebca8c0367941f7a975417f60fe2e2dab25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-linux-diagnostic-extension-toomonitor-hello-performance-and-diagnostic-data-of-a-linux-vm"></a>Merhaba Linux tanılama uzantısını toomonitor hello performans ve bir Linux VM tanılama verilerini kullanın

Bu belgede hello Linux tanılama uzantısını 2.3 sürümü açıklanmaktadır.

> [!IMPORTANT]
> Bu sürüm kullanım dışıdır ve 30 Haziran 2018 sonra her zaman yayımdan olabilir. 3.0 sürümünde değiştirilmiştir. Daha fazla bilgi için bkz: Merhaba [hello Linux tanılama uzantısı sürüm 3.0 belgelerine](../diagnostic-extension.md).

## <a name="introduction"></a>Giriş

(**Not**: Linux tanılama uzantısını açık kaynaklıdır hello [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) burada hello en güncel bilgiler hello uzantısındaki ilk yayımlanır. Toocheck hello isteyebilirsiniz [GitHub sayfası](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) ilk.)

Merhaba Linux tanılama uzantısını kullanıcı İzleyicisi Merhaba Microsoft Azure üzerinde çalışan Linux VM'ler yardımcı olur. Hello aşağıdaki özellikleri içerir:

* Toplar ve tanılama ve syslog bilgiler dahil olmak üzere hello Linux VM toohello kullanıcının depolama tablosundan hello sistem performans bilgileri yükler.
* Toplanan ve karşıya kullanıcılar toocustomize hello veri ölçümleri sağlar.
* Kullanıcıların tooupload belirtilen günlük dosyaları tooa atanan depolama tablosu sağlar.

Merhaba geçerli sürümde 2.3 hello verileri şunları içerir:

* Sistem, güvenlik ve uygulama günlükleri de dahil olmak üzere tüm Linux Rsyslog günlükleri.
* Belirtilen tüm sistem verileri [hello System Center Çapraz Platform çözümlerini site](https://scx.codeplex.com/wikipage?title=xplatproviders).
* Kullanıcı tarafından belirtilen günlük dosyaları.

Bu uzantı hello Klasik ve Resource Manager dağıtım modelleri ile çalışır.

### <a name="current-version-of-hello-extension-and-deprecation-of-old-versions"></a>Geçerli sürümünü hello uzantısı ve eski sürümleri kullanımdan kaldırma

Merhaba uzantısı'nın en son sürüm Hello **2.3**, ve **eski sürümlerini (2.0, 2.1 ve 2.2) kullanım dışı ve, bu yılın sonuna (2017) tarafından yayımlanmamış**. Merhaba Linux tanılama uzantısını devre dışı otomatik alt sürüm yükseltme işlemine yüklediyseniz, hello uzantısı kaldırıp etkin otomatik alt sürüm yükseltme işlemine yeniden yüklemeniz önerilir. Klasik (ASM) Vm'lerinde, bu hello uzantısı Azure XPLAT CLI veya Powershell aracılığıyla yüklüyorsanız '2.*' hello sürümü belirterek elde edebilirsiniz. ARM Vm'leri üzerinde bu dahil ederek elde edebilirsiniz ' "olan": true' hello VM Dağıtım şablonu olarak. Ayrıca, tüm yeni uzantısını yükleme işlemi hello hello otomatik alt sürüm yükseltme seçeneği açık olması gerekir.

## <a name="enable-hello-extension"></a>Merhaba uzantısını etkinleştirme

Bu uzantı hello kullanarak etkinleştirebilirsiniz [Azure portal](https://portal.azure.com/#), Azure PowerShell veya Azure CLI komut dosyaları.

tooview hello sistem yapılandırmanıza ve performans verileri doğrudan Azure portal hello izleyin [hello Azure blogu üzerinde aşağıdaki adımları](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).

Bu makalede odaklanılmaktadır tooenable ve Azure CLI komutları kullanarak hello uzantısı yapılandırın. Bu, tooread ve görünüm hello verileri doğrudan hello depolama tablosu sağlar.

Burada açıklanan hello yapılandırma yöntemleri hello Azure portal çalışmaz unutmayın. tooview ve hello sistem ve performans verileri doğrudan hello Azure portal yapılandırma, hello uzantısı hello Portalı aracılığıyla etkinleştirilmesi gerekir.

## <a name="prerequisites"></a>Ön koşullar

* **Azure Linux Aracısı sürüm 2.0.6 veya daha sonra**.

  Çoğu Azure VM Linux galeri görüntüleri sürümü 2.0.6 dahil Not veya sonraki bir sürümü. Çalıştırabilirsiniz **WAAgent-sürüm** tooconfirm hangi sürümünün hello VM üzerinde yüklü. Merhaba VM 2.0.6 önceki bir sürümünü çalıştırıyorsa, takip edebilirsiniz [github'daki bu yönergeleri](https://github.com/Azure/WALinuxAgent "yönergeleri") tooupdate onu.
* **Azure CLI**. İzleyin [CLI yüklemek için bu Kılavuzu](../../../cli-install-nodejs.md) hello Azure CLI çevresi makinenizde tooset. Azure CLI yüklendikten sonra hello kullanabilirsiniz **azure** , komut satırı arabirimi (Bash, Terminal veya komut istemi) tooaccess hello Azure CLI komutlarının komutu. Örneğin:

  * Çalıştırma **azure vm uzantısı kümesi--Yardım** ayrıntılı yardım bilgi.
  * Çalıştırma **azure oturum açma** tooAzure toosign.
  * Çalıştırma **azure vm listesi** toolist tüm hello Azure üzerinde sahip sanal makineler.
* Depolama hesabı toostore hello verileri. Daha önce oluşturulmuş bir depolama hesabı adı ve bir erişim anahtarı tooupload hello veri tooyour depolama gerekir.

## <a name="use-hello-azure-cli-command-tooenable-hello-linux-diagnostic-extension"></a>Hello Azure CLI komutu tooenable hello Linux tanılama uzantısını kullanın

### <a name="scenario-1-enable-hello-extension-with-hello-default-data-set"></a>Senaryo 1. Merhaba varsayılan veri kümesi Hello uzantısını etkinleştirme

2.3 veya sonraki sürümü içinde toplanacağını hello varsayılan veri içerir:

* Tüm Rsyslog bilgileri (Sistem, güvenlik ve uygulama günlükleri dahil).  
* Temel sistem verileri çekirdek kümesi. Tam veri kümesi hello Not üzerinde hello açıklanan [System Center Çapraz Platform çözümlerini site](https://scx.codeplex.com/wikipage?title=xplatproviders).
  Tooenable isterseniz ek veriler devam senaryoları 2 ve 3'te hello adımlara.

1. Adım Aşağıdaki hello ile PrivateConfig.json adlı bir dosya içerik oluşturun:

    {
        "storageAccountName" : "hello storage account tooreceive data",
        "storageAccountKey" : "hello key of hello account"
    }

2. Adım Çalıştırma  **azure vm uzantısı ayarlamak vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --özel yapılandırma yolu PrivateConfig.json**.

### <a name="scenario-2-customize-hello-performance-monitor-metrics"></a>Senaryo 2. Merhaba Performans İzleyicisi ölçümlerini özelleştirme

Bu bölümde toocustomize nasıl hello performans ve tanı veri tablosu açıklanmaktadır.

1. Adım Senaryo 1'de açıklanan hello içerikle PrivateConfig.json adlı bir dosya oluşturun. Ayrıca PublicConfig.json adlı bir dosya oluşturun. Hello belirli veri toocollect istediğinizi belirtin.

Desteklenen tüm sağlayıcıları ve değişkenleri için hello başvuru [System Center Çapraz Platform çözümlerini site](https://scx.codeplex.com/wikipage?title=xplatproviders). Birden çok sorgu sahip ve birden fazla tabloya daha fazla sorguları toohello komut dosyası eklenerek depolayabilirsiniz.

Varsayılan olarak, her zaman hello Rsyslog verileri toplanır.

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


2. Adım Çalıştırma  **azure vm uzantısı ayarlamak vm_name LinuxDiagnostic Microsoft.OSTCExtensions ' 2.*'--özel yapılandırma yolu PrivateConfig.json--ortak yapılandırma yolu PublicConfig.json**.

### <a name="scenario-3-upload-your-own-log-files"></a>Senaryo 3. Kendi günlük dosyalarını karşıya yükleme

Bu bölümde, nasıl tooyour depolama hesabı toocollect ve karşıya yükleme belirli günlük dosyalarını açıklar. Her iki hello yolu tooyour günlük dosya ve hello günlüğünüzün toostore istediğiniz yere Merhaba tablonun adını toospecify gerekir. Birden çok dosya/tablo girişleri toohello betik ekleyerek, birden çok günlük dosyası oluşturabilirsiniz.

1. Adım Senaryo 1'de açıklanan hello içerikle PrivateConfig.json adlı bir dosya oluşturun. Ardından aşağıdaki hello ile PublicConfig.json adlı başka bir dosya içerik oluşturun:

```json
{
    "fileCfg" :
    [
        {
            "file" : "/var/log/mysql.err",
            "table" : "mysqlerr"
            }
    ]
}
```

2. Adım `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json` öğesini çalıştırın.

Tüm günlükleri çok yazılmış hello uzantısı sürümleri önceki too2.3, bu ayarı ile unutmayın`/var/log/mysql.err` çok yinelenen`/var/log/syslog` (veya `/var/log/messages` hello Linux distro bağlı olarak) de. Günlüğü bu yinelenen tooavoid kullanmak isterseniz, günlüğe dışlayabilirsiniz `local6` tesis rsyslog yapılandırmanızda günlüğe kaydeder. Merhaba Linux distro üzerinde bağlıdır, ancak bir Ubuntu 14.04 sistemde hello dosya toomodify dir `/etc/rsyslog.d/50-default.conf` ve hello satır değiştirebilirsiniz `*.*;auth,authpriv.none -/var/log/syslog` çok`*.*;auth,authpriv,local6.none -/var/log/syslog`. Merhaba en son düzeltme sürümünde 2.3 (2.3.9007), bu sorun düzeltilene şekilde hello uzantısı sürüm 2.3 varsa, bu sorun değil gerçekleşmelidir. Hala bile VM'yi yeniden başlatıldıktan sonra varsa, lütfen bizimle iletişime geçin ve hello en son düzeltme sürümü otomatik olarak yüklenmez neden gidermenize yardımcı.

### <a name="scenario-4-stop-hello-extension-from-collecting-any-logs"></a>Senaryo 4. Herhangi bir günlük toplama gelen hello uzantısı Durdur

Bu bölümde, nasıl toplama gelen toostop hello uzantı günlükleri açıklanmaktadır. İzleme Aracısı işlemi hello Not hala hazır ve çalışır bile bu yeniden yapılandırmaya olacaktır. İzleme Aracısı işlemi tamamen toostop hello isterseniz hello uzantı devre dışı bırakarak bunu yapabilirsiniz. Merhaba komutu toodisable hello uzantısı `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.

1. Adım Senaryo 1'de açıklanan hello içerikle PrivateConfig.json adlı bir dosya oluşturun. Aşağıdaki hello ile PublicConfig.json adlı başka bir dosya içerik oluşturun:

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


2. Adım Çalıştırma  **azure vm uzantısı ayarlamak vm_name LinuxDiagnostic Microsoft.OSTCExtensions ' 2.*'--özel yapılandırma yolu PrivateConfig.json--ortak yapılandırma yolu PublicConfig.json**.

## <a name="review-your-data"></a>Verilerinizi gözden geçirin

Merhaba performans ve tanılama verilerini bir Azure Storage tablosunda depolanır. Gözden geçirme [nasıl toouse Ruby Azure tablo depolamasından](../../../cosmos-db/table-storage-how-to-use-ruby.md) hello depolama tooaccess hello verileri nasıl tablo Azure CLI komut dosyalarını kullanarak toolearn.

Ayrıca, kullanıcı Arabirimi araçlarını tooaccess hello verileri kullanabilirsiniz:

1. Visual Studio Sunucu Gezgini. Tooyour depolama hesabına gidin. Merhaba VM yaklaşık beş dakika boyunca çalıştıktan sonra hello dört varsayılan tabloları görürsünüz: "LinuxCpu", "LinuxDisk", "LinuxMemory" ve "Linuxsyslog". Merhaba tablo adları tooview hello verileri çift tıklayın.
1. [Azure Storage Gezgini](https://azurestorageexplorer.codeplex.com/ "Azure Storage Gezgini").

![Görüntü](./media/diagnostic-extension/no1.png)

FileCfg veya (senaryoları 2 ve 3'te açıklandığı gibi) perfCfg etkinleştirdiyseniz, Visual Studio Sunucu Gezgini ve Azure Storage Gezgini tooview varsayılan olmayan verileri kullanabilirsiniz.

## <a name="known-issues"></a>Bilinen sorunlar

* Rsyslog bilgi hello ve müşteri tarafından belirtilen günlük dosyası yalnızca komut dosyası aracılığıyla erişilebilir.
