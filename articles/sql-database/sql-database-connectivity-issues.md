---
title: "aaaFix SQL bağlantı hatası, geçici hata | Microsoft Docs"
description: "Nasıl tootroubleshoot, tanılama ve SQL bağlantı hatası veya Azure SQL veritabanındaki geçici hata önlemek öğrenin. "
keywords: "SQL bağlantısı, bağlantı dizesi, bağlantı sorunları, geçici bir hata oluştu, bağlantı hatası"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: efb35451-3fed-4264-bf86-72b350f67d50
ms.service: sql-database
ms.custom: develop apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: d225e610b9e88170ab53ca16d615bd07220603cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a>SQL Database için SQL bağlantı hatalarını ve geçici hataları giderme, tanılama ve önleme
Bu makalede nasıl tooprevent, sorun giderme, tanılama ve bağlantı hataları ve Azure SQL veritabanı ile etkileşim kurarken, istemci uygulamanız karşılaştığında geçici hataları etkisini açıklar. Nasıl tooconfigure mantığı yeniden dene, hello bağlantı dizesi oluşturma ve diğer bağlantı ayarlarını öğrenin.

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a>Geçici hataları geçici
Geçici bir hata - Ayrıca, geçici hata - kendisini yakında çözümleyecek bir temel nedeni vardır. Hello Azure sistem çeşitli iş yükleri donanım kaynakları toobetter Yük Dengelemesi hızla geçtiğinde geçici hataları zaman zaman bir nedenidir. Bu yeniden yapılandırma olayları çoğunu genellikle 60 saniyeden daha kısa bir süre içinde tamamlayın. Bu yeniden yapılandırma zaman aralığı sırasında bağlantısına sahip olabilir tooAzure SQL veritabanı verir. SQL veritabanı olmalıdır tooAzure bağlanan uygulamaları yerleşik tooexpect bu geçici hataları işleme mantığı toousers uygulama hataları olarak görünmesini yerine kendi kodunda bunları uygulayarak yeniden deneyin.

İstemci programınız ADO.NET kullanıyorsanız, programınız tarafından hello throw hello geçici hata hakkında işe bir **SqlException**. Merhaba **numarası** özelliği, geçici hataları hello konunun hello üstüne yakın hello listesi karşı karşılaştırılabilir: [SQL Database istemci uygulamaları için SQL hata kodları](sql-database-develop-error-messages.md).

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a>Bağlantı komutu karşılaştırması
Merhaba SQL bağlantısı yeniden deneyin veya hello aşağıdaki bağlı olarak yeniden kurmak:

* **Bir bağlantı try sırasında geçici bir hata oluşur**: hello bağlantı yeniden geciktirme birkaç saniye sonra.
* **Bir SQL sorgu komutu sırasında geçici bir hata oluşur**: hello komutu değil hemen yeniden. Bunun yerine, bir gecikmeden sonra hello bağlantı istemcinin yeniden kurulmalıdır. Ardından hello komutu yeniden denenebilir.

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a>Geçici hatalar için yeniden deneme mantığı
Yeniden deneme mantığı içerdiğinde bazen geçici bir hatayla karşılaşırsanız istemci programları daha sağlamdır.

Programınızı 3 bir taraf ara yazılımı Azure SQL veritabanı ile iletişim kurduğunda, geçici hataları yeniden deneme mantığı hello Ara içerip içermediğini hello satıcıyla sorgulayın.

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a>Yeniden deneme ilkelerini
* Merhaba geçici bir hatadır, bir bağlantı girişimi tooopen denenmeli.
* Geçici bir hata ile başarısız olan bir SQL SELECT deyimi doğrudan denenmeli değil.
  
  * Bunun yerine, yeni bir bağlantı kurmak ve hello seçin yeniden deneyin.
* Bir SQL UPDATE deyimi geçici bir hata ile başarısız olduğunda, güncelleştirme denenen hello önce yeni bir bağlantı kurulmalıdır.
  
  * Merhaba yeniden deneme mantığı hello tüm veritabanı işlem tamamlandı ya da bu hello işlemin tamamını geri alınır emin olmalısınız.

