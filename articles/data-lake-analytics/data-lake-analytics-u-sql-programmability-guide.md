---
title: "Azure Data Lake için U-SQL Programlama Kılavuzu | Microsoft Docs"
description: "Bir bulut tabanlı büyük veri platformu oluşturmanıza olanak sağlayan bir hizmetler kümesi olan Azure Data Lake içinde hakkında bilgi edinin."
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
ms.openlocfilehash: e4e298475d7be7d51c8bd55be498371ed6ce77a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="85873-103">U-SQL Programlama Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="85873-103">U-SQL programmability guide</span></span>

<span data-ttu-id="85873-104">U-SQL, büyük veri türü için iş yüklerinin tasarlanmış bir sorgu dildir.</span><span class="sxs-lookup"><span data-stu-id="85873-104">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="85873-105">U-SQL benzersiz özellikler SQL benzeri tanımlayıcı dili genişletilebilirlik ve C# tarafından sağlanan programlama ile birleşimidir.</span><span class="sxs-lookup"><span data-stu-id="85873-105">One of the unique features of U-SQL is the combination of the SQL-like declarative language with the extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="85873-106">Bu kılavuzda, biz genişletilebilirlik ve C# kullanarak etkin U-SQL dili ile programlama yoğunlaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85873-106">In this guide, we concentrate on the extensibility and programmability of the U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="85873-107">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="85873-107">Requirements</span></span>

