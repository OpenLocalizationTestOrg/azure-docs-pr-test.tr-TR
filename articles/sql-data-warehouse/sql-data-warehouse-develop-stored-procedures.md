---
title: "Saklı yordamlar SQL veri ambarı'nda | Microsoft Docs"
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
ms.openlocfilehash: e42d80f0ca35f3fbb67389c66d072bc40d8a8d2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a><span data-ttu-id="04774-103">Saklı yordamlar SQL veri ambarı</span><span class="sxs-lookup"><span data-stu-id="04774-103">Stored procedures in SQL Data Warehouse</span></span>
<span data-ttu-id="04774-104">SQL veri ambarı SQL Server'da bulunan Transact-SQL özelliklerinin çoğunu destekler.</span><span class="sxs-lookup"><span data-stu-id="04774-104">SQL Data Warehouse supports many of the Transact-SQL features found in SQL Server.</span></span> <span data-ttu-id="04774-105">Daha da önemlisi ölçek genişletme biz çözümünüzün performansını en üst düzeye çıkarmak için yararlanmak isteyen belirli özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="04774-105">More importantly there are scale out specific features that we will want to leverage to maximize the performance of your solution.</span></span>

<span data-ttu-id="04774-106">Ancak, korumak için ölçek ve var. SQL veri ambarı performansını ayrıca bazı özellikler ve davranış farklılıkları ve diğerleri desteklenmeyen işlevsellik değildir.</span><span class="sxs-lookup"><span data-stu-id="04774-106">However, to maintain the scale and performance of SQL Data Warehouse there are also some features and functionality that have behavioral differences and others that are not supported.</span></span>

<span data-ttu-id="04774-107">Bu makalede, SQL Data Warehouse içinde saklı yordamlar uygulamak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="04774-107">This article explains how to implement stored procedures within SQL Data Warehouse.</span></span>

## <a name="introducing-stored-procedures"></a><span data-ttu-id="04774-108">Saklı yordamlar Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="04774-108">Introducing stored procedures</span></span>
<span data-ttu-id="04774-109">Saklı yordamlar SQL kodunuzu Kapsüllenen harika bir yöntemdir; verilerinizi veri ambarındaki yakın depolama.</span><span class="sxs-lookup"><span data-stu-id="04774-109">Stored procedures are a great way for encapsulating your SQL code; storing it close to your data in the data warehouse.</span></span> <span data-ttu-id="04774-110">Kod yönetilebilir birimler halinde kapsülleyerek saklı yordamlar çözümleri modülarize etmek geliştiricilerin yardımcı; kod büyük re-usability kolaylaştırmanın.</span><span class="sxs-lookup"><span data-stu-id="04774-110">By encapsulating the code into manageable units stored procedures help developers modularize their solutions; facilitating greater re-usability of code.</span></span> <span data-ttu-id="04774-111">Her bir saklı yordam, ayrıca bunları daha esnek hale getirmek için parametre kabul edebilir.</span><span class="sxs-lookup"><span data-stu-id="04774-111">Each stored procedure can also accept parameters to make them even more flexible.</span></span>

<span data-ttu-id="04774-112">SQL veri ambarı Basitleştirilmiş ve kolaylaştırılmış saklı yordam uygulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="04774-112">SQL Data Warehouse provides a simplified and streamlined stored procedure implementation.</span></span> <span data-ttu-id="04774-113">SQL Server'a karşılaştırma büyük fark saklı yordamı önceden derlenmiş kod olmamasıdır.</span><span class="sxs-lookup"><span data-stu-id="04774-113">The biggest difference compared to SQL Server is that the stored procedure is not pre-compiled code.</span></span> <span data-ttu-id="04774-114">Veri ambarları genellikle derleme süresi ile daha az endişe duyuyoruz.</span><span class="sxs-lookup"><span data-stu-id="04774-114">In data warehouses we are generally less concerned with the compilation time.</span></span> <span data-ttu-id="04774-115">Saklı yordam kodu doğru büyük veri birimlerine karşı çalışırken en iyi duruma getirilmiş emin daha önemlidir.</span><span class="sxs-lookup"><span data-stu-id="04774-115">It is more important that the stored procedure code is correctly optimised when operating against large data volumes.</span></span> <span data-ttu-id="04774-116">Saat, dakika ve saniyeleri değil milisaniye kaydetmek için belirtilir.</span><span class="sxs-lookup"><span data-stu-id="04774-116">The goal is to save hours, minutes and seconds not milliseconds.</span></span> <span data-ttu-id="04774-117">Bu nedenle saklı yordamlar SQL mantığı için kapsayıcı olarak düşünmek daha yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="04774-117">It is therefore more helpful to think of stored procedures as containers for SQL logic.</span></span>     

