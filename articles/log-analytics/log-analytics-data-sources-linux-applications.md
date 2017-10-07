---
title: "aaaCollect Linux uygulama performansını OMS günlük analizi | Microsoft Docs"
description: "Bu makalede, MySQL ve Apache HTTP Server için Linux toocollect performans sayaçları için OMS aracısının hello yapılandırma ayrıntıları sağlar."
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
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 51105c6add5c7941a004570a76a4d94c02fc8a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-performance-counters-for-linux-applications-in-log-analytics"></a>Günlük analizi Linux uygulamaları için performans sayaçlarını Topla 
Bu makalede hello yapılandırmak için Ayrıntılar sunulmaktadır [Linux için OMS aracısının](https://github.com/Microsoft/OMS-Agent-for-Linux) toocollect performans sayaçları belirli uygulamalar için.  Bu makalede bulunan hello uygulamalar şunlardır:  

- [MySQL](#MySQL)
- [Apache HTTP Server](#apache-http-server)

## <a name="mysql"></a>MySQL
Merhaba OMS Aracısı yüklendiğinde MySQL Server veya MariaDB Server hello bilgisayarında algılanırsa, bir performans izleme sağlayıcısı MySQL sunucusu için otomatik olarak yüklenir. Bu sağlayıcı toohello yerel MySQL/MariaDB sunucu tooexpose performans istatistikleri bağlanır. MySQL kullanıcı kimlik bilgilerini Hello sağlayıcısı hello MySQL Server erişebilmesi için yapılandırılması gerekir.

### <a name="configure-mysql-credentials"></a>MySQL kimlik bilgilerini yapılandırın
Merhaba MySQL OMI sağlayıcısı önceden yapılandırılmış bir MySQL kullanıcının gerektiren ve MySQL istemci kitaplıkları sipariş tooquery hello performans ve sistem durumu bilgilerini hello MySQL örneğinden yüklenir.  Bu kimlik bilgileri hello Linux Aracısı'nı depolanan bir kimlik doğrulama dosyasında depolanır.  Hangi bağlama adresini Hello kimlik doğrulama dosyasını belirtir ve bağlantı noktası hello MySQL örneğine dinlediği ve ne toouse toogather ölçümleri kimlik bilgileri.  

Linux hello MySQL OMI Merhaba OMS Aracısı yüklenmesi sırasında sağlayıcısı MySQL my.cnf yapılandırma dosyalarını (varsayılan konumları) bağ adresi ve bağlantı noktası kümesi hello MySQL OMI kimlik doğrulama dosyasını için ve kısmen tarar.

Merhaba MySQL kimlik doğrulama dosyasını şurada saklanır `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`.


### <a name="authentication-file-format"></a>Kimlik doğrulama dosya biçimi
Merhaba biçimidir hello MySQL OMI kimlik doğrulaması dosyası için aşağıdaki

    [Port]=[Bind-Address], [username], [Base64 encoded Password]
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    AutoUpdate=[true|false]

Aşağıdaki tablonun hello Hello giriş hello kimlik doğrulaması dosyası açıklanmaktadır.

| Özellik | Açıklama |
|:--|:--|
| Bağlantı noktası | Merhaba geçerli bağlantı noktası hello örneğinin dinlediği MySQL temsil eder. Bağlantı noktası 0 hello özellikler aşağıdaki varsayılan örnek için kullanıldığını belirtir. |
| Bağ adresi| Geçerli MySQL bağlama-adresi. |
| kullanıcı adı| MySQL kullanıcı toouse toomonitor hello MySQL server örneği kullanılır. |
| Parola Base64 ile kodlanmış| Base64 ile kodlanmış hello MySQL izleme kullanıcının parolası. |
| Otomatik güncelleştirme| İçin toorescan hello my.cnf dosyasında değiştirilip değiştirilmediğini belirtir ve hello MySQL OMI sağlayıcı yükseltildiğinde hello MySQL OMI kimlik doğrulaması dosyanın üzerine yazın. |

### <a name="default-instance"></a>Varsayılan örneği
Merhaba MySQL OMI kimlik doğrulama dosyasını varsayılan örneği ve bağlantı noktası numarası toomake daha kolay bir Linux ana bilgisayarda birden çok MySQL örneklerini yönetme tanımlayabilirsiniz.  Merhaba varsayılan örneği, bağlantı noktası 0 ile bir örneği tarafından belirtilir. Tüm ek örnekleri farklı değerler belirtilmedikçe hello varsayılan örneğinden ayarlanan özellikleri devralır. Örneğin, '3308' numaralı bağlantı noktasını dinlemeye MySQL örneği eklediyseniz, hello varsayılan örneğinin bağ adresi, kullanıcı adı ve Base64 ile kodlanmış parola kullanılan tootry olması ve 3308 üzerinde dinleme hello örneği izleme. 3308 Hello örneğinde ilişkili tooanother adresidir ve kullanıyorsa hello aynı MySQL kullanıcı adı ve parola çifti yalnızca hello bağ adresi gereklidir ve hello diğer özellikleri devralınır.

Aşağıdaki tablonun hello örnek örneği ayarlara sahip 

| Açıklama | Dosya |
|:--|:--|
| Varsayılan örneği ve bağlantı noktası 3308 ile örneği. | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=, ,`<br>`AutoUpdate=true` |
| Varsayılan örneği ve bağlantı noktası 3308 ve farklı bir kullanıcı adı ve parola ile örneği. | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=127.0.1.1, myuser2,cGluaGVhZA==`<br>`AutoUpdate=true` |


### <a name="mysql-omi-authentication-file-program"></a>MySQL OMI kimlik doğrulaması dosya programı
Merhaba MySQL OMI başlangıç yüklemesinde ile kullanılan tooedit hello MySQL OMI kimlik doğrulama dosyasını olabilen bir MySQL OMI kimlik doğrulaması dosya programı sağlayıcıdır. Merhaba kimlik doğrulaması dosya programı konumu aşağıdaki hello bulunabilir.

    /opt/microsoft/mysql-cimprov/bin/mycimprovauth

> [!NOTE]
> Merhaba kimlik bilgileri dosyası hello omsagent hesabı tarafından okunabilir olması gerekir. Omsgent Hello mycimprovauth komutunun çalıştırılması önerilir.

Merhaba aşağıdaki tabloda Ayrıntılar hello sözdizimine mycimprovauth kullanımı sağlar.

| İşlem | Örnek | Açıklama
|:--|:--|:--|
| Otomatik güncelleştirme * false\|TRUE * | mycimprovauth otomatik güncelleştirme false | Desteklemediğini hello kimlik doğrulama dosyasını otomatik olarak güncelleştirilecek kümeleri üzerinde yeniden başlatın veya güncelleştirin. |
| Varsayılan *bağ adresi kullanıcı adı parolası* | mycimprovauth varsayılan 127.0.0.1 kök pwd | Ayarlar hello MySQL OMI kimlik doğrulama dosyasını varsayılan örneğinde hello.<br>Merhaba parola alanı düz metin olarak girilmelidir - hello MySQL OMI kimlik doğrulama dosyasını hello Parolada Base 64 kodlu olacaktır. |
| silme * default\|port_num * | mycimprovauth 3308 | Merhaba belirtilen örneği ya da varsayılan olarak veya bağlantı noktası numarasına göre siler. |
| Yardım | mycimprov Yardım | Komutları toouse listesini yazdırır. |
| Yazdırma | mycimprov yazdırma | Kolay bir tooread MySQL OMI kimlik doğrulama dosyasını yazdırır. |
| port_num güncelleştirme *bağ adresi kullanıcı adı parolası* | mycimprov güncelleştirme 3307 127.0.0.1 kök pwd | Merhaba belirtilen örneğini güncelleştirir veya henüz yoksa hello örneği ekler. |

Merhaba aşağıdaki örnek komutlar hello MySQL sunucusu için varsayılan bir kullanıcı hesabı üzerinde localhost tanımlayın.  Merhaba parola alanı düz metin olarak girilmelidir - hello MySQL OMI kimlik doğrulama dosyasını hello Parolada Base 64 kodlu olacaktır

    sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>'
    sudo /opt/omi/bin/service_control restart

### <a name="database-permissions-required-for-mysql-performance-counters"></a>MySQL performans sayaçları için gereken veritabanı izinleri
MySQL kullanıcı Hello sorguları toocollect MySQL sunucusu performans verilerini izleyen erişim toohello gerektirir. 

    SHOW GLOBAL STATUS;
    SHOW GLOBAL VARIABLES:


Merhaba MySQL kullanıcı aynı zamanda varsayılan tabloları aşağıdaki SELECT erişim toohello gerektirir.

- INFORMATION_SCHEMA
- MySQL. 

Bu ayrıcalıkları verme komutları aşağıdaki hello çalıştırarak verilebilir.

    GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
    GRANT SELECT ON mysql.* too‘monuser’@’localhost’;


> [!NOTE]
> toogrant izinleri tooa kullanıcı verme kullanıcı hello izleme MySQL verilmeden hello ayrıcalık yanı sıra hello 'GRANT option' ayrıcalığına sahip olmalıdır.

### <a name="define-performance-counters"></a>Performans sayaçları tanımlayın

Linux toosend veri tooLog analizi için OMS aracısının hello yapılandırdıktan sonra hello performans sayaçları toocollect yapılandırmanız gerekir.  Merhaba yordamı kullanın [Windows ve Linux performans veri kaynaklarında günlük analizi](log-analytics-data-sources-windows-events.md) aşağıdaki tablonun hello hello sayaçlarla.

| Nesne adı | Sayaç adı |
|:--|:--|
| MySQL Veritabanı | Disk alanı bayt |
| MySQL Veritabanı | Tablolar |
| MySQL sunucusu | Bağlantı durduruldu Pct |
| MySQL sunucusu | Bağlantı kullanım yüzdesi |
| MySQL sunucusu | Disk alanı kullanımını bayt |
| MySQL sunucusu | Tam tablo tarama Pct |
| MySQL sunucusu | Pct InnoDB arabellek havuzu ulaştı. |
| MySQL sunucusu | InnoDB arabellek havuzu kullanım yüzdesi |
| MySQL sunucusu | InnoDB arabellek havuzu kullanım yüzdesi |
| MySQL sunucusu | Anahtar önbelleği isabet yüzdesi |
| MySQL sunucusu | Anahtar önbelleği kullanım yüzdesi |
| MySQL sunucusu | Anahtar önbelleği yazma Pct |
| MySQL sunucusu | Sorgu önbellek isabet yüzdesi |
| MySQL sunucusu | Sorgu önbellek ayıklar Pct |
| MySQL sunucusu | Sorgu önbellek kullanım yüzdesi |
| MySQL sunucusu | Tablo önbelleği isabet yüzdesi |
| MySQL sunucusu | Tablo Önbellek kullanım yüzdesi |
| MySQL sunucusu | Tablo kilit çekişmesini Pct |

## <a name="apache-http-server"></a>Apache HTTP Server 
Hello omsagent paketi yüklendiğinde, Apache HTTP Server hello bilgisayarında algılanırsa, bir performans izlemesi için Apache HTTP Server sağlayıcısı otomatik olarak yüklenir. Bu sağlayıcı hello Apache HTTP Server sipariş tooaccess performans verilerini içine yüklenmesi gereken bir Apache modülü kullanır. Merhaba modülü komutu aşağıdaki hello ile yüklenebilir:
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

komutu aşağıdaki hello çalıştırmak toounload hello Apache izleme Modülü'nü:
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```

### <a name="define-performance-counters"></a>Performans sayaçları tanımlayın

Linux toosend veri tooLog analizi için OMS aracısının hello yapılandırdıktan sonra hello performans sayaçları toocollect yapılandırmanız gerekir.  Merhaba yordamı kullanın [Windows ve Linux performans veri kaynaklarında günlük analizi](log-analytics-data-sources-windows-events.md) aşağıdaki tablonun hello hello sayaçlarla.

| Nesne adı | Sayaç adı |
|:--|:--|
| Apache HTTP Server | Meşgul çalışanların |
| Apache HTTP Server | Boşta çalışan |
| Apache HTTP Server | PCT meşgul çalışanların |
| Apache HTTP Server | Toplam Pct CPU |
| Apache sanal ana bilgisayar | Dakikada - istemci hataları |
| Apache sanal ana bilgisayar | Dakikada - sunucu hataları |
| Apache sanal ana bilgisayar | İstek başına KB |
| Apache sanal ana bilgisayar | Saniye başına istek KB |
| Apache sanal ana bilgisayar | Saniye başına istek sayısı |



## <a name="next-steps"></a>Sonraki adımlar
* [Performans sayaçlarını Topla](log-analytics-data-sources-performance-counters.md) Linux aracılardan gelen.
* Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) tooanalyze hello veri toplanan veri kaynakları ve çözümler. 
