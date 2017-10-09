---
title: "Günlük analizi izleme çözümüne aaaVMware | Microsoft Docs"
description: "Nasıl hello VMware izlemesi çözümü günlüklerini yönetmek ve ESXi konakları izlemenize yardımcı olabilir hakkında bilgi edinin."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 16516639-cc1e-465c-a22f-022f3be297f1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: 959d5c2201fc5c7947f8b8870d055cdf9eea8e01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="vmware-monitoring-preview-solution-in-log-analytics"></a>Günlük analizi çözümüne VMware izleme (Önizleme)

![VMware simgesi](./media/log-analytics-vmware/vmware-symbol.png)

Merhaba günlük analizi VMware izleme çözümde, Merkezi günlük kaydı ve büyük VMware günlükleri için izleme yaklaşımı oluşturmanıza yardımcı olan bir çözümdür. Bu makalede nasıl sorun giderme, yakalama ve hello ESXi konaklarının hello çözümünü kullanarak tek bir konumda açıklanmaktadır. Merhaba çözümüyle tüm ESXi konaklarının tek bir konumda ayrıntılı veri görebilirsiniz. Üst olay sayısı, durumu ve eğilimleri hello ESXi ana günlükleri ile sağlanan VM ve ESXi konakları görebilirsiniz. Görüntüleme ve merkezi ESXi ana günlüklerini arama giderebilirsiniz. Ve günlük arama sorgularına dayalı uyarılar oluşturabilirsiniz.

Merhaba çözüm hello ESXi ana toopush veri tooa hedef OMS Aracısı VM yerel syslog işlevselliğini kullanır. Ancak, hello çözüm hello hedef VM içinde syslog içine dosyaları yazma değil. Merhaba OMS Aracısı bağlantı noktası 1514 açar ve toothis dinler. Merhaba verileri aldıktan sonra hello OMS Aracısı hello veri OMS iter.

## <a name="installing-and-configuring-hello-solution"></a>Yükleme ve yapılandırma hello çözümü
Bilgi tooinstall aşağıdaki hello kullanın ve hello çözüm yapılandırın.

* Çözüm tooyour VMware izleme hello Hello işlemi kullanarak OMS çalışma açıklanan eklemek [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).

#### <a name="supported-vmware-esxi-hosts"></a>Desteklenen VMware ESXi konakları
vSphere ESXi ana 5.5 ve 6.0

#### <a name="prepare-a-linux-server"></a>Linux sunucusunu hazırlama
Linux işletim sistemi VM tooreceive tüm syslog veri hello ESXi konakları oluşturun. Merhaba [OMS Linux Aracısı](log-analytics-linux-agents.md) tüm ESXi syslog verileri barındırmak için hello koleksiyonu noktasıdır. Birden çok ESXi konakları tooforward günlükleri tooa tek Linux sunucusu, aşağıdaki örneğine hello olduğu gibi kullanabilirsiniz.  

   ![Syslog akışı](./media/log-analytics-vmware/diagram.png)

### <a name="configure-syslog-collection"></a>Syslog koleksiyonunu yapılandırma
1. Syslog iletme VSphere için ayarlayın. Ayrıntılı bilgi toohelp Syslog iletme yukarı ayarlamak için bkz: [syslog ESXi üzerinde yapılandırma 5.x ve 6.0 (2003322)](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2003322). Çok Git**ESXi ana bilgisayar yapılandırması** > **yazılım** > **Gelişmiş ayarları** > **Syslog**.
   ![vsphereconfig](./media/log-analytics-vmware/vsphere1.png)  
2. Merhaba, *Syslog.global.logHost* alan, Linux sunucusu ve başlangıç bağlantı noktası numarası eklemek *1514*. Örneğin, `tcp://hostname:1514` veya`tcp://123.456.789.101:1514`
3. Syslog Hello ESXi ana bilgisayar Güvenlik Duvarı'nı açın. **ESXi ana bilgisayar yapılandırması** > **yazılım** > **güvenlik profili** > **Güvenlik Duvarı** ve açın **Özellikler**.  

    ![vspherefw](./media/log-analytics-vmware/vsphere2.png)  

    ![vspherefwproperties](./media/log-analytics-vmware/vsphere3.png)  
