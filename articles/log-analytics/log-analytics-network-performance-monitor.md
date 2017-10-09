---
title: "aaaNetwork Azure günlük analizi Performans İzleyicisi çözümde | Microsoft Docs"
description: "Ağ Performans İzleyicisi'nde Azure günlük analizi ağları eklentinizi real zamanlı toodetect yakın hello performansını izlemek ve ağ performans sorunlarını bulmanıza yardımcı olur."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 5b9c9c83-3435-488c-b4f6-7653003ae18a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: e074948221fdd003c640861d759c4ce69ced1cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="network-performance-monitor-solution-in-log-analytics"></a>Günlük analizi Performans İzleyicisi çözümde ağ

![Ağ Performans İzleyici simgesi](./media/log-analytics-network-performance-monitor/npm-symbol.png)

Bu belgede ağları eklentinizi real zamanlı toodetect yakın hello performansını izlemek ve ağ performans sorunlarını bulmanıza yardımcı olur günlük analizi Ağ Performansı İzleyicisi çözümde tooset yukarı ve kullanım nasıl hello açıklanmaktadır. Merhaba Ağ Performansı İzleyicisi çözüm hello kaybı ve gecikme süresi iki ağ, alt ağları veya sunucular arasında izleyebilirsiniz. Ağ Performansı İzleyicisi trafiği blackholing, yönlendirme hataları ve geleneksel ağ izleme yöntemleri mümkün toodetect olmayan sorunlar gibi ağ sorunları algılar. Ağ Performansı İzleyicisi uyarılar oluşturur ve olarak ve bir ağ bağlantısı için bir eşik aşıldığında bildirir. Bu eşikler hello sistem tarafından otomatik olarak öğrenilebilecek veya toouse özel uyarı kuralları yapılandırabilirsiniz. Ağ Performansı İzleyicisi Merhaba kaynak hello sorun tooa belirli ağ kesimine veya aygıtın yerelletirilmesi ve ağ performans sorunlarını zamanında algılanması sağlar.

Son ağ sistem durumu olayları, sağlıksız ağ bağlantıları ve yüksek paket kaybı ve gecikme süresi karşılıklı alt ağ bağlantıları dahil olmak üzere ağınız hakkında özet bilgileri görüntüler hello çözüm Panosu ağ sorunları algılayabilir. Bir ağ bağlantısı tooview hello geçerli sistem durumunu alt ağ bağlantıları ve bunun yanı sıra düğümü düğümü bağlantılarını ayrıntıya. Merhaba geçmiş eğilim kaybı ve gecikme hello ağ, alt ağ ve düğümü düğümü düzeyinde de görüntüleyebilirsiniz. Paket kaybı ve gecikme süresi geçmiş eğilim grafiklerde görüntüleyerek geçici ağ sorunları algılar ve bir topoloji Haritası üzerinde ağ engelleri bulun. Merhaba etkileşimli topoloji grafik hello hello sorunun kaynağını belirlemek ve toovisualize hello atlama atlamalı ağ yollarını sağlar. Günlük arama çeşitli analiz için kullanabileceğiniz diğer çözümleri gibi ağ performansı İzleyicisi tarafından toplanan hello verileri temel gereksinimleri toocreate özel raporlar.

Merhaba çözüm yapay işlemler bir birincil mekanizmayı toodetect ağ hatalarını kullanır. Bu nedenle, belirli ağ cihazın satıcı veya model için bakmadan kullanabilirsiniz. Şirket içi, bulut (Iaas) ve karma ortamlar arasında çalışır. Merhaba çözüm hello ağ topolojisi ve ağınızdaki çeşitli yolları otomatik olarak bulur.

Merhaba izleme tipik ağ izleme ürünleri odaklanmasına cihaz (yönlendiriciler, anahtarlar vb.) sistem durumu ağ ancak hello gerçek ağ performansı İzleyicisi mu iki nokta arasında ağ bağlantısı kalitesini Öngörüler sağlamaz.

### <a name="using-hello-solution-standalone"></a>Merhaba çözüm tek başına kullanma
Ağ bağlantıları, kritik iş yüklerini arasında toomonitor hello kalitesini istiyorsanız, ağları, veri merkezleri veya office siteleri sonra hello Ağ Performansı İzleyicisi çözüm tek başına toomonitor bağlantı durumu arasında kullanabilirsiniz:

* bir genel veya özel ağ kullanarak bağlanan birden çok veri merkezi veya office siteler
* İş kolu uygulamaları çalıştıran kritik iş yükleri
* Microsoft Azure veya Amazon Web Hizmetleri (AWS) ve şirket içi ağlar, Iaas (VM) kullanılabilir varsa ve ağ geçitleri gibi genel bulut hizmetlerini şirket içi ağlar ve bulut ağları arasında tooallow iletişim yapılandırılmış
* Hızlı rota kullandığınızda azure ve şirket içi ağlar

### <a name="using-hello-solution-with-other-networking-tools"></a>Merhaba çözümü ile ağ diğer araçları kullanarak
Bir iş hattı uygulaması toomonitor istiyorsanız, bir yardımcı çözüm tooother ağ araçları hello Ağ Performansı İzleyicisi çözüm kullanabilirsiniz. Yavaş bir ağ tooslow uygulamaları açabilir ve Ağ Performansı İzleyicisi tarafından temel ağ sorunları nedeniyle uygulama performans sorunlarını araştırmanıza yardımcı olabilir. Merhaba çözüm herhangi erişim toonetwork aygıtları gerektirmediğinden hello Uygulama Yöneticisi toorely hello ağ uygulamaları nasıl etkilediğini hakkında ağ bir takım tooprovide bilgileri gerekmez.

