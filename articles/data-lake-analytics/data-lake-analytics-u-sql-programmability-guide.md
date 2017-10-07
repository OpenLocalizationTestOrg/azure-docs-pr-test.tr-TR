---
title: "Azure Data Lake için aaaU-SQL Programlama Kılavuzu | Microsoft Docs"
description: "Merhaba toocreate sağlayan bir hizmetler kümesi olan Azure Data Lake içinde hakkında bir bulut tabanlı büyük veri platformu öğrenin."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
ms.assetid: 63be271e-7c44-4d19-9897-c2913ee9599d
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: saveenr
ms.openlocfilehash: cc8f126234c6106a0dc633ce85a1d9ab1e634e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-programmability-guide"></a>U-SQL Programlama Kılavuzu

U-SQL, büyük veri türü için iş yüklerinin tasarlanmış bir sorgu dildir. Merhaba benzersiz özelliklerinden biri U-SQL hello hello SQL benzeri tanımlayıcı dili hello genişletilebilirlik ve C# tarafından sağlanan programlama ile birleşimidir. Bu kılavuzda, biz hello genişletilebilirlik ve C# kullanarak etkin hello U-SQL dili ile programlama yoğunlaşabilirsiniz.

## <a name="requirements"></a>Gereksinimler

İndirme ve yükleme [Visual Studio için Azure Data Lake Araçları](https://www.microsoft.com/download/details.aspx?id=49504).

## <a name="get-started-with-u-sql"></a>U-SQL ile çalışmaya başlama  

U-SQL betiği aşağıdaki hello bakalım:

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso",   1500.0, "2017-03-39"),
            ("Woodgrove", 2700.0, "2017-04-10")
        ) AS 
              D( customer, amount );
@results =
    SELECT
        customer,
    amount,
    date
    FROM @a;    
```

Adlı bir satır kümesi tanımlar @a ve adlı bir satır kümesi oluşturur @results gelen @a.

## <a name="c-types-and-expressions-in-u-sql-script"></a>C# türleri ve U-SQL betiği ifadeleri

Bir C# ifadesi gibi U-SQL mantıksal işlemleriyle birlikte bir U-SQL ifadesidir `AND`, `OR`, ve `NOT`. U-SQL deyimleri seçin, ayıklama, kullanılabilir nerede, otomatik olarak sahip olmak ve GROUP BY BİLDİRİN.

Örneğin, komut dosyası izleyen hello bir dize bir DateTime değeri hello SELECT yan tümcesinde ayrıştırır.

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

Merhaba aşağıdaki komut dosyasını bir dize bir DateTime değeri DECLARE deyimi içinde ayrıştırır.

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a>Veri türü dönüştürmeleri için C# ifadeleri kullanma
C# ifadeler kullanarak bir datetime veri dönüştürme nasıl yapabilirsiniz aşağıdaki örneğine hello gösterir. Bu belirli bir senaryoda, gece yarısı 00:00:00 saat gösterimi dönüştürülmüş toostandard datetime dize datetime verilerdir.

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a>Bugünün tarihini C# ifadeleri kullanma
toopull bugünün tarihini, C# ifade aşağıdaki hello biz kullanabilirsiniz:

```
DateTime.Now.ToString("M/d/yyyy")
```

Örneği nasıl toouse bu ifadede bir komut dosyası:

```
@rs1 =
    SELECT
        MAX(guid) AS start_id,
        MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        user,
        des
    FROM @rs0
    GROUP BY user, des;