4. Bu syslog doğru şekilde kurulduğundan hello vSphere konsol tooverify denetleyin. ESXI konağı, bağlantı noktası üzerinde Hello onaylayın **1514** yapılandırılır.
5. Karşıdan yükleyip hello OMS aracısı için Linux hello Linux sunucusu üzerinde. Daha fazla bilgi için bkz: Merhaba [Linux için OMS aracısının belgelere](https://github.com/Microsoft/OMS-Agent-for-Linux).
6. Merhaba Linux için OMS Aracısı yüklendikten sonra toohello /etc/opt/microsoft/omsagent/sysconf/omsagent.d dizin ve kopyalama hello vmware_esxi.conf dosyası toohello /etc/opt/microsoft/omsagent/conf/omsagent.d dizini gidin ve değişiklik hello sahibi/Grup hello ve hello dosyasının izinler. Örneğin:

    ```
    sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/vmware_esxi.conf /etc/opt/microsoft/omsagent/conf/omsagent.d
   sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf
    ```
7. Merhaba OMS aracısı için Linux çalıştırarak yeniden `sudo /opt/microsoft/omsagent/bin/service_control restart`.
8. Test hello Linux sunucusu ile Merhaba ESXi ana bilgisayar arasında hello bağlantı hello kullanarak `nc` hello ESXi ana bilgisayar üzerinde komutu. Örneğin:

    ```
    [root@ESXiHost:~] nc -z 123.456.789.101 1514
    Connection too123.456.789.101 1514 port [tcp/*] succeeded!
    ```

9. Bir günlük araması Hello OMS portalı, `Type=VMware_CL`. OMS hello syslog veri topladığında, hello syslog biçimine korunur. Merhaba Portalı'nda belirli bazı alanlar, gibi yakalanır *ana bilgisayar adı* ve *işlemadı*.  

    ![type](./media/log-analytics-vmware/type.png)  

    Görünüm günlük arama sonuçlarınızı yukarıdaki benzer toohello görüntü varsa, toouse hello OMS VMware izleme çözüm panosunu hazırsınız.  

## <a name="vmware-data-collection-details"></a>VMware veri toplama ayrıntıları
Merhaba VMware izlemesi çözümü hello OMS Aracısı etkinleştirdiğiniz Linux için kullanarak ESXi ana bilgisayarları çeşitli performans ölçümleri ve günlük verilerini toplar.

Merhaba aşağıdaki tabloda veri toplama yöntemleri ve verileri nasıl toplanır ilgili diğer ayrıntıları gösterir.

| Platform | Linux için OMS Aracısı | SCOM Aracısı | Azure Storage | SCOM gerekli? | Yönetim grubu gönderilen SCOM Aracısı verileri | Toplama sıklığı |
| --- | --- | --- | --- | --- | --- | --- |
| Linux |&#8226; |  |  |  |  |3 dakikada bir |

Aşağıdaki tablonun hello hello VMware izlemesi çözümü tarafından toplanan veri alanlarının örnekler:

| Alan adı | açıklama |
| --- | --- |
| Device_s |VMware depolama aygıtları |
| ESXIFailure_s |hata türleri |
| EventTime_t |Olay gerçekleştiği zaman |
| HostName_s |ESXi ana bilgisayar adı |
| Operation_s |VM oluşturma veya VM silme |
| ProcessName_s |Olay adı |
| ResourceId_s |Merhaba VMware ana bilgisayar adı |
| ResourceLocation_s |VMware |
| ResourceName_s |VMware |
| ResourceType_s |Hyper-V |
| SCSIStatus_s |VMware SCSI durumu |
| SyslogMessage_s |Syslog verilerinin |
| UserName_s |oluşturulan veya silinen VM kullanıcı |
| VMName_s |VM adı |
| Bilgisayar |ana bilgisayar |
| TimeGenerated |zaman hello veri oluşturuldu |
| DataCenter_s |VMware datacenter |
| StorageLatency_s |Depolama gecikme süresi (ms) |

## <a name="vmware-monitoring-solution-overview"></a>VMware izleme çözümüne genel bakış
Merhaba VMware döşeme hello OMS portalında görünür. Hataları üst düzey bir görünümünü sağlar. Merhaba kutucuğa tıkladığınızda, Pano Görünümü'ne gidin.

![Döşeme](./media/log-analytics-vmware/tile.png)

#### <a name="navigate-hello-dashboard-view"></a>Merhaba Pano görünümü gidin
Merhaba, **VMware** Pano görünümü Kanatlar göre düzenlenir:

* Hata durum sayısı
* Üst konak olay tarafından sayar
* Üst olay sayısı
* Sanal makine etkinlikleri
* ESXi ana Disk olayları

![solution1](./media/log-analytics-vmware/solutionview1-1.png)

![solution2](./media/log-analytics-vmware/solutionview1-2.png)

Tüm dikey tooopen ayrıntılı bilgiler için hello dikey belirli gösterilmektedir günlük analizi arama Bölmesi'ı tıklatın.

Buradan, hello arama sorgusu toomodify düzenleyebilirsiniz belirli bir şey için. OMS arama hello temelleri üzerinde bir öğretici için hello denetleyin [OMS günlük arama öğretici.](log-analytics-log-searches.md)

#### <a name="find-esxi-host-events"></a>ESXi ana bilgisayar olaylarını Bul
Tek bir ESXi ana kendi işlemleri temel alan birden çok günlükleri oluşturur. Merhaba VMware izlemesi çözümü bunları merkezi hale getirir ve hello olay sayıları özetlenmektedir. Merkezi bu görünüm, yüksek hacimli olayları hangi ESXi ana bilgisayarı vardır ve ortamınızda hangi olayların sık karşılaşılan anlamanıza yardımcı olur.

![Olay](./media/log-analytics-vmware/events.png)

Ayrıntıya inebilir başka bir ESXi ana bilgisayar veya bir olay türü'ı tıklatarak.

Bir ESXi ana bilgisayar adını tıklattığınızda, o ESXi ana bilgisayardan bilgileri görüntüleyin. Merhaba olay türü ile toonarrow sonuçları istiyorsanız ekleyin `“ProcessName_s=EVENT TYPE”` arama Sorgunuzdaki. Seçebileceğiniz **işlemadı** hello arama filtresi. Hello bilgileri daraltır.

![Detaya gitme](./media/log-analytics-vmware/eventhostdrilldown.png)

#### <a name="find-high-vm-activities"></a>Yüksek VM etkinlikleri Bul
Bir sanal makine oluşturulur ve herhangi bir ESXi ana silinir. ESXi ana bilgisayar oluşturur kaç VM için bir yönetici tooidentify yardımcı olur. Bu dönüş, toounderstand performans ve kapasite planlamasına yardımcı olur. Ortamınızı yönetirken VM etkinlik olayları izlemek önemlidir.

![Detaya gitme](./media/log-analytics-vmware/vmactivities1.png)

Toosee ek ESXi ana VM oluşturma verileri istiyorsanız, bir ESXi ana bilgisayar adına tıklayın.

![Detaya gitme](./media/log-analytics-vmware/createvm.png)

#### <a name="common-search-queries"></a>Ortak arama sorguları
Merhaba çözüm yüksek depolama alanı, depolama gecikmesi ve yol hatası gibi ESXi konakları yönetmenize yardımcı olabilir diğer yararlı sorgular içerir.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Sorguları](./media/log-analytics-vmware/queries.png)