İzleme Araçları diğer ağ zaten yatırım, çoğu geleneksel ağ izleme çözümleri uçtan uca ağ performans ölçümleri kaybı ve gecikme gibi Öngörüler sağlamadığı için Ayrıca, ardından hello çözüm araçların tamamlayabilir.  Merhaba Ağ Performansı İzleyicisi çözümü bu boşluğu doldurmak yardımcı olabilir.

## <a name="installing-and-configuring-agents-for-hello-solution"></a>Merhaba çözüm için aracıları yükleme ve yapılandırma
Merhaba temel işlemleri tooinstall aracıların adresindeki [bağlanmak Windows bilgisayarları tooLog Analytics](log-analytics-windows-agents.md) ve [Operations Manager bağlanmak tooLog Analytics](log-analytics-om-agents.md).

> [!NOTE]
> Sipariş toohave tooinstall en az 2 aracıları yeterli veri toodiscover gerekir ve ağ kaynaklarınıza izleme. Aksi durumda, ek aracıları yükleyip kadar hello Çözüm yapılandırılırken bir durumda kalır.
>
>

### <a name="where-tooinstall-hello-agents"></a>Burada tooinstall hello aracıları
Aracıları yüklemeden önce ağınızın hello topolojisi ve hangi bölümlerinin hello ağ istediğiniz toomonitor göz önünde bulundurun. Toomonitor istediğiniz her alt ağ için birden fazla aracı yüklemenizi öneririz. Diğer bir deyişle, toomonitor istediğiniz her bir alt iki veya daha fazla sunucular veya VM'ler seçin ve bunlar üzerinde hello aracısını yükleyin.

Ağınızın hello topolojisi hakkında emin değilseniz, toomonitor hello ağ performansını istediğiniz kritik iş yükleri ile sunucularda hello aracıları yükleyin. Örneğin, bir Web sunucusu ve SQL Server çalıştıran bir sunucu arasındaki ağ bağlantısının tookeep izlemek isteyebilirsiniz. Bu örnekte, bir aracı sunucularda hem de yüklenir.

Aracıları konakları--değil hello konakları kendilerini arasında ağ bağlantısı (Bağlantılar) izleyin. Bu nedenle, toomonitor bir ağ bağlantısı o bağlantı üzerindeki her iki uç noktaları aracıları yüklemeniz gerekir.

### <a name="configure-agents"></a>Aracıları yapılandırma

Yapay işlemler için toouse hello ICMP Protokolü düşünüyorsanız, güvenilir bir şekilde ICMP kullanan için güvenlik duvarı kuralları aşağıdaki tooenable hello gerekir:

```
netsh advfirewall firewall add rule name="NPMDICMPV4Echo" protocol="icmpv4:8,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6Echo" protocol="icmpv6:128,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV4DestinationUnreachable" protocol="icmpv4:3,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6DestinationUnreachable" protocol="icmpv6:1,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV4TimeExceeded" protocol="icmpv4:11,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6TimeExceeded" protocol="icmpv6:3,any" dir=in action=allow
```


