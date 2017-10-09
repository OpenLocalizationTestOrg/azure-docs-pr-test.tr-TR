---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: True
ROBOTS: NOINDEX
ms.openlocfilehash: 8b526144cd565f6750368e12970f008e66cc2023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toolog-analytics"></a>Linux bilgisayarları tooLog Analytics Bağlan
Günlük analizi kullanarak toplamak ve Linux bilgisayarları oluşturulan veri hareket. Linux tooOMS ' toplanan verileri eklemeye izin verir, toomanage Linux sistemleri ve nerede olursa olsun bilgisayarlarınızı kapsayıcı çözümleri Docker gibi — neredeyse her yerden. Veri kaynakları, fiziksel sunucuları, Amazon Web Hizmetleri (AWS) veya Microsoft Azure gibi bir bulutta barındırılan hizmetindeki sanal bilgisayarlar olarak, şirket içi veri merkezinizde bulunabilir veya bile dizüstü masanıza hello. Gerçekten karma BT ortamında destekler şekilde ek olarak, OMS ayrıca Windows bilgisayarlardan benzer şekilde, toplar.

Görüntüleme ve tüm OMS günlük analizi ile bu kaynakları tek bir Yönetim Portalı ile verileri yönetme. Bu hello ihtiyacını azaltır toomonitor birçok farklı sistemleri kullanarak kılar kolay tooconsume ve sahip olduğunuz toowhatever iş analiz çözümü veya sistem gibi herhangi bir veriyi dışa aktarabilirsiniz.

Bu makalede toplamak ve Linux için OMS aracısının hello kullanarak, Linux bilgisayarların verilerini yönetmenize yardımcı olacak bir Hızlı Başlangıç Kılavuzu ' dir. Proxy sunucu yapılandırması, CollectD ölçümleri ve özel JSON veri kaynakları hakkında bilgi gibi daha fazla teknik bilgi için bu bilgileri bulabilirsiniz [Linux genel bakış için OMS Aracısı](https://github.com/Microsoft/OMS-Agent-for-Linux) ve [Linux için OMS Aracısı tam belgelerine](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) github'da.

Şu anda veri türleri Linux bilgisayarları izleyen hello toplayabilirsiniz:

* Performans ölçümleri
* Syslog olayları
* Nagios ve Zabbix uyarıları
* Docker kapsayıcısı performans ölçümleri, Envanter ve günlükleri

## <a name="supported-linux-versions"></a>Desteklenen Linux sürümleri
Hem x86 hem x64 sürümleri Linux dağıtımları çeşitli resmi olarak desteklenir. Ancak, hello OMS Aracısı Linux için listelenmeyen diğer dağıtımlar da çalıştırabilirsiniz.

* Amazon Linux 2015.09 aracılığıyla 2012.09
* CentOS Linux 5, 6 ve 7
* Oracle Linux 5, 6 ve 7
* Red Hat Enterprise Linux Server 5, 6 ve 7
* Debian GNU/Linux 6, 7 ve 8
* Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10
* SUSE Linux Enterprise Server 11 ve 12

## <a name="oms-agent-for-linux"></a>Linux için OMS Aracısı
Merhaba Linux için Operations Management Suite Aracısı birden çok paket oluşur. Merhaba yayın dosyasını içeren paketler, çalışan hello Kabuk Paketle tarafından kullanılabilen aşağıdaki hello `--extract`.

| **Paket** | **Sürüm** | **Açıklama** |
| --- | --- | --- |
| omsagent |1.1.0 |Merhaba Linux için Operations Management Suite Aracısı |
| omsconfig |1.1.1 |Merhaba OMS aracısı için yapılandırma aracısı |
| OMI |1.0.8.3 |Açık Yönetim Altyapısı (OMI)--bir basit CIM sunucusu |
| scx |1.6.2 |İşletim sistemi performans ölçümleri için OMI CIM sağlayıcıları |
| Apache cimprov |1.0.0 |Apache HTTP Server performansı sağlayıcısı OMI için izleme. Apache HTTP Server algılanırsa, yalnızca yüklü. |
| MySQL cimprov |1.0.0 |MySQL sunucusu performans sağlayıcısı OMI için izleme. MySQL/MariaDB sunucu algılanırsa, yalnızca yüklü. |
| docker cimprov |0.1.0 |OMI docker sağlayıcısı. Docker algılanırsa, yalnızca yüklü. |

### <a name="additional-installation-artifacts"></a>Ek yükleme yapıları
Linux paketler için Hello OMS Aracısı yüklendikten sonra hello aşağıdaki ek sistem genelinde yapılandırma değişiklikleri uygulanır. Bu yapıtların Hello omsagent paket kaldırıldığında kaldırılır.

* Adlı bir ayrıcalıklı olmayan kullanıcı: `omsagent` oluşturulur. Merhaba hesap hello omsagent arka plan programı çalışırken budur
* "Ekle" sudoers dosyası oluşturulur omsagent toorestart hello syslog ve omsagent deamon'lar /etc/sudoers.d/omsagent bu yetkilendirir. Sudo "Ekle" yönergeleri sudo yüklü hello sürümünde desteklenmez, bu girişler çok/etc/sudoers yazılır.
* Değiştirilen tooforward olayları toohello Aracısı'nın bir alt Hello syslog yapılandırmadır. Merhaba daha fazla bilgi için bkz: **yapılandırma veri toplama** bölümüne bakın

### <a name="linux-data-collection-details"></a>Linux veri toplama ayrıntıları
Merhaba aşağıdaki tabloda veri toplama yöntemleri ve verileri nasıl toplanır ilgili diğer ayrıntıları gösterir.

