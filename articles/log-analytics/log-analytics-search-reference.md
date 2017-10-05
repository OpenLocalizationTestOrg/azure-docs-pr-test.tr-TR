---
title: "Azure günlük analizi Arama başvurusu | Microsoft Docs"
description: "Günlük Arama başvurusu arama dili açıklar ve genel sorgu sözdizimi seçenekleri sağlar analizi kullanılacağı verileri için arama ve filtreleme aramanızı daraltmak yardımcı olmak üzere ifadeler."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 402615a2-bed0-4831-ba69-53be49059718
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc9c9b0a6292dab256997a86a6db16367fc48cd3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="log-analytics-search-reference"></a><span data-ttu-id="a942b-103">Günlük analizi başvuru arama</span><span class="sxs-lookup"><span data-stu-id="a942b-103">Log Analytics search reference</span></span>

>[!NOTE]
> <span data-ttu-id="a942b-104">Bu makalede geçerli sorgu dili günlük analizi kullanarak günlük aramaları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a942b-104">This article describes log searches using the current query language in Log Analytics.</span></span>  <span data-ttu-id="a942b-105">Çalışma alanınız için yükseltildiyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), için başvurmalıdır sonra [yeni dil için dil başvurusu](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="a942b-105">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer to [the language reference for the new language](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="a942b-106">Şu bölüme arama dili hakkında ne zaman kullanabilir genel sorgu sözdizimi seçenekleri açıklar verileri için arama ve filtreleme aramanızı daraltmak yardımcı olmak üzere ifadeler.</span><span class="sxs-lookup"><span data-stu-id="a942b-106">The following reference section about search language describes the general query syntax options you can use when searching for data and filtering expressions to help narrow your search.</span></span> <span data-ttu-id="a942b-107">Ayrıca, alınan veri eyleme geçmek için kullanabileceğiniz komutlar anlatır.</span><span class="sxs-lookup"><span data-stu-id="a942b-107">It also describes commands that you can use to take action on the data retrieved.</span></span>

<span data-ttu-id="a942b-108">Aramalarda dönen alanları hakkında bilgi edinebilirsiniz ve veri benzer kategorileri hakkında daha fazla keşfetmesine yardımcı modelleri içinde [arama alanı ve model başvuru bölüm](#search-field-and-facet-reference).</span><span class="sxs-lookup"><span data-stu-id="a942b-108">You can read about the fields returned in searches, and the facets that help you discover more about similar categories of data, in the [Search field and facet reference section](#search-field-and-facet-reference).</span></span>

## <a name="general-query-syntax"></a><span data-ttu-id="a942b-109">Genel sorgu söz dizimi</span><span class="sxs-lookup"><span data-stu-id="a942b-109">General query syntax</span></span>
<span data-ttu-id="a942b-110">Genel sorgulamak için sözdizimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="a942b-110">The syntax for general querying is as follows:</span></span>

```
filterExpression | command1 | command2 …
```

<span data-ttu-id="a942b-111">Filtre ifadesi (`filterExpression`) "where" için sorgu koşul tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a942b-111">The filter expression (`filterExpression`) defines the "where" condition for the query.</span></span> <span data-ttu-id="a942b-112">Sorgu tarafından döndürülen sonuçlar komutları uygulamak.</span><span class="sxs-lookup"><span data-stu-id="a942b-112">The commands apply to the results returned by the query.</span></span> <span data-ttu-id="a942b-113">Birden çok komut dikey çizgi karakterinden (|) tarafından ayrılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a942b-113">Multiple commands must be separated by the pipe character ( | ).</span></span>

### <a name="general-syntax-examples"></a><span data-ttu-id="a942b-114">Genel sözdizimi örnekleri</span><span class="sxs-lookup"><span data-stu-id="a942b-114">General syntax examples</span></span>
<span data-ttu-id="a942b-115">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="a942b-115">Examples:</span></span>

```
system
```

<span data-ttu-id="a942b-116">Bu sorgunun döndürdüğü sözcüğünü içeren sonuçları *sistem* için tam metin dizinli veya arama koşulları herhangi bir alanda.</span><span class="sxs-lookup"><span data-stu-id="a942b-116">This query returns results that contain the word *system* in any field that has been indexed for full text or terms searching.</span></span>

> [!NOTE]
> <span data-ttu-id="a942b-117">Bu şekilde tüm alanlar dizini, ancak en sık kullanılan metinsel alanlar (açıklamaları ve adları gibi) genellikle şunlardır.</span><span class="sxs-lookup"><span data-stu-id="a942b-117">Not all fields are indexed this way, but the most common textual fields (such as descriptions and names) usually are.</span></span>
>
>

```
system error
```

<span data-ttu-id="a942b-118">Sözcükler içeren sonuçları bu sorgunun döndürdüğü *sistem* ve *hata*.</span><span class="sxs-lookup"><span data-stu-id="a942b-118">This query returns results that contain the words *system* and *error*.</span></span>

```
system error | sort ManagementGroupName, TimeGenerated desc | top 10
```

<span data-ttu-id="a942b-119">Sözcükler içeren sonuçları bu sorgunun döndürdüğü *sistem* ve *hata*.</span><span class="sxs-lookup"><span data-stu-id="a942b-119">This query returns results that contain the words *system* and *error*.</span></span> <span data-ttu-id="a942b-120">Ardından sonuçları göre sıralar *ManagementGroupName* (artan düzende), alan ve sonra *TimeGenerated* alanındaki (Azalan).</span><span class="sxs-lookup"><span data-stu-id="a942b-120">It then sorts the results by the *ManagementGroupName* field (in ascending order), and then by the *TimeGenerated* field (in descending order).</span></span> <span data-ttu-id="a942b-121">Yalnızca ilk 10 sonuçlarını alır.</span><span class="sxs-lookup"><span data-stu-id="a942b-121">It takes only the first 10 results.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a942b-122">Tüm alan adları ve değerleri dize ve metin alanları için büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="a942b-122">All the field names and the values for the string and text fields are case sensitive.</span></span>
>
>

## <a name="filter-expressions"></a><span data-ttu-id="a942b-123">Filtre ifadeleri</span><span class="sxs-lookup"><span data-stu-id="a942b-123">Filter expressions</span></span>
<span data-ttu-id="a942b-124">Aşağıdaki alt bölümlerde filtre ifadeleri açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a942b-124">The following subsections explain the filter expressions.</span></span>

### <a name="string-literals"></a><span data-ttu-id="a942b-125">Dize değişmez değerleri</span><span class="sxs-lookup"><span data-stu-id="a942b-125">String literals</span></span>
<span data-ttu-id="a942b-126">Bir dize sabit değeri bir anahtar sözcük veya önceden tanımlanmış veri türü (örneğin, bir sayı veya tarih) ayrıştırıcı tarafından tanınmıyor herhangi bir dize ' dir.</span><span class="sxs-lookup"><span data-stu-id="a942b-126">A string literal is any string that is not recognized by the parser as a keyword or a predefined data type (for example, a number or date).</span></span>

<span data-ttu-id="a942b-127">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="a942b-127">Examples:</span></span>

```
These all are string literals
```

<span data-ttu-id="a942b-128">Bu sorgu için tüm beş sözcükleri oluşumları içeren sonuçları arar.</span><span class="sxs-lookup"><span data-stu-id="a942b-128">This query searches for results that contain occurrences of all five words.</span></span> <span data-ttu-id="a942b-129">Karmaşık dize araması yapmak için dize sabit değeri tırnak işaretleri içine alın.</span><span class="sxs-lookup"><span data-stu-id="a942b-129">To perform a complex string search, enclose the string literal in quotation marks.</span></span> <span data-ttu-id="a942b-130">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a942b-130">For example:</span></span>

```
"Windows Server"
```

<span data-ttu-id="a942b-131">Bu yalnızca tam eşleşmeleri olan sonuçlar döndürür *Windows Server*.</span><span class="sxs-lookup"><span data-stu-id="a942b-131">This only returns results with exact matches for *Windows Server*.</span></span>

### <a name="numbers"></a><span data-ttu-id="a942b-132">Sayılar</span><span class="sxs-lookup"><span data-stu-id="a942b-132">Numbers</span></span>
<span data-ttu-id="a942b-133">Ayrıştırıcının sayısal alanlar için ondalık tamsayı ve kayan noktalı sayı sözdizimini destekler.</span><span class="sxs-lookup"><span data-stu-id="a942b-133">The parser supports the decimal integer and floating-point number syntax for numerical fields.</span></span>

<span data-ttu-id="a942b-134">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="a942b-134">Examples:</span></span>

```
Type:Perf 0.5
```

```
HTTP 500
```

### <a name="dates-and-times"></a><span data-ttu-id="a942b-135">Tarihler ve saatler</span><span class="sxs-lookup"><span data-stu-id="a942b-135">Dates and times</span></span>
<span data-ttu-id="a942b-136">Her bir veri sisteminde parçası olan bir *TimeGenerated* özgün tarih ve saat kaydının temsil eden özellik.</span><span class="sxs-lookup"><span data-stu-id="a942b-136">Every piece of data in the system has a *TimeGenerated* property, which represents the original date and time of the record.</span></span> <span data-ttu-id="a942b-137">Bazı veri türleri ek tarih ve saat alanları olabilir (örneğin, *LastModified*).</span><span class="sxs-lookup"><span data-stu-id="a942b-137">Some types of data can have additional date and time fields (for example, *LastModified*).</span></span>

<span data-ttu-id="a942b-138">Zaman Çizelgesi **grafik/saat** Azure günlük analizi seçicide sonuçlar dağıtılması (göre çalıştırılan geçerli sorgu) zamanla gösterilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-138">The timeline **Chart/Time** selector in Azure Log Analytics shows a distribution of results over time (according to the current query being run).</span></span> <span data-ttu-id="a942b-139">Bu temel alır *TimeGenerated* alan.</span><span class="sxs-lookup"><span data-stu-id="a942b-139">This is based on the *TimeGenerated* field.</span></span> <span data-ttu-id="a942b-140">Tarih ve saat alanları sorgularında belirli bir zaman çerçevesi sorgusunu sınırlamak için kullanılan bir belirli dize biçimine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a942b-140">Date and time fields have a specific string format that can be used in queries to restrict the query to a particular timeframe.</span></span> <span data-ttu-id="a942b-141">Sözdizimi, göreli zaman aralıkları (örneğin, "arasındaki 3 gün önce 2 saat önce") başvurmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a942b-141">You can also use syntax to refer to relative time intervals (for example, "between 3 days ago and 2 hours ago").</span></span>

<span data-ttu-id="a942b-142">Geçerli tür sözdizimi tarihler ve saatler için şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a942b-142">The following are valid forms of syntax for dates and times:</span></span>

```
yyyy-mm-ddThh:mm:ss.dddZ
```

```
yyyy-mm-ddThh:mm:ss.ddd
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm
```

```
yyyy-mm-dd
```


<span data-ttu-id="a942b-143">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a942b-143">For example:</span></span>

```
TimeGenerated:2013-10-01T12:20
```

<span data-ttu-id="a942b-144">Önceki komutu yalnızca kayıtları döndüren bir *TimeGenerated* değeri tam olarak 12:20 1 Ekim 2013.</span><span class="sxs-lookup"><span data-stu-id="a942b-144">The previous command returns only records with a *TimeGenerated* value of exactly 12:20 on October 1, 2013.</span></span>

<span data-ttu-id="a942b-145">Ayrıştırıcının anımsatıcı tarih/saat değeri şimdi de destekler.</span><span class="sxs-lookup"><span data-stu-id="a942b-145">The parser also supports the mnemonic Date/Time value, NOW.</span></span> <span data-ttu-id="a942b-146">(Veri ile bu hızlı sistemin yapmaz olduğundan, bu herhangi bir sonuç sunacak düşüktür.)</span><span class="sxs-lookup"><span data-stu-id="a942b-146">(It is unlikely that this will yield any results, because data doesn’t make it through the system that fast.)</span></span>

<span data-ttu-id="a942b-147">Bu örnek için mutlak tarihleri kullanmak için yapı taşları verilebilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-147">These examples are building blocks to use for relative and absolute dates.</span></span> <span data-ttu-id="a942b-148">Sonraki üç alt bölümlerde, göreli bir tarih aralıkları kullanmanız örnekleriyle daha gelişmiş filtreleri kullanmak nasıl görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a942b-148">In the next three subsections, you'll see how to use them in more advanced filters, with examples that use relative date ranges.</span></span>

### <a name="datetime-math"></a><span data-ttu-id="a942b-149">Matematik tarih</span><span class="sxs-lookup"><span data-stu-id="a942b-149">Date/Time math</span></span>
<span data-ttu-id="a942b-150">Uzaklık ya da basit tarih hesaplamaları kullanarak bir tarih/saat değeri yuvarlamak için tarih matematik işleçleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="a942b-150">Use the Date/Time math operators to offset or round the Date/Time value, by using simple Date/Time calculations.</span></span>

<span data-ttu-id="a942b-151">Sözdizimi:</span><span class="sxs-lookup"><span data-stu-id="a942b-151">Syntax:</span></span>

```
datetime/unit
```

```
datetime[+|-]count unit
```

| <span data-ttu-id="a942b-152">işleci</span><span class="sxs-lookup"><span data-stu-id="a942b-152">Operator</span></span> | <span data-ttu-id="a942b-153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a942b-153">Description</span></span> |
| --- | --- |
| / |<span data-ttu-id="a942b-154">Tarih için belirtilen birim yuvarlar.</span><span class="sxs-lookup"><span data-stu-id="a942b-154">Rounds Date/Time to the specified unit.</span></span> <span data-ttu-id="a942b-155">Örneğin, şimdi / gün geçerli günün gece yarısına geçerli tarih/saat yuvarlar.</span><span class="sxs-lookup"><span data-stu-id="a942b-155">For example, NOW/DAY rounds the current Date/Time to midnight of the current day.</span></span> |
| <span data-ttu-id="a942b-156">+ veya -</span><span class="sxs-lookup"><span data-stu-id="a942b-156">+ or -</span></span> |<span data-ttu-id="a942b-157">Tarih/Saat birimleri belirtilen sayıda tarafından kaydırır.</span><span class="sxs-lookup"><span data-stu-id="a942b-157">Offsets Date/Time by the specified number of units.</span></span> <span data-ttu-id="a942b-158">Örneğin, şimdi + 1 saat kaydırır geçerli tarih/saat şimdi bir saat.</span><span class="sxs-lookup"><span data-stu-id="a942b-158">For example, NOW+1HOUR offsets the current Date/Time by one hour ahead.</span></span> <span data-ttu-id="a942b-159">2013-10-01T12:00-10 gün tarih değerini 10 gün tarafından yeniden kaydırır.</span><span class="sxs-lookup"><span data-stu-id="a942b-159">2013-10-01T12:00-10DAYS offsets the Date value back by 10 days.</span></span> |

<span data-ttu-id="a942b-160">Tarih/saat matematik işleçleri birlikte zincir.</span><span class="sxs-lookup"><span data-stu-id="a942b-160">You can chain the Date/Time math operators together.</span></span> <span data-ttu-id="a942b-161">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a942b-161">For example:</span></span>

```
NOW+1HOUR-10MONTHS/MINUTE
```

<span data-ttu-id="a942b-162">Aşağıdaki tabloda, desteklenen tarih/saat birimleri listeler.</span><span class="sxs-lookup"><span data-stu-id="a942b-162">The following table lists the supported Date/Time units.</span></span>

| <span data-ttu-id="a942b-163">Tarih/saat birim</span><span class="sxs-lookup"><span data-stu-id="a942b-163">Date/Time unit</span></span> | <span data-ttu-id="a942b-164">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a942b-164">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a942b-165">YIL, YIL</span><span class="sxs-lookup"><span data-stu-id="a942b-165">YEAR, YEARS</span></span> |<span data-ttu-id="a942b-166">Geçerli yıl yuvarlar veya belirtilen yıl sayısı kadar kaydırır.</span><span class="sxs-lookup"><span data-stu-id="a942b-166">Rounds to current year, or offsets by the specified number of years.</span></span> |
| <span data-ttu-id="a942b-167">AY, AY</span><span class="sxs-lookup"><span data-stu-id="a942b-167">MONTH, MONTHS</span></span> |<span data-ttu-id="a942b-168">Geçerli ay yuvarlar veya belirtilen ay sayısı kadar kaydırır.</span><span class="sxs-lookup"><span data-stu-id="a942b-168">Rounds to current month, or offsets by the specified number of months.</span></span> |
| <span data-ttu-id="a942b-169">GÜN, TARİH</span><span class="sxs-lookup"><span data-stu-id="a942b-169">DAY, DAYS, DATE</span></span> |<span data-ttu-id="a942b-170">Geçerli ayın yuvarlar veya belirtilen gün sayısı tarafından kaydırır.</span><span class="sxs-lookup"><span data-stu-id="a942b-170">Rounds to current day of the month, or offsets by the specified number of days.</span></span> |
| <span data-ttu-id="a942b-171">SAAT, SAAT</span><span class="sxs-lookup"><span data-stu-id="a942b-171">HOUR, HOURS</span></span> |<span data-ttu-id="a942b-172">Geçerli saat yuvarlar veya tarafından belirtilen sayıda saat kaydırır.</span><span class="sxs-lookup"><span data-stu-id="a942b-172">Rounds to current hour, or offsets by the specified number of hours.</span></span> |
| <span data-ttu-id="a942b-173">DAKİKA, DAKİKA</span><span class="sxs-lookup"><span data-stu-id="a942b-173">MINUTE, MINUTES</span></span> |<span data-ttu-id="a942b-174">Geçerli dakikada yuvarlar veya belirtilen dakika sayısı kadar kaydırır.</span><span class="sxs-lookup"><span data-stu-id="a942b-174">Rounds to current minute, or offsets by the specified number of minutes.</span></span> |
| <span data-ttu-id="a942b-175">İKİNCİ OLARAK, SANİYE</span><span class="sxs-lookup"><span data-stu-id="a942b-175">SECOND, SECONDS</span></span> |<span data-ttu-id="a942b-176">Geçerli ikinci yuvarlar veya belirtilen sayıda saniye tarafından kaydırır.</span><span class="sxs-lookup"><span data-stu-id="a942b-176">Rounds to current second, or offsets by the specified number of seconds.</span></span> |
| <span data-ttu-id="a942b-177">MİLİSANİYE, MİLİSANİYE CİNSİNDEN MİLİSANİYE, MILLIS</span><span class="sxs-lookup"><span data-stu-id="a942b-177">MILLISECOND, MILLISECONDS, MILLI, MILLIS</span></span> |<span data-ttu-id="a942b-178">Geçerli saniyeye yuvarlar veya belirtilen milisaniye sayısı kadar kaydırır.</span><span class="sxs-lookup"><span data-stu-id="a942b-178">Rounds to current millisecond, or offsets by the specified number of milliseconds.</span></span> |

### <a name="field-facets"></a><span data-ttu-id="a942b-179">Alan modelleri</span><span class="sxs-lookup"><span data-stu-id="a942b-179">Field facets</span></span>
<span data-ttu-id="a942b-180">Alan modelleri kullanarak, belirli alanlar ve tam değerlerine için arama koşulu belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a942b-180">By using field facets, you can specify the search condition for specific fields and their exact values.</span></span> <span data-ttu-id="a942b-181">Bu dizin boyunca çeşitli koşullar için "serbest metin" sorguları yazma farklıdır.</span><span class="sxs-lookup"><span data-stu-id="a942b-181">This differs from writing "free text" queries for various terms throughout the index.</span></span> <span data-ttu-id="a942b-182">Bu teknik birkaç önceki örneklerde zaten gördünüz.</span><span class="sxs-lookup"><span data-stu-id="a942b-182">You have already seen this technique in several previous examples.</span></span> <span data-ttu-id="a942b-183">Daha karmaşık örnekleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a942b-183">The following are more complex examples.</span></span>

<span data-ttu-id="a942b-184">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="a942b-184">**Syntax**</span></span>

```
field:value
```

```
field=value
```

<span data-ttu-id="a942b-185">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="a942b-185">**Description**</span></span>

<span data-ttu-id="a942b-186">Belirli değer alanını arar.</span><span class="sxs-lookup"><span data-stu-id="a942b-186">Searches the field for the specific value.</span></span> <span data-ttu-id="a942b-187">Değer bir dize sabit değeri, sayı veya tarih ve saat olabilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-187">The value can be a string literal, number, or date and time.</span></span>

<span data-ttu-id="a942b-188">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a942b-188">For example:</span></span>

```
TimeGenerated:NOW
```

```
ObjectDisplayName:"server01.contoso.com"
```

```
SampleValue:0.3
```

<span data-ttu-id="a942b-189">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="a942b-189">**Syntax**</span></span>

<span data-ttu-id="a942b-190">*alan > değeri*</span><span class="sxs-lookup"><span data-stu-id="a942b-190">*field>value*</span></span>

<span data-ttu-id="a942b-191">*alan < değeri*</span><span class="sxs-lookup"><span data-stu-id="a942b-191">*field<value*</span></span>

<span data-ttu-id="a942b-192">*alan > = değer*</span><span class="sxs-lookup"><span data-stu-id="a942b-192">*field>=value*</span></span>

<span data-ttu-id="a942b-193">*alan < value =*</span><span class="sxs-lookup"><span data-stu-id="a942b-193">*field<=value*</span></span>

<span data-ttu-id="a942b-194">*alan! = değer*</span><span class="sxs-lookup"><span data-stu-id="a942b-194">*field!=value*</span></span>

<span data-ttu-id="a942b-195">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="a942b-195">**Description**</span></span>

<span data-ttu-id="a942b-196">Karşılaştırmaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="a942b-196">Provides comparisons.</span></span>

<span data-ttu-id="a942b-197">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a942b-197">For example:</span></span>

```
TimeGenerated>NOW+2HOURS
```

<span data-ttu-id="a942b-198">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="a942b-198">**Syntax**</span></span>

```
field:[from..to]
```

<span data-ttu-id="a942b-199">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="a942b-199">**Description**</span></span>

<span data-ttu-id="a942b-200">Aralık olduğunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="a942b-200">Provides range faceting.</span></span>

<span data-ttu-id="a942b-201">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a942b-201">For example:</span></span>

```
TimeGenerated:[NOW..NOW+1DAY]
```

```
SampleValue:[0..2]
```

### <a name="in"></a><span data-ttu-id="a942b-202">IN</span><span class="sxs-lookup"><span data-stu-id="a942b-202">IN</span></span>
<span data-ttu-id="a942b-203">**IN** anahtar sözcüğü değerler listesinden seçmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a942b-203">The **IN** keyword allows you to select from a list of values.</span></span> <span data-ttu-id="a942b-204">Kullandığınız sözdizimi bağlı olarak, bu basit sağladığınız değerler listesini ya da bir toplama değerleri listesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-204">Depending on the syntax you use, this can be a simple list of values you provide, or a list of values from an aggregation.</span></span>

<span data-ttu-id="a942b-205">Sözdizimi 1:</span><span class="sxs-lookup"><span data-stu-id="a942b-205">Syntax 1:</span></span>

```
field IN {value1,value2,value3,...}
```

<span data-ttu-id="a942b-206">Bu sözdizimi, basit bir listedeki tüm değerlerin içermek üzere sağlar.</span><span class="sxs-lookup"><span data-stu-id="a942b-206">This syntax allows you to include all values in a simple list.</span></span>



<span data-ttu-id="a942b-207">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="a942b-207">Examples:</span></span>

```
EventID IN {1201,1204,1210}
```

```
Computer IN {"srv01.contoso.com","srv02.contoso.com"}
```

<span data-ttu-id="a942b-208">Sözdizimi 2:</span><span class="sxs-lookup"><span data-stu-id="a942b-208">Syntax 2:</span></span>

```
(Outer query) (Field to use with inner query results) IN {Inner query | measure count() by (Field to send to outer query)} (rest  of outer query)  
```

<span data-ttu-id="a942b-209">Bu söz dizimi, bir toplama oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a942b-209">This syntax allows you to create an aggregation.</span></span> <span data-ttu-id="a942b-210">Ardından, bu toplama bu değerle olaylarını arar başka bir dış (birincil) arama içine gelen değerler listesi akış.</span><span class="sxs-lookup"><span data-stu-id="a942b-210">You can then feed the list of values from that aggregation into another outer (primary) search that looks for events with those value.</span></span> <span data-ttu-id="a942b-211">İç arama ayraçlar içinde kapsayan ve ın işlecini kullanarak bir alan dış arama için olası değerler olarak sonuçlarını besleme yapın.</span><span class="sxs-lookup"><span data-stu-id="a942b-211">You do this by enclosing the inner search in braces, and feeding its results as possible values for a field in the outer search by using the IN operator.</span></span>

<span data-ttu-id="a942b-212">İç sorgu örnek: *şu anda güvenlik güncelleştirmeleri eksik olan bilgisayarlar* aşağıdaki toplama sorguyla:</span><span class="sxs-lookup"><span data-stu-id="a942b-212">Inner query example: *computers currently missing security updates* with the following aggregation query:</span></span>

```
Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer
```    

<span data-ttu-id="a942b-213">Bulur son sorgu *şu anda güvenlik güncelleştirmeleri eksik olan bilgisayarlar için tüm Windows olayları* aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="a942b-213">The final query that finds *all Windows events for computers currently missing security updates* resembles the following:</span></span>

```
Type=Event Computer IN {Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer}
```

### <a name="contains"></a><span data-ttu-id="a942b-214">Contains</span><span class="sxs-lookup"><span data-stu-id="a942b-214">Contains</span></span>
<span data-ttu-id="a942b-215">**İçerir** anahtar sözcüğü, belirtilen dizeyi içeren bir alanla kayıtlar için filtre olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a942b-215">The **Contains** keyword allows you to filter for records with a field that contains a specified string.</span></span> <span data-ttu-id="a942b-216">Bu büyük küçük harfe duyarlıdır, yalnızca dize alanları ile çalışır ve herhangi bir kaçış karakteri içeremez.</span><span class="sxs-lookup"><span data-stu-id="a942b-216">This is case sensitive, works only with string fields, and may not include any escape characters.</span></span>

<span data-ttu-id="a942b-217">Sözdizimi:</span><span class="sxs-lookup"><span data-stu-id="a942b-217">Syntax:</span></span>

```
field:contains("string")
```

<span data-ttu-id="a942b-218">Örnek:</span><span class="sxs-lookup"><span data-stu-id="a942b-218">Example:</span></span>

```
Type:contains("Event")
```

<span data-ttu-id="a942b-219">Bu, "Olay" dizesini içeren bir türü kayıtlarıyla döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-219">This returns records with a type that contains the string "Event".</span></span> <span data-ttu-id="a942b-220">Örnekler **olay**, **SecurityEvent**, ve **ServiceFabricOperationEvent**.</span><span class="sxs-lookup"><span data-stu-id="a942b-220">Examples include **Event**, **SecurityEvent**, and **ServiceFabricOperationEvent**.</span></span>



### <a name="regular-expressions"></a><span data-ttu-id="a942b-221">Normal ifadeler</span><span class="sxs-lookup"><span data-stu-id="a942b-221">Regular expressions</span></span>
<span data-ttu-id="a942b-222">Kullanarak bir normal ifade ile bir alan için bir arama koşulu belirtebilirsiniz **Regex** anahtar sözcüğü.</span><span class="sxs-lookup"><span data-stu-id="a942b-222">You can specify a search condition for a field with a regular expression, by using the **Regex** keyword.</span></span> <span data-ttu-id="a942b-223">Normal ifadelerde kullanabileceğiniz sözdizimi tam bir açıklaması için bkz: [günlük analizi günlük aramalarda filtrelemek için normal ifadeler kullanarak](log-analytics-log-searches-regex.md).</span><span class="sxs-lookup"><span data-stu-id="a942b-223">For a complete description of the syntax you can use in regular expressions, see [Using regular expressions to filter log searches in Log Analytics](log-analytics-log-searches-regex.md).</span></span>

<span data-ttu-id="a942b-224">Sözdizimi:</span><span class="sxs-lookup"><span data-stu-id="a942b-224">Syntax:</span></span>

```
field:Regex("Regular Expression")
```

<span data-ttu-id="a942b-225">Örnek:</span><span class="sxs-lookup"><span data-stu-id="a942b-225">Example:</span></span>

```
Computer:Regex("^C.*")
```

### <a name="logical-operators"></a><span data-ttu-id="a942b-226">Mantıksal işleçler</span><span class="sxs-lookup"><span data-stu-id="a942b-226">Logical operators</span></span>
<span data-ttu-id="a942b-227">Mantıksal işleçler sorgu dili destekler (*ve*, *veya*, ve *değil*) ve C tarzı benzersizse (*&&*,  *||* , ve *!*sırasıyla).</span><span class="sxs-lookup"><span data-stu-id="a942b-227">The query languages support the logical operators (*AND*, *OR*, and *NOT*) and their C-style aliases (*&&*, *||*, and *!*, respectively).</span></span> <span data-ttu-id="a942b-228">Bu işleçlere gruplandırmak için parantez kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a942b-228">You can use parentheses to group these operators.</span></span>

<span data-ttu-id="a942b-229">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="a942b-229">Examples:</span></span>

```
system OR error

```

```
Type:Alert AND NOT(Severity:1 OR ObjectId:"8066bbc0-9ec8-ca83-1edc-6f30d4779bcb8066bbc0-9ec8-ca83-1edc-6f30d4779bcb")
```

<span data-ttu-id="a942b-230">Üst düzey filtre bağımsız değişkenler için mantıksal işleç atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a942b-230">You can omit the logical operator for the top-level filter arguments.</span></span> <span data-ttu-id="a942b-231">Bu durumda, AND işleci varsayılır.</span><span class="sxs-lookup"><span data-stu-id="a942b-231">In this case, the AND operator is assumed.</span></span>

| <span data-ttu-id="a942b-232">Filtre ifadesi</span><span class="sxs-lookup"><span data-stu-id="a942b-232">Filter expression</span></span> | <span data-ttu-id="a942b-233">Eşdeğer</span><span class="sxs-lookup"><span data-stu-id="a942b-233">Equivalent to</span></span> |
| --- | --- |
| <span data-ttu-id="a942b-234">Sistem hatası</span><span class="sxs-lookup"><span data-stu-id="a942b-234">system error</span></span> |<span data-ttu-id="a942b-235">Sistem ve hata</span><span class="sxs-lookup"><span data-stu-id="a942b-235">system AND error</span></span> |
| <span data-ttu-id="a942b-236">Sistem "Windows Server" veya önem derecesi: 1</span><span class="sxs-lookup"><span data-stu-id="a942b-236">system "Windows Server" OR Severity:1</span></span> |<span data-ttu-id="a942b-237">Sistem ve ("Windows Server" veya önem derecesi: 1)</span><span class="sxs-lookup"><span data-stu-id="a942b-237">system AND ("Windows Server" OR Severity:1)</span></span> |

### <a name="wildcarding"></a><span data-ttu-id="a942b-238">Joker karakterler</span><span class="sxs-lookup"><span data-stu-id="a942b-238">Wildcarding</span></span>
<span data-ttu-id="a942b-239">Sorgu dili kullanarak destekler ( \* ) sorguda bir değer için bir veya daha fazla karakteri temsil etmesi için.</span><span class="sxs-lookup"><span data-stu-id="a942b-239">The query language supports using the ( \* ) character to  represent one or more characters for a value in a query.</span></span>

<span data-ttu-id="a942b-240">Örnek:</span><span class="sxs-lookup"><span data-stu-id="a942b-240">Example:</span></span>

 <span data-ttu-id="a942b-241">"Redmond-SQL" gibi adında "SQL" içeren tüm bilgisayarları bulur.</span><span class="sxs-lookup"><span data-stu-id="a942b-241">Find all computers with "SQL" in the name, such as "Redmond-SQL".</span></span>

```
Type=Event Computer=*SQL*
```

> [!NOTE]
> <span data-ttu-id="a942b-242">Şu anda tırnak işaretleri joker karakterler kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="a942b-242">At this time, wildcards cannot be used within quotations.</span></span> <span data-ttu-id="a942b-243">Örneğin, ileti `"*This text*"` göz önünde bulundurur (\*) sabit değer olarak kullanılan (\*) karakter.</span><span class="sxs-lookup"><span data-stu-id="a942b-243">For example, the message `"*This text*"` considers the (\*) used as a literal (\*) character.</span></span>


## <a name="commands"></a><span data-ttu-id="a942b-244">Komutlar</span><span class="sxs-lookup"><span data-stu-id="a942b-244">Commands</span></span>


<span data-ttu-id="a942b-245">Sorgu tarafından döndürülen sonuçları komutları uygulamak.</span><span class="sxs-lookup"><span data-stu-id="a942b-245">The commands apply to the results that are returned by the query.</span></span> <span data-ttu-id="a942b-246">Bir komut alınan sonuçları uygulamak için dikey çizgi karakterinden (|) kullanın.</span><span class="sxs-lookup"><span data-stu-id="a942b-246">Use the pipe character ( | ) to apply a command to the retrieved results.</span></span> <span data-ttu-id="a942b-247">Birden çok komut dikey çizgi karakteriyle ayrılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a942b-247">Multiple commands must be separated by the pipe character.</span></span>

> [!NOTE]
> <span data-ttu-id="a942b-248">Komut adları büyük harf ya da alan adları ve veri aksine, küçük harf yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-248">Command names can be written in upper case or lower case, unlike the field names and the data.</span></span>
>
>

### <a name="sort"></a><span data-ttu-id="a942b-249">Sırala</span><span class="sxs-lookup"><span data-stu-id="a942b-249">Sort</span></span>
<span data-ttu-id="a942b-250">Sözdizimi:</span><span class="sxs-lookup"><span data-stu-id="a942b-250">Syntax:</span></span>

    sort field1 asc|desc, field2 asc|desc, …

<span data-ttu-id="a942b-251">Sonuçları belirli alanlara göre sıralar.</span><span class="sxs-lookup"><span data-stu-id="a942b-251">Sorts the results by particular fields.</span></span> <span data-ttu-id="a942b-252">Artan veya azalan düzende sonuçları sıralamak için asc/desc sonek isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="a942b-252">The asc/desc suffix to sort the results in ascending or descending order is optional.</span></span> <span data-ttu-id="a942b-253">Belirtilmezse, *asc* sıralama düzeni varsayılır.</span><span class="sxs-lookup"><span data-stu-id="a942b-253">If it is omitted, the *asc* sort order is assumed.</span></span> <span data-ttu-id="a942b-254">İçin **TimeGenerated** alanı *desc* sıralama düzeni varsayılır, varsayılan olarak en son sonuçları ilk döndürecek şekilde.</span><span class="sxs-lookup"><span data-stu-id="a942b-254">For the **TimeGenerated** field, *desc* sort order is assumed, so it returns the most recent results first by default.</span></span>

### <a name="toplimit"></a><span data-ttu-id="a942b-255">Üst/sınırı</span><span class="sxs-lookup"><span data-stu-id="a942b-255">Top/Limit</span></span>
<span data-ttu-id="a942b-256">Sözdizimi:</span><span class="sxs-lookup"><span data-stu-id="a942b-256">Syntax:</span></span>

    top number


    limit number
<span data-ttu-id="a942b-257">İlk N sonuçları yanıtı sınırlar.</span><span class="sxs-lookup"><span data-stu-id="a942b-257">Limits the response to the top N results.</span></span>

<span data-ttu-id="a942b-258">Örnek:</span><span class="sxs-lookup"><span data-stu-id="a942b-258">Example:</span></span>

    Type:Alert errors detected | top 10

<span data-ttu-id="a942b-259">En iyi 10 eşleşen sonuç döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-259">Returns the top 10 matching results.</span></span>

### <a name="skip"></a><span data-ttu-id="a942b-260">Atla</span><span class="sxs-lookup"><span data-stu-id="a942b-260">Skip</span></span>
<span data-ttu-id="a942b-261">Sözdizimi:</span><span class="sxs-lookup"><span data-stu-id="a942b-261">Syntax:</span></span>

    skip number

<span data-ttu-id="a942b-262">Listelenen sonuç sayısını atlar.</span><span class="sxs-lookup"><span data-stu-id="a942b-262">Skips the number of results listed.</span></span>

<span data-ttu-id="a942b-263">Örnek:</span><span class="sxs-lookup"><span data-stu-id="a942b-263">Example:</span></span>

    Type:Alert errors detected | top 10 | skip 200

<span data-ttu-id="a942b-264">200 sonucunda başlangıç üst 10 eşleşen sonuç döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-264">Returns top 10 matching results starting at result 200.</span></span>

### <a name="select"></a><span data-ttu-id="a942b-265">Şunu seçin:</span><span class="sxs-lookup"><span data-stu-id="a942b-265">Select</span></span>
<span data-ttu-id="a942b-266">Sözdizimi:</span><span class="sxs-lookup"><span data-stu-id="a942b-266">Syntax:</span></span>

    select field1, field2, ...

<span data-ttu-id="a942b-267">Seçtiğiniz alan sonuçlarını sınırlandırır.</span><span class="sxs-lookup"><span data-stu-id="a942b-267">Limits results to the fields you choose.</span></span>

<span data-ttu-id="a942b-268">Örnek:</span><span class="sxs-lookup"><span data-stu-id="a942b-268">Example:</span></span>

    Type:Alert errors detected | select Name, Severity

<span data-ttu-id="a942b-269">Döndürülen sonuçlar alanları sınırlar *adı* ve *önem*.</span><span class="sxs-lookup"><span data-stu-id="a942b-269">Limits the returned results fields to *Name* and *Severity*.</span></span>

### <a name="measure"></a><span data-ttu-id="a942b-270">Ölçü birimi</span><span class="sxs-lookup"><span data-stu-id="a942b-270">Measure</span></span>
<span data-ttu-id="a942b-271">*Ölçü* komutu ham arama sonuçlarını istatistik işlevleri uygulamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a942b-271">The *measure* command is used to apply statistical functions to the raw search results.</span></span> <span data-ttu-id="a942b-272">Bu almak çok kullanışlıdır *grubu tarafından* görünümleri veriler üzerinde.</span><span class="sxs-lookup"><span data-stu-id="a942b-272">This is very useful to get *group-by* views over the data.</span></span> <span data-ttu-id="a942b-273">Ölçü komutunu kullandığınızda, günlük analizi arama toplanmış sonuçlarını içeren bir tablo görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a942b-273">When you use the measure command, Log Analytics search displays a table with aggregated results.</span></span>

<span data-ttu-id="a942b-274">**Sözdizimi:**</span><span class="sxs-lookup"><span data-stu-id="a942b-274">**Syntax:**</span></span>

    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]] by groupField1 [, groupField2 [, groupField3]]  [interval interval]


    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]]  interval interval