<span data-ttu-id="04774-118">SQL Data Warehouse, saklı yordam yürüttüğünde SQL deyimlerini, çevrilen ve çalışma zamanında en iyi duruma getirilmiş ayrıştırılır.</span><span class="sxs-lookup"><span data-stu-id="04774-118">When SQL Data Warehouse executes your stored procedure the SQL statements are parsed, translated and optimized at run time.</span></span> <span data-ttu-id="04774-119">Bu işlem sırasında her deyim dağıtılmış sorgular dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="04774-119">During this process each statement is converted into distributed queries.</span></span> <span data-ttu-id="04774-120">Veri karşı gerçekleştirilmeden SQL kodunu gönderilen sorgu farklıdır.</span><span class="sxs-lookup"><span data-stu-id="04774-120">The SQL code that is actually executed against the data is different to the query submitted.</span></span>

## <a name="nesting-stored-procedures"></a><span data-ttu-id="04774-121">İç içe geçme saklı yordamlar</span><span class="sxs-lookup"><span data-stu-id="04774-121">Nesting stored procedures</span></span>
<span data-ttu-id="04774-122">Ne zaman saklı yordamlar diğer saklı yordamlar çağırabilir veya iç saklı yordam veya kod çağırma iç içe söylenir sonra dinamik sql Yürüt.</span><span class="sxs-lookup"><span data-stu-id="04774-122">When stored procedures call other stored procedures or execute dynamic sql then the inner stored procedure or code invocation is said to be nested.</span></span>

<span data-ttu-id="04774-123">SQL veri ambarı en fazla 8 iç içe geçme düzeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="04774-123">SQL Data Warehouse support a maximum of 8 nesting levels.</span></span> <span data-ttu-id="04774-124">Bu SQL Server için biraz farklıdır.</span><span class="sxs-lookup"><span data-stu-id="04774-124">This is slightly different to SQL Server.</span></span> <span data-ttu-id="04774-125">SQL Server iç içe geçirme düzeyi 32'dir.</span><span class="sxs-lookup"><span data-stu-id="04774-125">The nest level in SQL Server is 32.</span></span>

<span data-ttu-id="04774-126">Üst düzey saklı yordam çağrısı düzey 1 iç içe karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="04774-126">The top level stored procedure call equates to nest level 1</span></span>

```sql
EXEC prc_nesting
```
<span data-ttu-id="04774-127">Ardından saklı yordamı da başka bir yürütme çağrı yaparsa bu 2 iç içe geçirme düzeyi artırır</span><span class="sxs-lookup"><span data-stu-id="04774-127">If the stored procedure also makes another EXEC call then this will increase the nest level to 2</span></span>

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
<span data-ttu-id="04774-128">Ardından ikinci yordam sonra bazı dinamik sql çalıştırırsa bu iç içe geçirme düzeyi 3 artırır</span><span class="sxs-lookup"><span data-stu-id="04774-128">If the second procedure then executes some dynamic sql then this will increase the nest level to 3</span></span>

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

<span data-ttu-id="04774-129">Not SQL Data Warehouse desteklememektedir@NESTLEVEL.</span><span class="sxs-lookup"><span data-stu-id="04774-129">Note SQL Data Warehouse does not currently support @@NESTLEVEL.</span></span> <span data-ttu-id="04774-130">Bir iç içe geçirme düzeyi kendiniz izlenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="04774-130">You will need to keep a track of your nest level yourself.</span></span> <span data-ttu-id="04774-131">8 iç içe geçirme düzeyi sınırı karşılaşır ancak bunu yaparsanız bu sınırı içinde uyduğunu böylece kodunuzu yeniden çalışmaya ve "düzleştirmek" gerekir olası değil.</span><span class="sxs-lookup"><span data-stu-id="04774-131">It is unlikely you will hit the 8 nest level limit but if you do you will need to re-work your code and "flatten" it so that it fits within this limit.</span></span>