Toouse hello TCP protokolü düşünüyorsanız, aracıları iletişim kurabilen bu bilgisayarları tooensure için tooopen güvenlik duvarı bağlantı noktaları gerekir. Toodownload gerekir ve ardından hello çalıştırın [EnableRules.ps1 PowerShell Betiği](https://gallery.technet.microsoft.com/OMS-Network-Performance-04a66634) yönetici ayrıcalıklarıyla bir PowerShell penceresinde herhangi bir parametre olmadan.

Ağ Performansı İzleyicisi Merhaba tarafından gerekli kayıt defteri anahtarlarını Hello betiği oluşturur ve onu Windows Güvenlik duvarı kuralları tooallow aracıları toocreate TCP bağlantılarını birbirleri ile oluşturur. Merhaba komut dosyası tarafından oluşturulan hello kayıt defteri anahtarlarını da toolog hello günlükleri ve hello yolu hello günlükleri dosyası için hata ayıklama olup olmadığını belirtin. Ayrıca, hello Aracısı TCP bağlantı noktası iletişimi için kullanılan tanımlar. Bu anahtarları el ile değiştirmemelisiniz şekilde hello değerleri bu anahtarları için başlangıç betiği tarafından otomatik olarak ayarlanır.

Varsayılan olarak açılır hello bağlantı noktası 8084'dir. Özel bir bağlantı noktası hello parametre sağlayarak kullanabileceğiniz `portNumber` toohello komut dosyası. Ancak, hello aynı bağlantı noktasını tüm hello bilgisayarlarda hello betik çalıştırdığı kullanılmalıdır.

> [!NOTE]
> Hello EnableRules.ps1 komut dosyası hello betik çalıştırdığı yalnızca hello bilgisayarda Windows Güvenlik duvarı kuralları yapılandırır. Ağ güvenlik duvarı varsa, Ağ Performansı İzleyicisi tarafından kullanılan hello TCP bağlantı noktası için giden trafiğe izin verdiğinden emin olun.
>
>

## <a name="configuring-hello-solution"></a>Merhaba çözüm yapılandırılıyor
Bilgi tooinstall aşağıdaki hello kullanın ve hello çözüm yapılandırın.

1. Merhaba Ağ Performansı İzleyicisi çözüm edinme verileri Windows Server 2008 SP 1 veya sonrasını çalıştıran bilgisayarlar veya Windows 7 SP1 veya daha sonra hangi olan hello aynı Microsoft İzleme Aracısı'nı (MMA) hello gibi gereksinimleri. NPM aracıları, Windows Masaüstü/istemci işletim sistemlerinde (Windows 10, Windows 8.1, Windows 8 ve Windows 7) olarak da çalıştırabilirsiniz.
    >[!NOTE]
    >Windows server işletim sistemleri için Hello aracıları hello protokolleri yapay işlem olarak TCP ve ICMP destekler. Ancak, Windows istemci işletim sistemleri için hello aracıları yalnızca ICMP yapay işlem hello protokol olarak destekler.

2. Merhaba Ağ Performansı İzleyicisi çözüm tooyour çalışma alanından eklemek [Azure Market](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.NetworkMonitoringOMS?tab=Overview) veya açıklanan hello işlemi kullanarak [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).  
   ![Ağ Performans İzleyici simgesi](./media/log-analytics-network-performance-monitor/npm-symbol.png)
3. Merhaba OMS portalında başlıklı yeni bir kutucuk görürsünüz **Ağ Performansı İzleyicisi** hello iletiyle *çözüm ek yapılandırma gerektirir*. Alt ağlar ve aracıları tarafından bulunan düğümleri göre tooconfigure hello çözüm tooadd ağlar gerekir. Tıklatın **Ağ Performansı İzleyicisi** toostart hello varsayılan ağ yapılandırma.  
   ![Çözüm ek yapılandırma gerektirir](./media/log-analytics-network-performance-monitor/npm-config.png)

### <a name="configure-hello-solution-with-a-default-network"></a>Bir varsayılan ağ ile Merhaba çözümünüzü yapılandırma
Merhaba yapılandırma sayfasında adlı tek bir ağ göreceksiniz **varsayılan**. Herhangi bir ağa tanımlandığında yapmadıysanız, otomatik olarak bulunan tüm hello alt hello varsayılan ağında yerleştirilir.

Her bir ağ oluşturduğunuzda, bir alt ağ tooit ve o alt hello varsayılan ağdan kaldırılır ekleyin. Bir ağ silerseniz, tüm alt toohello varsayılan ağ otomatik olarak döndürülür.

Diğer bir deyişle, hello varsayılan ağ hello herhangi bir kullanıcı tarafından tanımlanan ağ içinde yer almayan tüm hello alt ağlar için kapsayıcıdır. Düzenleyemez veya hello varsayılan ağ silinemedi. Her zaman, hello sistemde kalır. Ancak, gerektiği kadar ağlar oluşturabilirsiniz.

Çoğu durumda hello alt ağlar, kuruluşunuzda birden fazla ağ düzenlenmiş ve bir kısayol oluşturmanız gerekir veya daha fazla ağları toologically ağlarınızı grup.

### <a name="create-new-networks"></a>Yeni ağ oluşturma
Ağ Performans İzleyicisi'nde bir ağ alt ağlar için bir kapsayıcıdır. İstediğiniz ve alt ağları toohello ağ Ekle herhangi bir adı ile ağ oluşturabilirsiniz. Örneğin, adlı bir ağ oluşturabilirsiniz *Building1* ve alt ağlar eklemek veya adlı bir ağ oluşturabilirsiniz *DMZ* ve toodemilitarized bölge toothis ağ ait tüm alt ağlar ekleyin.

#### <a name="toocreate-a-new-network"></a>toocreate yeni bir ağ
1. Tıklatın **Ekle ağ** ve hello ağ adını ve açıklamasını yazın.
2. Bir veya daha fazla alt ağ seçin ve ardından **Ekle**.
3. tıklatın **kaydetmek** toosave hello yapılandırma.  
   ![Ağ ekleme](./media/log-analytics-network-performance-monitor/npm-add-network.png)

### <a name="wait-for-data-aggregation"></a>Veri toplama bekle
Merhaba yapılandırma ilk kez kaydettikten sonra aracılar yüklendiği hello düğümler arasında ağ paket kaybı ve gecikme bilgileri toplanıyor hello çözüm başlatır. Bu işlem, bazen zaman 30 dakika. Bu aşamasında, hello Ağ Performansı İzleyicisi Merhaba genel bakış sayfasında parçasında belirten bir ileti görüntüler *veri toplama işleminde*.

![veri toplama işlemi sürüyor](./media/log-analytics-network-performance-monitor/npm-aggregation.png)

Merhaba veriler karşıya yüklendikten sonra hello Ağ Performansı İzleyicisi güncelleştirilmiş döşeme gösteren veri görürsünüz.

![Ağ Performans İzleyicisi kutucuğu](./media/log-analytics-network-performance-monitor/npm-tile.png)

Merhaba döşeme tooview hello Ağ Performansı İzleyicisi Pano'ı tıklatın.

![Ağ Performans İzleyicisi Panosu](./media/log-analytics-network-performance-monitor/npm-dash01.png)

### <a name="edit-monitoring-settings-for-subnets"></a>Alt ağlar için izleme ayarlarını Düzenle
En az bir Aracısı yüklendiği tüm alt ağlar üzerinde hello listelenen **ağlarla** hello yapılandırma sayfası sekmesindedir.

#### <a name="tooenable-or-disable-monitoring-for-particular-subnetworks"></a>tooenable veya belirli alt ağlar için izleme devre dışı
1. Seçin veya temizleyin hello kutusunu sonraki toohello **alt ağ kimliği** ve emin olun **kullanım izleme için** seçili veya temizlenmiş, uygun şekilde şeklindedir. Seçin veya birden çok alt ağı temizleyin. Merhaba aracıları diğer aracıları ping güncelleştirilmiş toostop olarak devre dışı bırakıldığında, alt ağlar izlenmeyen.
2. İzlenmeyen ve izlenen düğümleri içeren hello listeleri arasındaki gerekli düğümleri hello listesi ve taşıma hello alt ağı seçerek, belirli bir alt ağ için toomonitor istediğiniz hello düğümleri hello seçin.
   Özel bir ekleyebilirsiniz **açıklama** toohello alt ağ, isterseniz.
3. tıklatın **kaydetmek** toosave hello yapılandırma.  
   ![alt ağ Düzenle](./media/log-analytics-network-performance-monitor/npm-edit-subnet.png)

### <a name="choose-nodes-toomonitor"></a>Düğümleri toomonitor seçin
Bir aracısı yüklü olan tüm hello düğümleri hello listelenen **düğümleri** sekmesi.

#### <a name="tooenable-or-disable-monitoring-for-nodes"></a>tooenable veya düğümler için izleme devre dışı
1. Seçin veya toomonitor istediğiniz veya izlemeyi durdurmak hello düğüm temizleyin.
2. Tıklatın **kullanım izleme için**, veya, uygun şekilde temizleyin.
3. **Kaydet** düğmesine tıklayın.  
   ![düğüm izlemeyi etkinleştir](./media/log-analytics-network-performance-monitor/npm-enable-node-monitor.png)

### <a name="set-monitoring-rules"></a>İzleme kurallarını ayarlama
Ağ Performansı İzleyicisi sistem durumu olayları düğümleri veya bir eşik aşıldığında alt ağ veya ağ bağlantılarını çifti arasında hello bağlantısı hakkında oluşturur. Bu eşikler hello sistem tarafından otomatik olarak öğrenilebilecek veya özel uyarı kuralları yapılandırabilirsiniz.

Merhaba *varsayılan kural* hello sistem tarafından oluşturulan ve kayıp veya herhangi bir çifti ağların veya alt ağ arasındaki gecikme süresi ihlallerini hello sistem öğrenilen eşik bağlar her bir sistem durumu olayı oluşturur. Toodisable hello varsayılan kural'ı seçin ve özel izleme kurallarını oluşturun

#### <a name="toocreate-custom-monitoring-rules"></a>İzleme kurallarını özel toocreate
1. Tıklatın **Kuralı Ekle** hello içinde **İzleyici** sekmesinde ve hello kural ad ve açıklama girin.
2. Ağ veya alt ağ bağlantıları toomonitor Hello çifti hello listelerden seçin.
3. İlk hangi hello ilk alt ağ/s ilgi bulunan hello ağ hello ağ aşağı açılır listeden seçin ve ardından hello alt ağ/s hello karşılık gelen alt ağ aşağı açılır listeden seçin.
   Seçin **tüm alt ağlar** toomonitor istiyorsanız, tüm ağ bağlantısı alt ağlar hello. Benzer şekilde seçin, başka alt ağ/s ilgi hello. Ve tıklayabilirsiniz **özel durum ekleyin** hello seçimden belirli alt ağ bağlantıları için tooexclude izleme yaptığınız.
4. ICMP ve TCP arasında yapay işlemler yürütme için protokol seçin.
5. Seçtiğiniz hello öğeleri için toocreate sistem durumu olayları istemiyorsanız, ardından temizleyin **bu kural tarafından kapsanan hello bağlantılarında sistem durumu izlemeyi etkinleştir**.
6. İzleme koşulları seçin.
   Eşik değerleri yazarak, sistem olay oluşturma için özel eşikler ayarlayabilirsiniz. Seçili eşiğini hello seçili ağ/alt ağ çifti için yukarıdaki hello koşul Hello değerini gider olduğunda, bir sistem durumu olayı oluşturulur.
7. tıklatın **kaydetmek** toosave hello yapılandırma.  
   ![Özel İzleme kuralı oluşturma](./media/log-analytics-network-performance-monitor/npm-monitor-rule.png)

Bir izleme kuralı kaydettikten sonra bu kural uyarı yönetimi ile tıklayarak tümleştirebilirsiniz **oluşturma uyarı**. Bir uyarı kuralı hello arama sorgusu ve diğer gerekli otomatik olarak oluşturulan otomatik olarak doldurulmuş parametreler. Bir uyarı kuralı kullanarak, ayrıca toohello varolan NPM içinde Uyarıları e-posta tabanlı uyarılar alabilir. Uyarılar ayrıca eylemlerden runbook'larla tetikleyebilir veya Web kancalarını kullanarak mevcut hizmet yönetimi çözümleriyle tümleştirilebilir. Tıklayabilirsiniz **yönetmek uyarı** tooedit hello uyarı ayarları.

### <a name="choose-hello-right-protocol-icmp-or-tcp"></a>Merhaba sağ Protokolü ICMP veya TCP seçin

Ağ Performans İzleyicisi'ni (NPM) yapay işlemler toocalculate ağ performans ölçümleri paket kaybı ve bağlantı gecikme süresi gibi kullanır. toounderstand bu daha iyi ve göz önünde bulundurun bir ağ bağlantısı NPM Aracısı bağlı tooone sonu. Bu NPM Aracısı gönderir araştırma paketleri tooa ikinci NPM Aracısı bağlı tooanother sonu hello ağ. Merhaba ikinci Aracısı yanıtlar yanıt paketleri ile. Bu işlem birkaç kez yinelenir. Yanıtlar ve geçen süre tooreceive hello sayısı her yanıt ölçme, bağlantı gecikmesi hello ilk NPM Aracısı değerlendirir ve paket bırakma.

Merhaba biçimi, boyut ve bu paketlerin dizisini belirlenir izleme kurallarını oluştururken seçtiğiniz hello protokolü. Ara ağ aygıtlarını (yönlendiriciler, anahtarlar vb.) hello Karşılama paketleri protokole ilişkin bağlı olarak, bu paketleri farklı işlem. Sonuç olarak, Protokolü tercih ettiğiniz hello sonuçları hello doğruluğunu etkiler. Ve protokolü tercih ettiğiniz de hello NPM çözümü dağıttıktan sonra herhangi bir el ile adımlar atmanız gerekir olup olmadığını belirler.

NPM, yapay işlemleri yürütmek ICMP ve TCP protokollerini arasında seçim hello sunar.
Yapay işlem kuralı oluşturduğunuzda, ICMP seçerseniz, ICMP YANKI iletileri toocalculate hello ağ gecikme süresi ve paket kaybı hello NPM aracıları kullanın. İleti almak için diğer bir deyişle, aynı ICMP YANKI kullanır hello hello geleneksel Ping yardımcı programı tarafından gönderilir. Merhaba protokol olarak TCP'yi kullandığınızda NPM aracıları hello ağ üzerinden TCP Eşitlemeye paket gönderin. Bu bir TCP anlaşması tarafından izlenir tamamlama ve RST paketlerini kullanarak hello bağlantı kaldırılıyor.

#### <a name="points-tooconsider-before-choosing-hello-protocol"></a>Merhaba Protokolü işaretlemeden önce noktaları tooconsider
Bir protokol toouse seçmeden önce aşağıdaki bilgilerle hello göz önünde bulundurun:

##### <a name="discovering-multiple-network-routes"></a>Birden çok ağ yollarını keşfetme
Birden çok yol keşfederken TCP daha doğru olduğunu ve her alt ağda daha az aracıları gerekiyor. Örneğin, TCP kullanarak bir veya iki aracılarını alt ağlar arasındaki tüm yedekli yollar bulabilir. Ancak, ICMP tooachieve benzer sonuçlar kullanarak birkaç aracılarını gerekir. ICMP, varsa kullanarak *N* 5'ten fazla ihtiyacınız iki alt ağ arasındaki yolları sayısı*N* kaynak veya hedef alt ağdaki aracıları.

##### <a name="accuracy-of-results"></a>Sonuçları doğruluğunu
Yönlendiriciler ve anahtarlar tooassign daha düşük öncelik tooICMP YANKI karşılaştırıldığında paketleri tooTCP paketlerini eğilimi gösterir. Ağ aygıtlarını yoğun olarak yüklendiğinde, belirli durumlarda, TCP tarafından daha yakından alınan hello veriler hello kaybı ve gecikme uygulamalar tarafından yaşadı yansıtır. Bu hello uygulama trafiğini çoğunu akışlar için TCP üzerinden oluşur. Böyle durumlarda, daha az doğru sonuçlar karşılaştırıldığında tooTCP ICMP sağlar.

##### <a name="firewall-configuration"></a>Güvenlik duvarı yapılandırması
TCP protokol TCP paketleri tooa hedef bağlantı noktası gönderilir gerektirir. aracıları yapılandırdığınızda bu değiştirebilirsiniz ancak NPM aracıları tarafından kullanılan hello varsayılan bağlantı noktası 8084, ' dir. Bu nedenle, ağ güvenlik duvarları veya NSG kuralları (azure'da) hello bağlantı noktasındaki trafiğe izin tooensure gerekir. Toomake etmeniz bu hello yerel bilgisayarlarda güvenlik duvarı aracıları yüklendiği hello emin yapılandırılmış tooallow trafiği bu bağlantı noktasında.