<span data-ttu-id="a942b-275">Sonuçlarına göre toplayan *grup alanı*ve toplanan ölçüm değerlerini kullanarak hesaplar *aggregatedField*.</span><span class="sxs-lookup"><span data-stu-id="a942b-275">Aggregates the results by *groupField*, and calculates the aggregated measure values by using *aggregatedField*.</span></span>

| <span data-ttu-id="a942b-276">Ölçü istatistiksel işlevi</span><span class="sxs-lookup"><span data-stu-id="a942b-276">Measure statistical function</span></span> | <span data-ttu-id="a942b-277">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a942b-277">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a942b-278">*aggregateFunction*</span><span class="sxs-lookup"><span data-stu-id="a942b-278">*aggregateFunction*</span></span> |<span data-ttu-id="a942b-279">Toplama işlevi (büyük küçük harfe duyarlı) adı.</span><span class="sxs-lookup"><span data-stu-id="a942b-279">The name of the aggregate function (case insensitive).</span></span> <span data-ttu-id="a942b-280">Aşağıdaki toplama işlevleri desteklenir: COUNT, MAX, MIN, SUM, AVG, STDDEV, COUNTDISTINCT, yüzdebirlik ## veya PCT ## (## herhangi bir sayı 1 ile 99 arasında).</span><span class="sxs-lookup"><span data-stu-id="a942b-280">The following aggregate functions are supported: COUNT, MAX, MIN, SUM, AVG, STDDEV, COUNTDISTINCT, PERCENTILE##, or PCT## (## is any number between 1 and 99).</span></span> |
| <span data-ttu-id="a942b-281">*aggregatedField*</span><span class="sxs-lookup"><span data-stu-id="a942b-281">*aggregatedField*</span></span> |<span data-ttu-id="a942b-282">Toplanmakta alan.</span><span class="sxs-lookup"><span data-stu-id="a942b-282">The field that is being aggregated.</span></span> <span data-ttu-id="a942b-283">Bu alan sayısı toplama işlevi için isteğe bağlıdır, ancak SUM, MAX, MIN, AVG, STDDEV, yüzdebirlik ## veya PCT ## için varolan bir sayısal alana olmalıdır (## herhangi bir sayı 1 ile 99 arasında).</span><span class="sxs-lookup"><span data-stu-id="a942b-283">This field is optional for the COUNT aggregate function, but has to be an existing numeric field for SUM, MAX, MIN, AVG, STDDEV, PERCENTILE##, or PCT## (## is any number between 1 and 99).</span></span> <span data-ttu-id="a942b-284">AggregatedField herhangi birini de olabilir **Genişlet** işlevleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a942b-284">The aggregatedField can also be any of the **Extend** supported functions.</span></span> |
| <span data-ttu-id="a942b-285">*fieldAlias*</span><span class="sxs-lookup"><span data-stu-id="a942b-285">*fieldAlias*</span></span> |<span data-ttu-id="a942b-286">(İsteğe bağlı) diğer hesaplanan değer birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-286">The (optional) alias for the calculated aggregated value.</span></span> <span data-ttu-id="a942b-287">Belirtilmezse, alan adıdır **AggregatedValue**.</span><span class="sxs-lookup"><span data-stu-id="a942b-287">If not specified, the field name is **AggregatedValue**.</span></span> |
| <span data-ttu-id="a942b-288">*Grup alanı*</span><span class="sxs-lookup"><span data-stu-id="a942b-288">*groupField*</span></span> |<span data-ttu-id="a942b-289">Sonuç kümesi alanın adını göre gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="a942b-289">The name of the field that the result set is grouped by.</span></span> |
| <span data-ttu-id="a942b-290">*Aralığı*</span><span class="sxs-lookup"><span data-stu-id="a942b-290">*Interval*</span></span> |<span data-ttu-id="a942b-291">Zaman aralığındaki biçimi:**nnnNAME**.</span><span class="sxs-lookup"><span data-stu-id="a942b-291">The time interval, in the format:**nnnNAME**.</span></span> <span data-ttu-id="a942b-292">**nnn**pozitif bir tamsayı değil.</span><span class="sxs-lookup"><span data-stu-id="a942b-292">**nnn** is the positive integer number.</span></span> <span data-ttu-id="a942b-293">**AD** aralığı adıdır.</span><span class="sxs-lookup"><span data-stu-id="a942b-293">**NAME** is the interval name.</span></span> <span data-ttu-id="a942b-294">Desteklenen aralık adları büyük küçük harfe duyarlı bağlıdır ve şunları içerir: MİLİSANİYE [S] ikinci [S] DAKİKADA [S], saat [S] günü [S], [S] ay ve yıl [S].</span><span class="sxs-lookup"><span data-stu-id="a942b-294">Supported interval names are case sensitive, and include:MILLISECOND[S], SECOND[S], MINUTE[S], HOUR[S], DAY[S], MONTH[S], and YEAR[S].</span></span> |