```



## <a name="using-net-assemblies"></a>.NET derlemelerini kullanma
U-SQL'nin genişletilebilirlik modeli yoğun hello özelliği tooadd özel kodunu kullanır. Şu anda, U-SQL, kolay yolları tooadd ile kendi Microsoft sağlar. NET tabanlı kodda (özellikle, C#). Ancak, VB.NET veya F # gibi diğer .NET dilleri yazılmış özel kod ekleyebilirsiniz. 

### <a name="register-a-net-assembly"></a>Bir .NET derlemesi kaydetme

Merhaba CREATE ASSEMBLY deyimi tooplace bir U-SQL veritabanına bir .NET derlemesi kullanın. Bir veritabanında bir derlemeyi olduktan sonra U-SQL betikleri hello referans DERLEMESİNİ deyimi kullanarak bu derlemeler kullanabilirsiniz. 

kodun gösterdiği nasıl aşağıdaki hello tooregister bütünleştirilmiş:

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

kodun gösterdiği nasıl aşağıdaki hello tooreference bütünleştirilmiş:

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

Merhaba başvurun [derleme kayıt yönergeleri](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) , bu konuda daha ayrıntılı ele alınmaktadır.


### <a name="use-assembly-versioning"></a>Derleme sürümü oluşturma kullanın
Şu anda, U-SQL hello .NET Framework sürüm 4.5 kullanır. Bu nedenle, kendi derlemeleri hello çalışma zamanı bu sürümü ile uyumlu olduğundan emin olun.

U-SQL kodun bir 64-bit (x 64) biçiminde daha önce belirtildiği gibi. Böylece kodunuzu derlenmiş toorun x64 üzerinde olduğundan emin olun. Aksi takdirde, daha önce gösterilen hello yanlış biçim hatası alırsınız.

Her derleme dll dosyasını karşıya ve farklı bir çalışma zamanı, yerel bir derleme veya bir yapılandırma dosyası gibi bir kaynak dosya en fazla 400 MB olabilir. Kaynak dağıtma aracılığıyla veya başvuruları tooassemblies ve bunların ek dosyaları aracılığıyla dağıtılan kaynakları Hello toplam boyutu 3 GB aşamaz.

Son olarak, her U-SQL veritabanı herhangi verilen derleme bir sürümü yalnızca içerebileceğini unutmayın. Sürüm 7 ve 8 sürümü hello NewtonSoft Json.Net kitaplığı ihtiyacınız varsa, örneğin, tooregister gereken iki farklı veritabanlarındaki bunları. Ayrıca, her komut dosyası yalnızca belirli bir derleme DLL tooone sürümü başvurabilir. Bu bakımdan, U-SQL Yönetimi ve sürüm oluşturma derleme hello C# semantiği izler.


## <a name="use-user-defined-functions-udf"></a>Kullanıcı tanımlı işlevler kullanın: UDF
U-SQL kullanıcı tanımlı işlevler veya UDF, parametreleri kabul eder, (örneğin, karmaşık bir hesaplama) bir eylem gerçekleştirmek ve bir değer olarak bu eylemin hello sonuç yordamları programlama. Merhaba Döndür UDF değeri yalnızca tek bir skaler olabilir. U-SQL UDF temel U-SQL betiği diğer C# skaler bir işlev gibi çağrılabilir.

U-SQL kullanıcı tanımlı işlevler olarak başlatma öneririz **ortak** ve **statik**.

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

İlk bir UDF oluşturma hello basit örneğe bakalım.

Bu kullanım örneği senaryosu hello mali çeyreği ve mali ayı hello ilk oturum açma hello belirli bir kullanıcı için de dahil olmak üzere toodetermine hello mali süresi gerekir. Merhaba bizim senaryoda hello yılın ilk mali ayı Haziran ' dir.

toocalculate mali dönem, biz C# işlevi aşağıdaki hello sunar:

```
public static string GetFiscalPeriod(DateTime dt)
{
    int FiscalMonth=0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter=0;
    if (FiscalMonth >=1 && FiscalMonth<=3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return "Q" + FiscalQuarter.ToString() + ":P" + FiscalMonth.ToString();
}
```

Mali ayı ve üç aylık dönem hesaplar ve bir string değeri döndürür. Merhaba ilk ayın hello ilk mali çeyreği, Haziran için "Q1:P1" kullanın. Temmuz, biz "Q1:P2" kullanın ve benzeri.

Devam eden toouse U-SQL Projemizin gerçekleştirildiğine dair normal bir C# işlevi budur.

Merhaba arka plan kodu bölüm bu senaryoda, nasıl göründüğünü aşağıda verilmiştir:

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        public static string GetFiscalPeriod(DateTime dt)
        {
            int FiscalMonth=0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter=0;
            if (FiscalMonth >=1 && FiscalMonth<=3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return "Q" + FiscalQuarter.ToString() + ":" + FiscalMonth.ToString();
        }

    }

}
```

Şimdi biz toocall bu işlev hello temel U-SQL komut dosyasından adımıdır. toodo Bu, biz tooprovide hello ad alanı, bu durumda NameSpace.Class.Function(parameter) olduğu dahil olmak üzere hello işlevi için tam bir ada sahip.

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

Merhaba gerçek U-SQL temel betiği aşağıdadır:

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt DateTime,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

DECLARE @default_dt DateTime = Convert.ToDateTime("06/01/2016");

@rs1 =
    SELECT
        MAX(guid) AS start_id,
    MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        user,
        des
    FROM @rs0
    GROUP BY user, des;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

Merhaba çıktı dosyası hello komut dosyası yürütme aşağıdadır:

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

Bu örnek, basit bir satır içi U-SQL UDF'de kullanımını gösterir.

### <a name="keep-state-between-udf-invocations"></a>UDF çağrılarını arasında durumu tutun
U-SQL C# programlama nesnelerini daha, hello arka plan kodu Genel değişkenler aracılığıyla etkileşim kullanan gelişmiş. İş kullanım örneği senaryosu aşağıdaki hello bakalım.

Büyük kuruluşlarda, kullanıcıların iç uygulamaları çeşitleri arasında geçiş yapabilirsiniz. Bunlar, Microsoft Dynamics CRM, Powerbı vb. içerebilir. Müşteriler tooapply kullanıcıların hangi hello kullanım olan ve benzeri eğilimlerin farklı uygulamalar arasında nasıl geçiş, bir telemetri analizi isteyebilirsiniz. Merhaba hello iş için toooptimize uygulama kullanımı hedeftir. Ayrıca toocombine farklı uygulamalar veya oturum açma belirli yordamları isteyebilirsiniz.

tooachieve bu hedef toodetermine oturum kimlikleri ve gecikme süresi arasında hello oluştu son oturumun sunuyoruz.

Bir önceki oturum açma toofind gerekir ve oluşturulan toohello yükleniyor bu oturum açma tooall oturumları atamak aynı uygulama. Merhaba ilk temel U-SQL betiği bize tooapply hesaplamalar önceden hesaplanan sütunlar ÖTELEME işleviyle üzerinden izin vermez, iştir. Merhaba ikinci tookeep hello hello içindeki tüm oturumlar için belirli bir oturum sahibiz iştir aynı süre.

toosolve Bu sorun bir arka plan kodu bölüm içinde genel değişkeni kullanırız: `static public string globalSession;`.

Bu genel değişkeni bizim komut dosyası yürütme sırasında uygulanan toohello tüm satır kümesidir.

U-SQL programımız hello arka plan kodu bölümü aşağıda verilmiştir:

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQLApplication21
{
    public class UserSession
    {
        static public string globalSession;
        static public string StampUserSession(string eventTime, string PreviousRow, string Session)
        {

            if (!string.IsNullOrEmpty(PreviousRow))
            {
                double timeGap = Convert.ToDateTime(eventTime).Subtract(Convert.ToDateTime(PreviousRow)).TotalMinutes;
                if (timeGap <= 60) {return Session;}
                else {return Guid.NewGuid().ToString();}
            }
            else {return Guid.NewGuid().ToString();}

        }

        static public string getStampUserSession(string Session)
        {
            if (Session != globalSession && !string.IsNullOrEmpty(Session)) { globalSession = Session; }
            return globalSession;
        }

    }
}
```

Gösterir hello genel değişkeni Bu örnek `static public string globalSession;` hello içinde kullanılan `getStampUserSession` işlevi ve alma yeniden her zaman hello oturum parametresi değiştirilir.

Merhaba temel U-SQL betiği aşağıdaki gibidir:

```
DECLARE @in string = @"\UserSession\test1.tsv";
DECLARE @out1 string = @"\UserSession\Out1.csv";
DECLARE @out2 string = @"\UserSession\Out2.csv";
DECLARE @out3 string = @"\UserSession\Out3.csv";

@records =
    EXTRACT DataId string,
            EventDateTime string,           
            UserName string,
            UserSessionTimestamp string

    FROM @in
    USING Extractors.Tsv();

@rs1 =
    SELECT 
        EventDateTime,
        UserName,
    LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,          
        string.IsNullOrEmpty(LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,           
        USQLApplication21.UserSession.StampUserSession
           (
            EventDateTime,
            LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC),
            LAG(UserSessionTimestamp, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)
           ) AS UserSessionTimestamp
    FROM @records;

@rs2 =
    SELECT 
        EventDateTime,
        UserName,
        LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,
        string.IsNullOrEmpty( LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,
        USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp) AS UserSessionTimestamp
    FROM @rs1
    WHERE UserName != "UserName";

OUTPUT @rs2
    too@out2
    ORDER BY UserName, EventDateTime ASC
    USING Outputters.Csv();
```

İşlev `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` burada hello ikinci bellek satır kümesi hesaplama sırasında çağrılır. Merhaba geçirir `UserSessionTimestamp` sütun ve döndürür hello değeri kadar `UserSessionTimestamp` değişti.

Merhaba çıktı dosyası aşağıdaki gibidir:

```
"2016-02-19T07:32:36.8420000-08:00","User1",,True,"72a0660e-22df-428e-b672-e0977007177f"
"2016-02-17T11:52:43.6350000-08:00","User2",,True,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-17T11:59:08.8320000-08:00","User2","2016-02-17T11:52:43.6350000-08:00",False,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-11T07:04:17.2630000-08:00","User3",,True,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-11T07:10:33.9720000-08:00","User3","2016-02-11T07:04:17.2630000-08:00",False,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-15T21:27:41.8210000-08:00","User3","2016-02-11T07:10:33.9720000-08:00",False,"4d2bc48d-bdf3-4591-a9c1-7b15ceb8e074"
"2016-02-16T05:48:49.6360000-08:00","User3","2016-02-15T21:27:41.8210000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-16T06:22:43.6390000-08:00","User3","2016-02-16T05:48:49.6360000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-17T16:29:53.2280000-08:00","User3","2016-02-16T06:22:43.6390000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T16:39:07.2430000-08:00","User3","2016-02-17T16:29:53.2280000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T17:20:39.3220000-08:00","User3","2016-02-17T16:39:07.2430000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-19T05:23:54.5710000-08:00","User3","2016-02-17T17:20:39.3220000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T05:48:37.7510000-08:00","User3","2016-02-19T05:23:54.5710000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T06:40:27.4830000-08:00","User3","2016-02-19T05:48:37.7510000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T07:27:37.7550000-08:00","User3","2016-02-19T06:40:27.4830000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T19:35:40.9450000-08:00","User3","2016-02-19T07:27:37.7550000-08:00",False,"3f385f0b-3e68-4456-ac74-ff6cef093674"
"2016-02-20T00:07:37.8250000-08:00","User3","2016-02-19T19:35:40.9450000-08:00",False,"685f76d5-ca48-4c58-b77d-bd3a9ddb33da"
"2016-02-11T09:01:33.9720000-08:00","User4",,True,"9f0cf696-c8ba-449a-8d5f-1ca6ed8f2ee8"
"2016-02-17T06:30:38.6210000-08:00","User4","2016-02-11T09:01:33.9720000-08:00",False,"8b11fd2a-01bf-4a5e-a9af-3c92c4e4382a"
"2016-02-17T22:15:26.4020000-08:00","User4","2016-02-17T06:30:38.6210000-08:00",False,"4e1cb707-3b5f-49c1-90c7-9b33b86ca1f4"
"2016-02-18T14:37:27.6560000-08:00","User4","2016-02-17T22:15:26.4020000-08:00",False,"f4e44400-e837-40ed-8dfd-2ea264d4e338"
"2016-02-19T01:20:31.4800000-08:00","User4","2016-02-18T14:37:27.6560000-08:00",False,"2136f4cf-7c7d-43c1-8ae2-08f4ad6a6e08"
```

Bu örnek bir genel değişkeni uygulanan toohello tüm bellek satır kümesi olan bir arka plan kodu bölüm içinde kullandığımız daha karmaşık bir kullanım örneği senaryosu gösterilmektedir.

## <a name="use-user-defined-types-udt"></a>Kullanıcı tanımlı türler kullanın: UDT
Kullanıcı tanımlı türler veya UDT, başka bir programlama, U-SQL özelliğidir. U-SQL UDT bir normal C# kullanıcı tanımlı tür gibi davranır. C# yerleşik ve özel kullanıcı tanımlı türler hello kullanılmasına kesin türü belirtilmiş bir dil değil.

U-SQL örtük olarak serileştirmek veya satır kümeleri tepe arasında hello UDT geçirildiğinde rasgele atama anlayabileceği olamaz. Bu, açık bir biçimlendirici tooprovide hello IFormatter arabirimini kullanarak hello kullanıcının sahip anlamına gelir. Bu U-SQL ile Merhaba sağlar seri hale getirmek ve seri durumdan hello UDT yöntemleri.

> [!NOTE]
> U-SQL'nin yerleşik ayıklayıcıları ve outputters şu anda serileştirmek veya seri durumdan UDT veri tooor dosyalarını bile hello IFormatter kümesi. UDT veri tooa hello çıkış deyimi dosyasıyla yazıyorsanız ya da toopass sahip bir ayıklayıcısı okuma, böyle bir string veya byte dizisi olarak. Ardından hello serileştirme çağırın ve kod (diğer bir deyişle, hello UDT'ın ToString() yöntemini) açıkça seri durumundan çıkarma. Kullanıcı tanımlı ayıklayıcıları ve hello diğer üzerinde outputters el okuyabilir ve atama yazma.

Aşağıda gösterildiği gibi toouse AYIKLAYICISI veya OUTPUTTER (dışında önceki seçin), UDT deneyin ise:

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

Aşağıdaki hata hello aldığımız:

```
Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used toooutput column myfield of type
MyNameSpace.Myfunction_Returning_UDT.

Description:

Outputters.Text only supports built-in types.

Resolution:

Implement a custom outputter that knows how tooserialize this type, or call a serialization method on hello type in
hello preceding SELECT. C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

outputter içinde toowork UDT ile ya da sahip olduğumuz tooserialize, toostring ile ToString() yöntemini hello veya özel bir outputter oluşturun.

Atama, grup tarafından şu anda kullanılamaz. UDT grubu tarafından kullanılıyorsa, aşağıdaki hata hello oluşturulur:

```
Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
for column myfield

Description:

GROUP BY doesn't support UDT or Complex types.

Resolution:

Add a SELECT statement where you can project a scalar column that you want toouse with GROUP BY.
C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
62  5   USQL-Programmability
```

UDT toodefine, biz gerekir:

* Ad alanları aşağıdaki hello ekleyin:

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* Ekleme `Microsoft.Analytics.Interfaces`, hello UDT arabirimler için gerekli olduğu. Ayrıca, `System.IO` gerekli toodefine hello IFormatter arabirimi olabilir.

* Kullanılan tanımlı bir tür SqlUserDefinedType özniteliğiyle tanımlayın.

**SqlUserDefinedType** kullanılan toomark bir türü kullanıcı tanımlı bir tür (UDT) olarak derlemedeki U-SQL tanımıdır. Merhaba özellikleri hello öznitelikte hello UDT fiziksel özelliklerini hello yansıtır. Bu sınıf devralınan olamaz.

SqlUserDefinedType UDT tanımı için gerekli bir özniteliktir.

Merhaba sınıfının Hello Oluşturucusu:  

* SqlUserDefinedTypeAttribute (türü biçimlendirici)

* Biçimlendirici yazın: gerekli parametre toodefine bir UDT biçimlendirici--özellikle hello hello türü `IFormatter` arabirimi gerekir bayraklarıdır burada.

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* Tipik UDT hello aşağıdaki örnekte gösterildiği gibi hello IFormatter arabirimi tanımını da gerektirir:

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

Merhaba `IFormatter` arabirimi serileştirir ve hello kök türüne sahip bir nesne grafiğinin XML'deki serileştiren \<typeparamref name = "T" >.

\<typeparam name = "T" > merhaba kök türü için hello Nesne grafiği tooserialize ve seri durumdan.

* **Seri durumdan**: sağlanan hello akış hello verileri XML'deki serileştirir ve hello grafik nesnelerinin reconstitutes.

* **Seri hale**: bir nesne ya da nesne, grafik kök toohello sağlanan akış verilen hello ile Serileştirir.

`MyType`Örnek: Merhaba türünün örneği.  
`IColumnWriter`yazıcı / `IColumnReader` okuyucu: sütun akış temel hello.  
`ISerializationContext`Bağlam: Enum hello kaynak veya hedef bağlamı hello akış için serileştirme sırasında belirten bayrakları kümesini tanımlar.

* **Ara**: Bu hello kaynak veya hedef bağlamı kalıcı depolama değil belirtir.

* **Kalıcılığı**: Bu hello kaynak veya hedef bağlam kalıcı depolama olduğunu belirtir.

Bir normal C# türü olarak bir U-SQL UDT tanımı geçersiz kılmaları işleçlerini gibi içerebilir +/ == /! =. Statik yöntemler de içerir. Biz toouse bu UDT parametresi tooa U-SQL MIN toplama işlevi kullanacaksanız, örneğin, toodefine sahibiz < işleci geçersiz kılma.

Bu kılavuzda daha önce Qn:Pn (Q1:P10) hello biçiminde hello belirli tarihten mali dönem tanımlaması için bir örnek gösterilmektedir. Aşağıdaki örnek hello nasıl toodefine özel mali dönem için değerler girin gösterir.

Aşağıdaki özel UDT ve IFormatter arabirimi arka plan kodu bölümle örneğidir:

```
[SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
public struct FiscalPeriod
{
    public int Quarter { get; private set; }

    public int Month { get; private set; }

    public FiscalPeriod(int quarter, int month):this()
    {
    this.Quarter = quarter;
    this.Month = month;
    }

    public override bool Equals(object obj)
    {
    if (ReferenceEquals(null, obj))
    {
        return false;
    }

    return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
    }

    public bool Equals(FiscalPeriod other)
    {
return this.Quarter.Equals(other.Quarter) && this.Month.Equals(other.Month);
    }

    public bool GreaterThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
    }

    public bool LessThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
    }

    public override int GetHashCode()
    {
    unchecked
    {
        return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
    }
    }

    public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
    {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
    }

    public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.Equals(c2);
    }

    public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
    {
    return !c1.Equals(c2);
    }
    public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.GreaterThan(c2);
    }
    public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.LessThan(c2);
    }
    public override string ToString()
    {
    return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
    }

}

public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
{
    public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
    {
    using (var binaryWriter = new BinaryWriter(writer.BaseStream))
    {
        binaryWriter.Write(instance.Quarter);
        binaryWriter.Write(instance.Month);
        binaryWriter.Flush();
    }
    }

    public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
    {
    using (var binaryReader = new BinaryReader(reader.BaseStream))
    {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
        return result;
    }
    }
}
```

Merhaba tanımlı türünü içeren iki sayı: üç aylık dönem ve ay. İşleç == /! = / > / < ve statik yöntemi ToString() burada tanımlanır.

Daha önce belirtildiği gibi UDT SELECT ifadelerde kullanılabilir, ancak OUTPUTTER/AYIKLAYICISI özel serileştirme kullanılamaz. Ya da ToString() bir dize olarak serileştirilmiş veya özel bir OUTPUTTER/AYIKLAYICISI kullanılan toobe de vardır.

Şimdi şimdi UDT kullanımını tartışın. Arka plan kodu bölümünde bizim GetFiscalPeriod işlevi toohello aşağıdaki değiştirilmiştir:

```
public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
{
    int FiscalMonth = 0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter = 0;
    if (FiscalMonth >= 1 && FiscalMonth <= 3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return new FiscalPeriod(FiscalQuarter, FiscalMonth);
}
```

Gördüğünüz gibi bizim FiscalPeriod türü hello değerini döndürür.

Burada nasıl toouse başka işlemler U-SQL temel komut dosyasında bir örnek sağlar. Bu örnek, farklı UDT çağırma formlardan U-SQL betiği gösterir.

```
DECLARE @input_file string = @"c:\work\cosmos\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"c:\work\cosmos\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        guid string,
        dt DateTime,
        user String,
        des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT 
        guid AS start_id,
        dt,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Quarter AS fiscalquarter,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Month AS fiscalmonth,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt) + new USQL_Programmability.CustomFunctions.FiscalPeriod(1,7) AS fiscalperiod_adjusted,
        user,
        des
    FROM @rs0;

@rs2 =
    SELECT 
           start_id,
           dt,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           fiscalquarter,
           fiscalmonth,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS fiscalperiod,

       // This user-defined type was created in hello prior SELECT.  Passing hello UDT toothis subsequent SELECT would have failed if hello UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    too@output_file 
    USING Outputters.Text();
```

Bir tam arka plan kodu bölümü bir örneği burada verilmiştir:

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        static public DateTime? ToDateTime(string dt)
        {
            DateTime dtValue;

            if (!DateTime.TryParse(dt, out dtValue))
                return Convert.ToDateTime(dt);
            else
                return null;
        }

        public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
        {
            int FiscalMonth = 0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter = 0;
            if (FiscalMonth >= 1 && FiscalMonth <= 3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return new FiscalPeriod(FiscalQuarter, FiscalMonth);
        }



        [SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
        public struct FiscalPeriod
        {
            public int Quarter { get; private set; }

            public int Month { get; private set; }

            public FiscalPeriod(int quarter, int month):this()
            {
                this.Quarter = quarter;
                this.Month = month;
            }

            public override bool Equals(object obj)
            {
                if (ReferenceEquals(null, obj))
                {
                    return false;
                }

                return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
            }

            public bool Equals(FiscalPeriod other)
            {
return this.Quarter.Equals(other.Quarter) &&    this.Month.Equals(other.Month);
            }

            public bool GreaterThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
            }

            public bool LessThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
            }

            public override int GetHashCode()
            {
                unchecked
                {
                    return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
                }
            }

            public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
            {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
            }

            public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.Equals(c2);
            }

            public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
            {
                return !c1.Equals(c2);
            }
            public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.GreaterThan(c2);
            }
            public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.LessThan(c2);
            }
            public override string ToString()
            {
                return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
            }

        }

        public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
        {
public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
            {
                using (var binaryWriter = new BinaryWriter(writer.BaseStream))
                {
                    binaryWriter.Write(instance.Quarter);
                    binaryWriter.Write(instance.Month);
                    binaryWriter.Flush();
                }
            }

public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
            {
                using (var binaryReader = new BinaryReader(reader.BaseStream))
                {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
                    return result;
                }
            }
        }
    }
}
```

## <a name="use-user-defined-aggregates-udagg"></a>Kullanıcı tanımlı toplamlarda kullanın: UDAGG
Kullanıcı tanımlı toplamlarda, toplama ile ilgili olan tüm işlevler out-of--box U-SQL ile gönderilmeyen ' dir. Merhaba örneği özel matematik hesaplamaları, dize birleştirmeler işlemeleri dizeler, bir toplama tooperform olması ve benzeri.

Merhaba kullanıcı tanımlı toplama temel sınıf tanımı aşağıdaki gibidir:

```c#
    [SqlUserDefinedAggregate]
    public abstract class IAggregate<T1, T2, TResult> : IAggregate
    {
        protected IAggregate();

        public abstract void Accumulate(T1 t1, T2 t2);
        public abstract void Init();
        public abstract TResult Terminate();
    }
