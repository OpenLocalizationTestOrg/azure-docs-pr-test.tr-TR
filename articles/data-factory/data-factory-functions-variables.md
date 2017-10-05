---
title: "Veri Fabrikası işlevleri ve sistem değişkenleri | Microsoft Docs"
description: "Azure Data Factory işlevler ve sistem değişkenleri listesini sağlar"
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 72a966bdc271f86b9568d3310d2e22d83b447594
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="74eeb-103">Azure Data Factory - işlevler ve sistem değişkenleri</span><span class="sxs-lookup"><span data-stu-id="74eeb-103">Azure Data Factory - Functions and System Variables</span></span>
<span data-ttu-id="74eeb-104">Bu makalede, işlevleri ve değişkenler Azure Data Factory ile desteklenen hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="74eeb-104">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="74eeb-105">Veri Fabrikası sistem değişkenleri</span><span class="sxs-lookup"><span data-stu-id="74eeb-105">Data Factory system variables</span></span>
| <span data-ttu-id="74eeb-106">Değişken adı</span><span class="sxs-lookup"><span data-stu-id="74eeb-106">Variable Name</span></span> | <span data-ttu-id="74eeb-107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="74eeb-107">Description</span></span> | <span data-ttu-id="74eeb-108">Nesne kapsamı</span><span class="sxs-lookup"><span data-stu-id="74eeb-108">Object Scope</span></span> | <span data-ttu-id="74eeb-109">JSON kapsamı ve kullanım örnekleri</span><span class="sxs-lookup"><span data-stu-id="74eeb-109">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="74eeb-110">WindowStart</span><span class="sxs-lookup"><span data-stu-id="74eeb-110">WindowStart</span></span> |<span data-ttu-id="74eeb-111">Geçerli etkinlik penceresini çalıştırmak için zaman aralığı başlangıcı</span><span class="sxs-lookup"><span data-stu-id="74eeb-111">Start of time interval for current activity run window</span></span> |<span data-ttu-id="74eeb-112">Etkinlik</span><span class="sxs-lookup"><span data-stu-id="74eeb-112">activity</span></span> |<ol><li><span data-ttu-id="74eeb-113">Veri seçimi sorguları belirtin.</span><span class="sxs-lookup"><span data-stu-id="74eeb-113">Specify data selection queries.</span></span> <span data-ttu-id="74eeb-114">Başvurulan bağlayıcı makalelerine bakın [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="74eeb-114">See connector articles referenced in the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="74eeb-115">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="74eeb-115">WindowEnd</span></span> |<span data-ttu-id="74eeb-116">Geçerli etkinlik penceresini çalıştırmak için zaman aralığı sonu</span><span class="sxs-lookup"><span data-stu-id="74eeb-116">End of time interval for current activity run window</span></span> |<span data-ttu-id="74eeb-117">Etkinlik</span><span class="sxs-lookup"><span data-stu-id="74eeb-117">activity</span></span> |<span data-ttu-id="74eeb-118">WindowStart ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="74eeb-118">same as WindowStart.</span></span> |
| <span data-ttu-id="74eeb-119">SliceStart</span><span class="sxs-lookup"><span data-stu-id="74eeb-119">SliceStart</span></span> |<span data-ttu-id="74eeb-120">Zaman aralığı için üretilen veri dilimi başlangıcı</span><span class="sxs-lookup"><span data-stu-id="74eeb-120">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="74eeb-121">Etkinlik</span><span class="sxs-lookup"><span data-stu-id="74eeb-121">activity</span></span><br/><span data-ttu-id="74eeb-122">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="74eeb-122">dataset</span></span> |<ol><li><span data-ttu-id="74eeb-123">Dinamik klasör yolu belirtin ve dosya adları ile çalışırken [Azure Blob](data-factory-azure-blob-connector.md) ve [dosya sistemi veri kümeleri](data-factory-onprem-file-system-connector.md).</span><span class="sxs-lookup"><span data-stu-id="74eeb-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="74eeb-124">Veri Fabrikası işlevleriyle etkinlik girişleri koleksiyonu giriş bağımlılıkları belirtin.</span><span class="sxs-lookup"><span data-stu-id="74eeb-124">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="74eeb-125">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="74eeb-125">SliceEnd</span></span> |<span data-ttu-id="74eeb-126">Geçerli veri dilimi için zaman aralığı sonu.</span><span class="sxs-lookup"><span data-stu-id="74eeb-126">End of time interval for current data slice.</span></span> |<span data-ttu-id="74eeb-127">Etkinlik</span><span class="sxs-lookup"><span data-stu-id="74eeb-127">activity</span></span><br/><span data-ttu-id="74eeb-128">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="74eeb-128">dataset</span></span> |<span data-ttu-id="74eeb-129">SliceStart ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="74eeb-129">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="74eeb-130">Şu anda veri fabrikası etkinliğin tam olarak belirtilen zamanlaması çıktı veri kümesi kullanılabilirliğini içinde belirtilen zamanlaması eşleştiğini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="74eeb-130">Currently data factory requires that the schedule specified in the activity exactly matches the schedule specified in availability of the output dataset.</span></span> <span data-ttu-id="74eeb-131">Bu nedenle, WindowStart, WindowEnd ve SliceStart ve SliceEnd her zaman aynı zaman dilimi ve tek bir çıktı dilim eşlenir.</span><span class="sxs-lookup"><span data-stu-id="74eeb-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map to the same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="74eeb-132">Bir sistem değişkeni kullanma örneği</span><span class="sxs-lookup"><span data-stu-id="74eeb-132">Example for using a system variable</span></span>
<span data-ttu-id="74eeb-133">Aşağıdaki örnek, yıl, ay, gün ve saati de **SliceStart** tarafından kullanılan ayrı değişkenleri içine ayıklanan **folderPath** ve **fileName** özellikleri.</span><span class="sxs-lookup"><span data-stu-id="74eeb-133">In the following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