<span data-ttu-id="a942b-295">Aralık seçeneği yalnızca tarih/saat grubu alanlarında kullanılabilir (gibi *TimeGenerated* ve *TimeCreated*).</span><span class="sxs-lookup"><span data-stu-id="a942b-295">The interval option can only be used in Date/Time group fields (such as *TimeGenerated* and *TimeCreated*).</span></span> <span data-ttu-id="a942b-296">Şu anda, bu hizmet tarafından zorlanmaz ancak arka ucuna geçirilen tarih/saat olmayan bir alan bir çalışma zamanı hatası neden olur.</span><span class="sxs-lookup"><span data-stu-id="a942b-296">Currently, this is not enforced by the service, but a field without Date/Time that is passed to the back end causes a runtime error.</span></span> <span data-ttu-id="a942b-297">Şema doğrulaması uygulandığında hizmeti API'si için aralığı toplama alanları tarih olmadan kullanan sorguları reddeder.</span><span class="sxs-lookup"><span data-stu-id="a942b-297">When the schema validation is implemented, the service API rejects queries that use fields without Date/Time for interval aggregation.</span></span> <span data-ttu-id="a942b-298">Geçerli *ölçü* uygulaması herhangi bir toplama işlevi için aralığı gruplandırma destekler.</span><span class="sxs-lookup"><span data-stu-id="a942b-298">The current *Measure* implementation supports interval grouping for any aggregate function.</span></span>

<span data-ttu-id="a942b-299">BY yan tümcesi girilmezse, ancak bir zaman aralığı (bir ikinci sözdizimi), belirtilen *TimeGenerated* alan varsayılan olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-299">If the BY clause is omitted, but an interval is specified (as a second syntax), the *TimeGenerated* field is assumed by default.</span></span>

<span data-ttu-id="a942b-300">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="a942b-300">Examples:</span></span>

<span data-ttu-id="a942b-301">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="a942b-301">**Example 1**</span></span>

    Type:Alert | measure count() as Count by ObjectId

<span data-ttu-id="a942b-302">Uyarıları göre gruplandırır *objectID*ve her grup için uyarı sayısını hesaplar.</span><span class="sxs-lookup"><span data-stu-id="a942b-302">Groups the alerts by *ObjectID*, and calculates the number of alerts for each group.</span></span> <span data-ttu-id="a942b-303">Toplu değer olarak döndürülür *sayısı* alan (diğer ad).</span><span class="sxs-lookup"><span data-stu-id="a942b-303">The aggregated value is returned as the *Count* field (alias).</span></span>

<span data-ttu-id="a942b-304">**Örnek 2**</span><span class="sxs-lookup"><span data-stu-id="a942b-304">**Example 2**</span></span>

    Type:Alert | measure count() interval 1HOUR

<span data-ttu-id="a942b-305">Uyarıları kullanarak 1 saat aralıklarına göre gruplandırır *TimeGenerated* alan ve her aralığa uyarıların sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-305">Groups the alerts by 1-hour intervals by using the *TimeGenerated* field, and returns the number of alerts in each interval.</span></span>

<span data-ttu-id="a942b-306">**Örnek 3**</span><span class="sxs-lookup"><span data-stu-id="a942b-306">**Example 3**</span></span>

    Type:Alert | measure count() as AlertsPerHour interval 1HOUR

<span data-ttu-id="a942b-307">Önceki örnekte, ancak toplu alan diğer ad ile aynı (*AlertsPerHour*).</span><span class="sxs-lookup"><span data-stu-id="a942b-307">Same as the previous example, but with an aggregated field alias (*AlertsPerHour*).</span></span>

<span data-ttu-id="a942b-308">**Örnek 4**</span><span class="sxs-lookup"><span data-stu-id="a942b-308">**Example 4**</span></span>

    * <span data-ttu-id="a942b-309">| Ölçü count() TimeCreated aralığı 5DAYS tarafından</span><span class="sxs-lookup"><span data-stu-id="a942b-309">| measure count() by TimeCreated interval 5DAYS</span></span>

<span data-ttu-id="a942b-310">Kullanarak sonuçları 5 gün aralıklarına göre gruplandırır *TimeCreated* alan ve her aralığa sonuç sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-310">Groups the results by 5-day intervals by using the *TimeCreated* field, and returns the number of results in each interval.</span></span>

<span data-ttu-id="a942b-311">**Örnek 5**</span><span class="sxs-lookup"><span data-stu-id="a942b-311">**Example 5**</span></span>

    Type:Alert | measure max(Severity) by WorkflowName

<span data-ttu-id="a942b-312">Uyarıları iş yükü ada göre gruplandırır ve her bir iş akışı için en fazla uyarı önem derecesi değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-312">Groups the alerts by workload name, and returns the maximum alert severity value for each workflow.</span></span>

<span data-ttu-id="a942b-313">**Örnek 6**</span><span class="sxs-lookup"><span data-stu-id="a942b-313">**Example 6**</span></span>

    Type:Alert | measure min(Severity) by WorkflowName

<span data-ttu-id="a942b-314">Önceki örnekte, ancak ile aynı *min* işlevi bir araya getirilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-314">Same as the previous example, but with the *min* aggregated function.</span></span>

<span data-ttu-id="a942b-315">**Örnek 7**</span><span class="sxs-lookup"><span data-stu-id="a942b-315">**Example 7**</span></span>

    Type:Perf | measure avg(CounterValue) by Computer

<span data-ttu-id="a942b-316">Bilgisayar tarafından Perf grupları ve ortalama (Ort) hesaplar.</span><span class="sxs-lookup"><span data-stu-id="a942b-316">Groups Perf by computer, and calculates the average (avg).</span></span>

<span data-ttu-id="a942b-317">**Örnek 8**</span><span class="sxs-lookup"><span data-stu-id="a942b-317">**Example 8**</span></span>

    Type:Perf | measure sum(CounterValue) by Computer

<span data-ttu-id="a942b-318">Önceki örnekte, aynı ancak kullanan *toplam*.</span><span class="sxs-lookup"><span data-stu-id="a942b-318">Same as the previous example, but uses *sum*.</span></span>

<span data-ttu-id="a942b-319">**Örnek 9**</span><span class="sxs-lookup"><span data-stu-id="a942b-319">**Example 9**</span></span>

    Type:Perf | measure stddev(CounterValue) by Computer

<span data-ttu-id="a942b-320">Önceki örnekte, aynı ancak kullanan *stddev*.</span><span class="sxs-lookup"><span data-stu-id="a942b-320">Same as the previous example, but uses *stddev*.</span></span>

<span data-ttu-id="a942b-321">**Örnek 10**</span><span class="sxs-lookup"><span data-stu-id="a942b-321">**Example 10**</span></span>

    Type:Perf | measure percentile70(CounterValue) by Computer

<span data-ttu-id="a942b-322">Önceki örnekte, aynı ancak kullanan *percentile70*.</span><span class="sxs-lookup"><span data-stu-id="a942b-322">Same as the previous example, but uses *percentile70*.</span></span>

<span data-ttu-id="a942b-323">**Örnek 11**</span><span class="sxs-lookup"><span data-stu-id="a942b-323">**Example 11**</span></span>

    Type:Perf | measure pct70(CounterValue) by Computer

<span data-ttu-id="a942b-324">Önceki örnekte, aynı ancak kullanan *pct70*.</span><span class="sxs-lookup"><span data-stu-id="a942b-324">Same as the previous example, but uses *pct70*.</span></span> <span data-ttu-id="a942b-325">Unutmayın *PCT ##* yalnızca için diğer ad olduğu *yüzdebirlik ##* işlevi.</span><span class="sxs-lookup"><span data-stu-id="a942b-325">Note that *PCT##* is only an alias for *PERCENTILE##* function.</span></span>

<span data-ttu-id="a942b-326">**Örnek 12**</span><span class="sxs-lookup"><span data-stu-id="a942b-326">**Example 12**</span></span>

    Type:Perf | measure avg(CounterValue) by Computer, CounterName

<span data-ttu-id="a942b-327">Perf ilk bilgisayar tarafından grupları ve ardından CounterName ve ortalama (Ort) hesaplar.</span><span class="sxs-lookup"><span data-stu-id="a942b-327">Groups Perf first by Computer and then CounterName, and calculates the average (avg).</span></span>

<span data-ttu-id="a942b-328">**Örnek 13**</span><span class="sxs-lookup"><span data-stu-id="a942b-328">**Example 13**</span></span>

    Type:Alert | measure count() as Count by WorkflowName | sort Count desc | top 5

<span data-ttu-id="a942b-329">En fazla uyarı sayısı üst beş akışlarıyla alır.</span><span class="sxs-lookup"><span data-stu-id="a942b-329">Gets the top five workflows with the maximum number of alerts.</span></span>

<span data-ttu-id="a942b-330">**Örnek 14**</span><span class="sxs-lookup"><span data-stu-id="a942b-330">**Example 14**</span></span>

    * <span data-ttu-id="a942b-331">| countdistinct(Computer) türüne göre ölçün</span><span class="sxs-lookup"><span data-stu-id="a942b-331">| measure countdistinct(Computer) by Type</span></span>

<span data-ttu-id="a942b-332">Her tür için raporlama benzersiz bilgisayar sayısını sayar.</span><span class="sxs-lookup"><span data-stu-id="a942b-332">Counts the number of unique computers reporting for each Type.</span></span>

<span data-ttu-id="a942b-333">**Örnek 15**</span><span class="sxs-lookup"><span data-stu-id="a942b-333">**Example 15**</span></span>

    * <span data-ttu-id="a942b-334">| Ölçü countdistinct(Computer) aralığı 1 saat</span><span class="sxs-lookup"><span data-stu-id="a942b-334">| measure countdistinct(Computer) Interval 1HOUR</span></span>

<span data-ttu-id="a942b-335">Her saat için raporlama benzersiz bilgisayar sayısını sayar.</span><span class="sxs-lookup"><span data-stu-id="a942b-335">Counts the number of unique computers reporting for every hour.</span></span>

<span data-ttu-id="a942b-336">**Örnek 16**</span><span class="sxs-lookup"><span data-stu-id="a942b-336">**Example 16**</span></span>

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total” | measure avg(CounterValue) by Computer Interval 1HOUR
```

<span data-ttu-id="a942b-337">% İşlemci zamanı bilgisayara göre gruplandırır ve her saat için ortalamasını döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-337">Groups % Processor Time by Computer, and returns the average for every hour.</span></span>

<span data-ttu-id="a942b-338">**Örnek 17**</span><span class="sxs-lookup"><span data-stu-id="a942b-338">**Example 17**</span></span>

    Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES

<span data-ttu-id="a942b-339">Yöntemi tarafından W3CIISLog grupları ve en fazla 5 dakikada döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-339">Groups W3CIISLog by method, and returns the maximum for every 5 minutes.</span></span>

<span data-ttu-id="a942b-340">**Örnek 18**</span><span class="sxs-lookup"><span data-stu-id="a942b-340">**Example 18**</span></span>

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer Interval 1HOUR
```

<span data-ttu-id="a942b-341">% İşlemci zamanı bilgisayar grupları ve her saat için minimum ve ortalama, 75. yüzdebirlik ve maksimum döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-341">Groups % Processor Time by computer, and returns the minimum, average, 75th percentile, and maximum for every hour.</span></span>

<span data-ttu-id="a942b-342">**Örnek 19**</span><span class="sxs-lookup"><span data-stu-id="a942b-342">**Example 19**</span></span>

```
Type:Perf CounterName=”% Processor Time”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer, InstanceName Interval 1HOUR
```

<span data-ttu-id="a942b-343">% İşlemci zamanı ilk bilgisayar tarafından ardından örnek adını göre gruplandırır ve her saat için minimum ve ortalama, 75. yüzdebirlik ve maksimum döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-343">Groups % Processor Time first by computer and then by Instance name, and returns the minimum, average, 75th percentile, and maximum for every hour.</span></span>