Tooconfigure gerekiyor ancak PowerShell komut dosyaları tooconfigure güvenlik duvarı kuralları Windows çalıştıran bilgisayarlarınızda, ağ Güvenlik Duvarı'nı el ile kullanabilirsiniz.

Buna karşılık, ICMP bağlantı noktası kullanılarak çalışmaz. Çoğu Kurumsal senaryoda, toouse Ağ Tanılama araçları Ping yardımcı programı hello gibi hello güvenlik duvarları tooallow ICMP trafiğine izin verilir. Başka bir makineden Ping, bu nedenle, daha sonra hello ICMP Protokolü tooconfigure güvenlik duvarları el ile gerek kalmadan kullanabilirsiniz.

> [!NOTE]
> Hangi protokolü toouse emin olmayan olasılığına ICMP toostart ile seçin. Merhaba Sonuçlardan memnun değilseniz, tooTCP daha sonra her zaman geçiş yapabilirsiniz.


#### <a name="how-tooswitch-hello-protocol"></a>Nasıl tooswitch hello Protokolü

Dağıtım sırasında toouse ICMP seçerseniz, izleme kuralı hello varsayılan düzenleyerek herhangi bir zamanda tooTCP geçiş yapabilirsiniz.

##### <a name="tooedit-hello-default-monitoring-rule"></a>tooedit hello varsayılan izleme kuralı
1.  Çok gidin**ağ performansını** > **İzleyici** > **yapılandırma** > **İzleyici** ve ardından **varsayılan kuralı**.
2.  Toohello kaydırma **Protokolü** bölümünde ve toouse istediğiniz hello protokolü seçin.
3.  Tıklatın **kaydetmek** tooapply hello ayarı.

