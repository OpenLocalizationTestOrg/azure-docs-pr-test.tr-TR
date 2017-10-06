---
title: "Azure günlük analizi aaaTrack değişikliklerle | Microsoft Docs"
description: "Merhaba günlük analizi değişiklik izleme çözümünde yazılım ve ortamınızda ortaya Windows hizmet değişiklikleri belirlemenize yardımcı olur."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f8040d5d-3c89-4f0c-8520-751c00251cb7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2bb1938caad25101e167927200ac3ef495120fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="track-software-changes-in-your-environment-with-hello-change-tracking-solution"></a>Merhaba değişiklik izleme çözümü ile ortamınızdaki yazılım değişiklikleri izle

![Değişiklik izleme simgesi](./media/log-analytics-change-tracking/change-tracking-symbol.png)

Bu makale size yardımcı olur kullanım hello günlük analizi tooeasily değişiklik izleme çözümünde tanımlamak, ortamınızda değişiklikler. Merhaba çözüm değişiklikleri tooWindows ve Linux yazılım, Windows dosya ve kayıt defteri anahtarları, Windows Hizmetleri ve Linux Daemon izler. Yapılandırma değişiklikleri tanımlayan işletim sorunları belirlemenize yardımcı olabilir.

Merhaba çözüm tooupdate hello türü yüklediğiniz aracısı yükleyin. Değişiklikleri tooinstalled yazılım, Windows Hizmetleri ve Linux Daemon hello izlenen sunuculara salt okunurdur. Ardından, hello veri işleme hello bulutta toohello günlük analizi hizmeti gönderilir. Mantığı uygulanan toohello alınan veri ve hello bulut hizmeti hello verilerini kaydeder. Değişiklik izleme hello Panoda Hello bilgileri kullanarak, sunucu altyapınızda yapılan hello değişiklikler kolayca görebilirsiniz.

## <a name="installing-and-configuring-hello-solution"></a>Yükleme ve yapılandırma hello çözümü
Bilgi tooinstall aşağıdaki hello kullanın ve hello çözüm yapılandırın.

* Bilmeniz gereken bir [Windows](log-analytics-windows-agents.md), [Operations Manager](log-analytics-om-agents.md), veya [Linux](log-analytics-linux-agents.md) toomonitor değişiklikleri istediğiniz her bilgisayarda aracı.
* Merhaba değişiklik izleme çözümü tooyour OMS çalışma hello eklemek [Azure Market](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ChangeTrackingOMS?tab=Overview). Ya da hello bilgileri kullanarak hello çözüm ekleyebilirsiniz [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md). Ek yapılandırma gerekli değildir.

### <a name="configure-linux-files-tootrack"></a>Linux dosyaları tootrack yapılandırın
Adımları tooconfigure dosyaları tootrack Linux bilgisayarlarda aşağıdaki hello kullanın.

1. Merhaba OMS portalında tıklatın **ayarları** (Merhaba dişli symbol).
2. Merhaba üzerinde **ayarları** sayfasında, **veri**ve ardından **Linux dosya izleme**.
3. Linux dosya değişiklik izleme altında tootrack istediğiniz ve hello ardından hello dosyasının hello dosya adı dahil olmak üzere hello tüm yol yazın **Ekle** simgesi. Örneğin: "/etc/*.conf"
4. **Kaydet** düğmesine tıklayın.  

> [!NOTE]
> Linux dosya izleme dizini izleme, dizinler ve izleme joker aracılığıyla recrusion dahil olmak üzere ek özellikleri vardır.

### <a name="configure-windows-files-tootrack"></a>Windows dosyaları tootrack yapılandırın
Windows bilgisayarlarda adımları tooconfigure dosyaları tootrack aşağıdaki hello kullanın.

1. Merhaba OMS portalında tıklatın **ayarları** (Merhaba dişli symbol).
2. Merhaba üzerinde **ayarları** sayfasında, **veri**ve ardından **Windows dosya izleme**.
3. Windows dosya değişiklik izleme altında tootrack istediğiniz ve hello ardından hello dosyasının hello dosya adı dahil olmak üzere hello tüm yol yazın **Ekle** simgesi. Örneğin: C:\Program Files (x86) \Internet Explorer\iexplore.exe veya C:\Windows\System32\drivers\etc\hosts.
4. **Kaydet** düğmesine tıklayın.  
   ![Windows dosya değişiklik izleme](./media/log-analytics-change-tracking/windows-file-change-tracking.png)