```

**SqlUserDefinedAggregate** hello türü kullanıcı tanımlı toplama olarak kayıtlı olduğunu belirtir. Bu sınıf devralınan olamaz.

SqlUserDefinedType özniteliği **isteğe bağlı** UDAGG tanımı.


Merhaba temel sınıf toopass üç soyut parametrelerinin sağlar: iki giriş parametreleri ve bir hello sonucunda olarak. Başlangıç veri türleri değişkendir ve sınıf devralma sırasında tanımlanması gerekir.

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    { … }

    public override void Accumulate(string guid, string user)
    { … }

    public override string Terminate()
    { … }
}
```

* **Init** hesaplaması sırasında her grup için bir kez çağırır. Bu, her toplama grubu için bir başlatma yordamının sağlar.  
* **Accumulate** her bir değer için bir kez çalıştırılır. Bu, hello toplama algoritması hello ana işlevsellik sağlar. Kullanılan tooaggregate değerleri sınıf devralma sırasında tanımlanan çeşitli veri türlerine sahip olabilir. Değişken veri türünde iki parametre kabul edebilir.
* **Sonlandırma** toooutput hello sonuç her grup için işleme hello sonunda toplama grubu başına bir kez çalıştırılır.

toodeclare doğru girdi ve çıktı veri türlerini kullanın hello sınıf tanımını gibi:

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* T1: İlk parametre tooaccumulate
* T2: İlk parametre tooaccumulate
* TResult: dönüş türü Sonlandır