Merhaba varsayılan kural belirli bir protokol kullanıyor olsa bile, farklı bir protokol yeni kurallar oluşturabilirsiniz. Burada bazı hello kuralları ICMP kullanmak ve başka bir TCP kullandığı kuralları bir karışımını bile oluşturabilirsiniz.




## <a name="data-collection-details"></a>Veri toplama ayrıntıları
ICMP hello Protokolü toocollect kaybı ve gecikme bilgileri seçildiğinde TCP seçilen ICMP YANKI ICMP YANKI YANITI olduğunda ve Ağ Performansı İzleyicisi TCP Eşitlemeye SYNACK ACK el sıkışması paketleri kullanır. İzleme yolu da kullanılan tooget topoloji bilgilerdir.

Merhaba aşağıdaki tabloda veri toplama yöntemleri ve Ağ Performansı İzleyicisi için verileri nasıl toplanır ilgili diğer ayrıntıları gösterir.

| Platform | Doğrudan Aracısı | SCOM Aracısı | Azure Storage | SCOM gerekli? | Yönetim grubu gönderilen SCOM Aracısı verileri | Toplama sıklığı |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | &#8226; | &#8226; |  |  |  |Gönderilen TCP el sıkışmaları/ICMP YANKI iletileri 5 saniyede veri 3 dakikada bir |