### <a name="configure-windows-registry-keys-tootrack"></a>Windows kayıt defteri anahtarları tootrack yapılandırın
Windows bilgisayarlarda adımları tooconfigure kayıt defteri anahtarları tootrack aşağıdaki hello kullanın.

1. Merhaba OMS portalında tıklatın **ayarları** (Merhaba dişli symbol).
2. Merhaba üzerinde **ayarları** sayfasında, **veri**ve ardından **Windows kayıt defteri izleme**.
3. Windows kayıt defteri değişikliği izleme altında tootrack istediğiniz ve hello ardından hello tüm anahtarı yazın **Ekle** simgesi.
4. **Kaydet** düğmesine tıklayın.  
   ![Windows kayıt defteri değişiklik izleme](./media/log-analytics-change-tracking/windows-registry-change-tracking.png)

### <a name="explanation-of-linux-file-collection-properties"></a>Linux dosya koleksiyonu özellikleri açıklaması
1. **Tür**
   * **Dosya** (rapor dosya meta verileri - boyutu, değiştirilme tarihi, karma, vs.)
   * **Dizin** (rapor dizini meta verilerinin - boyutu, değiştirilme tarihi vb..)
2. **Bağlantılar** (Linux işleme simgesel başvuran tooother dosyaları veya dizinleri)
   * **Yoksay** (Yoksay simgesel bağlantı recurions toonot sırasında hello dosya veya dizinlerin başvurulan içerir)
   * **İzleyin** (izleyin hello simgesel bağlantı özyineleme tooalso sırasında hello dosya veya dizinlerin başvurulan içerir)
   * **Yönetme** (Merhaba simgesel bağlantı izleyin ve döndürülen içeriği hello işlenmesi alter)

   > [!NOTE]   
   > Merhaba "Manage" bağlantıları seçeneği önerilmez. Dosya içeriği alma desteklenmiyor.

3. **Recurse** (klasör düzeyleri arasında Recurse ve hello yol ifadesi toplantı tüm dosyaları izlemek)
4. **Sudo** (access dosyalarını veya sudo ayrıcalık gerektiren dizinleri etkinleştir)

### <a name="limitations"></a>Sınırlamalar
Merhaba değişiklik izleme çözümü şu anda aşağıdaki öğelerindeki hello desteklemez:

* Windows dosya izleme klasörleri (dizinleri)
* Windows dosya izleme için özyineleme
* Joker karakterler Windows dosya izleme
* Yol değişkenleri
* Ağ dosya sistemleri
* Dosya içeriği

Diğer sınırlamaları:

* Merhaba **en büyük dosya boyutu** sütun ve değerleri hello geçerli uygulamasında kullanılmayan.
* Birden fazla 2500 dosyaları hello 30 dakikalık toplama döngüsü toplarsanız çözüm performansın düşük.
* Ağ trafiği yüksek olduğunda, değişikliği kayıtları tooa altı saat toodisplay en fazla sürebilir.
* Bir bilgisayar kapalıyken hello yapılandırmasını değiştirirseniz, hello bilgisayar toohello önceki yapılandırmasına ait dosya değişiklikleri sonrasında.

## <a name="change-tracking-data-collection-details"></a>Veri toplama ayrıntılı izleme değiştirme
Değişiklik izleme, yazılım envanteri ve etkinleştirdiğiniz hello aracıları kullanarak Windows hizmeti meta verileri toplar.

Merhaba aşağıdaki tabloda veri toplama yöntemleri ve değişiklik izleme verileri nasıl toplanır ilgili diğer ayrıntıları gösterir.

| Platform | Doğrudan Aracısı | Operations Manager Aracısı | Linux Aracısı | Azure Storage | Operations Manager gerekli? | Operations Manager Aracısı verilerinin yönetim grubu gönderilen | Toplama sıklığı |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Windows ve Linux | &#8226; | &#8226; | &#8226; |  |  | &#8226; | Merhaba değişiklik türüne bağlı olarak too50 dakika 5 dakika. Merhaba aşağıdaki tablonun daha fazla bilgi için bkz. |


