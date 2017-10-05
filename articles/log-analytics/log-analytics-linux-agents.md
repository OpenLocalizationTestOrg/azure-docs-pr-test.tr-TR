---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: TRUE
ROBOTS: NOINDEX
ms.openlocfilehash: 8332bdd39effab8c2ac9a75ca9a1e2510c940719
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-your-linux-computers-to-log-analytics"></a>Linux bilgisayarlarınızı günlük Analizi'ne bağlayın
Günlük analizi kullanarak toplamak ve Linux bilgisayarları oluşturulan veri hareket. Linux OMS için toplanan verileri eklemeye izin verir, Linux sistemleri ve nerede olursa olsun bilgisayarlarınızı Docker gibi kapsayıcı çözümleri yönetmek — neredeyse her yerden. Veri kaynakları, Amazon Web Hizmetleri (AWS) veya Microsoft Azure veya hatta masanıza dizüstü bilgisayar gibi bir bulutta barındırılan hizmetindeki sanal bilgisayarlar fiziksel sunucuları olarak, şirket içi veri merkezinizde bulunması. Gerçekten karma BT ortamında destekler şekilde ek olarak, OMS ayrıca Windows bilgisayarlardan benzer şekilde, toplar.

Görüntüleme ve tüm OMS günlük analizi ile bu kaynakları tek bir Yönetim Portalı ile verileri yönetme. Bu, birçok farklı sistemleri, kullanmak kolay ve hangi iş analiz çözümü veya zaten sistem istediğiniz herhangi bir veri verebilirsiniz yapar kullanarak izlemek için gereken azaltır.