Merhaba çözüm yapay işlemler tooassess hello hello ağ durumunu kullanır. Bir noktada çeşitli hello ağ exchange TCP paketleri veya ICMP Yankı (izleme için seçilen hello Protokolü) bağlı olarak birbirleriyle yüklü OMS aracılar. Merhaba işleminde aracıları varsa hello gidiş dönüş süresi ve paket kaybı öğrenin. Düzenli olarak, her bir aracının tüm test edilmelidir hello ağ çeşitli yollar hello bir izleme yolu tooother aracıları toofind gerçekleştirir. Bu verileri kullanarak hello aracıları hello ağ gecikme süresi ve paket kaybı rakamları türetme. Merhaba testler, her beş saniyede ve verileri toplanır üç dakika boyunca hello aracıları tarafından toohello günlük analizi hizmeti yüklemeden önce yinelenir.

> [!NOTE]
> Aracıları sık birbirleriyle iletişim olsa da, bunlar çok miktarda ağ trafiği hello testleri yürütürken oluşturmaz. Aracılar, yalnızca TCP Eşitlemeye SYNACK ACK el sıkışma paketleri toodetermine hello kaybı ve gecikme--paketler arasında alınıp verilen veri kullanır. Bu işlem sırasında aracılar birbiriyle yalnızca gerekli olduğunda iletişim ve hello aracı iletişim topolojisinin getirilmiştir tooreduce ağ trafiği.
>
>

## <a name="using-hello-solution"></a>Merhaba çözümünü kullanarak
Bu bölümde, tüm hello Pano işlevleri açıklanır ve nasıl toouse bunları.

### <a name="solution-overview-tile"></a>Çözüm genel bakış kutucuğu
Merhaba Ağ Performansı İzleyicisi çözüm etkinleştirdikten sonra hello çözüm kutucuğu hello OMS genel bakış sayfasında hello ağ durumunu hızlı bir genel bakış sağlar. Sağlıklı ve sağlıksız alt ağ bağlantıları hello sayısını gösteren bir halka grafiği görüntüler. Merhaba kutucuğa tıkladığınızda hello çözüm panosu açılır.

![Ağ Performans İzleyicisi kutucuğu](./media/log-analytics-network-performance-monitor/npm-tile.png)

### <a name="network-performance-monitor-solution-dashboard"></a>Ağ Performans İzleyicisi çözüm Panosu
Merhaba **ağ Özet** dikey penceresinde hello ağları göreli boyutlarına birlikte özetini gösterir. Bu, ağ bağlantıları, alt ağ bağlantıları ve yolları toplam sayısı (bir yolu aracıları ile iki ana ve aralarındaki tüm hello atlama hello IP adreslerini oluşur) hello sistemindeki gösteren döşeme tarafından izlenir.

Merhaba **üst ağ sistem durumu olayları** dikey bir listesi verilmiştir en son sistem durumu olayları ve Uyarıları hello sistem ve hello saat hello olay etkin edildiğinden. Merhaba paket kaybı veya bir ağ veya alt ağ bağlantısının gecikme eşiği aştığında bir sistem durumu olayı ya da uyarı oluşturulur.

Merhaba **üst sağlıksız ağ bağlantıları** dikey sağlıksız ağ bağlantıları listesini gösterir. Bir veya daha fazla olumsuz sistem durumu olayı kendileri için hello şu anda sahip hello ağ bağlantıları bunlar.

Merhaba **üst alt ağ bağlantıları en kaybı ile** ve **en gecikme süresi ile alt ağ bağlantıları** Kanatlar paket kaybı tarafından hello üst alt ağ bağlantıları göstermek ve alt ağ bağlantıları gecikmesine sırasıyla üst. Belirli ağ bağlantıları bekleniyordu yüksek gecikme veya miktar paket kaybı. Bu gibi bağlantılar hello üst on listelerinde görünür ancak sağlıksız olarak işaretlenmez.

Merhaba **genel sorgular** dikey ham ağ verileri doğrudan izleme fetch arama sorguları kümesi içerir. Özelleştirilmiş raporlama için kendi sorguları oluşturmak için bu sorguları bir başlangıç noktası olarak kullanabilirsiniz.

![Ağ Performans İzleyicisi Panosu](./media/log-analytics-network-performance-monitor/npm-dash01.png)

### <a name="drill-down-for-depth"></a>Derinliği için detayına gitme
Herhangi bir ilgi alanına hello çözüm Panosu toodrill aşağı daha derin çeşitli bağlantıları tıklatabilirsiniz. Örneğin, bir uyarı veya hello Panoda görünmesini bir sağlıksız ağ bağlantısı gördüğünüzde, daha fazla tooinvestigate tıklayabilirsiniz. Merhaba belirli ağ bağlantısı için tüm hello alt ağ bağlantıları listeler tooa sayfa alınması. Hangi alt ağ bağlantıları bulma hello sorunu neden hızla ve her alt ağ bağlantısının mümkün toosee hello kaybı, gecikme ve sistem durumu olacaktır. Daha sonra tıklatabilirsiniz **görüntülemek düğüm bağlantıları** toosee bağlantı hello sağlıksız alt ağ için tüm hello düğüm bağlantıları. Ardından, tek tek düğümü düğümü bağlantılara bakın ve hello sağlıksız düğüm bağlantıları bulun.

Tıklayabilirsiniz **görünüm topoloji** tooview hello atlama atlamalı topoloji hello kaynak ve hedef düğümleri arasında hello yolların. sağlıksız yollar hello veya hızlı bir şekilde hello sorun tooa belirli kısmı hello ağ belirleyebilir atlama kırmızı olarak gösterilir.

![Ayrıntıya veri](./media/log-analytics-network-performance-monitor/npm-drill.png)

