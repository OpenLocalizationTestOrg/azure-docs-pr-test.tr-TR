---
title: "SQL veri ambarı aaaStored yordamlarda | Microsoft Docs"
description: "Saklı yordamlar çözümleri geliştirmek için Azure SQL Data Warehouse'da uygulamak için ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 9b238789-6efe-4820-bf77-5a5da2afa0e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 416252dd3dea95c66aa5e886860b933b22578002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a><span data-ttu-id="587cb-103">Saklı yordamlar SQL veri ambarı</span><span class="sxs-lookup"><span data-stu-id="587cb-103">Stored procedures in SQL Data Warehouse</span></span>
<span data-ttu-id="587cb-104">SQL veri ambarı SQL Server'da bulunan hello Transact-SQL özelliklerini çoğunu destekler.</span><span class="sxs-lookup"><span data-stu-id="587cb-104">SQL Data Warehouse supports many of hello Transact-SQL features found in SQL Server.</span></span> <span data-ttu-id="587cb-105">Daha da önemlisi biz tooleverage toomaximize hello çözümünüzün performansını istediğiniz belirli özellikleri genişletme vardır.</span><span class="sxs-lookup"><span data-stu-id="587cb-105">More importantly there are scale out specific features that we will want tooleverage toomaximize hello performance of your solution.</span></span>

<span data-ttu-id="587cb-106">Ancak, toomaintain hello ölçek ve var. SQL veri ambarı performansını ayrıca bazı özellikler ve davranış farklılıkları ve diğerleri desteklenmeyen işlev değildir.</span><span class="sxs-lookup"><span data-stu-id="587cb-106">However, toomaintain hello scale and performance of SQL Data Warehouse there are also some features and functionality that have behavioral differences and others that are not supported.</span></span>

<span data-ttu-id="587cb-107">Bu makalede nasıl tooimplement saklı yordamlar SQL Data warehouse'da açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="587cb-107">This article explains how tooimplement stored procedures within SQL Data Warehouse.</span></span>

## <a name="introducing-stored-procedures"></a><span data-ttu-id="587cb-108">Saklı yordamlar Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="587cb-108">Introducing stored procedures</span></span>
<span data-ttu-id="587cb-109">Saklı yordamlar SQL kodunuzu Kapsüllenen harika bir yöntemdir; Bu, hello veri ambarında Kapat tooyour veri depolama.</span><span class="sxs-lookup"><span data-stu-id="587cb-109">Stored procedures are a great way for encapsulating your SQL code; storing it close tooyour data in hello data warehouse.</span></span> <span data-ttu-id="587cb-110">Merhaba kod yönetilebilir birimler halinde kapsülleyerek saklı yordamlar çözümleri modülarize etmek geliştiricilerin yardımcı; kod büyük re-usability kolaylaştırmanın.</span><span class="sxs-lookup"><span data-stu-id="587cb-110">By encapsulating hello code into manageable units stored procedures help developers modularize their solutions; facilitating greater re-usability of code.</span></span> <span data-ttu-id="587cb-111">Her bir saklı yordam parametreleri toomake kabul edebilir bunları bile daha esnektir.</span><span class="sxs-lookup"><span data-stu-id="587cb-111">Each stored procedure can also accept parameters toomake them even more flexible.</span></span>

<span data-ttu-id="587cb-112">SQL veri ambarı Basitleştirilmiş ve kolaylaştırılmış saklı yordam uygulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="587cb-112">SQL Data Warehouse provides a simplified and streamlined stored procedure implementation.</span></span> <span data-ttu-id="587cb-113">Bu saklı yordam hello sunucusudur hello büyük karşılaştırıldığında fark tooSQL önceden derlenmiş kod değil.</span><span class="sxs-lookup"><span data-stu-id="587cb-113">hello biggest difference compared tooSQL Server is that hello stored procedure is not pre-compiled code.</span></span> <span data-ttu-id="587cb-114">Veri ambarları genellikle hello derleme süresi ile daha az endişe duyuyoruz.</span><span class="sxs-lookup"><span data-stu-id="587cb-114">In data warehouses we are generally less concerned with hello compilation time.</span></span> <span data-ttu-id="587cb-115">Merhaba saklı yordamı kodu doğru büyük veri birimlerine karşı çalışırken en iyi duruma getirilmiş emin daha önemlidir.</span><span class="sxs-lookup"><span data-stu-id="587cb-115">It is more important that hello stored procedure code is correctly optimised when operating against large data volumes.</span></span> <span data-ttu-id="587cb-116">Merhaba toosave saat, dakika ve saniyeleri değil milisaniye hedeftir.</span><span class="sxs-lookup"><span data-stu-id="587cb-116">hello goal is toosave hours, minutes and seconds not milliseconds.</span></span> <span data-ttu-id="587cb-117">Bu nedenle SQL mantığı için kapsayıcı olarak daha yararlı toothink saklı yordamların orantılıdır.</span><span class="sxs-lookup"><span data-stu-id="587cb-117">It is therefore more helpful toothink of stored procedures as containers for SQL logic.</span></span>     

