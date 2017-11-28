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
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="9e433-103">U-SQL Programlama Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="9e433-103">U-SQL programmability guide</span></span>

<span data-ttu-id="9e433-104">U-SQL, büyük veri türü için iş yüklerinin tasarlanmış bir sorgu dildir.</span><span class="sxs-lookup"><span data-stu-id="9e433-104">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="9e433-105">Merhaba benzersiz özelliklerinden biri U-SQL hello hello SQL benzeri tanımlayıcı dili hello genişletilebilirlik ve C# tarafından sağlanan programlama ile birleşimidir.</span><span class="sxs-lookup"><span data-stu-id="9e433-105">One of hello unique features of U-SQL is hello combination of hello SQL-like declarative language with hello extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="9e433-106">Bu kılavuzda, biz hello genişletilebilirlik ve C# kullanarak etkin hello U-SQL dili ile programlama yoğunlaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e433-106">In this guide, we concentrate on hello extensibility and programmability of hello U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="9e433-107">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="9e433-107">Requirements</span></span>

<span data-ttu-id="9e433-108">İndirme ve yükleme [Visual Studio için Azure Data Lake Araçları](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="9e433-108">Download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="9e433-109">U-SQL ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="9e433-109">Get started with U-SQL</span></span>  

<span data-ttu-id="9e433-110">U-SQL betiği aşağıdaki hello bakalım:</span><span class="sxs-lookup"><span data-stu-id="9e433-110">Let’s look at hello following U-SQL script:</span></span>

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

<span data-ttu-id="9e433-111">Adlı bir satır kümesi tanımlar @a ve adlı bir satır kümesi oluşturur @results gelen @a.</span><span class="sxs-lookup"><span data-stu-id="9e433-111">It defines a RowSet called @a and creates a RowSet called @results from @a.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="9e433-112">C# türleri ve U-SQL betiği ifadeleri</span><span class="sxs-lookup"><span data-stu-id="9e433-112">C# types and expressions in U-SQL script</span></span>

<span data-ttu-id="9e433-113">Bir C# ifadesi gibi U-SQL mantıksal işlemleriyle birlikte bir U-SQL ifadesidir `AND`, `OR`, ve `NOT`.</span><span class="sxs-lookup"><span data-stu-id="9e433-113">A U-SQL Expression is a C# expression combined with U-SQL logical operations such `AND`, `OR`, and `NOT`.</span></span> <span data-ttu-id="9e433-114">U-SQL deyimleri seçin, ayıklama, kullanılabilir nerede, otomatik olarak sahip olmak ve GROUP BY BİLDİRİN.</span><span class="sxs-lookup"><span data-stu-id="9e433-114">U-SQL Expressions can be used with SELECT, EXTRACT, WHERE, HAVING, GROUP BY and DECLARE.</span></span>

<span data-ttu-id="9e433-115">Örneğin, komut dosyası izleyen hello bir dize bir DateTime değeri hello SELECT yan tümcesinde ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="9e433-115">For example, hello following script parses a string a DateTime value in hello SELECT clause.</span></span>

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

<span data-ttu-id="9e433-116">Merhaba aşağıdaki komut dosyasını bir dize bir DateTime değeri DECLARE deyimi içinde ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="9e433-116">hello following script parses a string a DateTime value in a DECLARE statement.</span></span>

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="9e433-117">Veri türü dönüştürmeleri için C# ifadeleri kullanma</span><span class="sxs-lookup"><span data-stu-id="9e433-117">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="9e433-118">C# ifadeler kullanarak bir datetime veri dönüştürme nasıl yapabilirsiniz aşağıdaki örneğine hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="9e433-118">hello following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="9e433-119">Bu belirli bir senaryoda, gece yarısı 00:00:00 saat gösterimi dönüştürülmüş toostandard datetime dize datetime verilerdir.</span><span class="sxs-lookup"><span data-stu-id="9e433-119">In this particular scenario, string datetime data is converted toostandard datetime with midnight 00:00:00 time notation.</span></span>

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="9e433-120">Bugünün tarihini C# ifadeleri kullanma</span><span class="sxs-lookup"><span data-stu-id="9e433-120">Use C# expressions for today’s date</span></span>
<span data-ttu-id="9e433-121">toopull bugünün tarihini, C# ifade aşağıdaki hello biz kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9e433-121">toopull today’s date, we can use hello following C# expression:</span></span>

```
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="9e433-122">Örneği nasıl toouse bu ifadede bir komut dosyası:</span><span class="sxs-lookup"><span data-stu-id="9e433-122">Here's an example of how toouse this expression in a script:</span></span>

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



## <a name="using-net-assemblies"></a><span data-ttu-id="9e433-123">.NET derlemelerini kullanma</span><span class="sxs-lookup"><span data-stu-id="9e433-123">Using .NET assemblies</span></span>
<span data-ttu-id="9e433-124">U-SQL'nin genişletilebilirlik modeli yoğun hello özelliği tooadd özel kodunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="9e433-124">U-SQL’s extensibility model relies heavily on hello ability tooadd custom code.</span></span> <span data-ttu-id="9e433-125">Şu anda, U-SQL, kolay yolları tooadd ile kendi Microsoft sağlar. NET tabanlı kodda (özellikle, C#).</span><span class="sxs-lookup"><span data-stu-id="9e433-125">Currently, U-SQL provides you with easy ways tooadd your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="9e433-126">Ancak, VB.NET veya F # gibi diğer .NET dilleri yazılmış özel kod ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e433-126">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span> 

### <a name="register-a-net-assembly"></a><span data-ttu-id="9e433-127">Bir .NET derlemesi kaydetme</span><span class="sxs-lookup"><span data-stu-id="9e433-127">Register a .NET assembly</span></span>

<span data-ttu-id="9e433-128">Merhaba CREATE ASSEMBLY deyimi tooplace bir U-SQL veritabanına bir .NET derlemesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="9e433-128">Use hello CREATE ASSEMBLY statement tooplace a .NET assembly into a U-SQL Database.</span></span> <span data-ttu-id="9e433-129">Bir veritabanında bir derlemeyi olduktan sonra U-SQL betikleri hello referans DERLEMESİNİ deyimi kullanarak bu derlemeler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e433-129">Once an assembly is in a database, U-SQL scripts can use those assemblies by using hello REFERENCE ASSEMBLY statement.</span></span> 

<span data-ttu-id="9e433-130">kodun gösterdiği nasıl aşağıdaki hello tooregister bütünleştirilmiş:</span><span class="sxs-lookup"><span data-stu-id="9e433-130">hello following code shows how tooregister an assembly:</span></span>

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

<span data-ttu-id="9e433-131">kodun gösterdiği nasıl aşağıdaki hello tooreference bütünleştirilmiş:</span><span class="sxs-lookup"><span data-stu-id="9e433-131">hello following code shows how tooreference an assembly:</span></span>

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

<span data-ttu-id="9e433-132">Merhaba başvurun [derleme kayıt yönergeleri](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) , bu konuda daha ayrıntılı ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9e433-132">Consult hello [assembly registration instructions](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) that covers this topic in greater detail.</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="9e433-133">Derleme sürümü oluşturma kullanın</span><span class="sxs-lookup"><span data-stu-id="9e433-133">Use assembly versioning</span></span>
<span data-ttu-id="9e433-134">Şu anda, U-SQL hello .NET Framework sürüm 4.5 kullanır.</span><span class="sxs-lookup"><span data-stu-id="9e433-134">Currently, U-SQL uses hello .NET Framework version 4.5.</span></span> <span data-ttu-id="9e433-135">Bu nedenle, kendi derlemeleri hello çalışma zamanı bu sürümü ile uyumlu olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9e433-135">So ensure that your own assemblies are compatible with that version of hello runtime.</span></span>

<span data-ttu-id="9e433-136">U-SQL kodun bir 64-bit (x 64) biçiminde daha önce belirtildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="9e433-136">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="9e433-137">Böylece kodunuzu derlenmiş toorun x64 üzerinde olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9e433-137">So make sure that your code is compiled toorun on x64.</span></span> <span data-ttu-id="9e433-138">Aksi takdirde, daha önce gösterilen hello yanlış biçim hatası alırsınız.</span><span class="sxs-lookup"><span data-stu-id="9e433-138">Otherwise you get hello incorrect format error shown earlier.</span></span>

<span data-ttu-id="9e433-139">Her derleme dll dosyasını karşıya ve farklı bir çalışma zamanı, yerel bir derleme veya bir yapılandırma dosyası gibi bir kaynak dosya en fazla 400 MB olabilir.</span><span class="sxs-lookup"><span data-stu-id="9e433-139">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="9e433-140">Kaynak dağıtma aracılığıyla veya başvuruları tooassemblies ve bunların ek dosyaları aracılığıyla dağıtılan kaynakları Hello toplam boyutu 3 GB aşamaz.</span><span class="sxs-lookup"><span data-stu-id="9e433-140">hello total size of deployed resources, either via DEPLOY RESOURCE or via references tooassemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="9e433-141">Son olarak, her U-SQL veritabanı herhangi verilen derleme bir sürümü yalnızca içerebileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9e433-141">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="9e433-142">Sürüm 7 ve 8 sürümü hello NewtonSoft Json.Net kitaplığı ihtiyacınız varsa, örneğin, tooregister gereken iki farklı veritabanlarındaki bunları.</span><span class="sxs-lookup"><span data-stu-id="9e433-142">For example, if you need both version 7 and version 8 of hello NewtonSoft Json.Net library, you need tooregister them in two different databases.</span></span> <span data-ttu-id="9e433-143">Ayrıca, her komut dosyası yalnızca belirli bir derleme DLL tooone sürümü başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="9e433-143">Furthermore, each script can only refer tooone version of a given assembly DLL.</span></span> <span data-ttu-id="9e433-144">Bu bakımdan, U-SQL Yönetimi ve sürüm oluşturma derleme hello C# semantiği izler.</span><span class="sxs-lookup"><span data-stu-id="9e433-144">In this respect, U-SQL follows hello C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="9e433-145">Kullanıcı tanımlı işlevler kullanın: UDF</span><span class="sxs-lookup"><span data-stu-id="9e433-145">Use user-defined functions: UDF</span></span>
<span data-ttu-id="9e433-146">U-SQL kullanıcı tanımlı işlevler veya UDF, parametreleri kabul eder, (örneğin, karmaşık bir hesaplama) bir eylem gerçekleştirmek ve bir değer olarak bu eylemin hello sonuç yordamları programlama.</span><span class="sxs-lookup"><span data-stu-id="9e433-146">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return hello result of that action as a value.</span></span> <span data-ttu-id="9e433-147">Merhaba Döndür UDF değeri yalnızca tek bir skaler olabilir.</span><span class="sxs-lookup"><span data-stu-id="9e433-147">hello return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="9e433-148">U-SQL UDF temel U-SQL betiği diğer C# skaler bir işlev gibi çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="9e433-148">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="9e433-149">U-SQL kullanıcı tanımlı işlevler olarak başlatma öneririz **ortak** ve **statik**.</span><span class="sxs-lookup"><span data-stu-id="9e433-149">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

<span data-ttu-id="9e433-150">İlk bir UDF oluşturma hello basit örneğe bakalım.</span><span class="sxs-lookup"><span data-stu-id="9e433-150">First let’s look at hello simple example of creating a UDF.</span></span>

<span data-ttu-id="9e433-151">Bu kullanım örneği senaryosu hello mali çeyreği ve mali ayı hello ilk oturum açma hello belirli bir kullanıcı için de dahil olmak üzere toodetermine hello mali süresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e433-151">In this use-case scenario, we need toodetermine hello fiscal period, including hello fiscal quarter and fiscal month of hello first sign-in for hello specific user.</span></span> <span data-ttu-id="9e433-152">Merhaba bizim senaryoda hello yılın ilk mali ayı Haziran ' dir.</span><span class="sxs-lookup"><span data-stu-id="9e433-152">hello first fiscal month of hello year in our scenario is June.</span></span>

<span data-ttu-id="9e433-153">toocalculate mali dönem, biz C# işlevi aşağıdaki hello sunar:</span><span class="sxs-lookup"><span data-stu-id="9e433-153">toocalculate fiscal period, we introduce hello following C# function:</span></span>

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

<span data-ttu-id="9e433-154">Mali ayı ve üç aylık dönem hesaplar ve bir string değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="9e433-154">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="9e433-155">Merhaba ilk ayın hello ilk mali çeyreği, Haziran için "Q1:P1" kullanın.</span><span class="sxs-lookup"><span data-stu-id="9e433-155">For June, hello first month of hello first fiscal quarter, we use "Q1:P1".</span></span> <span data-ttu-id="9e433-156">Temmuz, biz "Q1:P2" kullanın ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="9e433-156">For July, we use "Q1:P2", and so on.</span></span>

<span data-ttu-id="9e433-157">Devam eden toouse U-SQL Projemizin gerçekleştirildiğine dair normal bir C# işlevi budur.</span><span class="sxs-lookup"><span data-stu-id="9e433-157">This is a regular C# function that we are going toouse in our U-SQL project.</span></span>

<span data-ttu-id="9e433-158">Merhaba arka plan kodu bölüm bu senaryoda, nasıl göründüğünü aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9e433-158">Here is how hello code-behind section looks in this scenario:</span></span>

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

<span data-ttu-id="9e433-159">Şimdi biz toocall bu işlev hello temel U-SQL komut dosyasından adımıdır.</span><span class="sxs-lookup"><span data-stu-id="9e433-159">Now we are going toocall this function from hello base U-SQL script.</span></span> <span data-ttu-id="9e433-160">toodo Bu, biz tooprovide hello ad alanı, bu durumda NameSpace.Class.Function(parameter) olduğu dahil olmak üzere hello işlevi için tam bir ada sahip.</span><span class="sxs-lookup"><span data-stu-id="9e433-160">toodo this, we have tooprovide a fully qualified name for hello function, including hello namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="9e433-161">Merhaba gerçek U-SQL temel betiği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="9e433-161">Following is hello actual U-SQL base script:</span></span>

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

<span data-ttu-id="9e433-162">Merhaba çıktı dosyası hello komut dosyası yürütme aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="9e433-162">Following is hello output file of hello script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="9e433-163">Bu örnek, basit bir satır içi U-SQL UDF'de kullanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="9e433-163">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="9e433-164">UDF çağrılarını arasında durumu tutun</span><span class="sxs-lookup"><span data-stu-id="9e433-164">Keep state between UDF invocations</span></span>
<span data-ttu-id="9e433-165">U-SQL C# programlama nesnelerini daha, hello arka plan kodu Genel değişkenler aracılığıyla etkileşim kullanan gelişmiş.</span><span class="sxs-lookup"><span data-stu-id="9e433-165">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through hello code-behind global variables.</span></span> <span data-ttu-id="9e433-166">İş kullanım örneği senaryosu aşağıdaki hello bakalım.</span><span class="sxs-lookup"><span data-stu-id="9e433-166">Let’s look at hello following business use-case scenario.</span></span>

<span data-ttu-id="9e433-167">Büyük kuruluşlarda, kullanıcıların iç uygulamaları çeşitleri arasında geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e433-167">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="9e433-168">Bunlar, Microsoft Dynamics CRM, Powerbı vb. içerebilir.</span><span class="sxs-lookup"><span data-stu-id="9e433-168">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="9e433-169">Müşteriler tooapply kullanıcıların hangi hello kullanım olan ve benzeri eğilimlerin farklı uygulamalar arasında nasıl geçiş, bir telemetri analizi isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e433-169">Customers might want tooapply a telemetry analysis of how users switch between different applications, what hello usage trends are, and so on.</span></span> <span data-ttu-id="9e433-170">Merhaba hello iş için toooptimize uygulama kullanımı hedeftir.</span><span class="sxs-lookup"><span data-stu-id="9e433-170">hello goal for hello business is toooptimize application usage.</span></span> <span data-ttu-id="9e433-171">Ayrıca toocombine farklı uygulamalar veya oturum açma belirli yordamları isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e433-171">They also might want toocombine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="9e433-172">tooachieve bu hedef toodetermine oturum kimlikleri ve gecikme süresi arasında hello oluştu son oturumun sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="9e433-172">tooachieve this goal, we have toodetermine session IDs and lag time between hello last session that occurred.</span></span>

<span data-ttu-id="9e433-173">Bir önceki oturum açma toofind gerekir ve oluşturulan toohello yükleniyor bu oturum açma tooall oturumları atamak aynı uygulama.</span><span class="sxs-lookup"><span data-stu-id="9e433-173">We need toofind a previous sign-in and then assign this sign-in tooall sessions that are being generated toohello same application.</span></span> <span data-ttu-id="9e433-174">Merhaba ilk temel U-SQL betiği bize tooapply hesaplamalar önceden hesaplanan sütunlar ÖTELEME işleviyle üzerinden izin vermez, iştir.</span><span class="sxs-lookup"><span data-stu-id="9e433-174">hello first challenge is that U-SQL base script doesn't allow us tooapply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="9e433-175">Merhaba ikinci tookeep hello hello içindeki tüm oturumlar için belirli bir oturum sahibiz iştir aynı süre.</span><span class="sxs-lookup"><span data-stu-id="9e433-175">hello second challenge is that we have tookeep hello specific session for all sessions within hello same time period.</span></span>

<span data-ttu-id="9e433-176">toosolve Bu sorun bir arka plan kodu bölüm içinde genel değişkeni kullanırız: `static public string globalSession;`.</span><span class="sxs-lookup"><span data-stu-id="9e433-176">toosolve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="9e433-177">Bu genel değişkeni bizim komut dosyası yürütme sırasında uygulanan toohello tüm satır kümesidir.</span><span class="sxs-lookup"><span data-stu-id="9e433-177">This global variable is applied toohello entire rowset during our script execution.</span></span>

<span data-ttu-id="9e433-178">U-SQL programımız hello arka plan kodu bölümü aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9e433-178">Here is hello code-behind section of our U-SQL program:</span></span>

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

<span data-ttu-id="9e433-179">Gösterir hello genel değişkeni Bu örnek `static public string globalSession;` hello içinde kullanılan `getStampUserSession` işlevi ve alma yeniden her zaman hello oturum parametresi değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="9e433-179">This example shows hello global variable `static public string globalSession;` used inside hello `getStampUserSession` function and getting reinitialized each time hello Session parameter is changed.</span></span>

<span data-ttu-id="9e433-180">Merhaba temel U-SQL betiği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9e433-180">hello U-SQL base script is as follows:</span></span>

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

<span data-ttu-id="9e433-181">İşlev `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` burada hello ikinci bellek satır kümesi hesaplama sırasında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="9e433-181">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during hello second memory rowset calculation.</span></span> <span data-ttu-id="9e433-182">Merhaba geçirir `UserSessionTimestamp` sütun ve döndürür hello değeri kadar `UserSessionTimestamp` değişti.</span><span class="sxs-lookup"><span data-stu-id="9e433-182">It passes hello `UserSessionTimestamp` column and returns hello value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="9e433-183">Merhaba çıktı dosyası aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9e433-183">hello output file is as follows:</span></span>

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

<span data-ttu-id="9e433-184">Bu örnek bir genel değişkeni uygulanan toohello tüm bellek satır kümesi olan bir arka plan kodu bölüm içinde kullandığımız daha karmaşık bir kullanım örneği senaryosu gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9e433-184">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied toohello entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="9e433-185">Kullanıcı tanımlı türler kullanın: UDT</span><span class="sxs-lookup"><span data-stu-id="9e433-185">Use user-defined types: UDT</span></span>
<span data-ttu-id="9e433-186">Kullanıcı tanımlı türler veya UDT, başka bir programlama, U-SQL özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="9e433-186">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="9e433-187">U-SQL UDT bir normal C# kullanıcı tanımlı tür gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="9e433-187">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="9e433-188">C# yerleşik ve özel kullanıcı tanımlı türler hello kullanılmasına kesin türü belirtilmiş bir dil değil.</span><span class="sxs-lookup"><span data-stu-id="9e433-188">C# is a strongly typed language that allows hello use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="9e433-189">U-SQL örtük olarak serileştirmek veya satır kümeleri tepe arasında hello UDT geçirildiğinde rasgele atama anlayabileceği olamaz.</span><span class="sxs-lookup"><span data-stu-id="9e433-189">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when hello UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="9e433-190">Bu, açık bir biçimlendirici tooprovide hello IFormatter arabirimini kullanarak hello kullanıcının sahip anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="9e433-190">This means that hello user has tooprovide an explicit formatter by using hello IFormatter interface.</span></span> <span data-ttu-id="9e433-191">Bu U-SQL ile Merhaba sağlar seri hale getirmek ve seri durumdan hello UDT yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="9e433-191">This provides U-SQL with hello serialize and de-serialize methods for hello UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="9e433-192">U-SQL'nin yerleşik ayıklayıcıları ve outputters şu anda serileştirmek veya seri durumdan UDT veri tooor dosyalarını bile hello IFormatter kümesi.</span><span class="sxs-lookup"><span data-stu-id="9e433-192">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data tooor from files even with hello IFormatter set.</span></span> <span data-ttu-id="9e433-193">UDT veri tooa hello çıkış deyimi dosyasıyla yazıyorsanız ya da toopass sahip bir ayıklayıcısı okuma, böyle bir string veya byte dizisi olarak.</span><span class="sxs-lookup"><span data-stu-id="9e433-193">So when you're writing UDT data tooa file with hello OUTPUT statement, or reading it with an extractor, you have toopass it as a string or byte array.</span></span> <span data-ttu-id="9e433-194">Ardından hello serileştirme çağırın ve kod (diğer bir deyişle, hello UDT'ın ToString() yöntemini) açıkça seri durumundan çıkarma.</span><span class="sxs-lookup"><span data-stu-id="9e433-194">Then you call hello serialization and deserialization code (that is, hello UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="9e433-195">Kullanıcı tanımlı ayıklayıcıları ve hello diğer üzerinde outputters el okuyabilir ve atama yazma.</span><span class="sxs-lookup"><span data-stu-id="9e433-195">User-defined extractors and outputters, on hello other hand, can read and write UDTs.</span></span>

<span data-ttu-id="9e433-196">Aşağıda gösterildiği gibi toouse AYIKLAYICISI veya OUTPUTTER (dışında önceki seçin), UDT deneyin ise:</span><span class="sxs-lookup"><span data-stu-id="9e433-196">If we try toouse UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="9e433-197">Aşağıdaki hata hello aldığımız:</span><span class="sxs-lookup"><span data-stu-id="9e433-197">We receive hello following error:</span></span>

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

<span data-ttu-id="9e433-198">outputter içinde toowork UDT ile ya da sahip olduğumuz tooserialize, toostring ile ToString() yöntemini hello veya özel bir outputter oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e433-198">toowork with UDT in outputter, we either have tooserialize it toostring with hello ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="9e433-199">Atama, grup tarafından şu anda kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="9e433-199">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="9e433-200">UDT grubu tarafından kullanılıyorsa, aşağıdaki hata hello oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="9e433-200">If UDT is used in GROUP BY, hello following error is thrown:</span></span>

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

<span data-ttu-id="9e433-201">UDT toodefine, biz gerekir:</span><span class="sxs-lookup"><span data-stu-id="9e433-201">toodefine a UDT, we have to:</span></span>

* <span data-ttu-id="9e433-202">Ad alanları aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9e433-202">Add hello following namespaces:</span></span>

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* <span data-ttu-id="9e433-203">Ekleme `Microsoft.Analytics.Interfaces`, hello UDT arabirimler için gerekli olduğu.</span><span class="sxs-lookup"><span data-stu-id="9e433-203">Add `Microsoft.Analytics.Interfaces`, which is required for hello UDT interfaces.</span></span> <span data-ttu-id="9e433-204">Ayrıca, `System.IO` gerekli toodefine hello IFormatter arabirimi olabilir.</span><span class="sxs-lookup"><span data-stu-id="9e433-204">In addition, `System.IO` might be needed toodefine hello IFormatter interface.</span></span>

* <span data-ttu-id="9e433-205">Kullanılan tanımlı bir tür SqlUserDefinedType özniteliğiyle tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="9e433-205">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="9e433-206">**SqlUserDefinedType** kullanılan toomark bir türü kullanıcı tanımlı bir tür (UDT) olarak derlemedeki U-SQL tanımıdır.</span><span class="sxs-lookup"><span data-stu-id="9e433-206">**SqlUserDefinedType** is used toomark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="9e433-207">Merhaba özellikleri hello öznitelikte hello UDT fiziksel özelliklerini hello yansıtır.</span><span class="sxs-lookup"><span data-stu-id="9e433-207">hello properties on hello attribute reflect hello physical characteristics of hello UDT.</span></span> <span data-ttu-id="9e433-208">Bu sınıf devralınan olamaz.</span><span class="sxs-lookup"><span data-stu-id="9e433-208">This class cannot be inherited.</span></span>

<span data-ttu-id="9e433-209">SqlUserDefinedType UDT tanımı için gerekli bir özniteliktir.</span><span class="sxs-lookup"><span data-stu-id="9e433-209">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="9e433-210">Merhaba sınıfının Hello Oluşturucusu:</span><span class="sxs-lookup"><span data-stu-id="9e433-210">hello constructor of hello class:</span></span>  

* <span data-ttu-id="9e433-211">SqlUserDefinedTypeAttribute (türü biçimlendirici)</span><span class="sxs-lookup"><span data-stu-id="9e433-211">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="9e433-212">Biçimlendirici yazın: gerekli parametre toodefine bir UDT biçimlendirici--özellikle hello hello türü `IFormatter` arabirimi gerekir bayraklarıdır burada.</span><span class="sxs-lookup"><span data-stu-id="9e433-212">Type formatter: Required parameter toodefine an UDT formatter--specifically, hello type of hello `IFormatter` interface must be passed here.</span></span>

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* <span data-ttu-id="9e433-213">Tipik UDT hello aşağıdaki örnekte gösterildiği gibi hello IFormatter arabirimi tanımını da gerektirir:</span><span class="sxs-lookup"><span data-stu-id="9e433-213">Typical UDT also requires definition of hello IFormatter interface, as shown in hello following example:</span></span>

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

<span data-ttu-id="9e433-214">Merhaba `IFormatter` arabirimi serileştirir ve hello kök türüne sahip bir nesne grafiğinin XML'deki serileştiren \<typeparamref name = "T" >.</span><span class="sxs-lookup"><span data-stu-id="9e433-214">hello `IFormatter` interface serializes and de-serializes an object graph with hello root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="9e433-215">\<typeparam name = "T" > merhaba kök türü için hello Nesne grafiği tooserialize ve seri durumdan.</span><span class="sxs-lookup"><span data-stu-id="9e433-215">\<typeparam name="T">hello root type for hello object graph tooserialize and de-serialize.</span></span>

* <span data-ttu-id="9e433-216">**Seri durumdan**: sağlanan hello akış hello verileri XML'deki serileştirir ve hello grafik nesnelerinin reconstitutes.</span><span class="sxs-lookup"><span data-stu-id="9e433-216">**Deserialize**: De-serializes hello data on hello provided stream and reconstitutes hello graph of objects.</span></span>

* <span data-ttu-id="9e433-217">**Seri hale**: bir nesne ya da nesne, grafik kök toohello sağlanan akış verilen hello ile Serileştirir.</span><span class="sxs-lookup"><span data-stu-id="9e433-217">**Serialize**: Serializes an object, or graph of objects, with hello given root toohello provided stream.</span></span>

<span data-ttu-id="9e433-218">`MyType`Örnek: Merhaba türünün örneği.</span><span class="sxs-lookup"><span data-stu-id="9e433-218">`MyType` instance: Instance of hello type.</span></span>  
<span data-ttu-id="9e433-219">`IColumnWriter`yazıcı / `IColumnReader` okuyucu: sütun akış temel hello.</span><span class="sxs-lookup"><span data-stu-id="9e433-219">`IColumnWriter` writer / `IColumnReader` reader: hello underlying column stream.</span></span>  
<span data-ttu-id="9e433-220">`ISerializationContext`Bağlam: Enum hello kaynak veya hedef bağlamı hello akış için serileştirme sırasında belirten bayrakları kümesini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9e433-220">`ISerializationContext` context: Enum that defines a set of flags that specifies hello source or destination context for hello stream during serialization.</span></span>

* <span data-ttu-id="9e433-221">**Ara**: Bu hello kaynak veya hedef bağlamı kalıcı depolama değil belirtir.</span><span class="sxs-lookup"><span data-stu-id="9e433-221">**Intermediate**: Specifies that hello source or destination context is not a persisted store.</span></span>

* <span data-ttu-id="9e433-222">**Kalıcılığı**: Bu hello kaynak veya hedef bağlam kalıcı depolama olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="9e433-222">**Persistence**: Specifies that hello source or destination context is a persisted store.</span></span>

<span data-ttu-id="9e433-223">Bir normal C# türü olarak bir U-SQL UDT tanımı geçersiz kılmaları işleçlerini gibi içerebilir +/ == /! =.</span><span class="sxs-lookup"><span data-stu-id="9e433-223">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="9e433-224">Statik yöntemler de içerir.</span><span class="sxs-lookup"><span data-stu-id="9e433-224">It can also include static methods.</span></span> <span data-ttu-id="9e433-225">Biz toouse bu UDT parametresi tooa U-SQL MIN toplama işlevi kullanacaksanız, örneğin, toodefine sahibiz < işleci geçersiz kılma.</span><span class="sxs-lookup"><span data-stu-id="9e433-225">For example, if we are going toouse this UDT as a parameter tooa U-SQL MIN aggregate function, we have toodefine < operator override.</span></span>

<span data-ttu-id="9e433-226">Bu kılavuzda daha önce Qn:Pn (Q1:P10) hello biçiminde hello belirli tarihten mali dönem tanımlaması için bir örnek gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9e433-226">Earlier in this guide, we demonstrated an example for fiscal period identification from hello specific date in hello format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="9e433-227">Aşağıdaki örnek hello nasıl toodefine özel mali dönem için değerler girin gösterir.</span><span class="sxs-lookup"><span data-stu-id="9e433-227">hello following example shows how toodefine a custom type for fiscal period values.</span></span>

<span data-ttu-id="9e433-228">Aşağıdaki özel UDT ve IFormatter arabirimi arka plan kodu bölümle örneğidir:</span><span class="sxs-lookup"><span data-stu-id="9e433-228">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

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

<span data-ttu-id="9e433-229">Merhaba tanımlı türünü içeren iki sayı: üç aylık dönem ve ay.</span><span class="sxs-lookup"><span data-stu-id="9e433-229">hello defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="9e433-230">İşleç == /! = / > / < ve statik yöntemi ToString() burada tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="9e433-230">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="9e433-231">Daha önce belirtildiği gibi UDT SELECT ifadelerde kullanılabilir, ancak OUTPUTTER/AYIKLAYICISI özel serileştirme kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="9e433-231">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="9e433-232">Ya da ToString() bir dize olarak serileştirilmiş veya özel bir OUTPUTTER/AYIKLAYICISI kullanılan toobe de vardır.</span><span class="sxs-lookup"><span data-stu-id="9e433-232">It either has toobe serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="9e433-233">Şimdi şimdi UDT kullanımını tartışın.</span><span class="sxs-lookup"><span data-stu-id="9e433-233">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="9e433-234">Arka plan kodu bölümünde bizim GetFiscalPeriod işlevi toohello aşağıdaki değiştirilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9e433-234">In a code-behind section, we changed our GetFiscalPeriod function toohello following:</span></span>

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

<span data-ttu-id="9e433-235">Gördüğünüz gibi bizim FiscalPeriod türü hello değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="9e433-235">As you can see, it returns hello value of our FiscalPeriod type.</span></span>

<span data-ttu-id="9e433-236">Burada nasıl toouse başka işlemler U-SQL temel komut dosyasında bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="9e433-236">Here we provide an example of how toouse it further in U-SQL base script.</span></span> <span data-ttu-id="9e433-237">Bu örnek, farklı UDT çağırma formlardan U-SQL betiği gösterir.</span><span class="sxs-lookup"><span data-stu-id="9e433-237">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

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

<span data-ttu-id="9e433-238">Bir tam arka plan kodu bölümü bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9e433-238">Here's an example of a full code-behind section:</span></span>

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

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="9e433-239">Kullanıcı tanımlı toplamlarda kullanın: UDAGG</span><span class="sxs-lookup"><span data-stu-id="9e433-239">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="9e433-240">Kullanıcı tanımlı toplamlarda, toplama ile ilgili olan tüm işlevler out-of--box U-SQL ile gönderilmeyen ' dir.</span><span class="sxs-lookup"><span data-stu-id="9e433-240">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="9e433-241">Merhaba örneği özel matematik hesaplamaları, dize birleştirmeler işlemeleri dizeler, bir toplama tooperform olması ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="9e433-241">hello example can be an aggregate tooperform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="9e433-242">Merhaba kullanıcı tanımlı toplama temel sınıf tanımı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9e433-242">hello user-defined aggregate base class definition is as follows:</span></span>

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

<span data-ttu-id="9e433-243">**SqlUserDefinedAggregate** hello türü kullanıcı tanımlı toplama olarak kayıtlı olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="9e433-243">**SqlUserDefinedAggregate** indicates that hello type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="9e433-244">Bu sınıf devralınan olamaz.</span><span class="sxs-lookup"><span data-stu-id="9e433-244">This class cannot be inherited.</span></span>

<span data-ttu-id="9e433-245">SqlUserDefinedType özniteliği **isteğe bağlı** UDAGG tanımı.</span><span class="sxs-lookup"><span data-stu-id="9e433-245">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="9e433-246">Merhaba temel sınıf toopass üç soyut parametrelerinin sağlar: iki giriş parametreleri ve bir hello sonucunda olarak.</span><span class="sxs-lookup"><span data-stu-id="9e433-246">hello base class allows you toopass three abstract parameters: two as input parameters and one as hello result.</span></span> <span data-ttu-id="9e433-247">Başlangıç veri türleri değişkendir ve sınıf devralma sırasında tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e433-247">hello data types are variable and should be defined during class inheritance.</span></span>

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

* <span data-ttu-id="9e433-248">**Init** hesaplaması sırasında her grup için bir kez çağırır.</span><span class="sxs-lookup"><span data-stu-id="9e433-248">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="9e433-249">Bu, her toplama grubu için bir başlatma yordamının sağlar.</span><span class="sxs-lookup"><span data-stu-id="9e433-249">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="9e433-250">**Accumulate** her bir değer için bir kez çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="9e433-250">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="9e433-251">Bu, hello toplama algoritması hello ana işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="9e433-251">It provides hello main functionality for hello aggregation algorithm.</span></span> <span data-ttu-id="9e433-252">Kullanılan tooaggregate değerleri sınıf devralma sırasında tanımlanan çeşitli veri türlerine sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="9e433-252">It can be used tooaggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="9e433-253">Değişken veri türünde iki parametre kabul edebilir.</span><span class="sxs-lookup"><span data-stu-id="9e433-253">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="9e433-254">**Sonlandırma** toooutput hello sonuç her grup için işleme hello sonunda toplama grubu başına bir kez çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="9e433-254">**Terminate** is executed once per aggregation group at hello end of processing toooutput hello result for each group.</span></span>

<span data-ttu-id="9e433-255">toodeclare doğru girdi ve çıktı veri türlerini kullanın hello sınıf tanımını gibi:</span><span class="sxs-lookup"><span data-stu-id="9e433-255">toodeclare correct input and output data types, use hello class definition as follows:</span></span>

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="9e433-256">T1: İlk parametre tooaccumulate</span><span class="sxs-lookup"><span data-stu-id="9e433-256">T1: First parameter tooaccumulate</span></span>
* <span data-ttu-id="9e433-257">T2: İlk parametre tooaccumulate</span><span class="sxs-lookup"><span data-stu-id="9e433-257">T2: First parameter tooaccumulate</span></span>
* <span data-ttu-id="9e433-258">TResult: dönüş türü Sonlandır</span><span class="sxs-lookup"><span data-stu-id="9e433-258">TResult: Return type of terminate</span></span>

<span data-ttu-id="9e433-259">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="9e433-259">For example:</span></span>

```
public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="9e433-260">or</span><span class="sxs-lookup"><span data-stu-id="9e433-260">or</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="9e433-261">U-SQL UDAGG kullanın</span><span class="sxs-lookup"><span data-stu-id="9e433-261">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="9e433-262">toouse UDAGG, ilk kod arkasında tanımlayın veya daha önce bahsedildiği gibi hello varolan programlama DLL başvurun.</span><span class="sxs-lookup"><span data-stu-id="9e433-262">toouse UDAGG, first define it in code-behind or reference it from hello existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="9e433-263">Ardından sözdizimi aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="9e433-263">Then use hello following syntax:</span></span>

```
AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="9e433-264">UDAGG bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9e433-264">Here is an example of UDAGG:</span></span>

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

<span data-ttu-id="9e433-265">Ve temel U-SQL betiği:</span><span class="sxs-lookup"><span data-stu-id="9e433-265">And base U-SQL script:</span></span>

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

<span data-ttu-id="9e433-266">Bu kullanım örneği senaryosu sınıfı GUID'leri hello belirli kullanıcılar için birleştirme.</span><span class="sxs-lookup"><span data-stu-id="9e433-266">In this use-case scenario, we concatenate class GUIDs for hello specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="9e433-267">Kullanıcı tanımlı nesneler kullanın: UDO</span><span class="sxs-lookup"><span data-stu-id="9e433-267">Use user-defined objects: UDO</span></span>
<span data-ttu-id="9e433-268">U-SQL kullanıcı tanımlı nesneler veya UDO adlı toodefine özel programlama nesnelerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="9e433-268">U-SQL enables you toodefine custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="9e433-269">Merhaba, U-SQL UDO listesi aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="9e433-269">hello following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="9e433-270">Kullanıcı tanımlı ayıklayıcıları</span><span class="sxs-lookup"><span data-stu-id="9e433-270">User-defined extractors</span></span>
    * <span data-ttu-id="9e433-271">Extract satır satır</span><span class="sxs-lookup"><span data-stu-id="9e433-271">Extract row by row</span></span>
    * <span data-ttu-id="9e433-272">Özel yapılandırılmış dosyalarından tooimplement veri ayıklama kullanılan</span><span class="sxs-lookup"><span data-stu-id="9e433-272">Used tooimplement data extraction from custom structured files</span></span>

* <span data-ttu-id="9e433-273">Kullanıcı tanımlı outputters</span><span class="sxs-lookup"><span data-stu-id="9e433-273">User-defined outputters</span></span>
    * <span data-ttu-id="9e433-274">Çıkış satır satır</span><span class="sxs-lookup"><span data-stu-id="9e433-274">Output row by row</span></span>
    * <span data-ttu-id="9e433-275">Kullanılan toooutput özel veri türleri veya özel dosya biçimleri</span><span class="sxs-lookup"><span data-stu-id="9e433-275">Used toooutput custom data types or custom file formats</span></span>

* <span data-ttu-id="9e433-276">Kullanıcı tanımlı işlemcileri</span><span class="sxs-lookup"><span data-stu-id="9e433-276">User-defined processors</span></span>
    * <span data-ttu-id="9e433-277">Bir satır almak ve bir satır üretir</span><span class="sxs-lookup"><span data-stu-id="9e433-277">Take one row and produce one row</span></span>
    * <span data-ttu-id="9e433-278">Kullanılan tooreduce sütun sayısı hello veya varolan bir sütun kümesinden türetilmiş değerlerle yeni sütun oluşturmak</span><span class="sxs-lookup"><span data-stu-id="9e433-278">Used tooreduce hello number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="9e433-279">Kullanıcı tanımlı appliers</span><span class="sxs-lookup"><span data-stu-id="9e433-279">User-defined appliers</span></span>
    * <span data-ttu-id="9e433-280">Bir satır alın ve 0 toon satır üretir</span><span class="sxs-lookup"><span data-stu-id="9e433-280">Take one row and produce 0 toon rows</span></span>
    * <span data-ttu-id="9e433-281">Dış/ARASI UYGULA ile kullanılan</span><span class="sxs-lookup"><span data-stu-id="9e433-281">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="9e433-282">Kullanıcı tanımlı combiners</span><span class="sxs-lookup"><span data-stu-id="9e433-282">User-defined combiners</span></span>
    * <span data-ttu-id="9e433-283">Satır kümeleri--kullanıcı tanımlı birleştirmeler birleştirir</span><span class="sxs-lookup"><span data-stu-id="9e433-283">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="9e433-284">Kullanıcı tanımlı reducers</span><span class="sxs-lookup"><span data-stu-id="9e433-284">User-defined reducers</span></span>
    * <span data-ttu-id="9e433-285">N satırları almak ve bir satır üretir</span><span class="sxs-lookup"><span data-stu-id="9e433-285">Take n rows and produce one row</span></span>
    * <span data-ttu-id="9e433-286">Kullanılan tooreduce hello satır sayısı</span><span class="sxs-lookup"><span data-stu-id="9e433-286">Used tooreduce hello number of rows</span></span>

<span data-ttu-id="9e433-287">UDO genellikle U-SQL komut U-SQL deyimlerini aşağıdaki hello bir parçası olarak açıkça çağrılır:</span><span class="sxs-lookup"><span data-stu-id="9e433-287">UDO is typically called explicitly in U-SQL script as part of hello following U-SQL statements:</span></span>

* <span data-ttu-id="9e433-288">EXTRACT</span><span class="sxs-lookup"><span data-stu-id="9e433-288">EXTRACT</span></span>
* <span data-ttu-id="9e433-289">ÇIKTI</span><span class="sxs-lookup"><span data-stu-id="9e433-289">OUTPUT</span></span>
* <span data-ttu-id="9e433-290">İŞLEM</span><span class="sxs-lookup"><span data-stu-id="9e433-290">PROCESS</span></span>
* <span data-ttu-id="9e433-291">BİRLEŞTİRME</span><span class="sxs-lookup"><span data-stu-id="9e433-291">COMBINE</span></span>
* <span data-ttu-id="9e433-292">AZALTMA</span><span class="sxs-lookup"><span data-stu-id="9e433-292">REDUCE</span></span>

> [!NOTE]  
> <span data-ttu-id="9e433-293">UDO'ın sınırlı tooconsume 0,5 Gb bellek var.</span><span class="sxs-lookup"><span data-stu-id="9e433-293">UDO’s are limited tooconsume 0.5Gb memory.</span></span>  <span data-ttu-id="9e433-294">Bu bellek sınırlama toolocal yürütmeleri geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="9e433-294">This memory limitation does not apply toolocal executions.</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="9e433-295">Kullanıcı tanımlı ayıklayıcıları kullanın</span><span class="sxs-lookup"><span data-stu-id="9e433-295">Use user-defined extractors</span></span>
<span data-ttu-id="9e433-296">U-SQL EXTRACT deyimi kullanarak tooimport dış veri sağlar.</span><span class="sxs-lookup"><span data-stu-id="9e433-296">U-SQL allows you tooimport external data by using an EXTRACT statement.</span></span> <span data-ttu-id="9e433-297">Bir ayıklama deyimi yerleşik UDO ayıklayıcıları kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9e433-297">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="9e433-298">*Extractors.Text()*: farklı kodlamaları sınırlandırılmış metin dosyalarından ayıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="9e433-298">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="9e433-299">*Extractors.Csv()*: ayıklama virgülle ayrılmış değer (CSV) dosyaları farklı kodlamaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="9e433-299">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="9e433-300">*Extractors.Tsv()*: ayıklama sekmeyle ayrılmış değerinden farklı kodlamaları (TSV) dosyaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="9e433-300">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="9e433-301">Yararlı toodevelop özel ayıklayıcısı olabilir.</span><span class="sxs-lookup"><span data-stu-id="9e433-301">It can be useful toodevelop a custom extractor.</span></span> <span data-ttu-id="9e433-302">Biz toodo görevleri aşağıdaki hello hiçbirini istiyorsanız, bu veri içe aktarma sırasında yararlı olabilir:</span><span class="sxs-lookup"><span data-stu-id="9e433-302">This can be helpful during data import if we want toodo any of hello following tasks:</span></span>

* <span data-ttu-id="9e433-303">Giriş verisi sütunları bölme ve tek tek değerleri değiştirerek değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9e433-303">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="9e433-304">Merhaba İŞLEMCİ işlevselliğini sütunları birleştirmek için daha iyi olur.</span><span class="sxs-lookup"><span data-stu-id="9e433-304">hello PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="9e433-305">Web sayfaları ve e-posta gibi yapılandırılmamış veriler veya XML/JSON gibi yarı yapılandırılmamış veriler ayrıştırılamadı.</span><span class="sxs-lookup"><span data-stu-id="9e433-305">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="9e433-306">Desteklenmeyen kodlama verileri ayrıştırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="9e433-306">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="9e433-307">bir kullanıcı tarafından tanımlanan ayıklayıcısı toodefine veya Opyalanan, ihtiyacımız toocreate bir `IExtractor` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="9e433-307">toodefine a user-defined extractor, or UDE, we need toocreate an `IExtractor` interface.</span></span> <span data-ttu-id="9e433-308">Sütun/satır sınırlayıcıları ve kodlama, hello sınıfı hello oluşturucuda tanımlanan toobe gerektiği gibi tüm parametreleri toohello ayıklayıcısı girin.</span><span class="sxs-lookup"><span data-stu-id="9e433-308">All input parameters toohello extractor, such as column/row delimiters, and encoding, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="9e433-309">Merhaba `IExtractor` arabirimi hello için bir tanım da içermelidir `IEnumerable<IRow>` gibi geçersiz kıl:</span><span class="sxs-lookup"><span data-stu-id="9e433-309">hello `IExtractor`  interface should also contain a definition for hello `IEnumerable<IRow>` override as follows:</span></span>

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

<span data-ttu-id="9e433-310">Merhaba **SqlUserDefinedExtractor** öznitelik, hello türü kullanıcı tanımlı bir ayıklayıcısı kayıtlı olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="9e433-310">hello **SqlUserDefinedExtractor** attribute indicates that hello type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="9e433-311">Bu sınıf devralınan olamaz.</span><span class="sxs-lookup"><span data-stu-id="9e433-311">This class cannot be inherited.</span></span>

<span data-ttu-id="9e433-312">SqlUserDefinedExtractor Opyalanan tanımı için isteğe bağlı bir özniteliktir.</span><span class="sxs-lookup"><span data-stu-id="9e433-312">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="9e433-313">Toodefine AtomicFileProcessing özelliği hello Opyalanan nesne için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9e433-313">It used toodefine AtomicFileProcessing property for hello UDE object.</span></span>

* <span data-ttu-id="9e433-314">bool AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="9e433-314">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="9e433-315">**doğru** bu ayıklayıcısı atomik giriş dosyaları (JSON, XML,...) gerektirdiğini belirtir =</span><span class="sxs-lookup"><span data-stu-id="9e433-315">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="9e433-316">**yanlış** bu ayıklayıcısı bölünmüş / dağıtılmış dosyalarla (CSV, SEQ,...) başa belirtir =</span><span class="sxs-lookup"><span data-stu-id="9e433-316">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="9e433-317">Merhaba ana Opyalanan programlamasına nesneler **giriş** ve **çıkış**.</span><span class="sxs-lookup"><span data-stu-id="9e433-317">hello main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="9e433-318">Merhaba giriş nesnesidir kullanılan tooenumerate girdi verisi olarak `IUnstructuredReader`.</span><span class="sxs-lookup"><span data-stu-id="9e433-318">hello input object is used tooenumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="9e433-319">kullanılan tooset çıktı verilerini hello ayıklayıcısı etkinlik sonucunda Hello çıkış nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="9e433-319">hello output object is used tooset output data as a result of hello extractor activity.</span></span>

<span data-ttu-id="9e433-320">Merhaba giriş verileri üzerinden erişildiğinde `System.IO.Stream` ve `System.IO.StreamReader`.</span><span class="sxs-lookup"><span data-stu-id="9e433-320">hello input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="9e433-321">Giriş sütunları numaralandırması için biz ilk hello Giriş akışı satır ayırıcı kullanarak ayırın.</span><span class="sxs-lookup"><span data-stu-id="9e433-321">For input columns enumeration, we first split hello input stream by using a row delimiter.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

<span data-ttu-id="9e433-322">Ardından, daha fazla giriş satır sütun bölün.</span><span class="sxs-lookup"><span data-stu-id="9e433-322">Then, further split input row into column parts.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

<span data-ttu-id="9e433-323">tooset çıktı verilerini, hello kullanırız `output.Set` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9e433-323">tooset output data, we use hello `output.Set` method.</span></span>

<span data-ttu-id="9e433-324">Merhaba çıkışıyla sütunlar ve tanımlanmış değerler yalnızca özel ayıklayıcısı hello toounderstand çıkarır önemlidir.</span><span class="sxs-lookup"><span data-stu-id="9e433-324">It's important toounderstand that hello custom extractor only outputs columns and values that are defined with hello output.</span></span> <span data-ttu-id="9e433-325">Yöntem çağrısının ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9e433-325">Set method call.</span></span>

```
output.Set<string>(count, part);
```

<span data-ttu-id="9e433-326">Merhaba gerçek ayıklayıcısı çıkış çağırarak tetiklenir `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="9e433-326">hello actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="9e433-327">Merhaba ayıklayıcısı örneği aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9e433-327">Following is hello extractor example:</span></span>

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

<span data-ttu-id="9e433-328">Bu kullanım örneği senaryosu hello ayıklayıcısı hello GUID "guid" sütunu için yeniden oluşturur ve "kullanıcı" sütun tooupper örneğinin hello değerleri dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="9e433-328">In this use-case scenario, hello extractor regenerates hello GUID for “guid” column and converts hello values of “user” column tooupper case.</span></span> <span data-ttu-id="9e433-329">Özel ayıklayıcıları giriş verilerini ayrıştırma ve onu düzenleme daha karmaşık sonuçlara yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="9e433-329">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="9e433-330">Özel ayıklayıcısı kullanan temel U-SQL komut dosyası aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="9e433-330">Following is base U-SQL script that uses a custom extractor:</span></span>

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

## <a name="use-user-defined-outputters"></a><span data-ttu-id="9e433-331">Kullanıcı tanımlı outputters kullanın</span><span class="sxs-lookup"><span data-stu-id="9e433-331">Use user-defined outputters</span></span>
<span data-ttu-id="9e433-332">Kullanıcı tanımlı outputter tooextend yerleşik U-SQL işlevselliği sağlayan başka bir U-SQL UDO ' dir.</span><span class="sxs-lookup"><span data-stu-id="9e433-332">User-defined outputter is another U-SQL UDO that allows you tooextend built-in U-SQL functionality.</span></span> <span data-ttu-id="9e433-333">Benzer toohello ayıklayıcısı, birkaç yerleşik outputters vardır.</span><span class="sxs-lookup"><span data-stu-id="9e433-333">Similar toohello extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="9e433-334">*Outputters.Text()*: metin dosyalarını farklı kodlamaları veri toodelimited yazar.</span><span class="sxs-lookup"><span data-stu-id="9e433-334">*Outputters.Text()*: Writes data toodelimited text files of different encodings.</span></span>
* <span data-ttu-id="9e433-335">*Outputters.Csv()*: veri toocomma virgülle ayrılmış değer (CSV) dosyaları farklı kodlamaları yazar.</span><span class="sxs-lookup"><span data-stu-id="9e433-335">*Outputters.Csv()*: Writes data toocomma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="9e433-336">*Outputters.Tsv()*: veri tootab virgülle ayrılmış değer (TSV) dosyaları farklı kodlamaları yazar.</span><span class="sxs-lookup"><span data-stu-id="9e433-336">*Outputters.Tsv()*: Writes data tootab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="9e433-337">Özel outputter özel tanımlanmış bir biçimde toowrite veri sağlar.</span><span class="sxs-lookup"><span data-stu-id="9e433-337">Custom outputter allows you toowrite data in a custom defined format.</span></span> <span data-ttu-id="9e433-338">Bu görevleri aşağıdaki hello için yararlı olabilir:</span><span class="sxs-lookup"><span data-stu-id="9e433-338">This can be useful for hello following tasks:</span></span>

* <span data-ttu-id="9e433-339">Veri toosemi yapılandırılmış veya yapılandırılmamış dosyaları yazma.</span><span class="sxs-lookup"><span data-stu-id="9e433-339">Writing data toosemi-structured or unstructured files.</span></span>
* <span data-ttu-id="9e433-340">Veri yazma değil Kodlamalar desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9e433-340">Writing data not supported encodings.</span></span>
* <span data-ttu-id="9e433-341">Çıktı verilerini değiştirme veya özel öznitelikleri ekleme.</span><span class="sxs-lookup"><span data-stu-id="9e433-341">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="9e433-342">Kullanıcı tanımlı toodefine outputter ihtiyacımız toocreate hello `IOutputter` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="9e433-342">toodefine user-defined outputter, we need toocreate hello `IOutputter` interface.</span></span>

<span data-ttu-id="9e433-343">Aşağıdadır hello temel `IOutputter` sınıfı uygulama:</span><span class="sxs-lookup"><span data-stu-id="9e433-343">Following is hello base `IOutputter` class implementation:</span></span>

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

<span data-ttu-id="9e433-344">Sütun/satır sınırlayıcıları, kodlama ve benzeri, hello sınıfı hello oluşturucuda tanımlanan toobe gerektiği gibi tüm parametreleri toohello outputter girin.</span><span class="sxs-lookup"><span data-stu-id="9e433-344">All input parameters toohello outputter, such as column/row delimiters, encoding, and so on, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="9e433-345">Merhaba `IOutputter` arabirimi için bir tanım da içermelidir `void Output` geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="9e433-345">hello `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="9e433-346">Merhaba özniteliği `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` atomik dosya işleme için isteğe bağlı olarak ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="9e433-346">hello attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="9e433-347">Daha fazla bilgi için hello aşağıdaki ayrıntılara bakın.</span><span class="sxs-lookup"><span data-stu-id="9e433-347">For more information, see hello following details.</span></span>

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

* <span data-ttu-id="9e433-348">`Output`Giriş her satır için çağrılır.</span><span class="sxs-lookup"><span data-stu-id="9e433-348">`Output` is called for each input row.</span></span> <span data-ttu-id="9e433-349">Merhaba döndürür `IUnstructuredWriter output` satır kümesi.</span><span class="sxs-lookup"><span data-stu-id="9e433-349">It returns hello `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="9e433-350">Merhaba Oluşturucusu sınıfı kullanılır toopass parametreleri toohello kullanıcı tanımlı outputter.</span><span class="sxs-lookup"><span data-stu-id="9e433-350">hello Constructor class is used toopass parameters toohello user-defined outputter.</span></span>
* <span data-ttu-id="9e433-351">`Close`kullanılan toooptionally toorelease pahalı durumu geçersiz kılabilir veya ne zaman hello son satırını yazıldı belirleyin.</span><span class="sxs-lookup"><span data-stu-id="9e433-351">`Close` is used toooptionally override toorelease expensive state or determine when hello last row was written.</span></span>

<span data-ttu-id="9e433-352">**SqlUserDefinedOutputter** öznitelik, hello türü kullanıcı tanımlı bir outputter kayıtlı olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="9e433-352">**SqlUserDefinedOutputter** attribute indicates that hello type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="9e433-353">Bu sınıf devralınan olamaz.</span><span class="sxs-lookup"><span data-stu-id="9e433-353">This class cannot be inherited.</span></span>

<span data-ttu-id="9e433-354">SqlUserDefinedOutputter, kullanıcı tanımlı outputter tanımı için isteğe bağlı bir özniteliktir.</span><span class="sxs-lookup"><span data-stu-id="9e433-354">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="9e433-355">Toodefine hello AtomicFileProcessing özelliği kullandı.</span><span class="sxs-lookup"><span data-stu-id="9e433-355">It's used toodefine hello AtomicFileProcessing property.</span></span>

* <span data-ttu-id="9e433-356">bool AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="9e433-356">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="9e433-357">**doğru** bu outputter atomik çıktı dosyaları (JSON, XML,...) gerektirdiğini belirtir =</span><span class="sxs-lookup"><span data-stu-id="9e433-357">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="9e433-358">**yanlış** bu outputter bölünmüş / dağıtılmış dosyalarla (CSV, SEQ,...) başa belirtir =</span><span class="sxs-lookup"><span data-stu-id="9e433-358">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="9e433-359">Merhaba ana programlamasına nesneler **satır** ve **çıkış**.</span><span class="sxs-lookup"><span data-stu-id="9e433-359">hello main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="9e433-360">Merhaba **satır** nesnesidir kullanılan tooenumerate çıktı verisi olarak `IRow` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="9e433-360">hello **row** object is used tooenumerate output data as `IRow` interface.</span></span> <span data-ttu-id="9e433-361">**Çıktı** kullanılan tooset çıkış veri toohello hedef dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="9e433-361">**Output** is used tooset output data toohello target file.</span></span>

<span data-ttu-id="9e433-362">Merhaba çıktı verilerini hello erişilen `IRow` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="9e433-362">hello output data is accessed through hello `IRow` interface.</span></span> <span data-ttu-id="9e433-363">Çıktı verilerini bir satır aynı anda geçirilir.</span><span class="sxs-lookup"><span data-stu-id="9e433-363">Output data is passed a row at a time.</span></span>

<span data-ttu-id="9e433-364">Merhaba tek tek değerleri hello IRow arabiriminin hello Get yöntemini çağırarak numaralandırılmıştır:</span><span class="sxs-lookup"><span data-stu-id="9e433-364">hello individual values are enumerated by calling hello Get method of hello IRow interface:</span></span>

```
row.Get<string>("column_name")
```

<span data-ttu-id="9e433-365">Tek tek sütun adları çağırarak belirlenebilir `row.Schema`:</span><span class="sxs-lookup"><span data-stu-id="9e433-365">Individual column names can be determined by calling `row.Schema`:</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="9e433-366">Bu yaklaşım toobuild herhangi bir meta veri şema için esnek bir outputter sağlar.</span><span class="sxs-lookup"><span data-stu-id="9e433-366">This approach enables you toobuild a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="9e433-367">Merhaba çıktı verilerini toofile kullanılarak yazılan `System.IO.StreamWriter`.</span><span class="sxs-lookup"><span data-stu-id="9e433-367">hello output data is written toofile by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="9e433-368">Merhaba akışı parametre olarak ayarlanmış çok`output.BaseStrea` parçası olarak `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="9e433-368">hello stream parameter is set too`output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="9e433-369">Her satır yinelemeden sonra önemli tooflush hello veri arabelleği toohello dosyası olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9e433-369">Note that it's important tooflush hello data buffer toohello file after each row iteration.</span></span> <span data-ttu-id="9e433-370">Ayrıca, hello `StreamWriter` nesne özniteliğiyle etkin hello atılabilir (varsayılan) ile Merhaba kullanılmalıdır **kullanarak** anahtar sözcüğü:</span><span class="sxs-lookup"><span data-stu-id="9e433-370">In addition, hello `StreamWriter` object must be used with hello Disposable attribute enabled (default) and with hello **using** keyword:</span></span>

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

<span data-ttu-id="9e433-371">Aksi takdirde Flush() yöntemini her yinelemeden sonra açıkça çağırın.</span><span class="sxs-lookup"><span data-stu-id="9e433-371">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="9e433-372">Bu örnekte aşağıdaki hello gösteriyoruz.</span><span class="sxs-lookup"><span data-stu-id="9e433-372">We show this in hello following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="9e433-373">Üstbilgiler ve altbilgiler kullanıcı tanımlı outputter için ayarlama</span><span class="sxs-lookup"><span data-stu-id="9e433-373">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="9e433-374">tooset bir üstbilgi tek yineleme yürütme akışı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9e433-374">tooset a header, use single iteration execution flow.</span></span>

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

<span data-ttu-id="9e433-375">Merhaba kodda ilk hello `if (isHeaderRow)` blok yalnızca bir kez gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9e433-375">hello code in hello first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="9e433-376">Merhaba altbilgiyi hello başvuru toohello örneğini kullanması `System.IO.Stream` nesne (`output.BaseStream`).</span><span class="sxs-lookup"><span data-stu-id="9e433-376">For hello footer, use hello reference toohello instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="9e433-377">Merhaba altbilgi hello hello çağrısının yöntemi yazma `IOutputter` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="9e433-377">Write hello footer in hello Close() method of hello `IOutputter` interface.</span></span>  <span data-ttu-id="9e433-378">(Daha fazla bilgi için aşağıdaki örneğine hello bakın.)</span><span class="sxs-lookup"><span data-stu-id="9e433-378">(For more information, see hello following example.)</span></span>

<span data-ttu-id="9e433-379">Kullanıcı tanımlı bir outputter örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="9e433-379">Following is an example of a user-defined outputter:</span></span>

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

<span data-ttu-id="9e433-380">Ve U-SQL temel betiği:</span><span class="sxs-lookup"><span data-stu-id="9e433-380">And U-SQL base script:</span></span>

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

<span data-ttu-id="9e433-381">Tablo verisi bir HTML dosyası oluşturur bir HTML outputter budur.</span><span class="sxs-lookup"><span data-stu-id="9e433-381">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="9e433-382">U-SQL temel betikten outputter çağırın</span><span class="sxs-lookup"><span data-stu-id="9e433-382">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="9e433-383">toocall özel outputter hello temel U-SQL komut dosyasından, oluşturulan toobe hello yeni hello outputter nesnesinin örneği vardır.</span><span class="sxs-lookup"><span data-stu-id="9e433-383">toocall a custom outputter from hello base U-SQL script, hello new instance of hello outputter object has toobe created.</span></span>

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="9e433-384">Merhaba örneği oluşturmayı tooavoid nesne temel komut dosyasında bizim önceki örnekte gösterildiği gibi bir işlevi sarmalayıcı oluşturabilir:</span><span class="sxs-lookup"><span data-stu-id="9e433-384">tooavoid creating an instance of hello object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

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

<span data-ttu-id="9e433-385">Bu durumda, hello özgün çağrısı hello aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="9e433-385">In this case, hello original call looks like hello following:</span></span>

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="9e433-386">Kullanıcı tanımlı işlemcilerini kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="9e433-386">Use user-defined processors</span></span>
<span data-ttu-id="9e433-387">Kullanıcı tanımlı işlemci veya UDP, U-SQL programlama özelliklerine uygulayarak tooprocess hello gelen satırları sağlayan UDO türüdür.</span><span class="sxs-lookup"><span data-stu-id="9e433-387">User-defined processor, or UDP, is a type of U-SQL UDO that enables you tooprocess hello incoming rows by applying programmability features.</span></span> <span data-ttu-id="9e433-388">UDP toocombine sütunları sağlar, değerleri değiştirmek ve gerekirse, yeni sütun ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9e433-388">UDP enables you toocombine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="9e433-389">Temel olarak bir satır kümesi tooproduce gerekli veri öğeleri tooprocess yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9e433-389">Basically, it helps tooprocess a rowset tooproduce required data elements.</span></span>

<span data-ttu-id="9e433-390">toodefine bir UDP, ihtiyacımız toocreate bir `IProcessor` hello arabirimiyle `SqlUserDefinedProcessor` için UDP isteğe bağlı öznitelik.</span><span class="sxs-lookup"><span data-stu-id="9e433-390">toodefine a UDP, we need toocreate an `IProcessor` interface with hello `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="9e433-391">Bu arabirim hello hello tanımı içermelidir `IRow` arabirimi satır kümesi geçersiz kılmak, hello aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="9e433-391">This interface should contain hello definition for hello `IRow` interface rowset override, as shown in hello following example:</span></span>

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

<span data-ttu-id="9e433-392">**SqlUserDefinedProcessor** hello türü kullanıcı tanımlı bir işlemci olarak kayıtlı olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="9e433-392">**SqlUserDefinedProcessor** indicates that hello type should be registered as a user-defined processor.</span></span> <span data-ttu-id="9e433-393">Bu sınıf devralınan olamaz.</span><span class="sxs-lookup"><span data-stu-id="9e433-393">This class cannot be inherited.</span></span>

<span data-ttu-id="9e433-394">Merhaba SqlUserDefinedProcessor özniteliği **isteğe bağlı** UDP tanımı.</span><span class="sxs-lookup"><span data-stu-id="9e433-394">hello SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="9e433-395">Merhaba ana programlamasına nesneler **giriş** ve **çıkış**.</span><span class="sxs-lookup"><span data-stu-id="9e433-395">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="9e433-396">Merhaba giriş kullanılan tooenumerate giriş sütunları ve çıktı ve tooset çıktı verilerini hello işlemci etkinliğinin sonucunda nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="9e433-396">hello input object is used tooenumerate input columns and output, and tooset output data as a result of hello processor activity.</span></span>

<span data-ttu-id="9e433-397">Giriş sütunları numaralandırması için kullandığımız hello `input.Get` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9e433-397">For input columns enumeration, we use hello `input.Get` method.</span></span>

```
string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="9e433-398">parametresi için hello `input.Get` yöntemdir hello bir parçası olarak geçirilen bir sütun `PRODUCE` hello yan tümcesi `PROCESS` temel hello U-SQL komut dosyası ifadesi.</span><span class="sxs-lookup"><span data-stu-id="9e433-398">hello parameter for `input.Get` method is a column that's passed as part of hello `PRODUCE` clause of hello `PROCESS` statement of hello U-SQL base script.</span></span> <span data-ttu-id="9e433-399">Toouse ihtiyacımız hello doğru veri buraya yazın.</span><span class="sxs-lookup"><span data-stu-id="9e433-399">We need toouse hello correct data type here.</span></span>

<span data-ttu-id="9e433-400">Çıkış için hello kullan `output.Set` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9e433-400">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="9e433-401">Önemli toonote o özel üretici yalnızca çıkarır sütunlar ve hello ile tanımlı değerler `output.Set` yöntem çağrısı.</span><span class="sxs-lookup"><span data-stu-id="9e433-401">It's important toonote that custom producer only outputs columns and values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="9e433-402">Merhaba gerçek işlemci çıktı çağırarak tetiklenir `return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="9e433-402">hello actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="9e433-403">Bir işlemci örneği aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9e433-403">Following is a processor example:</span></span>

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

<span data-ttu-id="9e433-404">Bu kullanım örneği senaryosu hello işlemci büyük harf ve "des" "kullanıcı" Merhaba varolan sütunlar--bu durumda, birleştirerek "full_description" adlı yeni bir sütun oluşturuyor.</span><span class="sxs-lookup"><span data-stu-id="9e433-404">In this use-case scenario, hello processor is generating a new column called “full_description” by combining hello existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="9e433-405">Ayrıca, bir GUID oluşturur ve hello özgün ve yeni GUID değerleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="9e433-405">It also regenerates a GUID and returns hello original and new GUID values.</span></span>

<span data-ttu-id="9e433-406">Merhaba önceki örnekte görebildiğiniz gibi C# sırasında yöntemi çağırabilirsiniz `output.Set` yöntem çağrısı.</span><span class="sxs-lookup"><span data-stu-id="9e433-406">As you can see from hello previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="9e433-407">Özel bir işlemci kullanan temel U-SQL komut dosyası örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9e433-407">Following is an example of base U-SQL script that uses a custom processor:</span></span>

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

## <a name="use-user-defined-appliers"></a><span data-ttu-id="9e433-408">Kullanıcı tanımlı appliers kullanın</span><span class="sxs-lookup"><span data-stu-id="9e433-408">Use user-defined appliers</span></span>
<span data-ttu-id="9e433-409">Kullanıcı tanımlı bir U-SQL applier hello dış tablo ifadesi bir sorgu tarafından döndürülen her satır için tooinvoke özel C# işlevi sağlar.</span><span class="sxs-lookup"><span data-stu-id="9e433-409">A U-SQL user-defined applier enables you tooinvoke a custom C# function for each row that's returned by hello outer table expression of a query.</span></span> <span data-ttu-id="9e433-410">Merhaba sağ giriş hello sol giriş gelen her satır için hesaplanan ve üretilen hello satırları hello son çıktı için birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9e433-410">hello right input is evaluated for each row from hello left input, and hello rows that are produced are combined for hello final output.</span></span> <span data-ttu-id="9e433-411">Merhaba hello UYGULA operatör tarafından üretilen sütunları listesidir hello sol ve sağ giriş hello sütunlar hello kümesiyle hello birleşimi.</span><span class="sxs-lookup"><span data-stu-id="9e433-411">hello list of columns that are produced by hello APPLY operator are hello combination of hello set of columns in hello left and hello right input.</span></span>

<span data-ttu-id="9e433-412">Kullanıcı tanımlı applier hello USQL seçin ifadesi bir parçası olarak çağrılır.</span><span class="sxs-lookup"><span data-stu-id="9e433-412">User-defined applier is being invoked as part of hello USQL SELECT expression.</span></span>

<span data-ttu-id="9e433-413">Merhaba tipik kullanıcı tanımlı applier görünüyor hello aşağıdaki gibi toohello arayın:</span><span class="sxs-lookup"><span data-stu-id="9e433-413">hello typical call toohello user-defined applier looks like hello following:</span></span>

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="9e433-414">Bir SELECT ifadesinde appliers kullanma hakkında daha fazla bilgi için bkz: [seçin, U-SQL seçme ARASI uygulamak ve OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e433-414">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="9e433-415">Merhaba kullanıcı tanımlı applier temel sınıf tanımı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9e433-415">hello user-defined applier base class definition is as follows:</span></span>

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

<span data-ttu-id="9e433-416">Kullanıcı tanımlı bir applier toodefine ihtiyacımız toocreate hello `IApplier` hello arabirimiyle [`SqlUserDefinedApplier`] özniteliği için kullanıcı tanımlı applier tanım isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="9e433-416">toodefine a user-defined applier, we need toocreate hello `IApplier` interface with hello [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

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

* <span data-ttu-id="9e433-417">Uygulama hello dış tablodaki her satır için çağrılır.</span><span class="sxs-lookup"><span data-stu-id="9e433-417">Apply is called for each row of hello outer table.</span></span> <span data-ttu-id="9e433-418">Merhaba döndürür `IUpdatableRow` satır kümesi çıktı.</span><span class="sxs-lookup"><span data-stu-id="9e433-418">It returns hello `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="9e433-419">Merhaba Oluşturucusu kullanılan toopass parametreleri toohello applier kullanıcı tanımlı bir sınıftır.</span><span class="sxs-lookup"><span data-stu-id="9e433-419">hello Constructor class is used toopass parameters toohello user-defined applier.</span></span>

<span data-ttu-id="9e433-420">**SqlUserDefinedApplier** hello türü kullanıcı tanımlı bir applier kayıtlı olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="9e433-420">**SqlUserDefinedApplier** indicates that hello type should be registered as a user-defined applier.</span></span> <span data-ttu-id="9e433-421">Bu sınıf devralınan olamaz.</span><span class="sxs-lookup"><span data-stu-id="9e433-421">This class cannot be inherited.</span></span>

<span data-ttu-id="9e433-422">**SqlUserDefinedApplier** olan **isteğe bağlı** kullanıcı tanımlı applier tanımı.</span><span class="sxs-lookup"><span data-stu-id="9e433-422">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="9e433-423">Merhaba ana programlamasına nesneleri aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9e433-423">hello main programmability objects are as follows:</span></span>

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="9e433-424">Giriş satır kümeleri olarak geçirilir `IRow` giriş.</span><span class="sxs-lookup"><span data-stu-id="9e433-424">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="9e433-425">Merhaba çıkış satır olarak oluşturulan `IUpdatableRow` çıkış arabirimi.</span><span class="sxs-lookup"><span data-stu-id="9e433-425">hello output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="9e433-426">Tek tek sütun adlarına göre arama hello belirlenebilir `IRow` şema yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9e433-426">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="9e433-427">Merhaba gelen tooget hello gerçek veri değerleri `IRow`, hello Get() yöntemi kullanırız `IRow` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="9e433-427">tooget hello actual data values from hello incoming `IRow`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="9e433-428">Veya hello şema sütun adı kullanırız:</span><span class="sxs-lookup"><span data-stu-id="9e433-428">Or we use hello schema column name:</span></span>

```
row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="9e433-429">Merhaba çıkış değerleri ile ayarlanmalıdır `IUpdatableRow` çıktı:</span><span class="sxs-lookup"><span data-stu-id="9e433-429">hello output values must be set with `IUpdatableRow` output:</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="9e433-430">Özel appliers sütunlar ve ile tanımlanmış değerler yalnızca çıktı önemli toounderstand olan `output.Set` yöntem çağrısı.</span><span class="sxs-lookup"><span data-stu-id="9e433-430">It is important toounderstand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="9e433-431">Merhaba gerçek çıkış çağırarak tetiklenir `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="9e433-431">hello actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="9e433-432">Merhaba kullanıcı tanımlı applier parametreleri toohello Oluşturucusu geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="9e433-432">hello user-defined applier parameters can be passed toohello constructor.</span></span> <span data-ttu-id="9e433-433">Applier hello applier temel U-SQL betiği çağrısında sırasında tanımlanan toobe gereken sütunlar değişken sayıda geri dönebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e433-433">Applier can return a variable number of columns that need toobe defined during hello applier call in base U-SQL Script.</span></span>

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="9e433-434">Merhaba kullanıcı tanımlı applier örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="9e433-434">Here is hello user-defined applier example:</span></span>

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

<span data-ttu-id="9e433-435">Bu kullanıcı tarafından tanımlanan applier hello temel U-SQL betiği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="9e433-435">Following is hello base U-SQL script for this user-defined applier:</span></span>

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

<span data-ttu-id="9e433-436">Bu kullanım örnek senaryoda, kullanıcı tanımlı applier görevi görür hello araba için virgülle ayrılmış değer ayrıştırıcı özellikleri yakıt.</span><span class="sxs-lookup"><span data-stu-id="9e433-436">In this use case scenario, user-defined applier acts as a comma-delimited value parser for hello car fleet properties.</span></span> <span data-ttu-id="9e433-437">Merhaba giriş dosyası satırları hello şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="9e433-437">hello input file rows look like hello following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="9e433-438">Normal bir sekmeyle ayrılmış TSV dosya marka ve model gibi araba özellikleri içeren özellikleri sütunu var.</span><span class="sxs-lookup"><span data-stu-id="9e433-438">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="9e433-439">Bu özellikler ayrıştırılmış toohello tablo sütunları olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e433-439">Those properties must be parsed toohello table columns.</span></span> <span data-ttu-id="9e433-440">sağlanan hello applier ayrıca hello özelliklerinde dinamik bir dizi satır kümesi, geçirilen hello parametresi temelinde neden toogenerate sağlar.</span><span class="sxs-lookup"><span data-stu-id="9e433-440">hello applier that's provided also enables you toogenerate a dynamic number of properties in hello result rowset, based on hello parameter that's passed.</span></span> <span data-ttu-id="9e433-441">Tüm özellikleri veya özellikler yalnızca belirli bir grup oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e433-441">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="9e433-442">Merhaba kullanıcı tanımlı applier applier nesnesinin yeni bir örneğini çağrılabilir:</span><span class="sxs-lookup"><span data-stu-id="9e433-442">hello user-defined applier can be called as a new instance of applier object:</span></span>

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="9e433-443">Veya bir sarmalayıcı fabrika yöntemi hello çağrıldı:</span><span class="sxs-lookup"><span data-stu-id="9e433-443">Or with hello invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="9e433-444">Kullanıcı tanımlı combiners kullanın</span><span class="sxs-lookup"><span data-stu-id="9e433-444">Use user-defined combiners</span></span>
<span data-ttu-id="9e433-445">Kullanıcı tanımlı Birleştirici veya UDC, sol ve sağ satır kümeleri özel mantığına göre toocombine satırları etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="9e433-445">User-defined combiner, or UDC, enables you toocombine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="9e433-446">Kullanıcı tanımlı birleştirici birleştirme ifadesiyle kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9e433-446">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="9e433-447">Her iki hello giriş satır kümeleri hakkında gerekli bilgileri hello sağlar hello birleştirme ifade ile bir Birleştirici çağrılmakta, sütunlar hello gruplandırma hello beklenen sonucu şema ve ek bilgi.</span><span class="sxs-lookup"><span data-stu-id="9e433-447">A combiner is being invoked with hello COMBINE expression that provides hello necessary information about both hello input rowsets, hello grouping columns, hello expected result schema, and additional information.</span></span>

<span data-ttu-id="9e433-448">temel bir U-SQL komut dosyasında bir Birleştirici toocall, söz dizimi aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="9e433-448">toocall a combiner in a base U-SQL script, we use hello following syntax:</span></span>

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

<span data-ttu-id="9e433-449">Daha fazla bilgi için bkz: [BİRLEŞTİRMEK ifade (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e433-449">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="9e433-450">Kullanıcı tanımlı bir Birleştirici toodefine ihtiyacımız toocreate hello `ICombiner` hello arabirimiyle [`SqlUserDefinedCombiner`] özniteliği için bir kullanıcı tarafından tanımlanan birleştirici tanım isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="9e433-450">toodefine a user-defined combiner, we need toocreate hello `ICombiner` interface with hello [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="9e433-451">Temel `ICombiner` sınıf tanımı:</span><span class="sxs-lookup"><span data-stu-id="9e433-451">Base `ICombiner` class definition:</span></span>

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

<span data-ttu-id="9e433-452">Özel uyarlamasını hello bir `ICombiner` arabirimi hello tanımı içermelidir bir `IEnumerable<IRow>` geçersiz kılma birleştirin.</span><span class="sxs-lookup"><span data-stu-id="9e433-452">hello custom implementation of an `ICombiner` interface should contain hello definition for an `IEnumerable<IRow>` Combine override.</span></span>

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

<span data-ttu-id="9e433-453">Merhaba **SqlUserDefinedCombiner** öznitelik, hello türü kullanıcı tanımlı bir Birleştirici kayıtlı olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="9e433-453">hello **SqlUserDefinedCombiner** attribute indicates that hello type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="9e433-454">Bu sınıf devralınan olamaz.</span><span class="sxs-lookup"><span data-stu-id="9e433-454">This class cannot be inherited.</span></span>

<span data-ttu-id="9e433-455">**SqlUserDefinedCombiner** kullanılan toodefine hello Birleştirici modu özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="9e433-455">**SqlUserDefinedCombiner** is used toodefine hello Combiner mode property.</span></span> <span data-ttu-id="9e433-456">Bir kullanıcı tarafından tanımlanan birleştirici tanımı için isteğe bağlı bir özniteliktir.</span><span class="sxs-lookup"><span data-stu-id="9e433-456">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="9e433-457">CombinerMode modu</span><span class="sxs-lookup"><span data-stu-id="9e433-457">CombinerMode     Mode</span></span>

<span data-ttu-id="9e433-458">CombinerMode enum değerleri aşağıdaki hello alabilir:</span><span class="sxs-lookup"><span data-stu-id="9e433-458">CombinerMode enum can take hello following values:</span></span>

* <span data-ttu-id="9e433-459">Her çıktı satır olası tüm hello giriş satırları bağlıdır tam (0) sol ve sağ hello ile aynı anahtar değeri.</span><span class="sxs-lookup"><span data-stu-id="9e433-459">Full  (0) Every output row potentially depends on all hello input rows from left and right       with hello same key value.</span></span>

* <span data-ttu-id="9e433-460">Sol (1) tek bir giriş satır hello soldan her çıktı satır bağlıdır (ve büyük olasılıkla tüm satırları hello hello sağ ile aynı anahtar değeri).</span><span class="sxs-lookup"><span data-stu-id="9e433-460">Left  (1) Every output row depends on a single input row from hello left (and potentially all rows       from hello right with hello same key value).</span></span>

* <span data-ttu-id="9e433-461">Sağa doğru hello tek giriş satırdan her çıktı satır bağlıdır (2) (ve büyük olasılıkla tüm satırları hello ile Merhaba soldan aynı anahtar değeri).</span><span class="sxs-lookup"><span data-stu-id="9e433-461">Right (2)     Every output row depends on a single input row from hello right (and potentially all rows       from hello left with hello same key value).</span></span>

* <span data-ttu-id="9e433-462">Her çıktı satır bağlıdır tek bir giriş, iç (3) satır sol ve sağ hello ile aynı değer.</span><span class="sxs-lookup"><span data-stu-id="9e433-462">Inner (3) Every output row depends on a single input row from left and right with hello same value.</span></span>

<span data-ttu-id="9e433-463">Örnek: [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="9e433-463">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="9e433-464">Merhaba ana programlamasına nesneler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9e433-464">hello main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="9e433-465">Giriş satır kümeleri olarak geçirilir **sol** ve **sağ** `IRowset` arabirimi türü.</span><span class="sxs-lookup"><span data-stu-id="9e433-465">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="9e433-466">Her iki satır kümeleri işleme için numaralandırılmış gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e433-466">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="9e433-467">Böylece tooenumerate sahip ve gerekirse, önbelleğe yalnızca her bir arabirime bir kez sıralayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e433-467">You can only enumerate each interface once, so we have tooenumerate and cache it if necessary.</span></span>

<span data-ttu-id="9e433-468">Amacıyla önbelleğe alma işlemi için bir liste oluşturabilir\<T\> tür bellek yapısı sonuç olarak bir LINQ Sorgu yürütme, özellikle listesi <`IRow`>.</span><span class="sxs-lookup"><span data-stu-id="9e433-468">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="9e433-469">Merhaba anonim veri türü de numaralandırma sırasında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9e433-469">hello anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="9e433-470">Bkz: [giriş tooLINQ sorgular (C#)](https://msdn.microsoft.com/library/bb397906.aspx) LINQ sorguları hakkında daha fazla bilgi ve [IEnumerable\<T\> arabirimi](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) IEnumerablehakkındadahafazlabilgiiçin\<T\> arabirimi.</span><span class="sxs-lookup"><span data-stu-id="9e433-470">See [Introduction tooLINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="9e433-471">Merhaba gelen tooget hello gerçek veri değerleri `IRowset`, hello Get() yöntemi kullanırız `IRow` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="9e433-471">tooget hello actual data values from hello incoming `IRowset`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="9e433-472">Tek tek sütun adlarına göre arama hello belirlenebilir `IRow` şema yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9e433-472">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="9e433-473">Veya hello şema sütun adı kullanarak:</span><span class="sxs-lookup"><span data-stu-id="9e433-473">Or by using hello schema column name:</span></span>

```
c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="9e433-474">LINQ ile Merhaba genel numaralandırma hello aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="9e433-474">hello general enumeration with LINQ looks like hello following:</span></span>

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="9e433-475">Her iki satır kümeleri numaralandırma sonra tüm satırların üzerinden tooloop çağıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="9e433-475">After enumerating both rowsets, we are going tooloop through all rows.</span></span> <span data-ttu-id="9e433-476">Merhaba sol satır kümesindeki her satır için biz toofind bizim Birleştirici hello koşulu karşılayan tüm satırları adımıdır.</span><span class="sxs-lookup"><span data-stu-id="9e433-476">For each row in hello left rowset, we are going toofind all rows that satisfy hello condition of our combiner.</span></span>

<span data-ttu-id="9e433-477">Merhaba çıkış değerleri ile ayarlanmalıdır `IUpdatableRow` çıktı.</span><span class="sxs-lookup"><span data-stu-id="9e433-477">hello output values must be set with `IUpdatableRow` output.</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="9e433-478">Merhaba gerçek çıkış çok çağırarak tetiklenir`yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="9e433-478">hello actual output is triggered by calling too`yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="9e433-479">Birleştirici örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9e433-479">Following is a combiner example:</span></span>

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

<span data-ttu-id="9e433-480">Bu kullanım örneği senaryosu biz analizi raporu hello satıcısında için oluşturmakta olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="9e433-480">In this use-case scenario, we are building an analytics report for hello retailer.</span></span> <span data-ttu-id="9e433-481">Merhaba, belirli bir zaman çerçevesi içinde hello normal perakende üzerinden daha hızlı hello Web sitesi aracılığıyla maliyet birden fazla $20.000 ve, tüm ürünleri satmak toofind hedefidir.</span><span class="sxs-lookup"><span data-stu-id="9e433-481">hello goal is toofind all products that cost more than $20,000 and that sell through hello website faster than through hello regular retailer within a certain time frame.</span></span>

<span data-ttu-id="9e433-482">Merhaba temel U-SQL betiği aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="9e433-482">Here is hello base U-SQL script.</span></span> <span data-ttu-id="9e433-483">Normal bir birleştirme ve bir Birleştirici arasında hello mantığı karşılaştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9e433-483">You can compare hello logic between a regular JOIN and a combiner:</span></span>

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

<span data-ttu-id="9e433-484">Kullanıcı tanımlı bir Birleştirici hello applier nesnesinin yeni bir örneğini çağrılabilir:</span><span class="sxs-lookup"><span data-stu-id="9e433-484">A user-defined combiner can be called as a new instance of hello applier object:</span></span>

```
USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="9e433-485">Veya bir sarmalayıcı fabrika yöntemi hello çağrıldı:</span><span class="sxs-lookup"><span data-stu-id="9e433-485">Or with hello invocation of a wrapper factory method:</span></span>

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="9e433-486">Kullanıcı tanımlı reducers kullanın</span><span class="sxs-lookup"><span data-stu-id="9e433-486">Use user-defined reducers</span></span>

<span data-ttu-id="9e433-487">U-SQL, C# toowrite özel satır kümesi reducers hello kullanıcı tanımlı işleci Genişletilebilirlik Çerçevesi'ni kullanıp IReducer arabirimi uygulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="9e433-487">U-SQL enables you toowrite custom rowset reducers in C# by using hello user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="9e433-488">Kullanıcı tanımlı reducer veya UDR, kullanılan tooeliminate gereksiz satır veri ayıklama sırasında (içe aktarma) olabilir.</span><span class="sxs-lookup"><span data-stu-id="9e433-488">User-defined reducer, or UDR, can be used tooeliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="9e433-489">Ayrıca kullanılan toomanipulate ve olması satırları ve sütunları değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="9e433-489">It also can be used toomanipulate and evaluate rows and columns.</span></span> <span data-ttu-id="9e433-490">Programlanabilirlik mantığına göre onu da hangi satırların ayıklanan toobe gereksinim tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e433-490">Based on programmability logic, it can also define which rows need toobe extracted.</span></span>

<span data-ttu-id="9e433-491">toodefine UDR sınıfı, ihtiyacımız toocreate bir `IReducer` isteğe bağlı bir arabirimiyle `SqlUserDefinedReducer` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="9e433-491">toodefine a UDR class, we need toocreate an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="9e433-492">Bu sınıf arabirimi hello için bir tanım içermelidir `IEnumerable` arabirimi satır kümesi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="9e433-492">This class interface should contain a definition for hello `IEnumerable` interface rowset override.</span></span>

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

<span data-ttu-id="9e433-493">Merhaba **SqlUserDefinedReducer** öznitelik, hello türü kullanıcı tanımlı bir reducer kayıtlı olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="9e433-493">hello **SqlUserDefinedReducer** attribute indicates that hello type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="9e433-494">Bu sınıf devralınan olamaz.</span><span class="sxs-lookup"><span data-stu-id="9e433-494">This class cannot be inherited.</span></span>
<span data-ttu-id="9e433-495">**SqlUserDefinedReducer** kullanıcı tanımlı reducer tanımı için isteğe bağlı bir özniteliktir.</span><span class="sxs-lookup"><span data-stu-id="9e433-495">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="9e433-496">Toodefine IsRecursive özelliği kullandı.</span><span class="sxs-lookup"><span data-stu-id="9e433-496">It's used toodefine IsRecursive property.</span></span>

* <span data-ttu-id="9e433-497">bool IsRecursive</span><span class="sxs-lookup"><span data-stu-id="9e433-497">bool     IsRecursive</span></span>    
* <span data-ttu-id="9e433-498">**doğru** bu Reducer ıdempotent olup olmadığını gösterir =</span><span class="sxs-lookup"><span data-stu-id="9e433-498">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="9e433-499">Merhaba ana programlamasına nesneler **giriş** ve **çıkış**.</span><span class="sxs-lookup"><span data-stu-id="9e433-499">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="9e433-500">Merhaba giriş kullanılan tooenumerate giriş satırları nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="9e433-500">hello input object is used tooenumerate input rows.</span></span> <span data-ttu-id="9e433-501">Çıktı etkinlik azaltma sonucu olarak kullanılan tooset çıkış satır sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="9e433-501">Output is used tooset output rows as a result of reducing activity.</span></span>

<span data-ttu-id="9e433-502">Giriş satırları numaralandırması için kullandığımız hello `Row.Get` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9e433-502">For input rows enumeration, we use hello `Row.Get` method.</span></span>

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

<span data-ttu-id="9e433-503">hello için parametresi hello `Row.Get` yöntemdir hello bir parçası olarak geçirilen bir sütun `PRODUCE` hello sınıfının `REDUCE` temel hello U-SQL komut dosyası ifadesi.</span><span class="sxs-lookup"><span data-stu-id="9e433-503">hello parameter for hello `Row.Get` method is a column that's passed as part of hello `PRODUCE` class of hello `REDUCE` statement of hello U-SQL base script.</span></span> <span data-ttu-id="9e433-504">Toouse ihtiyacımız burada hello doğru veri türü de.</span><span class="sxs-lookup"><span data-stu-id="9e433-504">We need toouse hello correct data type here as well.</span></span>

<span data-ttu-id="9e433-505">Çıkış için hello kullan `output.Set` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9e433-505">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="9e433-506">İle tanımlanan özel reducer çıkışları değerler yalnızca hello önemli toounderstand olan `output.Set` yöntem çağrısı.</span><span class="sxs-lookup"><span data-stu-id="9e433-506">It is important toounderstand that custom reducer only outputs values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="9e433-507">Merhaba gerçek reducer çıkış çağırarak tetiklenir `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="9e433-507">hello actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="9e433-508">Reducer örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9e433-508">Following is a reducer example:</span></span>

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

<span data-ttu-id="9e433-509">Bu kullanım örneği senaryosu hello reducer boş kullanıcı adı satırlarla atlıyor.</span><span class="sxs-lookup"><span data-stu-id="9e433-509">In this use-case scenario, hello reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="9e433-510">Her satır kümesinde için gereken her sütun okur, ardından hello hello kullanıcı adının uzunluğu değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="9e433-510">For each row in rowset, it reads each required column, then evaluates hello length of hello user name.</span></span> <span data-ttu-id="9e433-511">Kullanıcı adı değer uzunluğu 0'dan ise hello gerçek satır çıkarır.</span><span class="sxs-lookup"><span data-stu-id="9e433-511">It outputs hello actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="9e433-512">Özel reducer kullanan temel U-SQL komut dosyası aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="9e433-512">Following is base U-SQL script that uses a custom reducer:</span></span>

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
