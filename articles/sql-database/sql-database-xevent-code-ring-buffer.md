---
title: "SQL veritabanı için halka arabelleği kodu aaaXEvent | Microsoft Docs"
description: "Azure SQL veritabanında hello halka arabelleği hedef kullanımını yapılır, kolay ve hızlı bir Transact-SQL kod örneğini sağlar."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 2510fb3f-c8f2-437a-8f49-9d5f6c96e75b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 21df748d9999d6837d2b5bbe4a3f47fb351b4633
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="709f1-103">Halka arabelleği hedef kod SQL veritabanında genişletilmiş olaylar</span><span class="sxs-lookup"><span data-stu-id="709f1-103">Ring Buffer target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="709f1-104">Hello kolay hızlı şekilde toocapture ve rapor bilgileri için genişletilmiş bir olay için bir test sırasında tam bir kod örneği istiyor.</span><span class="sxs-lookup"><span data-stu-id="709f1-104">You want a complete code sample for hello easiest quick way toocapture and report information for an extended event during a test.</span></span> <span data-ttu-id="709f1-105">Merhaba kolay genişletilmiş olay verilerini hedefidir hello [halka arabelleği hedef](http://msdn.microsoft.com/library/ff878182.aspx).</span><span class="sxs-lookup"><span data-stu-id="709f1-105">hello easiest target for extended event data is hello [Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx).</span></span>

<span data-ttu-id="709f1-106">Bu konuda, bir Transact-SQL kodunu örnek sunulmaktadır:</span><span class="sxs-lookup"><span data-stu-id="709f1-106">This topic presents a Transact-SQL code sample that:</span></span>

1. <span data-ttu-id="709f1-107">Veri toodemonstrate ile içeren bir tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="709f1-107">Creates a table with data toodemonstrate with.</span></span>
2. <span data-ttu-id="709f1-108">Ayrıca varolan bir genişletilmiş olay için bir oturum oluşturur **sqlserver.sql_statement_starting**.</span><span class="sxs-lookup"><span data-stu-id="709f1-108">Creates a session for an existing extended event, namely **sqlserver.sql_statement_starting**.</span></span>
   
   * <span data-ttu-id="709f1-109">Merhaba, belirli bir güncelleştirme dize içeren sınırlı tooSQL deyimleri olaydır: **deyimi '% güncelleştirme tabEmployee %' gibi**.</span><span class="sxs-lookup"><span data-stu-id="709f1-109">hello event is limited tooSQL statements that contain a particular Update string: **statement LIKE '%UPDATE tabEmployee%'**.</span></span>
   * <span data-ttu-id="709f1-110">Merhaba olay tooa hedef türü halka arabelleği toosend hello çıktısı öğesine seçer **package0.ring_buffer**.</span><span class="sxs-lookup"><span data-stu-id="709f1-110">Chooses toosend hello output of hello event tooa target of type Ring Buffer, namely  **package0.ring_buffer**.</span></span>
3. <span data-ttu-id="709f1-111">Merhaba olay oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="709f1-111">Starts hello event session.</span></span>
4. <span data-ttu-id="709f1-112">Birkaç basit SQL güncelleştirme deyimleri verir.</span><span class="sxs-lookup"><span data-stu-id="709f1-112">Issues a couple of simple SQL UPDATE statements.</span></span>
5. <span data-ttu-id="709f1-113">Bir SQL SELECT deyimi tooretrieve olay çıktısını hello halka arabelleği verir.</span><span class="sxs-lookup"><span data-stu-id="709f1-113">Issues a SQL SELECT statement tooretrieve event output from hello Ring Buffer.</span></span>
   
   * <span data-ttu-id="709f1-114">**sys.dm_xe_database_session_targets** ve diğer dinamik yönetim görünümlerini (Dmv'leri) birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="709f1-114">**sys.dm_xe_database_session_targets** and other dynamic management views (DMVs) are joined.</span></span>
6. <span data-ttu-id="709f1-115">Merhaba olay oturumu durdurur.</span><span class="sxs-lookup"><span data-stu-id="709f1-115">Stops hello event session.</span></span>
7. <span data-ttu-id="709f1-116">Düşme halka arabelleği hedef, toorelease kaynaklarını hello.</span><span class="sxs-lookup"><span data-stu-id="709f1-116">Drops hello Ring Buffer target, toorelease its resources.</span></span>
8. <span data-ttu-id="709f1-117">Merhaba olay oturumu ve hello demo tabloyu bırakır.</span><span class="sxs-lookup"><span data-stu-id="709f1-117">Drops hello event session and hello demo table.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="709f1-118">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="709f1-118">Prerequisites</span></span>

* <span data-ttu-id="709f1-119">Bir Azure hesabı ve aboneliği</span><span class="sxs-lookup"><span data-stu-id="709f1-119">An Azure account and subscription.</span></span> <span data-ttu-id="709f1-120">[Ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="709f1-120">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="709f1-121">Herhangi bir veritabanı, bir tablodaki oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="709f1-121">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="709f1-122">İsteğe bağlı olarak yapabileceğiniz [oluşturma bir **AdventureWorksLT** demo veritabanı](sql-database-get-started.md) dakika.</span><span class="sxs-lookup"><span data-stu-id="709f1-122">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="709f1-123">SQL Server Management Studio (ssms.exe), ideal olarak en son aylık güncelleştirme sürümü.</span><span class="sxs-lookup"><span data-stu-id="709f1-123">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="709f1-124">Merhaba son ssms.exe öğesinden yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="709f1-124">You can download hello latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="709f1-125">Başlıklı konuda [SQL Server Management Studio'yu indirme](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="709f1-125">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="709f1-126">Doğrudan bağlantı toohello indirme.</span><span class="sxs-lookup"><span data-stu-id="709f1-126">A direct link toohello download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a><span data-ttu-id="709f1-127">Kod örneği</span><span class="sxs-lookup"><span data-stu-id="709f1-127">Code sample</span></span>

<span data-ttu-id="709f1-128">Çok küçük değişikliğe sahip hello aşağıdaki halka arabelleği kod örneği Azure SQL Database veya Microsoft SQL Server üzerinde çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="709f1-128">With very minor modification, hello following Ring Buffer code sample can be run on either Azure SQL Database or Microsoft SQL Server.</span></span> <span data-ttu-id="709f1-129">Merhaba, adım 5'te hello FROM yan tümcesinde kullanılan hello varlığı bazı dinamik yönetim görünümlerini (Dmv'leri) hello adını ' _veritabanı' hello düğümünün farktır.</span><span class="sxs-lookup"><span data-stu-id="709f1-129">hello difference is hello presence of hello node '_database' in hello name of some dynamic management views (DMVs), used in hello FROM clause in Step 5.</span></span> <span data-ttu-id="709f1-130">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="709f1-130">For example:</span></span>

* <span data-ttu-id="709f1-131">sys.dm_xe**_veritabanı**_session_targets</span><span class="sxs-lookup"><span data-stu-id="709f1-131">sys.dm_xe**_database**_session_targets</span></span>
* <span data-ttu-id="709f1-132">sys.dm_xe_session_targets</span><span class="sxs-lookup"><span data-stu-id="709f1-132">sys.dm_xe_session_targets</span></span>

&nbsp;

```sql
GO
----  Transact-SQL.
---- Step set 1.

SET NOCOUNT ON;
GO


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'tabEmployee')
BEGIN
    DROP TABLE tabEmployee;
END
GO


CREATE TABLE tabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO tabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO

---- Step set 2.


IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'eventsession_gm_azuresqldb51')
BEGIN
    DROP EVENT SESSION eventsession_gm_azuresqldb51
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE '%UPDATE tabEmployee%'
            )
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
GO

---- Step set 3.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = START;
GO

---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
GO

---- Step set 5.


SELECT
    se.name                      AS [session-name],
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source,
    st.target_data,
    CAST(st.target_data AS XML)  AS [target_data_XML]
FROM
               sys.dm_xe_database_session_event_actions  AS ac

    INNER JOIN sys.dm_xe_database_session_events         AS ev  ON ev.event_name = ac.event_name
        AND CAST(ev.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_object_columns AS oc
         ON CAST(oc.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_targets        AS st
         ON CAST(st.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_sessions               AS se
         ON CAST(ac.event_session_address AS BINARY(8)) = CAST(se.address AS BINARY(8))
WHERE
        oc.column_name = 'occurrence_number'
    AND
        se.name        = 'eventsession_gm_azuresqldb51'
    AND
        ac.action_name = 'sql_text'
ORDER BY
    se.name,
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source
;
GO

---- Step set 6.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = STOP;
GO

---- Step set 7.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO

---- Step set 8.


DROP EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE;
GO

DROP TABLE tabEmployee;
GO
```


&nbsp;

## <a name="ring-buffer-contents"></a><span data-ttu-id="709f1-133">Halka arabelleği içeriği</span><span class="sxs-lookup"><span data-stu-id="709f1-133">Ring Buffer contents</span></span>

<span data-ttu-id="709f1-134">Ssms.exe toorun hello kod örneği kullandık.</span><span class="sxs-lookup"><span data-stu-id="709f1-134">We used ssms.exe toorun hello code sample.</span></span>

<span data-ttu-id="709f1-135">tooview hello sonuçları, biz tıklattınız hello hücre hello sütun başlığı altında **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="709f1-135">tooview hello results, we clicked hello cell under hello column header **target_data_XML**.</span></span>

<span data-ttu-id="709f1-136">Merhaba sonuçlar bölmesinde biz hello hücre hello sütun başlığı altında tıklattınız sonra **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="709f1-136">Then in hello results pane we clicked hello cell under hello column header **target_data_XML**.</span></span> <span data-ttu-id="709f1-137">Bunu başka bir dosya sekmesini hangi hello hello sonuç hücrenin içeriğinin, XML olarak görüntülenen ssms.exe oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="709f1-137">This click created another file tab in ssms.exe in which hello content of hello result cell was displayed, as XML.</span></span>

<span data-ttu-id="709f1-138">Merhaba çıkış blok aşağıdaki hello gösterilir.</span><span class="sxs-lookup"><span data-stu-id="709f1-138">hello output is shown in hello following block.</span></span> <span data-ttu-id="709f1-139">Uzun görünüyor, ancak bunu yalnızca iki  **<event>**  öğeleri.</span><span class="sxs-lookup"><span data-stu-id="709f1-139">It looks long, but it is just two **<event>** elements.</span></span>

&nbsp;

```
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="1728">
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.317Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>7</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>184</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>328</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.327Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>10</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>340</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>486</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
</RingBufferTarget>
```


#### <a name="release-resources-held-by-your-ring-buffer"></a><span data-ttu-id="709f1-140">Halka arabelleği ile tutulan yayın kaynakları</span><span class="sxs-lookup"><span data-stu-id="709f1-140">Release resources held by your Ring Buffer</span></span>

<span data-ttu-id="709f1-141">Halka arabelleği ile işiniz bittiğinde, kaldırmak ve veren kaynaklarını serbest bir **ALTER** hello aşağıdaki ister:</span><span class="sxs-lookup"><span data-stu-id="709f1-141">When you are done with your Ring Buffer, you can remove it and release its resources issuing an **ALTER** like hello following:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


<span data-ttu-id="709f1-142">Olay oturumunuz Hello tanımını güncelleştirildi, ancak atılmadı.</span><span class="sxs-lookup"><span data-stu-id="709f1-142">hello definition of your event session is updated, but not dropped.</span></span> <span data-ttu-id="709f1-143">Daha sonra başka bir örneği hello halka arabelleği tooyour olay oturumu ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="709f1-143">Later you can add another instance of hello Ring Buffer tooyour event session:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a><span data-ttu-id="709f1-144">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="709f1-144">More information</span></span>

<span data-ttu-id="709f1-145">Azure SQL veritabanı genişletilmiş olaylar için birincil konu Hello şöyledir:</span><span class="sxs-lookup"><span data-stu-id="709f1-145">hello primary topic for extended events on Azure SQL Database is:</span></span>

* <span data-ttu-id="709f1-146">[SQL veritabanı olay konuları Genişletilmiş](sql-database-xevent-db-diff-from-svr.md), Microsoft SQL Server ile Azure SQL veritabanı arasında farklılık genişletilmiş olaylar bazı yönlerini karşılaştırır.</span><span class="sxs-lookup"><span data-stu-id="709f1-146">[Extended event considerations in SQL Database](sql-database-xevent-db-diff-from-svr.md), which contrasts some aspects of extended events that differ between Azure SQL Database versus Microsoft SQL Server.</span></span>

<span data-ttu-id="709f1-147">Bağlantılar aşağıdaki hello diğer kod örnek konuları genişletilmiş olaylar için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="709f1-147">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="709f1-148">Ancak, Microsoft SQL Server Azure SQL veritabanına karşı Hello örnek hedefler olup olmadığını herhangi örnek toosee düzenli olarak denetlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="709f1-148">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="709f1-149">Ardından, küçük değişiklikler gerekli toorun hello örnek olup karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="709f1-149">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

* <span data-ttu-id="709f1-150">Azure SQL veritabanı için kod örneği: [SQL veritabanında genişletilmiş olaylar için olay dosyası hedef kodu](sql-database-xevent-code-event-file.md)</span><span class="sxs-lookup"><span data-stu-id="709f1-150">Code sample for Azure SQL Database: [Event File target code for extended events in SQL Database](sql-database-xevent-code-event-file.md)</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