<span data-ttu-id="85873-108">İndirme ve yükleme [Visual Studio için Azure Data Lake Araçları](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="85873-108">Download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="85873-109">U-SQL ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="85873-109">Get started with U-SQL</span></span>  

<span data-ttu-id="85873-110">Aşağıdaki U-SQL betiği bakalım:</span><span class="sxs-lookup"><span data-stu-id="85873-110">Let’s look at the following U-SQL script:</span></span>

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

<span data-ttu-id="85873-111">Adlı bir satır kümesi tanımlar @a ve adlı bir satır kümesi oluşturur @results gelen @a.</span><span class="sxs-lookup"><span data-stu-id="85873-111">It defines a RowSet called @a and creates a RowSet called @results from @a.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="85873-112">C# türleri ve U-SQL betiği ifadeleri</span><span class="sxs-lookup"><span data-stu-id="85873-112">C# types and expressions in U-SQL script</span></span>

<span data-ttu-id="85873-113">Bir C# ifadesi gibi U-SQL mantıksal işlemleriyle birlikte bir U-SQL ifadesidir `AND`, `OR`, ve `NOT`.</span><span class="sxs-lookup"><span data-stu-id="85873-113">A U-SQL Expression is a C# expression combined with U-SQL logical operations such `AND`, `OR`, and `NOT`.</span></span> <span data-ttu-id="85873-114">U-SQL deyimleri seçin, ayıklama, kullanılabilir nerede, otomatik olarak sahip olmak ve GROUP BY BİLDİRİN.</span><span class="sxs-lookup"><span data-stu-id="85873-114">U-SQL Expressions can be used with SELECT, EXTRACT, WHERE, HAVING, GROUP BY and DECLARE.</span></span>

<span data-ttu-id="85873-115">Örneğin, aşağıdaki komut dosyasını bir dize bir DateTime değeri SELECT yan tümcesinde ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="85873-115">For example, the following script parses a string a DateTime value in the SELECT clause.</span></span>

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

<span data-ttu-id="85873-116">Aşağıdaki komut dosyasını bir dize bir DateTime değeri DECLARE deyimi içinde ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="85873-116">The following script parses a string a DateTime value in a DECLARE statement.</span></span>

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="85873-117">Veri türü dönüştürmeleri için C# ifadeleri kullanma</span><span class="sxs-lookup"><span data-stu-id="85873-117">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="85873-118">Aşağıdaki örnek, C# ifadeler kullanarak bir datetime veri dönüştürme nasıl yapabilirsiniz gösterir.</span><span class="sxs-lookup"><span data-stu-id="85873-118">The following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="85873-119">Bu belirli bir senaryoda, dize TarihSaat veri gece 00:00:00 saat gösterimi standart DateTime değerine dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="85873-119">In this particular scenario, string datetime data is converted to standard datetime with midnight 00:00:00 time notation.</span></span>

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="85873-120">Bugünün tarihini C# ifadeleri kullanma</span><span class="sxs-lookup"><span data-stu-id="85873-120">Use C# expressions for today’s date</span></span>
<span data-ttu-id="85873-121">Bugünün tarihini çıkarmak için aşağıdaki C# ifade kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="85873-121">To pull today’s date, we can use the following C# expression:</span></span>

```
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="85873-122">Bu ifade bir komut dosyası kullanma örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="85873-122">Here's an example of how to use this expression in a script:</span></span>

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



## <a name="using-net-assemblies"></a><span data-ttu-id="85873-123">.NET derlemelerini kullanma</span><span class="sxs-lookup"><span data-stu-id="85873-123">Using .NET assemblies</span></span>
<span data-ttu-id="85873-124">U-SQL'nin genişletilebilirlik modeli, özel kod ekleme olanağı yoğun olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="85873-124">U-SQL’s extensibility model relies heavily on the ability to add custom code.</span></span> <span data-ttu-id="85873-125">Şu anda, U-SQL kendi Microsoft eklemek için kolay yollar sağlar. NET tabanlı kodda (özellikle, C#).</span><span class="sxs-lookup"><span data-stu-id="85873-125">Currently, U-SQL provides you with easy ways to add your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="85873-126">Ancak, VB.NET veya F # gibi diğer .NET dilleri yazılmış özel kod ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85873-126">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span> 

### <a name="register-a-net-assembly"></a><span data-ttu-id="85873-127">Bir .NET derlemesi kaydetme</span><span class="sxs-lookup"><span data-stu-id="85873-127">Register a .NET assembly</span></span>

<span data-ttu-id="85873-128">Bir .NET derlemesi bir U-SQL veritabanına yerleştirmek için CREATE ASSEMBLY deyimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="85873-128">Use the CREATE ASSEMBLY statement to place a .NET assembly into a U-SQL Database.</span></span> <span data-ttu-id="85873-129">Bir veritabanında bir derlemeyi olduktan sonra U-SQL betiklerini referans DERLEMESİNİ deyimi kullanarak bu derlemeler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85873-129">Once an assembly is in a database, U-SQL scripts can use those assemblies by using the REFERENCE ASSEMBLY statement.</span></span> 

<span data-ttu-id="85873-130">Aşağıdaki kod, bir derlemeyi kaydetmeye gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="85873-130">The following code shows how to register an assembly:</span></span>

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

<span data-ttu-id="85873-131">Aşağıdaki kod, bir derleme başvurusu gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="85873-131">The following code shows how to reference an assembly:</span></span>

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

<span data-ttu-id="85873-132">Başvurun [derleme kayıt yönergeleri](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) , bu konuda daha ayrıntılı ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="85873-132">Consult the [assembly registration instructions](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) that covers this topic in greater detail.</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="85873-133">Derleme sürümü oluşturma kullanın</span><span class="sxs-lookup"><span data-stu-id="85873-133">Use assembly versioning</span></span>
<span data-ttu-id="85873-134">Şu anda, U-SQL .NET Framework sürüm 4.5 kullanır.</span><span class="sxs-lookup"><span data-stu-id="85873-134">Currently, U-SQL uses the .NET Framework version 4.5.</span></span> <span data-ttu-id="85873-135">Bu nedenle, kendi derlemeleri çalışma zamanı bu sürümü ile uyumlu olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="85873-135">So ensure that your own assemblies are compatible with that version of the runtime.</span></span>

<span data-ttu-id="85873-136">U-SQL kodun bir 64-bit (x 64) biçiminde daha önce belirtildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="85873-136">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="85873-137">Bu nedenle, kodunuzu x64 üzerinde çalıştırmak için derlendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="85873-137">So make sure that your code is compiled to run on x64.</span></span> <span data-ttu-id="85873-138">Aksi takdirde, daha önce gösterilen yanlış biçim hatası alırsınız.</span><span class="sxs-lookup"><span data-stu-id="85873-138">Otherwise you get the incorrect format error shown earlier.</span></span>

<span data-ttu-id="85873-139">Her derleme dll dosyasını karşıya ve farklı bir çalışma zamanı, yerel bir derleme veya bir yapılandırma dosyası gibi bir kaynak dosya en fazla 400 MB olabilir.</span><span class="sxs-lookup"><span data-stu-id="85873-139">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="85873-140">Kaynak dağıtma aracılığıyla ya da derlemeler ve ek dosyalarına başvuruları yoluyla dağıtılan kaynakları toplam boyutu 3 GB aşamaz.</span><span class="sxs-lookup"><span data-stu-id="85873-140">The total size of deployed resources, either via DEPLOY RESOURCE or via references to assemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="85873-141">Son olarak, her U-SQL veritabanı herhangi verilen derleme bir sürümü yalnızca içerebileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="85873-141">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="85873-142">Örneğin, sürüm 7 ve sürüm 8 NewtonSoft Json.Net kitaplığının ihtiyacınız varsa, bunları iki farklı veritabanlarında kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="85873-142">For example, if you need both version 7 and version 8 of the NewtonSoft Json.Net library, you need to register them in two different databases.</span></span> <span data-ttu-id="85873-143">Ayrıca, her komut dosyası yalnızca bir verilen derleme DLL sürümüne başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="85873-143">Furthermore, each script can only refer to one version of a given assembly DLL.</span></span> <span data-ttu-id="85873-144">Bu bakımdan, U-SQL C# derleme yönetimi ve sürüm oluşturma semantiğini izler.</span><span class="sxs-lookup"><span data-stu-id="85873-144">In this respect, U-SQL follows the C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="85873-145">Kullanıcı tanımlı işlevler kullanın: UDF</span><span class="sxs-lookup"><span data-stu-id="85873-145">Use user-defined functions: UDF</span></span>
<span data-ttu-id="85873-146">U-SQL kullanıcı tanımlı işlevler veya UDF, parametreleri kabul, (örneğin, karmaşık bir hesaplama) bir eylem gerçekleştirmek ve bu eylem bir değer olarak sonuç yordamları programlama.</span><span class="sxs-lookup"><span data-stu-id="85873-146">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return the result of that action as a value.</span></span> <span data-ttu-id="85873-147">UDF dönüş değerini, yalnızca tek bir skaler olabilir.</span><span class="sxs-lookup"><span data-stu-id="85873-147">The return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="85873-148">U-SQL UDF temel U-SQL betiği diğer C# skaler bir işlev gibi çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="85873-148">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="85873-149">U-SQL kullanıcı tanımlı işlevler olarak başlatma öneririz **ortak** ve **statik**.</span><span class="sxs-lookup"><span data-stu-id="85873-149">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

<span data-ttu-id="85873-150">İlk bir UDF oluşturma basit örneğe bakalım.</span><span class="sxs-lookup"><span data-stu-id="85873-150">First let’s look at the simple example of creating a UDF.</span></span>

<span data-ttu-id="85873-151">Bu kullanım örneği senaryosu biz mali ayı ilk oturum açma için belirli kullanıcı ve Mali Çeyrek yıl de dahil olmak üzere mali dönemi belirlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="85873-151">In this use-case scenario, we need to determine the fiscal period, including the fiscal quarter and fiscal month of the first sign-in for the specific user.</span></span> <span data-ttu-id="85873-152">Senaryomuzda yılın ilk mali ayı Haziran ' dir.</span><span class="sxs-lookup"><span data-stu-id="85873-152">The first fiscal month of the year in our scenario is June.</span></span>

<span data-ttu-id="85873-153">Mali dönemi hesaplamak için size aşağıdaki C# işlevi tanıtmaktadır:</span><span class="sxs-lookup"><span data-stu-id="85873-153">To calculate fiscal period, we introduce the following C# function:</span></span>

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

<span data-ttu-id="85873-154">Mali ayı ve üç aylık dönem hesaplar ve bir string değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="85873-154">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="85873-155">Haziran için ilk mali Çeyreğin ilk ayı "Q1:P1" kullanırız.</span><span class="sxs-lookup"><span data-stu-id="85873-155">For June, the first month of the first fiscal quarter, we use "Q1:P1".</span></span> <span data-ttu-id="85873-156">Temmuz, biz "Q1:P2" kullanın ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="85873-156">For July, we use "Q1:P2", and so on.</span></span>

<span data-ttu-id="85873-157">Bu, biz U-SQL Projemizin kullanacaksanız bir normal C# işlevdir.</span><span class="sxs-lookup"><span data-stu-id="85873-157">This is a regular C# function that we are going to use in our U-SQL project.</span></span>

<span data-ttu-id="85873-158">Arka plan kodu bölüm bu senaryoda, nasıl göründüğünü aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="85873-158">Here is how the code-behind section looks in this scenario:</span></span>

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

<span data-ttu-id="85873-159">Şimdi Biz bu işlev temel U-SQL komut dosyasından çağıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="85873-159">Now we are going to call this function from the base U-SQL script.</span></span> <span data-ttu-id="85873-160">Bunu yapmak için bu durumda NameSpace.Class.Function(parameter) olduğu ad alanı dahil işlevi tam olarak nitelenmiş bir ad vermek sahibiz.</span><span class="sxs-lookup"><span data-stu-id="85873-160">To do this, we have to provide a fully qualified name for the function, including the namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="85873-161">Gerçek U-SQL temel betiği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="85873-161">Following is the actual U-SQL base script:</span></span>

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
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="85873-162">Çıkış dosyası komut dosyası yürütme aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="85873-162">Following is the output file of the script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="85873-163">Bu örnek, basit bir satır içi U-SQL UDF'de kullanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="85873-163">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="85873-164">UDF çağrılarını arasında durumu tutun</span><span class="sxs-lookup"><span data-stu-id="85873-164">Keep state between UDF invocations</span></span>
<span data-ttu-id="85873-165">U-SQL C# programlama nesnelerini daha, arka plan kodu Genel değişkenler aracılığıyla etkileşim kullanan gelişmiş.</span><span class="sxs-lookup"><span data-stu-id="85873-165">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through the code-behind global variables.</span></span> <span data-ttu-id="85873-166">Aşağıdaki iş kullanım örneği senaryosu bakalım.</span><span class="sxs-lookup"><span data-stu-id="85873-166">Let’s look at the following business use-case scenario.</span></span>

<span data-ttu-id="85873-167">Büyük kuruluşlarda, kullanıcıların iç uygulamaları çeşitleri arasında geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85873-167">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="85873-168">Bunlar, Microsoft Dynamics CRM, Powerbı vb. içerebilir.</span><span class="sxs-lookup"><span data-stu-id="85873-168">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="85873-169">Müşteriler kullanıcılar kullanım eğilimleri nelerdir, farklı uygulamalar arasında nasıl geçiş, bir telemetri analizi uygulamak istediğiniz ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="85873-169">Customers might want to apply a telemetry analysis of how users switch between different applications, what the usage trends are, and so on.</span></span> <span data-ttu-id="85873-170">Uygulama kullanımı en iyi duruma getirme iş için belirtilir.</span><span class="sxs-lookup"><span data-stu-id="85873-170">The goal for the business is to optimize application usage.</span></span> <span data-ttu-id="85873-171">Farklı uygulamalar veya oturum açma belirli yordamları birleştirmek de isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85873-171">They also might want to combine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="85873-172">Bu hedefe ulaşmak için biz oturum kimliklerini belirlemek ve öteleme arasında oluştu son oturumun süresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="85873-172">To achieve this goal, we have to determine session IDs and lag time between the last session that occurred.</span></span>

<span data-ttu-id="85873-173">Bir önceki oturum açma bulma ve ardından bu oturum açma aynı uygulama için oluşturulan tüm oturumları atamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="85873-173">We need to find a previous sign-in and then assign this sign-in to all sessions that are being generated to the same application.</span></span> <span data-ttu-id="85873-174">U-SQL temel betiği bize ÖTELEME işlevi zaten hesaplanmış sütunlar üzerinde hesaplamalar uygulamak izin vermeyen ilk iştir.</span><span class="sxs-lookup"><span data-stu-id="85873-174">The first challenge is that U-SQL base script doesn't allow us to apply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="85873-175">Belirli bir oturum için aynı süre içinde tüm oturumları tutmak sahibiz ikinci iştir.</span><span class="sxs-lookup"><span data-stu-id="85873-175">The second challenge is that we have to keep the specific session for all sessions within the same time period.</span></span>

<span data-ttu-id="85873-176">İçinde bir arka plan kodu bölümü genel değişkeni kullanırız bu sorunu çözmek için: `static public string globalSession;`.</span><span class="sxs-lookup"><span data-stu-id="85873-176">To solve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="85873-177">Bu genel değişkeni tüm satır kümesi için komut dosyası yürütme sırasında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="85873-177">This global variable is applied to the entire rowset during our script execution.</span></span>

<span data-ttu-id="85873-178">U-SQL programımız arka plan kodu bölümünü şöyledir:</span><span class="sxs-lookup"><span data-stu-id="85873-178">Here is the code-behind section of our U-SQL program:</span></span>

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

<span data-ttu-id="85873-179">Bu örnek, genel değişkeni gösterir `static public string globalSession;` içinde kullanılan `getStampUserSession` işlevi ve oturum parametresi değiştirildiğinde her zaman yeniden.</span><span class="sxs-lookup"><span data-stu-id="85873-179">This example shows the global variable `static public string globalSession;` used inside the `getStampUserSession` function and getting reinitialized each time the Session parameter is changed.</span></span>

<span data-ttu-id="85873-180">U-SQL temel komut aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="85873-180">The U-SQL base script is as follows:</span></span>

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
    TO @out2
    ORDER BY UserName, EventDateTime ASC
    USING Outputters.Csv();
```

<span data-ttu-id="85873-181">İşlev `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` burada ikinci bellek satır kümesi hesaplama sırasında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="85873-181">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during the second memory rowset calculation.</span></span> <span data-ttu-id="85873-182">Bunu geçirir `UserSessionTimestamp` sütun ve kadar değeri döndürür `UserSessionTimestamp` değişti.</span><span class="sxs-lookup"><span data-stu-id="85873-182">It passes the `UserSessionTimestamp` column and returns the value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="85873-183">Çıktı dosyası aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="85873-183">The output file is as follows:</span></span>

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

<span data-ttu-id="85873-184">Bu örnek bir genel değişkeni tüm bellek satır kümesi için uygulanan bir arka plan kodu bölüm içinde kullandığımız daha karmaşık bir kullanım örneği senaryosu gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="85873-184">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied to the entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="85873-185">Kullanıcı tanımlı türler kullanın: UDT</span><span class="sxs-lookup"><span data-stu-id="85873-185">Use user-defined types: UDT</span></span>
<span data-ttu-id="85873-186">Kullanıcı tanımlı türler veya UDT, başka bir programlama, U-SQL özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="85873-186">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="85873-187">U-SQL UDT bir normal C# kullanıcı tanımlı tür gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="85873-187">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="85873-188">C# yerleşik ve özel kullanıcı tanımlı türler kullanılmasına kesin türü belirtilmiş bir dil değil.</span><span class="sxs-lookup"><span data-stu-id="85873-188">C# is a strongly typed language that allows the use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="85873-189">U-SQL örtük olarak serileştirmek veya satır kümeleri tepe arasında UDT geçirildiğinde rasgele atama anlayabileceği olamaz.</span><span class="sxs-lookup"><span data-stu-id="85873-189">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when the UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="85873-190">Bu, kullanıcının açık bir biçimlendirici IFormatter arabirimini kullanarak sağlamak sahip anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="85873-190">This means that the user has to provide an explicit formatter by using the IFormatter interface.</span></span> <span data-ttu-id="85873-191">Bu, U-SQL ile serileştirme sağlar ve yöntemleri için UDT anlayabileceği.</span><span class="sxs-lookup"><span data-stu-id="85873-191">This provides U-SQL with the serialize and de-serialize methods for the UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="85873-192">U-SQL'nin yerleşik ayıklayıcıları ve outputters şu anda serileştirmek veya seri durumdan UDT veri ya da hatta IFormatter kümesiyle dosyalarından.</span><span class="sxs-lookup"><span data-stu-id="85873-192">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data to or from files even with the IFormatter set.</span></span> <span data-ttu-id="85873-193">Bu nedenle çıktı ifadesiyle bir dosyaya UDT veri yazma veya bir ayıklayıcısı ile okuma, bir string veya byte dizisi olarak geçirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="85873-193">So when you're writing UDT data to a file with the OUTPUT statement, or reading it with an extractor, you have to pass it as a string or byte array.</span></span> <span data-ttu-id="85873-194">Ardından serileştirme çağırın ve kod (diğer bir deyişle, UDT'ın ToString() yöntemini) açıkça seri durumundan çıkarma.</span><span class="sxs-lookup"><span data-stu-id="85873-194">Then you call the serialization and deserialization code (that is, the UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="85873-195">Kullanıcı tanımlı ayıklayıcıları ve outputters, diğer yandan okuyabilir ve atama yazma.</span><span class="sxs-lookup"><span data-stu-id="85873-195">User-defined extractors and outputters, on the other hand, can read and write UDTs.</span></span>

<span data-ttu-id="85873-196">Biz UDT AYIKLAYICISI veya OUTPUTTER (dışında önceki seçin), aşağıda gösterildiği gibi kullanırsanız:</span><span class="sxs-lookup"><span data-stu-id="85873-196">If we try to use UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="85873-197">Biz, şu hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="85873-197">We receive the following error:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used to output column myfield of type
MyNameSpace.Myfunction_Returning_UDT.

Description:

Outputters.Text only supports built-in types.

Resolution:

Implement a custom outputter that knows how to serialize this type, or call a serialization method on the type in
the preceding SELECT.   C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

<span data-ttu-id="85873-198">İçinde outputter UDT ile çalışmak için ya da ToString() yöntemiyle dize veya bir özel outputter oluşturmak için seri hale getirmek sahibiz.</span><span class="sxs-lookup"><span data-stu-id="85873-198">To work with UDT in outputter, we either have to serialize it to string with the ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="85873-199">Atama, grup tarafından şu anda kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="85873-199">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="85873-200">UDT grubu tarafından kullanılıyorsa, aşağıdaki hata oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="85873-200">If UDT is used in GROUP BY, the following error is thrown:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
for column myfield

Description:

GROUP BY doesn't support UDT or Complex types.

Resolution:

Add a SELECT statement where you can project a scalar column that you want to use with GROUP BY.
C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
62  5   USQL-Programmability
```

<span data-ttu-id="85873-201">UDT tanımlamak için biz gerekir:</span><span class="sxs-lookup"><span data-stu-id="85873-201">To define a UDT, we have to:</span></span>

* <span data-ttu-id="85873-202">Şu ad alanlarından ekleyin:</span><span class="sxs-lookup"><span data-stu-id="85873-202">Add the following namespaces:</span></span>

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* <span data-ttu-id="85873-203">Ekleme `Microsoft.Analytics.Interfaces`, UDT arabirimler için gerekli olduğu.</span><span class="sxs-lookup"><span data-stu-id="85873-203">Add `Microsoft.Analytics.Interfaces`, which is required for the UDT interfaces.</span></span> <span data-ttu-id="85873-204">Ayrıca, `System.IO` IFormatter arabirimi tanımlamak için gerekli.</span><span class="sxs-lookup"><span data-stu-id="85873-204">In addition, `System.IO` might be needed to define the IFormatter interface.</span></span>

* <span data-ttu-id="85873-205">Kullanılan tanımlı bir tür SqlUserDefinedType özniteliğiyle tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="85873-205">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="85873-206">**SqlUserDefinedType** bir tür tanımı bir kullanıcı tanımlı tür (UDT) U-SQL'de bir bütünleştirilmiş işaretlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85873-206">**SqlUserDefinedType** is used to mark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="85873-207">Öznitelik özellikleri UDT fiziksel özelliklerini yansıtır.</span><span class="sxs-lookup"><span data-stu-id="85873-207">The properties on the attribute reflect the physical characteristics of the UDT.</span></span> <span data-ttu-id="85873-208">Bu sınıf devralınan olamaz.</span><span class="sxs-lookup"><span data-stu-id="85873-208">This class cannot be inherited.</span></span>

<span data-ttu-id="85873-209">SqlUserDefinedType UDT tanımı için gerekli bir özniteliktir.</span><span class="sxs-lookup"><span data-stu-id="85873-209">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="85873-210">Sınıf oluşturucu:</span><span class="sxs-lookup"><span data-stu-id="85873-210">The constructor of the class:</span></span>  

* <span data-ttu-id="85873-211">SqlUserDefinedTypeAttribute (türü biçimlendirici)</span><span class="sxs-lookup"><span data-stu-id="85873-211">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="85873-212">Biçimlendirici yazın: gerekli bir UDT biçimlendirici--özellikle tanımlamak için parametre türü `IFormatter` arabirimi gerekir bayraklarıdır burada.</span><span class="sxs-lookup"><span data-stu-id="85873-212">Type formatter: Required parameter to define an UDT formatter--specifically, the type of the `IFormatter` interface must be passed here.</span></span>

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* <span data-ttu-id="85873-213">Tipik UDT, ayrıca aşağıdaki örnekte gösterildiği gibi IFormatter arabirimi tanımını gerektirir:</span><span class="sxs-lookup"><span data-stu-id="85873-213">Typical UDT also requires definition of the IFormatter interface, as shown in the following example:</span></span>

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

<span data-ttu-id="85873-214">`IFormatter` Arabirimi serileştirir ve kök türüne sahip bir nesne grafiğinin XML'deki serileştiren \<typeparamref name = "T" >.</span><span class="sxs-lookup"><span data-stu-id="85873-214">The `IFormatter` interface serializes and de-serializes an object graph with the root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="85873-215">\<typeparam name = "T" > serileştirme ve seri durumdan kök türü için Nesne grafiği.</span><span class="sxs-lookup"><span data-stu-id="85873-215">\<typeparam name="T">The root type for the object graph to serialize and de-serialize.</span></span>

* <span data-ttu-id="85873-216">**Seri durumdan**: Sağlanan akış verilerini XML'deki serileştirir ve grafik nesnelerinin reconstitutes.</span><span class="sxs-lookup"><span data-stu-id="85873-216">**Deserialize**: De-serializes the data on the provided stream and reconstitutes the graph of objects.</span></span>

* <span data-ttu-id="85873-217">**Seri hale**: bir nesne ya da nesneleriyle verilen kök sağlanan akış grafiği Serileştirir.</span><span class="sxs-lookup"><span data-stu-id="85873-217">**Serialize**: Serializes an object, or graph of objects, with the given root to the provided stream.</span></span>

<span data-ttu-id="85873-218">`MyType`Örnek: türünün örneği.</span><span class="sxs-lookup"><span data-stu-id="85873-218">`MyType` instance: Instance of the type.</span></span>  
<span data-ttu-id="85873-219">`IColumnWriter`yazıcı / `IColumnReader` okuyucu: temel sütun akış.</span><span class="sxs-lookup"><span data-stu-id="85873-219">`IColumnWriter` writer / `IColumnReader` reader: The underlying column stream.</span></span>  
<span data-ttu-id="85873-220">`ISerializationContext`Bağlam: seri hale getirme sırasında akış kaynak veya hedef bağlamının belirten bayrakları kümesini tanımlayan Enum.</span><span class="sxs-lookup"><span data-stu-id="85873-220">`ISerializationContext` context: Enum that defines a set of flags that specifies the source or destination context for the stream during serialization.</span></span>

* <span data-ttu-id="85873-221">**Ara**: kaynak veya hedef bağlamı kalıcı depolama olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="85873-221">**Intermediate**: Specifies that the source or destination context is not a persisted store.</span></span>

* <span data-ttu-id="85873-222">**Kalıcılığı**: kaynak veya hedef bağlamı kalıcı depolama alanının olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="85873-222">**Persistence**: Specifies that the source or destination context is a persisted store.</span></span>

<span data-ttu-id="85873-223">Bir normal C# türü olarak bir U-SQL UDT tanımı geçersiz kılmaları işleçlerini gibi içerebilir +/ == /! =.</span><span class="sxs-lookup"><span data-stu-id="85873-223">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="85873-224">Statik yöntemler de içerir.</span><span class="sxs-lookup"><span data-stu-id="85873-224">It can also include static methods.</span></span> <span data-ttu-id="85873-225">Biz bu UDT U-SQL MIN toplama işlevi için parametre olarak kullanacaksanız, örneğin, biz tanımlamak varsa < işleci geçersiz kılma.</span><span class="sxs-lookup"><span data-stu-id="85873-225">For example, if we are going to use this UDT as a parameter to a U-SQL MIN aggregate function, we have to define < operator override.</span></span>

<span data-ttu-id="85873-226">Bu kılavuzda daha önce belirli bir tarihten Qn:Pn (Q1:P10) biçiminde mali dönem tanımlaması için bir örnek gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="85873-226">Earlier in this guide, we demonstrated an example for fiscal period identification from the specific date in the format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="85873-227">Aşağıdaki örnek, mali dönemi değerlerini için özel bir tür tanımlamak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="85873-227">The following example shows how to define a custom type for fiscal period values.</span></span>

<span data-ttu-id="85873-228">Aşağıdaki özel UDT ve IFormatter arabirimi arka plan kodu bölümle örneğidir:</span><span class="sxs-lookup"><span data-stu-id="85873-228">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

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

<span data-ttu-id="85873-229">İki sayı türü tanımlanmış içerir: üç aylık dönem ve ay.</span><span class="sxs-lookup"><span data-stu-id="85873-229">The defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="85873-230">İşleç == /! = / > / < ve statik yöntemi ToString() burada tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="85873-230">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="85873-231">Daha önce belirtildiği gibi UDT SELECT ifadelerde kullanılabilir, ancak OUTPUTTER/AYIKLAYICISI özel serileştirme kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="85873-231">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="85873-232">ToString() bir dize olarak serileştirilmesi gereken ya da özel bir OUTPUTTER/AYIKLAYICISI kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85873-232">It either has to be serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="85873-233">Şimdi şimdi UDT kullanımını tartışın.</span><span class="sxs-lookup"><span data-stu-id="85873-233">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="85873-234">Arka plan kodu bölümünde, biz bizim GetFiscalPeriod işlevi için değiştirilmiştir:</span><span class="sxs-lookup"><span data-stu-id="85873-234">In a code-behind section, we changed our GetFiscalPeriod function to the following:</span></span>

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

<span data-ttu-id="85873-235">Gördüğünüz gibi bizim FiscalPeriod türü değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="85873-235">As you can see, it returns the value of our FiscalPeriod type.</span></span>

<span data-ttu-id="85873-236">Daha fazla U-SQL temel komut dosyasında kullanmak nasıl bir örneği burada sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="85873-236">Here we provide an example of how to use it further in U-SQL base script.</span></span> <span data-ttu-id="85873-237">Bu örnek, farklı UDT çağırma formlardan U-SQL betiği gösterir.</span><span class="sxs-lookup"><span data-stu-id="85873-237">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

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

       // This user-defined type was created in the prior SELECT.  Passing the UDT to this subsequent SELECT would have failed if the UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="85873-238">Bir tam arka plan kodu bölümü bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="85873-238">Here's an example of a full code-behind section:</span></span>

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

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="85873-239">Kullanıcı tanımlı toplamlarda kullanın: UDAGG</span><span class="sxs-lookup"><span data-stu-id="85873-239">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="85873-240">Kullanıcı tanımlı toplamlarda, toplama ile ilgili olan tüm işlevler out-of--box U-SQL ile gönderilmeyen ' dir.</span><span class="sxs-lookup"><span data-stu-id="85873-240">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="85873-241">Örneğin, özel matematik hesaplamaları, dize birleştirmeler, işlemeleri dizeler vb. ile gerçekleştirmek için bir toplama olabilir.</span><span class="sxs-lookup"><span data-stu-id="85873-241">The example can be an aggregate to perform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="85873-242">Kullanıcı tanımlı toplama temel sınıf tanımı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="85873-242">The user-defined aggregate base class definition is as follows:</span></span>

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

<span data-ttu-id="85873-243">**SqlUserDefinedAggregate** türü kullanıcı tanımlı toplama olarak kayıtlı olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="85873-243">**SqlUserDefinedAggregate** indicates that the type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="85873-244">Bu sınıf devralınan olamaz.</span><span class="sxs-lookup"><span data-stu-id="85873-244">This class cannot be inherited.</span></span>

<span data-ttu-id="85873-245">SqlUserDefinedType özniteliği **isteğe bağlı** UDAGG tanımı.</span><span class="sxs-lookup"><span data-stu-id="85873-245">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="85873-246">Üç soyut parametreleri geçirmek temel sınıf sağlar: iki giriş parametreleri ve bir sonucu olarak.</span><span class="sxs-lookup"><span data-stu-id="85873-246">The base class allows you to pass three abstract parameters: two as input parameters and one as the result.</span></span> <span data-ttu-id="85873-247">Veri türleri değişkendir ve sınıf devralma sırasında tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="85873-247">The data types are variable and should be defined during class inheritance.</span></span>

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

* <span data-ttu-id="85873-248">**Init** hesaplaması sırasında her grup için bir kez çağırır.</span><span class="sxs-lookup"><span data-stu-id="85873-248">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="85873-249">Bu, her toplama grubu için bir başlatma yordamının sağlar.</span><span class="sxs-lookup"><span data-stu-id="85873-249">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="85873-250">**Accumulate** her bir değer için bir kez çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="85873-250">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="85873-251">Toplama algoritması ana işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="85873-251">It provides the main functionality for the aggregation algorithm.</span></span> <span data-ttu-id="85873-252">Sınıf devralma sırasında tanımlanan çeşitli veri türlerine sahip toplama değerlerini için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="85873-252">It can be used to aggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="85873-253">Değişken veri türünde iki parametre kabul edebilir.</span><span class="sxs-lookup"><span data-stu-id="85873-253">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="85873-254">**Sonlandırma** her grup için sonucu çıkarmak için işlem sonunda toplama grubu başına bir kez çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="85873-254">**Terminate** is executed once per aggregation group at the end of processing to output the result for each group.</span></span>

<span data-ttu-id="85873-255">Doğru giriş ve çıkış veri türlerinin bildirmek için sınıf tanımını aşağıdaki şekilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="85873-255">To declare correct input and output data types, use the class definition as follows:</span></span>

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="85873-256">T1: ilk parametre birikmesine</span><span class="sxs-lookup"><span data-stu-id="85873-256">T1: First parameter to accumulate</span></span>
* <span data-ttu-id="85873-257">T2: ilk parametre birikmesine</span><span class="sxs-lookup"><span data-stu-id="85873-257">T2: First parameter to accumulate</span></span>
* <span data-ttu-id="85873-258">TResult: dönüş türü Sonlandır</span><span class="sxs-lookup"><span data-stu-id="85873-258">TResult: Return type of terminate</span></span>

<span data-ttu-id="85873-259">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="85873-259">For example:</span></span>

```
public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="85873-260">or</span><span class="sxs-lookup"><span data-stu-id="85873-260">or</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="85873-261">U-SQL UDAGG kullanın</span><span class="sxs-lookup"><span data-stu-id="85873-261">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="85873-262">UDAGG kullanmak için ilk kod arkasında tanımlayın veya daha önce bahsedildiği gibi varolan programlama DLL başvuru.</span><span class="sxs-lookup"><span data-stu-id="85873-262">To use UDAGG, first define it in code-behind or reference it from the existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="85873-263">Ardından aşağıdaki sözdizimini kullanın:</span><span class="sxs-lookup"><span data-stu-id="85873-263">Then use the following syntax:</span></span>

```
AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="85873-264">UDAGG bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="85873-264">Here is an example of UDAGG:</span></span>

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

<span data-ttu-id="85873-265">Ve temel U-SQL betiği:</span><span class="sxs-lookup"><span data-stu-id="85873-265">And base U-SQL script:</span></span>

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

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="85873-266">Bu kullanım örneği senaryosu sınıfı GUID'leri belirli kullanıcılar için birleştirme.</span><span class="sxs-lookup"><span data-stu-id="85873-266">In this use-case scenario, we concatenate class GUIDs for the specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="85873-267">Kullanıcı tanımlı nesneler kullanın: UDO</span><span class="sxs-lookup"><span data-stu-id="85873-267">Use user-defined objects: UDO</span></span>
<span data-ttu-id="85873-268">U-SQL kullanıcı tanımlı nesneler veya UDO adlı özel programlama nesneleri tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="85873-268">U-SQL enables you to define custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="85873-269">U-SQL UDO listesi aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="85873-269">The following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="85873-270">Kullanıcı tanımlı ayıklayıcıları</span><span class="sxs-lookup"><span data-stu-id="85873-270">User-defined extractors</span></span>
    * <span data-ttu-id="85873-271">Extract satır satır</span><span class="sxs-lookup"><span data-stu-id="85873-271">Extract row by row</span></span>
    * <span data-ttu-id="85873-272">Özel yapılandırılmış dosyalarından veri ayıklama gerçekleştirmek için kullanılır</span><span class="sxs-lookup"><span data-stu-id="85873-272">Used to implement data extraction from custom structured files</span></span>

* <span data-ttu-id="85873-273">Kullanıcı tanımlı outputters</span><span class="sxs-lookup"><span data-stu-id="85873-273">User-defined outputters</span></span>
    * <span data-ttu-id="85873-274">Çıkış satır satır</span><span class="sxs-lookup"><span data-stu-id="85873-274">Output row by row</span></span>
    * <span data-ttu-id="85873-275">Çıktı özel veri türleri veya özel dosya biçimleri kullanılan</span><span class="sxs-lookup"><span data-stu-id="85873-275">Used to output custom data types or custom file formats</span></span>

* <span data-ttu-id="85873-276">Kullanıcı tanımlı işlemcileri</span><span class="sxs-lookup"><span data-stu-id="85873-276">User-defined processors</span></span>
    * <span data-ttu-id="85873-277">Bir satır almak ve bir satır üretir</span><span class="sxs-lookup"><span data-stu-id="85873-277">Take one row and produce one row</span></span>
    * <span data-ttu-id="85873-278">Sütun sayısını azaltın veya varolan bir sütun kümesinden türetilmiş değerlerle yeni sütun oluşturmak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="85873-278">Used to reduce the number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="85873-279">Kullanıcı tanımlı appliers</span><span class="sxs-lookup"><span data-stu-id="85873-279">User-defined appliers</span></span>
    * <span data-ttu-id="85873-280">Bir satır alın ve n satır 0 üretir</span><span class="sxs-lookup"><span data-stu-id="85873-280">Take one row and produce 0 to n rows</span></span>
    * <span data-ttu-id="85873-281">Dış/ARASI UYGULA ile kullanılan</span><span class="sxs-lookup"><span data-stu-id="85873-281">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="85873-282">Kullanıcı tanımlı combiners</span><span class="sxs-lookup"><span data-stu-id="85873-282">User-defined combiners</span></span>
    * <span data-ttu-id="85873-283">Satır kümeleri--kullanıcı tanımlı birleştirmeler birleştirir</span><span class="sxs-lookup"><span data-stu-id="85873-283">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="85873-284">Kullanıcı tanımlı reducers</span><span class="sxs-lookup"><span data-stu-id="85873-284">User-defined reducers</span></span>
    * <span data-ttu-id="85873-285">N satırları almak ve bir satır üretir</span><span class="sxs-lookup"><span data-stu-id="85873-285">Take n rows and produce one row</span></span>
    * <span data-ttu-id="85873-286">Satır sayısını azaltmak için kullanılan</span><span class="sxs-lookup"><span data-stu-id="85873-286">Used to reduce the number of rows</span></span>

<span data-ttu-id="85873-287">UDO genellikle açıkça U-SQL komut dosyasında aşağıdaki U-SQL deyimlerini bir parçası olarak adlandırılır:</span><span class="sxs-lookup"><span data-stu-id="85873-287">UDO is typically called explicitly in U-SQL script as part of the following U-SQL statements:</span></span>

* <span data-ttu-id="85873-288">EXTRACT</span><span class="sxs-lookup"><span data-stu-id="85873-288">EXTRACT</span></span>
* <span data-ttu-id="85873-289">ÇIKTI</span><span class="sxs-lookup"><span data-stu-id="85873-289">OUTPUT</span></span>
* <span data-ttu-id="85873-290">İŞLEM</span><span class="sxs-lookup"><span data-stu-id="85873-290">PROCESS</span></span>
* <span data-ttu-id="85873-291">BİRLEŞTİRME</span><span class="sxs-lookup"><span data-stu-id="85873-291">COMBINE</span></span>
* <span data-ttu-id="85873-292">AZALTMA</span><span class="sxs-lookup"><span data-stu-id="85873-292">REDUCE</span></span>

> [!NOTE]  
> <span data-ttu-id="85873-293">UDO'ın 0,5 Gb bellek tüketmesine sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="85873-293">UDO’s are limited to consume 0.5Gb memory.</span></span>  <span data-ttu-id="85873-294">Bu bellek kısıtlaması yerel yürütmeleri için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="85873-294">This memory limitation does not apply to local executions.</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="85873-295">Kullanıcı tanımlı ayıklayıcıları kullanın</span><span class="sxs-lookup"><span data-stu-id="85873-295">Use user-defined extractors</span></span>
<span data-ttu-id="85873-296">U-SQL EXTRACT deyimi kullanarak dış veri almanıza izin verir.</span><span class="sxs-lookup"><span data-stu-id="85873-296">U-SQL allows you to import external data by using an EXTRACT statement.</span></span> <span data-ttu-id="85873-297">Bir ayıklama deyimi yerleşik UDO ayıklayıcıları kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="85873-297">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="85873-298">*Extractors.Text()*: farklı kodlamaları sınırlandırılmış metin dosyalarından ayıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="85873-298">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="85873-299">*Extractors.Csv()*: ayıklama virgülle ayrılmış değer (CSV) dosyaları farklı kodlamaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="85873-299">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="85873-300">*Extractors.Tsv()*: ayıklama sekmeyle ayrılmış değerinden farklı kodlamaları (TSV) dosyaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="85873-300">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="85873-301">Özel ayıklayıcısı geliştirmek yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="85873-301">It can be useful to develop a custom extractor.</span></span> <span data-ttu-id="85873-302">Biz aşağıdaki görevlerden herhangi birini yapmak istiyorsanız, bu veri içe aktarma sırasında yararlı olabilir:</span><span class="sxs-lookup"><span data-stu-id="85873-302">This can be helpful during data import if we want to do any of the following tasks:</span></span>

* <span data-ttu-id="85873-303">Giriş verisi sütunları bölme ve tek tek değerleri değiştirerek değiştirin.</span><span class="sxs-lookup"><span data-stu-id="85873-303">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="85873-304">İŞLEMCİ işlevselliğini sütunları birleştirmek için daha iyi olur.</span><span class="sxs-lookup"><span data-stu-id="85873-304">The PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="85873-305">Web sayfaları ve e-posta gibi yapılandırılmamış veriler veya XML/JSON gibi yarı yapılandırılmamış veriler ayrıştırılamadı.</span><span class="sxs-lookup"><span data-stu-id="85873-305">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="85873-306">Desteklenmeyen kodlama verileri ayrıştırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="85873-306">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="85873-307">Bir kullanıcı tarafından tanımlanan ayıklayıcısı veya Opyalanan tanımlamak için oluşturmamız gerekir bir `IExtractor` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="85873-307">To define a user-defined extractor, or UDE, we need to create an `IExtractor` interface.</span></span> <span data-ttu-id="85873-308">Tüm giriş parametreleri için sütun/satır sınırlayıcıları gibi ayıklayıcısı ve kodlama, sınıf oluşturucuda tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="85873-308">All input parameters to the extractor, such as column/row delimiters, and encoding, need to be defined in the constructor of the class.</span></span> <span data-ttu-id="85873-309">`IExtractor` Arabirimi için bir tanım da içermelidir `IEnumerable<IRow>` gibi geçersiz kıl:</span><span class="sxs-lookup"><span data-stu-id="85873-309">The `IExtractor`  interface should also contain a definition for the `IEnumerable<IRow>` override as follows:</span></span>

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

<span data-ttu-id="85873-310">**SqlUserDefinedExtractor** öznitelik türü kullanıcı tanımlı bir ayıklayıcısı kayıtlı olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="85873-310">The **SqlUserDefinedExtractor** attribute indicates that the type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="85873-311">Bu sınıf devralınan olamaz.</span><span class="sxs-lookup"><span data-stu-id="85873-311">This class cannot be inherited.</span></span>

<span data-ttu-id="85873-312">SqlUserDefinedExtractor Opyalanan tanımı için isteğe bağlı bir özniteliktir.</span><span class="sxs-lookup"><span data-stu-id="85873-312">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="85873-313">Opyalanan nesnesi için AtomicFileProcessing özelliği tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85873-313">It used to define AtomicFileProcessing property for the UDE object.</span></span>

* <span data-ttu-id="85873-314">bool AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="85873-314">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="85873-315">**doğru** bu ayıklayıcısı atomik giriş dosyaları (JSON, XML,...) gerektirdiğini belirtir =</span><span class="sxs-lookup"><span data-stu-id="85873-315">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="85873-316">**yanlış** bu ayıklayıcısı bölünmüş / dağıtılmış dosyalarla (CSV, SEQ,...) başa belirtir =</span><span class="sxs-lookup"><span data-stu-id="85873-316">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="85873-317">Ana Opyalanan programlamasına nesneler **giriş** ve **çıkış**.</span><span class="sxs-lookup"><span data-stu-id="85873-317">The main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="85873-318">Giriş nesnesi girdi verisi olarak numaralandırmak için kullanılan `IUnstructuredReader`.</span><span class="sxs-lookup"><span data-stu-id="85873-318">The input object is used to enumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="85873-319">Çıkış nesnesi ayıklayıcısı etkinlik sonucunda çıkış veri kümesi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85873-319">The output object is used to set output data as a result of the extractor activity.</span></span>

<span data-ttu-id="85873-320">Giriş verisi üzerinden erişilen `System.IO.Stream` ve `System.IO.StreamReader`.</span><span class="sxs-lookup"><span data-stu-id="85873-320">The input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="85873-321">Giriş sütunları numaralandırması için biz ilk giriş akışı satır ayırıcı kullanarak ayırın.</span><span class="sxs-lookup"><span data-stu-id="85873-321">For input columns enumeration, we first split the input stream by using a row delimiter.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

<span data-ttu-id="85873-322">Ardından, daha fazla giriş satır sütun bölün.</span><span class="sxs-lookup"><span data-stu-id="85873-322">Then, further split input row into column parts.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

<span data-ttu-id="85873-323">Çıktı veri kümesi için kullanırız `output.Set` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="85873-323">To set output data, we use the `output.Set` method.</span></span>

<span data-ttu-id="85873-324">Özel ayıklayıcısı yalnızca sütunlar ve tanımlanmış değerler ile çıkış çıktıları anlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="85873-324">It's important to understand that the custom extractor only outputs columns and values that are defined with the output.</span></span> <span data-ttu-id="85873-325">Yöntem çağrısının ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="85873-325">Set method call.</span></span>

```
output.Set<string>(count, part);
```

<span data-ttu-id="85873-326">Gerçek ayıklayıcısı çıkış çağırarak tetiklenir `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="85873-326">The actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="85873-327">Ayıklayıcısı örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="85873-327">Following is the extractor example:</span></span>

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
         //Read the input line by line
         foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
         {
        using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
         {
             line = streamReader.ReadToEnd().Trim();
             //Split the input by the column delimiter
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
                 // for column “user”, convert to UPPER case
                 output.Set<string>(count, part.ToUpper());

             }
             else
             {
                 // keep the rest of the columns as-is
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

<span data-ttu-id="85873-328">Bu kullanım örneği senaryosu ayıklayıcısı "guid" sütunu için GUID oluşturur ve "kullanıcı" sütundaki değerleri büyük harflere dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="85873-328">In this use-case scenario, the extractor regenerates the GUID for “guid” column and converts the values of “user” column to upper case.</span></span> <span data-ttu-id="85873-329">Özel ayıklayıcıları giriş verilerini ayrıştırma ve onu düzenleme daha karmaşık sonuçlara yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="85873-329">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="85873-330">Özel ayıklayıcısı kullanan temel U-SQL komut dosyası aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="85873-330">Following is base U-SQL script that uses a custom extractor:</span></span>

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

OUTPUT @rs0 TO @output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a><span data-ttu-id="85873-331">Kullanıcı tanımlı outputters kullanın</span><span class="sxs-lookup"><span data-stu-id="85873-331">Use user-defined outputters</span></span>
<span data-ttu-id="85873-332">Kullanıcı tanımlı outputter yerleşik U-SQL işlevselliğini genişletmek izin veren başka bir U-SQL UDO ' dir.</span><span class="sxs-lookup"><span data-stu-id="85873-332">User-defined outputter is another U-SQL UDO that allows you to extend built-in U-SQL functionality.</span></span> <span data-ttu-id="85873-333">Benzer şekilde ayıklayıcısı vardır birkaç yerleşik outputters.</span><span class="sxs-lookup"><span data-stu-id="85873-333">Similar to the extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="85873-334">*Outputters.Text()*: veri farklı kodlamaları sınırlandırılmış metin dosyasına yazar.</span><span class="sxs-lookup"><span data-stu-id="85873-334">*Outputters.Text()*: Writes data to delimited text files of different encodings.</span></span>
* <span data-ttu-id="85873-335">*Outputters.Csv()*: veri farklı kodlamaları virgülle ayrılmış değer (CSV) dosyasına yazar.</span><span class="sxs-lookup"><span data-stu-id="85873-335">*Outputters.Csv()*: Writes data to comma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="85873-336">*Outputters.Tsv()*: veri farklı kodlamaları sekmesini ayrılmış değerler (TSV) dosyasına yazar.</span><span class="sxs-lookup"><span data-stu-id="85873-336">*Outputters.Tsv()*: Writes data to tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="85873-337">Özel outputter özel tanımlanmış bir biçimde veri yazmak sağlar.</span><span class="sxs-lookup"><span data-stu-id="85873-337">Custom outputter allows you to write data in a custom defined format.</span></span> <span data-ttu-id="85873-338">Aşağıdaki görevler için yararlı olabilir:</span><span class="sxs-lookup"><span data-stu-id="85873-338">This can be useful for the following tasks:</span></span>

* <span data-ttu-id="85873-339">Veri yarı yapılandırılmış veya yapılandırılmamış dosyalara yazma.</span><span class="sxs-lookup"><span data-stu-id="85873-339">Writing data to semi-structured or unstructured files.</span></span>
* <span data-ttu-id="85873-340">Veri yazma değil Kodlamalar desteklenir.</span><span class="sxs-lookup"><span data-stu-id="85873-340">Writing data not supported encodings.</span></span>
* <span data-ttu-id="85873-341">Çıktı verilerini değiştirme veya özel öznitelikleri ekleme.</span><span class="sxs-lookup"><span data-stu-id="85873-341">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="85873-342">Kullanıcı tanımlı outputter tanımlamak için oluşturmamız gerekir `IOutputter` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="85873-342">To define user-defined outputter, we need to create the `IOutputter` interface.</span></span>

<span data-ttu-id="85873-343">Aşağıdadır temel `IOutputter` sınıfı uygulama:</span><span class="sxs-lookup"><span data-stu-id="85873-343">Following is the base `IOutputter` class implementation:</span></span>

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

<span data-ttu-id="85873-344">Sütun/satır sınırlayıcıları, kodlama ve vb. gibi outputter tüm giriş parametreleri sınıfı oluşturucuda tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="85873-344">All input parameters to the outputter, such as column/row delimiters, encoding, and so on, need to be defined in the constructor of the class.</span></span> <span data-ttu-id="85873-345">`IOutputter` Arabirimi için bir tanım da içermelidir `void Output` geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="85873-345">The `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="85873-346">Öznitelik `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` atomik dosya işleme için isteğe bağlı olarak ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="85873-346">The attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="85873-347">Daha fazla bilgi için aşağıdaki ayrıntılarına bakın.</span><span class="sxs-lookup"><span data-stu-id="85873-347">For more information, see the following details.</span></span>

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

* <span data-ttu-id="85873-348">`Output`Giriş her satır için çağrılır.</span><span class="sxs-lookup"><span data-stu-id="85873-348">`Output` is called for each input row.</span></span> <span data-ttu-id="85873-349">Döndürdüğü `IUnstructuredWriter output` satır kümesi.</span><span class="sxs-lookup"><span data-stu-id="85873-349">It returns the `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="85873-350">Oluşturucu sınıfı için kullanıcı tanımlı outputter parametreleri geçirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85873-350">The Constructor class is used to pass parameters to the user-defined outputter.</span></span>
* <span data-ttu-id="85873-351">`Close`İsteğe bağlı olarak pahalı durumunu serbest bırakmak veya son satırını zaman yazıldı belirlemek için geçersiz kılmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85873-351">`Close` is used to optionally override to release expensive state or determine when the last row was written.</span></span>

<span data-ttu-id="85873-352">**SqlUserDefinedOutputter** öznitelik türü kullanıcı tanımlı bir outputter kayıtlı olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="85873-352">**SqlUserDefinedOutputter** attribute indicates that the type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="85873-353">Bu sınıf devralınan olamaz.</span><span class="sxs-lookup"><span data-stu-id="85873-353">This class cannot be inherited.</span></span>

<span data-ttu-id="85873-354">SqlUserDefinedOutputter, kullanıcı tanımlı outputter tanımı için isteğe bağlı bir özniteliktir.</span><span class="sxs-lookup"><span data-stu-id="85873-354">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="85873-355">AtomicFileProcessing özelliği tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85873-355">It's used to define the AtomicFileProcessing property.</span></span>

* <span data-ttu-id="85873-356">bool AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="85873-356">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="85873-357">**doğru** bu outputter atomik çıktı dosyaları (JSON, XML,...) gerektirdiğini belirtir =</span><span class="sxs-lookup"><span data-stu-id="85873-357">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="85873-358">**yanlış** bu outputter bölünmüş / dağıtılmış dosyalarla (CSV, SEQ,...) başa belirtir =</span><span class="sxs-lookup"><span data-stu-id="85873-358">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="85873-359">Ana programlamasına nesneler **satır** ve **çıkış**.</span><span class="sxs-lookup"><span data-stu-id="85873-359">The main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="85873-360">**Satır** nesne çıktı verisi olarak numaralandırmak için kullanılan `IRow` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="85873-360">The **row** object is used to enumerate output data as `IRow` interface.</span></span> <span data-ttu-id="85873-361">**Çıktı** hedef dosyasına çıkış veri kümesi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85873-361">**Output** is used to set output data to the target file.</span></span>

<span data-ttu-id="85873-362">Çıktı verilerini üzerinden erişilen `IRow` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="85873-362">The output data is accessed through the `IRow` interface.</span></span> <span data-ttu-id="85873-363">Çıktı verilerini bir satır aynı anda geçirilir.</span><span class="sxs-lookup"><span data-stu-id="85873-363">Output data is passed a row at a time.</span></span>

<span data-ttu-id="85873-364">Değerlerini ayrı ayrı IRow arabiriminin Get yöntemini çağırarak numaralandırılmıştır:</span><span class="sxs-lookup"><span data-stu-id="85873-364">The individual values are enumerated by calling the Get method of the IRow interface:</span></span>

```
row.Get<string>("column_name")
```

<span data-ttu-id="85873-365">Tek tek sütun adları çağırarak belirlenebilir `row.Schema`:</span><span class="sxs-lookup"><span data-stu-id="85873-365">Individual column names can be determined by calling `row.Schema`:</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="85873-366">Bu yaklaşım, herhangi bir meta veri şema için esnek bir outputter oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="85873-366">This approach enables you to build a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="85873-367">Çıktı verilerini kullanarak dosyaya yazılan `System.IO.StreamWriter`.</span><span class="sxs-lookup"><span data-stu-id="85873-367">The output data is written to file by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="85873-368">Akış parametre kümesine `output.BaseStrea` parçası olarak `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="85873-368">The stream parameter is set to `output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="85873-369">Dosyaya veri arabelleği sonra her bir satır yineleme temizlemek önemli olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="85873-369">Note that it's important to flush the data buffer to the file after each row iteration.</span></span> <span data-ttu-id="85873-370">Ayrıca, `StreamWriter` nesne özniteliğiyle etkin atılabilir (varsayılan) ve birlikte kullanılmalıdır **kullanarak** anahtar sözcüğü:</span><span class="sxs-lookup"><span data-stu-id="85873-370">In addition, the `StreamWriter` object must be used with the Disposable attribute enabled (default) and with the **using** keyword:</span></span>

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

<span data-ttu-id="85873-371">Aksi takdirde Flush() yöntemini her yinelemeden sonra açıkça çağırın.</span><span class="sxs-lookup"><span data-stu-id="85873-371">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="85873-372">Bu aşağıdaki örnekte gösteriyoruz.</span><span class="sxs-lookup"><span data-stu-id="85873-372">We show this in the following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="85873-373">Üstbilgiler ve altbilgiler kullanıcı tanımlı outputter için ayarlama</span><span class="sxs-lookup"><span data-stu-id="85873-373">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="85873-374">Üstbilgi ayarlamak için tek yineleme yürütme akışı kullanın.</span><span class="sxs-lookup"><span data-stu-id="85873-374">To set a header, use single iteration execution flow.</span></span>

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

<span data-ttu-id="85873-375">İlk kodda `if (isHeaderRow)` blok yalnızca bir kez gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="85873-375">The code in the first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="85873-376">Altbilgi için örneğine başvuru kullanın `System.IO.Stream` nesne (`output.BaseStream`).</span><span class="sxs-lookup"><span data-stu-id="85873-376">For the footer, use the reference to the instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="85873-377">Altbilgi çağrısının yönteminde yazma `IOutputter` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="85873-377">Write the footer in the Close() method of the `IOutputter` interface.</span></span>  <span data-ttu-id="85873-378">(Daha fazla bilgi için aşağıdaki örneğe bakın.)</span><span class="sxs-lookup"><span data-stu-id="85873-378">(For more information, see the following example.)</span></span>

<span data-ttu-id="85873-379">Kullanıcı tanımlı bir outputter örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="85873-379">Following is an example of a user-defined outputter:</span></span>

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

    // The Close method is used to write the footer to the file. It's executed only once, after all rows
    public override void Close().
    {
    //Reference to IO.Stream object - g_writer
    StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
    streamWriter.Write("</table>");
    streamWriter.Flush();
    streamWriter.Close();
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
    System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

    // Metadata schema initialization to enumerate column names
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
        // Data type enumeration--required to match the distinct list of types from OUTPUT statement
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
    // Reference to the instance of the IO.Stream object for footer generation
    g_writer = output.BaseStream;
    streamWriter.Flush();
    }
}

// Define the factory classes
public static class Factory
{
    public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    return new HTMLOutputter(isHeader, encoding);
    }
}
```

<span data-ttu-id="85873-380">Ve U-SQL temel betiği:</span><span class="sxs-lookup"><span data-stu-id="85873-380">And U-SQL base script:</span></span>

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
    TO @output_file 
    USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="85873-381">Tablo verisi bir HTML dosyası oluşturur bir HTML outputter budur.</span><span class="sxs-lookup"><span data-stu-id="85873-381">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="85873-382">U-SQL temel betikten outputter çağırın</span><span class="sxs-lookup"><span data-stu-id="85873-382">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="85873-383">Özel outputter temel U-SQL komut dosyasından çağırmak için outputter nesne yeni bir örneğini oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="85873-383">To call a custom outputter from the base U-SQL script, the new instance of the outputter object has to be created.</span></span>

```sql
OUTPUT @rs0 TO @output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="85873-384">Nesnesinin bir örneği temel komut dosyasında oluşturmamak için size bir işlev sarmalayıcı bizim önceki örnekte gösterildiği gibi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="85873-384">To avoid creating an instance of the object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

```c#
        // Define the factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

<span data-ttu-id="85873-385">Bu durumda, özgün çağrısı aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="85873-385">In this case, the original call looks like the following:</span></span>

```
OUTPUT @rs0 
TO @output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="85873-386">Kullanıcı tanımlı işlemcilerini kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="85873-386">Use user-defined processors</span></span>
<span data-ttu-id="85873-387">Kullanıcı tanımlı işlemci veya UDP, U-SQL programlama özelliklerine uygulayarak gelen satırların işlemenize olanak sağlayan UDO türüdür.</span><span class="sxs-lookup"><span data-stu-id="85873-387">User-defined processor, or UDP, is a type of U-SQL UDO that enables you to process the incoming rows by applying programmability features.</span></span> <span data-ttu-id="85873-388">UDP sütunu birleştirme, değerleri değiştirmek ve gerekirse, yeni sütun eklemek etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="85873-388">UDP enables you to combine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="85873-389">Temel olarak, gerekli veri öğeleri oluşturmak için bir satır kümesi işlem yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="85873-389">Basically, it helps to process a rowset to produce required data elements.</span></span>

<span data-ttu-id="85873-390">Bir UDP tanımlamak için oluşturmamız gerekir bir `IProcessor` ile arabirim `SqlUserDefinedProcessor` için UDP isteğe bağlı öznitelik.</span><span class="sxs-lookup"><span data-stu-id="85873-390">To define a UDP, we need to create an `IProcessor` interface with the `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="85873-391">Bu arabirim tanımı içermelidir `IRow` arabirimi satır kümesi geçersiz kılmak, aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="85873-391">This interface should contain the definition for the `IRow` interface rowset override, as shown in the following example:</span></span>

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

<span data-ttu-id="85873-392">**SqlUserDefinedProcessor** türü kullanıcı tanımlı bir işlemci olarak kayıtlı olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="85873-392">**SqlUserDefinedProcessor** indicates that the type should be registered as a user-defined processor.</span></span> <span data-ttu-id="85873-393">Bu sınıf devralınan olamaz.</span><span class="sxs-lookup"><span data-stu-id="85873-393">This class cannot be inherited.</span></span>

<span data-ttu-id="85873-394">SqlUserDefinedProcessor özniteliği **isteğe bağlı** UDP tanımı.</span><span class="sxs-lookup"><span data-stu-id="85873-394">The SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="85873-395">Ana programlamasına nesneler **giriş** ve **çıkış**.</span><span class="sxs-lookup"><span data-stu-id="85873-395">The main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="85873-396">Giriş nesnesi giriş sütunları ve çıkış numaralandırır ve çıktı verilerini işlemci etkinliğinin sonucu olarak ayarlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85873-396">The input object is used to enumerate input columns and output, and to set output data as a result of the processor activity.</span></span>

<span data-ttu-id="85873-397">Giriş sütunları numaralandırması için kullandığımız `input.Get` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="85873-397">For input columns enumeration, we use the `input.Get` method.</span></span>

```
string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="85873-398">Parametresi için `input.Get` yöntemdir parçası olarak geçirilen bir sütun `PRODUCE` yan tümcesi `PROCESS` U-SQL temel komut dosyası ifadesi.</span><span class="sxs-lookup"><span data-stu-id="85873-398">The parameter for `input.Get` method is a column that's passed as part of the `PRODUCE` clause of the `PROCESS` statement of the U-SQL base script.</span></span> <span data-ttu-id="85873-399">Burada doğru veri türünü kullanmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="85873-399">We need to use the correct data type here.</span></span>

<span data-ttu-id="85873-400">Çıkış için kullan `output.Set` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="85873-400">For output, use the `output.Set` method.</span></span>

<span data-ttu-id="85873-401">Bu özel üretici yalnızca çıkarır sütunlar ve ile tanımlanmış değerler dikkate almak önemlidir `output.Set` yöntem çağrısı.</span><span class="sxs-lookup"><span data-stu-id="85873-401">It's important to note that custom producer only outputs columns and values that are defined with the `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="85873-402">Gerçek işlemci çıktı çağırarak tetiklenir `return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="85873-402">The actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="85873-403">Bir işlemci örneği aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="85873-403">Following is a processor example:</span></span>

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

<span data-ttu-id="85873-404">Bu kullanım örneği senaryosu, var olan sütunlar--bu durumda, "kullanıcı" için büyük harf ve "des" birleştirerek "full_description" adlı yeni bir sütun işlemci oluşturuyor.</span><span class="sxs-lookup"><span data-stu-id="85873-404">In this use-case scenario, the processor is generating a new column called “full_description” by combining the existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="85873-405">Ayrıca, bir GUID oluşturur ve özgün ve yeni GUID değerleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="85873-405">It also regenerates a GUID and returns the original and new GUID values.</span></span>

<span data-ttu-id="85873-406">Önceki örnekte görebildiğiniz gibi C# sırasında yöntemi çağırabilirsiniz `output.Set` yöntem çağrısı.</span><span class="sxs-lookup"><span data-stu-id="85873-406">As you can see from the previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="85873-407">Özel bir işlemci kullanan temel U-SQL komut dosyası örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="85873-407">Following is an example of base U-SQL script that uses a custom processor:</span></span>

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

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a><span data-ttu-id="85873-408">Kullanıcı tanımlı appliers kullanın</span><span class="sxs-lookup"><span data-stu-id="85873-408">Use user-defined appliers</span></span>
<span data-ttu-id="85873-409">U-SQL kullanıcı tanımlı bir applier, özel bir C# işlev Sorguda dış tablo ifadesi tarafından döndürülen her satır için çağrılacak sağlar.</span><span class="sxs-lookup"><span data-stu-id="85873-409">A U-SQL user-defined applier enables you to invoke a custom C# function for each row that's returned by the outer table expression of a query.</span></span> <span data-ttu-id="85873-410">Sağ giriş sol girdisinden her satır için hesaplanan ve üretilen satırları son çıktı için birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="85873-410">The right input is evaluated for each row from the left input, and the rows that are produced are combined for the final output.</span></span> <span data-ttu-id="85873-411">Sol ve sağ giriş sütunları kümesi birleşimi UYGULA operatör tarafından üretilen sütun listesi var.</span><span class="sxs-lookup"><span data-stu-id="85873-411">The list of columns that are produced by the APPLY operator are the combination of the set of columns in the left and the right input.</span></span>

<span data-ttu-id="85873-412">Kullanıcı tanımlı applier USQL seçin ifadenin bir parçası çağrılır.</span><span class="sxs-lookup"><span data-stu-id="85873-412">User-defined applier is being invoked as part of the USQL SELECT expression.</span></span>

<span data-ttu-id="85873-413">Kullanıcı tanımlı applier tipik çağrısı aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="85873-413">The typical call to the user-defined applier looks like the following:</span></span>

```
SELECT …
FROM …
CROSS APPLYis used to pass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="85873-414">Bir SELECT ifadesinde appliers kullanma hakkında daha fazla bilgi için bkz: [seçin, U-SQL seçme ARASI uygulamak ve OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span><span class="sxs-lookup"><span data-stu-id="85873-414">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="85873-415">Kullanıcı tanımlı applier temel sınıf tanımı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="85873-415">The user-defined applier base class definition is as follows:</span></span>

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

<span data-ttu-id="85873-416">Kullanıcı tanımlı bir applier tanımlamak için oluşturmamız gerekir `IApplier` ile Arabirimi [`SqlUserDefinedApplier`] özniteliği için kullanıcı tanımlı applier tanım isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="85873-416">To define a user-defined applier, we need to create the `IApplier` interface with the [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

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

* <span data-ttu-id="85873-417">Uygulama dış tablonun her satırı için çağrılır.</span><span class="sxs-lookup"><span data-stu-id="85873-417">Apply is called for each row of the outer table.</span></span> <span data-ttu-id="85873-418">Döndürdüğü `IUpdatableRow` satır kümesi çıktı.</span><span class="sxs-lookup"><span data-stu-id="85873-418">It returns the `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="85873-419">Oluşturucu sınıfı için kullanıcı tanımlı applier parametreleri geçirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85873-419">The Constructor class is used to pass parameters to the user-defined applier.</span></span>

<span data-ttu-id="85873-420">**SqlUserDefinedApplier** türü kullanıcı tanımlı bir applier kayıtlı olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="85873-420">**SqlUserDefinedApplier** indicates that the type should be registered as a user-defined applier.</span></span> <span data-ttu-id="85873-421">Bu sınıf devralınan olamaz.</span><span class="sxs-lookup"><span data-stu-id="85873-421">This class cannot be inherited.</span></span>

<span data-ttu-id="85873-422">**SqlUserDefinedApplier** olan **isteğe bağlı** kullanıcı tanımlı applier tanımı.</span><span class="sxs-lookup"><span data-stu-id="85873-422">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="85873-423">Ana programlamasına nesneleri aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="85873-423">The main programmability objects are as follows:</span></span>

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="85873-424">Giriş satır kümeleri olarak geçirilir `IRow` giriş.</span><span class="sxs-lookup"><span data-stu-id="85873-424">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="85873-425">Çıktı satırları olarak oluşturulan `IUpdatableRow` çıkış arabirimi.</span><span class="sxs-lookup"><span data-stu-id="85873-425">The output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="85873-426">Tek tek sütun adları çağırarak belirlenebilir `IRow` şema yöntemi.</span><span class="sxs-lookup"><span data-stu-id="85873-426">Individual column names can be determined by calling the `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="85873-427">Gelen gerçek veri değerleri almak için `IRow`, Get() yöntemi kullanırız `IRow` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="85873-427">To get the actual data values from the incoming `IRow`, we use the Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="85873-428">Veya şema sütun adı kullanırız:</span><span class="sxs-lookup"><span data-stu-id="85873-428">Or we use the schema column name:</span></span>

```
row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="85873-429">Çıkış değerleri ile ayarlanmalıdır `IUpdatableRow` çıktı:</span><span class="sxs-lookup"><span data-stu-id="85873-429">The output values must be set with `IUpdatableRow` output:</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="85873-430">Özel appliers sütunlar ve ile tanımlanmış değerler yalnızca çıktı anlamak önemlidir `output.Set` yöntem çağrısı.</span><span class="sxs-lookup"><span data-stu-id="85873-430">It is important to understand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="85873-431">Gerçek çıkış çağırarak tetiklenir `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="85873-431">The actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="85873-432">Kullanıcı tanımlı applier parametreleri oluşturucuya geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="85873-432">The user-defined applier parameters can be passed to the constructor.</span></span> <span data-ttu-id="85873-433">Applier temel U-SQL betiği applier çağrısında sırasında tanımlanması gerektiğini sütunlar değişken sayıda geri dönebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85873-433">Applier can return a variable number of columns that need to be defined during the applier call in base U-SQL Script.</span></span>

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="85873-434">Kullanıcı tanımlı applier örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="85873-434">Here is the user-defined applier example:</span></span>

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

<span data-ttu-id="85873-435">Bu kullanıcı tarafından tanımlanan applier için temel U-SQL betiği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="85873-435">Following is the base U-SQL script for this user-defined applier:</span></span>

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

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="85873-436">Bu kullanım örnek senaryoda, kullanıcı tanımlı applier araba yakıt özellikleri için virgülle ayrılmış değer ayrıştırıcı gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="85873-436">In this use case scenario, user-defined applier acts as a comma-delimited value parser for the car fleet properties.</span></span> <span data-ttu-id="85873-437">Giriş dosyası satırları şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="85873-437">The input file rows look like the following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="85873-438">Normal bir sekmeyle ayrılmış TSV dosya marka ve model gibi araba özellikleri içeren özellikleri sütunu var.</span><span class="sxs-lookup"><span data-stu-id="85873-438">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="85873-439">Bu özellikler Ayrıştırılmış tablo sütunları için gerekir.</span><span class="sxs-lookup"><span data-stu-id="85873-439">Those properties must be parsed to the table columns.</span></span> <span data-ttu-id="85873-440">Sağlanan applier geçirilen parametresine bağlı olarak sonuç kümesinde özellikleri sayısını dinamik oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="85873-440">The applier that's provided also enables you to generate a dynamic number of properties in the result rowset, based on the parameter that's passed.</span></span> <span data-ttu-id="85873-441">Tüm özellikleri veya özellikler yalnızca belirli bir grup oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85873-441">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="85873-442">Kullanıcı tanımlı applier applier nesnesinin yeni bir örneğini çağrılabilir:</span><span class="sxs-lookup"><span data-stu-id="85873-442">The user-defined applier can be called as a new instance of applier object:</span></span>

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="85873-443">Veya bir sarmalayıcı fabrika yöntemi çağrıldı:</span><span class="sxs-lookup"><span data-stu-id="85873-443">Or with the invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="85873-444">Kullanıcı tanımlı combiners kullanın</span><span class="sxs-lookup"><span data-stu-id="85873-444">Use user-defined combiners</span></span>
<span data-ttu-id="85873-445">Kullanıcı tanımlı Birleştirici veya UDC, sol ve sağ satır kümeleri özel mantığına göre satırları birleştirmek sağlar.</span><span class="sxs-lookup"><span data-stu-id="85873-445">User-defined combiner, or UDC, enables you to combine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="85873-446">Kullanıcı tanımlı birleştirici birleştirme ifadesiyle kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85873-446">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="85873-447">Bir Birleştirici hem giriş satır kümeleri, gruplandırma sütunlarında, beklenen sonucu şema ve ek bilgiler hakkında gerekli bilgileri sağlar birleştirme ifade ile çağrılan.</span><span class="sxs-lookup"><span data-stu-id="85873-447">A combiner is being invoked with the COMBINE expression that provides the necessary information about both the input rowsets, the grouping columns, the expected result schema, and additional information.</span></span>

<span data-ttu-id="85873-448">Temel bir U-SQL komut dosyasında bir Birleştirici çağırmak için size aşağıdaki sözdizimini kullanın:</span><span class="sxs-lookup"><span data-stu-id="85873-448">To call a combiner in a base U-SQL script, we use the following syntax:</span></span>

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

<span data-ttu-id="85873-449">Daha fazla bilgi için bkz: [BİRLEŞTİRMEK ifade (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span><span class="sxs-lookup"><span data-stu-id="85873-449">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="85873-450">Kullanıcı tanımlı bir Birleştirici tanımlamak için oluşturmamız gerekir `ICombiner` ile Arabirimi [`SqlUserDefinedCombiner`] özniteliği için bir kullanıcı tarafından tanımlanan birleştirici tanım isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="85873-450">To define a user-defined combiner, we need to create the `ICombiner` interface with the [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="85873-451">Temel `ICombiner` sınıf tanımı:</span><span class="sxs-lookup"><span data-stu-id="85873-451">Base `ICombiner` class definition:</span></span>

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

<span data-ttu-id="85873-452">Özel uygulanması bir `ICombiner` arabirim tanımı içermelidir bir `IEnumerable<IRow>` geçersiz kılma birleştirin.</span><span class="sxs-lookup"><span data-stu-id="85873-452">The custom implementation of an `ICombiner` interface should contain the definition for an `IEnumerable<IRow>` Combine override.</span></span>

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

<span data-ttu-id="85873-453">**SqlUserDefinedCombiner** öznitelik türü kullanıcı tanımlı bir Birleştirici kayıtlı olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="85873-453">The **SqlUserDefinedCombiner** attribute indicates that the type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="85873-454">Bu sınıf devralınan olamaz.</span><span class="sxs-lookup"><span data-stu-id="85873-454">This class cannot be inherited.</span></span>

<span data-ttu-id="85873-455">**SqlUserDefinedCombiner** Birleştirici modu özelliği tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85873-455">**SqlUserDefinedCombiner** is used to define the Combiner mode property.</span></span> <span data-ttu-id="85873-456">Bir kullanıcı tarafından tanımlanan birleştirici tanımı için isteğe bağlı bir özniteliktir.</span><span class="sxs-lookup"><span data-stu-id="85873-456">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="85873-457">CombinerMode modu</span><span class="sxs-lookup"><span data-stu-id="85873-457">CombinerMode     Mode</span></span>

<span data-ttu-id="85873-458">CombinerMode enum, şu değerleri alabilir:</span><span class="sxs-lookup"><span data-stu-id="85873-458">CombinerMode enum can take the following values:</span></span>

* <span data-ttu-id="85873-459">Tam (0) her çıktı satır olası tüm giriş satırları sol ve sağ ile aynı anahtar değerine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="85873-459">Full  (0) Every output row potentially depends on all the input rows from left and right       with the same key value.</span></span>

* <span data-ttu-id="85873-460">Sol soldan (ve büyük olasılıkla tüm satırların aynı anahtar değeriyle sağdan) tek bir giriş satır her çıktı satır bağlıdır (1).</span><span class="sxs-lookup"><span data-stu-id="85873-460">Left  (1) Every output row depends on a single input row from the left (and potentially all rows       from the right with the same key value).</span></span>

* <span data-ttu-id="85873-461">Sağa (2) sağa (ve büyük olasılıkla tüm satırların aynı anahtar değeriyle soldan) tek bir giriş satır her çıktı satır bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="85873-461">Right (2)     Every output row depends on a single input row from the right (and potentially all rows       from the left with the same key value).</span></span>

* <span data-ttu-id="85873-462">İç (3) tek bir giriş satır sol ve sağda aynı değere sahip her çıktı satır bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="85873-462">Inner (3) Every output row depends on a single input row from left and right with the same value.</span></span>

<span data-ttu-id="85873-463">Örnek: [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="85873-463">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="85873-464">Ana programlamasına nesneler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="85873-464">The main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="85873-465">Giriş satır kümeleri olarak geçirilir **sol** ve **sağ** `IRowset` arabirimi türü.</span><span class="sxs-lookup"><span data-stu-id="85873-465">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="85873-466">Her iki satır kümeleri işleme için numaralandırılmış gerekir.</span><span class="sxs-lookup"><span data-stu-id="85873-466">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="85873-467">Böylece biz numaralandırır ve gerekirse, önbelleğe zorunda kez, her bir arabirime yalnızca sıralayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85873-467">You can only enumerate each interface once, so we have to enumerate and cache it if necessary.</span></span>

<span data-ttu-id="85873-468">Amacıyla önbelleğe alma işlemi için bir liste oluşturabilir\<T\> tür bellek yapısı sonuç olarak bir LINQ Sorgu yürütme, özellikle listesi <`IRow`>.</span><span class="sxs-lookup"><span data-stu-id="85873-468">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="85873-469">Anonim veri türü, numaralandırma sırasında da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="85873-469">The anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="85873-470">Bkz: [LINQ sorgularını (C#) giriş](https://msdn.microsoft.com/library/bb397906.aspx) LINQ sorguları hakkında daha fazla bilgi ve [IEnumerable\<T\> arabirimi](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) IEnumerablehakkındadahafazlabilgiiçin\<T\> arabirimi.</span><span class="sxs-lookup"><span data-stu-id="85873-470">See [Introduction to LINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="85873-471">Gelen gerçek veri değerleri almak için `IRowset`, Get() yöntemi kullanırız `IRow` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="85873-471">To get the actual data values from the incoming `IRowset`, we use the Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="85873-472">Tek tek sütun adları çağırarak belirlenebilir `IRow` şema yöntemi.</span><span class="sxs-lookup"><span data-stu-id="85873-472">Individual column names can be determined by calling the `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="85873-473">Veya şema sütun adı kullanarak:</span><span class="sxs-lookup"><span data-stu-id="85873-473">Or by using the schema column name:</span></span>

```
c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="85873-474">LINQ ile genel numaralandırma aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="85873-474">The general enumeration with LINQ looks like the following:</span></span>

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="85873-475">Her iki satır kümeleri numaralandırma sonra biz tüm satırları döngü alınacaktır.</span><span class="sxs-lookup"><span data-stu-id="85873-475">After enumerating both rowsets, we are going to loop through all rows.</span></span> <span data-ttu-id="85873-476">Sol satır kümesindeki her satır için biz bizim Birleştirici koşulu karşılıyor tüm satırları bulmak için adımıdır.</span><span class="sxs-lookup"><span data-stu-id="85873-476">For each row in the left rowset, we are going to find all rows that satisfy the condition of our combiner.</span></span>

<span data-ttu-id="85873-477">Çıkış değerleri ile ayarlanmalıdır `IUpdatableRow` çıktı.</span><span class="sxs-lookup"><span data-stu-id="85873-477">The output values must be set with `IUpdatableRow` output.</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="85873-478">Arama için gerçek çıktı tetiklediği `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="85873-478">The actual output is triggered by calling to `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="85873-479">Birleştirici örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="85873-479">Following is a combiner example:</span></span>

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

<span data-ttu-id="85873-480">Bu kullanım örneği senaryosu biz için satıcıya bir analiz raporu oluşturmakta olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="85873-480">In this use-case scenario, we are building an analytics report for the retailer.</span></span> <span data-ttu-id="85873-481">Birden fazla $20.000 maliyet ve, belirli bir zaman çerçevesi içinde normal perakende üzerinden daha hızlı Web sitesi aracılığıyla satmak tüm ürünleri bulmak için belirtilir.</span><span class="sxs-lookup"><span data-stu-id="85873-481">The goal is to find all products that cost more than $20,000 and that sell through the website faster than through the regular retailer within a certain time frame.</span></span>

<span data-ttu-id="85873-482">Burada, temel U-SQL betiği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="85873-482">Here is the base U-SQL script.</span></span> <span data-ttu-id="85873-483">Normal bir birleştirme ve bir Birleştirici arasında mantığı karşılaştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="85873-483">You can compare the logic between a regular JOIN and a combiner:</span></span>

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

OUTPUT @rs1 TO @output_file1 USING Outputters.Tsv();
OUTPUT @rs2 TO @output_file2 USING Outputters.Tsv();
```

<span data-ttu-id="85873-484">Kullanıcı tanımlı bir Birleştirici applier nesnesinin yeni bir örneğini çağrılabilir:</span><span class="sxs-lookup"><span data-stu-id="85873-484">A user-defined combiner can be called as a new instance of the applier object:</span></span>

```
USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="85873-485">Veya bir sarmalayıcı fabrika yöntemi çağrıldı:</span><span class="sxs-lookup"><span data-stu-id="85873-485">Or with the invocation of a wrapper factory method:</span></span>

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="85873-486">Kullanıcı tanımlı reducers kullanın</span><span class="sxs-lookup"><span data-stu-id="85873-486">Use user-defined reducers</span></span>

<span data-ttu-id="85873-487">U-SQL özel satır kümesi reducers C# ile kullanıcı tanımlı işleci Genişletilebilirlik Çerçevesi'ni kullanıp IReducer arabirimi uygulama yazmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="85873-487">U-SQL enables you to write custom rowset reducers in C# by using the user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="85873-488">Kullanıcı tanımlı reducer veya UDR, gereksiz satırları (içe aktarma) veri ayıklama sırasında ortadan kaldırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="85873-488">User-defined reducer, or UDR, can be used to eliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="85873-489">Ayrıca, yönetmek ve satırları ve sütunları değerlendirmek için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="85873-489">It also can be used to manipulate and evaluate rows and columns.</span></span> <span data-ttu-id="85873-490">Programlanabilirlik mantığına göre onu da hangi satırların ayıklanması gereken tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85873-490">Based on programmability logic, it can also define which rows need to be extracted.</span></span>

<span data-ttu-id="85873-491">UDR sınıf tanımlamak için oluşturmamız gerekir bir `IReducer` isteğe bağlı bir arabirimiyle `SqlUserDefinedReducer` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="85873-491">To define a UDR class, we need to create an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="85873-492">Bu sınıf arabirimi için bir tanım içermelidir `IEnumerable` arabirimi satır kümesi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="85873-492">This class interface should contain a definition for the `IEnumerable` interface rowset override.</span></span>

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

<span data-ttu-id="85873-493">**SqlUserDefinedReducer** öznitelik türü kullanıcı tanımlı bir reducer kayıtlı olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="85873-493">The **SqlUserDefinedReducer** attribute indicates that the type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="85873-494">Bu sınıf devralınan olamaz.</span><span class="sxs-lookup"><span data-stu-id="85873-494">This class cannot be inherited.</span></span>
<span data-ttu-id="85873-495">**SqlUserDefinedReducer** kullanıcı tanımlı reducer tanımı için isteğe bağlı bir özniteliktir.</span><span class="sxs-lookup"><span data-stu-id="85873-495">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="85873-496">IsRecursive özelliği tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85873-496">It's used to define IsRecursive property.</span></span>

* <span data-ttu-id="85873-497">bool IsRecursive</span><span class="sxs-lookup"><span data-stu-id="85873-497">bool     IsRecursive</span></span>    
* <span data-ttu-id="85873-498">**doğru** bu Reducer ıdempotent olup olmadığını gösterir =</span><span class="sxs-lookup"><span data-stu-id="85873-498">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="85873-499">Ana programlamasına nesneler **giriş** ve **çıkış**.</span><span class="sxs-lookup"><span data-stu-id="85873-499">The main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="85873-500">Giriş nesnesi giriş satırları numaralandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85873-500">The input object is used to enumerate input rows.</span></span> <span data-ttu-id="85873-501">Çıkış, etkinlik azaltma sonucunda çıktı satırları ayarlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85873-501">Output is used to set output rows as a result of reducing activity.</span></span>

<span data-ttu-id="85873-502">Giriş satırları numaralandırması için kullandığımız `Row.Get` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="85873-502">For input rows enumeration, we use the `Row.Get` method.</span></span>

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

<span data-ttu-id="85873-503">Parametresi için `Row.Get` yöntemdir parçası olarak geçirilen bir sütun `PRODUCE` sınıfının `REDUCE` U-SQL temel komut dosyası ifadesi.</span><span class="sxs-lookup"><span data-stu-id="85873-503">The parameter for the `Row.Get` method is a column that's passed as part of the `PRODUCE` class of the `REDUCE` statement of the U-SQL base script.</span></span> <span data-ttu-id="85873-504">Biz de doğru veri türünde burada kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="85873-504">We need to use the correct data type here as well.</span></span>

<span data-ttu-id="85873-505">Çıkış için kullan `output.Set` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="85873-505">For output, use the `output.Set` method.</span></span>

<span data-ttu-id="85873-506">Bu özel reducer yalnızca ile tanımlanmış değerleri çıkarır anlamak önemlidir `output.Set` yöntem çağrısı.</span><span class="sxs-lookup"><span data-stu-id="85873-506">It is important to understand that custom reducer only outputs values that are defined with the `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="85873-507">Gerçek reducer çıkış çağırarak tetiklenir `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="85873-507">The actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="85873-508">Reducer örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="85873-508">Following is a reducer example:</span></span>

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

<span data-ttu-id="85873-509">Bu kullanım örneği senaryosu reducer boş kullanıcı adı satırlarla atlıyor.</span><span class="sxs-lookup"><span data-stu-id="85873-509">In this use-case scenario, the reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="85873-510">Her satır kümesinde için gereken her sütun okur, ardından, kullanıcı adının uzunluğu değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="85873-510">For each row in rowset, it reads each required column, then evaluates the length of the user name.</span></span> <span data-ttu-id="85873-511">Kullanıcı adı değer uzunluğu 0'dan ise gerçek satır çıkarır.</span><span class="sxs-lookup"><span data-stu-id="85873-511">It outputs the actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="85873-512">Özel reducer kullanan temel U-SQL komut dosyası aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="85873-512">Following is base U-SQL script that uses a custom reducer:</span></span>

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
    TO @output_file 
    USING Outputters.Text();
```
