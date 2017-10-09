---
title: "aaaCollect ve OMS günlük analizi Syslog iletileri analiz | Microsoft Docs"
description: "Syslog ortak tooLinux olan bir olay günlüğü protokolüdür. Bu makalede nasıl günlük analizi Syslog iletileri tooconfigure koleksiyonunu ve hello kayıtları ayrıntılarını hello OMS deposunda oluşturdukları açıklanmaktadır."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 8bfa0bca3f2f18287d1352c98bbaa2a70e41e276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a>Syslog veri kaynaklarında günlük analizi
Syslog ortak tooLinux olan bir olay günlüğü protokolüdür.  Uygulamaları hello yerel makine üzerinde depolanan olabilir veya tooa Syslog Toplayıcı teslim iletileri gönderir.  Merhaba Linux için OMS Aracısı yüklendiğinde hello yerel Syslog arka plan programı tooforward iletileri toohello aracı yapılandırır.  Merhaba aracı karşılık gelen bir kayıt hello OMS deposunda oluşturulduğu hello ileti tooLog Analytics sonra gönderir.  

> [!NOTE]
> Günlük analizi rsyslog hello varsayılan arka plan programı olduğu rsyslog veya syslog-ng tarafından gönderilen iletileri koleksiyonu destekler. Red Hat Enterprise Linux, CentOS ve Oracle Linux sürümü (sysklog) 5 sürümünü Hello varsayılan syslog arka plan syslog olay toplaması için desteklenmiyor. Bu sürümü bu dağıtımları toocollect syslog verileri hello [rsyslog arka plan programı](http://rsyslog.com) yüklü olmalıdır ve tooreplace sysklog yapılandırılır.
>
>

![Syslog koleksiyonu](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a>Syslog yapılandırma
Merhaba Linux için OMS aracısının yalnızca hello tesis ve yapılandırmasıyla belirtilen önem derecelerine sahip olayları toplar.  Syslog hello OMS portalı üzerinden veya Linux aracıları yapılandırma dosyalarını yönetme tarafından yapılandırabilirsiniz.

### <a name="configure-syslog-in-hello-oms-portal"></a>Syslog hello OMS portalında yapılandırın
Syslog hello yapılandırma [günlük analizi ayarları veri menüde](log-analytics-data-sources.md#configuring-data-sources).  Bu yapılandırma her Linux Aracısı toohello yapılandırma dosyası teslim edilir.

Adını yazıp'yi tıklatarak yeni bir tesis ekleyebilirsiniz  **+** .  Her özelliği için seçilen hello önem derecelerine sahip yalnızca iletileri toplanacaktır.  Merhaba önem derecelerine toocollect istediğiniz hello belirli olanağı için denetleyin.  Herhangi bir ek ölçütü toofilter iletileri sağlayamaz.

![Syslog yapılandırın](media/log-analytics-data-sources-syslog/configure.png)

Varsayılan olarak, tüm yapılandırma değişiklikleri otomatik olarak tooall aracıları gönderilir.  Her Linux aracısında el ile tooconfigure Syslog istiyorsanız hello kutunun işaretini *aşağıdaki yapılandırma toomy Linux makineler Uygula*.

### <a name="configure-syslog-on-linux-agent"></a>Syslog Linux Aracısı'nı yapılandırma
Ne zaman hello [OMS Aracısı Linux istemcide yüklü](log-analytics-linux-agents.md)hello tesis tanımlayan bir varsayılan syslog yapılandırma dosyası yükler ve önem derecesi hello iletileri toplanır.  Bu dosya toochange hello yapılandırmasını değiştirebilirsiniz.  Merhaba yapılandırma dosyası istemci hello arka plan programı yüklediği Syslog hello bağlı olarak farklılık gösterir.

> [!NOTE]
> Merhaba syslog yapılandırma düzenlerseniz, hello değişiklikleri tootake etkisi hello syslog arka plan yeniden başlatmanız gerekir.
>
>

#### <a name="rsyslog"></a>rsyslog
Merhaba rsyslog için yapılandırma dosyası bulunur **/etc/rsyslog.d/95-omsagent.conf**.  Varsayılan içeriğini aşağıda verilmiştir.  Bu, uyarı ya da daha yüksek bir düzeyinde tüm tesisler için yerel hello Aracısı'ndan gönderilen syslog iletileri toplar.

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

Kendi hello yapılandırma dosyası bölümünü kaldırarak bir tesis kaldırabilirsiniz.  Bu tesis 's girdisini değiştirerek belirli olanağını toplanan hello önem derecelerine sınırlayabilirsiniz.  Örneğin, toolimit hello kullanıcı tesis toomessages hata veya daha büyük bir önem derecesi aşağıdaki hello yapılandırma dosyası toohello satırını değiştirirsiniz:

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a>Syslog ng
syslog ng Hello yapılandırma dosyası olduğu konumda **/etc/syslog-ng/syslog-ng.conf**.  Varsayılan içeriğini aşağıda verilmiştir.  Tüm Tesisler ve tüm önem dereceleridir için yerel hello Aracısı'ndan gönderilen syslog iletileri toplar.   

    #
    # Warnings (except iptables) in one file:
    #
    destination warn { file("/var/log/warn" fsync(yes)); };
    log { source(src); filter(f_warn); destination(warn); };

    #OMS_Destination
    destination d_oms { udp("127.0.0.1" port(25224)); };

    #OMS_facility = auth
    filter f_auth_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(auth); };
    log { source(src); filter(f_auth_oms); destination(d_oms); };

    #OMS_facility = authpriv
    filter f_authpriv_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(authpriv); };
    log { source(src); filter(f_authpriv_oms); destination(d_oms); };

    #OMS_facility = cron
    filter f_cron_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(cron); };
    log { source(src); filter(f_cron_oms); destination(d_oms); };

    #OMS_facility = daemon
    filter f_daemon_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(daemon); };
    log { source(src); filter(f_daemon_oms); destination(d_oms); };

    #OMS_facility = kern
    filter f_kern_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(kern); };
    log { source(src); filter(f_kern_oms); destination(d_oms); };

    #OMS_facility = local0
    filter f_local0_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local0); };
    log { source(src); filter(f_local0_oms); destination(d_oms); };

    #OMS_facility = local1
    filter f_local1_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local1); };
    log { source(src); filter(f_local1_oms); destination(d_oms); };

    #OMS_facility = mail
    filter f_mail_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(mail); };
    log { source(src); filter(f_mail_oms); destination(d_oms); };

    #OMS_facility = syslog
    filter f_syslog_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(syslog); };
    log { source(src); filter(f_syslog_oms); destination(d_oms); };

    #OMS_facility = user
    filter f_user_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };

