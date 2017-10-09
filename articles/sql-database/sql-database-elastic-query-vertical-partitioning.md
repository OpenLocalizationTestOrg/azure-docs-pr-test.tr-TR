---
title: "Bulut üzerinden aaaQuery veritabanları farklı şemasıyla | Microsoft Docs"
description: "nasıl tooset dikey bölümleri veritabanları arası sorguları ayarlama"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 84c261f2-9edc-42f4-988c-cf2f251f5eff
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 1134e2e608128b7a9cac47ff35a22a11e6e5bc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a><span data-ttu-id="5a3e6-103">Bulut veritabanları farklı şemaları (Önizleme) ile sorgulama</span><span class="sxs-lookup"><span data-stu-id="5a3e6-103">Query across cloud databases with different schemas (preview)</span></span>
![Farklı veritabanı tablolarında sorgulama][1]

<span data-ttu-id="5a3e6-105">Veritabanlarını dikey olarak bölümlenmiş tabloları kümesi farklı farklı veritabanlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-105">Vertically-partitioned databases use different sets of tables on different databases.</span></span> <span data-ttu-id="5a3e6-106">Bu hello şema farklı veritabanlarında farklı olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-106">That means that hello schema is different on different databases.</span></span> <span data-ttu-id="5a3e6-107">Örneğin, tüm hesap ilişkili tabloları ikinci bir veritabanı üzerinde çalışırken tüm tablolar için stok bir veritabanında ' dir.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5a3e6-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5a3e6-108">Prerequisites</span></span>
* <span data-ttu-id="5a3e6-109">Merhaba kullanıcı ALTER ANY dış veri KAYNAĞINA iznine sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-109">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="5a3e6-110">Bu izni hello ALTER DATABASE iznine dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-110">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="5a3e6-111">ALTER ANY dış veri kaynağı, veri kaynağı arka plandaki gerekli toorefer toohello izinlerdir.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="5a3e6-112">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="5a3e6-112">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="5a3e6-113">Farklı yatay bölümleme bu DDL deyimleri parça eşlemesiyle hello esnek veritabanı istemci kitaplığı aracılığıyla veri katmanı tanımlama güvenmeyin.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through hello elastic database client library.</span></span>
>

