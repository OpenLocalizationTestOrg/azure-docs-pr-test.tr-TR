---
title: "Azure API yönetimi ilkelerini aaaHow toouse özellikleri"
description: "Bilgi nasıl Azure API yönetimi ilkelerini toouse özelliklerinde."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f39b00f-cf6e-4cef-9bf2-1f89202c0bc0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 1ff096deeb97543b48dcf1f40be9dbfcbcd09542
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-properties-in-azure-api-management-policies"></a><span data-ttu-id="03ba0-103">Nasıl toouse özelliklerinde Azure API Management ilkeleri</span><span class="sxs-lookup"><span data-stu-id="03ba0-103">How toouse properties in Azure API Management policies</span></span>
<span data-ttu-id="03ba0-104">API Management, güçlü bir özellik toochange hello davranışını yapılandırma yoluyla hello API hello publisher izin hello sisteminin ilkelerdir.</span><span class="sxs-lookup"><span data-stu-id="03ba0-104">API Management policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="03ba0-105">Merhaba istek üzerinde sırayla yürütülen deyimlerin bir koleksiyon veya bir API yanıtını ilkelerdir.</span><span class="sxs-lookup"><span data-stu-id="03ba0-105">Policies are a collection of statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="03ba0-106">İlke deyimleri metin değerleri, ilke ifadelerini ve özellikleri kullanarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="03ba0-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="03ba0-107">Her API Management hizmeti örneği genel toohello hizmet örneği anahtar/değer çiftleri özellikleri koleksiyonu vardır.</span><span class="sxs-lookup"><span data-stu-id="03ba0-107">Each API Management service instance has a properties collection of key/value pairs that are global toohello service instance.</span></span> <span data-ttu-id="03ba0-108">Bu özellikler, tüm API yapılandırması ve ilkeleri kullanılan toomanage sabit dize değerleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="03ba0-108">These properties can be used toomanage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="03ba0-109">Her bir özellik öznitelikleri aşağıdaki hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="03ba0-109">Each property has hello following attributes.</span></span>

| <span data-ttu-id="03ba0-110">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="03ba0-110">Attribute</span></span> | <span data-ttu-id="03ba0-111">Tür</span><span class="sxs-lookup"><span data-stu-id="03ba0-111">Type</span></span> | <span data-ttu-id="03ba0-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="03ba0-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="03ba0-113">Ad</span><span class="sxs-lookup"><span data-stu-id="03ba0-113">Name</span></span> |<span data-ttu-id="03ba0-114">Dize</span><span class="sxs-lookup"><span data-stu-id="03ba0-114">string</span></span> |<span data-ttu-id="03ba0-115">Merhaba özelliğinin Hello adı.</span><span class="sxs-lookup"><span data-stu-id="03ba0-115">hello name of hello property.</span></span> <span data-ttu-id="03ba0-116">İçeren yalnızca harf, rakam, nokta, tire ve alt çizgi karakterleri.</span><span class="sxs-lookup"><span data-stu-id="03ba0-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="03ba0-117">Değer</span><span class="sxs-lookup"><span data-stu-id="03ba0-117">Value</span></span> |<span data-ttu-id="03ba0-118">Dize</span><span class="sxs-lookup"><span data-stu-id="03ba0-118">string</span></span> |<span data-ttu-id="03ba0-119">Merhaba özelliğinin Hello değeri.</span><span class="sxs-lookup"><span data-stu-id="03ba0-119">hello value of hello property.</span></span> <span data-ttu-id="03ba0-120">Bunu boş olamaz veya yalnızca boşluktan oluşamaz.</span><span class="sxs-lookup"><span data-stu-id="03ba0-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="03ba0-121">Gizli dizi</span><span class="sxs-lookup"><span data-stu-id="03ba0-121">Secret</span></span> |<span data-ttu-id="03ba0-122">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="03ba0-122">boolean</span></span> |<span data-ttu-id="03ba0-123">Merhaba değeri gizli olmadığından ve veya şifrelenmelidir olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="03ba0-123">Determines whether hello value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="03ba0-124">Etiketler</span><span class="sxs-lookup"><span data-stu-id="03ba0-124">Tags</span></span> |<span data-ttu-id="03ba0-125">Dize dizisi</span><span class="sxs-lookup"><span data-stu-id="03ba0-125">array of string</span></span> |<span data-ttu-id="03ba0-126">İsteğe bağlı etiketleri, sağlandığında kullanılan toofilter hello özellik listesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="03ba0-126">Optional tags that when provided can be used toofilter hello property list.</span></span> |