Kendi hello yapılandırma dosyası bölümünü kaldırarak bir tesis kaldırabilirsiniz.  Belirli bir özellik için listeden kaldırarak toplanır hello önem derecelerine sınırlayabilirsiniz.  Örneğin, toolimit hello kullanıcı tesis toojust uyarı ve kritik iletileri aşağıdaki hello yapılandırma dosyası toohello ilgili bölümünü değiştirmek:

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a>Ek Syslog bağlantı noktalarından verileri toplama
Merhaba OMS Aracısı Syslog iletileri hello yerel istemci 25224 bağlantı noktasında dinler.  Merhaba Aracısı yüklendiğinde varsayılan syslog yapılandırması uygulanan ve konumu aşağıdaki hello bulundu:

* Rsyslog:`/etc/rsyslog.d/95-omsagent.conf`
* Syslog-ng:`/etc/syslog-ng/syslog-ng.conf`

İki yapılandırma dosyası oluşturarak başlangıç bağlantı noktası numarasını değiştirebilirsiniz: FluentD yapılandırma dosyası ve bir rsyslog veya syslog ng dosyası hello Syslog arka plan programı yüklediğiniz bağlı olarak.  

* Merhaba FluentD yapılandırma dosyasında bulunan yeni bir dosya olmalıdır: `/etc/opt/microsoft/omsagent/conf/omsagent.d` ve hello hello değerinde değiştirme **bağlantı noktası** giriş, özel bir bağlantı noktası numarasına sahip.

        <source>
          type syslog
          port %SYSLOG_PORT%
          bind 127.0.0.1
          protocol_type udp
          tag oms.syslog
        </source>
        <filter oms.syslog.**>
          type filter_syslog
        </filter>