Örneğin:

```
public class GuidAggregate : IAggregate<string, int, int>
```

or

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a>U-SQL UDAGG kullanın
toouse UDAGG, ilk kod arkasında tanımlayın veya daha önce bahsedildiği gibi hello varolan programlama DLL başvurun.

Ardından sözdizimi aşağıdaki hello kullanın:

```
AGG<UDAGG_functionname>(param1,param2)
```

UDAGG bir örneği burada verilmiştir:

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    {
        guid_agg = "";
    }

    public override void Accumulate(string guid, string user)
    {
        if (user.ToUpper()== "USER1")
        {
        guid_agg += "{" + guid + "}";
        }
    }

    public override string Terminate()
    {
        return guid_agg;
    }

}
```

Ve temel U-SQL betiği:

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @" \usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    SELECT
        user,
        AGG<USQL_Programmability.GuidAggregate>(guid,user) AS guid_list
    FROM @rs0
    GROUP BY user;

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

Bu kullanım örneği senaryosu sınıfı GUID'leri hello belirli kullanıcılar için birleştirme.

## <a name="use-user-defined-objects-udo"></a>Kullanıcı tanımlı nesneler kullanın: UDO
U-SQL kullanıcı tanımlı nesneler veya UDO adlı toodefine özel programlama nesnelerini sağlar.

Merhaba, U-SQL UDO listesi aşağıdadır:

* Kullanıcı tanımlı ayıklayıcıları
    * Extract satır satır
    * Özel yapılandırılmış dosyalarından tooimplement veri ayıklama kullanılan

* Kullanıcı tanımlı outputters
    * Çıkış satır satır
    * Kullanılan toooutput özel veri türleri veya özel dosya biçimleri

* Kullanıcı tanımlı işlemcileri
    * Bir satır almak ve bir satır üretir
    * Kullanılan tooreduce sütun sayısı hello veya varolan bir sütun kümesinden türetilmiş değerlerle yeni sütun oluşturmak

* Kullanıcı tanımlı appliers
    * Bir satır alın ve 0 toon satır üretir
    * Dış/ARASI UYGULA ile kullanılan

* Kullanıcı tanımlı combiners
    * Satır kümeleri--kullanıcı tanımlı birleştirmeler birleştirir

* Kullanıcı tanımlı reducers
    * N satırları almak ve bir satır üretir
    * Kullanılan tooreduce hello satır sayısı

UDO genellikle U-SQL komut U-SQL deyimlerini aşağıdaki hello bir parçası olarak açıkça çağrılır:

* EXTRACT
* ÇIKTI
* İŞLEM
* BİRLEŞTİRME
* AZALTMA

> [!NOTE]  
> UDO'ın sınırlı tooconsume 0,5 Gb bellek var.  Bu bellek sınırlama toolocal yürütmeleri geçerli değildir.

## <a name="use-user-defined-extractors"></a>Kullanıcı tanımlı ayıklayıcıları kullanın
U-SQL EXTRACT deyimi kullanarak tooimport dış veri sağlar. Bir ayıklama deyimi yerleşik UDO ayıklayıcıları kullanabilirsiniz:  

* *Extractors.Text()*: farklı kodlamaları sınırlandırılmış metin dosyalarından ayıklama sağlar.

* *Extractors.Csv()*: ayıklama virgülle ayrılmış değer (CSV) dosyaları farklı kodlamaları sağlar.

* *Extractors.Tsv()*: ayıklama sekmeyle ayrılmış değerinden farklı kodlamaları (TSV) dosyaları sağlar.

Yararlı toodevelop özel ayıklayıcısı olabilir. Biz toodo görevleri aşağıdaki hello hiçbirini istiyorsanız, bu veri içe aktarma sırasında yararlı olabilir:

* Giriş verisi sütunları bölme ve tek tek değerleri değiştirerek değiştirin. Merhaba İŞLEMCİ işlevselliğini sütunları birleştirmek için daha iyi olur.
* Web sayfaları ve e-posta gibi yapılandırılmamış veriler veya XML/JSON gibi yarı yapılandırılmamış veriler ayrıştırılamadı.
* Desteklenmeyen kodlama verileri ayrıştırılamıyor.

bir kullanıcı tarafından tanımlanan ayıklayıcısı toodefine veya Opyalanan, ihtiyacımız toocreate bir `IExtractor` arabirimi. Sütun/satır sınırlayıcıları ve kodlama, hello sınıfı hello oluşturucuda tanımlanan toobe gerektiği gibi tüm parametreleri toohello ayıklayıcısı girin. Merhaba `IExtractor` arabirimi hello için bir tanım da içermelidir `IEnumerable<IRow>` gibi geçersiz kıl:

```
[SqlUserDefinedExtractor]
public class SampleExtractor : IExtractor
{
     public SampleExtractor(string row_delimiter, char col_delimiter)
     { … }