Merhaba aşağıdaki tabloda değişiklik hello türleri için hello veri toplama sıklığını gösterir.

| **türünü değiştirme** | **Sıklık** | **Mu****Aracısı****bulunduğunda farklar Gönder?**  |
| --- | --- | --- |
| Windows kayıt defteri | 50 dakika | Hayır |
| Windows dosya | 30 dakika | Evet. 24 saat içindeki herhangi bir değişiklik varsa, bir anlık görüntü gönderilir. |
| Linux dosya | 15 dakika | Evet. 24 saat içindeki herhangi bir değişiklik varsa, bir anlık görüntü gönderilir. |
| Windows hizmetleri | 30 dakika | Evet, değişiklikler bulunduğunda 30 dakikada. 24 saatte bir anlık görüntü, değişiklik bağımsız olarak gönderilir. Bu nedenle, hello anlık görüntü bile gönderilen hiçbir değişiklik olduğu. |
| Linux Daemon | 5 dakika | Evet. 24 saat içindeki herhangi bir değişiklik varsa, bir anlık görüntü gönderilir. |
| Windows yazılım | 30 dakika | Evet, değişiklikler bulunduğunda 30 dakikada. 24 saatte bir anlık görüntü, değişiklik bağımsız olarak gönderilir. Bu nedenle, hello anlık görüntü bile gönderilen hiçbir değişiklik olduğu. |
| Linux yazılım | 5 dakika | Evet. 24 saat içindeki herhangi bir değişiklik varsa, bir anlık görüntü gönderilir. |

### <a name="registry-key-change-tracking"></a>Kayıt defteri anahtarı değişiklik izleme

Günlük analizi izleme ve hello değişiklik izleme çözümü ile izleme Windows kayıt defteri gerçekleştirir. değişiklikleri tooregistry anahtarları izleme hello toopinpoint genişletilebilirlik noktaları nerede etkinleştirebilir üçüncü taraf kodu ve kötü amaçlı yazılım amaçtır. Merhaba hello çözümü tarafından izlenen ve her neden izlenen gösterir hello varsayılan kayıt defteri anahtarlarının listesi.

- HKEY\_yerel\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Startup
    - Başlangıçta çalıştırılmasını izleyiciler betikler.
- HKEY\_yerel\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Shutdown
    - İzleyiciler kapatma sırasında çalışan komutlar.
- HKEY\_yerel\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Run
    - Merhaba kullanıcı işaretleri tootheir Windows hesabı önce yüklenen anahtarları izler. Merhaba anahtarı, 64-bit bilgisayarlar üzerinde çalışan 32-bit programlar için kullanılır.
- HKEY\_yerel\_MACHINE\SOFTWARE\Microsoft\Active Setup\Installed bileşenleri
    - İzleyiciler tooapplication ayarlarını değiştirir.
- HKEY\_yerel\_MACHINE\Software\Classes\Directory\ShellEx\ContextMenuHandlers
    - Windows Gezgini ve genellikle çalışma işlemdeki Explorer.exe ile doğrudan kanca izleyiciler ortak autostart girişleri.
- HKEY\_yerel\_MACHINE\Software\Classes\Directory\Shellex\CopyHookHandlers
    - Windows Gezgini ve genellikle çalışma işlemdeki Explorer.exe ile doğrudan kanca izleyiciler ortak autostart girişleri.
- HKEY\_yerel\_MACHINE\Software\Classes\Directory\Background\ShellEx\ContextMenuHandlers
    - Windows Gezgini ve genellikle çalışma işlemdeki Explorer.exe ile doğrudan kanca izleyiciler ortak autostart girişleri.
- HKEY\_yerel\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - İzleyici simgesi için işleyici kaydı kaplama.
- HKEY\_yerel\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - İzleyici simgesi için 64-bit bilgisayarlar üzerinde çalışan 32-bit programlar için işleyici kaydı kaplama.
- HKEY\_yerel\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\Browser yardımcı nesneleri
    - Internet Explorer için yeni tarayıcı Yardımcısı nesnesi eklentilerin izleyiciler. Kullanılan tooaccess hello geçerli sayfa ve toocontrol Gezinti belge nesne modeli (DOM) hello.