### <a name="network-state-recorder"></a>Ağ durumu Kaydedicisi

Her görünüm, ağ durumu görüntüsünü belirli bir noktada zamanında görüntüler. Varsayılan olarak, hello en son durum gösterilir. Merhaba çubuğu hello sayfanın üst kısmındaki hello hello noktası hello durumu görüntülenmektedir zamanında gösterir. Merhaba çubuğunda tıklayarak geri zaman ve görünüm hello anlık görüntüsünü ağ durumu içinde toogo seçebilirsiniz **Eylemler**. Ayrıca, tooenable seçin veya hello en son durumunu görüntülerken herhangi bir sayfa için Otomatik yenilemeyi devre dışı bırakın.

![ağ durumu](./media/log-analytics-network-performance-monitor/network-state.png)

#### <a name="trend-charts"></a>Eğilim grafikleri
Her biri, düzeydeki ayrıntısına gitme hello eğilimini kaybı ve gecikme süresi bir ağ bağlantısının görebilirsiniz. Eğilim grafikleri de alt ağ ve düğüm bağlantıları için kullanılabilir. Merhaba grafik hello üstünde hello zamanı denetimi kullanarak hello grafik tooplot hello zaman aralığını değiştirebilirsiniz.

Eğilim grafikleri, geçmiş bir perspektif bir ağ bağlantısının hello performansını gösterir. Bazı ağ sorunları doğası gereği geçici ve sabit toocatch yalnızca hello geçerli durumunu hello ağ bakarak olacaktır. Sorunları hızla yüzey ve herkesin bildirimler önce yalnızca, bir sonraki bir noktada tooreappear kayboluyor olmasıdır. Bu sorunlar nedeniyle genellikle yüzeyini uygulama yanıt süresini, tüm uygulama bileşenleri toorun sorunsuz göründüğünde bile açıklanamayan artışlar olarak tür geçici sorunlar Ayrıca uygulama yöneticileri için zor olabilir.

Bu tür sorunlar, ağ gecikme veya paket kaybı ani bir depo olarak hello sorun nerede görüneceğini eğilim Grafiği bakarak kolayca algılayabilir.

![Eğilim grafiği](./media/log-analytics-network-performance-monitor/npm-trend.png)

#### <a name="hop-by-hop-topology-map"></a>atlama atlamalı topoloji Haritası
Ağ atlama atlamalı topoloji etkileşimli topoloji Haritası üzerinde iki düğüm arasında yolların hello Performans İzleyicisi'ni gösterir. Bir düğüm bağlantısını seçerek ve ardından hello topoloji Haritası görüntüleyebilirsiniz **görünüm topoloji**. Ayrıca, hello topoloji Haritası tıklatarak görüntüleyebileceğiniz **yolları** döşeme hello Panoda. Tıkladığınızda **yolları** kaynak ve hedef düğümleri hello sol panelindeki hello ve ardından tooselect sahip hello Panoda **çizmek** tooplot hello yollar hello iki düğüm arasında.

Merhaba topoloji Haritası kaç yollar iki düğüm arasında hello olan ve veri paketleri al ne yolları hello görüntüler. Ağ performans sorunları hello topoloji haritaya kırmızı işaretlenir. Hatalı ağ bağlantısı veya hatalı ağ aygıtı hello topoloji haritasında kırmızı renkli öğeler arayarak bulabilirsiniz.

Bir düğüm veya vurgulu hello topoloji haritasında tıklattığınızda, FQDN ve IP adresi gibi hello düğümü hello özelliklerini görürsünüz. IP adresidir atlamanın toosee'ı tıklatın. Merhaba daraltılabilir Eylem Bölmesi'nde hello filtreleri kullanarak belirli yollar toofilter seçebilirsiniz. Ve hello Ara atlama hello Eylem Bölmesi'nde hello kaydırıcıyı kullanarak gizleme tarafından hello ağ topolojileri basitleştirebilirsiniz. Yakınlaştırma veya için fare tekerleği kullanarak hello topoloji haritasını out.

Merhaba eşlemesinde gösterilen bu hello topolojisi Katman 3 topolojisi ve Katman 2 aygıtlarını ve bağlantıları içermiyor unutmayın.

![atlama atlamalı topoloji Haritası](./media/log-analytics-network-performance-monitor/npm-topology.png)

#### <a name="fault-localization"></a>Hataya yerelleştirme
Ağ Performansı İzleyicisi toohello ağ aygıtlarını bağlanmadan mümkün toofind hello ağ performans sorunlarını ' dir. Merhaba ağdan ve gelişmiş algoritmalar hello ağ grafikte uygulayarak toplayan hello veri bağlı olarak, Ağ Performansı İzleyicisi Merhaba hello sorun büyük olasılıkla hello kaynağı olan ağ bölümlerini probabilistic tahmin yapar.

Yönlendiriciler veya anahtarlar gibi hello ağ aygıtlardan toplanan hiçbir veri toobe gerektirmediğinden erişim toohops kullanılabilir olmadığı durumlarda bu kullanışlı toodetermine hello ağ performans sorunlarını yaklaşımdır. Bu da iki düğüm arasında Hello atlamanın yönetimsel denetiminde olmadığında yararlıdır. Örneğin, hello atlama ISS yönlendiriciler olabilir.

### <a name="log-analytics-search"></a>Günlük analizi arama
Grafik hello Ağ Performansı İzleyicisi panoyu ve ayrıntıya sayfaları sunulan tüm verileri de yerel olarak günlük analizi aramada mevcut değil. Merhaba arama sorgu dili kullanarak hello verileri sorgulamak ve hello veri tooExcel veya Powerbı vererek özel raporlar oluşturun. Merhaba **genel sorgular** dikey penceresinde hello Pano sahip olarak hello başlangıç noktası kendi sorgular ve raporlar oluşturmak için kullanabileceğiniz bazı yararlı sorgular.