     public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
     { … }
}
```

Merhaba **SqlUserDefinedExtractor** öznitelik, hello türü kullanıcı tanımlı bir ayıklayıcısı kayıtlı olduğunu gösterir. Bu sınıf devralınan olamaz.

SqlUserDefinedExtractor Opyalanan tanımı için isteğe bağlı bir özniteliktir. Toodefine AtomicFileProcessing özelliği hello Opyalanan nesne için kullanılır.

* bool AtomicFileProcessing   

* **doğru** bu ayıklayıcısı atomik giriş dosyaları (JSON, XML,...) gerektirdiğini belirtir =
* **yanlış** bu ayıklayıcısı bölünmüş / dağıtılmış dosyalarla (CSV, SEQ,...) başa belirtir =

Merhaba ana Opyalanan programlamasına nesneler **giriş** ve **çıkış**. Merhaba giriş nesnesidir kullanılan tooenumerate girdi verisi olarak `IUnstructuredReader`. kullanılan tooset çıktı verilerini hello ayıklayıcısı etkinlik sonucunda Hello çıkış nesnesidir.

Merhaba giriş verileri üzerinden erişildiğinde `System.IO.Stream` ve `System.IO.StreamReader`.

Giriş sütunları numaralandırması için biz ilk hello Giriş akışı satır ayırıcı kullanarak ayırın.

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

Ardından, daha fazla giriş satır sütun bölün.

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

tooset çıktı verilerini, hello kullanırız `output.Set` yöntemi.

Merhaba çıkışıyla sütunlar ve tanımlanmış değerler yalnızca özel ayıklayıcısı hello toounderstand çıkarır önemlidir. Yöntem çağrısının ayarlayın.

```
output.Set<string>(count, part);
```

Merhaba gerçek ayıklayıcısı çıkış çağırarak tetiklenir `yield return output.AsReadOnly();`.

Merhaba ayıklayıcısı örneği aşağıda verilmiştir:

```
[SqlUserDefinedExtractor(AtomicFileProcessing = true)]
public class FullDescriptionExtractor : IExtractor
{
     private Encoding _encoding;
     private byte[] _row_delim;
     private char _col_delim;

    public FullDescriptionExtractor(Encoding encoding, string row_delim = "\r\n", char col_delim = '\t')
    {
         this._encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
         this._row_delim = this._encoding.GetBytes(row_delim);
         this._col_delim = col_delim;

    }

    public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
    {
         string line;
         //Read hello input line by line
         foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
         {
        using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
         {
             line = streamReader.ReadToEnd().Trim();
             //Split hello input by hello column delimiter
             string[] parts = line.Split(this._col_delim);
             int count = 0; // start with first column
             foreach (string part in parts)
             {
    if (count == 0)
             {  // for column “guid”, re-generated guid
                 Guid new_guid = Guid.NewGuid();
                 output.Set<Guid>(count, new_guid);
             }
             else if (count == 2)
             {
                 // for column “user”, convert tooUPPER case
                 output.Set<string>(count, part.ToUpper());

             }
             else
             {
                 // keep hello rest of hello columns as-is
                 output.Set<string>(count, part);
             }
             count += 1;
             }

         }
         yield return output.AsReadOnly();
         }
         yield break;
     }
}
```

Bu kullanım örneği senaryosu hello ayıklayıcısı hello GUID "guid" sütunu için yeniden oluşturur ve "kullanıcı" sütun tooupper örneğinin hello değerleri dönüştürür. Özel ayıklayıcıları giriş verilerini ayrıştırma ve onu düzenleme daha karmaşık sonuçlara yol açabilir.

Özel ayıklayıcısı kullanan temel U-SQL komut dosyası aşağıdadır:

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file
        USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a>Kullanıcı tanımlı outputters kullanın
Kullanıcı tanımlı outputter tooextend yerleşik U-SQL işlevselliği sağlayan başka bir U-SQL UDO ' dir. Benzer toohello ayıklayıcısı, birkaç yerleşik outputters vardır.

* *Outputters.Text()*: metin dosyalarını farklı kodlamaları veri toodelimited yazar.
* *Outputters.Csv()*: veri toocomma virgülle ayrılmış değer (CSV) dosyaları farklı kodlamaları yazar.
* *Outputters.Tsv()*: veri tootab virgülle ayrılmış değer (TSV) dosyaları farklı kodlamaları yazar.

Özel outputter özel tanımlanmış bir biçimde toowrite veri sağlar. Bu görevleri aşağıdaki hello için yararlı olabilir:

* Veri toosemi yapılandırılmış veya yapılandırılmamış dosyaları yazma.
* Veri yazma değil Kodlamalar desteklenir.
* Çıktı verilerini değiştirme veya özel öznitelikleri ekleme.

Kullanıcı tanımlı toodefine outputter ihtiyacımız toocreate hello `IOutputter` arabirimi.

Aşağıdadır hello temel `IOutputter` sınıfı uygulama:

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

Sütun/satır sınırlayıcıları, kodlama ve benzeri, hello sınıfı hello oluşturucuda tanımlanan toobe gerektiği gibi tüm parametreleri toohello outputter girin. Merhaba `IOutputter` arabirimi için bir tanım da içermelidir `void Output` geçersiz kılar. Merhaba özniteliği `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` atomik dosya işleme için isteğe bağlı olarak ayarlanabilir. Daha fazla bilgi için hello aşağıdaki ayrıntılara bakın.

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class MyOutputter : IOutputter
{

    public MyOutputter(myparam1, myparam2)
    {
      …
    }

    public override void Close()
    {
      …
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
      …
    }
}
```

* `Output`Giriş her satır için çağrılır. Merhaba döndürür `IUnstructuredWriter output` satır kümesi.
* Merhaba Oluşturucusu sınıfı kullanılır toopass parametreleri toohello kullanıcı tanımlı outputter.
* `Close`kullanılan toooptionally toorelease pahalı durumu geçersiz kılabilir veya ne zaman hello son satırını yazıldı belirleyin.

**SqlUserDefinedOutputter** öznitelik, hello türü kullanıcı tanımlı bir outputter kayıtlı olduğunu gösterir. Bu sınıf devralınan olamaz.

SqlUserDefinedOutputter, kullanıcı tanımlı outputter tanımı için isteğe bağlı bir özniteliktir. Toodefine hello AtomicFileProcessing özelliği kullandı.

* bool AtomicFileProcessing   

* **doğru** bu outputter atomik çıktı dosyaları (JSON, XML,...) gerektirdiğini belirtir =
* **yanlış** bu outputter bölünmüş / dağıtılmış dosyalarla (CSV, SEQ,...) başa belirtir =

Merhaba ana programlamasına nesneler **satır** ve **çıkış**. Merhaba **satır** nesnesidir kullanılan tooenumerate çıktı verisi olarak `IRow` arabirimi. **Çıktı** kullanılan tooset çıkış veri toohello hedef dosyasıdır.

Merhaba çıktı verilerini hello erişilen `IRow` arabirimi. Çıktı verilerini bir satır aynı anda geçirilir.

Merhaba tek tek değerleri hello IRow arabiriminin hello Get yöntemini çağırarak numaralandırılmıştır:

```
row.Get<string>("column_name")
```

Tek tek sütun adları çağırarak belirlenebilir `row.Schema`:

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

Bu yaklaşım toobuild herhangi bir meta veri şema için esnek bir outputter sağlar.

Merhaba çıktı verilerini toofile kullanılarak yazılan `System.IO.StreamWriter`. Merhaba akışı parametre olarak ayarlanmış çok`output.BaseStrea` parçası olarak `IUnstructuredWriter output`.

Her satır yinelemeden sonra önemli tooflush hello veri arabelleği toohello dosyası olduğunu unutmayın. Ayrıca, hello `StreamWriter` nesne özniteliğiyle etkin hello atılabilir (varsayılan) ile Merhaba kullanılmalıdır **kullanarak** anahtar sözcüğü:

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

Aksi takdirde Flush() yöntemini her yinelemeden sonra açıkça çağırın. Bu örnekte aşağıdaki hello gösteriyoruz.

### <a name="set-headers-and-footers-for-user-defined-outputter"></a>Üstbilgiler ve altbilgiler kullanıcı tanımlı outputter için ayarlama
tooset bir üstbilgi tek yineleme yürütme akışı kullanın.

```
public override void Output(IRow row, IUnstructuredWriter output)
{
 …
if (isHeaderRow)
{
    …                
}

 …
if (isHeaderRow)
{
    isHeaderRow = false;
}
 …
}
}
```

Merhaba kodda ilk hello `if (isHeaderRow)` blok yalnızca bir kez gerçekleştirilir.

Merhaba altbilgiyi hello başvuru toohello örneğini kullanması `System.IO.Stream` nesne (`output.BaseStream`). Merhaba altbilgi hello hello çağrısının yöntemi yazma `IOutputter` arabirimi.  (Daha fazla bilgi için aşağıdaki örneğine hello bakın.)