#### <a name="save-queries"></a>Sorguları Kaydet
Arama sorguları kaydetme OMS standart bir özelliktir ve yararlı buldunuz herhangi bir sorgu tutmanıza yardımcı olabilir. Size kullanışlı bir sorgu oluşturduktan sonra hello tıklayarak Kaydet **Sık Kullanılanlar**. Kayıtlı bir sorguyu kolayca hello daha sonra yeniden olanak sağlayan [My Pano](log-analytics-dashboards.md) kendi özel panolar oluşturabileceğiniz sayfası.

![DockerDashboardView](./media/log-analytics-vmware/dockerdashboardview.png)

#### <a name="create-alerts-from-queries"></a>Uyarı sorgularından oluşturma
Sorgularınızın oluşturduktan sonra toouse hello sorguları tooalert isteyebilirsiniz, belirli olaylar meydana geldiğinde. Bkz: [günlük analizi uyarılarını](log-analytics-alerts.md) hakkında bilgi için toocreate uyarıları. Merhaba sorguları ve diğer sorgu örnekleri örnekler için bkz [İzleyici OMS günlük analizi kullanarak VMware](https://blogs.technet.microsoft.com/msoms/2016/06/15/monitor-vmware-using-oms-log-analytics) blog postası.

## <a name="frequently-asked-questions"></a>Sık sorulan sorular
### <a name="what-do-i-need-toodo-on-hello-esxi-host-setting-what-impact-will-it-have-on-my-current-environment"></a>Ayarı hello ESXi ana bilgisayarda toodo ne yapmalıyım? Hangi, my geçerli ortamda etkileyecek?
Merhaba çözüm hello yerel ESXi ana Syslog iletme mekanizması kullanır. Herhangi bir ek Microsoft yazılım hello ESXi ana toocapture hello günlükleri üzerinde gerekmez. Düşük etkisi tooyour varolan ortam olmalıdır. Ancak, ESXI işlevselliği tooset syslog iletme gerekir.

### <a name="do-i-need-toorestart-my-esxi-host"></a>My ESXi ana toorestart gerekiyor mu?
Hayır. Bu işlem, yeniden başlatma gerektirmez. Bazı durumlarda, vSphere hello syslog düzgün şekilde güncelleştirmez. Böyle bir durumda toohello ESXi ana bilgisayarda oturum açın ve hello syslog yeniden yükleyin. Yeniden, bu işlem kesintiye uğratan tooyour ortamı değil şekilde toorestart hello konak yok.

### <a name="can-i-increase-or-decrease-hello-volume-of-log-data-sent-toooms"></a>I artırıp hello toplu günlük verileri tooOMS gönderilen azaltabilirsiniz?
Evet, engelleyebilirsiniz. VSphere içinde hello ESXi ana günlük düzeyi ayarlarını kullanabilirsiniz. Günlük toplama hello üzerinde temel *bilgisi* düzeyi. Tooaudit VM oluşturulurken veya silinirken istiyorsanız, bu nedenle, tookeep hello gerekir *bilgisi* Hostd düzeyi. Daha fazla bilgi için bkz: Merhaba [VMware Bilgi Bankası](https://kb.vmware.com/selfservice/microsites/search.do?&cmd=displayKC&externalId=1017658).

### <a name="why-is-hostd-not-providing-data-toooms-my-log-setting-is-set-tooinfo"></a>Neden Hostd veri tooOMS sağlamıyor? My günlük ayarı tooinfo ayarlanır.
Merhaba syslog zaman damgası için bir ESXi ana bilgisayar hata oluştu. Daha fazla bilgi için bkz: Merhaba [VMware Bilgi Bankası](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2111202). Merhaba geçici çözüm uygulandıktan sonra Hostd normal olarak çalışması.

### <a name="can-i-have-multiple-esxi-hosts-forwarding-syslog-data-tooa-single-vm-with-omsagent"></a>Birden çok ESXi sahip olabilir syslog veri tooa iletmek hosts tek VM ile omsagent?
Evet. Birden çok ESXi olabilir tooa iletmek hosts tek VM ile omsagent.

### <a name="why-dont-i-see-data-flowing-into-oms"></a>Veri akışının OMS neden göremiyorum?
Birden çok nedeni olabilir:

* Merhaba ESXi ana bilgisayar veri toohello VM çalışan omsagent doğru Ftp'den değil. tootest, hello aşağıdaki adımları gerçekleştirin:

  1. tooconfirm, toohello ESXi ana bilgisayarında ssh kullanarak oturum açın ve hello aşağıdaki komutu çalıştırın:`nc -z ipaddressofVM 1514`

      Bu başarılı olmazsa, Gelişmiş Yapılandırma olan büyük olasılıkla hello vSphere ayarlarında düzeltin değil. Bkz: [syslog koleksiyonunu yapılandırma](#configure-syslog-collection) tooset hello ESXi yukarı syslog iletme için nasıl ana bilgisayar hakkında bilgi.
  2. Syslog bağlantı noktası bağlantı başarılı olur, ancak yine de hiçbir veri görmezsiniz, hello syslog hello ESXi ana bilgisayarda ssh komutu aşağıdaki toorun hello kullanarak yeniden:` esxcli system syslog reload`
* Merhaba VM OMS Aracısı ile düzgün ayarlanmadı. tootest bunu hello aşağıdaki adımları gerçekleştirin:

  1. OMS toohello bağlantı noktası 1514 dinler ve veri OMS iter. açık olduğunu tooverify hello aşağıdaki komutu çalıştırın:`netstat -a | grep 1514`
  2. Bağlantı noktası görmelisiniz `1514/tcp` açın. Bunu yapmazsanız, o hello omsagent düzgün yüklendiğini doğrulayın. Başlangıç bağlantı noktası bilgilerini görmüyorsanız hello syslog bağlantı noktası hello VM üzerinde açık değil.

     1. OMS Aracısı çalıştıran kullanarak bu hello doğrulayın `ps -ef | grep oms`. Merhaba komutu çalıştırarak hello işlem çalışmıyorsa, Başlat` sudo /opt/microsoft/omsagent/bin/service_control start`
     2. Açık hello `/etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf` dosya.

         Merhaba uygun kullanıcı ve grup ayarı geçerli ve benzer şekilde doğrulayın:`-rw-r--r-- 1 omsagent omiusers 677 Sep 20 16:46 vmware_esxi.conf`

         Merhaba dosya yok veya hello kullanıcı ve grup ayarı yanlış ise, tarafından düzeltici işlemleri [Linux sunucusu hazırlama](#prepare-a-linux-server).

## <a name="next-steps"></a>Sonraki adımlar
* Kullanım [günlük aramaları](log-analytics-log-searches.md) günlük analizi tooview VMware ana verileri ayrıntılı.
* [Kendi panolar oluşturun](log-analytics-dashboards.md) VMware ana verileri gösterme.
* [Uyarı oluşturma](log-analytics-alerts.md) belirli VMware konak olayları olduğunda.