Bu makalede, bir hızlı başlangıç toplamak ve Linux için OMS Aracısı'nı kullanarak, Linux bilgisayarların verilerini yönetmenize yardımcı olacak Kılavuzu ' dir. Proxy sunucu yapılandırması, CollectD ölçümleri ve özel JSON veri kaynakları hakkında bilgi gibi daha fazla teknik bilgi için bu bilgileri bulabilirsiniz [Linux genel bakış için OMS Aracısı](https://github.com/Microsoft/OMS-Agent-for-Linux) ve [Linux için OMS Aracısı tam belgelerine](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) github'da.

Şu anda aşağıdaki veri türlerini Linux bilgisayarlardan toplayabilirsiniz:

* Performans ölçümleri
* Syslog olayları
* Nagios ve Zabbix uyarıları
* Docker kapsayıcısı performans ölçümleri, Envanter ve günlükleri

## <a name="supported-linux-versions"></a>Desteklenen Linux sürümleri
Hem x86 hem x64 sürümleri Linux dağıtımları çeşitli resmi olarak desteklenir. Ancak, OMS Aracısı Linux için listelenmeyen diğer dağıtımlar da çalıştırabilirsiniz.

* Amazon Linux 2015.09 aracılığıyla 2012.09
* CentOS Linux 5, 6 ve 7
* Oracle Linux 5, 6 ve 7
* Red Hat Enterprise Linux Server 5, 6 ve 7
* Debian GNU/Linux 6, 7 ve 8
* Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10
* SUSE Linux Enterprise Server 11 ve 12

## <a name="oms-agent-for-linux"></a>Linux için OMS Aracısı
Linux için Operations Management Suite Aracısı birden çok paket oluşur. Aşağıdaki paketler, kabuk Paketle çalıştırarak kullanılabilir sürüm dosyasını içeren `--extract`.

| **Paket** | **Sürüm** | **Açıklama** |
| --- | --- | --- |
| omsagent |1.1.0 |Linux için Operations Management Suite Aracısı |
| omsconfig |1.1.1 |OMS aracısı için yapılandırma aracısı |
| OMI |1.0.8.3 |Açık Yönetim Altyapısı (OMI)--bir basit CIM sunucusu |
| scx |1.6.2 |İşletim sistemi performans ölçümleri için OMI CIM sağlayıcıları |
| Apache cimprov |1.0.0 |Apache HTTP Server performansı sağlayıcısı OMI için izleme. Apache HTTP Server algılanırsa, yalnızca yüklü. |
| MySQL cimprov |1.0.0 |MySQL sunucusu performans sağlayıcısı OMI için izleme. MySQL/MariaDB sunucu algılanırsa, yalnızca yüklü. |
| docker cimprov |0.1.0 |OMI docker sağlayıcısı. Docker algılanırsa, yalnızca yüklü. |

### <a name="additional-installation-artifacts"></a>Ek yükleme yapıları
Linux paketler için OMS Aracısı yükledikten sonra aşağıdaki ek sistem genelinde yapılandırma değişikliklerini uygulanır. Bu yapıtların omsagent paket kaldırıldığında kaldırılır.

* Adlı bir ayrıcalıklı olmayan kullanıcı: `omsagent` oluşturulur. Bu olarak omsagent arka plan programı çalıştıran hesabıdır
* "Ekle" sudoers dosyası oluşturulur /etc/sudoers.d/omsagent bu syslog ve omsagent Daemon başlatmayı omsagent yetkilendirir. Sudo "Ekle" yönergeleri sudo yüklü sürümünde desteklenmez Bu girdiler için /etc/sudoers yazılır.
* Syslog yapılandırma aracıya bir alt olayların iletecek şekilde değiştirilir. Daha fazla bilgi için bkz: **yapılandırma veri toplama** bölümüne bakın

### <a name="linux-data-collection-details"></a>Linux veri toplama ayrıntıları
Aşağıdaki tabloda, veri toplama yöntemleri ve verileri nasıl toplanır ilgili diğer ayrıntıları gösterir.

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
> Rsyslog veya syslog ng syslog iletileri toplamak için gereklidir. Red Hat Enterprise Linux, CentOS ve Oracle Linux sürümü (sysklog) 5 sürümünü varsayılan syslog arka plan syslog olay toplaması için desteklenmiyor. Bu dağıtımları bu sürümünden Syslog verileri toplamak için rsyslog arka plan programı yüklenmeli ve sysklog değiştirmek için yapılandırılmalıdır.
>
>

## <a name="quick-install"></a>Hızlı yükleme
Omsagent indirin, sağlama toplamı doğrulama, daha sonra yüklemek için aşağıdaki komutları çalıştırın ve yerleşik aracı. 64 bit için komutlardır. Çalışma alanı kimliği ve birincil anahtar OMS portalında altında bulunan **ayarları** üzerinde **bağlı kaynakları** sekmesi.

![çalışma alanı ayrıntıları](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

Çeşitli aracıyı yüklemek ve yükseltmek için diğer yöntemler vardır. Daha fazla bilgiyi onları hakkında [Linux için OMS Aracısı'nı yüklemek için adımları](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).

Ayrıca görüntüleyebilirsiniz [Azure videosu](https://www.youtube.com/watch?v=mF1wtHPEzT0).

## <a name="choose-your-linux-data-collection-method"></a>Linux veri toplama yönteminizi seçin
Nasıl toplamak istediğiniz veri türlerini bağlı olarak çeşitli yapılandırma dosyalarını doğrudan Linux istemcileriniz düzenlemek istiyorsanız veya OMS portalı kullanmak isteyip istemediğinizi seçin. Yapılandırma Portalı'nı kullanmayı tercih ederseniz, tüm Linux istemcileriniz otomatik olarak gönderilir. Farklı Linux istemcileri için farklı yapılandırmaları gerekiyorsa, istemci dosyalarını ayrı ayrı – düzenlemek veya PowerShell DSC, Chef veya Puppet gibi bir alternatif kullanmak gerekir.

Syslog olayları ve Linux bilgisayarları yapılandırma dosyalarını kullanarak toplamak istediğiniz performans sayaçları belirtebilirsiniz. *Veri toplama Aracısı Yapılandırma dosyalarını düzenleyerek yapılandırmak seçerseniz, merkezi yapılandırma devre dışı bırakmanız gerekir.*  Yönergeler aracısının yapılandırma dosyalarında veri toplamayı yapılandırmak için yanı sıra tüm OMS aracılar için merkezi yapılandırma Linux ya da ayrı bilgisayarlar için devre dışı bırakmak için aşağıda verilmiştir.

### <a name="disable-oms-management-for-an-individual-linux-computer"></a>Tek bir Linux bilgisayar için OMS yönetimi devre dışı
Yapılandırma verileri için merkezi veri toplama OMS_MetaConfigHelper.py betiği ile tek bir Linux bilgisayarı devre dışı bırakılmıştır. Bu, bilgisayarların alt ağlarından özel bir yapılandırmanız varsa yararlı olabilir.

Merkezi yapılandırma devre dışı bırakmak için:

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

Merkezi yapılandırma yeniden etkinleştirmek için:

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a>Linux performans sayaçları
Linux performans sayaçları için Windows performans sayaçlarını benzer — her ikisi de aynı şekilde çalışır. Ekleyin ve bunları yapılandırmak için aşağıdaki yordamları kullanabilirsiniz. Verileri için OMS eklendikten sonra bunlar için her 30 saniyede toplanır.

### <a name="to-add-a-linux-performance-counter-in-oms"></a>Bir Linux performans sayacı OMS eklemek için
1. OMS Portalı'nı kullanarak Linux için OMS aracısı yapılandırmak için Ayarlar sayfasında Linux performans sayaçlarını Ekle, tıklatın **veri**.  
2. Üzerinde **ayarları** altında sayfa **veri** , tıklatın **Linux performans sayaçları** ve daha sonra seçin veya eklemek istediğiniz sayacının adını yazın.  
    ![veri](./media/log-analytics-linux-agents/oms-settings-data01.png)
3. Sayacın tam adını bilmiyorsanız, kısmi bir ad yazarak başlatabilirsiniz ve kullanılabilir sayaçlarının listesi görüntülenir. Eklemek istediğiniz sayacı bulduğunuzda, listedeki adına tıklayın ve ardından sayaç eklemek için artı simgesine tıklayın.
4. Sayaç ekledikten sonra renkli çubuk ile vurgulanan sayaçlarının listesi görüntülenir.
5. Varsayılan olarak, **aşağıdaki yapılandırmayı makinelerime Uygula** seçeneği işaretlidir. Gönderen yapılandırmasını devre dışı bırakmak seçimi temizleyin.
6. Değiştirme performans sayaçları, sayfanın sonundaki bittiğinde tıklatın **kaydetmek** değişikliklerinizi sona erdirmek için. Yaptığınız yapılandırma değişikliklerini OMS ile genellikle 5 dakika içinde kayıtlı Linux için OMS aracılara tüm sonra gönderilir.

### <a name="configure-linux-performance-counters-in-oms"></a>Linux performans sayaçları OMS yapılandırın
Windows performans sayaçları için her performans sayacı için belirli bir örneği seçebilirsiniz. Ancak, Linux performans sayaçları için ne olursa olsun, seçtiğiniz bir sayaç örneği üst sayacı tüm alt sayaçları geçerlidir. Aşağıdaki tabloda, Linux ve Windows performans sayaçları için kullanılabilen ortak örnekleri gösterilmektedir.

| **Örnek adı** | **Anlamı** |
| --- | --- |
| \_Toplam |Tüm örnekleri toplamı |
| \* |Tüm örnekleri |
| (/ &#124; / var) |Eşleşen adlandırılmış örnekleri: / veya /var |

Benzer şekilde, bir üst sayaç için seçtiğiniz örnek aralığı, tüm alt sayaçlarını geçerlidir. Diğer bir deyişle, tüm alt sayacı örnek aralıklar ve örnekleri birbirine bağlıdır.

### <a name="add-and-configure-performance-metrics-with-linux"></a>Ekleme ve performans ölçümleri Linux ile yapılandırma
Performans ölçümleri toplamak için giriş/etc/opt/microsoft/omsagent yapılandırması tarafından denetlenen/&lt;çalışma alanı kimliği&gt;/conf/omsagent.conf. Bkz: [kullanılabilir performans ölçümleri](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) kullanılabilir sınıfların ve Linux için OMS aracısının ölçümleri.

Tek bir yapılandırma dosyasındaki her nesne veya toplamak için performans ölçümleri kategorisi tanımlanmalıdır `<source>` öğesi. Sözdizimi deseni izler.

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

Bu öğenin yapılandırılabilir Parametreler şunlardır:

* **Nesne\_adı**: koleksiyon için nesne adı.
* **Örnek\_regex**: bir *normal ifade* toplamak için hangi örnekleri tanımlama. Değer: `.*` tüm örneklerini belirtir. Yalnızca işlemci ölçümleri toplamak için \_toplam örneğini belirtmek `_Total`. Yalnızca crond veya sshd örnekleri için işlem ölçümlerini toplamak için belirtebilirsiniz: `(crond|sshd)`.
* **Sayaç\_adı\_regex**: bir *normal ifade* hangi toplamak için (nesne için) sayaçları tanımlama. Nesne için tüm sayaçlar toplanacak belirtin: `.*`. Yalnızca takas alanı sayaçları için bellek nesnesi toplanacak belirtebilirsiniz:`.+Swap.+`
* **Aralığı:**: nesnesinin sayaçları toplanır sıklığı.

Performans ölçümleri için varsayılan yapılandırmayı şöyledir:

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
Omsagent paketi yüklendiğinde, MySQL Server veya MariaDB Server bilgisayarda algılanırsa, bir performans izleme sağlayıcısı MySQL sunucusu için otomatik olarak yüklenir. Bu sağlayıcı performans istatistiklerini kullanıma sunmak için yerel MySQL/MariaDB sunucusuna bağlanır. MySQL kullanıcı kimlik bilgileri sağlayıcısı MySQL Server erişebilmesi için yapılandırmanız gerekir.

MySQL sunucusu için varsayılan bir kullanıcı hesabı üzerinde localhost tanımlamak için aşağıdaki komut örneği kullanın.

> [!NOTE]
> Kimlik bilgileri dosyası omsagent hesap tarafından okunabilir olması gerekir. Omsgent mycimprovauth komutunun çalıştırılması önerilir.
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


Bir dosyada dosya oluşturarak gerekli MySQL kimlik alternatif olarak, belirtebilirsiniz: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. Mysql auth dosyası aracılığıyla izleme MySQL kimlik bilgilerini yönetme hakkında daha fazla bilgi için bkz: [kimlik bilgileri kimlik doğrulama dosyasındaki İzleme MySQL yönetmek](#manage-mysql-monitoring-credentials-in-the-authentication-file).

Bkz: [veritabanı için MySQL performans sayaçları gerekli izinler](#database-permissions-required-for-mysql-performance-counters) MySQL sunucusu performans verilerini toplamak için MySQL kullanıcı tarafından gerekli nesne izinleri hakkında ayrıntılı bilgi için.

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a>Linux komutlarını kullanarak Apache HTTP Server performans sayaçları sağlar
Apache HTTP Server omsagent paket yüklü olduğunda bilgisayarda algılanırsa, bir performans izlemesi için Apache HTTP Server sağlayıcısı otomatik olarak yüklenir. Bu sağlayıcı Apache "Apache HTTP Server performans verilerini erişmek için yüklenmesi gereken modül" kullanır.

Modül aşağıdaki komutu kullanarak yükleyebilirsiniz:

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

Apache izleme modülü kaldırmak için aşağıdaki komutu çalıştırın:

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="to-view-performance-data-with-log-analytics"></a>Günlük analizi ile performans verilerini görüntülemek için
1. Operations Management Suite Portalı'nda günlük arama kutucuğuna tıklayın.
2. Arama çubuğuna `* (Type=Perf)` tüm performans sayaçlarını görüntülemek için.

OMS aynı zamanda Windows performans sayacı verilerini toplar olduğundan, kapsam Linux'a özgü verileri aramayı aşağı. Bu nedenle, aşağıdaki örnek performans verileri Chorizo21 adlandırılmış bir örnek Linux sunucusuna belirli gösterir.

```
Type=Perf Computer=chorizo*
```

![arama sonuçlarında gösterilen örnekte, sunucu](./media/log-analytics-linux-agents/oms-perfsearch01.png)

Sonuçlarda tıklayabilirsiniz **ölçümleri** veri için toplanan sayaçlarını görüntülemek için. Gerçek zamanlı veri grafikleri her sayacı olarak gösterilir.

![metrics](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a>Syslog
Syslog protokolüdür bir olay günlüğü Windows olay günlüklerini benzer — hem OMS görüntülendiğinde benzer şekilde çalışır.

### <a name="to-add-a-new-linux-syslog-facility-in-oms"></a>OMS içinde yeni bir Linux syslog özelliğini eklemek için
1. Üzerinde **ayarları** altında sayfa **veri** , tıklatın **Syslog** ve ardından artı simgesinin solunda eklemek istediğiniz syslog özelliğini adını yazın.
    ![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)
2. Tesis tam adını bilmiyorsanız, kısmi bir ad yazarak başlatabilirsiniz ve kullanılabilir syslog tesis listesi görüntülenir. Eklemek istediğiniz syslog özelliğini bulduğunuzda, listedeki adına tıklayın ve ardından syslog özelliğini eklemek için artı simgesine tıklayın.
3. Listesinde görünür tesis ekledikten sonra renkli çubuk ile vurgulanır. Ardından, toplamak istediğiniz önem derecelerinin (syslog tesis bilgi kategorilerde) seçin.
4. Sayfanın alt kısmında tıklatın **kaydetmek** değişikliklerinizi sona erdirmek için. Yaptığınız yapılandırma değişikliklerini OMS ile genellikle 5 dakika içinde kayıtlı Linux için OMS aracılara tüm sonra gönderilir.

### <a name="configure-linux-syslog-facilities-in-linux"></a>Linux syslog Linux tesislerde yapılandırın
Syslog olayları syslog arka plan programından, örneğin rsyslog veya syslog-ng, aracının dinlediği yerel bir bağlantı noktasına gönderilir. Varsayılan olarak, bağlantı noktası 25224. Aracıyı yüklediğinizde, varsayılan bir syslog yapılandırma uygulanır. Bu da bulunur:

Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf

Syslog ng: /etc/syslog-ng/syslog-ng.conf

Varsayılan OMS Aracısı syslog yapılandırması tüm uyarı veya daha büyük bir önem derecesi araçlarıyla syslog olayları yükler.

> [!NOTE]
> Syslog yapılandırma düzenlerseniz, syslog arka plan programı değişikliklerin etkili olması yeniden başlatmanız gerekir.
>
>

Syslog için varsayılan yapılandırmayı OMS aracısı için Linux için OMS şöyledir:

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

### <a name="to-view-all-syslog-events-with-log-analytics"></a>Günlük analizi ile tüm Syslog olayları görüntülemek için
1. Operations Management Suite Portalı'nda tıklatın **günlük arama** döşeme.
2. İçinde **Günlüğü Yönetimi** gruplandırma, önceden tanımlanmış syslog arama seçin ve sonra bir çalıştırmak için seçin.

Bu örnekte tüm Syslog olayları gösterir.

![Günlük aramada gösterilen Syslog olayları](./media/log-analytics-linux-agents/oms-linux-syslog.png)

Şimdi arama sonuçlarında detaya inebilirsiniz.

## <a name="linux-alerts"></a>Linux uyarıları
Linux makineler yönetmek için Nagios veya Zabbix kullanırsanız, OMS bu Araçları'ndan oluşturulan uyarıların alabilir. Ancak, şu anda OMS Portalı'nı kullanarak gelen uyarı verileri yapılandırmak için yöntemi yoktur. Bunun yerine, uyarılar için OMS gönderme başlamak için bir yapılandırma dosyasını düzenlemeniz gerekir.

### <a name="collect-alerts-from-nagios"></a>Nagios toplama uyarıları
Nagios sunucudan uyarılarını toplamak için aşağıdaki yapılandırma değişiklikleri yapmanız gerekir.

1. Kullanıcının izni **omsagent** Nagios günlük dosyasına (yani /var/log/nagios/nagios.log) okuma erişimi. Nagios.log dosya varsayılarak grupla sahibi **nagios** , kullanıcı ekleyebilir **omsagent** için **nagios** grubu.

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. Omsagent.confconfiguration dosyasını değiştirme (/ etc/opt/microsoft/omsagent/&lt;çalışma alanı kimliği&gt;/conf/omsagent.conf). Mevcut ve kullanıma açıklamalı aşağıdaki girdileri çalıştığından emin olun:

    ```
    <source>
    type tail
    #Update path to point to your nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. Omsagent arka plan programı yeniden başlatın:

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a>Zabbix toplama uyarıları
Bir kullanıcı ve parola belirtmeniz gerekir dışında Zabbix sunucudan uyarılarını toplamak için yukarıdaki Nagios için olanlar için benzer adımları gerçekleştirirsiniz *açık metin*. Bu ideal olmayan, ancak büyük olasılıkla yakında değiştirir. Bu sorunu gidermek için kullanıcı oluşturun ve onu yalnızca izlemek için izni öneririz.

Bir örnek bölüm omsagent.conf yapılandırma dosyasının (/ etc/opt/microsoft/omsagent/&lt;çalışma alanı kimliği&gt;/conf/omsagent.conf) Zabbix aşağıdaki benzemelidir için:

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
OMS için uyarıları göndermek üzere, Linux Bilgisayarları yapılandırdıktan sonra birkaç basit günlük arama sorguları uyarıları görüntülemek için kullanabilirsiniz. Aşağıdaki arama sorgusu örneğinde oluşturulan tüm kayıtlı uyarıların döndürür. BT altyapınızın sorun çeşit meydana gelirse, örneğin, ardından aşağıdaki örnek sorgu sonuçlarını sorunun nerede kaynaklanan gösterebilir. Ve, kolayca uyarılara daraltmaya yardımcı olmak için kaynak sistem tarafından araştırmanızı inebilir. Avantajı, mutlaka başından çeşitli yönetim sistemleri için Git gerekmemesidir — uyarılarınızı için OMS gönderilen koşuluyla var. başlatabilirsiniz.

```
Type=Alert
```

#### <a name="to-view-all-nagios-alerts-with-log-analytics"></a>Günlük analizi ile tüm Nagios uyarıları görüntülemek için
1. Operations Management Suite Portalı'nda tıklatın **günlük arama** döşeme.
2. Sorgu çubuğuna aşağıdaki arama sorgusu yazın

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Günlük aramada gösterilen Nagios uyarıları](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

Arama sonuçlarını gördükten sonra ek ayrıntılar gibi inebilir *AlertState*.

### <a name="to-view-all-zabbix-alerts-with-log-analytics"></a>Günlük analizi ile tüm Zabbix uyarıları görüntülemek için
1. Operations Management Suite Portalı'nda tıklatın **günlük arama** döşeme.
2. Sorgu çubuğuna aşağıdaki arama sorgusu yazın

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Günlük aramada gösterilen Zabbix uyarıları](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

Arama sonuçlarını gördükten sonra ek ayrıntılar gibi inebilir *AlertName*.

## <a name="compatibility-with-system-center-operations-manager"></a>System Center Operations Manager ile uyumluluk
Linux için OMS aracısının Aracısı ikili dosyaları System Center Operations Manager Aracısı ile paylaşır. Şu anda Operations Manager tarafından yönetilen bir sistemde Linux için OMS Aracısı'nı yükleme bilgisayardaki OMI ve SCX paketleri daha yeni bir sürüme yükseltir. Linux ve System Center 2012 R2 için OMS aracısının uyumlu olur. Ancak, **System Center 2012 SP1 ve önceki sürümleri olmayan şu anda uyumlu ya da desteklenen Linux için OMS Aracısı ile.**

> [!NOTE]
> Bilgisayar Bul önce Linux için OMS aracısının şu anda Operations Manager tarafından yönetilmeyen bir bilgisayara yüklü olduğundan ve daha sonra bilgisayar Operations Manager ile yönetmek istediğiniz, OMI yapılandırma değiştirmeniz gerekir. **Linux için Operations Manager Aracısı önce OMS Aracısı yüklüyse, bu adım gerekli değildir.**
>
>

### <a name="to-enable-the-oms-agent-for-linux-to-communicate-with-operations-manager"></a>Operations Manager ile iletişim kurmak Linux için OMS Aracısı etkinleştirmek için
1. Dosya /etc/opt/omi/conf/omiserver.conf Düzenle
2. Satır başlayarak emin **httpsport =** bağlantı noktası 1270 tanımlar. Gibi`httpsport=1270`
3. OMI sunucuyu yeniden başlatın:

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a>MySQL performans sayaçları için gereken veritabanı izinleri
Bir MySQL izleme kullanıcı izinlerini vermek için izni veriliyor kullanıcının verilmeden ayrıcalık yanı sıra, 'GRANT option' ayrıcalığı olmalıdır.

MySQL kullanıcının kullanıcı performans verileri döndürmek sırayla aşağıdaki sorguları erişimi gerekir:

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

Bu sorguları MySQL yanı sıra kullanıcı aşağıdaki varsayılan tabloları seçme erişimi gerektirir:

* INFORMATION_SCHEMA
* MySQL

Bu ayrıcalıklar aşağıdaki grant komutlarını çalıştırarak verilebilir.

```
GRANT SELECT ON information_schema.* TO ‘monuser’@’localhost’;
GRANT SELECT ON mysql.* TO ‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-the-authentication-file"></a>Kimlik doğrulama dosyasını kimlik bilgilerini izleme MySQL yönetme
Aşağıdaki bölümlerde MySQL kimlik bilgilerini yönetmenize yardımcı olur.

### <a name="configure-the-mysql-omi-provider"></a>MySQL OMI sağlayıcı yapılandırma
MySQL OMI sağlayıcı önceden yapılandırılmış bir MySQL kullanıcının gerektiren ve MySQL örneğine performans/sistem durumu bilgileri sorgulamak için MySQL istemci kitaplıkları yüklü.

### <a name="mysql-omi-authentication-file"></a>MySQL OMI kimlik doğrulaması dosyası
Hangi bağlama adresini belirlemek ve örnek dinlediği MySQL ve ne ölçümleri toplamak için kullanılacak kimlik bilgileri bağlantı noktası için bir kimlik doğrulama dosyasını MySQL OMI sağlayıcısını kullanır. MySQL OMI yükleme sırasında sağlayıcısı bağ adresi ve bağlantı noktası için MySQL my.cnf yapılandırma dosyalarını (varsayılan konumları) tarama ve kısmen MySQL OMI kimlik doğrulama dosyasını ayarlayın.

MySQL sunucusu örneğini izleme tamamlamak için önceden oluşturulmuş bir MySQL OMI kimlik doğrulaması dosya doğru dizine ekleyin.

### <a name="authentication-file-format"></a>Kimlik doğrulama dosya biçimi
MySQL OMI kimlik doğrulama dosyasını hakkında bilgi içeren bir metin dosyasıdır:

* Bağlantı noktası
* Bağ adresi
* MySQL kullanıcı adı
* Base64 ile kodlanmış parola

MySQL OMI kimlik doğrulama dosyasını okuma/yazma için ayrıcalıkları oluşturan Linux kullanıcı yalnızca verir.

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

Varsayılan MySQL OMI kimlik doğrulama dosyasını varsayılan bir örnek ve bağlı olarak hangi bilgilerin bulunan MySQL yapılandırma dosyasından ayrıştırılmış ve kullanılabilir bir bağlantı noktası numarası içeriyor.

Varsayılan örneği daha kolay bir Linux ana bilgisayarda birden çok MySQL örneklerini yönetme yapmak için bir araçtır ve bağlantı noktası 0 ile örneği tarafından belirtilir. Tüm ek örneklerini varsayılan örneğinden ayarlanan özellikleri devralır. MySQL örneği '3308' numaralı bağlantı noktasını dinlemeye eklediyseniz, örneğin, varsayılan örneğinin bağ adresi, kullanıcı adı ve Base64 ile kodlanmış parola deneyin ve 3308 üzerinde dinleme örneği izlemek için kullanılacak. 3308 örneğinde başka bir adres bağlanıp ve aynı MySQL kullanıcı adı ve parola çifti kullanıyorsa yalnızca bağlama adresinin respecification gereklidir ve diğer özellikleri devralınır.

Kimlik doğrulama dosyasını örnekleri aşağıdakine benzer.

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
| Bağlantı noktası |Bağlantı noktası MySQL örneği üzerinde dinleme geçerli bağlantı noktası temsil eder.  0 bağlantı noktası, aşağıdaki özellikler varsayılan örnek için kullanıldığı anlamına gelir. |
| Bağ adresi |Geçerli MySQL bağ adresi bağlamak adresidir |
| kullanıcı adı |Bu MySQL server örneği izlemek için kullanmak istediğiniz MySQL kullanıcının kullanıcı adı. |
| Parola Base64 ile kodlanmış |Base64 ile kodlanmış MySQL izleme kullanıcının parolası budur. |
| Otomatik güncelleştirme |MySQL OMI sağlayıcı yükseltildiğinde sağlayıcı my.cnf dosyasındaki değişiklikleri için yeniden tarayın ve MySQL OMI kimlik doğrulaması bu dosyanın üzerine. Bu bayrak true veya false MySQL OMI kimlik doğrulama dosyasını gerekli güncelleştirmeler bağlı olarak ayarlayın. |

#### <a name="authentication-file-location"></a>Kimlik doğrulama dosya konumu
MySQL OMI kimlik doğrulaması dosyası şu konumda bulunan ve "auth mysql" adlı:

/var/OPT/Microsoft/MySQL-cimprov/auth/omsagent/MySQL-auth

Dosya (ve kimlik doğrulama/omsagent dizin) omsagent kullanıcıya ait.

## <a name="agent-logs"></a>Aracı günlükleri
Linux için OMS aracısı için günlükleri olduğuna:

/ var/opt/microsoft/omsagent/&lt;çalışma alanı kimliği&gt;/log/

Linux için OMS aracısının günlükleri omsconfig (Aracısı yapılandırması) programı için aşağıdaki gibidir:

/ var/opt/microsoft/omsconfig/log /

Günlükleri (performans ölçüm verilerini sağlayan) OMI ve scx farklı bileşenlerin olduğuna:

/ var/opt/OMI/log/ve /var/opt/microsoft/scx/log

## <a name="troubleshooting-the-oms-agent-for-linux"></a>Linux için OMS Aracısı sorunlarını giderme
Tanılamak ve sık karşılaşılan sorunları gidermek için aşağıdaki bilgileri kullanın.

Bu bölümdeki sorun giderme bilgileri hiçbiri yardımcı olur, sorunu gidermek için aşağıdaki kaynaklara da kullanabilirsiniz.

* Müşteriler ile Premier Destek aracılığıyla bir destek talebi oturum açabilir [Premier](https://premier.microsoft.com/)
* Azure destek anlaşmaları sahip müşteriler oturum destek olaylarının [Azure portalı](https://manage.windowsazure.com/?getsupport=true)
* Dosya bir [GitHub sorunu](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)
* Geri bildirim Forumunda fikirleri ve bir hata raporu oluşturmak için [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)

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
> OMS portalı yapılandırması etkinse, performans sayaçları ve syslog için düzenleme yapılandırma dosyalarının üzerine yazılır. Yapılandırma portalında OMS (tüm düğümler) devre dışı bırakabilir veya aşağıdaki çalıştırarak tek düğümler için:
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a>Hata ayıklama günlük kaydını etkinleştir
Hata ayıklama günlüğünü etkinleştirmek için OMS çıkış eklentisi ve ayrıntılı çıktı kullanabilirsiniz.

#### <a name="oms-output-plugin"></a>OMS çıkış eklentisi
FluentD girişleri ve çıkışları için farklı günlük düzeyleri için günlüğe kaydetme düzeyini belirtmek eklenti sağlar. OMS çıktı için farklı günlük düzeyini belirtmek için genel Aracısı yapılandırmasında Düzenle `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` dosya.

Yapılandırma dosyası altına değiştirme `log_level` özelliğinden `info` için `debug`.

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

Hata ayıklama günlüğünü sayısı veri öğeleri ve göndermek için harcanan süre türü tarafından ayrılmış OMS hizmetine toplu yüklemeleri görmenizi sağlar.

*Örnek etkin hata ayıklama günlüğü:*

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a>Ayrıntılı çıktı
OMS çıkış eklentisini kullanmak yerine, ayrıca veri öğeleri doğrudan çıkarabilirsiniz `stdout`, Linux günlük dosyası için OMS aracısının görünür olduğu.

OMS genel Aracısı Yapılandırma dosyasında `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, yorum kullanıma OMS çıktı eklentisi ekleyerek bir `#` her satırın önünde.

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

Çıktı eklentisi yorum aşağıdaki bölümde kaldırmak `#` her satırın başındaki simgesi.

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-the-log"></a>İletilen Syslog iletilerini günlüğe görünmez
#### <a name="probable-causes"></a>Olası nedenler
* Linux sunucuya uygulanan yapılandırma gönderilen tesis ve/veya günlük düzeyleri koleksiyonunu izin verme
* Syslog doğru Linux sunucusuna İletiliyor değil
* Saniye başına iletilen iletilerin sayısını işlemek Linux için OMS aracısının temel yapılandırması için çok büyük

#### <a name="resolutions"></a>Çözümler
* Syslog OMS portalında yapılandırması tüm özellikleri ve doğru günlük düzeyleri sahip olduğunu doğrulayın
  * **OMS portalı > ayarları > veri > Syslog**
* Bu yerel syslog arka plan programları Mesajlaşma doğrulayın (`rsyslog`, `syslog-ng`) yönlendirilmiş iletiler alabilir
* İletileri engellenmediğinden emin olmak için Syslog sunucusunda güvenlik duvarı ayarlarını kontrol edin
* OMS kullanarak bir Syslog iletisi benzetimini `logger` command - örneğin:
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-to-oms-when-using-a-proxy"></a>Bir proxy kullanılırken için OMS bağlantısı sorunları
#### <a name="probable-causes"></a>Olası nedenler
* Proxy aracısı yükleme ve yapılandırma yanlış olduğunda belirtilen
* OMS hizmet uç noktaları, veri merkezinizdeki whitelistested değildir

#### <a name="resolutions"></a>Çözümler
* Seçeneğiyle aşağıdaki komutu kullanarak Linux için OMS Aracısı'nı yeniden `-v` etkin. Bu OMS hizmetine proxy üzerinden bağlanma Aracısı'nın ayrıntılı çıktı sağlar.
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * OMS proxy belgelerini gözden [aracı kullanmak için bir HTTP proxy sunucusu yapılandırma](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)
* Aşağıdaki OMS hizmet uç noktalarına Güvenilenler listesine olduğunu doğrulayın

| Aracı Kaynağı | Bağlantı Noktaları |
| --- | --- |
| &#42;. ods.opinsights.Azure.com |Bağlantı noktası 443 |
| &#42;. OMS.opinsights.Azure.com |Bağlantı noktası 443 |
| ods.systemcenteradvisor.com |Bağlantı noktası 443 |
| &#42;.blob.core.windows.net/ |Bağlantı noktası 443 |

### <a name="a-403-error-is-displayed-when-onboarding"></a>Bir 403 hatası görüntülenir, ekleme
#### <a name="probable-causes"></a>Olası nedenler
* Tarih ve saat Linux sunucusu üzerinde yanlış
* Kullanılan çalışma alanı kimliği ve çalışma alanı anahtarı yanlış

#### <a name="resolution"></a>Çözüm
* Linux sunucunuzla zamanında doğrulayın `date` komutu. Veri değerinden büyük veya geçerli saatten az 15 dakika sonra ekleme başarısız olur. Bu sorunu gidermek için tarih ve/veya saat dilimi Linux sunucunuzun güncelleştirin.
* Bir zaman farkı ekleme hatasına neden oluyorsa Linux için OMS aracısının en son sürümünü sizi bilgilendirir
* RE-doğru çalışma alanı kimliği ve çalışma alanı anahtarı kullanarak yerleşik. Bkz: [komut satırını kullanarak Onboarding](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) daha fazla bilgi için.

### <a name="a-500-error-or-404-error-appears-in-the-log-file-after-onboarding"></a>500 hata veya 404 hatası günlük dosyasında ekleme sonra görünür.
Bu OMS çalışma alanına Linux verilerin ilk yükleme sırasında oluşan bilinen bir sorundur. Bu, gönderilen veriler ya da diğer sorunlar etkilemez. İlk defa hataları yoksayabilirsiniz ekleme.

### <a name="nagios-data-does-not-appear-in-the-oms-portal"></a>Nagios veriler OMS Portalı'nda görünmüyor
#### <a name="probable-causes"></a>Olası nedenler
* Omsagent kullanıcının Nagios günlük dosyasından okuma izni yok
* Nagios kaynak ve filtre bölümleri hala omsagent.conf dosyasında bırakılır

#### <a name="resolutions"></a>Çözümler
* Nagios dosyadan okunan için omsagent kullanıcı ekleyin. Bkz: [Nagios uyarıları](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) daha fazla bilgi için.
* Linux genel yapılandırma dosyasını OMS Aracısı içinde `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, emin olun **her ikisi de** açıklamaları kaldırılan, aşağıdaki örneğe benzer şekilde Nagios kaynak ve filtre bölümü vardır.

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


### <a name="linux-data-doesnt-appear-in-the-oms-portal"></a>Linux veri OMS Portalı'nda görünmüyor
#### <a name="probable-causes"></a>Olası nedenler
* OMS hizmetine ekleme başarısız oldu
* OMS hizmetine bağlantı engellendi
* Yedeklenen Linux veriler için OMS Aracısı.

#### <a name="resolutions"></a>Çözümler
* Doğrulayın, ekleme OMS hizmetine başarılı olduğunu doğrulayarak `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` bulunmaktadır.
* RE-omsadmin.sh komut satırını kullanarak yerleşik. Bkz: [komut satırını kullanarak Onboarding](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) daha fazla bilgi için.
* Bir proxy sunucu kullanıyorsanız, yukarıdaki adımları sorun giderme proxy kullanın
* Bazı durumlarda, Linux için OMS aracısının OMS hizmetiyle iletişim kuramadığında aracı veri 50 MB tam arabellek boyutunu yedeklenmiş. OMS Aracısı'nı çalıştırarak Linux için yeniden `/opt/microsoft/omsagent/bin/service_control restart` komutu.
  >[AZURE.NOTE] Aracı sürümü 1.1.0-28 ve daha sonra bu sorun düzeltilmiştir.

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-the-oms-portal"></a>Syslog Linux performans sayacı yapılandırması OMS portalında uygulanmaz
#### <a name="probable-causes"></a>Olası nedenler
* Linux için OMS aracısının yapılandırma aracısı en son yapılandırma OMS Portalı'ndan alınmamış.
* Değiştirilen ayarlar portalında uygulanmadı

#### <a name="resolutions"></a>Çözümler
`omsconfig`5 dakikada bir OMS portalı yapılandırma değişiklikleri alır Linux için OMS aracısının içinde yapılandırma aracısıdır. Linux yapılandırma dosyalarını konumunda bulunan için bu yapılandırma için OMS aracısının sonra uygulanır `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.

* Bazı durumlarda, Linux yapılandırma aracı için OMS Aracısı uygulanmıyor son yapılandırmasında kaynaklanan portal yapılandırma hizmetiyle iletişim mümkün olmayabilir.
* Doğrulayın `omsconfig` Aracısı, aşağıdakilerle yüklenir:

  * `dpkg --list omsconfig` veya `rpm -qi omsconfig`
  * Yüklü değilse, Linux için OMS aracısının en son sürümünü yeniden yükleyin
* Doğrulayın `omsconfig` agent OMS hizmetiyle iletişim

  * Çalıştırma `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` komutu
    * Yukarıdaki komut, bu aracı yapılandırmasını döndürür Syslog ayarları, Linux performans sayaçları ve özel günlükleri gibi portaldan alır.
    * Yukarıdaki komut başarısız olursa, çalıştırmak `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` komutu. Bu komut, en son yapılandırmayı almak için OMS hizmetiyle iletişim kurmak için omsconfig Aracısı zorlar.

### <a name="custom-linux-log-data-does-not-appear-in-the-oms-portal"></a>Özel Linux günlük verilerini OMS Portalı'nda görünmüyor
#### <a name="probable-causes"></a>Olası nedenler
* OMS hizmetine ekleme başarısız oldu
* **Aşağıdaki yapılandırmayı Linux Sunucularım uygulamak** ayarı seçilmediğinden
* omsconfig Portalı'ndan en son özel günlük yukarı çekilen değil
* `omsagent` Kullanılmasıdır izinlerle ilgili bir sorun nedeniyle özel günlük erişemiyor veya `omsagent` bulunamadı. Bu durumda, aşağıdaki çıkış görürsünüz:
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* Bu OMS Aracısı Linux sürüm 1.1.0-217 için düzeltildi yarış durumu ile ilgili bilinen bir sorun olduğu

#### <a name="resolutions"></a>Çözümler
* Belirleyerek, edildi başarıyla olduğunuz doğrulayın olup olmadığını `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` dosya yok.
  * Gerekli olduğunda, yerleşik yeniden omsadmin.sh komut satırını kullanarak. Bkz: [komut satırını kullanarak Onboarding](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) daha fazla bilgi için.
* OMS portalında altında **ayarları** üzerinde **veri** sekmesinde, emin **aşağıdaki yapılandırmayı Linux Sunucularım uygulamak** ayarı seçildiğinde  
  ![yapılandırmasını Uygula](./media/log-analytics-linux-agents/customloglinuxenabled.png)
* Doğrulayın `omsconfig` agent OMS hizmetiyle iletişim

  * Çalıştırma `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` komutu
  * Yukarıdaki komut, bu aracı yapılandırmasını döndürür Syslog ayarları, Linux performans sayaçları ve özel günlükleri gibi portaldan alır.
  * Yukarıdaki komut başarısız olursa, çalıştırmak `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` komutu. Bu komut, OMS hizmetiyle iletişim kurmak ve en son yapılandırmayı almak için omsconfig Aracısı zorlar.

Ayrıcalıklı bir kullanıcı olarak çalışan Linux kullanıcı için OMS aracısının yerine `root`, Linux için OMS aracısının çalışır `omsagent` kullanıcı. Çoğu durumda, açık kullanıcıya belirli dosyaları okumak için izni verilmesi gerekir.

İzni vermek için `omsagent` kullanıcı, aşağıdaki komutları çalıştırın:

1. Ekleme `omsagent` ile belirli bir grup kullanıcı`sudo usermod -a -G <GROUPNAME> <USERNAME>`
2. Gerekli dosyasıyla Evrensel okuma erişimi verin`sudo chmod -R ugo+rw <FILE DIRECTORY>`

Linux sürüm 1.1.0-217 için OMS Aracısı giderilmiştir yarış durumu ile ilgili bilinen bir sorun yoktur. En son aracı güncelleştirdikten sonra çıktı eklentisi son sürümünü almak için aşağıdaki komutu çalıştırın:

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a>Bilinen sınırlamaları
Linux için OMS Aracısı'nın geçerli sınırlamalar hakkında bilgi edinmek için aşağıdaki bölümleri gözden geçirin.

### <a name="azure-diagnostics"></a>Azure Tanılama
Azure'da çalışan Linux sanal makineleri için ek adımlar veri toplama izin vermek için Azure tanılama ve Operations Management Suite tarafından gerekebilir. **Sürüm 2.2** Linux tanılama uzantısını Linux için OMS Aracısı ile uyumluluk için gereklidir.

Yükleme ve Linux için tanılama uzantısını yapılandırma hakkında daha fazla bilgi için bkz: [Linux tanılama uzantısını etkinleştirmek için Azure CLI komutunu kullanın](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).

**Linux tanılama uzantısını 2.2 Azure CLI ASM 2. 0'ı yükseltme:**

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

**ARM**

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

Bu komut örnekleri PrivateConfig.json adlı bir dosyaya başvuru. Bu dosya biçiminin aşağıdaki örneğe benzemelidir.

```
    {
    "storageAccountName":"the storage account to receive data",
    "storageAccountKey":"the key of the account"
    }
```

### <a name="sysklog-is-not-supported"></a>Sysklog desteklenmiyor
Rsyslog veya syslog ng syslog iletileri toplamak için gereklidir. Red Hat Enterprise Linux, CentOS ve Oracle Linux sürümü (sysklog) 5 sürümünü varsayılan syslog arka plan syslog olay toplaması için desteklenmiyor. Bu dağıtımları bu sürümünden Syslog verileri toplamak için rsyslog arka plan programı yüklenmeli ve sysklog değiştirmek için yapılandırılmalıdır. Sysklog rsyslog ile değiştirerek daha fazla bilgi için bkz: [yeni oluşturulan rsyslog RPM yüklemek](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).

## <a name="next-steps"></a>Sonraki Adımlar
* İşlev eklemek ve veri toplamak için bkz. [Çözüm Galerisinden Log Analytics çözümleri ekleme](log-analytics-add-solutions.md).
* Çözümler tarafından toplanan ayrıntılı bilgileri görüntülemek için [günlük aramaları](log-analytics-log-searches.md) hakkında bilgi edinin.
* Özel aramalarınızı kaydetmek ve görüntülemek için [panolar](log-analytics-dashboards.md)ı kullanın.