Kullanıcı tanımlı bir outputter örneği aşağıdadır:

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class HTMLOutputter : IOutputter
{
    // Local variables initialization
    private string row_delimiter;
    private char col_delimiter;
    private bool isHeaderRow;
    private Encoding encoding;
    private bool IsTableHeader = true;
    private Stream g_writer;

    // Parameters definition            
    public HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    this.isHeaderRow = isHeader;
    this.encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
    }

    // hello Close method is used toowrite hello footer toohello file. It's executed only once, after all rows
    public override void Close().
    {
    //Reference tooIO.Stream object - g_writer
    StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
    streamWriter.Write("</table>");
    streamWriter.Flush();
    streamWriter.Close();
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
    System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

    // Metadata schema initialization tooenumerate column names
    ISchema schema = row.Schema;

    // This is a data-independent header--HTML table definition
    if (IsTableHeader)
    {
        streamWriter.Write("<table border=1>");
        IsTableHeader = false;
    }

    // HTML table attributes
    string header_wrapper_on = "<th>";
    string header_wrapper_off = "</th>";
    string data_wrapper_on = "<td>";
    string data_wrapper_off = "</td>";

    // Header row output--runs only once
    if (isHeaderRow)
    {
        streamWriter.Write("<tr>");
        for (int i = 0; i < schema.Count(); i++)
        {
        var col = schema[i];
        streamWriter.Write(header_wrapper_on + col.Name + header_wrapper_off);
        }
        streamWriter.Write("</tr>");
    }

    // Data row output
    streamWriter.Write("<tr>");                
    for (int i = 0; i < schema.Count(); i++)
    {
        var col = schema[i];
        string val = "";
        try
        {
        // Data type enumeration--required toomatch hello distinct list of types from OUTPUT statement
        switch (col.Type.Name.ToString().ToLower())
        {
            case "string": val = row.Get<string>(col.Name).ToString(); break;
            case "guid": val = row.Get<Guid>(col.Name).ToString(); break;
            default: break;
        }
        }
        // Handling NULL values--keeping them empty
        catch (System.NullReferenceException)
        {
        }
        streamWriter.Write(data_wrapper_on + val + data_wrapper_off);
    }
    streamWriter.Write("</tr>");

    if (isHeaderRow)
    {
        isHeaderRow = false;
    }
    // Reference toohello instance of hello IO.Stream object for footer generation
    g_writer = output.BaseStream;
    streamWriter.Flush();
    }
}

// Define hello factory classes
public static class Factory
{
    public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    return new HTMLOutputter(isHeader, encoding);
    }
}
```

Ve U-SQL temel betiği:

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.html";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
         FROM @input_file
         USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 
    too@output_file 
    USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

Tablo verisi bir HTML dosyası oluşturur bir HTML outputter budur.

### <a name="call-outputter-from-u-sql-base-script"></a>U-SQL temel betikten outputter çağırın
toocall özel outputter hello temel U-SQL komut dosyasından, oluşturulan toobe hello yeni hello outputter nesnesinin örneği vardır.

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

Merhaba örneği oluşturmayı tooavoid nesne temel komut dosyasında bizim önceki örnekte gösterildiği gibi bir işlevi sarmalayıcı oluşturabilir:

```c#
        // Define hello factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

Bu durumda, hello özgün çağrısı hello aşağıdaki gibi görünür:

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a>Kullanıcı tanımlı işlemcilerini kullanıyor.
Kullanıcı tanımlı işlemci veya UDP, U-SQL programlama özelliklerine uygulayarak tooprocess hello gelen satırları sağlayan UDO türüdür. UDP toocombine sütunları sağlar, değerleri değiştirmek ve gerekirse, yeni sütun ekleyin. Temel olarak bir satır kümesi tooproduce gerekli veri öğeleri tooprocess yardımcı olur.

toodefine bir UDP, ihtiyacımız toocreate bir `IProcessor` hello arabirimiyle `SqlUserDefinedProcessor` için UDP isteğe bağlı öznitelik.

Bu arabirim hello hello tanımı içermelidir `IRow` arabirimi satır kümesi geçersiz kılmak, hello aşağıdaki örnekte gösterildiği gibi:

```
[SqlUserDefinedProcessor]
public class MyProcessor: IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
        …
 }
}
```

**SqlUserDefinedProcessor** hello türü kullanıcı tanımlı bir işlemci olarak kayıtlı olduğunu belirtir. Bu sınıf devralınan olamaz.

Merhaba SqlUserDefinedProcessor özniteliği **isteğe bağlı** UDP tanımı.

Merhaba ana programlamasına nesneler **giriş** ve **çıkış**. Merhaba giriş kullanılan tooenumerate giriş sütunları ve çıktı ve tooset çıktı verilerini hello işlemci etkinliğinin sonucunda nesnesidir.

Giriş sütunları numaralandırması için kullandığımız hello `input.Get` yöntemi.

```
string column_name = input.Get<string>("column_name");
```

parametresi için hello `input.Get` yöntemdir hello bir parçası olarak geçirilen bir sütun `PRODUCE` hello yan tümcesi `PROCESS` temel hello U-SQL komut dosyası ifadesi. Toouse ihtiyacımız hello doğru veri buraya yazın.

Çıkış için hello kullan `output.Set` yöntemi.

Önemli toonote o özel üretici yalnızca çıkarır sütunlar ve hello ile tanımlı değerler `output.Set` yöntem çağrısı.

```
output.Set<string>("mycolumn", mycolumn);
```

Merhaba gerçek işlemci çıktı çağırarak tetiklenir `return output.AsReadOnly();`.

Bir işlemci örneği aşağıda verilmiştir:

```
[SqlUserDefinedProcessor]
public class FullDescriptionProcessor : IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
     string user = input.Get<string>("user");
     string des = input.Get<string>("des");
     string full_description = user.ToUpper() + "=>" + des;
     output.Set<string>("dt", input.Get<string>("dt"));
     output.Set<string>("full_description", full_description);
     output.Set<Guid>("new_guid", Guid.NewGuid());
     output.Set<Guid>("guid", input.Get<Guid>("guid"));
     return output.AsReadOnly();
 }
}
```

Bu kullanım örneği senaryosu hello işlemci büyük harf ve "des" "kullanıcı" Merhaba varolan sütunlar--bu durumda, birleştirerek "full_description" adlı yeni bir sütun oluşturuyor. Ayrıca, bir GUID oluşturur ve hello özgün ve yeni GUID değerleri döndürür.

Merhaba önceki örnekte görebildiğiniz gibi C# sırasında yöntemi çağırabilirsiniz `output.Set` yöntem çağrısı.

Özel bir işlemci kullanan temel U-SQL komut dosyası örneği verilmiştir:

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
     PROCESS @rs0
     PRODUCE dt String,
             full_description String,
             guid Guid,
             new_guid Guid
     USING new USQL_Programmability.FullDescriptionProcessor();

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a>Kullanıcı tanımlı appliers kullanın
Kullanıcı tanımlı bir U-SQL applier hello dış tablo ifadesi bir sorgu tarafından döndürülen her satır için tooinvoke özel C# işlevi sağlar. Merhaba sağ giriş hello sol giriş gelen her satır için hesaplanan ve üretilen hello satırları hello son çıktı için birleştirilir. Merhaba hello UYGULA operatör tarafından üretilen sütunları listesidir hello sol ve sağ giriş hello sütunlar hello kümesiyle hello birleşimi.

Kullanıcı tanımlı applier hello USQL seçin ifadesi bir parçası olarak çağrılır.

Merhaba tipik kullanıcı tanımlı applier görünüyor hello aşağıdaki gibi toohello arayın:

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

Bir SELECT ifadesinde appliers kullanma hakkında daha fazla bilgi için bkz: [seçin, U-SQL seçme ARASI uygulamak ve OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).

Merhaba kullanıcı tanımlı applier temel sınıf tanımı aşağıdaki gibidir:

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

