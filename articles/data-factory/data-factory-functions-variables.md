---
title: "aaaData Fabrika işlevler ve sistem değişkenleri | Microsoft Docs"
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
ms.openlocfilehash: d2936c2821797947bb37d9775226a6c19c4b8ab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="df02c-103">Azure Data Factory - işlevler ve sistem değişkenleri</span><span class="sxs-lookup"><span data-stu-id="df02c-103">Azure Data Factory - Functions and System Variables</span></span>
<span data-ttu-id="df02c-104">Bu makalede, işlevleri ve değişkenler Azure Data Factory ile desteklenen hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="df02c-104">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="df02c-105">Veri Fabrikası sistem değişkenleri</span><span class="sxs-lookup"><span data-stu-id="df02c-105">Data Factory system variables</span></span>
| <span data-ttu-id="df02c-106">Değişken adı</span><span class="sxs-lookup"><span data-stu-id="df02c-106">Variable Name</span></span> | <span data-ttu-id="df02c-107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="df02c-107">Description</span></span> | <span data-ttu-id="df02c-108">Nesne kapsamı</span><span class="sxs-lookup"><span data-stu-id="df02c-108">Object Scope</span></span> | <span data-ttu-id="df02c-109">JSON kapsamı ve kullanım örnekleri</span><span class="sxs-lookup"><span data-stu-id="df02c-109">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="df02c-110">WindowStart</span><span class="sxs-lookup"><span data-stu-id="df02c-110">WindowStart</span></span> |<span data-ttu-id="df02c-111">Geçerli etkinlik penceresini çalıştırmak için zaman aralığı başlangıcı</span><span class="sxs-lookup"><span data-stu-id="df02c-111">Start of time interval for current activity run window</span></span> |<span data-ttu-id="df02c-112">Etkinlik</span><span class="sxs-lookup"><span data-stu-id="df02c-112">activity</span></span> |<ol><li><span data-ttu-id="df02c-113">Veri seçimi sorguları belirtin.</span><span class="sxs-lookup"><span data-stu-id="df02c-113">Specify data selection queries.</span></span> <span data-ttu-id="df02c-114">Hello başvurulan bağlayıcı makalelerine bakın [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="df02c-114">See connector articles referenced in hello [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="df02c-115">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="df02c-115">WindowEnd</span></span> |<span data-ttu-id="df02c-116">Geçerli etkinlik penceresini çalıştırmak için zaman aralığı sonu</span><span class="sxs-lookup"><span data-stu-id="df02c-116">End of time interval for current activity run window</span></span> |<span data-ttu-id="df02c-117">Etkinlik</span><span class="sxs-lookup"><span data-stu-id="df02c-117">activity</span></span> |<span data-ttu-id="df02c-118">WindowStart ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="df02c-118">same as WindowStart.</span></span> |
| <span data-ttu-id="df02c-119">SliceStart</span><span class="sxs-lookup"><span data-stu-id="df02c-119">SliceStart</span></span> |<span data-ttu-id="df02c-120">Zaman aralığı için üretilen veri dilimi başlangıcı</span><span class="sxs-lookup"><span data-stu-id="df02c-120">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="df02c-121">Etkinlik</span><span class="sxs-lookup"><span data-stu-id="df02c-121">activity</span></span><br/><span data-ttu-id="df02c-122">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="df02c-122">dataset</span></span> |<ol><li><span data-ttu-id="df02c-123">Dinamik klasör yolu belirtin ve dosya adları ile çalışırken [Azure Blob](data-factory-azure-blob-connector.md) ve [dosya sistemi veri kümeleri](data-factory-onprem-file-system-connector.md).</span><span class="sxs-lookup"><span data-stu-id="df02c-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="df02c-124">Veri Fabrikası işlevleriyle etkinlik girişleri koleksiyonu giriş bağımlılıkları belirtin.</span><span class="sxs-lookup"><span data-stu-id="df02c-124">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="df02c-125">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="df02c-125">SliceEnd</span></span> |<span data-ttu-id="df02c-126">Geçerli veri dilimi için zaman aralığı sonu.</span><span class="sxs-lookup"><span data-stu-id="df02c-126">End of time interval for current data slice.</span></span> |<span data-ttu-id="df02c-127">Etkinlik</span><span class="sxs-lookup"><span data-stu-id="df02c-127">activity</span></span><br/><span data-ttu-id="df02c-128">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="df02c-128">dataset</span></span> |<span data-ttu-id="df02c-129">SliceStart ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="df02c-129">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="df02c-130">Veri Fabrikası bu hello zamanlama içinde belirtilen hello gerektirir şu anda etkinlik hello çıkış dataset kullanılabilirliği içinde belirtilen hello zamanlaması tam olarak eşleşir.</span><span class="sxs-lookup"><span data-stu-id="df02c-130">Currently data factory requires that hello schedule specified in hello activity exactly matches hello schedule specified in availability of hello output dataset.</span></span> <span data-ttu-id="df02c-131">Bu nedenle, WindowStart, WindowEnd ve SliceStart ve SliceEnd her zaman toohello eşleme aynı zaman dönemi ve tek bir çıktı dilim.</span><span class="sxs-lookup"><span data-stu-id="df02c-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map toohello same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="df02c-132">Bir sistem değişkeni kullanma örneği</span><span class="sxs-lookup"><span data-stu-id="df02c-132">Example for using a system variable</span></span>
<span data-ttu-id="df02c-133">Aşağıdaki örnek, yıl, ay, gün ve saat hello içinde **SliceStart** tarafından kullanılan ayrı değişkenleri içine ayıklanan **folderPath** ve **fileName** özellikleri.</span><span class="sxs-lookup"><span data-stu-id="df02c-133">In hello following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span></span>

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