#### <a name="other-considerations-for-retry"></a>Yeniden deneme ile diğer değerlendirmeler
* Çalışma saatlerinden sonra otomatik olarak başlatılır ve sabah önce tamamlanır toplu iş programı toovery hasta uzun zaman aralıklarına kendi yeniden deneme girişimleri arasındaki ile destekleyebilir.
* Bir kullanıcı arabirimi programı hello İnsan eğilimi toogive için yukarı sonra çok uzun bekleme hesabı.
  
  * Ancak, bu ilkeyi istekleri hello sistemiyle bölgesini doldurmak için hello çözüm tooretry her birkaç saniyede olmamalıdır.

#### <a name="interval-increase-between-retries"></a>Denemeler arasındaki aralığı artırma
İlk, yeniden denemeden önce 5 saniye gecikme öneririz. 5 saniyeden daha kısa bir gecikme sonrasında yeniden deneniyor zorlamayı hello bulut hizmeti risklerini. Sonraki denemeler hello gecikme katlanarak, tooa 60 saniye olarak en fazla büyümesini.

Merhaba tartışması *engelleme süresi* ADO.NET kullanan istemciler için kullanılabilir [SQL Server bağlantı havuzu (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).

Merhaba programı otomatik olarak kapatılmadan önce tooset bir yeniden deneme sayısı da isteyebilirsiniz.

#### <a name="code-samples-with-retry-logic"></a>Yeniden deneme mantığı ile kod örnekleri
Kod örnekleri programlama dilleri, çeşitli yeniden deneme mantığı ile şu konumda mevcuttur:

* [SQL Database ve SQL Server için bağlantı kitaplıkları](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a>Yeniden deneme mantığı test
tootest, yeniden deneme mantığı benzetimini yapmak veya gerekir programınızı çalışmaya devam ederken düzeltilebilir daha hataya neden.

##### <a name="test-by-disconnecting-from-hello-network"></a>Merhaba ağ bağlantısını keserek test
Yeniden deneme mantığı sınayabilirsiniz bir hello istemci bilgisayarından ağ hello program çalışırken toodisconnect yoludur. Merhaba hata olacaktır:

* **SqlException.Number** 11001 =
* İleti: "gibi bir ana makine bilinmiyor"

Merhaba parçası ilk yeniden deneme girişimi gibi programınızı hello yazım hatası düzeltin ve tooconnect dener.

programınızı başlamadan önce bu pratik toomake, hello ağ bilgisayarınızdan çıkarın. Ardından, programı hello programına neden olan bir çalışma zamanı parametre tanır:

1. Geçici hatalar tooconsider 11001 tooits listesi geçici ekleyin.
2. İlk bağlantı her zamanki gibi çalışır.
3. Merhaba hata belirledi sonra 11001 hello listesinden kaldırır.
4. Merhaba kullanıcı tooplug hello bilgisayar hello ağınıza anlatan bir ileti görüntüler.
   * Daha fazla yürütme ya da hello kullanarak duraklatmak **Console.ReadLine** yöntemi veya bir iletişim kutusunda Tamam düğmesi. Merhaba bilgisayar hello ağa takılı sonra hello kullanıcı hello Enter tuşuna basar.
5. Başarı bekleniyor tooconnect, yeniden deneyin.

##### <a name="test-by-misspelling-hello-database-name-when-connecting"></a>Bağlanırken yazım hatası hello veritabanı adına göre test etme
Programınızı kasıtlı olarak, hata hello ilk bağlantı denemesine önce hello kullanıcı adı hatalı. Merhaba hata olacaktır:

* **SqlException.Number** 18456 =
* İleti: "'WRONG_MyUserName' kullanıcı için oturum açma başarısız."

Merhaba parçası ilk yeniden deneme girişimi gibi programınızı hello yazım hatası düzeltin ve tooconnect dener.

Bu pratik toomake, programınızı hello programına neden olan bir çalışma zamanı parametre tanı:

1. Geçici hatalar tooconsider 18456 tooits listesi geçici ekleyin.
2. Kasıtlı olarak 'WRONG_' toohello kullanıcı adını ekleyin.
3. Merhaba hata belirledi sonra 18456 hello listesinden kaldırır.
4. 'WRONG_' hello kullanıcı adından kaldırın.
5. Başarı bekleniyor tooconnect, yeniden deneyin.

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a>Bağlantı yeniden deneme için .NET SqlConnection parametreleri
İstemci programınız tootooAzure SQL veritabanı hello .NET Framework sınıf kullanarak bağlanıyorsa **System.Data.SqlClient.SqlConnection**, .NET 4.6.1 kullanması gereken veya daha sonra (veya .NET Core), bağlantı yeniden deneme özelliğinden yararlanabilirsiniz şekilde. Merhaba özelliğinin ayrıntıları [burada](http://go.microsoft.com/fwlink/?linkid=393996).

<!--
2015-11-30, FwLink 393996 points toodn632678.aspx, which links tooa downloadable .docx related tooSqlClient and SQL Server 2014.
-->


Merhaba oluşturduğunuzda [bağlantı dizesi](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) için **SqlConnection** nesne hello değerler şu parametreler hello arasında koordine:

* ConnectRetryCount &nbsp; &nbsp; *(varsayılan değer 1. Aralık 0 ile 255'dır.)*
* ConnectRetryInterval &nbsp; &nbsp; *(varsayılan değer 1 saniye. 1 ile 60 aralıktır.)*
* Bağlantı zaman aşımı &nbsp; &nbsp; *(varsayılan değer 15 saniye. Aralık 0 ile 2147483647'dır)*

Özellikle, seçilen değerlerinizi eşitlik true aşağıdaki hello olmanız gerekir:

* Bağlantı zaman aşımı ConnectRetryCount = * ConnectionRetryInterval

Örneğin, hello sayılacak = 3 ve aralığı 29 saniye oldukça hello sistem kendi 3 ve son yeniden bağlanma sırasında yeterli süre verirsiniz değil yalnızca = 10 saniye, bir zaman aşımı süresi: 29 < 3 * 10.

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a>Bağlantı komutu karşılaştırması
Merhaba **ConnectRetryCount** ve **ConnectRetryInterval** parametreleri sağlar, **SqlConnection** nesnesi yeniden deneme hello bağlantı işlemini belirten veya rahatsız etme, program, Denetim tooyour programı döndürme gibi. Merhaba deneme hello aşağıdaki durumlarda oluşabilir:

* mySqlConnection.Open yöntem çağrısı
* mySqlConnection.Execute yöntem çağrısı

Bir subtlety yoktur. Geçici bir hata oluşursa karşın, *sorgu* yürütülmekte olan, **SqlConnection** nesne değil yeniden deneme hello işlemi bağlanıyor ve bunu kesinlikle sorgunuzu yeniden denemez. Ancak, **SqlConnection** denetimleri sorgu yürütme için göndermeden önce bağlantı çok hızlı bir şekilde hello. Bir bağlantı sorunu Hello hızlı onay algılarsa, **SqlConnection** yeniden deneme hello bağlanma işlemi. Merhaba yeniden deneme başarılı olursa, sorgu yürütme için gönderilir.

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a>Uygulama yeniden deneme mantığı ile ConnectRetryCount birleştirilmelidir?
Güçlü özel yeniden deneme mantığı uygulamanız olduğunu varsayalım. Merhaba yeniden deneyebilirler işlemi 4 kez bağlanın. Eklerseniz **ConnectRetryInterval** ve **ConnectRetryCount** 3 tooyour bağlantı dizesi = hello yeniden deneme sayısı too4 artıracaktır * 3 = 12 yeniden dener. Yeniden deneme yüksek sayı düşündüğünüz değil.

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-tooazure-sql-database"></a>Bağlantıları tooAzure SQL veritabanı
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a>Bağlantı: Bağlantı dizesi
Merhaba bağlantı dizesi tooAzure bağlanmak için gerekli SQL veritabanı hello dizesinden tooMicrosoft SQL Server bağlamak için biraz farklı olur. Veritabanınız için hello hello bağlantı dizesini kopyalayabilirsiniz [Azure portal](https://portal.azure.com/).

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a>Bağlantı: IP adresi
Merhaba SQL veritabanı sunucusu tooaccept iletişimi hello IP adresinden istemci programınızı barındıran hello bilgisayarın yapılandırmanız gerekir. Merhaba aracılığıyla hello güvenlik duvarı ayarlarını düzenleyerek bunu [Azure portal](https://portal.azure.com/).

Tooconfigure başlangıç IP adresi unutursanız, programınızı hello gerekli IP adresi bildiren bir kullanışlı hata iletisi ile başarısız olur.

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

Daha fazla bilgi için bkz: [nasıl yapılır: SQL veritabanında güvenlik duvarı ayarlarını yapılandırma](sql-database-configure-firewall-settings.md)

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a>Bağlantı: bağlantı noktaları
Genellikle, yalnızca bağlantı noktası 1433 istemci programı barındıran hello bilgisayarda giden iletişim için açık olduğunu tooensure gerekir.

İstemci programınızı bir Windows bilgisayarda barındırılıyorsa, örneğin, hello ana bilgisayardaki Windows Güvenlik Duvarı hello tooopen bağlantı noktası 1433 sağlar:

1. Açık hello Denetim Masası
2. &gt;Tüm Denetim Masası öğeleri
3. &gt;Windows Güvenlik Duvarı
4. &gt;Gelişmiş ayarlar
5. &gt;Giden kuralları
6. &gt;Eylemler
7. &gt;Yeni Kural

İstemci programınız Azure sanal makine (VM) barındırılıp barındırılmadığını, okumanız gerekir:<br/>[ADO.NET 4.5 ve SQL veritabanı için 1433 dışındaki bağlantı noktaları](sql-database-develop-direct-route-ports-adonet-v12.md).

Arka plan IP adresi ve bağlantı noktaları hakkında bilgi için cofiguration, bkz: [Azure SQL veritabanı güvenlik duvarı](sql-database-firewall-configure.md)

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a>Bağlantı: ADO.NET 4.6.1
ADO.NET sınıflarını gibi programınızı kullanıyorsa, **System.Data.SqlClient.SqlConnection** tooconnect tooAzure SQL veritabanı, öneririz .NET Framework sürüm 4.6.1 kullanın ya da daha yüksek.

ADO.NET 4.6.1:

* Azure SQL veritabanı için yapıldığında geliştirilmiş güvenilirlik hello kullanarak bir bağlantı açmak **SqlConnection.Open** yöntemi. Merhaba **açık** yöntemi şimdi en iyi çaba yeniden deneme de mekanizmaları yanıt tootransient hataları hello bağlantı zaman aşımı süresi içinde belirli hataları içerir.
* Bağlantı havuzu destekler. Bu bağlantı hello verimli bir doğrulama içerir programınızı verir nesne çalışmasını.

Bir bağlantı havuzundan bir bağlantı nesnesi kullandığınızda, programınızı geçici olarak hello bağlantı hemen kullanırken, kapatmanızı öneririz. Bir bağlantısı'nı yeniden açmayı pahalı olmayan yeni bir bağlantı oluşturma hello yoludur.

ADO.NET 4.0 kullanıyorsanız veya daha önce toohello yükseltmenizi öneririz son ADO.NET.

* Kasım 2015'ten itibaren yapabilecekleriniz [ADO.NET 4.6.1 karşıdan](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a>Tanılama
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a>Tanılama: yardımcı programlar bağlanıp bağlanamadığınızı Test
Programınızı tooconnect tooAzure SQL veritabanı başarısız olduysa, bir tanılama yardımcı programı ile tootry tooconnect seçenektir. İdeal olarak hello yardımcı programı hello kullanarak bağlanması programınızın kullandığı aynı kitaplığı.

Herhangi bir Windows bilgisayarda bu yardımcı programları deneyebilirsiniz:

* SQL Server Management ADO.NET kullanarak bağlayan Studio (ssms.exe).
* kullanarak bağlanan sqlcmd.exe [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).

Kısa bir SQL SELECT sorgusu çalışır olup olmadığını bağlandıktan sonra test edin.

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-hello-open-ports"></a>Tanılama: Onay hello açık bağlantı noktaları
Bağlantı denemeleri tooport sorunları başarısız olan şüpheleniyorsanız varsayalım. Bilgisayarınızda hello bağlantı noktası yapılandırmalarını raporları bir yardımcı programı çalıştırabilirsiniz.

Linux hello üzerinde aşağıdaki yardımcı programlar yararlı olabilir:

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * (Merhaba örnek değer toobe, IP adresini değiştirin.)

Windows hello üzerinde [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) yardımcı programı yararlı olabilir. Başlangıç bağlantı noktası durumu bir Azure SQL veritabanı sunucusunda sorgulanan ve, bir dizüstü bilgisayar üzerinde çalıştırıldığı bir örnek yürütme şöyledir:

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting tooresolve name tooIP address...
Name resolved too23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a>Tanılama: hatalarınızı günlük
Aralıklı bir sorunun bazen en iyi genel bir desen algılanması gün veya hafta üzerinden tanı koydu.

İstemci, bulduğu tüm hataları günlüğü tarafından bir tanılama yardımcı olabilir. Dahili olarak kendisini Azure SQL veritabanı günlük hata verilerle mümkün toocorrelate hello günlük girişlerini olabilir.

Kurumsal kitaplığı 6 (EntLib60) günlük ile yönetilen .NET sınıfları tooassist sunar:

* [5 - olarak kolay olarak dönmeden kapalı bir günlük: hello günlük uygulama bloğu kullanma](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a>Tanılama: hatalar için sistem günlüklerini inceleyin
Burada, hata, sorgu günlükleri ve diğer bilgileri bazı Transact-SQL SELECT deyimleri bulunmaktadır.

| Sorgu günlüğü | Açıklama |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |Merhaba [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) görünümü geçici hataları veya bağlantısı hataları neden olabilir. bazı dahil olmak üzere ayrı ayrı olaylar hakkında bilgi sağlar.<br/><br/>İdeal olarak hello ilişkilendirebilirsiniz **start_time** veya **end_time** ne zaman istemci programınız sorunlarla karşılaştınız hakkında bilgi değerlerle.<br/><br/>**İpucu:** toohello bağlanmalısınız **ana** toorun bu veritabanı. |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |Merhaba [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) görünümü olay türleri, ek tanılama için toplanan sayısını sağlar.<br/><br/>**İpucu:** toohello bağlanmalısınız **ana** toorun bu veritabanı. |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-hello-sql-database-log"></a>Tanılama: Arama hello SQL veritabanı günlük sorun olayları için
Azure SQL veritabanı'nın hello günlüğüne sorun olaylarıyla ilgili girdileri arayabilirsiniz. Merhaba Transact-SQL SELECT deyiminde aşağıdaki hello deneyin **ana** veritabanı:

```
SELECT
   object_name
  ,CAST(f.event_data as XML).value
      ('(/event/@timestamp)[1]', 'datetime2')                      AS [timestamp]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="error"]/value)[1]', 'int')             AS [error]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="state"]/value)[1]', 'int')             AS [state]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="is_success"]/value)[1]', 'bit')        AS [is_success]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="database_name"]/value)[1]', 'sysname') AS [database_name]
FROM
  sys.fn_xe_telemetry_blob_target_read_file('el', null, null, null) AS f
WHERE
  object_name != 'login_event'  -- Login events are numerous.
  and
  '2015-06-21' < CAST(f.event_data as XML).value
        ('(/event/@timestamp)[1]', 'datetime2')
ORDER BY
  [timestamp] DESC
;
```


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a>Sys.fn_xe_telemetry_blob_target_read_file birkaç döndürülen satırları
Sonraki döndürülen satır aşağıdaki gibi görünmelidir olduğu. hello null değerler gösterilen diğer satırlardaki null olması genellikle gerekmez.

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a>Kurumsal kitaplığı 6
Kurumsal kitaplığı 6 (EntLib60) biri hello Azure SQL veritabanı hizmetinin olan bulut Hizmetleri, sağlam istemcileri uygulamanıza yardımcı olacak bir .NET sınıfları çerçevesidir. EntLib60 ilk ziyaret ederek yardımcı olabilecek konular ayrılmış tooeach alanı bulabilirsiniz:

* [Kurumsal kitaplığı 6 - Nisan 2013](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

Geçici hataları işlemek için yeniden deneme mantığı EntLib60 yardımcı olabilecek bir alandır:

* [4 - perseverance, tüm Triumphs sırrını: hello geçici hata işleme uygulama blok kullanma](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> Merhaba kaynak kodu EntLib60 kullanılabilir ortak için [karşıdan](http://go.microsoft.com/fwlink/p/?LinkID=290898). Microsoft hiçbir planları toomake daha fazla özelliği olan güncelleştirmeler ve Bakım tooEntLib güncelleştirir.
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a>Geçici hataları ve yeniden deneme için EntLib60 sınıfları
EntLib60 sınıfları aşağıdaki hello yeniden deneme mantığı için özellikle yararlıdır. Tüm bunlar içinde bulunan veya altında daha fazla ad alanı hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:

*Merhaba ad alanındaki **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*

* **RetryPolicy** sınıfı
  
  * **ExecuteAction** yöntemi
* **ExponentialBackoff** sınıfı
* **SqlDatabaseTransientErrorDetectionStrategy** sınıfı
* **ReliableSqlConnection** sınıfı
  
  * **ExecuteCommand** yöntemi

Merhaba ad alanındaki **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:

* **AlwaysTransientErrorDetectionStrategy** sınıfı
* **NeverTransientErrorDetectionStrategy** sınıfı

Bağlantılar tooinformation EntLib60 hakkında şunlardır:

* Ücretsiz [defteri indirin: Geliştirici Kılavuzu tooMicrosoft Kurumsal kitaplığı 2 sürümü](http://www.microsoft.com/download/details.aspx?id=41145)
* En iyi uygulamalar: [yeniden genel rehberlik](../best-practices-retry-general.md) mükemmel ayrıntılı incelemesi yeniden deneme mantığı vardır.
* NuGet yüklenmesini [Kurumsal Library - uygulama bloğu 6.0 geçici hata işleme](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-hello-logging-block"></a>EntLib60: hello günlük bloğu
* Merhaba günlük bloğu izin veren oldukça esnek ve yapılandırılabilir bir çözümdür:
  
  * Oluşturabilir ve çok çeşitli konumları günlük iletilerini depolayabilir.
  * Kategorilere ayırmak ve iletilerini filtreleyebilirsiniz.
  * Hata ayıklama ve izlemenin yanı sıra denetlemek için kullanışlı ve genel günlüğü gereksinimleri bağlamsal bilgi toplayın.
* Merhaba günlük bloğu hello uygulama kodu hello konumu ve tür hello hedef günlük deposu bağımsız olarak tutarlı olmasını sağlamak işlevselliği hello günlük hedeften günlüğü hello soyutlar.

Ayrıntılar için bkz: [5 - olarak kolay olarak dönmeden kapalı bir günlük: hello günlük uygulama bloğu kullanma](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a>EntLib60 IsTransient yöntemi kaynak kodu
Merhaba gelen sonraki **SqlDatabaseTransientErrorDetectionStrategy** sınıfı, hello hello C# kaynak kodu **IsTransient** yöntemi. Merhaba kaynak kodu hangi hatalarını toobe geçici ve Nisan 2013'ten itibaren yeniden deneme worthy kabul açıklar.

Çok sayıda **//comment** satırları bu kopya tooemphasize okunabilirlik kaldırıldı.

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in hello exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // hello service is currently busy. Retry hello request after 10 seconds.
            // Code: (reason code toobe decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode hello reason code from hello error message to
            // determine hello grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach hello decoded values as additional attributes to
            // hello original SQL exception.
            sqlException.Data[condition.ThrottlingMode.GetType().Name] =
              condition.ThrottlingMode.ToString();
            sqlException.Data[condition.GetType().Name] = condition;

            return true;

          case 10928:
          case 10929:
          case 10053:
          case 10054:
          case 10060:
          case 40197:
          case 40540:
          case 40613:
          case 40143:
          case 233:
          case 64:
            // DBNETLIB Error Code: 20
            // hello instance of SQL Server you attempted tooconnect to
            // does not support encryption.
          case (int)ProcessNetLibErrorCode.EncryptionNotSupported:
            return true;
        }
      }
    }
    else if (ex is TimeoutException)
    {
      return true;
    }
    else
    {
      EntityException entityException;
      if ((entityException = ex as EntityException) != null)
      {
        return this.IsTransient(entityException.InnerException);
      }
    }
  }

  return false;
}
```


## <a name="next-steps"></a>Sonraki adımlar
* Diğer ortak Azure SQL veritabanı bağlantı sorunlarını gidermek için ziyaret [sorun giderme bağlantı sorunları tooAzure SQL veritabanı](sql-database-troubleshoot-common-connection-issues.md).
* [SQL Server bağlantı (ADO.NET) havuzu](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [*Yeniden deneniyor* lisanslı bir Apache 2.0 yazılan kitaplığı yeniden deneniyor genel amaçlı olduğundan getirin **Python**, toosimplify hello görev yeniden deneme davranışı toojust hakkında hiçbir şey ekleme.](https://pypi.python.org/pypi/retrying)