1. [<span data-ttu-id="5a3e6-114">ANA ANAHTAR OLUŞTURMA</span><span class="sxs-lookup"><span data-stu-id="5a3e6-114">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="5a3e6-115">VERİTABANI KAPSAMLI OLUŞTURMAK KİMLİK BİLGİSİ</span><span class="sxs-lookup"><span data-stu-id="5a3e6-115">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="5a3e6-116">DIŞ VERİ KAYNAĞI OLUŞTURUN</span><span class="sxs-lookup"><span data-stu-id="5a3e6-116">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="5a3e6-117">DIŞ TABLO OLUŞTURMA</span><span class="sxs-lookup"><span data-stu-id="5a3e6-117">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="5a3e6-118">Kapsamlı veritabanı ana anahtarı ve kimlik bilgileri oluşturun</span><span class="sxs-lookup"><span data-stu-id="5a3e6-118">Create database scoped master key and credentials</span></span>
<span data-ttu-id="5a3e6-119">Merhaba kimlik bilgisi hello esnek sorgu tooconnect tooyour Uzak veritabanı tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-119">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="5a3e6-120">Bu hello olun `<username>` içermez **"@servername"** soneki.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-120">Ensure that hello `<username>` does not include any **"@servername"** suffix.</span></span> 
>

## <a name="create-external-data-sources"></a><span data-ttu-id="5a3e6-121">Dış veri kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="5a3e6-121">Create external data sources</span></span>
<span data-ttu-id="5a3e6-122">Sözdizimi:</span><span class="sxs-lookup"><span data-stu-id="5a3e6-122">Syntax:</span></span>

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> <span data-ttu-id="5a3e6-123">Merhaba tür parametresi çok ayarlanmalıdır**RDBMS**.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-123">hello TYPE parameter must be set too**RDBMS**.</span></span> 
>

### <a name="example"></a><span data-ttu-id="5a3e6-124">Örnek</span><span class="sxs-lookup"><span data-stu-id="5a3e6-124">Example</span></span>
<span data-ttu-id="5a3e6-125">Merhaba aşağıdaki örnek hello CREATE deyimi dış veri kaynakları için hello kullanımını göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-125">hello following example illustrates hello use of hello CREATE statement for external data sources.</span></span> 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

<span data-ttu-id="5a3e6-126">Geçerli dış veri kaynakları tooretrieve hello listesi:</span><span class="sxs-lookup"><span data-stu-id="5a3e6-126">tooretrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a><span data-ttu-id="5a3e6-127">Dış tablolar</span><span class="sxs-lookup"><span data-stu-id="5a3e6-127">External Tables</span></span>
<span data-ttu-id="5a3e6-128">Sözdizimi:</span><span class="sxs-lookup"><span data-stu-id="5a3e6-128">Syntax:</span></span>

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a><span data-ttu-id="5a3e6-129">Örnek</span><span class="sxs-lookup"><span data-stu-id="5a3e6-129">Example</span></span>
    CREATE EXTERNAL TABLE [dbo].[customer]( 
        [c_id] int NOT NULL, 
        [c_firstname] nvarchar(256) NULL, 
        [c_lastname] nvarchar(256) NOT NULL, 
        [street] nvarchar(256) NOT NULL, 
        [city] nvarchar(256) NOT NULL, 
        [state] nvarchar(20) NULL, 
        [country] nvarchar(50) NOT NULL, 
    ) 
    WITH 
    ( 
           DATA_SOURCE = RemoteReferenceData 
    ); 

<span data-ttu-id="5a3e6-130">Aşağıdaki örnek hello nasıl tooretrieve hello hello geçerli veritabanından dış tablolar listesini gösterir:</span><span class="sxs-lookup"><span data-stu-id="5a3e6-130">hello following example shows how tooretrieve hello list of external tables from hello current database:</span></span> 

    select * from sys.external_tables; 

### <a name="remarks"></a><span data-ttu-id="5a3e6-131">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="5a3e6-131">Remarks</span></span>
<span data-ttu-id="5a3e6-132">Esnek sorgu türü RDBMS dış veri kaynakları kullanan hello varolan dış tablo sözdizimi toodefine dış tablolara genişletir.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-132">Elastic query extends hello existing external table syntax toodefine external tables that use external data sources of type RDBMS.</span></span> <span data-ttu-id="5a3e6-133">Dikey bölümleme için bir dış tablo tanımındaki yönlerini aşağıdaki hello kapsar:</span><span class="sxs-lookup"><span data-stu-id="5a3e6-133">An external table definition for vertical partitioning covers hello following aspects:</span></span> 

* <span data-ttu-id="5a3e6-134">**Şema**: hello dış tablo DDL sorgularınızı kullanabileceğiniz bir şema tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-134">**Schema**: hello external table DDL defines a schema that your queries can use.</span></span> <span data-ttu-id="5a3e6-135">Dış tablo tanımı'nda sağlanan hello şema hello hello gerçek verilerinin depolandığı hello Uzak veritabanı tablolarında toomatch hello şeması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-135">hello schema provided in your external table definition needs toomatch hello schema of hello tables in hello remote database where hello actual data is stored.</span></span> 
* <span data-ttu-id="5a3e6-136">**Uzak veritabanı başvuru**: hello dış tablo DDL tooan dış veri kaynağına başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-136">**Remote database reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="5a3e6-137">Merhaba dış veri kaynağına hello mantıksal sunucu adını ve veritabanı adını hello uzak veritabanının hello gerçek tablo verilerinin nerede depolanacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-137">hello external data source specifies hello logical server name and database name of hello remote database where hello actual table data is stored.</span></span> 

<span data-ttu-id="5a3e6-138">Dış veri kaynağına hello önceki bölümde özetlendiği gibi kullanarak, hello sözdizimi toocreate dış tablolara şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="5a3e6-138">Using an external data source as outlined in hello previous section, hello syntax toocreate external tables is as follows:</span></span> 

<span data-ttu-id="5a3e6-139">Merhaba DATA_SOURCE tümcesi hello dış tablo için kullanılan hello dış veri kaynağı (dikey bölümleme durumunda yani hello Uzak veritabanı) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-139">hello DATA_SOURCE clause defines hello external data source (i.e. hello remote database in case of vertical partitioning) that is used for hello external table.</span></span>  

<span data-ttu-id="5a3e6-140">Merhaba SCHEMA_NAME ve OBJECT_NAME yan tümceleri hello özelliği toomap hello dış tablo tanımı tooa tabloda farklı bir şema hello Uzak veritabanı veya farklı bir adla tooa tablo sırasıyla sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-140">hello SCHEMA_NAME and OBJECT_NAME clauses provide hello ability toomap hello external table definition tooa table in a different schema on hello remote database, or tooa table with a different name, respectively.</span></span> <span data-ttu-id="5a3e6-141">Bu toodefine bir dış tablo tooa Katalog görünümü veya DMV uzak veritabanınızı - veya burada hello uzak tablo adı zaten yerel olarak alınmış diğer durum istiyorsanız kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-141">This is useful if you want toodefine an external table tooa catalog view or DMV on your remote database - or any other situation where hello remote table name is already taken locally.</span></span>  

<span data-ttu-id="5a3e6-142">Merhaba aşağıdaki DDL deyimi var olan bir dış tablo tanımındaki hello yerel Kataloğu'ndan bırakır.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-142">hello following DDL statement drops an existing external table definition from hello local catalog.</span></span> <span data-ttu-id="5a3e6-143">Merhaba Uzak veritabanı etkilemez.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-143">It does not impact hello remote database.</span></span> 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

<span data-ttu-id="5a3e6-144">**CREATE/DROP dış tablo izinlerini**: dış tablo aynı zamanda olan DDL toorefer toohello temel alınan veri kaynağı gerekli için ALTER ANY dış veri kaynağı izinleri gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed toorefer toohello underlying data source.</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="5a3e6-145">Güvenlikle ilgili dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="5a3e6-145">Security considerations</span></span>
<span data-ttu-id="5a3e6-146">Erişim toohello dış tablo kullanıcılarla otomatik olarak toohello temel alınan uzak tablolar hello dış veri kaynağı tanımına verilen hello kimlik bilgileri altında erişin.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-146">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="5a3e6-147">Dikkatli bir şekilde erişim toohello dış tablosunda sipariş istenmeden tooavoid ayrıcalıkların hello kimlik bilgisi hello dış veri kaynağının aracılığıyla yönetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-147">You should carefully manage access toohello external table in order tooavoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="5a3e6-148">Yalnızca dizinindeymiş gibi olağan bir tablo normal SQL izinleri kullanılan tooGRANT veya REVOKE erişim tooan dış tablo olabilir.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-148">Regular SQL permissions can be used tooGRANT or REVOKE access tooan external table just as though it were a regular table.</span></span>  

## <a name="example-querying-vertically-partitioned-databases"></a><span data-ttu-id="5a3e6-149">Örnek: dikey sorgulama veritabanları bölümlenmiş</span><span class="sxs-lookup"><span data-stu-id="5a3e6-149">Example: querying vertically partitioned databases</span></span>
<span data-ttu-id="5a3e6-150">Merhaba aşağıdaki sorguyu hello siparişleri ve sipariş satırlarını için iki yerel tabloları ve hello uzak tablo arasında üç yönlü birleşim müşteriler için gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-150">hello following query performs a three-way join between hello two local tables for orders and order lines and hello remote table for customers.</span></span> <span data-ttu-id="5a3e6-151">Bu, hello başvuru verileri kullanım durumu için esnek sorgu örneğidir:</span><span class="sxs-lookup"><span data-stu-id="5a3e6-151">This is an example of hello reference data use case for elastic query:</span></span> 

    SELECT      
     c_id as customer,
     c_lastname as customer_name,
     count(*) as cnt_orderline, 
     max(ol_quantity) as max_quantity,
     avg(ol_amount) as avg_amount,
     min(ol_delivery_d) as min_deliv_date
    FROM customer 
    JOIN orders 
    ON c_id = o_c_id
    JOIN  order_line 
    ON o_id = ol_o_id and o_c_id = ol_c_id
    WHERE c_id = 100


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="5a3e6-152">Saklı yordamı uzaktan T-SQL yürütmesi için: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="5a3e6-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="5a3e6-153">Esnek sorgu aynı zamanda toohello parça doğrudan erişim sağlayan bir saklı yordam sunar.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-153">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="5a3e6-154">Merhaba saklı yordam adı verilir [sp\_yürütme \_uzak](https://msdn.microsoft.com/library/mt703714) ve kullanılan tooexecute uzak saklı yordamları veya T-SQL kodunu hello Uzak veritabanı üzerinde çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-154">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="5a3e6-155">Şu parametreler hello alır:</span><span class="sxs-lookup"><span data-stu-id="5a3e6-155">It takes hello following parameters:</span></span> 

* <span data-ttu-id="5a3e6-156">Veri kaynağı adı (nvarchar): hello dış veri kaynağı türü RDBMS hello adı.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-156">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="5a3e6-157">Sorgu (nvarchar): hello T-SQL sorgusu toobe her parça üzerinde yürütülür.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-157">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="5a3e6-158">Parametre bildirimi (nvarchar) - isteğe bağlı: dize veri türü tanımları (gibi sp_executesql) hello Sorgu parametresinde kullanılan hello parametreler için.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-158">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="5a3e6-159">Parametre değeri listesi - isteğe bağlı: parametre değerleri (gibi sp_executesql) virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="5a3e6-160">Merhaba sp\_yürütme\_uzak kullanır hello hello çağırma parametreleri tooexecute hello T-SQL deyimini hello uzak veritabanlarında verilen sağlanan dış veri kaynağı.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-160">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="5a3e6-161">Merhaba dış veri kaynağı tooconnect toohello shardmap manager veritabanı ve hello uzak veritabanlarına hello kimlik bilgisi kullanır.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-161">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="5a3e6-162">Örnek:</span><span class="sxs-lookup"><span data-stu-id="5a3e6-162">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a><span data-ttu-id="5a3e6-163">Bağlantı için araçları</span><span class="sxs-lookup"><span data-stu-id="5a3e6-163">Connectivity for tools</span></span>
<span data-ttu-id="5a3e6-164">Etkin Esnek sorgu ve tanımlanan dış tablolara hello SQL DB sunucusunda, BI ve veri tümleştirme araçları toodatabases normal SQL Server bağlantı dizelerini tooconnect kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-164">You can use regular SQL Server connection strings tooconnect your BI and data integration tools toodatabases on hello SQL DB server that has elastic query enabled and external tables defined.</span></span> <span data-ttu-id="5a3e6-165">SQL Server, aracı için bir veri kaynağı olarak desteklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-165">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="5a3e6-166">Ardından toohello esnek sorgu veritabanını ve aracınızı toowith bağlamak yalnızca herhangi diğer SQL Server veritabanı gibi dış tabloları bakın.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-166">Then refer toohello elastic query database and its external tables just like any other SQL Server database that you would connect toowith your tool.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="5a3e6-167">En iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="5a3e6-167">Best practices</span></span>
* <span data-ttu-id="5a3e6-168">Hello esnek sorgu uç veritabanı erişim toohello uzak veritabanına erişim Azure hizmetlerini SQL DB güvenlik duvarı yapılandırmasıyla etkinleştirerek verilip verilmediğini emin olun.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-168">Ensure that hello elastic query endpoint database has been given access toohello remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span></span> <span data-ttu-id="5a3e6-169">Ayrıca hello dış veri kaynağı tanımını hello uzak veritabanına başarıyla oturum açabilir ve hello izinleri tooaccess hello uzak tablo sahip sağlanan bu hello kimlik bilgisi emin olun.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-169">Also ensure that hello credential provided in hello external data source definition can successfully log into hello remote database and has hello permissions tooaccess hello remote table.</span></span>  
* <span data-ttu-id="5a3e6-170">Esnek sorgu hello hesaplama çoğunu hello uzak veritabanlarında burada yapılabilir sorguları için en iyi şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-170">Elastic query works best for queries where most of hello computation can be done on hello remote databases.</span></span> <span data-ttu-id="5a3e6-171">Genellikle hello en iyi sorgu performansını hello uzak veritabanları veya tamamen hello Uzak veritabanı üzerinde gerçekleştirilebilir birleştirmeler hesaplanan seçmeli filtre koşulları sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-171">You typically get hello best query performance with selective filter predicates that can be evaluated on hello remote databases or joins that can be performed completely on hello remote database.</span></span> <span data-ttu-id="5a3e6-172">Diğer sorgu desenlerine tooload büyük miktarlarda veri hello uzak veritabanından gerekebilir ve kötü gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-172">Other query patterns may need tooload large amounts of data from hello remote database and may perform poorly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5a3e6-173">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5a3e6-173">Next steps</span></span>

* <span data-ttu-id="5a3e6-174">Esnek sorgu genel bakış için bkz: [esnek sorgu genel bakış](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5a3e6-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="5a3e6-175">Dikey bölümleme öğretici için bkz: [(dikey bölümleme) veritabanları arası sorgusu ile çalışmaya başlama](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="5a3e6-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="5a3e6-176">Yatay bölümleme (parçalama) bir öğretici için bkz: [yatay (parçalama) bölümleme için esnek sorgu ile çalışmaya başlama](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="5a3e6-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="5a3e6-177">Yatay olarak bölümlenmiş verilere ilişkin söz dizimi ve örnek sorgular için bkz: [yatay sorgulama bölümlenmiş veri)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="5a3e6-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="5a3e6-178">Bkz: [sp\_yürütme \_uzak](https://msdn.microsoft.com/library/mt703714) tek uzaktan Azure SQL veritabanı ya da yatay bölümleme düzenindeki parça olarak hizmet veren bir veritabanları kümesi üzerinde bir Transact-SQL deyimini yürütür bir saklı yordam için.</span><span class="sxs-lookup"><span data-stu-id="5a3e6-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