<span data-ttu-id="587cb-118">SQL veri ambarı yürütüldüğünde, saklı yordam hello SQL deyimleri ayrıştırılır, çevrilen ve çalışma zamanında en iyi duruma getirilmiş.</span><span class="sxs-lookup"><span data-stu-id="587cb-118">When SQL Data Warehouse executes your stored procedure hello SQL statements are parsed, translated and optimized at run time.</span></span> <span data-ttu-id="587cb-119">Bu işlem sırasında her deyim dağıtılmış sorgular dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="587cb-119">During this process each statement is converted into distributed queries.</span></span> <span data-ttu-id="587cb-120">Merhaba hello veri karşı gerçekleştirilmeden SQL kodu gönderildi farklı toohello sorgudur.</span><span class="sxs-lookup"><span data-stu-id="587cb-120">hello SQL code that is actually executed against hello data is different toohello query submitted.</span></span>

## <a name="nesting-stored-procedures"></a><span data-ttu-id="587cb-121">İç içe geçme saklı yordamlar</span><span class="sxs-lookup"><span data-stu-id="587cb-121">Nesting stored procedures</span></span>
<span data-ttu-id="587cb-122">Ne zaman saklı yordamlar diğer saklı yordamlar çağırabilir veya hello iç saklı yordam veya kod çağırma toobe iç içe geçmiş denirse ardından dinamik sql Yürüt.</span><span class="sxs-lookup"><span data-stu-id="587cb-122">When stored procedures call other stored procedures or execute dynamic sql then hello inner stored procedure or code invocation is said toobe nested.</span></span>

<span data-ttu-id="587cb-123">SQL veri ambarı en fazla 8 iç içe geçme düzeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="587cb-123">SQL Data Warehouse support a maximum of 8 nesting levels.</span></span> <span data-ttu-id="587cb-124">Biraz farklı tooSQL sunucu budur.</span><span class="sxs-lookup"><span data-stu-id="587cb-124">This is slightly different tooSQL Server.</span></span> <span data-ttu-id="587cb-125">SQL Server'da Hello iç içe geçirme düzeyi 32'dir.</span><span class="sxs-lookup"><span data-stu-id="587cb-125">hello nest level in SQL Server is 32.</span></span>

<span data-ttu-id="587cb-126">Merhaba üst düzey saklı yordam çağrısı toonest düzey 1 karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="587cb-126">hello top level stored procedure call equates toonest level 1</span></span>

```sql
EXEC prc_nesting
```
<span data-ttu-id="587cb-127">Merhaba depolanan yordamı de başka bir yürütme çağrı yapar sonra bu hello iç içe geçirme düzeyi too2 artırır</span><span class="sxs-lookup"><span data-stu-id="587cb-127">If hello stored procedure also makes another EXEC call then this will increase hello nest level too2</span></span>

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
<span data-ttu-id="587cb-128">Ardından Hello ikinci yordam sonra bazı dinamik sql çalıştırırsa bu hello iç içe geçirme düzeyi too3 artırır</span><span class="sxs-lookup"><span data-stu-id="587cb-128">If hello second procedure then executes some dynamic sql then this will increase hello nest level too3</span></span>

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