<span data-ttu-id="a942b-344">**Örnek 20**</span><span class="sxs-lookup"><span data-stu-id="a942b-344">**Example 20**</span></span>

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | measure max(product(CounterValue,60)) as MaxDWPerMin by InstanceName Interval 1HOUR
```

<span data-ttu-id="a942b-345">Bilgisayarınızda disk yazma işlemleri her disk için dakika başına maksimum hesaplar.</span><span class="sxs-lookup"><span data-stu-id="a942b-345">Calculates the maximum of disk writes per minute for every disk on your computer.</span></span>

### <a name="where"></a><span data-ttu-id="a942b-346">Burada</span><span class="sxs-lookup"><span data-stu-id="a942b-346">Where</span></span>
<span data-ttu-id="a942b-347">Sözdizimi:</span><span class="sxs-lookup"><span data-stu-id="a942b-347">Syntax:</span></span>

```
**where** AggregatedValue>20
```

<span data-ttu-id="a942b-348">Yalnızca sonra kullanılabilir bir *ölçü* daha fazla toplanmış filtrelemek için komutu sonuçları *ölçü* toplama işlevine üretilen.</span><span class="sxs-lookup"><span data-stu-id="a942b-348">Can only be used after a *Measure* command to further filter the aggregated results that the *Measure* aggregation function has produced.</span></span>

<span data-ttu-id="a942b-349">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="a942b-349">Examples:</span></span>

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) as MAXCPU by Computer

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) by Computer | where (AggregatedValue>50 and AggregatedValue<90)



### <a name="dedup"></a><span data-ttu-id="a942b-350">Yinelenenleri kaldırma</span><span class="sxs-lookup"><span data-stu-id="a942b-350">Dedup</span></span>
<span data-ttu-id="a942b-351">Sözdizimi:</span><span class="sxs-lookup"><span data-stu-id="a942b-351">Syntax:</span></span>

    Dedup FieldName

<span data-ttu-id="a942b-352">Belirtilen alan için her benzersiz değer bulunan ilk belgeyi döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-352">Returns the first document found for every unique value of the given field.</span></span>

<span data-ttu-id="a942b-353">Örnek:</span><span class="sxs-lookup"><span data-stu-id="a942b-353">Example:</span></span>

    Type=Event | Dedup EventID | sort TimeGenerated DESC

<span data-ttu-id="a942b-354">Bu örnek olay kimliği başına bir olay (en son olay) döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-354">This example returns one event (the latest event) per EventID.</span></span>

### <a name="join"></a><span data-ttu-id="a942b-355">Birleştir</span><span class="sxs-lookup"><span data-stu-id="a942b-355">Join</span></span>
<span data-ttu-id="a942b-356">Tek bir sonuç kümesi oluşturmak için iki sorguların sonuçlarını birleştirir.</span><span class="sxs-lookup"><span data-stu-id="a942b-356">Joins the results of two queries to form a single result set.</span></span>  <span data-ttu-id="a942b-357">İzleme tabloda birden fazla birleştirme türü destekler.</span><span class="sxs-lookup"><span data-stu-id="a942b-357">Supports multiple join types described in the follow table.</span></span>

| <span data-ttu-id="a942b-358">Katılım Türü</span><span class="sxs-lookup"><span data-stu-id="a942b-358">Join type</span></span> | <span data-ttu-id="a942b-359">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a942b-359">Description</span></span> |
|:--|:--|
| <span data-ttu-id="a942b-360">İç</span><span class="sxs-lookup"><span data-stu-id="a942b-360">inner</span></span> | <span data-ttu-id="a942b-361">Yalnızca kayıtları eşleşen değere sahip iki sorgularda döndür.</span><span class="sxs-lookup"><span data-stu-id="a942b-361">Return only records with a matching value in both queries.</span></span> |
| <span data-ttu-id="a942b-362">Dış</span><span class="sxs-lookup"><span data-stu-id="a942b-362">outer</span></span> | <span data-ttu-id="a942b-363">Tüm kayıtları hem sorgularından döndür.</span><span class="sxs-lookup"><span data-stu-id="a942b-363">Return all records from both queries.</span></span>  |
| <span data-ttu-id="a942b-364">Sol</span><span class="sxs-lookup"><span data-stu-id="a942b-364">left</span></span>  | <span data-ttu-id="a942b-365">Sol sorgu ve eşleşen kayıtları doğru sorgudan tüm kayıtları döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-365">Return all records from left query and matching records from right query.</span></span> |


- <span data-ttu-id="a942b-366">Birleştirmeler şu anda desteklemediği içeren sorgularını **IN** anahtar sözcüğü, **ölçü** komut veya **Genişlet** alana sağ sorgudan hedefler komutu.</span><span class="sxs-lookup"><span data-stu-id="a942b-366">Joins do not currently support queries that include the **IN** keyword, the **Measure** command or the **Extend** command if it targets a field from the right query.</span></span>
- <span data-ttu-id="a942b-367">Bu gibi durumlarda, yalnızca tek bir alan şu anda bir birleştirme ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a942b-367">You can currently include only a single field in a join.</span></span>
- <span data-ttu-id="a942b-368">Tek bir arama birden fazla birleşim içermeyebilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-368">A single search may not include more than one join.</span></span>

<span data-ttu-id="a942b-369">**Sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="a942b-369">**Syntax**</span></span>

```
<left-query> | JOIN <join-type> <left-query-field-name> (<right-query>) <right-query-field-name>
```

<span data-ttu-id="a942b-370">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="a942b-370">**Examples**</span></span>

<span data-ttu-id="a942b-371">Farklı bir birleştirme türü göstermek için bir veri türü birleştirme MyBackup_CL her bilgisayar için sinyal ile adlı özel bir günlük toplanan göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="a942b-371">To illustrate the different join types, consider joining a data type collected from a custom log called MyBackup_CL with the heartbeat for each computer.</span></span>  <span data-ttu-id="a942b-372">Bu veri türleri, aşağıdaki veri içeriyor.</span><span class="sxs-lookup"><span data-stu-id="a942b-372">These datatypes have the following data.</span></span>

`Type = MyBackup_CL`

| <span data-ttu-id="a942b-373">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="a942b-373">TimeGenerated</span></span> | <span data-ttu-id="a942b-374">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="a942b-374">Computer</span></span> | <span data-ttu-id="a942b-375">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="a942b-375">LastBackupStatus</span></span> |
|:---|:---|:---|
| <span data-ttu-id="a942b-376">20/4/2017 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="a942b-376">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="a942b-377">Srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="a942b-377">srv01.contoso.com</span></span> | <span data-ttu-id="a942b-378">Başarılı</span><span class="sxs-lookup"><span data-stu-id="a942b-378">Success</span></span> |
| <span data-ttu-id="a942b-379">20/4/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="a942b-379">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="a942b-380">SRV02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="a942b-380">srv02.contoso.com</span></span> | <span data-ttu-id="a942b-381">Başarılı</span><span class="sxs-lookup"><span data-stu-id="a942b-381">Success</span></span> |
| <span data-ttu-id="a942b-382">20/4/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="a942b-382">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="a942b-383">srv03.contoso.com</span><span class="sxs-lookup"><span data-stu-id="a942b-383">srv03.contoso.com</span></span> | <span data-ttu-id="a942b-384">Hata</span><span class="sxs-lookup"><span data-stu-id="a942b-384">Failure</span></span> |

<span data-ttu-id="a942b-385">`Type = Hearbeat`(Yalnızca bir alt kümesini gösterilen alanları)</span><span class="sxs-lookup"><span data-stu-id="a942b-385">`Type = Hearbeat` (Only a subset of fields shown)</span></span>

| <span data-ttu-id="a942b-386">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="a942b-386">TimeGenerated</span></span> | <span data-ttu-id="a942b-387">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="a942b-387">Computer</span></span> | <span data-ttu-id="a942b-388">ComputerIP</span><span class="sxs-lookup"><span data-stu-id="a942b-388">ComputerIP</span></span> |
|:---|:---|:---|
| <span data-ttu-id="a942b-389">21/4/2017 12:01:34.482 PM</span><span class="sxs-lookup"><span data-stu-id="a942b-389">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="a942b-390">Srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="a942b-390">srv01.contoso.com</span></span> | <span data-ttu-id="a942b-391">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="a942b-391">10.10.100.1</span></span> |
| <span data-ttu-id="a942b-392">21/4/2017 12:02:21.916 PM</span><span class="sxs-lookup"><span data-stu-id="a942b-392">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="a942b-393">SRV02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="a942b-393">srv02.contoso.com</span></span> | <span data-ttu-id="a942b-394">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="a942b-394">10.10.100.2</span></span> |
| <span data-ttu-id="a942b-395">21/4/2017 12:01:47.373 PM</span><span class="sxs-lookup"><span data-stu-id="a942b-395">4/21/2017 12:01:47.373 PM</span></span> | <span data-ttu-id="a942b-396">srv04.contoso.com</span><span class="sxs-lookup"><span data-stu-id="a942b-396">srv04.contoso.com</span></span> | <span data-ttu-id="a942b-397">10.10.100.4</span><span class="sxs-lookup"><span data-stu-id="a942b-397">10.10.100.4</span></span> |

#### <a name="inner-join"></a><span data-ttu-id="a942b-398">iç birleşim</span><span class="sxs-lookup"><span data-stu-id="a942b-398">inner join</span></span>

`Type=MyBackup_CL | join inner Computer (Type=Heartbeat) Computer`

<span data-ttu-id="a942b-399">Aşağıdaki kayıtları bilgisayar alanı hem de veri türleri için eşleştiği döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-399">Returns the following records where the computer field matches for both datatypes.</span></span>

| <span data-ttu-id="a942b-400">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="a942b-400">Computer</span></span>| <span data-ttu-id="a942b-401">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="a942b-401">TimeGenerated</span></span> | <span data-ttu-id="a942b-402">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="a942b-402">LastBackupStatus</span></span> | <span data-ttu-id="a942b-403">TimeGenerated_joined</span><span class="sxs-lookup"><span data-stu-id="a942b-403">TimeGenerated_joined</span></span> | <span data-ttu-id="a942b-404">ComputerIP_joined</span><span class="sxs-lookup"><span data-stu-id="a942b-404">ComputerIP_joined</span></span> | <span data-ttu-id="a942b-405">Type_joined</span><span class="sxs-lookup"><span data-stu-id="a942b-405">Type_joined</span></span> |
|:---|:---|:---|:---|:---|:---|
| <span data-ttu-id="a942b-406">Srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="a942b-406">srv01.contoso.com</span></span> | <span data-ttu-id="a942b-407">20/4/2017 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="a942b-407">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="a942b-408">Başarılı</span><span class="sxs-lookup"><span data-stu-id="a942b-408">Success</span></span> | <span data-ttu-id="a942b-409">21/4/2017 12:01:34.482 PM</span><span class="sxs-lookup"><span data-stu-id="a942b-409">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="a942b-410">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="a942b-410">10.10.100.1</span></span> | <span data-ttu-id="a942b-411">Sinyal</span><span class="sxs-lookup"><span data-stu-id="a942b-411">Heartbeat</span></span> |
| <span data-ttu-id="a942b-412">SRV02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="a942b-412">srv02.contoso.com</span></span> | <span data-ttu-id="a942b-413">20/4/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="a942b-413">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="a942b-414">Başarılı</span><span class="sxs-lookup"><span data-stu-id="a942b-414">Success</span></span> | <span data-ttu-id="a942b-415">21/4/2017 12:02:21.916 PM</span><span class="sxs-lookup"><span data-stu-id="a942b-415">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="a942b-416">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="a942b-416">10.10.100.2</span></span> | <span data-ttu-id="a942b-417">Sinyal</span><span class="sxs-lookup"><span data-stu-id="a942b-417">Heartbeat</span></span> |


#### <a name="outer-join"></a><span data-ttu-id="a942b-418">dış birleşim</span><span class="sxs-lookup"><span data-stu-id="a942b-418">outer join</span></span>

`Type=MyBackup_CL | join outer Computer (Type=Heartbeat) Computer`

<span data-ttu-id="a942b-419">Her iki veri türleri için aşağıdaki kayıtları döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-419">Returns the following records for both datatypes.</span></span>

| <span data-ttu-id="a942b-420">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="a942b-420">Computer</span></span>| <span data-ttu-id="a942b-421">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="a942b-421">TimeGenerated</span></span> | <span data-ttu-id="a942b-422">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="a942b-422">LastBackupStatus</span></span> | <span data-ttu-id="a942b-423">TimeGenerated_joined</span><span class="sxs-lookup"><span data-stu-id="a942b-423">TimeGenerated_joined</span></span> | <span data-ttu-id="a942b-424">ComputerIP_joined</span><span class="sxs-lookup"><span data-stu-id="a942b-424">ComputerIP_joined</span></span> | <span data-ttu-id="a942b-425">Type_joined</span><span class="sxs-lookup"><span data-stu-id="a942b-425">Type_joined</span></span> |
|:---|:---|:---|:---|:---|:---|
| <span data-ttu-id="a942b-426">Srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="a942b-426">srv01.contoso.com</span></span> | <span data-ttu-id="a942b-427">20/4/2017 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="a942b-427">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="a942b-428">Başarılı</span><span class="sxs-lookup"><span data-stu-id="a942b-428">Success</span></span>  | <span data-ttu-id="a942b-429">21/4/2017 12:01:34.482 PM</span><span class="sxs-lookup"><span data-stu-id="a942b-429">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="a942b-430">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="a942b-430">10.10.100.1</span></span> | <span data-ttu-id="a942b-431">Sinyal</span><span class="sxs-lookup"><span data-stu-id="a942b-431">Heartbeat</span></span> |
| <span data-ttu-id="a942b-432">SRV02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="a942b-432">srv02.contoso.com</span></span> | <span data-ttu-id="a942b-433">20/4/2017 02:14:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="a942b-433">4/20/2017 02:14:12.381 AM</span></span> | <span data-ttu-id="a942b-434">Başarılı</span><span class="sxs-lookup"><span data-stu-id="a942b-434">Success</span></span>  | <span data-ttu-id="a942b-435">21/4/2017 12:02:21.916 PM</span><span class="sxs-lookup"><span data-stu-id="a942b-435">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="a942b-436">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="a942b-436">10.10.100.2</span></span> | <span data-ttu-id="a942b-437">Sinyal</span><span class="sxs-lookup"><span data-stu-id="a942b-437">Heartbeat</span></span> |
| <span data-ttu-id="a942b-438">srv03.contoso.com</span><span class="sxs-lookup"><span data-stu-id="a942b-438">srv03.contoso.com</span></span> | <span data-ttu-id="a942b-439">20/4/2017 01:33:35.974 AM</span><span class="sxs-lookup"><span data-stu-id="a942b-439">4/20/2017 01:33:35.974 AM</span></span> | <span data-ttu-id="a942b-440">Hata</span><span class="sxs-lookup"><span data-stu-id="a942b-440">Failure</span></span>  | <span data-ttu-id="a942b-441">21/4/2017 12:01:47.373 PM</span><span class="sxs-lookup"><span data-stu-id="a942b-441">4/21/2017 12:01:47.373 PM</span></span> | | |
| <span data-ttu-id="a942b-442">srv04.contoso.com</span><span class="sxs-lookup"><span data-stu-id="a942b-442">srv04.contoso.com</span></span> |                           |          | <span data-ttu-id="a942b-443">21/4/2017 12:01:47.373 PM</span><span class="sxs-lookup"><span data-stu-id="a942b-443">4/21/2017 12:01:47.373 PM</span></span> | <span data-ttu-id="a942b-444">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="a942b-444">10.10.100.2</span></span> | <span data-ttu-id="a942b-445">Sinyal</span><span class="sxs-lookup"><span data-stu-id="a942b-445">Heartbeat</span></span> |



#### <a name="left-join"></a><span data-ttu-id="a942b-446">Sol birleştirme</span><span class="sxs-lookup"><span data-stu-id="a942b-446">left join</span></span>

`Type=MyBackup_CL | join left Computer (Type=Heartbeat) Computer`

<span data-ttu-id="a942b-447">Aşağıdaki kayıtları MyBackup_CL sinyal eşleşen tüm alanları ile döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-447">Returns the following records from MyBackup_CL with any matching fields from Heartbeat.</span></span>

| <span data-ttu-id="a942b-448">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="a942b-448">Computer</span></span>| <span data-ttu-id="a942b-449">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="a942b-449">TimeGenerated</span></span> | <span data-ttu-id="a942b-450">LastBackupStatus</span><span class="sxs-lookup"><span data-stu-id="a942b-450">LastBackupStatus</span></span> | <span data-ttu-id="a942b-451">TimeGenerated_joined</span><span class="sxs-lookup"><span data-stu-id="a942b-451">TimeGenerated_joined</span></span> | <span data-ttu-id="a942b-452">ComputerIP_joined</span><span class="sxs-lookup"><span data-stu-id="a942b-452">ComputerIP_joined</span></span> | <span data-ttu-id="a942b-453">Type_joined</span><span class="sxs-lookup"><span data-stu-id="a942b-453">Type_joined</span></span> |
|:---|:---|:---|:---|:---|:---|
| <span data-ttu-id="a942b-454">Srv01.contoso.com</span><span class="sxs-lookup"><span data-stu-id="a942b-454">srv01.contoso.com</span></span> | <span data-ttu-id="a942b-455">20/4/2017 01:26:32.137 AM</span><span class="sxs-lookup"><span data-stu-id="a942b-455">4/20/2017 01:26:32.137 AM</span></span> | <span data-ttu-id="a942b-456">Başarılı</span><span class="sxs-lookup"><span data-stu-id="a942b-456">Success</span></span> | <span data-ttu-id="a942b-457">21/4/2017 12:01:34.482 PM</span><span class="sxs-lookup"><span data-stu-id="a942b-457">4/21/2017 12:01:34.482 PM</span></span> | <span data-ttu-id="a942b-458">10.10.100.1</span><span class="sxs-lookup"><span data-stu-id="a942b-458">10.10.100.1</span></span> | <span data-ttu-id="a942b-459">Sinyal</span><span class="sxs-lookup"><span data-stu-id="a942b-459">Heartbeat</span></span> |
| <span data-ttu-id="a942b-460">SRV02.contoso.com</span><span class="sxs-lookup"><span data-stu-id="a942b-460">srv02.contoso.com</span></span> | <span data-ttu-id="a942b-461">20/4/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="a942b-461">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="a942b-462">Başarılı</span><span class="sxs-lookup"><span data-stu-id="a942b-462">Success</span></span> | <span data-ttu-id="a942b-463">21/4/2017 12:02:21.916 PM</span><span class="sxs-lookup"><span data-stu-id="a942b-463">4/21/2017 12:02:21.916 PM</span></span> | <span data-ttu-id="a942b-464">10.10.100.2</span><span class="sxs-lookup"><span data-stu-id="a942b-464">10.10.100.2</span></span> | <span data-ttu-id="a942b-465">Sinyal</span><span class="sxs-lookup"><span data-stu-id="a942b-465">Heartbeat</span></span> |
| <span data-ttu-id="a942b-466">srv03.contoso.com</span><span class="sxs-lookup"><span data-stu-id="a942b-466">srv03.contoso.com</span></span> | <span data-ttu-id="a942b-467">20/4/2017 02:13:12.381 AM</span><span class="sxs-lookup"><span data-stu-id="a942b-467">4/20/2017 02:13:12.381 AM</span></span> | <span data-ttu-id="a942b-468">Hata</span><span class="sxs-lookup"><span data-stu-id="a942b-468">Failure</span></span> | | | |


### <a name="extend"></a><span data-ttu-id="a942b-469">Genişletme</span><span class="sxs-lookup"><span data-stu-id="a942b-469">Extend</span></span>
<span data-ttu-id="a942b-470">Çalışma zamanı alanları içinde sorgu oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a942b-470">Allows you to create run-time fields in queries.</span></span> <span data-ttu-id="a942b-471">Çalışma zamanı alanlar ölçü komutuyla toplama gerçekleştirmek için kullanılamaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a942b-471">Note that run-time fields cannot be used with the measure command to perform aggregation.</span></span>

<span data-ttu-id="a942b-472">**Örnek 1**</span><span class="sxs-lookup"><span data-stu-id="a942b-472">**Example 1**</span></span>

    Type=SQLAssessmentRecommendation | Extend product(RecommendationScore, RecommendationWeight) AS RecommendationWeightedScore
<span data-ttu-id="a942b-473">Gösterir SQL değerlendirmesi önerileri için öneri puan ağırlıklı.</span><span class="sxs-lookup"><span data-stu-id="a942b-473">Shows weighted recommendation score for SQL Assessment recommendations.</span></span>

<span data-ttu-id="a942b-474">**Örnek 2**</span><span class="sxs-lookup"><span data-stu-id="a942b-474">**Example 2**</span></span>

    Type=Perf CounterName="Private Bytes" | EXTEND div(CounterValue,1024) AS KBs | Select CounterValue,Computer,KBs
<span data-ttu-id="a942b-475">Sayaç değeri içinde KB yerine bayt gösterir.</span><span class="sxs-lookup"><span data-stu-id="a942b-475">Shows counter value in KBs instead of bytes.</span></span>

<span data-ttu-id="a942b-476">**Örnek 3**</span><span class="sxs-lookup"><span data-stu-id="a942b-476">**Example 3**</span></span>

    Type=WireData | EXTEND scale(TotalBytes,0,100) AS ScaledTotalBytes | Select ScaledTotalBytes,TotalBytes | SORT TotalBytes DESC
<span data-ttu-id="a942b-477">0 ile 100 arasında olduğuna gibi tüm sonuçları WireData TotalBytes değerini ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="a942b-477">Scales the value of WireData TotalBytes, such that all results are between 0 and 100.</span></span>

<span data-ttu-id="a942b-478">**Örnek 4**</span><span class="sxs-lookup"><span data-stu-id="a942b-478">**Example 4**</span></span>

```
Type=Perf CounterName="% Processor Time" | EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION
```
<span data-ttu-id="a942b-479">Yüzde 50 olarak düşük ve diğerleri olarak yüksek değerinden performans sayacı değerlerini etiketler.</span><span class="sxs-lookup"><span data-stu-id="a942b-479">Tags Perf Counter Values less than 50 percent as LOW, and others as HIGH.</span></span>

<span data-ttu-id="a942b-480">**Örnek 5**</span><span class="sxs-lookup"><span data-stu-id="a942b-480">**Example 5**</span></span>

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | Extend product(CounterValue,60) as DWPerMin| measure max(DWPerMin) by InstanceName Interval 1HOUR
```
<span data-ttu-id="a942b-481">Bilgisayarınızda disk yazma işlemleri her disk için dakika başına maksimum hesaplar.</span><span class="sxs-lookup"><span data-stu-id="a942b-481">Calculates the maximum of disk writes per minute for every disk on your computer.</span></span>

<span data-ttu-id="a942b-482">**Desteklenen işlevler**</span><span class="sxs-lookup"><span data-stu-id="a942b-482">**Supported functions**</span></span>