Kullanıcı tanımlı bir applier toodefine ihtiyacımız toocreate hello `IApplier` hello arabirimiyle [`SqlUserDefinedApplier`] özniteliği için kullanıcı tanımlı applier tanım isteğe bağlıdır.

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
    public ParserApplier()
    {
        …
    }

    public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
    {
        …
    }
}
```

* Uygulama hello dış tablodaki her satır için çağrılır. Merhaba döndürür `IUpdatableRow` satır kümesi çıktı.
* Merhaba Oluşturucusu kullanılan toopass parametreleri toohello applier kullanıcı tanımlı bir sınıftır.

**SqlUserDefinedApplier** hello türü kullanıcı tanımlı bir applier kayıtlı olduğunu belirtir. Bu sınıf devralınan olamaz.

**SqlUserDefinedApplier** olan **isteğe bağlı** kullanıcı tanımlı applier tanımı.


Merhaba ana programlamasına nesneleri aşağıdaki gibidir:

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

Giriş satır kümeleri olarak geçirilir `IRow` giriş. Merhaba çıkış satır olarak oluşturulan `IUpdatableRow` çıkış arabirimi.

Tek tek sütun adlarına göre arama hello belirlenebilir `IRow` şema yöntemi.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

Merhaba gelen tooget hello gerçek veri değerleri `IRow`, hello Get() yöntemi kullanırız `IRow` arabirimi.

```
mycolumn = row.Get<int>("mycolumn")
```

Veya hello şema sütun adı kullanırız:

```
row.Get<int>(row.Schema[0].Name)
```

Merhaba çıkış değerleri ile ayarlanmalıdır `IUpdatableRow` çıktı:

```
output.Set<int>("mycolumn", mycolumn)
```

Özel appliers sütunlar ve ile tanımlanmış değerler yalnızca çıktı önemli toounderstand olan `output.Set` yöntem çağrısı.

Merhaba gerçek çıkış çağırarak tetiklenir `yield return output.AsReadOnly();`.

Merhaba kullanıcı tanımlı applier parametreleri toohello Oluşturucusu geçirilebilir. Applier hello applier temel U-SQL betiği çağrısında sırasında tanımlanan toobe gereken sütunlar değişken sayıda geri dönebilirsiniz.

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

Merhaba kullanıcı tanımlı applier örneği şöyledir:

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
private string parsingPart;

public ParserApplier(string parsingPart)
{
    if (parsingPart.ToUpper().Contains("ALL")
    || parsingPart.ToUpper().Contains("MAKE")
    || parsingPart.ToUpper().Contains("MODEL")
    || parsingPart.ToUpper().Contains("YEAR")
    || parsingPart.ToUpper().Contains("TYPE")
    || parsingPart.ToUpper().Contains("MILLAGE")
    )
    {
    this.parsingPart = parsingPart;
    }
    else
    {
    throw new ArgumentException("Incorrect parameter. Please use: 'ALL[MAKE|MODEL|TYPE|MILLAGE]'");
    }
}

public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
{

    string[] properties = input.Get<string>("properties").Split(',');

    //  only process with correct number of properties
    if (properties.Count() == 5)
    {

    string make = properties[0];
    string model = properties[1];
    string year = properties[2];
    string type = properties[3];
    int millage = -1;

    // Only return millage if it is number, otherwise, -1
    if (!int.TryParse(properties[4], out millage))
    {
        millage = -1;
    }

    if (parsingPart.ToUpper().Contains("MAKE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("make", make);
    if (parsingPart.ToUpper().Contains("MODEL") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("model", model);
    if (parsingPart.ToUpper().Contains("YEAR") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("year", year);
    if (parsingPart.ToUpper().Contains("TYPE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("type", type);
    if (parsingPart.ToUpper().Contains("MILLAGE") || parsingPart.ToUpper().Contains("ALL")) output.Set<int>("millage", millage);
    }
    yield return output.AsReadOnly();            
}
}
```

Bu kullanıcı tarafından tanımlanan applier hello temel U-SQL betiği aşağıdadır:

```
DECLARE @input_file string = @"c:\usql-programmability\car_fleet.tsv";
DECLARE @output_file string = @"c:\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        stocknumber int,
        vin String,
        properties String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT
        r.stocknumber,
        r.vin,
        properties.make,
        properties.model,
        properties.year,
        properties.type,
        properties.millage
    FROM @rs0 AS r
    CROSS APPLY
    new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

Bu kullanım örnek senaryoda, kullanıcı tanımlı applier görevi görür hello araba için virgülle ayrılmış değer ayrıştırıcı özellikleri yakıt. Merhaba giriş dosyası satırları hello şu şekilde görünür:

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

Normal bir sekmeyle ayrılmış TSV dosya marka ve model gibi araba özellikleri içeren özellikleri sütunu var. Bu özellikler ayrıştırılmış toohello tablo sütunları olması gerekir. sağlanan hello applier ayrıca hello özelliklerinde dinamik bir dizi satır kümesi, geçirilen hello parametresi temelinde neden toogenerate sağlar. Tüm özellikleri veya özellikler yalnızca belirli bir grup oluşturabilirsiniz.

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

Merhaba kullanıcı tanımlı applier applier nesnesinin yeni bir örneğini çağrılabilir:

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

Veya bir sarmalayıcı fabrika yöntemi hello çağrıldı:

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a>Kullanıcı tanımlı combiners kullanın
Kullanıcı tanımlı Birleştirici veya UDC, sol ve sağ satır kümeleri özel mantığına göre toocombine satırları etkinleştirir. Kullanıcı tanımlı birleştirici birleştirme ifadesiyle kullanılır.

Her iki hello giriş satır kümeleri hakkında gerekli bilgileri hello sağlar hello birleştirme ifade ile bir Birleştirici çağrılmakta, sütunlar hello gruplandırma hello beklenen sonucu şema ve ek bilgi.

temel bir U-SQL komut dosyasında bir Birleştirici toocall, söz dizimi aşağıdaki hello kullanın:

```
Combine_Expression :=
    'COMBINE' Combine_Input
    'WITH' Combine_Input
    Join_On_Clause
    Produce_Clause
    [Readonly_Clause]
    [Required_Clause]
    USING_Clause.
```

Daha fazla bilgi için bkz: [BİRLEŞTİRMEK ifade (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).

Kullanıcı tanımlı bir Birleştirici toodefine ihtiyacımız toocreate hello `ICombiner` hello arabirimiyle [`SqlUserDefinedCombiner`] özniteliği için bir kullanıcı tarafından tanımlanan birleştirici tanım isteğe bağlıdır.

Temel `ICombiner` sınıf tanımı:

```
public abstract class ICombiner : IUserDefinedOperator
{
protected ICombiner();
public virtual IEnumerable<IRow> Combine(List<IRowset> inputs,
       IUpdatableRow output);
public abstract IEnumerable<IRow> Combine(IRowset left, IRowset right,
       IUpdatableRow output);
}
```

Özel uyarlamasını hello bir `ICombiner` arabirimi hello tanımı içermelidir bir `IEnumerable<IRow>` geçersiz kılma birleştirin.

```
[SqlUserDefinedCombiner]
public class MyCombiner : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    …
}
}
```

Merhaba **SqlUserDefinedCombiner** öznitelik, hello türü kullanıcı tanımlı bir Birleştirici kayıtlı olduğunu gösterir. Bu sınıf devralınan olamaz.

**SqlUserDefinedCombiner** kullanılan toodefine hello Birleştirici modu özelliğidir. Bir kullanıcı tarafından tanımlanan birleştirici tanımı için isteğe bağlı bir özniteliktir.

CombinerMode modu

CombinerMode enum değerleri aşağıdaki hello alabilir:

* Her çıktı satır olası tüm hello giriş satırları bağlıdır tam (0) sol ve sağ hello ile aynı anahtar değeri.

* Sol (1) tek bir giriş satır hello soldan her çıktı satır bağlıdır (ve büyük olasılıkla tüm satırları hello hello sağ ile aynı anahtar değeri).

* Sağa doğru hello tek giriş satırdan her çıktı satır bağlıdır (2) (ve büyük olasılıkla tüm satırları hello ile Merhaba soldan aynı anahtar değeri).

* Her çıktı satır bağlıdır tek bir giriş, iç (3) satır sol ve sağ hello ile aynı değer.

Örnek: [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]


Merhaba ana programlamasına nesneler şunlardır:

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

Giriş satır kümeleri olarak geçirilir **sol** ve **sağ** `IRowset` arabirimi türü. Her iki satır kümeleri işleme için numaralandırılmış gerekir. Böylece tooenumerate sahip ve gerekirse, önbelleğe yalnızca her bir arabirime bir kez sıralayabilirsiniz.

Amacıyla önbelleğe alma işlemi için bir liste oluşturabilir\<T\> tür bellek yapısı sonuç olarak bir LINQ Sorgu yürütme, özellikle listesi <`IRow`>. Merhaba anonim veri türü de numaralandırma sırasında kullanılabilir.

Bkz: [giriş tooLINQ sorgular (C#)](https://msdn.microsoft.com/library/bb397906.aspx) LINQ sorguları hakkında daha fazla bilgi ve [IEnumerable\<T\> arabirimi](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) IEnumerablehakkındadahafazlabilgiiçin\<T\> arabirimi.

Merhaba gelen tooget hello gerçek veri değerleri `IRowset`, hello Get() yöntemi kullanırız `IRow` arabirimi.

```
mycolumn = row.Get<int>("mycolumn")
```

Tek tek sütun adlarına göre arama hello belirlenebilir `IRow` şema yöntemi.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

Veya hello şema sütun adı kullanarak:

```
c# row.Get<int>(row.Schema[0].Name)
```

LINQ ile Merhaba genel numaralandırma hello aşağıdaki gibi görünür:

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

Her iki satır kümeleri numaralandırma sonra tüm satırların üzerinden tooloop çağıracaksınız. Merhaba sol satır kümesindeki her satır için biz toofind bizim Birleştirici hello koşulu karşılayan tüm satırları adımıdır.

Merhaba çıkış değerleri ile ayarlanmalıdır `IUpdatableRow` çıktı.

```
output.Set<int>("mycolumn", mycolumn)
```

Merhaba gerçek çıkış çok çağırarak tetiklenir`yield return output.AsReadOnly();`.

Birleştirici örnek aşağıda verilmiştir:

```
[SqlUserDefinedCombiner]
public class CombineSales : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    var internetSales =
    (from row in left.Rows
          select new
          {
              ProductKey = row.Get<int>("ProductKey"),
              OrderDateKey = row.Get<int>("OrderDateKey"),
              SalesAmount = row.Get<decimal>("SalesAmount"),
              TaxAmt = row.Get<decimal>("TaxAmt")
          }).ToList();

    var resellerSales =
    (from row in right.Rows
     select new
     {
     ProductKey = row.Get<int>("ProductKey"),
     OrderDateKey = row.Get<int>("OrderDateKey"),
     SalesAmount = row.Get<decimal>("SalesAmount"),
     TaxAmt = row.Get<decimal>("TaxAmt")
     }).ToList();

    foreach (var row_i in internetSales)
    {
    foreach (var row_r in resellerSales)
    {

        if (
        row_i.OrderDateKey > 0
        && row_i.OrderDateKey < row_r.OrderDateKey
        && row_i.OrderDateKey == 20010701
        && (row_r.SalesAmount + row_r.TaxAmt) > 20000)
        {
        output.Set<int>("OrderDateKey", row_i.OrderDateKey);
        output.Set<int>("ProductKey", row_i.ProductKey);
        output.Set<decimal>("Internet_Sales_Amount", row_i.SalesAmount + row_i.TaxAmt);
        output.Set<decimal>("Reseller_Sales_Amount", row_r.SalesAmount + row_r.TaxAmt);
        }

    }
    }
    yield return output.AsReadOnly();
}
}
```

Bu kullanım örneği senaryosu biz analizi raporu hello satıcısında için oluşturmakta olduğunuz. Merhaba, belirli bir zaman çerçevesi içinde hello normal perakende üzerinden daha hızlı hello Web sitesi aracılığıyla maliyet birden fazla $20.000 ve, tüm ürünleri satmak toofind hedefidir.

Merhaba temel U-SQL betiği aşağıdadır. Normal bir birleştirme ve bir Birleştirici arasında hello mantığı karşılaştırabilirsiniz:

```sql
DECLARE @LocalURI string = @"\usql-programmability\";