| Kaynak | Doğrudan Aracısı | SCOM Aracısı | Azure Storage | SCOM gerekli? | Yönetim grubu gönderilen SCOM Aracısı verileri | Toplama sıklığı |
| --- | --- | --- | --- | --- | --- | --- |
| Zabbix |![Evet](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |1 dakika |
| Nagios |![Evet](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |geldiğinde |
| syslog |![Evet](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |Azure depolama biriminden: 10 dakika; aracısından: işle |
| Linux performans sayaçları |![Evet](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |Zamanlandığı gibi en az 10 saniye |
| değişiklik izleme |![Evet](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Hayır](./media/log-analytics-linux-agents/oms-bullet-red.png) |saatlik |

### <a name="package-requirements"></a>Paket gereksinimleri
| **Gerekli paket** | **Açıklama** | **En düşük sürüm** |
| --- | --- | --- |
| Glibc |GNU C Kitaplığı |2.5-12 |
| Openssl |OpenSSL kitaplıkları |0.9.8E veya 1.0 |
| Curl |cURL web istemcisi |7.15.5 |
| Python ctypes |işlev kitaplıkları |yok |
| PAM |Eklenebilir kimlik doğrulaması modülleri |yok |

> [!NOTE]
> Rsyslog veya syslog ng gerekli toocollect syslog iletileri şunlardır. Red Hat Enterprise Linux, CentOS ve Oracle Linux sürümü (sysklog) 5 sürümünü Hello varsayılan syslog arka plan syslog olay toplaması için desteklenmiyor. Bu sürümü bu dağıtımları toocollect syslog verileri hello rsyslog arka plan programı yüklenmelidir ve tooreplace sysklog yapılandırılır.
>
>

## <a name="quick-install"></a>Hızlı yükleme
Aşağıdaki komutları toodownload hello omsagent hello çalıştırın, hello sağlama toplamı, sonra Yükle ve yerleşik hello Aracısı doğrulayın. 64 bit için komutlardır. Merhaba çalışma alanı kimliği ve birincil anahtar hello OMS portalında altında bulunan **ayarları** hello üzerinde **bağlı kaynakları** sekmesi.

![çalışma alanı ayrıntıları](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

Diğer yöntemleri tooinstall çeşitli vardır hello aracısı ve bunu yükseltin. Daha fazla bilgiyi onları hakkında [adımları tooinstall hello Linux için OMS aracısının](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).

Merhaba de görüntüleyebilirsiniz [Azure videosu](https://www.youtube.com/watch?v=mF1wtHPEzT0).

## <a name="choose-your-linux-data-collection-method"></a>Linux veri toplama yönteminizi seçin
Nasıl hello toouse hello OMS portalı isteyip istemediğinizi toocollect bağlıdır gibi ya da Linux istemcileri doğrudan üzerinde çeşitli yapılandırma dosyalarını düzenlemek istiyorsanız yaptığınız veri türlerini seçin. Merhaba yapılandırma toouse hello portal seçerseniz, Linux istemcilerinizin tooall otomatik olarak gönderilir. Farklı Linux istemcileri için farklı yapılandırmaları gerekiyorsa, bunu tooedit istemci dosyalarını ayrı ayrı – gerekir veya alternatif PowerShell DSC, Chef veya Puppet gibi kullanabilirsiniz.

Merhaba Linux bilgisayarlarda yapılandırma dosyalarını kullanarak toocollect istediğiniz performans sayaçları ve hello syslog olayları belirtebilirsiniz. *Tooconfigure veri toplama Aracısı Yapılandırma dosyalarını düzenleyerek seçerseniz, hello Merkezi yapılandırma devre dışı bırakmanız gerekir.*  Yönergeler tooconfigure veri koleksiyonunda hello aracısının yapılandırma dosyalarının yanı sıra toodisable Linux ya da ayrı bilgisayarlar için tüm OMS aracılar için merkezi yapılandırma aşağıda verilmiştir.

### <a name="disable-oms-management-for-an-individual-linux-computer"></a>Tek bir Linux bilgisayar için OMS yönetimi devre dışı
Yapılandırma verileri için merkezi veri toplama hello OMS_MetaConfigHelper.py betik ile tek bir Linux bilgisayarı devre dışı bırakılmıştır. Bu, bilgisayarların alt ağlarından özel bir yapılandırmanız varsa yararlı olabilir.

toodisable Merkezi yapılandırma:

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

Merkezi yapılandırma toore etkinleştir:

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a>Linux performans sayaçları
Linux performans sayaçları olan benzer tooWindows performans sayaçları — her ikisi de aynı şekilde çalışır. Aşağıdaki yordamlar tooadd hello kullanın ve bunları yapılandırın. Verileri tooOMS eklendikten sonra bunlar için her 30 saniyede toplanır.

### <a name="tooadd-a-linux-performance-counter-in-oms"></a>tooadd OMS Linux performans sayacında
1. tooconfigure hello OMS portalı kullanarak Linux için OMS aracıları, Linux performans sayaçlarını ekleme yapabilir hello Ayarları sayfasında, tıklatın **veri**.  
2. Merhaba üzerinde **ayarları** altında sayfa **veri** , tıklatın **Linux performans sayaçları** ve ardından seçin ya da türü hello adı tooadd istediğiniz hello sayacını da.  
    ![veri](./media/log-analytics-linux-agents/oms-settings-data01.png)
3. Merhaba tam hello sayacının adını bilmiyorsanız, kısmi bir ad yazarak başlatabilirsiniz ve kullanılabilir sayaçlarının listesi görüntülenir. Merhaba sayaç bulduğunuzda, tooadd, hello listesinde hello adına tıklayın ve ardından hello artı simgesine tooadd hello sayacı.
4. Merhaba sayaç ekledikten sonra hello renkli çubuk ile vurgulanan sayaçlarının listesi görüntülenir.
5. Varsayılan olarak, hello **aşağıdaki yapılandırma toomy makineler Uygula** seçeneği işaretlidir. Yapılandırma verileri gönderme toodisable istiyorsanız hello seçimi temizleyin.
6. Merhaba sayfanın hello sonundaki değiştirme performans sayaçları bittiğinde tıklatın **kaydetmek** toofinalize değişikliklerinizi. yapmış olduğunuz hello yapılandırma değişiklikleri, OMS ile genellikle 5 dakika içinde kayıtlı Linux tooall hello OMS Aracısı sonra gönderilir.

### <a name="configure-linux-performance-counters-in-oms"></a>Linux performans sayaçları OMS yapılandırın
Windows performans sayaçları için her performans sayacı için belirli bir örneği seçebilirsiniz. Ancak, Linux performans sayaçlarını tooall alt sayaçları hello üst sayacının ne olursa olsun, seçtiğiniz bir sayaç örneği geçerlidir. Merhaba aşağıdaki tabloda hello ortak örnekleri kullanılabilir tooboth Linux ve Windows performans sayaçlarını gösterir.

| **Örnek adı** | **Anlamı** |
| --- | --- |
| \_Toplam |Tüm hello örnekleri toplamı |
| \* |Tüm örnekleri |
| (/ &#124; / var) |Eşleşen adlandırılmış örnekleri: / veya /var |

Benzer şekilde, seçtiğiniz bir üst sayacının hello örnekleme aralığı, alt sayaçlarını tooall geçerlidir. Diğer bir deyişle, tüm hello alt sayacı örnek aralıklar ve örnekleri birbirine bağlıdır.

### <a name="add-and-configure-performance-metrics-with-linux"></a>Ekleme ve performans ölçümleri Linux ile yapılandırma
Performans ölçümleri toocollect hello yapılandırma içinde/etc/opt/microsoft/omsagent tarafından denetlenen/&lt;çalışma alanı kimliği&gt;/conf/omsagent.conf. Bkz: [kullanılabilir performans ölçümleri](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) kullanılabilir sınıfların ve hello Linux için OMS aracısı için ölçümleri.

Tek bir olarak hello yapılandırma dosyasındaki her nesne veya kategorisi, performans ölçümleri toocollect tanımlanmalıdır `<source>` öğesi. Merhaba sözdizimi aşağıdaki hello deseni izler.

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

Bu öğenin Hello yapılandırılabilir Parametreler şunlardır:

* **Nesne\_adı**: hello koleksiyonu için hello nesne adı.
* **Örnek\_regex**: bir *normal ifade* hangi örnekleri toocollect tanımlama. Merhaba değeri: `.*` tüm örneklerini belirtir. yalnızca hello için toocollect işlemci ölçümleri \_toplam örneğini belirtmek `_Total`. toocollect işlem ölçümlerini yalnızca hello crond veya sshd örneği, belirtebilirsiniz: `(crond|sshd)`.
* **Sayaç\_adı\_regex**: bir *normal ifade* hangi (Merhaba nesnesi) sayaçları toocollect tanımlama. Merhaba nesnesi için tüm sayaçlar toocollect belirtin: `.*`. toocollect hello bellek nesnesi için yalnızca alanı sayaçları değiştirme, belirtebilirsiniz:`.+Swap.+`
* **Aralığı:**: Merhaba sıklığı hangi hello nesnesinin sayaçları toplanır.

Performans ölçümleri Hello varsayılan yapılandırmasını şöyledir:

```
<source>
  type oms_omi
  object_name "Physical Disk"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Logical Disk"
  instance_regex ".*
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Processor"
  instance_regex ".*
  counter_name_regex ".*"
  interval 30s
</source>

<source>
  type oms_omi
  object_name "Memory"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

### <a name="enable-mysql-performance-counters-using-linux-commands"></a>MySQL performans sayaçlarını Linux komutlarını kullanarak etkinleştirme
Hello omsagent paketi yüklendiğinde, MySQL Server veya MariaDB Server hello bilgisayarında algılanırsa, bir performans izleme sağlayıcısı MySQL sunucusu için otomatik olarak yüklenir. Bu sağlayıcı toohello yerel MySQL/MariaDB sunucu tooexpose performans istatistikleri bağlanır. Merhaba sağlayıcısı hello MySQL Server erişebilmesi için tooconfigure MySQL kullanıcı kimlik bilgileri gerekir.

toodefine varsayılan kullanıcı hello MySQL sunucusu için aşağıdaki komutu örneğine kullanım hello localhost üzerinde hesap.

> [!NOTE]
> Merhaba kimlik bilgileri dosyası hello omsagent hesabı tarafından okunabilir olması gerekir. Omsgent Hello mycimprovauth komutunun çalıştırılması önerilir.
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


Alternatif olarak, hello hello dosya oluşturarak bir dosyada MySQL kimlik bilgileri gerekli belirtebilirsiniz: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. Merhaba mysql auth dosyası aracılığıyla izleme MySQL kimlik bilgilerini yönetme hakkında daha fazla bilgi için bkz: [hello authentication dosyasındaki kimlik bilgilerini izleme MySQL yönetmek](#manage-mysql-monitoring-credentials-in-the-authentication-file).

Bkz: [veritabanı için MySQL performans sayaçları gerekli izinler](#database-permissions-required-for-mysql-performance-counters) hello MySQL kullanıcı toocollect MySQL sunucu performans verisi gerekli nesne izinler hakkında ayrıntılı bilgi için.

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a>Linux komutlarını kullanarak Apache HTTP Server performans sayaçları sağlar
Hello omsagent paketi yüklendiğinde, Apache HTTP Server hello bilgisayarında algılanırsa, bir performans izlemesi için Apache HTTP Server sağlayıcısı otomatik olarak yüklenir. Bu sağlayıcı bir Apache "Merhaba Apache HTTP Server sipariş tooaccess performans verilerindeki içine yüklenmesi gereken modül" kullanır.

Merhaba modülü komutu aşağıdaki hello ile yükleyebilirsiniz:

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

komutu aşağıdaki hello çalıştırmak toounload hello Apache izleme Modülü'nü:

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="tooview-performance-data-with-log-analytics"></a>Günlük analizi ile tooview performans verileri
1. Merhaba Operations Management Suite Portalı'nda hello günlük arama kutucuğuna tıklayın.
2. Merhaba Arama çubuğuna `* (Type=Perf)` tooview tüm performans sayaçları.

OMS aynı zamanda Windows performans sayacı verilerini toplar olduğundan, kapsam aşağı hello arama tooLinux özgü verileri. Bu nedenle, hello aşağıdaki örnek performans veri belirli tooan Örnek Linux sunucusu Chorizo21 adlı gösterir.

```
Type=Perf Computer=chorizo*
```

![arama sonuçlarında gösterilen örnekte, sunucu](./media/log-analytics-linux-agents/oms-perfsearch01.png)

Merhaba sonuçlarında tıklayabilirsiniz **ölçümleri** veri için toplanan tooview hello sayaçları. Gerçek zamanlı veri grafikleri her sayacı olarak gösterilir.

![metrics](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a>Syslog
Syslog olan bir olay günlüğü Protokolü benzer tooWindows olay günlükleri — hem OMS görüntülendiğinde benzer şekilde çalışır.

### <a name="tooadd-a-new-linux-syslog-facility-in-oms"></a>tooadd OMS yeni bir Linux syslog yerde
1. Merhaba üzerinde **ayarları** altında sayfa **veri** , tıklatın **Syslog** ve toohello sol hello artı simgesine yazın tooadd istediğiniz hello syslog özelliğini hello adı.
    ![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)
2. Merhaba tesis hello tam adını bilmiyorsanız, kısmi bir ad yazarak başlatabilirsiniz ve kullanılabilir syslog tesis listesi görüntülenir. Bul zaman, tooadd istediğiniz, hello listesinde hello adını tıklatın ve sonra hello artı simgesine tooadd hello hello syslog özelliğini syslog özelliğini.
3. Merhaba listesinde görüntülenir hello tesis ekledikten sonra renkli çubuk ile vurgulanır. Ardından, hello önem derecelerinin (syslog tesis bilgi kategorilerde) seçin toocollect istiyor.
4. Merhaba hello sayfa sonunda tıklatın **kaydetmek** toofinalize değişikliklerinizi. yapmış olduğunuz hello yapılandırma değişiklikleri, OMS ile genellikle 5 dakika içinde kayıtlı Linux tooall hello OMS Aracısı sonra gönderilir.

### <a name="configure-linux-syslog-facilities-in-linux"></a>Linux syslog Linux tesislerde yapılandırın
Syslog olayları hello syslog arka plan programından gönderilir, örneğin rsyslog veya syslog ng, tooa yerel bağlantı noktası, hello aracısının dinlediği. Varsayılan olarak, bağlantı noktası 25224. Merhaba Aracısı yüklendiğinde, varsayılan bir syslog yapılandırma uygulanır. Bu da bulunur:

Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf

Syslog ng: /etc/syslog-ng/syslog-ng.conf

Merhaba varsayılan OMS Aracısı syslog yapılandırması tüm uyarı veya daha büyük bir önem derecesi araçlarıyla syslog olayları yükler.

> [!NOTE]
> Merhaba syslog yapılandırma düzenlerseniz, hello değişiklikleri tootake etkisi hello syslog arka plan yeniden başlatmanız gerekir.
>
>

Merhaba syslog için varsayılan yapılandırmayı hello OMS aracısı için Linux için OMS şöyledir:

#### <a name="rsyslog"></a>rsyslog
```
kern.warning       @127.0.0.1:25224
user.warning       @127.0.0.1:25224
daemon.warning     @127.0.0.1:25224
auth.warning       @127.0.0.1:25224
syslog.warning     @127.0.0.1:25224
uucp.warning       @127.0.0.1:25224
authpriv.warning   @127.0.0.1:25224
ftp.warning        @127.0.0.1:25224
cron.warning       @127.0.0.1:25224
local0.warning     @127.0.0.1:25224
local1.warning     @127.0.0.1:25224
local2.warning     @127.0.0.1:25224
local3.warning     @127.0.0.1:25224
local4.warning     @127.0.0.1:25224
local5.warning     @127.0.0.1:25224
local6.warning     @127.0.0.1:25224
local7.warning     @127.0.0.1:25224
```

#### <a name="syslog-ng"></a>Syslog ng
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="tooview-all-syslog-events-with-log-analytics"></a>tooview günlük analizi ile tüm Syslog olayları
1. Merhaba Hello Operations Management Suite Portalı'nda tıklatın **günlük arama** döşeme.
2. Merhaba, **Günlüğü Yönetimi** gruplandırma, önceden tanımlanmış syslog arama seçin ve ardından bir toorun seçin.

Bu örnekte tüm Syslog olayları gösterir.

![Günlük aramada gösterilen Syslog olayları](./media/log-analytics-linux-agents/oms-linux-syslog.png)

Şimdi arama sonuçlarında detaya inebilirsiniz.

## <a name="linux-alerts"></a>Linux uyarıları
Nagios veya Zabbix toomanage kullanırsanız, Linux makineler sonra OMS bu Araçları'ndan oluşturulan hello uyarıları alabilirsiniz. Ancak, hello OMS portalı kullanarak şu anda yöntemi tooconfigure gelen uyarı verisi yok. Bunun yerine, bir yapılandırma dosyası toostart gönderen uyarılar tooOMS tooedit gerekir.

### <a name="collect-alerts-from-nagios"></a>Nagios toplama uyarıları
Nagios sunucusundan toocollect uyarıları, aşağıdaki yapılandırma değişiklikler toomake hello gerekir.

1. GRANT hello kullanıcı **omsagent** okuma erişimi toohello Nagios günlük dosyası (yani /var/log/nagios/nagios.log). Merhaba nagios.log dosya hello grupla ait olduğu varsayılarak **nagios** , hello kullanıcı ekleyebilir **omsagent** toohello **nagios** grubu.

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. Merhaba omsagent.confconfiguration dosyasını değiştirme (/ etc/opt/microsoft/omsagent/&lt;çalışma alanı kimliği&gt;/conf/omsagent.conf). Mevcut ve kullanıma açıklamalı girişleri aşağıdaki hello çalıştığından emin olun:

    ```
    <source>
    type tail
    #Update path toopoint tooyour nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. Merhaba omsagent arka plan programı yeniden başlatın:

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a>Zabbix toplama uyarıları
toocollect, gerçekleştireceğiniz benzer adımları toothose Nagios yukarıdaki toospecify bir kullanıcı ve parola gerekir dışında bir Zabbix sunucusundan uyarıları *açık metin*. Bu ideal olmayan, ancak büyük olasılıkla yakında değiştirir. tooaddress bu sorunu hello kullanıcı oluşturun ve yalnızca izin toomonitor vermek öneririz.

Bir örnek bölüm hello omsagent.conf yapılandırma dosyasının (/ etc/opt/microsoft/omsagent/&lt;çalışma alanı kimliği&gt;/conf/omsagent.conf) Zabbix hello aşağıdaki benzemelidir için:

```
<source>
  type zabbix_alerts
  run_interval 1m
  tag oms.zabbix
  zabbix_url http://localhost/zabbix/api_jsonrpc.php
  zabbix_username Admin
  zabbix_password zabbix
</source>

```

### <a name="view-alerts-in-log-analytics-search"></a>Günlük analizi arama uyarıları görüntüle
Linux bilgisayarları toosend uyarıları tooOMS yapılandırdıktan sonra birkaç basit günlük arama sorguları tooview hello uyarıları kullanabilirsiniz. Merhaba aşağıdaki arama sorgusu örneğinde oluşturulan tüm kayıtlı hello uyarıların döndürür. Örneğin, BT altyapınızın sorun çeşit meydana gelirse, ardından aşağıdaki sorgu hello sorun nerede kaynaklanan gösterebilir örneğine Merhaba sonuçlanır. Ve, kolayca toohello uyarılar kaynak sistem toohelp tarafından dar araştırmanızı inebilir. Merhaba hello başından toogo toovarious yönetim sistemleri mutlaka yok avantajdır — uyarılarınızı tooOMS gönderilen koşuluyla var. başlatabilirsiniz.

```
Type=Alert
```

#### <a name="tooview-all-nagios-alerts-with-log-analytics"></a>Tüm Nagios uyarıları günlük analizi ile tooview
1. Merhaba Hello Operations Management Suite Portalı'nda tıklatın **günlük arama** döşeme.
2. Arama sorgusu aşağıdaki hello Hello sorgu çubuğuna yazın

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Günlük aramada gösterilen Nagios uyarıları](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

Merhaba arama sonuçlarını sonra ek ayrıntılar gibi inebilir *AlertState*.

### <a name="tooview-all-zabbix-alerts-with-log-analytics"></a>tooview günlük analizi ile tüm Zabbix uyarıları
1. Merhaba Hello Operations Management Suite Portalı'nda tıklatın **günlük arama** döşeme.
2. Arama sorgusu aşağıdaki hello Hello sorgu çubuğuna yazın

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Günlük aramada gösterilen Zabbix uyarıları](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

Merhaba arama sonuçlarını sonra ek ayrıntılar gibi inebilir *AlertName*.

## <a name="compatibility-with-system-center-operations-manager"></a>System Center Operations Manager ile uyumluluk
Merhaba OMS Aracısı Linux Aracısı ikili dosyalarının hello System Center Operations Manager Aracısı ile paylaşır. Linux için şu anda Operations Manager tarafından yönetilen bir sistemi Hello OMS Aracısı yüklenmesi yükseltmeler hello bilgisayar tooa daha yeni sürümü OMI ve SCX paketleri hello. Merhaba Linux ve System Center 2012 R2 için OMS aracısının uyumlu. Ancak, **System Center 2012 SP1 ve önceki sürümleri olmayan şu anda desteklenen veya uyumlu hello Linux için OMS Aracısı ile.**

> [!NOTE]
> Merhaba bilgisayarını Bul önce hello OMS Aracısı Linux için Operations Manager tarafından yönetilen değil yüklü tooa bilgisayardır ve daha sonra toomanage hello bilgisayar Operations Manager ile istiyorsanız hello OMI yapılandırma değiştirmeniz gerekir. **Linux için OMS Aracısı hello önce Hello Operations Manager Aracısı yüklüyse, bu adım gerekli değildir.**
>
>

### <a name="tooenable-hello-oms-agent-for-linux-toocommunicate-with-operations-manager"></a>Operations Manager ile Linux toocommunicate tooenable Merhaba OMS Aracısı
1. Merhaba dosya /etc/opt/omi/conf/omiserver.conf Düzenle
2. Bu hello satır başlayarak olun **httpsport =** hello bağlantı noktası 1270 tanımlar. Gibi`httpsport=1270`
3. Merhaba OMI sunucuyu yeniden başlatın:

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a>MySQL performans sayaçları için gereken veritabanı izinleri
toogrant izinlerini tooa MySQL izleme kullanıcıya, hello izni veriliyor kullanıcı verilmeden hello ayrıcalık yanı sıra hello 'GRANT option' ayrıcalığına sahip olmalıdır.

Merhaba MySQL kullanıcı için sırayla tooreturn performans verileri hello kullanıcı sorguları aşağıdaki toohello erişecek:

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

Ayrıca toothese sorguları hello MySQL kullanıcı varsayılan tabloları aşağıdaki SELECT erişim toohello gerektirir:

* INFORMATION_SCHEMA
* MySQL

Bu ayrıcalıkları verme komutları aşağıdaki hello çalıştırarak verilebilir.

```
GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
GRANT SELECT ON mysql.* too‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-hello-authentication-file"></a>Kimlik bilgileri hello authentication dosyasındaki İzleme MySQL yönetme
MySQL kimlik bilgilerini yönetmenize yardımcı Hello aşağıdaki bölümler.

### <a name="configure-hello-mysql-omi-provider"></a>Merhaba MySQL OMI sağlayıcı yapılandırma
Merhaba MySQL OMI sağlayıcısı önceden yapılandırılmış bir MySQL kullanıcının gerektiren ve MySQL istemci kitaplıkları sipariş tooquery hello performans/sistem durumu bilgilerini hello MySQL örneğinden yüklenir.

### <a name="mysql-omi-authentication-file"></a>MySQL OMI kimlik doğrulaması dosyası
MySQL OMI sağlayıcısı hangi bağlama adresi ve bağlantı noktası hello MySQL örneği dinlediği bir kimlik doğrulama dosya toodetermine ve ne toouse toogather ölçümleri kimlik bilgilerini kullanır. Yükleme hello MySQL OMI sırasında bağlama adresi ve bağlantı noktası kümesi hello MySQL OMI kimlik doğrulama dosyasını için ve kısmen MySQL my.cnf yapılandırma dosyalarını (varsayılan konumları) sağlayıcısı tarar.

bir MySQL server örneğini toocomplete izleme hello doğru dizine önceden oluşturulmuş bir MySQL OMI kimlik doğrulaması dosya ekleyin.

### <a name="authentication-file-format"></a>Kimlik doğrulama dosya biçimi
Merhaba MySQL OMI kimlik doğrulama dosyasını hakkında bilgi içeren bir metin dosyasıdır:

* Bağlantı noktası
* Bağ adresi
* MySQL kullanıcı adı
* Base64 ile kodlanmış parola

Merhaba MySQL OMI kimlik doğrulama dosyasını yalnızca oluşturulduğu okuma/yazma toohello Linux kullanıcı ayrıcalıkları verir.

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

Varsayılan MySQL OMI kimlik doğrulama dosyasını varsayılan bir örnek ve hangi bilgilerin kullanılabilir ve MySQL yapılandırma dosyası buldu hello öğesinden Ayrıştırılan bağlı olarak bir bağlantı noktası numarası içeriyor.

Merhaba varsayılan örneği daha kolay bir Linux ana bilgisayarda birden çok MySQL örneklerini yönetme anlamına gelir toomake ve bağlantı noktası 0 ile Merhaba örneği tarafından belirtilir. Tüm ek örneklerini hello varsayılan örneğinden ayarlanan özellikleri devralır. Örneğin, '3308' numaralı bağlantı noktasını dinlemeye MySQL örneği eklediyseniz, hello varsayılan örneğinin bağ adresi, kullanıcı adı ve Base64 ile kodlanmış parola kullanılan tootry olması ve 3308 üzerinde dinleme hello örneği izleme. Bağlanmadıysa tooanother adresi 3308 Hello örneğinde ve kullandığı hello aynı MySQL kullanıcı adı ve parola çiftinin yalnızca hello respecification hello bağ adresi gereklidir ve hello diğer özellikleri devralınır.

Merhaba kimlik doğrulama dosyasını örnekleri hello aşağıdakine benzer.

Varsayılan örneği ve bağlantı noktası 3308 ile örneği:

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

Varsayılan örneği ve bağlantı noktası 3308 + farklı Base 64 örneğiyle parola kodlanmış:

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| **Özellik** | **Açıklama** |
| --- | --- |
| Bağlantı noktası |Bağlantı noktası hello geçerli bağlantı noktası hello örneğinin dinlediği MySQL temsil eder.  başlangıç bağlantı noktası 0 hello özellikler aşağıdaki varsayılan örnek için kullanıldığı anlamına gelir. |
| Bağ adresi |Merhaba bağlamak adresi hello geçerli MySQL bağlama-adresidir |
| kullanıcı adı |Bu hello kullanıcı adını hello MySQL toouse toomonitor hello MySQL server örneği istiyor. |
| Parola Base64 ile kodlanmış |Bu hello hello MySQL izleme kullanıcının Base64 ile kodlanmış paroladır. |
| Otomatik güncelleştirme |Merhaba MySQL OMI sağlayıcı yükseltildiğinde hello sağlayıcısı hello my.cnf dosyasındaki değişiklikleri için yeniden tara ve hello MySQL OMI kimlik doğrulaması dosyanın üzerine yazın. Bu bayrak tootrue ya da yanlış gerekli güncelleştirmeleri toohello MySQL OMI bağlı olarak kimlik doğrulama dosyasını ayarlayın. |

#### <a name="authentication-file-location"></a>Kimlik doğrulama dosya konumu
Merhaba MySQL OMI kimlik doğrulaması dosya konumu aşağıdaki hello bulunan ve "auth mysql" adlı:

/var/OPT/Microsoft/MySQL-cimprov/auth/omsagent/MySQL-auth

Merhaba dosya (ve kimlik doğrulama/omsagent dizin) hello omsagent kullanıcıya ait.

## <a name="agent-logs"></a>Aracı günlükleri
Hello günlükleri hello Linux için OMS aracısı için aşağıdaki gibidir:

/ var/opt/microsoft/omsagent/&lt;çalışma alanı kimliği&gt;/log/

Merhaba günlükleri hello için Linux omsconfig (Aracısı yapılandırması) programı için OMS aracısının altındadır:

/ var/opt/microsoft/omsconfig/log /

Günlükleri (performans ölçüm verilerini sağlayan) hello OMI ve scx farklı bileşenlerin olduğuna:

/ var/opt/OMI/log/ve /var/opt/microsoft/scx/log

## <a name="troubleshooting-hello-oms-agent-for-linux"></a>Merhaba OMS Aracısı Linux için sorun giderme
Sık rastlanan sorunları giderme ve bilgi toodiagnose aşağıdaki hello kullanın.

Bu bölümdeki bilgiler, sorun giderme hello hiçbiri yardımcı olur, sorununuzu kaynakları toohelp Çöz aşağıdaki hello de kullanabilirsiniz.

* Müşteriler ile Premier Destek aracılığıyla bir destek talebi oturum açabilir [Premier](https://premier.microsoft.com/)
* Azure destek anlaşmaları müşterilerle destek olaylarının hello oturum [Azure portalı](https://manage.windowsazure.com/?getsupport=true)
* Dosya bir [GitHub sorunu](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)
* Geri bildirim Forumunda fikirleri ve toocreate bir hata raporu [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)

### <a name="important-log-locations"></a>Önemli günlük konumları
| Dosya | Yol |
| --- | --- |
| Linux günlük dosyası için OMS Aracısı |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| OMS Aracısı Yapılandırma günlük dosyasını |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a>Önemli yapılandırma dosyaları
| Catergory | Dosya konumu |
| --- | --- |
| Syslog |`/etc/syslog-ng/syslog-ng.conf`veya `/etc/rsyslog.conf` veya`/etc/rsyslog.d/95-omsagent.conf` |
| Performans, Nagios, Zabbix, OMS çıkış ve genel Aracısı |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| Ek yapılandırmalar |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> OMS portalı yapılandırması etkinse, performans sayaçları ve syslog için düzenleme yapılandırma dosyalarının üzerine yazılır. Merhaba OMS portalı (tüm düğümler) yapılandırmasında devre dışı bırakabilir veya hello aşağıdaki çalıştırarak tek düğümler için:
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a>Hata ayıklama günlük kaydını etkinleştir
tooenable hata ayıklama günlüğü, hello OMS çıkış eklentisi ve ayrıntılı çıktı kullanabilirsiniz.

#### <a name="oms-output-plugin"></a>OMS çıkış eklentisi
FluentD hello eklentisi toospecify girişleri ve çıkışları için farklı günlük düzeyleri için günlüğe kaydetme düzeylerini sağlar. toospecify OMS çıktı için farklı günlük düzeyi Düzenle hello hello genel Aracısı yapılandırmasında `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` dosya.

Merhaba yapılandırma dosyası Hello altına hello değiştirme `log_level` özelliğinden `info` çok`debug`.

 ```
 <match oms.** docker.**>
  type out_oms
  log_level debug
  num_threads 5
  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
 ```

Hata ayıklama günlüğünü OMS hizmetine veri öğeleri ve toosend geçen süre sayısını türüne göre ayrılmış toplu hale toosee karşıya toohello sağlar.

*Örnek etkin hata ayıklama günlüğü:*

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a>Ayrıntılı çıktı
Merhaba OMS çıkış eklentisini kullanmak yerine, ayrıca veri öğeleri doğrudan çok çıkarabilirsiniz`stdout`, olduğu hello OMS Aracısı Linux günlük dosyası için görünür.

Hello OMS genel Aracısı Yapılandırma dosyasındaki `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, yorum kullanıma hello OMS çıktı eklentisi ekleyerek bir `#` her satırın önünde.

```
#<match oms.** docker.**>
#  type out_oms
#  log_level info
#  num_threads 5
#  buffer_chunk_limit 5m
#  buffer_type file
#  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
#  buffer_queue_limit 10
#  flush_interval 20s
#  retry_limit 10
#  retry_wait 30s
#</match>
```

Aşağıdaki çıkış eklentisi Merhaba, hello yorum hello kaldırarak bölümü aşağıdaki hello kaldırmak `#` hello her satırın başındaki simgesi.

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-hello-log"></a>İletilen Syslog iletileri hello günlüğüne görünmez
#### <a name="probable-causes"></a>Olası nedenler
* Merhaba uygulanan yapılandırma toohello Linux sunucusu değil gönderilen hello olanaklarının toplanmasına izin vermek ve/veya düzeyleri oturum
* Syslog doğru toohello Linux sunucusuna iletilmez değil
* saniye başına iletilen iletilerinin Hello sayısı Linux toohandle için OMS aracısının hello hello temel yapılandırması için çok büyük

#### <a name="resolutions"></a>Çözümler
* Syslog tüm hello tesis ve hello doğru günlük düzeyleri için hello OMS portalı o hello yapılandırmasını doğrulayın
  * **OMS portalı > ayarları > veri > Syslog**
* Bu yerel syslog arka plan programları Mesajlaşma doğrulayın (`rsyslog`, `syslog-ng`) mümkün tooreceive iletilen Merhaba iletileri olan
* İletileri engellenmediğinden hello Syslog sunucusu tooensure üzerinde güvenlik duvarı ayarlarını kontrol edin
* Hello kullanarak Syslog iletisi tooOMS benzetimini `logger` command - örneğin:
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-toooms-when-using-a-proxy"></a>Bir proxy kullanılırken tooOMS bağlantısı sorunları
#### <a name="probable-causes"></a>Olası nedenler
* Yükleme ve yapılandırma hello Aracısı yanlış olduğunda Hello proxy belirtildi
* Merhaba OMS hizmet uç noktaları, veri merkezinizdeki whitelistested değildir

#### <a name="resolutions"></a>Çözümler
* Merhaba seçeneğiyle komut aşağıdaki hello kullanarak Linux için Hello OMS aracısı yeniden `-v` etkin. Bu ayrıntılı çıktı hello proxy toohello OMS hizmeti bağlanma hello Aracısı'nın sağlar.
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * OMS proxy için hello belgelerini gözden [bir HTTP proxy sunucusu ile kullanmak için yapılandırma hello Aracısı](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)
* OMS hizmet uç noktaları aşağıdaki o hello Güvenilenler listesine doğrulayın

| Aracı Kaynağı | Bağlantı Noktaları |
| --- | --- |
| &#42;. ods.opinsights.Azure.com |Bağlantı noktası 443 |
| &#42;. OMS.opinsights.Azure.com |Bağlantı noktası 443 |
| ods.systemcenteradvisor.com |Bağlantı noktası 443 |
| &#42;.blob.core.windows.net/ |Bağlantı noktası 443 |

### <a name="a-403-error-is-displayed-when-onboarding"></a>Bir 403 hatası görüntülenir, ekleme
#### <a name="probable-causes"></a>Olası nedenler
* Başlangıç tarihi ve saati Linux sunucusu üzerinde yanlış
* Merhaba çalışma alanı kimliği ve çalışma alanı anahtarı yanlış

#### <a name="resolution"></a>Çözüm
* Linux sunucunuzla hello Hello zamanında doğrulayın `date` komutu. Merhaba veri değerinden daha büyük ya da 15 dakikadan kısa geçerli saati hello sonra ekleme başarısız olur. toocorrect Bu, başlangıç tarihi ve/veya saat dilimi Linux sunucunuzun güncelleştirin.
* bir zaman farkı ekleme hatasına neden oluyorsa hello Linux için OMS aracısının en son sürümünü hello sizi bilgilendirir
* RE yerleşik kullanarak doğru çalışma alanı kimliği ve çalışma alanı anahtarı hello. Bkz: [hello komut satırını kullanarak Onboarding](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) daha fazla bilgi için.

### <a name="a-500-error-or-404-error-appears-in-hello-log-file-after-onboarding"></a>500 hata veya 404 hatası hello günlük dosyasında ekleme sonra görünür.
Bu hello bir OMS çalışma alanına Linux verilerin ilk yükleme sırasında oluşan bilinen bir sorundur. Bu, gönderilen veriler ya da diğer sorunlar etkilemez. Merhaba hataları ilk defa yoksayabilirsiniz ekleme.

### <a name="nagios-data-does-not-appear-in-hello-oms-portal"></a>Nagios veriler hello OMS portalı görünmüyor
#### <a name="probable-causes"></a>Olası nedenler
* Merhaba omsagent kullanıcının izinleri tooread hello Nagios günlük dosyasından yok
* Merhaba Nagios kaynak ve filtre bölümleri hello omsagent.conf dosyasında hala bırakılır

#### <a name="resolutions"></a>Çözümler
* Merhaba omsagent kullanıcı sipariş tooread hello Nagios dosyasından ekleyin. Bkz: [Nagios uyarıları](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) daha fazla bilgi için.
* İçinde Linux genel yapılandırma dosyasını için OMS aracısının hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, emin **her ikisi de** kaynak ve filtre bölümleri kaldırıldı, Yorumlar sahip Nagios aşağıdaki örneğine benzer toohello hello.

```
<source>
  type tail
  path /var/log/nagios/nagios.log
  format none
  tag oms.nagios
</source>

<filter oms.nagios>
  type filter_nagios_log
</filter>
```


### <a name="linux-data-doesnt-appear-in-hello-oms-portal"></a>Linux veri hello OMS portalı görünmüyor
#### <a name="probable-causes"></a>Olası nedenler
* Onboarding toohello OMS hizmeti başarısız oldu
* Bağlantı toohello OMS hizmetine engellendi
* Yedeklenen Hello OMS Aracısı Linux veriler için

#### <a name="resolutions"></a>Çözümler
* Bu ekleme toohello OMS hizmetine başarılı oldu, hello doğrulayarak doğrulayın `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` bulunmaktadır.
* RE yerleşik kullanarak hello omsadmin.sh komut satırı. Bkz: [hello komut satırını kullanarak Onboarding](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) daha fazla bilgi için.
* Bir proxy sunucu kullanıyorsanız, hello proxy sorun giderme adımlarını yukarıdaki kullanın
* Merhaba Linux için OMS aracısının hello OMS hizmeti ile iletişim kuramadığında bazı durumlarda, hello aracı üzerindeki yedeklenen toohello tam arabellek boyutu 50 MB verilerdir. Merhaba çalıştırarak Hello OMS Aracısı Linux için yeniden `/opt/microsoft/omsagent/bin/service_control restart` komutu.
  >[AZURE.NOTE] Aracı sürümü 1.1.0-28 ve daha sonra bu sorun düzeltilmiştir.

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-hello-oms-portal"></a>Syslog Linux performans sayacı yapılandırması hello OMS portalında uygulanmaz
#### <a name="probable-causes"></a>Olası nedenler
* Linux için OMS aracısının hello Hello yapılandırma aracı hello en son yapılandırma hello OMS Portalı'ndan alınmamış.
* Merhaba hello portalında değiştirilen ayarlar uygulanmadı

#### <a name="resolutions"></a>Çözümler
`omsconfig`Merhaba OMS Aracısı Hello yapılandırma aracı her 5 dakikada bir OMS portalı yapılandırma değişiklikleri alır Linux için ' dir. Linux yapılandırma dosyaları için uygulanan toohello OMS Aracısı konumundaki sonra bu yapılandırmadır `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.

* Bazı durumlarda mümkün toocommunicate uygulanmıyor son yapılandırmasında kaynaklanan hello portal Yapılandırma hizmeti ile Merhaba OMS Aracısı Linux yapılandırma aracı için olmayabilir.
* Bu hello doğrulayın `omsconfig` aracısının hello aşağıdakilerle yüklü:

  * `dpkg --list omsconfig` veya `rpm -qi omsconfig`
  * Yüklü değilse, Linux için hello hello OMS aracısının en son sürümünü yeniden yükleyin
* Bu hello doğrulayın `omsconfig` aracı hello OMS hizmeti ile iletişim

  * Merhaba çalıştırmak `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` komutu
    * Merhaba yukarıdaki komutu hello yapılandırmasını bu aracı döndürür Syslog ayarları, Linux performans sayaçları ve özel günlükleri gibi hello Portalı'ndan alır.
    * Yukarıdaki Hello komutu başarısız olursa, hello çalıştırmak `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` komutu. Bu komut hello omsconfig Aracısı toocommunicate hello OMS hizmet tooretrieve hello en son yapılandırmayla zorlar.

### <a name="custom-linux-log-data-does-not-appear-in-hello-oms-portal"></a>Özel Linux günlük verilerini hello OMS portalı görünmüyor
#### <a name="probable-causes"></a>Olası nedenler
* Hizmet Onboarding tooOMS başarısız oldu
* Merhaba **yapılandırma toomy Linux sunucuları aşağıdaki Uygula hello** ayarı seçilmediğinden
* omsconfig hello son özel günlük hello portalından yukarı çekilen değil
* Merhaba `omsagent` kullanılmasıdır oluşturulamıyor tooaccess hello özel günlük tooa izinlerle ilgili bir sorun nedeniyle veya `omsagent` bulunamadı. Bu durumda, çıktı aşağıdaki hello görürsünüz:
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* Bu hello hello OMS Aracısı Linux sürüm 1.1.0-217 için düzeltildi yarış durumu ile ilgili bilinen bir sorun olduğu

#### <a name="resolutions"></a>Çözümler
* Merhaba olup olmadığını belirleme, edildi başarıyla olduğunuz doğrulayın `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` dosya yok.
  * Gerekli olduğunda, yerleşik yeniden hello omsadmin.sh komut satırını kullanarak. Bkz: [hello komut satırını kullanarak Onboarding](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) daha fazla bilgi için.
* Merhaba altında OMS portalı içinde **ayarları** hello üzerinde **veri** sekmesinde, bu hello olun **yapılandırma toomy Linux sunucuları aşağıdaki Uygula hello** ayarı seçildiğinde  
  ![yapılandırmasını Uygula](./media/log-analytics-linux-agents/customloglinuxenabled.png)
* Bu hello doğrulayın `omsconfig` aracı hello OMS hizmeti ile iletişim

  * Merhaba çalıştırmak `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` komutu
  * Merhaba yukarıdaki komutu hello yapılandırmasını bu aracı döndürür hello Syslog ayarları, Linux performans sayaçları ve özel günlükleri de dahil olmak üzere Portalı'ndan alır
  * Yukarıdaki Hello komutu başarısız olursa, hello çalıştırmak `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` komutu. Bu komut, OMS hizmeti ile Merhaba omsconfig Aracısı toocommunicate zorlar ve hello en son yapılandırmayı almak.

Ayrıcalıklı bir kullanıcı olarak çalışan Linux kullanıcı için OMS aracısının hello yerine `root`, hello Linux çalıştıran için OMS aracısının hello `omsagent` kullanıcı. Çoğu durumda, açık izni olmalıdır belirli dosyaları sipariş tooread toohello kullanıcı izni.

toogrant izni çok`omsagent` kullanıcı, hello aşağıdaki komutları çalıştırın:

1. Merhaba eklemek `omsagent` kullanıcı tooa belirli grubuyla`sudo usermod -a -G <GROUPNAME> <USERNAME>`
2. Evrensel okuma erişimi toohello gerekli dosyasıyla verin`sudo chmod -R ugo+rw <FILE DIRECTORY>`

Merhaba hello OMS Aracısı Linux sürüm 1.1.0-217 için düzeltildi yarış durumu ile ilgili bilinen bir sorun yoktur. Toohello son aracısını güncelleştirdikten sonra komut tooget hello en son sürümünü hello çıkış eklentisi aşağıdaki hello çalıştırın:

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a>Bilinen sınırlamaları
Aşağıdaki bölümlerde toolearn Linux hello OMS Aracısı, geçerli sınırlamalar hakkında hello gözden geçirin.

### <a name="azure-diagnostics"></a>Azure Tanılama
Azure'da çalışan Linux sanal makineleri için ek adımlar gerekli tooallow veri toplama işlemi Azure tanılama ve Operations Management Suite tarafından olabilir. **Sürüm 2.2** Merhaba hello Linux için OMS Aracısı ile uyumluluk için tanılama uzantısını Linux için gereklidir.

Yükleme ve Linux için hello tanılama uzantısını yapılandırma hakkında daha fazla bilgi için bkz: [hello Azure CLI komutu tooenable Linux tanılama uzantısını kullanmak](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).

**Merhaba Linux tanılama uzantısını 2.0 too2.2 Azure CLI ASM yükseltme:**

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

**ARM**

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

Bu komut örnekleri PrivateConfig.json adlı bir dosyaya başvuru. Bu dosya biçiminin Hello örnek aşağıdaki hello benzemelidir.

```
    {
    "storageAccountName":"hello storage account tooreceive data",
    "storageAccountKey":"hello key of hello account"
    }
```

### <a name="sysklog-is-not-supported"></a>Sysklog desteklenmiyor
Rsyslog veya syslog ng gerekli toocollect syslog iletileri şunlardır. Red Hat Enterprise Linux, CentOS ve Oracle Linux sürümü (sysklog) 5 sürümünü Hello varsayılan syslog arka plan syslog olay toplaması için desteklenmiyor. Bu sürümü bu dağıtımları toocollect syslog verileri hello rsyslog arka plan programı yüklenmelidir ve tooreplace sysklog yapılandırılır. Sysklog rsyslog ile değiştirerek daha fazla bilgi için bkz: [yeni yerleşik hello rsyslog RPM yüklemek](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).

## <a name="next-steps"></a>Sonraki Adımlar
* [Günlük analizi çözümleri Çözümleri Galerisi hello eklemek](log-analytics-add-solutions.md) tooadd işlevselliği ve toplama verileri.
* İle tanışın [oturum aramaları](log-analytics-log-searches.md) tooview ayrıntılı çözümler tarafından toplanan bilgiler.
* Kullanım [panolar](log-analytics-dashboards.md) toosave ve görüntü kendi özel arar.