## <a name="data-factory-functions"></a><span data-ttu-id="df02c-134">Veri Fabrikası işlevleri</span><span class="sxs-lookup"><span data-stu-id="df02c-134">Data Factory functions</span></span>
<span data-ttu-id="df02c-135">Merhaba amacıyla aşağıdaki sistem değişkenleri yanı sıra veri fabrikasında işlevleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="df02c-135">You can use functions in data factory along with system variables for hello following purposes:</span></span>

1. <span data-ttu-id="df02c-136">Veri seçimi sorguları belirtme (Merhaba tarafından başvurulan bağlayıcı makalelerine bakın [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="df02c-136">Specifying data selection queries (see connector articles referenced by hello [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="df02c-137">Veri Fabrikası işlevi sözdizimi tooinvoke hello:  **$$ <function>**  veri seçim sorguları ve diğer özellikleri hello etkinliği ve veri kümeleri için.</span><span class="sxs-lookup"><span data-stu-id="df02c-137">hello syntax tooinvoke a data factory function is: **$$<function>** for data selection queries and other properties in hello activity and datasets.</span></span>  
2. <span data-ttu-id="df02c-138">Veri Fabrikası işlevleriyle etkinlik girişleri koleksiyonu giriş bağımlılıkları belirtme.</span><span class="sxs-lookup"><span data-stu-id="df02c-138">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="df02c-139">$$ Giriş bağımlılık ifadeleri belirtmek için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="df02c-139">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="df02c-140">Aşağıdaki örnek, hello içinde **sqlReaderQuery** bir JSON dosyası özelliğinde hello tarafından döndürülen tooa değeri atanmış `Text.Format` işlevi.</span><span class="sxs-lookup"><span data-stu-id="df02c-140">In hello following sample, **sqlReaderQuery** property in a JSON file is assigned tooa value returned by hello `Text.Format` function.</span></span> <span data-ttu-id="df02c-141">Bu örnek ayrıca adlı bir sistem değişkeni kullanır **WindowStart**, penceresi hello aktivitesinin hello başlangıç saati temsil eder.</span><span class="sxs-lookup"><span data-stu-id="df02c-141">This sample also uses a system variable named **WindowStart**, which represents hello start time of hello activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="df02c-142">Bkz: [özel tarih ve saat biçim dizeleri](https://msdn.microsoft.com/library/8kb3ddd4.aspx) kullanabileceğiniz farklı biçimlendirme seçenekleri açıklar konu (örneğin: yyyy karşılaştırması ay).</span><span class="sxs-lookup"><span data-stu-id="df02c-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="df02c-143">İşlevler</span><span class="sxs-lookup"><span data-stu-id="df02c-143">Functions</span></span>
<span data-ttu-id="df02c-144">Aşağıdaki tablolar hello Azure Data Factory tüm hello işlevlerde listesi:</span><span class="sxs-lookup"><span data-stu-id="df02c-144">hello following tables list all hello functions in Azure Data Factory:</span></span>

| <span data-ttu-id="df02c-145">Kategori</span><span class="sxs-lookup"><span data-stu-id="df02c-145">Category</span></span> | <span data-ttu-id="df02c-146">İşlevi</span><span class="sxs-lookup"><span data-stu-id="df02c-146">Function</span></span> | <span data-ttu-id="df02c-147">Parametreler</span><span class="sxs-lookup"><span data-stu-id="df02c-147">Parameters</span></span> | <span data-ttu-id="df02c-148">Açıklama</span><span class="sxs-lookup"><span data-stu-id="df02c-148">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="df02c-149">Zaman</span><span class="sxs-lookup"><span data-stu-id="df02c-149">Time</span></span> |<span data-ttu-id="df02c-150">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="df02c-150">AddHours(X,Y)</span></span> |<span data-ttu-id="df02c-151">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="df02c-151">X: DateTime</span></span> <br/><br/><span data-ttu-id="df02c-152">Y: int</span><span class="sxs-lookup"><span data-stu-id="df02c-152">Y: int</span></span> |<span data-ttu-id="df02c-153">Y saatleri toohello zaman X verilen ekler.</span><span class="sxs-lookup"><span data-stu-id="df02c-153">Adds Y hours toohello given time X.</span></span> <br/><br/><span data-ttu-id="df02c-154">Örnek:`9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="df02c-154">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span></span> |
| <span data-ttu-id="df02c-155">Zaman</span><span class="sxs-lookup"><span data-stu-id="df02c-155">Time</span></span> |<span data-ttu-id="df02c-156">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="df02c-156">AddMinutes(X,Y)</span></span> |<span data-ttu-id="df02c-157">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="df02c-157">X: DateTime</span></span> <br/><br/><span data-ttu-id="df02c-158">Y: int</span><span class="sxs-lookup"><span data-stu-id="df02c-158">Y: int</span></span> |<span data-ttu-id="df02c-159">Y dakika tooX ekler.</span><span class="sxs-lookup"><span data-stu-id="df02c-159">Adds Y minutes tooX.</span></span><br/><br/><span data-ttu-id="df02c-160">Örnek:`9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span><span class="sxs-lookup"><span data-stu-id="df02c-160">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span></span> |
| <span data-ttu-id="df02c-161">Zaman</span><span class="sxs-lookup"><span data-stu-id="df02c-161">Time</span></span> |<span data-ttu-id="df02c-162">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="df02c-162">StartOfHour(X)</span></span> |<span data-ttu-id="df02c-163">X: Datetime</span><span class="sxs-lookup"><span data-stu-id="df02c-163">X: Datetime</span></span> |<span data-ttu-id="df02c-164">Hello için x hello saat bileşeni tarafından temsil edilen hello saat başlangıç saati alır.</span><span class="sxs-lookup"><span data-stu-id="df02c-164">Gets hello starting time for hello hour represented by hello hour component of X.</span></span> <br/><br/><span data-ttu-id="df02c-165">Örnek:`StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="df02c-165">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span></span> |
| <span data-ttu-id="df02c-166">Tarih</span><span class="sxs-lookup"><span data-stu-id="df02c-166">Date</span></span> |<span data-ttu-id="df02c-167">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="df02c-167">AddDays(X,Y)</span></span> |<span data-ttu-id="df02c-168">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="df02c-168">X: DateTime</span></span><br/><br/><span data-ttu-id="df02c-169">Y: int</span><span class="sxs-lookup"><span data-stu-id="df02c-169">Y: int</span></span> |<span data-ttu-id="df02c-170">Y gün tooX ekler.</span><span class="sxs-lookup"><span data-stu-id="df02c-170">Adds Y days tooX.</span></span> <br/><br/><span data-ttu-id="df02c-171">Örnek: 9/15/2013 12:00:00 PM + 2 gün = 9/17/2013 12:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="df02c-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="df02c-172">Negatif bir sayı Y belirterek gün çok çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df02c-172">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="df02c-173">Örnek: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="df02c-173">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="df02c-174">Tarih</span><span class="sxs-lookup"><span data-stu-id="df02c-174">Date</span></span> |<span data-ttu-id="df02c-175">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="df02c-175">AddMonths(X,Y)</span></span> |<span data-ttu-id="df02c-176">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="df02c-176">X: DateTime</span></span><br/><br/><span data-ttu-id="df02c-177">Y: int</span><span class="sxs-lookup"><span data-stu-id="df02c-177">Y: int</span></span> |<span data-ttu-id="df02c-178">Y ay tooX ekler.</span><span class="sxs-lookup"><span data-stu-id="df02c-178">Adds Y months tooX.</span></span><br/><br/><span data-ttu-id="df02c-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="df02c-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span></span><br/><br/><span data-ttu-id="df02c-180">Negatif bir sayı Y belirterek ay çok çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df02c-180">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="df02c-181">Örnek: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="df02c-181">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span></span>|
| <span data-ttu-id="df02c-182">Tarih</span><span class="sxs-lookup"><span data-stu-id="df02c-182">Date</span></span> |<span data-ttu-id="df02c-183">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="df02c-183">AddQuarters(X,Y)</span></span> |<span data-ttu-id="df02c-184">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="df02c-184">X: DateTime</span></span> <br/><br/><span data-ttu-id="df02c-185">Y: int</span><span class="sxs-lookup"><span data-stu-id="df02c-185">Y: int</span></span> |<span data-ttu-id="df02c-186">Y ekler * 3 ay tooX.</span><span class="sxs-lookup"><span data-stu-id="df02c-186">Adds Y * 3 months tooX.</span></span><br/><br/><span data-ttu-id="df02c-187">Örnek:`9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="df02c-187">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span></span> |
| <span data-ttu-id="df02c-188">Tarih</span><span class="sxs-lookup"><span data-stu-id="df02c-188">Date</span></span> |<span data-ttu-id="df02c-189">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="df02c-189">AddWeeks(X,Y)</span></span> |<span data-ttu-id="df02c-190">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="df02c-190">X: DateTime</span></span><br/><br/><span data-ttu-id="df02c-191">Y: int</span><span class="sxs-lookup"><span data-stu-id="df02c-191">Y: int</span></span> |<span data-ttu-id="df02c-192">Y ekler * 7 gün tooX</span><span class="sxs-lookup"><span data-stu-id="df02c-192">Adds Y * 7 days tooX</span></span><br/><br/><span data-ttu-id="df02c-193">Örnek: 9/15/2013 12:00:00 PM + 1 hafta = 9/22/2013 12:00:00 PM</span><span class="sxs-lookup"><span data-stu-id="df02c-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="df02c-194">Negatif bir sayı Y belirterek hafta çok çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df02c-194">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="df02c-195">Örnek: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="df02c-195">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="df02c-196">Tarih</span><span class="sxs-lookup"><span data-stu-id="df02c-196">Date</span></span> |<span data-ttu-id="df02c-197">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="df02c-197">AddYears(X,Y)</span></span> |<span data-ttu-id="df02c-198">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="df02c-198">X: DateTime</span></span><br/><br/><span data-ttu-id="df02c-199">Y: int</span><span class="sxs-lookup"><span data-stu-id="df02c-199">Y: int</span></span> |<span data-ttu-id="df02c-200">Y yıl tooX ekler.</span><span class="sxs-lookup"><span data-stu-id="df02c-200">Adds Y years tooX.</span></span><br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/><span data-ttu-id="df02c-201">Negatif bir sayı Y belirterek yıl çok çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df02c-201">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="df02c-202">Örnek: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="df02c-202">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span></span> |
| <span data-ttu-id="df02c-203">Tarih</span><span class="sxs-lookup"><span data-stu-id="df02c-203">Date</span></span> |<span data-ttu-id="df02c-204">Day(X)</span><span class="sxs-lookup"><span data-stu-id="df02c-204">Day(X)</span></span> |<span data-ttu-id="df02c-205">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="df02c-205">X: DateTime</span></span> |<span data-ttu-id="df02c-206">X Hello gün bileşenini alır.</span><span class="sxs-lookup"><span data-stu-id="df02c-206">Gets hello day component of X.</span></span><br/><br/><span data-ttu-id="df02c-207">Örnek: `Day of 9/15/2013 12:00:00 PM is 9`.</span><span class="sxs-lookup"><span data-stu-id="df02c-207">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span></span> |
| <span data-ttu-id="df02c-208">Tarih</span><span class="sxs-lookup"><span data-stu-id="df02c-208">Date</span></span> |<span data-ttu-id="df02c-209">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="df02c-209">DayOfWeek(X)</span></span> |<span data-ttu-id="df02c-210">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="df02c-210">X: DateTime</span></span> |<span data-ttu-id="df02c-211">Merhaba haftanın günü bileşenini x alır.</span><span class="sxs-lookup"><span data-stu-id="df02c-211">Gets hello day of week component of X.</span></span><br/><br/><span data-ttu-id="df02c-212">Örnek: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span><span class="sxs-lookup"><span data-stu-id="df02c-212">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span></span> |
| <span data-ttu-id="df02c-213">Tarih</span><span class="sxs-lookup"><span data-stu-id="df02c-213">Date</span></span> |<span data-ttu-id="df02c-214">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="df02c-214">DayOfYear(X)</span></span> |<span data-ttu-id="df02c-215">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="df02c-215">X: DateTime</span></span> |<span data-ttu-id="df02c-216">Merhaba gün hello yıl bileşenini X tarafından temsil edilen hello yıl içinde alır.</span><span class="sxs-lookup"><span data-stu-id="df02c-216">Gets hello day in hello year represented by hello year component of X.</span></span><br/><br/><span data-ttu-id="df02c-217">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="df02c-217">Examples:</span></span><br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| <span data-ttu-id="df02c-218">Tarih</span><span class="sxs-lookup"><span data-stu-id="df02c-218">Date</span></span> |<span data-ttu-id="df02c-219">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="df02c-219">DaysInMonth(X)</span></span> |<span data-ttu-id="df02c-220">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="df02c-220">X: DateTime</span></span> |<span data-ttu-id="df02c-221">Merhaba gün hello ay bileşenini X parametresi tarafından temsil edilen hello ay içinde alır.</span><span class="sxs-lookup"><span data-stu-id="df02c-221">Gets hello days in hello month represented by hello month component of parameter X.</span></span><br/><br/><span data-ttu-id="df02c-222">Örnek: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`.</span><span class="sxs-lookup"><span data-stu-id="df02c-222">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`.</span></span> |
| <span data-ttu-id="df02c-223">Tarih</span><span class="sxs-lookup"><span data-stu-id="df02c-223">Date</span></span> |<span data-ttu-id="df02c-224">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="df02c-224">EndOfDay(X)</span></span> |<span data-ttu-id="df02c-225">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="df02c-225">X: DateTime</span></span> |<span data-ttu-id="df02c-226">Merhaba son X hello gününün (gün bileşenini) temsil eden Hello tarih-saat alır.</span><span class="sxs-lookup"><span data-stu-id="df02c-226">Gets hello date-time that represents hello end of hello day (day component) of X.</span></span><br/><br/><span data-ttu-id="df02c-227">Örnek: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span><span class="sxs-lookup"><span data-stu-id="df02c-227">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span></span> |
| <span data-ttu-id="df02c-228">Tarih</span><span class="sxs-lookup"><span data-stu-id="df02c-228">Date</span></span> |<span data-ttu-id="df02c-229">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="df02c-229">EndOfMonth(X)</span></span> |<span data-ttu-id="df02c-230">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="df02c-230">X: DateTime</span></span> |<span data-ttu-id="df02c-231">X parametresi ay bileşen tarafından temsil edilen hello ayın Hello sonunu alır.</span><span class="sxs-lookup"><span data-stu-id="df02c-231">Gets hello end of hello month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="df02c-232">Örnek: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (güncel Eylül ayın hello sonunu temsil eden saat)</span><span class="sxs-lookup"><span data-stu-id="df02c-232">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents hello end of September month)</span></span> |
| <span data-ttu-id="df02c-233">Tarih</span><span class="sxs-lookup"><span data-stu-id="df02c-233">Date</span></span> |<span data-ttu-id="df02c-234">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="df02c-234">StartOfDay(X)</span></span> |<span data-ttu-id="df02c-235">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="df02c-235">X: DateTime</span></span> |<span data-ttu-id="df02c-236">Merhaba hello gün bileşeninin X parametresi tarafından temsil edilen hello günün başlangıcını alır.</span><span class="sxs-lookup"><span data-stu-id="df02c-236">Gets hello start of hello day represented by hello day component of parameter X.</span></span><br/><br/><span data-ttu-id="df02c-237">Örnek: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span><span class="sxs-lookup"><span data-stu-id="df02c-237">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span></span> |
| <span data-ttu-id="df02c-238">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="df02c-238">DateTime</span></span> |<span data-ttu-id="df02c-239">FROM(X)</span><span class="sxs-lookup"><span data-stu-id="df02c-239">From(X)</span></span> |<span data-ttu-id="df02c-240">X: dize</span><span class="sxs-lookup"><span data-stu-id="df02c-240">X: String</span></span> |<span data-ttu-id="df02c-241">Dize X tooa tarih saat ayrıştırılamadı.</span><span class="sxs-lookup"><span data-stu-id="df02c-241">Parse string X tooa date time.</span></span> |
| <span data-ttu-id="df02c-242">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="df02c-242">DateTime</span></span> |<span data-ttu-id="df02c-243">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="df02c-243">Ticks(X)</span></span> |<span data-ttu-id="df02c-244">X: DateTime</span><span class="sxs-lookup"><span data-stu-id="df02c-244">X: DateTime</span></span> |<span data-ttu-id="df02c-245">Merhaba çizgilerine X hello parametresi özelliğini alır. Bir değer 100 nanosaniye eşittir.</span><span class="sxs-lookup"><span data-stu-id="df02c-245">Gets hello ticks property of hello parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="df02c-246">Bu özellik başlangıç değeri 12:00:00 gece'den itibaren 1 Ocak 0001 geçen çizgilerine hello sayısını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="df02c-246">hello value of this property represents hello number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="df02c-247">Metin</span><span class="sxs-lookup"><span data-stu-id="df02c-247">Text</span></span> |<span data-ttu-id="df02c-248">Format(X)</span><span class="sxs-lookup"><span data-stu-id="df02c-248">Format(X)</span></span> |<span data-ttu-id="df02c-249">X: Dize değişkeni</span><span class="sxs-lookup"><span data-stu-id="df02c-249">X: String variable</span></span> |<span data-ttu-id="df02c-250">Biçimleri hello metin (kullanmak `\\'` birleşimi tooescape `'` karakter).</span><span class="sxs-lookup"><span data-stu-id="df02c-250">Formats hello text (use `\\'` combination tooescape `'` character).</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="df02c-251">Başka bir işlev içinde bir işlevi kullanılırken toouse gerekmez  **$$**  hello iç işlevi için önek.</span><span class="sxs-lookup"><span data-stu-id="df02c-251">When using a function within another function, you do not need toouse **$$** prefix for hello inner function.</span></span> <span data-ttu-id="df02c-252">Örneğin: $$Text.Format ('PartitionKey eq \\' my_pkey_filter_value\\' ve RowKey ge \\' {0: yyyy-aa-gg ss: dd:}\\'', Time.AddHours (SliceStart, -6)).</span><span class="sxs-lookup"><span data-stu-id="df02c-252">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="df02c-253">Bu örnekte, dikkat  **$$**  öneki Merhaba kullanılmaz **Time.AddHours** işlevi.</span><span class="sxs-lookup"><span data-stu-id="df02c-253">In this example, notice that **$$** prefix is not used for hello **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="df02c-254">Örnek</span><span class="sxs-lookup"><span data-stu-id="df02c-254">Example</span></span>
<span data-ttu-id="df02c-255">Hello hello Hive etkinliği için aşağıdaki örnek, giriş ve çıkış parametreleri hello kullanılarak belirlenir `Text.Format` işlevi ve SliceStart sistem değişkeni.</span><span class="sxs-lookup"><span data-stu-id="df02c-255">In hello following example, input and output parameters for hello Hive activity are determined by using hello `Text.Format` function and SliceStart system variable.</span></span> 

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

### <a name="example-2"></a><span data-ttu-id="df02c-256">Örnek 2</span><span class="sxs-lookup"><span data-stu-id="df02c-256">Example 2</span></span>

<span data-ttu-id="df02c-257">Aşağıdaki örneğine hello hello DateTime parametresi için saklı yordam etkinliği kullanılarak belirlenir hello hello metin.</span><span class="sxs-lookup"><span data-stu-id="df02c-257">In hello following example, hello DateTime parameter for hello Stored Procedure Activity is determined by using hello Text.</span></span> <span data-ttu-id="df02c-258">İşlev biçimlendirin ve SliceStart değişkeni hello.</span><span class="sxs-lookup"><span data-stu-id="df02c-258">Format function and hello SliceStart variable.</span></span> 

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

### <a name="example-3"></a><span data-ttu-id="df02c-259">Örnek 3</span><span class="sxs-lookup"><span data-stu-id="df02c-259">Example 3</span></span>
<span data-ttu-id="df02c-260">önceki gün SliceStart, hello tarafından temsil edilen gün yerine tooread verilerden hello aşağıdaki örnekte gösterildiği gibi hello AddDays işlevi kullanın:</span><span class="sxs-lookup"><span data-stu-id="df02c-260">tooread data from previous day instead of day represented by hello SliceStart, use hello AddDays function as shown in hello following example:</span></span> 

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

<span data-ttu-id="df02c-261">Bkz: [özel tarih ve saat biçim dizeleri](https://msdn.microsoft.com/library/8kb3ddd4.aspx) kullanabileceğiniz farklı biçimlendirme seçenekleri açıklar konu (örneğin: yy yyyy karşılaştırması).</span><span class="sxs-lookup"><span data-stu-id="df02c-261">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