DECLARE @input_file_internet_sales string = @LocalURI+"FactInternetSales.txt";
DECLARE @input_file_reseller_sales string = @LocalURI+"FactResellerSales.txt";
DECLARE @output_file1 string = @LocalURI+"output_file1.tsv";
DECLARE @output_file2 string = @LocalURI+"output_file2.tsv";

@fact_internet_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    CustomerKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_internet_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@fact_reseller_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    ResellerKey int ,
    EmployeeKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_reseller_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@rs1 =
SELECT
    fis.OrderDateKey,
    fis.ProductKey,
    fis.SalesAmount+fis.TaxAmt AS Internet_Sales_Amount,
    frs.SalesAmount+frs.TaxAmt AS Reseller_Sales_Amount
FROM @fact_internet_sales AS fis
     INNER JOIN @fact_reseller_sales AS frs
     ON fis.ProductKey == frs.ProductKey
WHERE
    fis.OrderDateKey < frs.OrderDateKey
    AND fis.OrderDateKey == 20010701
    AND frs.SalesAmount+frs.TaxAmt > 20000;

@rs2 =
COMBINE @fact_internet_sales AS fis
WITH @fact_reseller_sales AS frs
ON fis.ProductKey == frs.ProductKey
PRODUCE OrderDateKey int,
        ProductKey int,
        Internet_Sales_Amount decimal,
        Reseller_Sales_Amount decimal
USING new USQL_Programmability.CombineSales();

OUTPUT @rs1 too@output_file1 USING Outputters.Tsv();
OUTPUT @rs2 too@output_file2 USING Outputters.Tsv();
```

Kullanıcı tanımlı bir Birleştirici hello applier nesnesinin yeni bir örneğini çağrılabilir:

```
USING new MyNameSpace.MyCombiner();
```


Veya bir sarmalayıcı fabrika yöntemi hello çağrıldı:

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a>Kullanıcı tanımlı reducers kullanın

U-SQL, C# toowrite özel satır kümesi reducers hello kullanıcı tanımlı işleci Genişletilebilirlik Çerçevesi'ni kullanıp IReducer arabirimi uygulama sağlar.

Kullanıcı tanımlı reducer veya UDR, kullanılan tooeliminate gereksiz satır veri ayıklama sırasında (içe aktarma) olabilir. Ayrıca kullanılan toomanipulate ve olması satırları ve sütunları değerlendirin. Programlanabilirlik mantığına göre onu da hangi satırların ayıklanan toobe gereksinim tanımlayabilirsiniz.

toodefine UDR sınıfı, ihtiyacımız toocreate bir `IReducer` isteğe bağlı bir arabirimiyle `SqlUserDefinedReducer` özniteliği.

Bu sınıf arabirimi hello için bir tanım içermelidir `IEnumerable` arabirimi satır kümesi geçersiz.

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
        …
    }

}
```

Merhaba **SqlUserDefinedReducer** öznitelik, hello türü kullanıcı tanımlı bir reducer kayıtlı olduğunu gösterir. Bu sınıf devralınan olamaz.
**SqlUserDefinedReducer** kullanıcı tanımlı reducer tanımı için isteğe bağlı bir özniteliktir. Toodefine IsRecursive özelliği kullandı.

* bool IsRecursive    
* **doğru** bu Reducer ıdempotent olup olmadığını gösterir =

Merhaba ana programlamasına nesneler **giriş** ve **çıkış**. Merhaba giriş kullanılan tooenumerate giriş satırları nesnesidir. Çıktı etkinlik azaltma sonucu olarak kullanılan tooset çıkış satır sayısıdır.

Giriş satırları numaralandırması için kullandığımız hello `Row.Get` yöntemi.

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

hello için parametresi hello `Row.Get` yöntemdir hello bir parçası olarak geçirilen bir sütun `PRODUCE` hello sınıfının `REDUCE` temel hello U-SQL komut dosyası ifadesi. Toouse ihtiyacımız burada hello doğru veri türü de.

Çıkış için hello kullan `output.Set` yöntemi.

İle tanımlanan özel reducer çıkışları değerler yalnızca hello önemli toounderstand olan `output.Set` yöntem çağrısı.

```
output.Set<string>("mycolumn", guid);
```

Merhaba gerçek reducer çıkış çağırarak tetiklenir `yield return output.AsReadOnly();`.

Reducer örnek aşağıda verilmiştir:

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
    string guid;
    DateTime dt;
    string user;
    string des;

    foreach (IRow row in input.Rows)
    {
        guid = row.Get<string>("guid");
        dt = row.Get<DateTime>("dt");
        user = row.Get<string>("user");
        des = row.Get<string>("des");

        if (user.Length > 0)
        {
        output.Set<string>("guid", guid);
        output.Set<DateTime>("dt", dt);
        output.Set<string>("user", user);
        output.Set<string>("des", des);

        yield return output.AsReadOnly();
        }
    }
    }

}
```

Bu kullanım örneği senaryosu hello reducer boş kullanıcı adı satırlarla atlıyor. Her satır kümesinde için gereken her sütun okur, ardından hello hello kullanıcı adının uzunluğu değerlendirir. Kullanıcı adı değer uzunluğu 0'dan ise hello gerçek satır çıkarır.

Özel reducer kullanan temel U-SQL komut dosyası aşağıdadır:

```
DECLARE @input_file string = @"\usql-programmability\input_file_reducer.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    REDUCE @rs0 PRESORT guid
    ON guid  
    PRODUCE guid string, dt DateTime, user String, des String
    USING new USQL_Programmability.EmptyUserReducer();

@rs2 =
    SELECT guid AS start_id,
           dt AS start_time,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS start_fiscalperiod,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    too@output_file 
    USING Outputters.Text();
```