## <a name="data-factory-functions"></a><span data-ttu-id="74eeb-134">Veri Fabrikası işlevleri</span><span class="sxs-lookup"><span data-stu-id="74eeb-134">Data Factory functions</span></span>
<span data-ttu-id="74eeb-135">Aşağıdaki amaçlarla sistem değişkenleri yanı sıra veri fabrikasında işlevleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="74eeb-135">You can use functions in data factory along with system variables for the following purposes:</span></span>

1. <span data-ttu-id="74eeb-136">Veri seçimi sorguları belirtme (başvurduğu bağlayıcı makalelerine bakın [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="74eeb-136">Specifying data selection queries (see connector articles referenced by the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="74eeb-137">Bir veri fabrikası işlevi çağırmak için söz dizimi:  **$$ <function>**  veri seçim sorguları ve diğer özellikleri etkinliği ve veri kümeleri için.</span><span class="sxs-lookup"><span data-stu-id="74eeb-137">The syntax to invoke a data factory function is: **$$<function>** for data selection queries and other properties in the activity and datasets.</span></span>  
2. <span data-ttu-id="74eeb-138">Veri Fabrikası işlevleriyle etkinlik girişleri koleksiyonu giriş bağımlılıkları belirtme.</span><span class="sxs-lookup"><span data-stu-id="74eeb-138">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="74eeb-139">$$ Giriş bağımlılık ifadeleri belirtmek için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="74eeb-139">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="74eeb-140">Aşağıdaki örnekte, **sqlReaderQuery** bir JSON dosyası bir özellik tarafından döndürülen bir değer atanması `Text.Format` işlevi.</span><span class="sxs-lookup"><span data-stu-id="74eeb-140">In the following sample, **sqlReaderQuery** property in a JSON file is assigned to a value returned by the `Text.Format` function.</span></span> <span data-ttu-id="74eeb-141">Bu örnek ayrıca adlı bir sistem değişkeni kullanır **WindowStart**, etkinlik penceresinin başlangıç zamanı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="74eeb-141">This sample also uses a system variable named **WindowStart**, which represents the start time of the activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="74eeb-142">Bkz: [özel tarih ve saat biçim dizeleri](https://msdn.microsoft.com/library/8kb3ddd4.aspx) kullanabileceğiniz farklı biçimlendirme seçenekleri açıklar konu (örneğin: yyyy karşılaştırması ay).</span><span class="sxs-lookup"><span data-stu-id="74eeb-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="74eeb-143">İşlevler</span><span class="sxs-lookup"><span data-stu-id="74eeb-143">Functions</span></span>
<span data-ttu-id="74eeb-144">Aşağıdaki tablolarda, Azure Data Factory uygulamasında tüm işlevleri listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="74eeb-144">The following tables list all the functions in Azure Data Factory:</span></span>

| <span data-ttu-id="74eeb-145">Kategori</span><span class="sxs-lookup"><span data-stu-id="74eeb-145">Category</span></span> | <span data-ttu-id="74eeb-146">İşlevi</span><span class="sxs-lookup"><span data-stu-id="74eeb-146">Function</span></span> | <span data-ttu-id="74eeb-147">Parametreler</span><span class="sxs-lookup"><span data-stu-id="74eeb-147">Parameters</span></span> | <span data-ttu-id="74eeb-148">Açıklama</span><span class="sxs-lookup"><span data-stu-id="74eeb-148">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="74eeb-149">Zaman</span><span class="sxs-lookup"><span data-stu-id="74eeb-149">Time</span></span> |<span data-ttu-id="74eeb-150">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="74eeb-150">AddHours(X,Y)</span></span> |<span data-ttu-id="74eeb-151">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="74eeb-151">X: DateTime</span></span> <br/><br/><span data-ttu-id="74eeb-152">Y: int</span><span class="sxs-lookup"><span data-stu-id="74eeb-152">Y: int</span></span> |<span data-ttu-id="74eeb-153">Y saatleri verilen süre X ekler.</span><span class="sxs-lookup"><span data-stu-id="74eeb-153">Adds Y hours to the given time X.</span></span> <br/><br/><span data-ttu-id="74eeb-154">Örnek:`9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="74eeb-154">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span></span> |
| <span data-ttu-id="74eeb-155">Zaman</span><span class="sxs-lookup"><span data-stu-id="74eeb-155">Time</span></span> |<span data-ttu-id="74eeb-156">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="74eeb-156">AddMinutes(X,Y)</span></span> |<span data-ttu-id="74eeb-157">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="74eeb-157">X: DateTime</span></span> <br/><br/><span data-ttu-id="74eeb-158">Y: int</span><span class="sxs-lookup"><span data-stu-id="74eeb-158">Y: int</span></span> |<span data-ttu-id="74eeb-159">Y dakika X ekler.</span><span class="sxs-lookup"><span data-stu-id="74eeb-159">Adds Y minutes to X.</span></span><br/><br/><span data-ttu-id="74eeb-160">Örnek:`9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span><span class="sxs-lookup"><span data-stu-id="74eeb-160">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span></span> |
| <span data-ttu-id="74eeb-161">Zaman</span><span class="sxs-lookup"><span data-stu-id="74eeb-161">Time</span></span> |<span data-ttu-id="74eeb-162">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="74eeb-162">StartOfHour(X)</span></span> |<span data-ttu-id="74eeb-163">X: Datetime</span><span class="sxs-lookup"><span data-stu-id="74eeb-163">X: Datetime</span></span> |<span data-ttu-id="74eeb-164">X saat bileşeni tarafından temsil edilen bir saat için başlangıç saatini alır.</span><span class="sxs-lookup"><span data-stu-id="74eeb-164">Gets the starting time for the hour represented by the hour component of X.</span></span> <br/><br/><span data-ttu-id="74eeb-165">Örnek:`StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="74eeb-165">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span></span> |
| <span data-ttu-id="74eeb-166">Tarih</span><span class="sxs-lookup"><span data-stu-id="74eeb-166">Date</span></span> |<span data-ttu-id="74eeb-167">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="74eeb-167">AddDays(X,Y)</span></span> |<span data-ttu-id="74eeb-168">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="74eeb-168">X: DateTime</span></span><br/><br/><span data-ttu-id="74eeb-169">Y: int</span><span class="sxs-lookup"><span data-stu-id="74eeb-169">Y: int</span></span> |<span data-ttu-id="74eeb-170">Y günleri X ekler.</span><span class="sxs-lookup"><span data-stu-id="74eeb-170">Adds Y days to X.</span></span> <br/><br/><span data-ttu-id="74eeb-171">Örnek: 9/15/2013 12:00:00 PM + 2 gün = 9/17/2013 12:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="74eeb-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="74eeb-172">Negatif bir sayı Y belirterek gün çok çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74eeb-172">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="74eeb-173">Örnek: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="74eeb-173">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="74eeb-174">Tarih</span><span class="sxs-lookup"><span data-stu-id="74eeb-174">Date</span></span> |<span data-ttu-id="74eeb-175">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="74eeb-175">AddMonths(X,Y)</span></span> |<span data-ttu-id="74eeb-176">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="74eeb-176">X: DateTime</span></span><br/><br/><span data-ttu-id="74eeb-177">Y: int</span><span class="sxs-lookup"><span data-stu-id="74eeb-177">Y: int</span></span> |<span data-ttu-id="74eeb-178">X Y ay ekler.</span><span class="sxs-lookup"><span data-stu-id="74eeb-178">Adds Y months to X.</span></span><br/><br/><span data-ttu-id="74eeb-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="74eeb-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span></span><br/><br/><span data-ttu-id="74eeb-180">Negatif bir sayı Y belirterek ay çok çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74eeb-180">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="74eeb-181">Örnek: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="74eeb-181">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span></span>|
| <span data-ttu-id="74eeb-182">Tarih</span><span class="sxs-lookup"><span data-stu-id="74eeb-182">Date</span></span> |<span data-ttu-id="74eeb-183">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="74eeb-183">AddQuarters(X,Y)</span></span> |<span data-ttu-id="74eeb-184">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="74eeb-184">X: DateTime</span></span> <br/><br/><span data-ttu-id="74eeb-185">Y: int</span><span class="sxs-lookup"><span data-stu-id="74eeb-185">Y: int</span></span> |<span data-ttu-id="74eeb-186">Y ekler * x 3 ay.</span><span class="sxs-lookup"><span data-stu-id="74eeb-186">Adds Y * 3 months to X.</span></span><br/><br/><span data-ttu-id="74eeb-187">Örnek:`9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="74eeb-187">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span></span> |
| <span data-ttu-id="74eeb-188">Tarih</span><span class="sxs-lookup"><span data-stu-id="74eeb-188">Date</span></span> |<span data-ttu-id="74eeb-189">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="74eeb-189">AddWeeks(X,Y)</span></span> |<span data-ttu-id="74eeb-190">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="74eeb-190">X: DateTime</span></span><br/><br/><span data-ttu-id="74eeb-191">Y: int</span><span class="sxs-lookup"><span data-stu-id="74eeb-191">Y: int</span></span> |<span data-ttu-id="74eeb-192">Y ekler * x 7 gün</span><span class="sxs-lookup"><span data-stu-id="74eeb-192">Adds Y * 7 days to X</span></span><br/><br/><span data-ttu-id="74eeb-193">Örnek: 9/15/2013 12:00:00 PM + 1 hafta = 9/22/2013 12:00:00 PM</span><span class="sxs-lookup"><span data-stu-id="74eeb-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="74eeb-194">Negatif bir sayı Y belirterek hafta çok çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74eeb-194">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="74eeb-195">Örnek: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="74eeb-195">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="74eeb-196">Tarih</span><span class="sxs-lookup"><span data-stu-id="74eeb-196">Date</span></span> |<span data-ttu-id="74eeb-197">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="74eeb-197">AddYears(X,Y)</span></span> |<span data-ttu-id="74eeb-198">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="74eeb-198">X: DateTime</span></span><br/><br/><span data-ttu-id="74eeb-199">Y: int</span><span class="sxs-lookup"><span data-stu-id="74eeb-199">Y: int</span></span> |<span data-ttu-id="74eeb-200">Y yıl X ekler.</span><span class="sxs-lookup"><span data-stu-id="74eeb-200">Adds Y years to X.</span></span><br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/><span data-ttu-id="74eeb-201">Negatif bir sayı Y belirterek yıl çok çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74eeb-201">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="74eeb-202">Örnek: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="74eeb-202">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span></span> |
| <span data-ttu-id="74eeb-203">Tarih</span><span class="sxs-lookup"><span data-stu-id="74eeb-203">Date</span></span> |<span data-ttu-id="74eeb-204">Day(X)</span><span class="sxs-lookup"><span data-stu-id="74eeb-204">Day(X)</span></span> |<span data-ttu-id="74eeb-205">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="74eeb-205">X: DateTime</span></span> |<span data-ttu-id="74eeb-206">X değerinin gün bileşenini alır.</span><span class="sxs-lookup"><span data-stu-id="74eeb-206">Gets the day component of X.</span></span><br/><br/><span data-ttu-id="74eeb-207">Örnek: `Day of 9/15/2013 12:00:00 PM is 9`.</span><span class="sxs-lookup"><span data-stu-id="74eeb-207">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span></span> |
| <span data-ttu-id="74eeb-208">Tarih</span><span class="sxs-lookup"><span data-stu-id="74eeb-208">Date</span></span> |<span data-ttu-id="74eeb-209">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="74eeb-209">DayOfWeek(X)</span></span> |<span data-ttu-id="74eeb-210">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="74eeb-210">X: DateTime</span></span> |<span data-ttu-id="74eeb-211">Haftanın günü bileşenini x alır.</span><span class="sxs-lookup"><span data-stu-id="74eeb-211">Gets the day of week component of X.</span></span><br/><br/><span data-ttu-id="74eeb-212">Örnek: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span><span class="sxs-lookup"><span data-stu-id="74eeb-212">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span></span> |
| <span data-ttu-id="74eeb-213">Tarih</span><span class="sxs-lookup"><span data-stu-id="74eeb-213">Date</span></span> |<span data-ttu-id="74eeb-214">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="74eeb-214">DayOfYear(X)</span></span> |<span data-ttu-id="74eeb-215">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="74eeb-215">X: DateTime</span></span> |<span data-ttu-id="74eeb-216">X yıl bileşenini tarafından temsil edilen yılın günü alır.</span><span class="sxs-lookup"><span data-stu-id="74eeb-216">Gets the day in the year represented by the year component of X.</span></span><br/><br/><span data-ttu-id="74eeb-217">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="74eeb-217">Examples:</span></span><br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| <span data-ttu-id="74eeb-218">Tarih</span><span class="sxs-lookup"><span data-stu-id="74eeb-218">Date</span></span> |<span data-ttu-id="74eeb-219">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="74eeb-219">DaysInMonth(X)</span></span> |<span data-ttu-id="74eeb-220">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="74eeb-220">X: DateTime</span></span> |<span data-ttu-id="74eeb-221">X parametresi ay bileşenini tarafından temsil edilen aydaki gün alır.</span><span class="sxs-lookup"><span data-stu-id="74eeb-221">Gets the days in the month represented by the month component of parameter X.</span></span><br/><br/><span data-ttu-id="74eeb-222">Örnek: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month`.</span><span class="sxs-lookup"><span data-stu-id="74eeb-222">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month`.</span></span> |
| <span data-ttu-id="74eeb-223">Tarih</span><span class="sxs-lookup"><span data-stu-id="74eeb-223">Date</span></span> |<span data-ttu-id="74eeb-224">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="74eeb-224">EndOfDay(X)</span></span> |<span data-ttu-id="74eeb-225">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="74eeb-225">X: DateTime</span></span> |<span data-ttu-id="74eeb-226">Tarih-saat x (gün bileşenini) gün sonunu temsil eden alır.</span><span class="sxs-lookup"><span data-stu-id="74eeb-226">Gets the date-time that represents the end of the day (day component) of X.</span></span><br/><br/><span data-ttu-id="74eeb-227">Örnek: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span><span class="sxs-lookup"><span data-stu-id="74eeb-227">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span></span> |
| <span data-ttu-id="74eeb-228">Tarih</span><span class="sxs-lookup"><span data-stu-id="74eeb-228">Date</span></span> |<span data-ttu-id="74eeb-229">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="74eeb-229">EndOfMonth(X)</span></span> |<span data-ttu-id="74eeb-230">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="74eeb-230">X: DateTime</span></span> |<span data-ttu-id="74eeb-231">X parametresi ay bileşen tarafından temsil edilen ayın sonunu alır.</span><span class="sxs-lookup"><span data-stu-id="74eeb-231">Gets the end of the month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="74eeb-232">Örnek: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (güncel Eylül ayın sonunu temsil eden saat)</span><span class="sxs-lookup"><span data-stu-id="74eeb-232">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents the end of September month)</span></span> |
| <span data-ttu-id="74eeb-233">Tarih</span><span class="sxs-lookup"><span data-stu-id="74eeb-233">Date</span></span> |<span data-ttu-id="74eeb-234">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="74eeb-234">StartOfDay(X)</span></span> |<span data-ttu-id="74eeb-235">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="74eeb-235">X: DateTime</span></span> |<span data-ttu-id="74eeb-236">X parametresi gün bileşeni tarafından temsil edilen günün başlangıcını alır.</span><span class="sxs-lookup"><span data-stu-id="74eeb-236">Gets the start of the day represented by the day component of parameter X.</span></span><br/><br/><span data-ttu-id="74eeb-237">Örnek: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span><span class="sxs-lookup"><span data-stu-id="74eeb-237">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span></span> |
| <span data-ttu-id="74eeb-238">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="74eeb-238">DateTime</span></span> |<span data-ttu-id="74eeb-239">FROM(X)</span><span class="sxs-lookup"><span data-stu-id="74eeb-239">From(X)</span></span> |<span data-ttu-id="74eeb-240">X: dize</span><span class="sxs-lookup"><span data-stu-id="74eeb-240">X: String</span></span> |<span data-ttu-id="74eeb-241">Tarih saat X dizeye ayrıştırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="74eeb-241">Parse string X to a date time.</span></span> |
| <span data-ttu-id="74eeb-242">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="74eeb-242">DateTime</span></span> |<span data-ttu-id="74eeb-243">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="74eeb-243">Ticks(X)</span></span> |<span data-ttu-id="74eeb-244">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="74eeb-244">X: DateTime</span></span> |<span data-ttu-id="74eeb-245">Ticks X parametresi özelliğini alır. Bir değer 100 nanosaniye eşittir.</span><span class="sxs-lookup"><span data-stu-id="74eeb-245">Gets the ticks property of the parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="74eeb-246">Bu özelliğin değeri, 12:00:00 gece'den itibaren 1 Ocak 0001 geçen çizgilerine sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="74eeb-246">The value of this property represents the number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="74eeb-247">Metin</span><span class="sxs-lookup"><span data-stu-id="74eeb-247">Text</span></span> |<span data-ttu-id="74eeb-248">Format(X)</span><span class="sxs-lookup"><span data-stu-id="74eeb-248">Format(X)</span></span> |<span data-ttu-id="74eeb-249">X: Dize değişkeni</span><span class="sxs-lookup"><span data-stu-id="74eeb-249">X: String variable</span></span> |<span data-ttu-id="74eeb-250">Metin biçimleri (kullanmak `\\'` kaçınmak için birleşimi `'` karakter).</span><span class="sxs-lookup"><span data-stu-id="74eeb-250">Formats the text (use `\\'` combination to escape `'` character).</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="74eeb-251">Başka bir işlev içinde bir işlevi kullanılırken kullanmak gerekmez  **$$**  iç işlevi için önek.</span><span class="sxs-lookup"><span data-stu-id="74eeb-251">When using a function within another function, you do not need to use **$$** prefix for the inner function.</span></span> <span data-ttu-id="74eeb-252">Örneğin: $$Text.Format ('PartitionKey eq \\' my_pkey_filter_value\\' ve RowKey ge \\' {0: yyyy-aa-gg ss: dd:}\\'', Time.AddHours (SliceStart, -6)).</span><span class="sxs-lookup"><span data-stu-id="74eeb-252">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="74eeb-253">Bu örnekte, dikkat  **$$**  için önek kullanılmaz **Time.AddHours** işlevi.</span><span class="sxs-lookup"><span data-stu-id="74eeb-253">In this example, notice that **$$** prefix is not used for the **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="74eeb-254">Örnek</span><span class="sxs-lookup"><span data-stu-id="74eeb-254">Example</span></span>
<span data-ttu-id="74eeb-255">Aşağıdaki örnekte, Hive etkinliği için girdi ve çıktı parametreleri kullanılarak belirlenir `Text.Format` işlevi ve SliceStart sistem değişkeni.</span><span class="sxs-lookup"><span data-stu-id="74eeb-255">In the following example, input and output parameters for the Hive activity are determined by using the `Text.Format` function and SliceStart system variable.</span></span> 

```json  
{
    "name": "HiveActivitySamplePipeline",
        "properties": {
    "activities": [
            {
            "name": "HiveActivitySample",
            "type": "HDInsightHive",
            "inputs": [
                    {
                    "name": "HiveSampleIn"
                    }
            ],
            "outputs": [
                    {
                    "name": "HiveSampleOut"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                }
            }
            }
    ]
    }
}
```

### <a name="example-2"></a><span data-ttu-id="74eeb-256">Örnek 2</span><span class="sxs-lookup"><span data-stu-id="74eeb-256">Example 2</span></span>

<span data-ttu-id="74eeb-257">Aşağıdaki örnekte, DateTime parametresi saklı yordam etkinliği için metin kullanılarak belirlenir.</span><span class="sxs-lookup"><span data-stu-id="74eeb-257">In the following example, the DateTime parameter for the Stored Procedure Activity is determined by using the Text.</span></span> <span data-ttu-id="74eeb-258">İşlev ve SliceStart değişkeni biçimlendirin.</span><span class="sxs-lookup"><span data-stu-id="74eeb-258">Format function and the SliceStart variable.</span></span> 

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
            "start": "2016-08-02T00:00:00Z",
            "end": "2016-08-02T05:00:00Z",
        "isPaused": false
    }
}
```

### <a name="example-3"></a><span data-ttu-id="74eeb-259">Örnek 3</span><span class="sxs-lookup"><span data-stu-id="74eeb-259">Example 3</span></span>
<span data-ttu-id="74eeb-260">SliceStart tarafından temsil edilen gün yerine önceki gün verilerini okumak için aşağıdaki örnekte gösterildiği gibi AddDays işlevini kullanın:</span><span class="sxs-lookup"><span data-stu-id="74eeb-260">To read data from previous day instead of day represented by the SliceStart, use the AddDays function as shown in the following example:</span></span> 

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-01-01T08:00:00",
        "end": "2017-01-01T11:00:00",
        "description": "hive activity",
        "activities": [
            {
                "name": "SampleHiveActivity",
                "inputs": [
                    {
                        "name": "MyAzureBlobInput",
                        "startTime": "Date.AddDays(SliceStart, -1)",
                        "endTime": "Date.AddDays(SliceEnd, -1)"
                    }
                ],
                "outputs": [
                    {
                        "name": "MyAzureBlobOutput"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adftutorial\\hivequery.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Year": "$$Text.Format('{0:yyyy}',WindowsStart)",
                        "Month": "$$Text.Format('{0:MM}',WindowStart)",
                        "Day": "$$Text.Format('{0:dd}',WindowStart)"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "OldestFirst",
                    "retry": 2,
                    "timeout": "01:00:00"
                }
            }
        ]
    }
}
```

<span data-ttu-id="74eeb-261">Bkz: [özel tarih ve saat biçim dizeleri](https://msdn.microsoft.com/library/8kb3ddd4.aspx) kullanabileceğiniz farklı biçimlendirme seçenekleri açıklar konu (örneğin: yy yyyy karşılaştırması).</span><span class="sxs-lookup"><span data-stu-id="74eeb-261">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