* Rsyslog için bulunan yeni bir yapılandırma dosyası oluşturmanız gerekir: `/etc/rsyslog.d/` ve hello % SYSLOG_PORT % değerini, özel bir bağlantı noktası numarasıyla değiştirin.  

    > [!NOTE]
    > Merhaba yapılandırma dosyasında bu değeri değiştirirseniz, `95-omsagent.conf`, hello Aracısı varsayılan bir yapılandırma uyguladığında üzerine yazılır.
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* Merhaba syslog ng config aşağıda gösterilen hello örnek yapılandırma kopyalayarak değiştirilmesi gerektiğini ve bulunan hello syslog ng.conf yapılandırma dosyasının sonuna hello özel değiştirilen ayarlar toohello ekleme `/etc/syslog-ng/`.  Yapmak **değil** hello varsayılan etiket **% WORKSPACE_ID % _oms** veya **% WORKSPACE_ID_OMS**, özel tanımlama etiket toohelp yaptığınız değişiklikleri ayırt etmek.  

    > [!NOTE]
    > Hello yapılandırma dosyasındaki hello varsayılan değerleri değiştirirseniz, varsayılan bir yapılandırma hello Aracısı geçerli olduğu durumlarda bunların üzerine yazılacak.
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

Merhaba değişiklikler, hello Syslog ve hello tamamladıktan sonra OMS Aracısı hizmeti yeniden toobe tooensure hello yapılandırma değişiklikleri etkinleştirilmesi gerekir.   

## <a name="syslog-record-properties"></a>Syslog kaydı Özellikler
Syslog kayıtları sahip bir tür **Syslog** ve aşağıdaki tablonun hello hello özelliklere sahiptir.

| Özellik | Açıklama |
|:--- |:--- |
| Bilgisayar |Olay hello bilgisayar toplandığı. |
| Tesis |Merhaba selamlama iletisine oluşturulan hello sisteminin parçası tanımlar. |
| HostIP |Merhaba ileti gönderme hello sistem IP adresi. |
| Ana bilgisayar adı |Merhaba ileti gönderme hello sistem adı. |
| Önem düzeyi |Merhaba olay önem derecesi. |
| SyslogMessage |Merhaba ileti metni. |
| İşlem kimliği |Selamlama iletisine oluşturulan hello işlemin kimliği. |
| EventTime |Tarih ve saat olay hello üretilmiştir. |

## <a name="log-queries-with-syslog-records"></a>Syslog kayıtlarla günlük sorguları
Hello aşağıdaki tabloda, Syslog kayıtları almak günlük sorgularının farklı örnekler verilmektedir.

| Sorgu | Açıklama |
|:--- |:--- |
| Türü Syslog = |Tüm Syslog modüllerini. |
| Türü Syslog önem düzeyi = hata = |Tüm Syslog kayıtları hata önem derecesi. |
| Tür = Syslog &#124; Bilgisayar tarafından ölçü Count() işlevi |Bilgisayar tarafından sayısı, Syslog kaydeder. |
| Tür = Syslog &#124; Ölçü count() tesis tarafından |Tesis tarafından sayısı, Syslog kaydeder. |

>[!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sorguları yukarıda hello toohello aşağıdaki değişeceğinden sonra.

> | Sorgu | Açıklama |
|:--- |:--- |
| Syslog |Tüm Syslog modüllerini. |
| Syslog &#124; Burada önem düzeyi "error" == |Tüm Syslog kayıtları hata önem derecesi. |
| Syslog &#124; AggregatedValue özetlemek bilgisayar tarafından count() = |Bilgisayar tarafından sayısı, Syslog kaydeder. |
| Syslog &#124; AggregatedValue özetlemek tesis tarafından count() = |Tesis tarafından sayısı, Syslog kaydeder. |

## <a name="next-steps"></a>Sonraki adımlar
* Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) tooanalyze hello veri toplanan veri kaynakları ve çözümler.
* Kullanım [özel alanlar](log-analytics-custom-fields.md) syslog kayıtları tek tek alanlara tooparse verileri.
* [Linux aracılarını yapılandırma](log-analytics-linux-agents.md) toocollect diğer veri türleri.