| <span data-ttu-id="a942b-483">İşlevi</span><span class="sxs-lookup"><span data-stu-id="a942b-483">Function</span></span> | <span data-ttu-id="a942b-484">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a942b-484">Description</span></span> | <span data-ttu-id="a942b-485">Sözdizimi örnekleri</span><span class="sxs-lookup"><span data-stu-id="a942b-485">Syntax examples</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a942b-486">Abs</span><span class="sxs-lookup"><span data-stu-id="a942b-486">abs</span></span> |<span data-ttu-id="a942b-487">Belirtilen değer ya da işlevi mutlak değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-487">Returns the absolute value of the specified value or function.</span></span> |`abs(x)` <br> `abs(-5)` |
| <span data-ttu-id="a942b-488">ACOS</span><span class="sxs-lookup"><span data-stu-id="a942b-488">acos</span></span> |<span data-ttu-id="a942b-489">Bir değer veya bir işlev ARC kosinüsünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-489">Returns arc cosine of a value or a function.</span></span> |`acos(x)` |
| <span data-ttu-id="a942b-490">ve</span><span class="sxs-lookup"><span data-stu-id="a942b-490">and</span></span> |<span data-ttu-id="a942b-491">Tüm işlenenleri true olarak değerlendirmek ve yalnızca, true değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-491">Returns a value of true if and only if all of its operands evaluate to true.</span></span> |`and(not(exists(popularity)),exists(price))` |
| <span data-ttu-id="a942b-492">asin</span><span class="sxs-lookup"><span data-stu-id="a942b-492">asin</span></span> |<span data-ttu-id="a942b-493">Bir değer veya bir işlev ARC sinüsünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-493">Returns arc sine of a value or a function.</span></span> |`asin(x)` |
| <span data-ttu-id="a942b-494">atan</span><span class="sxs-lookup"><span data-stu-id="a942b-494">atan</span></span> |<span data-ttu-id="a942b-495">Bir değer veya bir işlev ARC tanjantını döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-495">Returns arc tangent of a value or a function.</span></span> |`atan(x)` |
| <span data-ttu-id="a942b-496">ATAN2</span><span class="sxs-lookup"><span data-stu-id="a942b-496">atan2</span></span> |<span data-ttu-id="a942b-497">Dikdörtgen koordinatları dönüştürme işlemini kaynaklanan olan açıyı döndürür x, y Kutupsal koordinatları.</span><span class="sxs-lookup"><span data-stu-id="a942b-497">Returns the angle resulting from the conversion of the rectangular coordinates x,y to polar coordinates.</span></span> |`atan2(x,y)` |
| <span data-ttu-id="a942b-498">cbrt</span><span class="sxs-lookup"><span data-stu-id="a942b-498">cbrt</span></span> |<span data-ttu-id="a942b-499">Küp kökü.</span><span class="sxs-lookup"><span data-stu-id="a942b-499">Cube root.</span></span> |`cbrt(x)` |
| <span data-ttu-id="a942b-500">ceil</span><span class="sxs-lookup"><span data-stu-id="a942b-500">ceil</span></span> |<span data-ttu-id="a942b-501">Bir tamsayıya yuvarlanır.</span><span class="sxs-lookup"><span data-stu-id="a942b-501">Rounds up to an integer.</span></span> |`ceil(x)`  <br> <span data-ttu-id="a942b-502">`ceil(5.6)`6'yı döndürür</span><span class="sxs-lookup"><span data-stu-id="a942b-502">`ceil(5.6)` Returns 6</span></span> |
| <span data-ttu-id="a942b-503">cos</span><span class="sxs-lookup"><span data-stu-id="a942b-503">cos</span></span> |<span data-ttu-id="a942b-504">Bir açının kosinüsünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-504">Returns cosine of an angle.</span></span> |`cos(x)` |
| <span data-ttu-id="a942b-505">COSH</span><span class="sxs-lookup"><span data-stu-id="a942b-505">cosh</span></span> |<span data-ttu-id="a942b-506">Bir açının hiperbolik kosinüsünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-506">Returns hyperbolic cosine of an angle.</span></span> |`cosh(x)` |
| <span data-ttu-id="a942b-507">def</span><span class="sxs-lookup"><span data-stu-id="a942b-507">def</span></span> |<span data-ttu-id="a942b-508">Varsayılan kısaltması.</span><span class="sxs-lookup"><span data-stu-id="a942b-508">Abbreviation for default.</span></span> <span data-ttu-id="a942b-509">Alan "alanını" değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-509">Returns the value of field "field".</span></span> <span data-ttu-id="a942b-510">Alan mevcut değilse, belirtilen varsayılan değerini döndürür ve ilk değer verir nerede: `exists()==true`.</span><span class="sxs-lookup"><span data-stu-id="a942b-510">If the field does not exist, returns the default value specified and yields the first value where: `exists()==true`.</span></span> |<span data-ttu-id="a942b-511">`def(rating,5)`.</span><span class="sxs-lookup"><span data-stu-id="a942b-511">`def(rating,5)`.</span></span> <span data-ttu-id="a942b-512">Bu def() işlevi derecelendirme döndürür veya derecelendirmesi belgede belirtilmişse, 5 döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-512">This def() function returns the rating, or if no rating is specified in the document, returns 5.</span></span> <br> <span data-ttu-id="a942b-513">`def(myfield, 1.0)`eşdeğer olan `if(exists(myfield),myfield,1.0)`.</span><span class="sxs-lookup"><span data-stu-id="a942b-513">`def(myfield, 1.0)` is equivalent to `if(exists(myfield),myfield,1.0)`.</span></span> |
| <span data-ttu-id="a942b-514">derece</span><span class="sxs-lookup"><span data-stu-id="a942b-514">deg</span></span> |<span data-ttu-id="a942b-515">Radyan cinsinden dereceye dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-515">Converts radians to degrees.</span></span> |`deg(x)` |
| <span data-ttu-id="a942b-516">div</span><span class="sxs-lookup"><span data-stu-id="a942b-516">div</span></span> |<span data-ttu-id="a942b-517">`div(x,y)`böler y x.</span><span class="sxs-lookup"><span data-stu-id="a942b-517">`div(x,y)` divides x by y.</span></span> |`div(1,y)` <br> `div(sum(x,100),max(y,1))` |
| <span data-ttu-id="a942b-518">Dağıtım</span><span class="sxs-lookup"><span data-stu-id="a942b-518">dist</span></span> |<span data-ttu-id="a942b-519">İki vektörüne (nokta) n boyutlu bir alanda arasındaki uzaklığı döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-519">Returns the distance between two vectors, (points) in an n-dimensional space.</span></span> <span data-ttu-id="a942b-520">Güç artı iki veya daha çok, ValueSource örneği alır ve iki vektörü arasındaki uzaklıkları hesaplar.</span><span class="sxs-lookup"><span data-stu-id="a942b-520">Takes in the power, plus two or more, ValueSource instances, and calculates the distances between the two vectors.</span></span> <span data-ttu-id="a942b-521">Her ValueSource bir sayı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a942b-521">Each ValueSource must be a number.</span></span> <span data-ttu-id="a942b-522">Geçirilen ValueSource örneklerinin bir çift sayı olmalıdır ve ilk yarı ilk vektör temsil eder ve ikinci yarısındaki temsil ikinci vektör yöntemi varsayar.</span><span class="sxs-lookup"><span data-stu-id="a942b-522">There must be an even number of ValueSource instances passed in, and the method assumes that the first half represent the first vector and the second half represent the second vector.</span></span> |<span data-ttu-id="a942b-523">`dist(2, x, y, 0, 0)`(0,0) arasındaki Euclidean uzaklığı hesaplar ve (x, y) her belge için.</span><span class="sxs-lookup"><span data-stu-id="a942b-523">`dist(2, x, y, 0, 0)` Calculates the Euclidean distance between (0,0) and (x,y) for each document.</span></span> <br> <span data-ttu-id="a942b-524">`dist(1, x, y, 0, 0)`(0,0) arasındaki Manhattan (taxicab) uzaklığı hesaplar ve (x, y) her belge için.</span><span class="sxs-lookup"><span data-stu-id="a942b-524">`dist(1, x, y, 0, 0)` Calculates the Manhattan (taxicab) distance between (0,0) and (x,y) for each document.</span></span> <br> <span data-ttu-id="a942b-525">`dist(2,,x,y,z,0,0,0)`(0,0,0) arasındaki Euclidean uzaklığı ve (x, y, z) her belge için.</span><span class="sxs-lookup"><span data-stu-id="a942b-525">`dist(2,,x,y,z,0,0,0)` Euclidean distance between (0,0,0) and (x,y,z) for each document.</span></span><br><span data-ttu-id="a942b-526">`dist(1,x,y,z,e,f,g)`Arasındaki Manhattan uzaklığı (x, y, z) ve (e, f, g), burada her harf, bir alan adı.</span><span class="sxs-lookup"><span data-stu-id="a942b-526">`dist(1,x,y,z,e,f,g)` Manhattan distance between (x,y,z) and (e,f,g), where each letter is a field name.</span></span> |
| <span data-ttu-id="a942b-527">var</span><span class="sxs-lookup"><span data-stu-id="a942b-527">exists</span></span> |<span data-ttu-id="a942b-528">Alan varsa TRUE üyesi döndürür bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a942b-528">Returns TRUE if any member of the field exists.</span></span> |<span data-ttu-id="a942b-529">`exists(author)`"Yazar" alanda bir değere sahip herhangi bir belgeyi TRUE döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-529">`exists(author)` Returns TRUE for any document that has a value in the "author" field.</span></span><br><span data-ttu-id="a942b-530">`exists(query(price:5.00))`"Fiyat" eşleşirse, TRUE döndürür "5.00".</span><span class="sxs-lookup"><span data-stu-id="a942b-530">`exists(query(price:5.00))` Returns TRUE if "price" matches,"5.00".</span></span> |
| <span data-ttu-id="a942b-531">exp</span><span class="sxs-lookup"><span data-stu-id="a942b-531">exp</span></span> |<span data-ttu-id="a942b-532">Euler'ın sayı x kuvvetini döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-532">Returns Euler's number raised to power x.</span></span> |`exp(x)` |
| <span data-ttu-id="a942b-533">Kat</span><span class="sxs-lookup"><span data-stu-id="a942b-533">floor</span></span> |<span data-ttu-id="a942b-534">Tamsayıya yuvarlar kapalı.</span><span class="sxs-lookup"><span data-stu-id="a942b-534">Rounds down to an integer.</span></span> |`floor(x)`  <br> <span data-ttu-id="a942b-535">`floor(5.6)`5 döndürür</span><span class="sxs-lookup"><span data-stu-id="a942b-535">`floor(5.6)` Returns 5</span></span> |
| <span data-ttu-id="a942b-536">hypo</span><span class="sxs-lookup"><span data-stu-id="a942b-536">hypo</span></span> |<span data-ttu-id="a942b-537">Ara taşması veya underflow olmadan Sqrt(SUM(pow(x,2),pow(y,2))) döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-537">Returns sqrt(sum(pow(x,2),pow(y,2))) without intermediate overflow or underflow.</span></span> |`hypo(x,y)`  <br> ` |
| <span data-ttu-id="a942b-538">Eğer</span><span class="sxs-lookup"><span data-stu-id="a942b-538">if</span></span> |<span data-ttu-id="a942b-539">Koşullu işlevi sorguları sağlar.</span><span class="sxs-lookup"><span data-stu-id="a942b-539">Enables conditional function queries.</span></span> <span data-ttu-id="a942b-540">İçinde `if(test,value1,value2)`, test olduğundan veya bir mantıksal değer veya bir mantıksal bir değer (TRUE veya FALSE) döndürür ifade başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="a942b-540">In `if(test,value1,value2)`, test is or refers to a logical value or expression that returns a logical value (TRUE or FALSE).</span></span> <span data-ttu-id="a942b-541">`value1`Test TRUE döndürürse değer işlev tarafından döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a942b-541">`value1` is the value returned by the function if test yields TRUE.</span></span> <span data-ttu-id="a942b-542">`value2`Test FALSE döndürürse değer işlev tarafından döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a942b-542">`value2` is the value returned by the function if test yields FALSE.</span></span> <span data-ttu-id="a942b-543">Bir ifade, Boole değerleri çıkarır herhangi bir işlev olabilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-543">An expression can be any function which outputs boolean values.</span></span> <span data-ttu-id="a942b-544">Ayrıca, durum değeri 0 false olarak yorumlanır veya dizeler, döndürme case hangi boş dize false olarak yorumlanır sayısal değerler döndüren bir işlev olabilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-544">It can also be a function returning numeric values, in which case value 0 is interpreted as false, or returning strings, in which case empty string is interpreted as false.</span></span> |<span data-ttu-id="a942b-545">`if(termfreq(cat,'electronics'),popularity,42)`Bu işlev her belge kat alanında "elektronik" terimi içerip içermediğini denetler.</span><span class="sxs-lookup"><span data-stu-id="a942b-545">`if(termfreq(cat,'electronics'),popularity,42)` This function checks each document to see if it contains the term "electronics" in the cat field.</span></span> <span data-ttu-id="a942b-546">Aşması durumunda popülerliği alanının değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a942b-546">If it does, then the value of the popularity field is returned.</span></span> <span data-ttu-id="a942b-547">Aksi takdirde, 42 değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a942b-547">Otherwise, the value of 42 is returned.</span></span> |
| <span data-ttu-id="a942b-548">Doğrusal</span><span class="sxs-lookup"><span data-stu-id="a942b-548">linear</span></span> |<span data-ttu-id="a942b-549">Implements `m*x+c`, burada m ve c sabitleri ve x, rasgele bir işlev.</span><span class="sxs-lookup"><span data-stu-id="a942b-549">Implements `m*x+c`, where m and c are constants, and x is an arbitrary function.</span></span> <span data-ttu-id="a942b-550">Bu eşdeğer olan `sum(product(m,x),c)`, ancak tek bir işlevi uygulanan biraz daha verimlidir.</span><span class="sxs-lookup"><span data-stu-id="a942b-550">This is equivalent to `sum(product(m,x),c)`, but slightly more efficient as it is implemented as a single function.</span></span> |<span data-ttu-id="a942b-551">`linear(x,m,c) linear(x,2,4)`döndürür`2*x+4`</span><span class="sxs-lookup"><span data-stu-id="a942b-551">`linear(x,m,c) linear(x,2,4)` returns `2*x+4`</span></span> |
| <span data-ttu-id="a942b-552">ln</span><span class="sxs-lookup"><span data-stu-id="a942b-552">ln</span></span> |<span data-ttu-id="a942b-553">Belirtilen işlev doğal günlüğü döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-553">Returns the natural log of the specified function.</span></span> |`ln(x)` |
| <span data-ttu-id="a942b-554">Günlük</span><span class="sxs-lookup"><span data-stu-id="a942b-554">log</span></span> |<span data-ttu-id="a942b-555">Belirtilen işlev temel 10 günlük döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-555">Returns the log base 10 of the specified function.</span></span> |`log(x)   log(sum(x,100))` |
| <span data-ttu-id="a942b-556">eşleme</span><span class="sxs-lookup"><span data-stu-id="a942b-556">map</span></span> |<span data-ttu-id="a942b-557">Min ve Mak, belirtilen hedef kapsayıcı içinde kalan herhangi bir giriş işlevi x değerleri eşler.</span><span class="sxs-lookup"><span data-stu-id="a942b-557">Maps any values of an input function x that fall within min and max, inclusive to the specified target.</span></span> <span data-ttu-id="a942b-558">Bağımsız değişkenler min ve Mak olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a942b-558">The arguments min and max must be constants.</span></span> <span data-ttu-id="a942b-559">Bağımsız değişkenler hedef ve varsayılan sabitler veya İşlevler olabilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-559">The arguments target and default can be constants or functions.</span></span> <span data-ttu-id="a942b-560">X değerini min ve max arasında uymazsa sonra x değeri döndürülür ya da 5 bağımsız değişkeni olarak belirtilen bir varsayılan değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="a942b-560">If the value of x does not fall between min and max, then either the value of x is returned, or a default value is returned if specified as a 5th argument.</span></span> |<span data-ttu-id="a942b-561">`map(x,min,max,target) map(x,0,0,1)`0 ve 1 tüm değerleri değiştirir.</span><span class="sxs-lookup"><span data-stu-id="a942b-561">`map(x,min,max,target) map(x,0,0,1)` Changes any values of 0 to 1.</span></span> <span data-ttu-id="a942b-562">Bu, varsayılan 0 değerleri işleme yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-562">This can be useful in handling default 0 values.</span></span><br> <span data-ttu-id="a942b-563">`map(x,min,max,target,default)    map(x,0,100,1,-1)`0 ile 100 için 1 arasında herhangi bir değere ve diğer tüm değerler -1 olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="a942b-563">`map(x,min,max,target,default)    map(x,0,100,1,-1)` Changes any values between 0 and 100 to 1, and all other values to -1.</span></span><br>  <span data-ttu-id="a942b-564">`map(x,0,100,sum(x,599),docfreq(text,solr))`Tüm değerleri 0 ile 100 x + 599 ve diğer tüm değerler arasındaki alan metni ' solr' terimi sıklığını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="a942b-564">`map(x,0,100,sum(x,599),docfreq(text,solr))` Changes any values between 0 and 100 to x+599, and all other values to frequency of the term 'solr' in the field text.</span></span> |
| <span data-ttu-id="a942b-565">max</span><span class="sxs-lookup"><span data-stu-id="a942b-565">max</span></span> |<span data-ttu-id="a942b-566">Birden çok iç içe geçmiş işlevler veya bağımsız değişken olarak belirtilmiş sabitleri en büyük sayısal değerini döndürür: `max(x,y,...)`.</span><span class="sxs-lookup"><span data-stu-id="a942b-566">Returns the maximum numeric value of multiple nested functions or constants, which are specified as arguments: `max(x,y,...)`.</span></span> <span data-ttu-id="a942b-567">Max işlevi de "başka bir işlev bottoming" için yararlı olabilir veya bazı alan sabiti belirtildi.</span><span class="sxs-lookup"><span data-stu-id="a942b-567">The max function can also be useful for "bottoming out" another function or field at some specified constant.</span></span>  <span data-ttu-id="a942b-568">Kullanım `field(myfield,max)` tek değerli bir alanı en büyük değerini seçmek için sözdizimi.</span><span class="sxs-lookup"><span data-stu-id="a942b-568">Use the `field(myfield,max)` syntax for selecting the maximum value of a single multivalued field.</span></span> |`max(myfield,myotherfield,0)` |
| <span data-ttu-id="a942b-569">dk</span><span class="sxs-lookup"><span data-stu-id="a942b-569">min</span></span> |<span data-ttu-id="a942b-570">Bağımsız değişken olarak belirtilmiş sabitlerin birden çok iç içe geçmiş işlevler en küçük sayısal değeri döndürür: `min(x,y,...)`.</span><span class="sxs-lookup"><span data-stu-id="a942b-570">Returns the minimum numeric value of multiple nested functions of constants, which are specified as arguments: `min(x,y,...)`.</span></span> <span data-ttu-id="a942b-571">Min işlevi de "üst sınırı" bir sabit kullanarak bir işlev sağlamak için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-571">The min function can also be useful for providing an "upper bound" on a function using a constant.</span></span> <span data-ttu-id="a942b-572">Kullanım `field(myfield,min)` tek değerli bir alanı en küçük değeri seçmek için sözdizimi.</span><span class="sxs-lookup"><span data-stu-id="a942b-572">Use the `field(myfield,min)` syntax for selecting the minimum value of a single multivalued field.</span></span> |`min(myfield,myotherfield,0)` |
| <span data-ttu-id="a942b-573">mod</span><span class="sxs-lookup"><span data-stu-id="a942b-573">mod</span></span> |<span data-ttu-id="a942b-574">Modulus işlevi y ile x işlevinin hesaplar.</span><span class="sxs-lookup"><span data-stu-id="a942b-574">Computes the modulus of the function x by the function y.</span></span> |`mod(1,x)` <br> `mod(sum(x,100), max(y,1))` |
| <span data-ttu-id="a942b-575">MS</span><span class="sxs-lookup"><span data-stu-id="a942b-575">ms</span></span> |<span data-ttu-id="a942b-576">Bağımsız değişkenler arasındaki farkı milisaniye olarak döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-576">Returns milliseconds of difference between its arguments.</span></span> <span data-ttu-id="a942b-577">Tarihleri UNIX ya da POSIX zaman dönem, gece yarısı, 1 Ocak 1970 UTC göreli ' dir.</span><span class="sxs-lookup"><span data-stu-id="a942b-577">Dates are relative to the Unix or POSIX time epoch, midnight, January 1, 1970 UTC.</span></span> <span data-ttu-id="a942b-578">Bağımsız değişkenler bir dizinlenmiş TrieDateField ya da sabit tarih temelli tarih matematik adı olması veya artık olabilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-578">Arguments may be the name of an indexed TrieDateField, or date math based on a constant date or NOW .</span></span> <span data-ttu-id="a942b-579">`ms()`eşdeğer olan `ms(NOW)`, dönem itibaren milisaniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="a942b-579">`ms()` is equivalent to `ms(NOW)`, number of milliseconds since the epoch.</span></span> <span data-ttu-id="a942b-580">`ms(a)`bağımsız değişkeni temsil eden dönem itibaren milisaniye sayısını döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-580">`ms(a)` returns the number of milliseconds since the epoch that the argument represents.</span></span> <span data-ttu-id="a942b-581">`ms(a,b)`Bu b milisaniye sayısını döndürür önce oluşur olduğu `a - b`.</span><span class="sxs-lookup"><span data-stu-id="a942b-581">`ms(a,b)` returns the number of milliseconds that b occurs before a, which is `a - b`.</span></span> |`ms(NOW/DAY)`<br>`ms(2000-01-01T00:00:00Z)`<br>`ms(mydatefield)`<br>`ms(NOW,mydatefield)`<br>`ms(mydatefield,2000-01-01T00:00:00Z)`<br>`ms(datefield1,datefield2)` |
| <span data-ttu-id="a942b-582">değil</span><span class="sxs-lookup"><span data-stu-id="a942b-582">not</span></span> |<span data-ttu-id="a942b-583">Mantıksal değeri kadar çevrilerek sarmalanmış işlev.</span><span class="sxs-lookup"><span data-stu-id="a942b-583">The logically negated value of the wrapped function.</span></span> |<span data-ttu-id="a942b-584">`not(exists(author))`Yalnızca TRUE olduğunda `exists(author)` false olur.</span><span class="sxs-lookup"><span data-stu-id="a942b-584">`not(exists(author))` TRUE only when `exists(author)` is false.</span></span> |
| <span data-ttu-id="a942b-585">or</span><span class="sxs-lookup"><span data-stu-id="a942b-585">or</span></span> |<span data-ttu-id="a942b-586">Mantıksal ayrım.</span><span class="sxs-lookup"><span data-stu-id="a942b-586">A logical disjunction.</span></span> |<span data-ttu-id="a942b-587">`or(value1,value2)`TRUE ya da value1 veya value2 doğrudur.</span><span class="sxs-lookup"><span data-stu-id="a942b-587">`or(value1,value2)` TRUE if either value1 or value2 is true.</span></span> |
| <span data-ttu-id="a942b-588">POW</span><span class="sxs-lookup"><span data-stu-id="a942b-588">pow</span></span> |<span data-ttu-id="a942b-589">Belirtilen güç belirtilen tabanda başlatır.</span><span class="sxs-lookup"><span data-stu-id="a942b-589">Raises the specified base to the specified power.</span></span> <span data-ttu-id="a942b-590">`pow(x,y)`başlatır y gücünü x.</span><span class="sxs-lookup"><span data-stu-id="a942b-590">`pow(x,y)` raises x to the power of y.</span></span> |`pow(x,y)`<br>`pow(x,log(y))`<br><span data-ttu-id="a942b-591">`pow(x,0.5)`Aynı sqrt.</span><span class="sxs-lookup"><span data-stu-id="a942b-591">`pow(x,0.5)` The same as sqrt.</span></span> |
| <span data-ttu-id="a942b-592">Ürün</span><span class="sxs-lookup"><span data-stu-id="a942b-592">product</span></span> |<span data-ttu-id="a942b-593">Birden çok değerler veya virgülle ayrılmış bir listede belirtilen işlevler çarpımını döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-593">Returns the product of multiple values or functions, which are specified in a comma-separated list.</span></span> <span data-ttu-id="a942b-594">`mul(...)`Ayrıca bir diğer ad olarak bu işlev için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-594">`mul(...)` may also be used as an alias for this function.</span></span> |`product(x,y,...)`<br>`product(x,2)`<br>`product(x,y)`<br>`mul(x,y)` |
| <span data-ttu-id="a942b-595">Alıcı</span><span class="sxs-lookup"><span data-stu-id="a942b-595">recip</span></span> |<span data-ttu-id="a942b-596">İle karşılıklı bir işlev gerçekleştirir `recip(x,m,a,b)` uygulama `a/(m*x+b)`, burada m, a, b olan sabitleri ve x, herhangi bir rastgele karmaşık işlev.</span><span class="sxs-lookup"><span data-stu-id="a942b-596">Performs a reciprocal function with `recip(x,m,a,b)` implementing `a/(m*x+b)`, where m, a,and b are constants, and x is any arbitrarily complex function.</span></span> <span data-ttu-id="a942b-597">Zaman bir ve b eşittir ve x > = 0, bu işlev bir maksimum değer olarak artar x bırakır 1 sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a942b-597">When a and b are equal, and x>=0, this function has a maximum value of 1 that drops as x increases.</span></span> <span data-ttu-id="a942b-598">Değerini artırmayı bir ve b birlikte tüm işlev eğri daha düz bir parçası için hareketini sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="a942b-598">Increasing the value of a and b together results in a movement of the entire function to a flatter part of the curve.</span></span> <span data-ttu-id="a942b-599">Bu özellikler bu x olduğunda daha yeni belgeleri artırmanın için ideal bir işlev yapabilirsiniz `rord(datefield)`.</span><span class="sxs-lookup"><span data-stu-id="a942b-599">These properties can make this an ideal function for boosting more recent documents when x is `rord(datefield)`.</span></span> |`recip(myfield,m,a,b)`<br>`recip(rord(creationDate),1,1000,1000)` |
| <span data-ttu-id="a942b-600">RAD</span><span class="sxs-lookup"><span data-stu-id="a942b-600">rad</span></span> |<span data-ttu-id="a942b-601">Derece radyan için dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-601">Converts degrees to radians.</span></span> |`rad(x)` |
| <span data-ttu-id="a942b-602">Yazdır</span><span class="sxs-lookup"><span data-stu-id="a942b-602">rint</span></span> |<span data-ttu-id="a942b-603">En yakın tamsayıya yuvarlar.</span><span class="sxs-lookup"><span data-stu-id="a942b-603">Rounds to the nearest integer.</span></span> |`rint(x)`  <br> <span data-ttu-id="a942b-604">`rint(5.6)`6'yı döndürür</span><span class="sxs-lookup"><span data-stu-id="a942b-604">`rint(5.6)` Returns 6</span></span> |
| <span data-ttu-id="a942b-605">sin</span><span class="sxs-lookup"><span data-stu-id="a942b-605">sin</span></span> |<span data-ttu-id="a942b-606">Bir açının sinüsünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-606">Returns sine of an angle.</span></span> |`sin(x)` |
| <span data-ttu-id="a942b-607">SİNH</span><span class="sxs-lookup"><span data-stu-id="a942b-607">sinh</span></span> |<span data-ttu-id="a942b-608">Bir açının hiperbolik sinüsünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-608">Returns hyperbolic sine of an angle.</span></span> |`sinh(x)` |
| <span data-ttu-id="a942b-609">Ölçek</span><span class="sxs-lookup"><span data-stu-id="a942b-609">scale</span></span> |<span data-ttu-id="a942b-610">İşlevin x değerleri belirtilen minTarget ve maxTarget (bunlar dahil) arasında olacak şekilde ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="a942b-610">Scales values of the function x, such that they fall between the specified minTarget and maxTarget inclusive.</span></span> <span data-ttu-id="a942b-611">Geçerli tüm doğru ölçek seçebilirsiniz şekilde min ve Mak edinme işlevi değerleri erişir.</span><span class="sxs-lookup"><span data-stu-id="a942b-611">The current implementation traverses all of the function values to obtain the min and max, so it can pick the correct scale.</span></span> <span data-ttu-id="a942b-612">Belgeleri sildikten sonra geçerli ayırt edemez ya da herhangi bir değer olan belgeler.</span><span class="sxs-lookup"><span data-stu-id="a942b-612">The current implementation cannot distinguish when documents have been deleted, or documents that have no value.</span></span> <span data-ttu-id="a942b-613">Bu durumlarda 0.0 değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="a942b-613">It uses 0.0 values for these cases.</span></span> <span data-ttu-id="a942b-614">Bu değerler normalde 0. 0 ' tüm büyük ise, bir hala 0,0 ile eşlenecek en küçük değer olarak düşebilir olduğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a942b-614">This means that if values are normally all greater than 0.0, one can still end up with 0.0 as the min value to map from.</span></span> <span data-ttu-id="a942b-615">Bu durumda, uygun bir `map()` işlevi kullanılabilirdi geçici bir çözüm olarak 0,0 gerçek aralıktaki bir değere değiştirmek için aşağıda gösterildiği gibi:`scale(map(x,0,0,5),1,2)`</span><span class="sxs-lookup"><span data-stu-id="a942b-615">In these cases, an appropriate `map()` function could be used as a workaround to change 0.0 to a value in the real range, as shown here: `scale(map(x,0,0,5),1,2)`</span></span> |`scale(x,minTarget,maxTarget)`<br><span data-ttu-id="a942b-616">`scale(x,1,2)`X değerleri tüm 1 ve 2 (bunlar dahil) arasında değerler şekilde ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="a942b-616">`scale(x,1,2)` Scales the values of x, such that all values are between 1 and 2 inclusive.</span></span> |
| <span data-ttu-id="a942b-617">Sqrt</span><span class="sxs-lookup"><span data-stu-id="a942b-617">sqrt</span></span> |<span data-ttu-id="a942b-618">Belirtilen değer ya da işlevin kare kökünü döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-618">Returns the square root of the specified value or function.</span></span> |`sqrt(x)`<br>`sqrt(100)`<br>`sqrt(sum(x,100))` |
| <span data-ttu-id="a942b-619">strdist</span><span class="sxs-lookup"><span data-stu-id="a942b-619">strdist</span></span> |<span data-ttu-id="a942b-620">İki dizeyi arasındaki uzaklığı hesaplar.</span><span class="sxs-lookup"><span data-stu-id="a942b-620">Calculates the distance between two strings.</span></span> <span data-ttu-id="a942b-621">Lucene yazım denetleyicisi StringDistance arabirimini kullanır ve tüm bu pakette kullanılabilir uygulamaları destekler.</span><span class="sxs-lookup"><span data-stu-id="a942b-621">Uses the Lucene spell checker StringDistance interface, and supports all of the implementations available in that package.</span></span> <span data-ttu-id="a942b-622">Kendi Solr'ın kaynak aracılığıyla yükleme özellikleri takın uygulamaların da sağlar.</span><span class="sxs-lookup"><span data-stu-id="a942b-622">Also allows applications to plug in their own, via Solr's resource loading capabilities.</span></span> <span data-ttu-id="a942b-623">strdist geçen `(string1, string2, distance measure)`.</span><span class="sxs-lookup"><span data-stu-id="a942b-623">strdist takes `(string1, string2, distance measure)`.</span></span> <span data-ttu-id="a942b-624">Uzaklık ölçü için olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a942b-624">Possible values for distance measure are:</span></span><ul><li><span data-ttu-id="a942b-625">jw: Jaro Winkler</span><span class="sxs-lookup"><span data-stu-id="a942b-625">jw: Jaro-Winkler</span></span></li><li><span data-ttu-id="a942b-626">Düzenle: Levenstein veya düzenleme uzaklığı</span><span class="sxs-lookup"><span data-stu-id="a942b-626">edit: Levenstein or Edit distance</span></span></li><li><span data-ttu-id="a942b-627">ngram: NGramDistance belirtilmişse, isteğe bağlı olarak iletebilir ngram boyutu çok.</span><span class="sxs-lookup"><span data-stu-id="a942b-627">ngram: The NGramDistance, if specified, can optionally pass in the ngram size too.</span></span> <span data-ttu-id="a942b-628">Varsayılan 2'dir.</span><span class="sxs-lookup"><span data-stu-id="a942b-628">Default is 2.</span></span></li><li><span data-ttu-id="a942b-629">FQN: Sınıf adı StringDistance arabirimi bir uygulama için tam.</span><span class="sxs-lookup"><span data-stu-id="a942b-629">FQN: Fully Qualified class Name for an implementation of the StringDistance interface.</span></span> <span data-ttu-id="a942b-630">Hayır arg oluşturucuya sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a942b-630">Must have a no-arg constructor.</span></span></li></ul> |`strdist("SOLR",id,edit)` |
| <span data-ttu-id="a942b-631">Sub</span><span class="sxs-lookup"><span data-stu-id="a942b-631">sub</span></span> |<span data-ttu-id="a942b-632">X-y döndürür `sub(x,y)`.</span><span class="sxs-lookup"><span data-stu-id="a942b-632">Returns x-y from `sub(x,y)`.</span></span> |`sub(myfield,myfield2)`<br>`sub(100,sqrt(myfield))` |
| <span data-ttu-id="a942b-633">TOPLA</span><span class="sxs-lookup"><span data-stu-id="a942b-633">sum</span></span> |<span data-ttu-id="a942b-634">Birden çok değerler veya virgülle ayrılmış bir listede belirtilen işlevler toplamını döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-634">Returns the sum of multiple values or functions, which are specified in a comma-separated list.</span></span> <span data-ttu-id="a942b-635">`add(...)`Bu işlev için bir diğer ad olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-635">`add(...)` may be used as an alias for this function.</span></span> |`sum(x,y,...)`<br>`sum(x,1)`<br>`sum(x,y)`<br>`sum(sqrt(x),log(y),z,0.5)`<br>`add(x,y)` |
| <span data-ttu-id="a942b-636">termfreq</span><span class="sxs-lookup"><span data-stu-id="a942b-636">termfreq</span></span> |<span data-ttu-id="a942b-637">Bu belge için alanında terimi görünür sayısı döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-637">Returns the number of times the term appears in the field for that document.</span></span> |<span data-ttu-id="a942b-638">termfreq(Text,'memory')</span><span class="sxs-lookup"><span data-stu-id="a942b-638">termfreq(text,'memory')</span></span> |
| <span data-ttu-id="a942b-639">tan</span><span class="sxs-lookup"><span data-stu-id="a942b-639">tan</span></span> |<span data-ttu-id="a942b-640">Bir açının tanjantını döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-640">Returns tangent of an angle.</span></span> |`tan(x)` |
| <span data-ttu-id="a942b-641">TANH</span><span class="sxs-lookup"><span data-stu-id="a942b-641">tanh</span></span> |<span data-ttu-id="a942b-642">Bir açının hiperbolik tanjantını döndürür.</span><span class="sxs-lookup"><span data-stu-id="a942b-642">Returns hyperbolic tangent of an angle.</span></span> |`tanh(x)` |