## <a name="insertexecute"></a><span data-ttu-id="04774-132">EKLE... YÜRÜTME</span><span class="sxs-lookup"><span data-stu-id="04774-132">INSERT..EXECUTE</span></span>
<span data-ttu-id="04774-133">SQL veri ambarı INSERT deyimi olan bir saklı yordam sonuç kümesini kullanmasına izin vermez.</span><span class="sxs-lookup"><span data-stu-id="04774-133">SQL Data Warehouse does not permit you to consume the result set of a stored procedure with an INSERT statement.</span></span> <span data-ttu-id="04774-134">Ancak, kullanabileceğiniz alternatif bir yaklaşım yoktur.</span><span class="sxs-lookup"><span data-stu-id="04774-134">However, there is an alternative approach you can use.</span></span>

<span data-ttu-id="04774-135">Lütfen üzerinde aşağıdaki makaleye bakın [geçici tablolara] bunun nasıl yapılacağı hakkında bir örnek.</span><span class="sxs-lookup"><span data-stu-id="04774-135">Please refer to the following article on [temporary tables] for an example on how to do this.</span></span>

## <a name="limitations"></a><span data-ttu-id="04774-136">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="04774-136">Limitations</span></span>
<span data-ttu-id="04774-137">SQL veri ambarı'nda uygulanmadı Transact-SQL saklı yordamları bazı yönleri vardır.</span><span class="sxs-lookup"><span data-stu-id="04774-137">There are some aspects of Transact-SQL stored procedures that are not implemented in SQL Data Warehouse.</span></span>

<span data-ttu-id="04774-138">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="04774-138">They are:</span></span>

* <span data-ttu-id="04774-139">geçici saklı yordamlar</span><span class="sxs-lookup"><span data-stu-id="04774-139">temporary stored procedures</span></span>
* <span data-ttu-id="04774-140">numaralandırılmış saklı yordamlar</span><span class="sxs-lookup"><span data-stu-id="04774-140">numbered stored procedures</span></span>
* <span data-ttu-id="04774-141">genişletilmiş saklı yordamlar</span><span class="sxs-lookup"><span data-stu-id="04774-141">extended stored procedures</span></span>
* <span data-ttu-id="04774-142">CLR saklı yordamlar</span><span class="sxs-lookup"><span data-stu-id="04774-142">CLR stored procedures</span></span>
* <span data-ttu-id="04774-143">şifreleme seçeneği</span><span class="sxs-lookup"><span data-stu-id="04774-143">encryption option</span></span>
* <span data-ttu-id="04774-144">çoğaltma seçeneği</span><span class="sxs-lookup"><span data-stu-id="04774-144">replication option</span></span>
* <span data-ttu-id="04774-145">Tablo değerli parametreleri</span><span class="sxs-lookup"><span data-stu-id="04774-145">table-valued parameters</span></span>
* <span data-ttu-id="04774-146">salt okunur parametreleri</span><span class="sxs-lookup"><span data-stu-id="04774-146">read-only parameters</span></span>
* <span data-ttu-id="04774-147">varsayılan parametreleri</span><span class="sxs-lookup"><span data-stu-id="04774-147">default parameters</span></span>
* <span data-ttu-id="04774-148">yürütme bağlamı</span><span class="sxs-lookup"><span data-stu-id="04774-148">execution contexts</span></span>
* <span data-ttu-id="04774-149">return deyimi</span><span class="sxs-lookup"><span data-stu-id="04774-149">return statement</span></span>

## <a name="next-steps"></a><span data-ttu-id="04774-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="04774-150">Next steps</span></span>
<span data-ttu-id="04774-151">Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].</span><span class="sxs-lookup"><span data-stu-id="04774-151">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
<span data-ttu-id="04774-152">[geçici tablolara]: ./sql-data-warehouse-tables-temporary.md#modularizing-code</span><span class="sxs-lookup"><span data-stu-id="04774-152">[temporary tables]: ./sql-data-warehouse-tables-temporary.md#modularizing-code</span></span>
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