![arama sorguları](./media/log-analytics-network-performance-monitor/npm-queries.png)

## <a name="investigate-hello-root-cause-of-a-health-alert"></a>Sistem durumu uyarı Hello kök nedeni araştırın
Ağ Performansı İzleyicisi hakkında okuduğunuza göre hello nedenin sistem durumu olayı için basit bir araştırmasını bakalım.

1. Merhaba genel bakış sayfasında hello izlenerek ağınızın hello durumunu hızlı bir anlık görüntü alırsınız **Ağ Performansı İzleyicisi** döşeme. Merhaba 6 ağlarla dışında izlenmekte olan bağlantılar dikkat edin, 2 kötü durumda. Bu araştırma gerektirir. Merhaba döşeme tooview hello çözüm panosu'ı tıklatın.  
   ![Ağ Performans İzleyicisi kutucuğu](./media/log-analytics-network-performance-monitor/npm-investigation01.png)
2. Merhaba örnek resimde, düzgün çalışmayan bir ağ bağlantısı bir sistem durumu olayı olduğunu fark edeceksiniz. Tooinvestigate hello sorunu karar verin ve üzerinde hello tıklatın **DMZ2 DMZ1** hello sorun hello kökündeki giden ağ bağlantısı toofind.  
   ![sağlıksız ağ bağlantısı örneği](./media/log-analytics-network-performance-monitor/npm-investigation02.png)
3. Merhaba ayrıntıya sayfası gösterir tüm hello alt ağ bağlantıları **DMZ2 DMZ1** ağ bağlantısı. Her iki hello alt ağ bağlantıları için hello ağ bağlantısı bozan hello eşik hello gecikme taşını fark edeceksiniz. Her iki hello alt ağ bağlantıları hello gecikme eğilimleri de görebilirsiniz. Zaman aralığı hello grafik toofocus seçimi denetiminde hello üzerinde gerekli hello süresi kullanabilirsiniz. Merhaba saati, en yüksek gecikme ulaşıldığında hello görebilirsiniz. Daha sonra hello günlükler bu zaman dönem tooinvestigate hello sorun için arama yapabilirsiniz. Tıklatın **görüntülemek düğüm bağlantıları** daha fazla toodrill aşağı.  
   ![sağlıksız alt ağ bağlantıları örneği](./media/log-analytics-network-performance-monitor/npm-investigation03.png)
4. Benzer toohello önceki sayfaya, onun bağlı düğüm bağlantıları hello ayrıntıya sayfa hello belirli alt ağ bağlantısı için listeler. Benzer eylemleri gerçekleştirebilirsiniz hello önceki adımda yaptığınız gibi burada. Tıklatın **görünüm topoloji** tooview hello topoloji hello 2 düğümler arasında.  
   ![sağlıksız düğüm bağlantıları örneği](./media/log-analytics-network-performance-monitor/npm-investigation04.png)
5. Seçili hello 2 düğümler arasındaki tüm hello yolları hello topoloji haritasında çizilir. Merhaba atlama atlamalı topoloji hello topoloji Haritası üzerinde iki düğüm arasında yolların görselleştirebilirsiniz. Kaç tane yollar hello iki düğüm arasında mevcut NET bir resim sunar ve veri paketlerinin ne yolları hello yapmakta. Ağ performans sorunları kırmızı renk işaretlenir. Hatalı ağ bağlantısı veya hatalı ağ aygıtı hello topoloji haritasında kırmızı renkli öğeler arayarak bulabilirsiniz.  
   ![sağlıksız topoloji görünümü örneği](./media/log-analytics-network-performance-monitor/npm-investigation05.png)
6. Merhaba kaybı, gecikme ve her yolundaki atlama sayısı hello hello gözden **eylemi** bölmesi. Merhaba scrollbar tooview hello sağlıksız bu yollar ayrıntılarını kullanın.  Kullanım hello filtreleri tooselect hello yollarını hello sağlıksız atlama ile böylece yalnızca hello hello topolojisini seçili yolları çizilir. İçinde veya dışında hello topoloji Haritası fare tekerleği toozoom kullanabilirsiniz.

   Görüntü aşağıda hello içinde açıkça görebilirsiniz hello yolları ve kırmızı renk atlama bakarak nedenin bölümünün hello sorun alanlarını toohello belirli hello ağ hello. Merhaba topoloji Haritası düğümünde tıklayarak hello FQDN ve IP adresi gibi hello düğümünün hello özellikleri gösterir. Atlama tıklatarak hello atlamanın IP adresi hello gösterir.  
   ![sağlıksız topolojisi - yolu örnek ayrıntıları](./media/log-analytics-network-performance-monitor/npm-investigation06.png)

## <a name="provide-feedback"></a>Geri bildirimde bulunma

- **UserVoice** -fikirlerinizi bize toowork üzerinde istediğiniz ağ performansı İzleyicisi özellikleri için nakledebilirsiniz. Ziyaret bizim [UserVoice sayfa](https://feedback.azure.com/forums/267889-log-analytics/category/188146-network-monitoring).
- **Bizim kohort katılma** -her zaman yeni müşteriler bizim kohort katılma elde etmeyle ilgilenen çalışıyoruz. Bunun bir parçası olarak toonew özellikleri erken erişim edinmek ve ağ Performans İzleyicisi'ni iyileştirmemize yardımcı olun. Bağlama düşünüyorsanız dolgu bu genişletme [hızlı anket](https://aka.ms/npmcohort).

## <a name="next-steps"></a>Sonraki adımlar
* [Arama günlüklerini](log-analytics-log-searches.md) tooview ayrıntılı ağ performans verilerini kaydeder.
