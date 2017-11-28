---
title: "aaaConstructing filtre dizeleri hello Tablo Tasarımcısı için | Microsoft Docs"
description: "Filtre dizeleri hello Tablo Tasarımcısı için oluşturma"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a1a10ea1-687a-4ee1-a952-6b24c2fe1a22
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 48b38d27b97936064daa875e41881d51546bc11f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="constructing-filter-strings-for-hello-table-designer"></a><span data-ttu-id="c21b1-103">Tablo Tasarımcısı hello için filtre dizeler oluşturma</span><span class="sxs-lookup"><span data-stu-id="c21b1-103">Constructing Filter Strings for hello Table Designer</span></span>
## <a name="overview"></a><span data-ttu-id="c21b1-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c21b1-104">Overview</span></span>
<span data-ttu-id="c21b1-105">görüntülenen bir Azure tablosunda toofilter veri hello Visual Studio **Tablo Tasarımcısı**, bir filtre dizesi oluşturmak ve hello filtre alanına girin.</span><span class="sxs-lookup"><span data-stu-id="c21b1-105">toofilter data in an Azure table that is displayed in hello Visual Studio **Table Designer**, you construct a filter string and enter it into hello filter field.</span></span> <span data-ttu-id="c21b1-106">Merhaba filtre dizesi sözdizimi hello WCF Veri Hizmetleri tarafından tanımlanır ve benzer tooa SQL WHERE yan tümcesi, ancak toohello tablo hizmeti bir HTTP isteği aracılığıyla gönderilir.</span><span class="sxs-lookup"><span data-stu-id="c21b1-106">hello filter string syntax is defined by hello WCF Data Services and is similar tooa SQL WHERE clause, but is sent toohello Table service via an HTTP request.</span></span> <span data-ttu-id="c21b1-107">Merhaba **Tablo Tasarımcısı** tanıtıcıları Merhaba, bunu toofilter istenen özellik değeri için uygun kodlama, hello özellik adı, karşılaştırma işleci ölçüt değeri yalnızca girmeniz gerekiyor ve isteğe bağlı olarak, hello Boole işleci filtre alan.</span><span class="sxs-lookup"><span data-stu-id="c21b1-107">hello **Table Designer** handles hello proper encoding for you, so toofilter on a desired property value, you need only enter hello property name, comparison operator, criteria value, and optionally, Boolean operator in hello filter field.</span></span> <span data-ttu-id="c21b1-108">Bir URL tooquery hello tablo hello aracılığıyla oluşturma yaptığınız gibi tooinclude hello $filter sorgu seçeneği gerekmez [depolama hizmetleri REST API Başvurusu](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span><span class="sxs-lookup"><span data-stu-id="c21b1-108">You do not need tooinclude hello $filter query option as you would if you were constructing a URL tooquery hello table via hello [Storage Services REST API Reference](http://go.microsoft.com/fwlink/p/?LinkId=400447).</span></span>

<span data-ttu-id="c21b1-109">Merhaba WCF veri hizmetleri üzerinde hello dayalı [açık veri Protokolü](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span><span class="sxs-lookup"><span data-stu-id="c21b1-109">hello WCF Data Services are based on hello [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData).</span></span> <span data-ttu-id="c21b1-110">Merhaba filtre sistem sorgusu seçeneği hakkında ayrıntılı bilgi için (**$filter**), hello bkz [OData URI kurallarını belirtimi](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span><span class="sxs-lookup"><span data-stu-id="c21b1-110">For details on hello filter system query option (**$filter**), see hello [OData URI Conventions specification](http://go.microsoft.com/fwlink/p/?LinkId=214806).</span></span>

## <a name="comparison-operators"></a><span data-ttu-id="c21b1-111">Karşılaştırma İşleçleri</span><span class="sxs-lookup"><span data-stu-id="c21b1-111">Comparison Operators</span></span>
<span data-ttu-id="c21b1-112">Merhaba aşağıdaki mantıksal işleçler tüm özellik türleri için desteklenir:</span><span class="sxs-lookup"><span data-stu-id="c21b1-112">hello following logical operators are supported for all property types:</span></span>

| <span data-ttu-id="c21b1-113">Mantıksal işleci</span><span class="sxs-lookup"><span data-stu-id="c21b1-113">Logical operator</span></span> | <span data-ttu-id="c21b1-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c21b1-114">Description</span></span> | <span data-ttu-id="c21b1-115">Örnek filtre dizesi</span><span class="sxs-lookup"><span data-stu-id="c21b1-115">Example filter string</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c21b1-116">EQ</span><span class="sxs-lookup"><span data-stu-id="c21b1-116">eq</span></span> |<span data-ttu-id="c21b1-117">Eşittir</span><span class="sxs-lookup"><span data-stu-id="c21b1-117">Equal</span></span> |<span data-ttu-id="c21b1-118">Şehir eq 'Redmond'</span><span class="sxs-lookup"><span data-stu-id="c21b1-118">City eq 'Redmond'</span></span> |
| <span data-ttu-id="c21b1-119">gt</span><span class="sxs-lookup"><span data-stu-id="c21b1-119">gt</span></span> |<span data-ttu-id="c21b1-120">Şu değerden fazla:</span><span class="sxs-lookup"><span data-stu-id="c21b1-120">Greater than</span></span> |<span data-ttu-id="c21b1-121">Fiyat gt 20</span><span class="sxs-lookup"><span data-stu-id="c21b1-121">Price gt 20</span></span> |
| <span data-ttu-id="c21b1-122">Ge</span><span class="sxs-lookup"><span data-stu-id="c21b1-122">ge</span></span> |<span data-ttu-id="c21b1-123">Büyük veya ona eşit çok</span><span class="sxs-lookup"><span data-stu-id="c21b1-123">Greater than or equal too</span></span>|<span data-ttu-id="c21b1-124">Fiyat ge 10</span><span class="sxs-lookup"><span data-stu-id="c21b1-124">Price ge 10</span></span> |
| <span data-ttu-id="c21b1-125">lt</span><span class="sxs-lookup"><span data-stu-id="c21b1-125">lt</span></span> |<span data-ttu-id="c21b1-126">Şu değerden az:</span><span class="sxs-lookup"><span data-stu-id="c21b1-126">Less than</span></span> |<span data-ttu-id="c21b1-127">Fiyat lt 20</span><span class="sxs-lookup"><span data-stu-id="c21b1-127">Price lt 20</span></span> |
| <span data-ttu-id="c21b1-128">le</span><span class="sxs-lookup"><span data-stu-id="c21b1-128">le</span></span> |<span data-ttu-id="c21b1-129">Küçüktür veya eşittir</span><span class="sxs-lookup"><span data-stu-id="c21b1-129">Less than or equal</span></span> |<span data-ttu-id="c21b1-130">Fiyat le 100</span><span class="sxs-lookup"><span data-stu-id="c21b1-130">Price le 100</span></span> |
| <span data-ttu-id="c21b1-131">ne</span><span class="sxs-lookup"><span data-stu-id="c21b1-131">ne</span></span> |<span data-ttu-id="c21b1-132">Eşit değildir</span><span class="sxs-lookup"><span data-stu-id="c21b1-132">Not equal</span></span> |<span data-ttu-id="c21b1-133">Şehir ne 'Londra'</span><span class="sxs-lookup"><span data-stu-id="c21b1-133">City ne 'London'</span></span> |
| <span data-ttu-id="c21b1-134">ve</span><span class="sxs-lookup"><span data-stu-id="c21b1-134">and</span></span> |<span data-ttu-id="c21b1-135">Ve</span><span class="sxs-lookup"><span data-stu-id="c21b1-135">And</span></span> |<span data-ttu-id="c21b1-136">Fiyat le 200 ve fiyat gt 3.5</span><span class="sxs-lookup"><span data-stu-id="c21b1-136">Price le 200 and Price gt 3.5</span></span> |
| <span data-ttu-id="c21b1-137">or</span><span class="sxs-lookup"><span data-stu-id="c21b1-137">or</span></span> |<span data-ttu-id="c21b1-138">Veya</span><span class="sxs-lookup"><span data-stu-id="c21b1-138">Or</span></span> |<span data-ttu-id="c21b1-139">Fiyat le 3.5 veya fiyat gt 200</span><span class="sxs-lookup"><span data-stu-id="c21b1-139">Price le 3.5 or Price gt 200</span></span> |
| <span data-ttu-id="c21b1-140">değil</span><span class="sxs-lookup"><span data-stu-id="c21b1-140">not</span></span> |<span data-ttu-id="c21b1-141">değil</span><span class="sxs-lookup"><span data-stu-id="c21b1-141">Not</span></span> |<span data-ttu-id="c21b1-142">IsAvailable değil</span><span class="sxs-lookup"><span data-stu-id="c21b1-142">not isAvailable</span></span> |

<span data-ttu-id="c21b1-143">Bir filtre dizesi oluşturulurken hello aşağıdaki kuralları önemlidir:</span><span class="sxs-lookup"><span data-stu-id="c21b1-143">When constructing a filter string, hello following rules are important:</span></span>

* <span data-ttu-id="c21b1-144">Merhaba mantıksal işleçler toocompare özellik tooa değerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c21b1-144">Use hello logical operators toocompare a property tooa value.</span></span> <span data-ttu-id="c21b1-145">Olası toocompare bir özellik tooa dinamik değeri olmadığını unutmayın; sütunlardan biri hello ifade bir sabit olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c21b1-145">Note that it is not possible toocompare a property tooa dynamic value; one side of hello expression must be a constant.</span></span>
* <span data-ttu-id="c21b1-146">Tüm parçalarını hello filtre dizesi büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="c21b1-146">All parts of hello filter string are case-sensitive.</span></span>
* <span data-ttu-id="c21b1-147">Merhaba sabit değer hello olmalıdır aynı veri türü hello filtre tooreturn geçerli sonuçları düzenini hello özelliği olarak.</span><span class="sxs-lookup"><span data-stu-id="c21b1-147">hello constant value must be of hello same data type as hello property in order for hello filter tooreturn valid results.</span></span> <span data-ttu-id="c21b1-148">Desteklenen özellik türleri hakkında daha fazla bilgi için bkz: [anlama hello tablo hizmeti veri modelini](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span><span class="sxs-lookup"><span data-stu-id="c21b1-148">For more information about supported property types, see [Understanding hello Table Service Data Model](http://go.microsoft.com/fwlink/p/?LinkId=400448).</span></span>

## <a name="filtering-on-string-properties"></a><span data-ttu-id="c21b1-149">Dize özellikleri filtreleme</span><span class="sxs-lookup"><span data-stu-id="c21b1-149">Filtering on String Properties</span></span>
<span data-ttu-id="c21b1-150">Dize özellikleri filtre uygularken hello dize sabiti tek tırnak işaretleri içine alın.</span><span class="sxs-lookup"><span data-stu-id="c21b1-150">When you filter on string properties, enclose hello string constant in single quotation marks.</span></span>

<span data-ttu-id="c21b1-151">Örnek filtreleri hello üzerinde aşağıdaki hello **PartitionKey** ve **RowKey** özellikleri; ek anahtar olmayan özellikler toohello filtre dizesini de eklenebiliyordu:</span><span class="sxs-lookup"><span data-stu-id="c21b1-151">hello following example filters on hello **PartitionKey** and **RowKey** properties; additional non-key properties could also be added toohello filter string:</span></span>

    PartitionKey eq 'Partition1' and RowKey eq '00001'

<span data-ttu-id="c21b1-152">Gerekli olmamasına rağmen her filtre ifadesi parantez içine alın:</span><span class="sxs-lookup"><span data-stu-id="c21b1-152">You can enclose each filter expression in parentheses, although it is not required:</span></span>

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

<span data-ttu-id="c21b1-153">Merhaba tablo hizmeti joker sorguları desteklemez ve hello Tablo Tasarımcısı da desteklenmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c21b1-153">Note that hello Table service does not support wildcard queries, and they are not supported in hello Table Designer either.</span></span> <span data-ttu-id="c21b1-154">Ancak, önek eşleştirme hello istenen ön ekini temel Karşılaştırma işleçleri kullanarak gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c21b1-154">However, you can perform prefix matching by using comparison operators on hello desired prefix.</span></span> <span data-ttu-id="c21b1-155">Merhaba aşağıdaki örnek varlıklar hello harf 'A' ile başlayan bir soyadı özelliği ile döndürür:</span><span class="sxs-lookup"><span data-stu-id="c21b1-155">hello following example returns entities with a LastName property beginning with hello letter 'A':</span></span>

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a><span data-ttu-id="c21b1-156">Sayısal özellikleri filtreleme</span><span class="sxs-lookup"><span data-stu-id="c21b1-156">Filtering on Numeric Properties</span></span>
<span data-ttu-id="c21b1-157">bir tamsayı veya kayan noktalı sayı toofilter tırnak işaretleri olmadan hello numarasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="c21b1-157">toofilter on an integer or floating-point number, specify hello number without quotation marks.</span></span>

<span data-ttu-id="c21b1-158">Bu örnek değeri 30'dan büyük olan bir geçerlilik süresi özelliğine sahip tüm varlıkları döndürür:</span><span class="sxs-lookup"><span data-stu-id="c21b1-158">This example returns all entities with an Age property whose value is greater than 30:</span></span>

    Age gt 30

<span data-ttu-id="c21b1-159">Bu örnek, değeri olan bir AmountDue özelliğine sahip tüm varlıklar döndürüyor küçüktür veya too100.25 eşit:</span><span class="sxs-lookup"><span data-stu-id="c21b1-159">This example returns all entities with an AmountDue property whose value is less than or equal too100.25:</span></span>

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a><span data-ttu-id="c21b1-160">Boole özellikleri filtreleme</span><span class="sxs-lookup"><span data-stu-id="c21b1-160">Filtering on Boolean Properties</span></span>
<span data-ttu-id="c21b1-161">toofilter bir Boole değeri belirtin **true** veya **false** tırnak işaretleri olmadan.</span><span class="sxs-lookup"><span data-stu-id="c21b1-161">toofilter on a Boolean value, specify **true** or **false** without quotation marks.</span></span>

<span data-ttu-id="c21b1-162">Merhaba aşağıdaki örnekte tüm varlıklar hello Isactive özelliği çok ayarlandığı döndürür**true**:</span><span class="sxs-lookup"><span data-stu-id="c21b1-162">hello following example returns all entities where hello IsActive property is set too**true**:</span></span>

    IsActive eq true

<span data-ttu-id="c21b1-163">Bu filtre ifadesi hello mantıksal işleç olmadan da yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c21b1-163">You can also write this filter expression without hello logical operator.</span></span> <span data-ttu-id="c21b1-164">Aşağıdaki örneğine hello hello tablo hizmeti de tüm varlıklar Isactive olduğu döndürülecek **true**:</span><span class="sxs-lookup"><span data-stu-id="c21b1-164">In hello following example, hello Table service will also return all entities where IsActive is **true**:</span></span>

    IsActive

<span data-ttu-id="c21b1-165">Isactive olduğu false, kullanabileceğiniz tüm varlıklar hello değil tooreturn işleci:</span><span class="sxs-lookup"><span data-stu-id="c21b1-165">tooreturn all entities where IsActive is false, you can use hello not operator:</span></span>

    not IsActive

## <a name="filtering-on-datetime-properties"></a><span data-ttu-id="c21b1-166">DateTime özellikleri üzerinde filtreleme</span><span class="sxs-lookup"><span data-stu-id="c21b1-166">Filtering on DateTime Properties</span></span>
<span data-ttu-id="c21b1-167">bir DateTime değeri toofilter belirtin hello **datetime** anahtar sözcüğü, tek tırnak işaretleri içindeki hello tarih sabiti arkasından.</span><span class="sxs-lookup"><span data-stu-id="c21b1-167">toofilter on a DateTime value, specify hello **datetime** keyword, followed by hello date/time constant in single quotation marks.</span></span> <span data-ttu-id="c21b1-168">bölümünde açıklandığı gibi Hello tarih sabiti birleşik UTC biçiminde olmalıdır [biçimlendirme DateTime özellik değerlerini](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span><span class="sxs-lookup"><span data-stu-id="c21b1-168">hello date/time constant must be in combined UTC format, as described in [Formatting DateTime Property Values](http://go.microsoft.com/fwlink/p/?LinkId=400449).</span></span>

<span data-ttu-id="c21b1-169">Aşağıdaki örnek hello hello CustomerSince özelliği 2008 eşit tooJuly 10 olduğu varlıklar döndürüyor:</span><span class="sxs-lookup"><span data-stu-id="c21b1-169">hello following example returns entities where hello CustomerSince property is equal tooJuly 10, 2008:</span></span>

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