- HKEY\_yerel\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\Browser yardımcı nesneleri
    - Internet Explorer için yeni tarayıcı Yardımcısı nesnesi eklentilerin izleyiciler. Kullanılan tooaccess hello 64-bit bilgisayarlar üzerinde çalışan 32-bit programlar için geçerli sayfa ve toocontrol Gezinti belge nesne modeli (DOM) hello.
- HKEY\_yerel\_MACHINE\Software\Microsoft\Internet Explorer\Extensions
    - Özel araç menüleri ve özel araç çubuğu düğmeleri gibi yeni Internet Explorer uzantıları için İzleyici.
- HKEY\_yerel\_MACHINE\Software\Wow6432Node\Microsoft\Internet Explorer\Extensions
    - Özel araç menüleri ve 64-bit bilgisayarlar üzerinde çalışan 32-bit programlar için özel araç çubuğu düğmeleri gibi yeni Internet Explorer uzantıları için İzleyici.
- HKEY\_yerel\_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    - Wavemapper, wave1 ve wave2, msacm.imaadpcm, .msadpcm, .msgsm610 ve vidc ile ilişkili hello 32-bit sürücüleri izler. Merhaba sistem benzer toohello [drivers] bölümü. INI dosyası.
- HKEY\_yerel\_MACHINE\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    - İzleyiciler hello 32-bit sürücüleri wavemapper, wave1 ve wave2, msacm.imaadpcm, .msadpcm, .msgsm610 ve 64-bit bilgisayarlar üzerinde çalışan 32-bit programlar için vidc ilişkili. Merhaba sistem benzer toohello [drivers] bölümü. INI dosyası.
- HKEY\_yerel\_MACHINE\System\CurrentControlSet\Control\Session Manager\KnownDlls
    - İzleyiciler bilinen veya sık kullanılan sistem DLL'leri listesi hello; Bu sistem, sistem DLL'leri Truva atı sürümlerinde bırakarak zayıf uygulama dizin izinlerini yararlanmasını kişilerin engeller.
- HKEY\_yerel\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify
    - Winlogon, hello etkileşimli oturum açma desteği modeli hello Windows işletim sistemi için paketler mümkün tooreceive olay bildirimleri izleyiciler hello listesi.


## <a name="use-change-tracking"></a>Değişiklik izlemeyi kullanma
Merhaba çözüm yüklendikten sonra değişikliklerin hello özeti izlenen sunucularınız için hello kullanarak görüntüleyebileceğiniz **değişiklik izleme** döşeme hello üzerinde **genel bakış** OMS sayfasında.

![Değişiklik izleme kutucuğu görüntüsü](./media/log-analytics-change-tracking/change-tracking-tile.png)

Değişiklikleri tooyour altyapı ve -ayrıntıya kategorileri aşağıdaki hello ayrıntılarını görüntüleyebilirsiniz:

* Yazılım ve Windows Hizmetleri için yapılandırma türüne göre değişiklikler
* Tooapplications ve tek tek sunucular için yazılım değişiklikleri
* Yazılım değişiklikleri her uygulama için toplam sayısı
* Linux paketleri
* Windows hizmet değişiklikleri tek tek sunucular için
* Linux daemon değişiklikleri

![Değişiklik izleme Panosu görüntüsü](./media/log-analytics-change-tracking/change-tracking-dash01.png)

![Değişiklik izleme Panosu görüntüsü](./media/log-analytics-change-tracking/change-tracking-dash02.png)

### <a name="tooview-changes-for-any-change-type"></a>tooview değişiklikleri herhangi türünü değiştirme
1. Merhaba üzerinde **genel bakış** hello sayfasında, **değişiklik izleme** döşeme.
2. Merhaba üzerinde **değişiklik izleme** panoyu hello değişiklik türü Kanatlar birinde hello özet bilgileri gözden geçirin ve ardından bir tooview hakkında ayrıntılı bilgi, hello içinde **günlük arama** sayfası.
3. Merhaba günlük arama sayfaları hiçbirinde, sonuçları zaman, ayrıntılı sonuçları ve günlük arama geçmişi görüntüleyebilirsiniz. Modelleri toonarrow hello sonuçlarına göre de filtre uygulayabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
* Kullanım [günlük analizi aramaları oturum](log-analytics-log-searches.md) tooview ayrıntılı izleme verilerini değiştirme.