<span data-ttu-id="03ba0-127">Özellikler hello hello yayımcı portalında yapılandırılır **özellikleri** sekmesi. Aşağıdaki örneğine hello üç özellikleri yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="03ba0-127">Properties are configured in hello publisher portal on hello **Properties** tab. In hello following example, three properties are configured.</span></span>

![Özellikler][api-management-properties]

<span data-ttu-id="03ba0-129">Özellik değerlerini değişmez değer dizeleri içerebilir ve [ilke ifadelerini](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span><span class="sxs-lookup"><span data-stu-id="03ba0-129">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="03ba0-130">Merhaba aşağıdaki tabloda hello önceki üç örnek özelliklerini ve bunların öznitelikleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="03ba0-130">hello following table shows hello previous three sample properties and their attributes.</span></span> <span data-ttu-id="03ba0-131">Merhaba değerini `ExpressionProperty` içeren bir dize döndürür bir ilke ifadesi hello geçerli tarih ve saat değil.</span><span class="sxs-lookup"><span data-stu-id="03ba0-131">hello value of `ExpressionProperty` is a policy expression that returns a string containing hello current date and time.</span></span> <span data-ttu-id="03ba0-132">Merhaba özelliği `ContosoHeaderValue` değerini gösterilmesi için gizlilik olarak işaretlenmiş.</span><span class="sxs-lookup"><span data-stu-id="03ba0-132">hello property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="03ba0-133">Ad</span><span class="sxs-lookup"><span data-stu-id="03ba0-133">Name</span></span> | <span data-ttu-id="03ba0-134">Değer</span><span class="sxs-lookup"><span data-stu-id="03ba0-134">Value</span></span> | <span data-ttu-id="03ba0-135">Gizli dizi</span><span class="sxs-lookup"><span data-stu-id="03ba0-135">Secret</span></span> | <span data-ttu-id="03ba0-136">Etiketler</span><span class="sxs-lookup"><span data-stu-id="03ba0-136">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="03ba0-137">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="03ba0-137">ContosoHeader</span></span> |<span data-ttu-id="03ba0-138">İzleme kodu</span><span class="sxs-lookup"><span data-stu-id="03ba0-138">TrackingId</span></span> |<span data-ttu-id="03ba0-139">False</span><span class="sxs-lookup"><span data-stu-id="03ba0-139">False</span></span> |<span data-ttu-id="03ba0-140">Contoso</span><span class="sxs-lookup"><span data-stu-id="03ba0-140">Contoso</span></span> |
| <span data-ttu-id="03ba0-141">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="03ba0-141">ContosoHeaderValue</span></span> |<span data-ttu-id="03ba0-142">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="03ba0-142">••••••••••••••••••••••</span></span> |<span data-ttu-id="03ba0-143">True</span><span class="sxs-lookup"><span data-stu-id="03ba0-143">True</span></span> |<span data-ttu-id="03ba0-144">Contoso</span><span class="sxs-lookup"><span data-stu-id="03ba0-144">Contoso</span></span> |
| <span data-ttu-id="03ba0-145">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="03ba0-145">ExpressionProperty</span></span> |<span data-ttu-id="03ba0-146">@(DateTime.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="03ba0-146">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="03ba0-147">False</span><span class="sxs-lookup"><span data-stu-id="03ba0-147">False</span></span> | |

## <a name="toouse-a-property"></a><span data-ttu-id="03ba0-148">toouse özelliği</span><span class="sxs-lookup"><span data-stu-id="03ba0-148">toouse a property</span></span>
<span data-ttu-id="03ba0-149">bir çift çift köşeli parantez içinde yer hello özellik adı toouse bir ilke özelliği, ister `{{ContosoHeader}}`hello aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="03ba0-149">toouse a property in a policy, place hello property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in hello following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="03ba0-150">Bu örnekte, `ContosoHeader` başlığı hello adı olarak kullanılan bir `set-header` İlkesi ve `ContosoHeaderValue` bu başlığı hello değeri olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="03ba0-150">In this example, `ContosoHeader` is used as hello name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as hello value of that header.</span></span> <span data-ttu-id="03ba0-151">Bu ilke bir istek veya yanıt toohello API Yönetimi ağ geçidi sırasında değerlendirildiğinde `{{ContosoHeader}}` ve `{{ContosoHeaderValue}}` ilgili özellik değerlerine ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="03ba0-151">When this policy is evaluated during a request or response toohello API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="03ba0-152">Özellikler tam özniteliği ya da hello önceki örnekte gösterildiği gibi öğesi değerleri olarak kullanılabilir, ancak bunlar da yüklenebilir eklenen veya hello aşağıdaki örnekte gösterildiği gibi bir metin ifadenin bir parçası birleştirilmiş:`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="03ba0-152">Properties can be used as complete attribute or element values as shown in hello previous example, but they can also be inserted into or combined with part of a literal text expression as shown in hello following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="03ba0-153">Özellikler de ilke ifadelerini içerebilir.</span><span class="sxs-lookup"><span data-stu-id="03ba0-153">Properties can also contain policy expressions.</span></span> <span data-ttu-id="03ba0-154">Aşağıdaki örneğine hello hello `ExpressionProperty` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="03ba0-154">In hello following example, hello `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="03ba0-155">Bu ilke değerlendirildiğinde `{{ExpressionProperty}}` değeriyle değiştirilir: `@(DateTime.Now.ToString())`.</span><span class="sxs-lookup"><span data-stu-id="03ba0-155">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="03ba0-156">Merhaba değeri bir ilke ifadesi olduğundan hello ifade değerlendirilir ve hello İlkesi yürütülmesinin ile devam eder.</span><span class="sxs-lookup"><span data-stu-id="03ba0-156">Since hello value is a policy expression, hello expression is evaluated and hello policy proceeds with its execution.</span></span>

<span data-ttu-id="03ba0-157">Bu sorunu anlamak hello Geliştirici Portalı'nda özelliklere sahip bir ilke kapsamında olan bir işlem çağırarak test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03ba0-157">You can test this out in hello developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="03ba0-158">Aşağıdaki örneğine hello hello iki önceki örnekle bir işlem çağrılır `set-header` ilkeleri özelliklere sahip.</span><span class="sxs-lookup"><span data-stu-id="03ba0-158">In hello following example, an operation is called with hello two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="03ba0-159">Merhaba yanıt özelliklere sahip ilkeleri kullanarak yapılandırılmış iki özel üstbilgi içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="03ba0-159">Note that hello response contains two custom headers that were configured using policies with properties.</span></span>

![Geliştirici portalı][api-management-send-results]

<span data-ttu-id="03ba0-161">Merhaba bakarsanız [API denetçisi izleme](api-management-howto-api-inspector.md) hello önceki örnek sahip iki ilke özellikleri içeren bir arama hello iki görebilirsiniz `set-header` hello özellik değerlerinin yanı sıra hello İlkesi ifade eklenen ilkeleriyle Değerlendirme hello İlkesi ifade bulunan hello özelliği.</span><span class="sxs-lookup"><span data-stu-id="03ba0-161">If you look at hello [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes hello two previous sample policies with properties, you can see hello two `set-header` policies with hello property values inserted as well as hello policy expression evaluation for hello property that contained hello policy expression.</span></span>

![API denetçisi izleme][api-management-api-inspector-trace]

<span data-ttu-id="03ba0-163">Özellik değerlerini ilke ifadelerini içerebilir olsa da, özellik değerleri diğer özellikleri içeremez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="03ba0-163">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="03ba0-164">Bir özellik referansı içeren metin gibi bir özellik değeri için kullanılıyorsa, `Property value text {{MyProperty}}`, Özellik Başvurusu değiştirilmesi olmaz ve hello özellik değerinin bir parçası olarak dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="03ba0-164">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of hello property value.</span></span>

## <a name="toocreate-a-property"></a><span data-ttu-id="03ba0-165">toocreate özelliği</span><span class="sxs-lookup"><span data-stu-id="03ba0-165">toocreate a property</span></span>
<span data-ttu-id="03ba0-166">toocreate bir özellik tıklatın **özellik ekleme** hello üzerinde **özellikleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="03ba0-166">toocreate a property, click **Add property** on hello **Properties** tab.</span></span>

![Özellik ekleme][api-management-properties-add-property-menu]

<span data-ttu-id="03ba0-168">**Ad** ve **değeri** gerekli değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="03ba0-168">**Name** and **Value** are required values.</span></span> <span data-ttu-id="03ba0-169">Bu özellik değeri bir gizli anahtarı ise hello denetleyin **bu gizli olmadığından** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="03ba0-169">If this property value is a secret, check hello **This is a secret** checkbox.</span></span> <span data-ttu-id="03ba0-170">Özelliklerinizi düzenleme ile bir veya daha fazla isteğe bağlı etiketleri toohelp girin ve **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="03ba0-170">Enter one or more optional tags toohelp with organizing your properties, and click **Save**.</span></span>

![Özellik ekleme][api-management-properties-add-property]

<span data-ttu-id="03ba0-172">Yeni bir özellik kaydedildiğinde hello **arama özelliği** textbox hello hello yeni bir özellik adıyla doldurulur ve hello yeni özellik görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="03ba0-172">When a new property is saved, hello **Search property** textbox is populated with hello name of hello new property and hello new property is displayed.</span></span> <span data-ttu-id="03ba0-173">Tüm özellikleri toodisplay temizleyin hello **arama özelliği** textbox ve ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="03ba0-173">toodisplay all properties, clear hello **Search property** textbox and press enter.</span></span>

![Özellikler][api-management-properties-property-saved]

<span data-ttu-id="03ba0-175">Merhaba REST API kullanarak bir özelliği oluşturma hakkında daha fazla bilgi için bkz: [hello REST API kullanarak özellik oluşturma](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span><span class="sxs-lookup"><span data-stu-id="03ba0-175">For information on creating a property using hello REST API, see [Create a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="tooedit-a-property"></a><span data-ttu-id="03ba0-176">tooedit özelliği</span><span class="sxs-lookup"><span data-stu-id="03ba0-176">tooedit a property</span></span>
<span data-ttu-id="03ba0-177">tooedit bir özellik tıklatın **Düzenle** hello özelliği tooedit yanında.</span><span class="sxs-lookup"><span data-stu-id="03ba0-177">tooedit a property, click **Edit** beside hello property tooedit.</span></span>

![Özelliği Düzenle][api-management-properties-edit]

<span data-ttu-id="03ba0-179">İstediğiniz değişiklikleri yapın ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="03ba0-179">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="03ba0-180">Merhaba özellik adını değiştirirseniz, bu özellik başvuran tüm otomatik olarak güncelleştirilen toouse hello yeni adı ilkelerdir.</span><span class="sxs-lookup"><span data-stu-id="03ba0-180">If you change hello property name, any policies that reference that property are automatically updated toouse hello new name.</span></span>

![Özelliği Düzenle][api-management-properties-edit-property]

<span data-ttu-id="03ba0-182">Merhaba REST API kullanarak özellik düzenleme hakkında daha fazla bilgi için bkz: [hello REST API kullanarak özellik Düzenle](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span><span class="sxs-lookup"><span data-stu-id="03ba0-182">For information on editing a property using hello REST API, see [Edit a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="toodelete-a-property"></a><span data-ttu-id="03ba0-183">toodelete özelliği</span><span class="sxs-lookup"><span data-stu-id="03ba0-183">toodelete a property</span></span>
<span data-ttu-id="03ba0-184">toodelete bir özellik tıklatın **silmek** hello özelliği toodelete yanında.</span><span class="sxs-lookup"><span data-stu-id="03ba0-184">toodelete a property, click **Delete** beside hello property toodelete.</span></span>

![Özellik Sil][api-management-properties-delete]

<span data-ttu-id="03ba0-186">Tıklatın **Evet, silmeden** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="03ba0-186">Click **Yes, delete it** tooconfirm.</span></span>

![Silmeyi onayla][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="03ba0-188">Merhaba özelliği hiçbir ilke tarafından başvurulduğunda, bağlanamayacak toosuccessfully silin hello özelliğini kullanan tüm ilkelerden kaldırana kadar.</span><span class="sxs-lookup"><span data-stu-id="03ba0-188">If hello property is referenced by any policies, you will be unable toosuccessfully delete it until you remove hello property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="03ba0-189">Merhaba REST API kullanarak bir özelliği silme hakkında daha fazla bilgi için bkz: [hello REST API kullanarak bir özelliği silmeye](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span><span class="sxs-lookup"><span data-stu-id="03ba0-189">For information on deleting a property using hello REST API, see [Delete a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="toosearch-and-filter-properties"></a><span data-ttu-id="03ba0-190">toosearch ve filtre özellikleri</span><span class="sxs-lookup"><span data-stu-id="03ba0-190">toosearch and filter properties</span></span>
<span data-ttu-id="03ba0-191">Merhaba **özellikleri** sekmesi, arama ve filtreleme yetenekleri toohelp özelliklerinizi yönettiğiniz içerir.</span><span class="sxs-lookup"><span data-stu-id="03ba0-191">hello **Properties** tab includes searching and filtering capabilities toohelp you manage your properties.</span></span> <span data-ttu-id="03ba0-192">özellik adı tarafından toofilter hello özellik listesi hello bir arama terimi girin **arama özelliği** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="03ba0-192">toofilter hello property list by property name, enter a search term in hello **Search property** textbox.</span></span> <span data-ttu-id="03ba0-193">Tüm özellikleri toodisplay temizleyin hello **arama özelliği** textbox ve ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="03ba0-193">toodisplay all properties, clear hello **Search property** textbox and press enter.</span></span>

![Arama][api-management-properties-search]

<span data-ttu-id="03ba0-195">Etiket değerlerine göre toofilter hello özellik listesi hello bir veya daha fazla etiket girin **filtre etiketleriyle** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="03ba0-195">toofilter hello property list by tag values, enter one or more tags into hello **Filter by tags** textbox.</span></span> <span data-ttu-id="03ba0-196">Tüm özellikleri toodisplay temizleyin hello **filtre etiketleriyle** textbox ve ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="03ba0-196">toodisplay all properties, clear hello **Filter by tags** textbox and press enter.</span></span>

![Filtre][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="03ba0-198">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="03ba0-198">Next steps</span></span>
* <span data-ttu-id="03ba0-199">İlkeleri ile çalışma hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="03ba0-199">Learn more about working with policies</span></span>
  * [<span data-ttu-id="03ba0-200">API Management ilkeleri</span><span class="sxs-lookup"><span data-stu-id="03ba0-200">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="03ba0-201">İlke başvurusu</span><span class="sxs-lookup"><span data-stu-id="03ba0-201">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="03ba0-202">İlke ifadeleri</span><span class="sxs-lookup"><span data-stu-id="03ba0-202">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="03ba0-203">Video genel izleyin</span><span class="sxs-lookup"><span data-stu-id="03ba0-203">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Use-Properties-in-Policies/player]
> 
> 

[api-management-properties]: ./media/api-management-howto-properties/api-management-properties.png
[api-management-properties-add-property]: ./media/api-management-howto-properties/api-management-properties-add-property.png
[api-management-properties-edit-property]: ./media/api-management-howto-properties/api-management-properties-edit-property.png
[api-management-properties-add-property-menu]: ./media/api-management-howto-properties/api-management-properties-add-property-menu.png
[api-management-properties-property-saved]: ./media/api-management-howto-properties/api-management-properties-property-saved.png
[api-management-properties-delete]: ./media/api-management-howto-properties/api-management-properties-delete.png
[api-management-properties-edit]: ./media/api-management-howto-properties/api-management-properties-edit.png
[api-management-delete-confirm]: ./media/api-management-howto-properties/api-management-delete-confirm.png
[api-management-properties-search]: ./media/api-management-howto-properties/api-management-properties-search.png
[api-management-send-results]: ./media/api-management-howto-properties/api-management-send-results.png
[api-management-properties-filter]: ./media/api-management-howto-properties/api-management-properties-filter.png
[api-management-api-inspector-trace]: ./media/api-management-howto-properties/api-management-api-inspector-trace.png