## <a name="search-field-and-facet-reference"></a><span data-ttu-id="a942b-643">Arama alanı ve modeli başvurusu</span><span class="sxs-lookup"><span data-stu-id="a942b-643">Search field and facet reference</span></span>
<span data-ttu-id="a942b-644">Verileri bulmak üzere günlük arama kullandığınızda, sonuçlar çeşitli alan ve modelleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a942b-644">When you use Log Search to find data, results display various field and facets.</span></span> <span data-ttu-id="a942b-645">Bazı bilgiler çok açıklayıcı görünmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-645">Some of the information might not appear very descriptive.</span></span> <span data-ttu-id="a942b-646">Sonuçları anlamanıza yardımcı olması için aşağıdaki bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="a942b-646">Use the following information to help you understand the results.</span></span>

| <span data-ttu-id="a942b-647">Alan</span><span class="sxs-lookup"><span data-stu-id="a942b-647">Field</span></span> | <span data-ttu-id="a942b-648">Arama türü</span><span class="sxs-lookup"><span data-stu-id="a942b-648">Search type</span></span> | <span data-ttu-id="a942b-649">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a942b-649">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a942b-650">Tenantıd</span><span class="sxs-lookup"><span data-stu-id="a942b-650">TenantId</span></span> |<span data-ttu-id="a942b-651">Tümü</span><span class="sxs-lookup"><span data-stu-id="a942b-651">All</span></span> |<span data-ttu-id="a942b-652">Bölüm verileri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a942b-652">Used to partition data.</span></span> |
| <span data-ttu-id="a942b-653">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="a942b-653">TimeGenerated</span></span> |<span data-ttu-id="a942b-654">Tümü</span><span class="sxs-lookup"><span data-stu-id="a942b-654">All</span></span> |<span data-ttu-id="a942b-655">Zaman çizelgesi, timeselectors (arama ve diğer ekranlar) sürücü için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a942b-655">Used to drive the timeline, timeselectors (in search and in other screens).</span></span> <span data-ttu-id="a942b-656">Veri parçası (genellikle aracı üzerinde) oluşturulduğunda temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a942b-656">It represents when the piece of data was generated (typically on the agent).</span></span> <span data-ttu-id="a942b-657">Süre ISO biçiminde ifade edilir ve her zaman UTC değil.</span><span class="sxs-lookup"><span data-stu-id="a942b-657">The time is expressed in ISO format, and is always UTC.</span></span> <span data-ttu-id="a942b-658">Varolan Araçları'nı (diğer bir deyişle, olay günlüğü'ndeki) temel alan türleri söz konusu olduğunda, bu genellikle günlük girişi/satır/kaydı günlüğe gerçek zamanlı olur.</span><span class="sxs-lookup"><span data-stu-id="a942b-658">In the case of types that are based on existing instrumentation (that is, events in a log), this is typically the real time that the log entry/line/record was logged.</span></span> <span data-ttu-id="a942b-659">Bazı yönetim paketleri aracılığıyla veya bulutta (örneğin, önerileri veya Uyarıları) üretilen diğer türlerini zaman farklı bir şey temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a942b-659">For some of the other types that are produced either via management packs or in the cloud (for example, recommendations or alerts), the time represents something different.</span></span> <span data-ttu-id="a942b-660">Bu zaman bu yeni veri parçası çeşit yapılandırmanın bir anlık görüntüsünü ile toplanan veya bir öneri/Uyarısı, göre üretilmiştir zamandır.</span><span class="sxs-lookup"><span data-stu-id="a942b-660">This is the time when this new piece of data with a snapshot of a configuration of some sort was collected, or a recommendation/alert was produced based on it.</span></span> |
| <span data-ttu-id="a942b-661">Olay Kimliği</span><span class="sxs-lookup"><span data-stu-id="a942b-661">EventID</span></span> |<span data-ttu-id="a942b-662">Olay</span><span class="sxs-lookup"><span data-stu-id="a942b-662">Event</span></span> |<span data-ttu-id="a942b-663">Windows olay günlüğünde olay kimliği.</span><span class="sxs-lookup"><span data-stu-id="a942b-663">EventID in the Windows event log.</span></span> |
| <span data-ttu-id="a942b-664">Olay günlüğü</span><span class="sxs-lookup"><span data-stu-id="a942b-664">EventLog</span></span> |<span data-ttu-id="a942b-665">Olay</span><span class="sxs-lookup"><span data-stu-id="a942b-665">Event</span></span> |<span data-ttu-id="a942b-666">Olay günlüğü olayı Windows tarafından burada günlüğe kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="a942b-666">Event log where the event was logged by Windows.</span></span> |
| <span data-ttu-id="a942b-667">EventLevelName</span><span class="sxs-lookup"><span data-stu-id="a942b-667">EventLevelName</span></span> |<span data-ttu-id="a942b-668">Olay</span><span class="sxs-lookup"><span data-stu-id="a942b-668">Event</span></span> |<span data-ttu-id="a942b-669">Kritik/Uyarı/bilgi/başarılı</span><span class="sxs-lookup"><span data-stu-id="a942b-669">Critical/warning/information/success</span></span> |
| <span data-ttu-id="a942b-670">eventLevel</span><span class="sxs-lookup"><span data-stu-id="a942b-670">EventLevel</span></span> |<span data-ttu-id="a942b-671">Olay</span><span class="sxs-lookup"><span data-stu-id="a942b-671">Event</span></span> |<span data-ttu-id="a942b-672">Kritik/Uyarı/bilgi/başarı ilişkin sayısal değer (EventLevelName daha kolay/daha okunabilir sorgular için bunun yerine kullanın).</span><span class="sxs-lookup"><span data-stu-id="a942b-672">Numerical value for critical/warning/information/success (use EventLevelName instead for easier/more readable queries).</span></span> |
| <span data-ttu-id="a942b-673">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="a942b-673">SourceSystem</span></span> |<span data-ttu-id="a942b-674">Tümü</span><span class="sxs-lookup"><span data-stu-id="a942b-674">All</span></span> |<span data-ttu-id="a942b-675">Verilerin nereden geldiği (cinsinden modu hizmetine ekleme).</span><span class="sxs-lookup"><span data-stu-id="a942b-675">Where the data comes from (in terms of attach mode to the service).</span></span> <span data-ttu-id="a942b-676">Örnek Microsoft System Center Operations Manager ve Azure Storage verilebilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-676">Examples include Microsoft System Center Operations Manager and Azure Storage.</span></span> |
| <span data-ttu-id="a942b-677">ObjectName</span><span class="sxs-lookup"><span data-stu-id="a942b-677">ObjectName</span></span> |<span data-ttu-id="a942b-678">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="a942b-678">PerfHourly</span></span> |<span data-ttu-id="a942b-679">Windows performans nesnesi adı.</span><span class="sxs-lookup"><span data-stu-id="a942b-679">Windows performance object name.</span></span> |
| <span data-ttu-id="a942b-680">InstanceName</span><span class="sxs-lookup"><span data-stu-id="a942b-680">InstanceName</span></span> |<span data-ttu-id="a942b-681">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="a942b-681">PerfHourly</span></span> |<span data-ttu-id="a942b-682">Windows performans sayacı örneği adı.</span><span class="sxs-lookup"><span data-stu-id="a942b-682">Windows performance counter instance name.</span></span> |
| <span data-ttu-id="a942b-683">CounteName</span><span class="sxs-lookup"><span data-stu-id="a942b-683">CounteName</span></span> |<span data-ttu-id="a942b-684">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="a942b-684">PerfHourly</span></span> |<span data-ttu-id="a942b-685">Windows performans sayacı adı.</span><span class="sxs-lookup"><span data-stu-id="a942b-685">Windows performance counter name.</span></span> |
| <span data-ttu-id="a942b-686">ObjectDisplayName</span><span class="sxs-lookup"><span data-stu-id="a942b-686">ObjectDisplayName</span></span> |<span data-ttu-id="a942b-687">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="a942b-687">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span></span> |<span data-ttu-id="a942b-688">Operations Manager bir performans toplama kuralı tarafından hedeflenen nesnenin adını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a942b-688">Display name of the object targeted by a performance collection rule in Operations Manager.</span></span> <span data-ttu-id="a942b-689">Operasyonel Öngörüler veya uyarının oluşturulduğu karşı bulunan nesnenin görünen adını da olabilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-689">Could also be the display name of the object discovered by Operational Insights, or against which the alert was generated.</span></span> |
| <span data-ttu-id="a942b-690">RootObjectName</span><span class="sxs-lookup"><span data-stu-id="a942b-690">RootObjectName</span></span> |<span data-ttu-id="a942b-691">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="a942b-691">PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty</span></span> |<span data-ttu-id="a942b-692">Üst (çift bir barındırma ilişkisi) Operations Manager bir performans toplama kuralı tarafından hedeflenen nesnenin üst görünen adı.</span><span class="sxs-lookup"><span data-stu-id="a942b-692">Display name of the parent of the parent (in a double hosting relationship) of the object targeted by a performance collection rule in Operations Manager.</span></span> <span data-ttu-id="a942b-693">Operasyonel Öngörüler veya uyarının oluşturulduğu karşı bulunan nesnenin görünen adını da olabilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-693">Could also be the display name of the object discovered by Operational Insights, or against which the alert was generated.</span></span> |
| <span data-ttu-id="a942b-694">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="a942b-694">Computer</span></span> |<span data-ttu-id="a942b-695">Çoğu türleri</span><span class="sxs-lookup"><span data-stu-id="a942b-695">Most types</span></span> |<span data-ttu-id="a942b-696">Veri ait olduğu bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="a942b-696">Computer name that the data belongs to.</span></span> |
| <span data-ttu-id="a942b-697">DeviceName</span><span class="sxs-lookup"><span data-stu-id="a942b-697">DeviceName</span></span> |<span data-ttu-id="a942b-698">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="a942b-698">ProtectionStatus</span></span> |<span data-ttu-id="a942b-699">Bilgisayar adı verileri ("Bilgisayar" ile aynı) ait.</span><span class="sxs-lookup"><span data-stu-id="a942b-699">Computer name the data belongs to (same as "Computer").</span></span> |
| <span data-ttu-id="a942b-700">DetectionId</span><span class="sxs-lookup"><span data-stu-id="a942b-700">DetectionId</span></span> |<span data-ttu-id="a942b-701">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="a942b-701">ProtectionStatus</span></span> | |
| <span data-ttu-id="a942b-702">ThreatStatusRank</span><span class="sxs-lookup"><span data-stu-id="a942b-702">ThreatStatusRank</span></span> |<span data-ttu-id="a942b-703">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="a942b-703">ProtectionStatus</span></span> |<span data-ttu-id="a942b-704">İş parçacığı durumu derece tehdit durum sayısal bir gösterimi ' dir.</span><span class="sxs-lookup"><span data-stu-id="a942b-704">Threat status rank is a numerical representation of the threat status.</span></span> <span data-ttu-id="a942b-705">HTTP yanıt kodları benzeyen, derecelendirme sayılar arasında boşluk sahiptir (herhangi bir tehdit neden olduğu 150 ve değil 100 veya 0 değil), yeni durum eklemek için yeriniz çıkılıyor.</span><span class="sxs-lookup"><span data-stu-id="a942b-705">Similar to HTTP response codes, the ranking has gaps between the numbers (which is why no threats is 150 and not 100 or 0), leaving room to add new states.</span></span> <span data-ttu-id="a942b-706">İş parçacığı durumu ve koruma durumu toplaması için amacınız bilgisayarın seçili dönemde düzeltilme en kötü durumu göstermektir.</span><span class="sxs-lookup"><span data-stu-id="a942b-706">For a rollup of threat status and protection status, the intention is to show the worst state that the computer has been in during the selected time period.</span></span> <span data-ttu-id="a942b-707">Kayıt için en yüksek sayıyı görebilecekleri sayıları farklı durumları rank.</span><span class="sxs-lookup"><span data-stu-id="a942b-707">The numbers rank the different states, so you can look for the record with the highest number.</span></span> |
| <span data-ttu-id="a942b-708">ThreatStatus</span><span class="sxs-lookup"><span data-stu-id="a942b-708">ThreatStatus</span></span> |<span data-ttu-id="a942b-709">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="a942b-709">ProtectionStatus</span></span> |<span data-ttu-id="a942b-710">ThreatStatus, açıklaması, 1:1 ThreatStatusRank ile eşler.</span><span class="sxs-lookup"><span data-stu-id="a942b-710">Description of ThreatStatus, maps 1:1 with ThreatStatusRank.</span></span> |
| <span data-ttu-id="a942b-711">TypeofProtection</span><span class="sxs-lookup"><span data-stu-id="a942b-711">TypeofProtection</span></span> |<span data-ttu-id="a942b-712">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="a942b-712">ProtectionStatus</span></span> |<span data-ttu-id="a942b-713">Bilgisayarda Algılanan kötü amaçlı yazılımdan koruma ürün: none, Microsoft kötü amaçlı yazılım kaldırma aracını, Forefront ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="a942b-713">Antimalware product that is detected in the computer: none, Microsoft Malware Removal tool, Forefront, and so on.</span></span> |
| <span data-ttu-id="a942b-714">ComputerName</span><span class="sxs-lookup"><span data-stu-id="a942b-714">ScanDate</span></span> |<span data-ttu-id="a942b-715">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="a942b-715">ProtectionStatus</span></span> | |
| <span data-ttu-id="a942b-716">SourceHealthServiceId</span><span class="sxs-lookup"><span data-stu-id="a942b-716">SourceHealthServiceId</span></span> |<span data-ttu-id="a942b-717">ProtectionStatus, RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="a942b-717">ProtectionStatus, RequiredUpdate</span></span> |<span data-ttu-id="a942b-718">Bu bilgisayarın aracı için sistem sağlığı hizmeti kimliği.</span><span class="sxs-lookup"><span data-stu-id="a942b-718">HealthService ID for this computer's agent.</span></span> |
| <span data-ttu-id="a942b-719">HealthServiceId</span><span class="sxs-lookup"><span data-stu-id="a942b-719">HealthServiceId</span></span> |<span data-ttu-id="a942b-720">Çoğu türleri</span><span class="sxs-lookup"><span data-stu-id="a942b-720">Most types</span></span> |<span data-ttu-id="a942b-721">Bu bilgisayarın aracı için sistem sağlığı hizmeti kimliği.</span><span class="sxs-lookup"><span data-stu-id="a942b-721">HealthService ID for this computer's agent.</span></span> |
| <span data-ttu-id="a942b-722">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="a942b-722">ManagementGroupName</span></span> |<span data-ttu-id="a942b-723">Çoğu türleri</span><span class="sxs-lookup"><span data-stu-id="a942b-723">Most types</span></span> |<span data-ttu-id="a942b-724">Operations Manager bağlı aracılar için yönetim grubu adı.</span><span class="sxs-lookup"><span data-stu-id="a942b-724">Management Group Name for Operations Manager-attached agents.</span></span> <span data-ttu-id="a942b-725">Aksi takdirde, null/boş olur.</span><span class="sxs-lookup"><span data-stu-id="a942b-725">Otherwise, it is null/blank.</span></span> |
| <span data-ttu-id="a942b-726">ObjectType</span><span class="sxs-lookup"><span data-stu-id="a942b-726">ObjectType</span></span> |<span data-ttu-id="a942b-727">ConfigurationObject</span><span class="sxs-lookup"><span data-stu-id="a942b-727">ConfigurationObject</span></span> |<span data-ttu-id="a942b-728">Günlük analizi yapılandırması değerlendirme tarafından bulunan bu nesne için (Operations Manager Yönetim Paketi türü/sınıfı olduğu gibi) yazın.</span><span class="sxs-lookup"><span data-stu-id="a942b-728">Type (as in Operations Manager management pack's type/class) for this object, discovered by Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="a942b-729">UpdateTitle</span><span class="sxs-lookup"><span data-stu-id="a942b-729">UpdateTitle</span></span> |<span data-ttu-id="a942b-730">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="a942b-730">RequiredUpdate</span></span> |<span data-ttu-id="a942b-731">Adı bulundu güncelleştirmesi yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="a942b-731">Name of the update that was found not installed.</span></span> |
| <span data-ttu-id="a942b-732">PublishDate</span><span class="sxs-lookup"><span data-stu-id="a942b-732">PublishDate</span></span> |<span data-ttu-id="a942b-733">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="a942b-733">RequiredUpdate</span></span> |<span data-ttu-id="a942b-734">Ne zaman güncelleştirme Microsoft Update sitesinde yayımlandı.</span><span class="sxs-lookup"><span data-stu-id="a942b-734">When the update was published on Microsoft Update.</span></span> |
| <span data-ttu-id="a942b-735">Sunucu</span><span class="sxs-lookup"><span data-stu-id="a942b-735">Server</span></span> |<span data-ttu-id="a942b-736">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="a942b-736">RequiredUpdate</span></span> |<span data-ttu-id="a942b-737">Bilgisayar adı verileri ("Bilgisayar" ile aynı) ait.</span><span class="sxs-lookup"><span data-stu-id="a942b-737">Computer name the data belongs to (same as "Computer").</span></span> |
| <span data-ttu-id="a942b-738">Ürün</span><span class="sxs-lookup"><span data-stu-id="a942b-738">Product</span></span> |<span data-ttu-id="a942b-739">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="a942b-739">RequiredUpdate</span></span> |<span data-ttu-id="a942b-740">Güncelleştirmenin geçerli ürün.</span><span class="sxs-lookup"><span data-stu-id="a942b-740">Product that the update applies to.</span></span> |
| <span data-ttu-id="a942b-741">UpdateClassification</span><span class="sxs-lookup"><span data-stu-id="a942b-741">UpdateClassification</span></span> |<span data-ttu-id="a942b-742">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="a942b-742">RequiredUpdate</span></span> |<span data-ttu-id="a942b-743">Güncelleştirme (örneğin, güncelleştirme paketi veya hizmet paketi) türü.</span><span class="sxs-lookup"><span data-stu-id="a942b-743">Type of update (for example, update rollup or service pack).</span></span> |
| <span data-ttu-id="a942b-744">KBID</span><span class="sxs-lookup"><span data-stu-id="a942b-744">KBID</span></span> |<span data-ttu-id="a942b-745">RequiredUpdate</span><span class="sxs-lookup"><span data-stu-id="a942b-745">RequiredUpdate</span></span> |<span data-ttu-id="a942b-746">Bu en iyi yöntem veya güncelleştirmeyi açıklayan KB makalesi kimliği.</span><span class="sxs-lookup"><span data-stu-id="a942b-746">KB article ID that describes this best practice or update.</span></span> |
| <span data-ttu-id="a942b-747">WorkflowName</span><span class="sxs-lookup"><span data-stu-id="a942b-747">WorkflowName</span></span> |<span data-ttu-id="a942b-748">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="a942b-748">ConfigurationAlert</span></span> |<span data-ttu-id="a942b-749">Kural veya İzleyici uyarıyı üretilen adı.</span><span class="sxs-lookup"><span data-stu-id="a942b-749">Name of the rule or monitor that produced the alert.</span></span> |
| <span data-ttu-id="a942b-750">Önem Derecesi</span><span class="sxs-lookup"><span data-stu-id="a942b-750">Severity</span></span> |<span data-ttu-id="a942b-751">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="a942b-751">ConfigurationAlert</span></span> |<span data-ttu-id="a942b-752">Uyarının önem derecesi.</span><span class="sxs-lookup"><span data-stu-id="a942b-752">Severity of the alert.</span></span> |
| <span data-ttu-id="a942b-753">Öncelik</span><span class="sxs-lookup"><span data-stu-id="a942b-753">Priority</span></span> |<span data-ttu-id="a942b-754">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="a942b-754">ConfigurationAlert</span></span> |<span data-ttu-id="a942b-755">Uyarı önceliği.</span><span class="sxs-lookup"><span data-stu-id="a942b-755">Priority of the alert.</span></span> |
| <span data-ttu-id="a942b-756">IsMonitorAlert</span><span class="sxs-lookup"><span data-stu-id="a942b-756">IsMonitorAlert</span></span> |<span data-ttu-id="a942b-757">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="a942b-757">ConfigurationAlert</span></span> |<span data-ttu-id="a942b-758">Bu uyarı bir izleyici (true) veya bir kural (false) tarafından oluşturulur?</span><span class="sxs-lookup"><span data-stu-id="a942b-758">Is this alert generated by a monitor (true) or a rule (false)?</span></span> |
| <span data-ttu-id="a942b-759">AlertParameters</span><span class="sxs-lookup"><span data-stu-id="a942b-759">AlertParameters</span></span> |<span data-ttu-id="a942b-760">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="a942b-760">ConfigurationAlert</span></span> |<span data-ttu-id="a942b-761">XML günlük analizi uyarı parametrelere sahip.</span><span class="sxs-lookup"><span data-stu-id="a942b-761">XML with the parameters of the Log Analytics alert.</span></span> |
| <span data-ttu-id="a942b-762">Bağlam</span><span class="sxs-lookup"><span data-stu-id="a942b-762">Context</span></span> |<span data-ttu-id="a942b-763">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="a942b-763">ConfigurationAlert</span></span> |<span data-ttu-id="a942b-764">XML ile günlük analizi uyarı bağlamı.</span><span class="sxs-lookup"><span data-stu-id="a942b-764">XML with the context of the Log Analytics alert.</span></span> |
| <span data-ttu-id="a942b-765">İş yükü</span><span class="sxs-lookup"><span data-stu-id="a942b-765">Workload</span></span> |<span data-ttu-id="a942b-766">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="a942b-766">ConfigurationAlert</span></span> |<span data-ttu-id="a942b-767">Teknoloji veya uyarı başvurduğu iş yükü.</span><span class="sxs-lookup"><span data-stu-id="a942b-767">Technology or workload that the alert refers to.</span></span> |
| <span data-ttu-id="a942b-768">AdvisorWorkload</span><span class="sxs-lookup"><span data-stu-id="a942b-768">AdvisorWorkload</span></span> |<span data-ttu-id="a942b-769">Öneri</span><span class="sxs-lookup"><span data-stu-id="a942b-769">Recommendation</span></span> |<span data-ttu-id="a942b-770">Teknoloji veya öneri başvurduğu iş yükü.</span><span class="sxs-lookup"><span data-stu-id="a942b-770">Technology or workload that the recommendation refers to.</span></span> |
| <span data-ttu-id="a942b-771">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a942b-771">Description</span></span> |<span data-ttu-id="a942b-772">ConfigurationAlert</span><span class="sxs-lookup"><span data-stu-id="a942b-772">ConfigurationAlert</span></span> |<span data-ttu-id="a942b-773">Uyarı açıklaması (kısa).</span><span class="sxs-lookup"><span data-stu-id="a942b-773">Alert description (short).</span></span> |
| <span data-ttu-id="a942b-774">DaysSinceLastUpdate</span><span class="sxs-lookup"><span data-stu-id="a942b-774">DaysSinceLastUpdate</span></span> |<span data-ttu-id="a942b-775">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="a942b-775">UpdateAgent</span></span> |<span data-ttu-id="a942b-776">Kaç gün (göre bu kaydın TimeGenerated) önce bu aracının herhangi bir güncelleştirme Windows Server Update Service (WSUS) veya Microsoft Update yüklediniz mi?</span><span class="sxs-lookup"><span data-stu-id="a942b-776">How many days ago (relative to TimeGenerated of this record) did this agent install any update from Windows Server Update Service (WSUS) or Microsoft Update?</span></span> |
| <span data-ttu-id="a942b-777">DaysSinceLastUpdateBucket</span><span class="sxs-lookup"><span data-stu-id="a942b-777">DaysSinceLastUpdateBucket</span></span> |<span data-ttu-id="a942b-778">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="a942b-778">UpdateAgent</span></span> |<span data-ttu-id="a942b-779">DaysSinceLastUpdate, kategori, ne kadar zaman önce bir bilgisayar son herhangi bir güncelleştirme WSUS/Microsoft Update sitesinden yüklenen zaman demet içinde temel.</span><span class="sxs-lookup"><span data-stu-id="a942b-779">Based on DaysSinceLastUpdate, a categorization in time buckets of how long ago a computer last installed any update from WSUS/Microsoft Update.</span></span> |
| <span data-ttu-id="a942b-780">AutomaticUpdateEnabled</span><span class="sxs-lookup"><span data-stu-id="a942b-780">AutomaticUpdateEnabled</span></span> |<span data-ttu-id="a942b-781">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="a942b-781">UpdateAgent</span></span> |<span data-ttu-id="a942b-782">Otomatik Güncelleştirme denetimi etkinleştirildiğini veya bu Aracısı'nı devre dışı?</span><span class="sxs-lookup"><span data-stu-id="a942b-782">Is automatic update checking enabled or disabled on this agent?</span></span> |
| <span data-ttu-id="a942b-783">AutomaticUpdateValue</span><span class="sxs-lookup"><span data-stu-id="a942b-783">AutomaticUpdateValue</span></span> |<span data-ttu-id="a942b-784">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="a942b-784">UpdateAgent</span></span> |<span data-ttu-id="a942b-785">Otomatik güncelleştirme otomatik olarak indirmeniz ve yüklemeniz, yalnızca yükleyin veya yalnızca denetlemek için kümesi denetliyor?</span><span class="sxs-lookup"><span data-stu-id="a942b-785">Is automatic update checking set to automatically download and install, only download, or only check?</span></span> |
| <span data-ttu-id="a942b-786">WindowsUpdateAgentVersion</span><span class="sxs-lookup"><span data-stu-id="a942b-786">WindowsUpdateAgentVersion</span></span> |<span data-ttu-id="a942b-787">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="a942b-787">UpdateAgent</span></span> |<span data-ttu-id="a942b-788">Microsoft Update Aracı sürüm numarası.</span><span class="sxs-lookup"><span data-stu-id="a942b-788">Version number of the Microsoft Update agent.</span></span> |
| <span data-ttu-id="a942b-789">WSUSServer</span><span class="sxs-lookup"><span data-stu-id="a942b-789">WSUSServer</span></span> |<span data-ttu-id="a942b-790">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="a942b-790">UpdateAgent</span></span> |<span data-ttu-id="a942b-791">Hangi WSUS sunucusu, bu güncelleştirme Aracısı hedeflediği?</span><span class="sxs-lookup"><span data-stu-id="a942b-791">Which WSUS server is this update agent targeting?</span></span> |
| <span data-ttu-id="a942b-792">OSVersion</span><span class="sxs-lookup"><span data-stu-id="a942b-792">OSVersion</span></span> |<span data-ttu-id="a942b-793">UpdateAgent</span><span class="sxs-lookup"><span data-stu-id="a942b-793">UpdateAgent</span></span> |<span data-ttu-id="a942b-794">Bu güncelleştirme Aracısı çalışan işletim sistemi sürümü.</span><span class="sxs-lookup"><span data-stu-id="a942b-794">Version of the operating system this update agent is running on.</span></span> |
| <span data-ttu-id="a942b-795">Ad</span><span class="sxs-lookup"><span data-stu-id="a942b-795">Name</span></span> |<span data-ttu-id="a942b-796">Öneri, ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="a942b-796">Recommendation, ConfigurationObjectProperty</span></span> |<span data-ttu-id="a942b-797">Ad/başlığı öneri veya günlük analizi yapılandırması değerlendirme özelliğinden adı.</span><span class="sxs-lookup"><span data-stu-id="a942b-797">Name/title of the recommendation, or name of the property from Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="a942b-798">Değer</span><span class="sxs-lookup"><span data-stu-id="a942b-798">Value</span></span> |<span data-ttu-id="a942b-799">ConfigurationObjectProperty</span><span class="sxs-lookup"><span data-stu-id="a942b-799">ConfigurationObjectProperty</span></span> |<span data-ttu-id="a942b-800">Günlük analizi yapılandırması değerlendirme özelliğinden değeri.</span><span class="sxs-lookup"><span data-stu-id="a942b-800">Value of a property from Log Analytics configuration assessment.</span></span> |
| <span data-ttu-id="a942b-801">KBLink</span><span class="sxs-lookup"><span data-stu-id="a942b-801">KBLink</span></span> |<span data-ttu-id="a942b-802">Öneri</span><span class="sxs-lookup"><span data-stu-id="a942b-802">Recommendation</span></span> |<span data-ttu-id="a942b-803">Bu en iyi yöntem veya güncelleştirmeyi açıklayan KB makalesine URL.</span><span class="sxs-lookup"><span data-stu-id="a942b-803">URL to the KB article that describes this best practice or update.</span></span> |
| <span data-ttu-id="a942b-804">RecommendationStatus</span><span class="sxs-lookup"><span data-stu-id="a942b-804">RecommendationStatus</span></span> |<span data-ttu-id="a942b-805">Öneri</span><span class="sxs-lookup"><span data-stu-id="a942b-805">Recommendation</span></span> |<span data-ttu-id="a942b-806">Arama dizini eklemiş kayıtlarını güncelleştirilmesi birkaç türleri arasında önerilerdir.</span><span class="sxs-lookup"><span data-stu-id="a942b-806">Recommendations are among the few types whose records get updated, not just added to the search index.</span></span> <span data-ttu-id="a942b-807">Bu durum, öneri etkin/açık olup olmadığını veya günlük analizi çözümlendiğini doğrulamaktadır algılarsa değiştirir.</span><span class="sxs-lookup"><span data-stu-id="a942b-807">This status changes whether the recommendation is active/open, or if Log Analytics detects that it has been resolved.</span></span> |
| <span data-ttu-id="a942b-808">RenderedDescription</span><span class="sxs-lookup"><span data-stu-id="a942b-808">RenderedDescription</span></span> |<span data-ttu-id="a942b-809">Olay</span><span class="sxs-lookup"><span data-stu-id="a942b-809">Event</span></span> |<span data-ttu-id="a942b-810">Bir Windows olayı (doldurulmuş parametrelerle yeniden kullanılan metin) açıklaması çizilir.</span><span class="sxs-lookup"><span data-stu-id="a942b-810">Rendered description (reused text with populated parameters) of a Windows event.</span></span> |
| <span data-ttu-id="a942b-811">ParameterXml</span><span class="sxs-lookup"><span data-stu-id="a942b-811">ParameterXml</span></span> |<span data-ttu-id="a942b-812">Olay</span><span class="sxs-lookup"><span data-stu-id="a942b-812">Event</span></span> |<span data-ttu-id="a942b-813">XML Windows (Olay Görüntüleyicisi'nde görüldüğü gibi) olay verileri bölümünde parametrelere sahip.</span><span class="sxs-lookup"><span data-stu-id="a942b-813">XML with the parameters in the data section of a Windows Event (as seen in event viewer).</span></span> |
| <span data-ttu-id="a942b-814">EventData</span><span class="sxs-lookup"><span data-stu-id="a942b-814">EventData</span></span> |<span data-ttu-id="a942b-815">Olay</span><span class="sxs-lookup"><span data-stu-id="a942b-815">Event</span></span> |<span data-ttu-id="a942b-816">Windows (Olay Görüntüleyicisi'nde görüldüğü gibi) olay tüm veri bölümünü içeren XML.</span><span class="sxs-lookup"><span data-stu-id="a942b-816">XML with the whole data section of a Windows Event (as seen in event viewer).</span></span> |
| <span data-ttu-id="a942b-817">Kaynak</span><span class="sxs-lookup"><span data-stu-id="a942b-817">Source</span></span> |<span data-ttu-id="a942b-818">Olay</span><span class="sxs-lookup"><span data-stu-id="a942b-818">Event</span></span> |<span data-ttu-id="a942b-819">Olayı oluşturan olay günlüğü kaynağı.</span><span class="sxs-lookup"><span data-stu-id="a942b-819">Event log source that generated the event.</span></span> |
| <span data-ttu-id="a942b-820">EventCategory</span><span class="sxs-lookup"><span data-stu-id="a942b-820">EventCategory</span></span> |<span data-ttu-id="a942b-821">Olay</span><span class="sxs-lookup"><span data-stu-id="a942b-821">Event</span></span> |<span data-ttu-id="a942b-822">Windows olay günlüğünden doğrudan olay kategorisi.</span><span class="sxs-lookup"><span data-stu-id="a942b-822">Category of the event, directly from the Windows event log.</span></span> |
| <span data-ttu-id="a942b-823">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="a942b-823">UserName</span></span> |<span data-ttu-id="a942b-824">Olay</span><span class="sxs-lookup"><span data-stu-id="a942b-824">Event</span></span> |<span data-ttu-id="a942b-825">Windows olay (genellikle, NT AUTHORITY\LOCALSYSTEM) kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="a942b-825">User name of the Windows event (typically, NT AUTHORITY\LOCALSYSTEM).</span></span> |
| <span data-ttu-id="a942b-826">Görüntülendiğinden</span><span class="sxs-lookup"><span data-stu-id="a942b-826">SampleValue</span></span> |<span data-ttu-id="a942b-827">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="a942b-827">PerfHourly</span></span> |<span data-ttu-id="a942b-828">Saatlik toplama, bir performans sayacının ortalama değeri.</span><span class="sxs-lookup"><span data-stu-id="a942b-828">Average value for the hourly aggregation of a performance counter.</span></span> |
| <span data-ttu-id="a942b-829">Min</span><span class="sxs-lookup"><span data-stu-id="a942b-829">Min</span></span> |<span data-ttu-id="a942b-830">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="a942b-830">PerfHourly</span></span> |<span data-ttu-id="a942b-831">Bir performans sayacı saatlik toplama saatlik aralığı en düşük değer.</span><span class="sxs-lookup"><span data-stu-id="a942b-831">Minimum value in the hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="a942b-832">Maks.</span><span class="sxs-lookup"><span data-stu-id="a942b-832">Max</span></span> |<span data-ttu-id="a942b-833">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="a942b-833">PerfHourly</span></span> |<span data-ttu-id="a942b-834">Bir performans sayacı saatlik toplama saatlik aralığı en büyük değeri.</span><span class="sxs-lookup"><span data-stu-id="a942b-834">Maximum value in the hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="a942b-835">Percentile95</span><span class="sxs-lookup"><span data-stu-id="a942b-835">Percentile95</span></span> |<span data-ttu-id="a942b-836">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="a942b-836">PerfHourly</span></span> |<span data-ttu-id="a942b-837">Bir performans sayacı saatlik toplama saatlik aralığı 95 yüzdelik değer.</span><span class="sxs-lookup"><span data-stu-id="a942b-837">The 95th percentile value for the hourly interval of a performance counter hourly aggregate.</span></span> |
| <span data-ttu-id="a942b-838">SampleCount</span><span class="sxs-lookup"><span data-stu-id="a942b-838">SampleCount</span></span> |<span data-ttu-id="a942b-839">PerfHourly</span><span class="sxs-lookup"><span data-stu-id="a942b-839">PerfHourly</span></span> |<span data-ttu-id="a942b-840">Kaç tane ham performans sayacı örneklerinin saatlik bu birleşik kayıt oluşturmak için kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="a942b-840">How many raw performance counter samples were used to produce this hourly aggregate record.</span></span> |
| <span data-ttu-id="a942b-841">Tehdit</span><span class="sxs-lookup"><span data-stu-id="a942b-841">Threat</span></span> |<span data-ttu-id="a942b-842">ProtectionStatus</span><span class="sxs-lookup"><span data-stu-id="a942b-842">ProtectionStatus</span></span> |<span data-ttu-id="a942b-843">Kötü amaçlı yazılım bulundu adı.</span><span class="sxs-lookup"><span data-stu-id="a942b-843">Name of malware found.</span></span> |
| <span data-ttu-id="a942b-844">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="a942b-844">StorageAccount</span></span> |<span data-ttu-id="a942b-845">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-845">W3CIISLog</span></span> |<span data-ttu-id="a942b-846">Azure depolama hesabı günlüğü okuma.</span><span class="sxs-lookup"><span data-stu-id="a942b-846">Azure Storage account the log was read from.</span></span> |
| <span data-ttu-id="a942b-847">AzureDeploymentID</span><span class="sxs-lookup"><span data-stu-id="a942b-847">AzureDeploymentID</span></span> |<span data-ttu-id="a942b-848">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-848">W3CIISLog</span></span> |<span data-ttu-id="a942b-849">Bulut hizmetinin günlük Azure dağıtım kimliği ait.</span><span class="sxs-lookup"><span data-stu-id="a942b-849">Azure deployment ID of the cloud service the log belongs to.</span></span> |
| <span data-ttu-id="a942b-850">Rol</span><span class="sxs-lookup"><span data-stu-id="a942b-850">Role</span></span> |<span data-ttu-id="a942b-851">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-851">W3CIISLog</span></span> |<span data-ttu-id="a942b-852">Azure bulut hizmeti günlük rolüne ait.</span><span class="sxs-lookup"><span data-stu-id="a942b-852">Role of the Azure cloud service the log belongs to.</span></span> |
| <span data-ttu-id="a942b-853">RoleInstance</span><span class="sxs-lookup"><span data-stu-id="a942b-853">RoleInstance</span></span> |<span data-ttu-id="a942b-854">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-854">W3CIISLog</span></span> |<span data-ttu-id="a942b-855">Günlük ait Azure rol RoleInstance.</span><span class="sxs-lookup"><span data-stu-id="a942b-855">RoleInstance of the Azure role that the log belongs to.</span></span> |
| <span data-ttu-id="a942b-856">sSiteName</span><span class="sxs-lookup"><span data-stu-id="a942b-856">sSiteName</span></span> |<span data-ttu-id="a942b-857">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-857">W3CIISLog</span></span> |<span data-ttu-id="a942b-858">Günlük (metatabanı gösterimine); ait olduğu IIS Web sitesi özgün günlüğü s-sitename alanında.</span><span class="sxs-lookup"><span data-stu-id="a942b-858">IIS website that the log belongs to (metabase notation); the s-sitename field in the original log.</span></span> |
| <span data-ttu-id="a942b-859">sComputerName</span><span class="sxs-lookup"><span data-stu-id="a942b-859">sComputerName</span></span> |<span data-ttu-id="a942b-860">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-860">W3CIISLog</span></span> |<span data-ttu-id="a942b-861">Özgün günlüğü s-computername alanında.</span><span class="sxs-lookup"><span data-stu-id="a942b-861">The s-computername field in the original log.</span></span> |
| <span data-ttu-id="a942b-862">SIP</span><span class="sxs-lookup"><span data-stu-id="a942b-862">sIP</span></span> |<span data-ttu-id="a942b-863">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-863">W3CIISLog</span></span> |<span data-ttu-id="a942b-864">Sunucu IP adresi HTTP isteği için giderilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a942b-864">Server IP address the HTTP request was addressed to.</span></span> <span data-ttu-id="a942b-865">Özgün günlüğü s-ip alanında.</span><span class="sxs-lookup"><span data-stu-id="a942b-865">The s-ip field in the original log.</span></span> |
| <span data-ttu-id="a942b-866">csMethod</span><span class="sxs-lookup"><span data-stu-id="a942b-866">csMethod</span></span> |<span data-ttu-id="a942b-867">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-867">W3CIISLog</span></span> |<span data-ttu-id="a942b-868">HTTP isteği istemci tarafından kullanılan HTTP yöntemini (örneğin, GET/POST).</span><span class="sxs-lookup"><span data-stu-id="a942b-868">HTTP method (for example, GET/POST) used by the client in the HTTP request.</span></span> <span data-ttu-id="a942b-869">Cs-yöntem özgün günlüğü.</span><span class="sxs-lookup"><span data-stu-id="a942b-869">The cs-method in the original log.</span></span> |
| <span data-ttu-id="a942b-870">CIP</span><span class="sxs-lookup"><span data-stu-id="a942b-870">cIP</span></span> |<span data-ttu-id="a942b-871">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-871">W3CIISLog</span></span> |<span data-ttu-id="a942b-872">İstemci IP adresi HTTP isteği geldi.</span><span class="sxs-lookup"><span data-stu-id="a942b-872">Client IP address the HTTP request came from.</span></span> <span data-ttu-id="a942b-873">Özgün günlüğü c-ip alanında.</span><span class="sxs-lookup"><span data-stu-id="a942b-873">The c-ip field in the original log.</span></span> |
| <span data-ttu-id="a942b-874">csUserAgent</span><span class="sxs-lookup"><span data-stu-id="a942b-874">csUserAgent</span></span> |<span data-ttu-id="a942b-875">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-875">W3CIISLog</span></span> |<span data-ttu-id="a942b-876">HTTP User-Agent istemci tarafından bildirilen (tarayıcı veya aksi halde).</span><span class="sxs-lookup"><span data-stu-id="a942b-876">HTTP User-Agent declared by the client (browser or otherwise).</span></span> <span data-ttu-id="a942b-877">Cs-user-agent özgün günlüğünde.</span><span class="sxs-lookup"><span data-stu-id="a942b-877">The cs-user-agent in the original log.</span></span> |
| <span data-ttu-id="a942b-878">scStatus</span><span class="sxs-lookup"><span data-stu-id="a942b-878">scStatus</span></span> |<span data-ttu-id="a942b-879">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-879">W3CIISLog</span></span> |<span data-ttu-id="a942b-880">Sunucu tarafından istemciye döndürülen HTTP durum kodu (örneğin, 200/403/500).</span><span class="sxs-lookup"><span data-stu-id="a942b-880">HTTP Status code (for example, 200/403/500) returned by the server to the client.</span></span> <span data-ttu-id="a942b-881">Özgün günlüğü cs-durum.</span><span class="sxs-lookup"><span data-stu-id="a942b-881">The cs-status in the original log.</span></span> |
| <span data-ttu-id="a942b-882">TimeTaken</span><span class="sxs-lookup"><span data-stu-id="a942b-882">TimeTaken</span></span> |<span data-ttu-id="a942b-883">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-883">W3CIISLog</span></span> |<span data-ttu-id="a942b-884">Nasıl isteği tamamlamak için harcanan uzun süre (milisaniye cinsinden).</span><span class="sxs-lookup"><span data-stu-id="a942b-884">How long (in milliseconds) that the request took to complete.</span></span> <span data-ttu-id="a942b-885">Özgün günlüğü timetaken alanında.</span><span class="sxs-lookup"><span data-stu-id="a942b-885">The timetaken field in the original log.</span></span> |
| <span data-ttu-id="a942b-886">csUriStem</span><span class="sxs-lookup"><span data-stu-id="a942b-886">csUriStem</span></span> |<span data-ttu-id="a942b-887">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-887">W3CIISLog</span></span> |<span data-ttu-id="a942b-888">Göreli URI (ana bilgisayar adresi olmadan, / arama) işlemi istendi.</span><span class="sxs-lookup"><span data-stu-id="a942b-888">Relative URI (without host address, that is, /search ) that was requested.</span></span> <span data-ttu-id="a942b-889">Özgün günlüğü cs bulunamadı.%n alanında.</span><span class="sxs-lookup"><span data-stu-id="a942b-889">The cs-uristem field in the original log.</span></span> |
| <span data-ttu-id="a942b-890">csUriQuery</span><span class="sxs-lookup"><span data-stu-id="a942b-890">csUriQuery</span></span> |<span data-ttu-id="a942b-891">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-891">W3CIISLog</span></span> |<span data-ttu-id="a942b-892">URI sorgusu.</span><span class="sxs-lookup"><span data-stu-id="a942b-892">URI query.</span></span> <span data-ttu-id="a942b-893">Bu alan bir tire statik sayfaları için genellikle içerecek şekilde URI sorgular yalnızca ASP sayfalarının gibi dinamik sayfalar için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a942b-893">URI queries are necessary only for dynamic pages, such as ASP pages, so this field usually contains a hyphen for static pages.</span></span> |
| <span data-ttu-id="a942b-894">Spor</span><span class="sxs-lookup"><span data-stu-id="a942b-894">sPort</span></span> |<span data-ttu-id="a942b-895">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-895">W3CIISLog</span></span> |<span data-ttu-id="a942b-896">HTTP isteğinin gönderildiği (ve bu toplanma beri için IIS'in dinler) sunucu bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="a942b-896">Server port that the HTTP request was sent to (and that IIS listens to, since it picked it up).</span></span> |
| <span data-ttu-id="a942b-897">csUserName</span><span class="sxs-lookup"><span data-stu-id="a942b-897">csUserName</span></span> |<span data-ttu-id="a942b-898">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-898">W3CIISLog</span></span> |<span data-ttu-id="a942b-899">İstek Kimliği doğrulanmış ve değil anonim ise kullanıcı adı kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="a942b-899">Authenticated user name, if the request is authenticated and not anonymous.</span></span> |
| <span data-ttu-id="a942b-900">csVersion</span><span class="sxs-lookup"><span data-stu-id="a942b-900">csVersion</span></span> |<span data-ttu-id="a942b-901">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-901">W3CIISLog</span></span> |<span data-ttu-id="a942b-902">(Örneğin, HTTP/1.1) istekte kullanılan HTTP protokolü sürümü.</span><span class="sxs-lookup"><span data-stu-id="a942b-902">HTTP Protocol version used in the request (for example, HTTP/1.1).</span></span> |
| <span data-ttu-id="a942b-903">csCookie</span><span class="sxs-lookup"><span data-stu-id="a942b-903">csCookie</span></span> |<span data-ttu-id="a942b-904">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-904">W3CIISLog</span></span> |<span data-ttu-id="a942b-905">Tanımlama bilgileri.</span><span class="sxs-lookup"><span data-stu-id="a942b-905">Cookie information.</span></span> |
| <span data-ttu-id="a942b-906">csReferer</span><span class="sxs-lookup"><span data-stu-id="a942b-906">csReferer</span></span> |<span data-ttu-id="a942b-907">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-907">W3CIISLog</span></span> |<span data-ttu-id="a942b-908">Kullanıcının son ziyaret sitesi.</span><span class="sxs-lookup"><span data-stu-id="a942b-908">Site that the user last visited.</span></span> <span data-ttu-id="a942b-909">Bu site geçerli siteye bir bağlantı sağladı.</span><span class="sxs-lookup"><span data-stu-id="a942b-909">This site provided a link to the current site.</span></span> |
| <span data-ttu-id="a942b-910">csHost</span><span class="sxs-lookup"><span data-stu-id="a942b-910">csHost</span></span> |<span data-ttu-id="a942b-911">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-911">W3CIISLog</span></span> |<span data-ttu-id="a942b-912">İstenen ana bilgisayar üst bilgisi (örneğin, www.mysite.com).</span><span class="sxs-lookup"><span data-stu-id="a942b-912">Host header (for example, www.mysite.com) that was requested.</span></span> |
| <span data-ttu-id="a942b-913">scSubStatus</span><span class="sxs-lookup"><span data-stu-id="a942b-913">scSubStatus</span></span> |<span data-ttu-id="a942b-914">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-914">W3CIISLog</span></span> |<span data-ttu-id="a942b-915">Alt durum hata kodu.</span><span class="sxs-lookup"><span data-stu-id="a942b-915">Substatus error code.</span></span> |
| <span data-ttu-id="a942b-916">scWin32Status</span><span class="sxs-lookup"><span data-stu-id="a942b-916">scWin32Status</span></span> |<span data-ttu-id="a942b-917">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-917">W3CIISLog</span></span> |<span data-ttu-id="a942b-918">Windows durum kodu.</span><span class="sxs-lookup"><span data-stu-id="a942b-918">Windows status code.</span></span> |
| <span data-ttu-id="a942b-919">csBytes</span><span class="sxs-lookup"><span data-stu-id="a942b-919">csBytes</span></span> |<span data-ttu-id="a942b-920">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-920">W3CIISLog</span></span> |<span data-ttu-id="a942b-921">İstekte istemciden sunucuya gönderilen bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="a942b-921">Bytes sent in the request from the client to the server.</span></span> |
| <span data-ttu-id="a942b-922">scBytes</span><span class="sxs-lookup"><span data-stu-id="a942b-922">scBytes</span></span> |<span data-ttu-id="a942b-923">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="a942b-923">W3CIISLog</span></span> |<span data-ttu-id="a942b-924">Sunucudan gelen yanıtı istemciye geri döndürülen bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="a942b-924">Bytes returned back in the response from the server to the client.</span></span> |
| <span data-ttu-id="a942b-925">ConfigChangeType</span><span class="sxs-lookup"><span data-stu-id="a942b-925">ConfigChangeType</span></span> |<span data-ttu-id="a942b-926">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="a942b-926">ConfigurationChange</span></span> |<span data-ttu-id="a942b-927">Değişiklik (örneğin, WindowsServices/yazılım) türü.</span><span class="sxs-lookup"><span data-stu-id="a942b-927">Type of change (for example, WindowsServices/Software).</span></span> |
| <span data-ttu-id="a942b-928">ChangeCategory</span><span class="sxs-lookup"><span data-stu-id="a942b-928">ChangeCategory</span></span> |<span data-ttu-id="a942b-929">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="a942b-929">ConfigurationChange</span></span> |<span data-ttu-id="a942b-930">(Değiştirilen/eklenen/kaldırıldı) değişiklik kategorisi.</span><span class="sxs-lookup"><span data-stu-id="a942b-930">Category of the change (Modified/Added/Removed).</span></span> |
| <span data-ttu-id="a942b-931">SoftwareType</span><span class="sxs-lookup"><span data-stu-id="a942b-931">SoftwareType</span></span> |<span data-ttu-id="a942b-932">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="a942b-932">ConfigurationChange</span></span> |<span data-ttu-id="a942b-933">Yazılım (güncelleştirme/uygulama) türü.</span><span class="sxs-lookup"><span data-stu-id="a942b-933">Type of software (Update/Application).</span></span> |
| <span data-ttu-id="a942b-934">SoftwareName</span><span class="sxs-lookup"><span data-stu-id="a942b-934">SoftwareName</span></span> |<span data-ttu-id="a942b-935">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="a942b-935">ConfigurationChange</span></span> |<span data-ttu-id="a942b-936">(Yalnızca yazılım değişiklikleri için geçerlidir) yazılım adı.</span><span class="sxs-lookup"><span data-stu-id="a942b-936">Name of the software (only applicable to software changes).</span></span> |
| <span data-ttu-id="a942b-937">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="a942b-937">Publisher</span></span> |<span data-ttu-id="a942b-938">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="a942b-938">ConfigurationChange</span></span> |<span data-ttu-id="a942b-939">(Yalnızca yazılım değişiklikleri için geçerlidir) yazılım yayımlar satıcı.</span><span class="sxs-lookup"><span data-stu-id="a942b-939">Vendor who publishes the software (only applicable to software changes).</span></span> |
| <span data-ttu-id="a942b-940">SvcChangeType</span><span class="sxs-lookup"><span data-stu-id="a942b-940">SvcChangeType</span></span> |<span data-ttu-id="a942b-941">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="a942b-941">ConfigurationChange</span></span> |<span data-ttu-id="a942b-942">Bir Windows hizmeti (durumu/StartupType/yol/HizmetHesabı) uygulandı değişiklik türü.</span><span class="sxs-lookup"><span data-stu-id="a942b-942">Type of change that was applied on a Windows service (State/StartupType/Path/ServiceAccount).</span></span> <span data-ttu-id="a942b-943">Bu yalnızca Windows hizmet değişiklikleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="a942b-943">This is only applicable to Windows service changes.</span></span> |
| <span data-ttu-id="a942b-944">SvcDisplayName</span><span class="sxs-lookup"><span data-stu-id="a942b-944">SvcDisplayName</span></span> |<span data-ttu-id="a942b-945">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="a942b-945">ConfigurationChange</span></span> |<span data-ttu-id="a942b-946">Değiştirilen hizmet görünen adı.</span><span class="sxs-lookup"><span data-stu-id="a942b-946">Display name of the service that was changed.</span></span> |
| <span data-ttu-id="a942b-947">SvcName</span><span class="sxs-lookup"><span data-stu-id="a942b-947">SvcName</span></span> |<span data-ttu-id="a942b-948">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="a942b-948">ConfigurationChange</span></span> |<span data-ttu-id="a942b-949">Değiştirildi hizmetin adı.</span><span class="sxs-lookup"><span data-stu-id="a942b-949">Name of the service that was changed.</span></span> |
| <span data-ttu-id="a942b-950">SvcState</span><span class="sxs-lookup"><span data-stu-id="a942b-950">SvcState</span></span> |<span data-ttu-id="a942b-951">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="a942b-951">ConfigurationChange</span></span> |<span data-ttu-id="a942b-952">Hizmetinin yeni (geçerli) durumu.</span><span class="sxs-lookup"><span data-stu-id="a942b-952">New (current) state of the service.</span></span> |
| <span data-ttu-id="a942b-953">SvcPreviousState</span><span class="sxs-lookup"><span data-stu-id="a942b-953">SvcPreviousState</span></span> |<span data-ttu-id="a942b-954">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="a942b-954">ConfigurationChange</span></span> |<span data-ttu-id="a942b-955">(Yalnızca hizmet durumu değişirse geçerlidir) hizmetinin durumunu bilinen önceki.</span><span class="sxs-lookup"><span data-stu-id="a942b-955">Previous known state of the service (only applicable if service state changed).</span></span> |
| <span data-ttu-id="a942b-956">SvcStartupType</span><span class="sxs-lookup"><span data-stu-id="a942b-956">SvcStartupType</span></span> |<span data-ttu-id="a942b-957">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="a942b-957">ConfigurationChange</span></span> |<span data-ttu-id="a942b-958">Hizmet başlangıç türü.</span><span class="sxs-lookup"><span data-stu-id="a942b-958">Service startup type.</span></span> |
| <span data-ttu-id="a942b-959">SvcPreviousStartupType</span><span class="sxs-lookup"><span data-stu-id="a942b-959">SvcPreviousStartupType</span></span> |<span data-ttu-id="a942b-960">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="a942b-960">ConfigurationChange</span></span> |<span data-ttu-id="a942b-961">Önceki hizmet başlatma türünü (yalnızca hizmet başlatma türünü değiştirdiyseniz geçerlidir).</span><span class="sxs-lookup"><span data-stu-id="a942b-961">Previous service startup type (only applicable if service startup type changed).</span></span> |
| <span data-ttu-id="a942b-962">SvcAccount</span><span class="sxs-lookup"><span data-stu-id="a942b-962">SvcAccount</span></span> |<span data-ttu-id="a942b-963">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="a942b-963">ConfigurationChange</span></span> |<span data-ttu-id="a942b-964">Hizmet hesabı.</span><span class="sxs-lookup"><span data-stu-id="a942b-964">Service account.</span></span> |
| <span data-ttu-id="a942b-965">SvcPreviousAccount</span><span class="sxs-lookup"><span data-stu-id="a942b-965">SvcPreviousAccount</span></span> |<span data-ttu-id="a942b-966">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="a942b-966">ConfigurationChange</span></span> |<span data-ttu-id="a942b-967">Önceki hizmet hesabı (yalnızca hizmet hesabı değiştirdiyseniz geçerlidir).</span><span class="sxs-lookup"><span data-stu-id="a942b-967">Previous service account (only applicable if service account changed).</span></span> |
| <span data-ttu-id="a942b-968">SvcPath</span><span class="sxs-lookup"><span data-stu-id="a942b-968">SvcPath</span></span> |<span data-ttu-id="a942b-969">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="a942b-969">ConfigurationChange</span></span> |<span data-ttu-id="a942b-970">Windows hizmeti yürütülebilir dosya yolu.</span><span class="sxs-lookup"><span data-stu-id="a942b-970">Path to the executable of the Windows service.</span></span> |
| <span data-ttu-id="a942b-971">SvcPreviousPath</span><span class="sxs-lookup"><span data-stu-id="a942b-971">SvcPreviousPath</span></span> |<span data-ttu-id="a942b-972">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="a942b-972">ConfigurationChange</span></span> |<span data-ttu-id="a942b-973">Yürütülebilir dosya (yalnızca onu değiştirdiyseniz geçerlidir) Windows hizmeti için önceki yolu.</span><span class="sxs-lookup"><span data-stu-id="a942b-973">Previous path of the executable for the Windows service (only applicable if it changed).</span></span> |
| <span data-ttu-id="a942b-974">SvcDescription</span><span class="sxs-lookup"><span data-stu-id="a942b-974">SvcDescription</span></span> |<span data-ttu-id="a942b-975">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="a942b-975">ConfigurationChange</span></span> |<span data-ttu-id="a942b-976">Hizmet açıklaması.</span><span class="sxs-lookup"><span data-stu-id="a942b-976">Description of the service.</span></span> |
| <span data-ttu-id="a942b-977">Önceki</span><span class="sxs-lookup"><span data-stu-id="a942b-977">Previous</span></span> |<span data-ttu-id="a942b-978">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="a942b-978">ConfigurationChange</span></span> |<span data-ttu-id="a942b-979">Bu yazılımı (yüklü/değil yüklü/önceki sürüm) önceki durumu.</span><span class="sxs-lookup"><span data-stu-id="a942b-979">Previous state of this software (Installed/Not Installed/previous version).</span></span> |
| <span data-ttu-id="a942b-980">Geçerli</span><span class="sxs-lookup"><span data-stu-id="a942b-980">Current</span></span> |<span data-ttu-id="a942b-981">ConfigurationChange</span><span class="sxs-lookup"><span data-stu-id="a942b-981">ConfigurationChange</span></span> |<span data-ttu-id="a942b-982">Son durum bu yazılımın (yüklü/değil yüklü/geçerli sürüm).</span><span class="sxs-lookup"><span data-stu-id="a942b-982">Latest state of this software (Installed/Not Installed/current version).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a942b-983">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a942b-983">Next steps</span></span>
<span data-ttu-id="a942b-984">Günlük aramaları hakkında ek bilgi için:</span><span class="sxs-lookup"><span data-stu-id="a942b-984">For additional information about log searches:</span></span>

* <span data-ttu-id="a942b-985">Çözümler tarafından toplanan ayrıntılı bilgileri görüntülemek için [günlük aramaları](log-analytics-log-searches.md) hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="a942b-985">Get familiar with [log searches](log-analytics-log-searches.md) to view detailed information gathered by solutions.</span></span>
* <span data-ttu-id="a942b-986">Kullanım [günlük analizi içinde özel alanlar](log-analytics-custom-fields.md) günlük aramaları genişletmek için.</span><span class="sxs-lookup"><span data-stu-id="a942b-986">Use [custom fields in Log Analytics](log-analytics-custom-fields.md) to extend log searches.</span></span>