<span data-ttu-id="587cb-129">Not SQL Data Warehouse desteklememektedir@NESTLEVEL.</span><span class="sxs-lookup"><span data-stu-id="587cb-129">Note SQL Data Warehouse does not currently support @@NESTLEVEL.</span></span> <span data-ttu-id="587cb-130">İç içe geçirme düzeyi izini tookeep kendiniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="587cb-130">You will need tookeep a track of your nest level yourself.</span></span> <span data-ttu-id="587cb-131">Merhaba 8 iç içe geçirme düzeyi sınırı karşılaşır ancak, bunu yaparsanız kodunuzu toore iş gerekir ve ", böylece bu sınırı içinde sığar düzleştirmek" olası değil.</span><span class="sxs-lookup"><span data-stu-id="587cb-131">It is unlikely you will hit hello 8 nest level limit but if you do you will need toore-work your code and "flatten" it so that it fits within this limit.</span></span>

## <a name="insertexecute"></a><span data-ttu-id="587cb-132">EKLE... YÜRÜTME</span><span class="sxs-lookup"><span data-stu-id="587cb-132">INSERT..EXECUTE</span></span>
<span data-ttu-id="587cb-133">SQL veri ambarı tooconsume hello sonuç kümesi, INSERT deyimi olan bir saklı yordam izin vermez.</span><span class="sxs-lookup"><span data-stu-id="587cb-133">SQL Data Warehouse does not permit you tooconsume hello result set of a stored procedure with an INSERT statement.</span></span> <span data-ttu-id="587cb-134">Ancak, kullanabileceğiniz alternatif bir yaklaşım yoktur.</span><span class="sxs-lookup"><span data-stu-id="587cb-134">However, there is an alternative approach you can use.</span></span>

<span data-ttu-id="587cb-135">Lütfen aşağıdaki makaleye bakın toohello başvurun [geçici tablolara] konusunda bir örnek toodo bu.</span><span class="sxs-lookup"><span data-stu-id="587cb-135">Please refer toohello following article on [temporary tables] for an example on how toodo this.</span></span>

## <a name="limitations"></a><span data-ttu-id="587cb-136">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="587cb-136">Limitations</span></span>
<span data-ttu-id="587cb-137">SQL veri ambarı'nda uygulanmadı Transact-SQL saklı yordamları bazı yönleri vardır.</span><span class="sxs-lookup"><span data-stu-id="587cb-137">There are some aspects of Transact-SQL stored procedures that are not implemented in SQL Data Warehouse.</span></span>

<span data-ttu-id="587cb-138">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="587cb-138">They are:</span></span>

* <span data-ttu-id="587cb-139">geçici saklı yordamlar</span><span class="sxs-lookup"><span data-stu-id="587cb-139">temporary stored procedures</span></span>
* <span data-ttu-id="587cb-140">numaralandırılmış saklı yordamlar</span><span class="sxs-lookup"><span data-stu-id="587cb-140">numbered stored procedures</span></span>
* <span data-ttu-id="587cb-141">genişletilmiş saklı yordamlar</span><span class="sxs-lookup"><span data-stu-id="587cb-141">extended stored procedures</span></span>
* <span data-ttu-id="587cb-142">CLR saklı yordamlar</span><span class="sxs-lookup"><span data-stu-id="587cb-142">CLR stored procedures</span></span>
* <span data-ttu-id="587cb-143">şifreleme seçeneği</span><span class="sxs-lookup"><span data-stu-id="587cb-143">encryption option</span></span>
* <span data-ttu-id="587cb-144">çoğaltma seçeneği</span><span class="sxs-lookup"><span data-stu-id="587cb-144">replication option</span></span>
* <span data-ttu-id="587cb-145">Tablo değerli parametreleri</span><span class="sxs-lookup"><span data-stu-id="587cb-145">table-valued parameters</span></span>
* <span data-ttu-id="587cb-146">salt okunur parametreleri</span><span class="sxs-lookup"><span data-stu-id="587cb-146">read-only parameters</span></span>
* <span data-ttu-id="587cb-147">varsayılan parametreleri</span><span class="sxs-lookup"><span data-stu-id="587cb-147">default parameters</span></span>
* <span data-ttu-id="587cb-148">yürütme bağlamı</span><span class="sxs-lookup"><span data-stu-id="587cb-148">execution contexts</span></span>
* <span data-ttu-id="587cb-149">return deyimi</span><span class="sxs-lookup"><span data-stu-id="587cb-149">return statement</span></span>

## <a name="next-steps"></a><span data-ttu-id="587cb-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="587cb-150">Next steps</span></span>
<span data-ttu-id="587cb-151">Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].</span><span class="sxs-lookup"><span data-stu-id="587cb-151">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[geçici tablolara]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
