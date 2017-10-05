---
title: "Azure API Management ilkeleri özelliklerini kullanma"
description: "Azure API Management ilkeleri özelliklerini kullanmayı öğrenin."
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
ms.openlocfilehash: 3b0fe2a300038e13cc488bdb4f50f8be270ea8f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-properties-in-azure-api-management-policies"></a><span data-ttu-id="35fa6-103">Azure API Management ilkeleri özelliklerini kullanma</span><span class="sxs-lookup"><span data-stu-id="35fa6-103">How to use properties in Azure API Management policies</span></span>
<span data-ttu-id="35fa6-104">API yönetimi ilkelerini yapılandırma yoluyla API'nin davranışını değiştirmek yayımcının sisteminin güçlü bir özellik var.</span><span class="sxs-lookup"><span data-stu-id="35fa6-104">API Management policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="35fa6-105">İlkeler, bir API isteği veya yanıtı üzerinde sırayla yürütülen deyimlerin bir koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="35fa6-105">Policies are a collection of statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="35fa6-106">İlke deyimleri metin değerleri, ilke ifadelerini ve özellikleri kullanarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="35fa6-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="35fa6-107">Her API Management hizmet örneği için hizmet örneği genel anahtar/değer çiftleri özellikleri koleksiyonu vardır.</span><span class="sxs-lookup"><span data-stu-id="35fa6-107">Each API Management service instance has a properties collection of key/value pairs that are global to the service instance.</span></span> <span data-ttu-id="35fa6-108">Bu özellikler, sabit dize değerlerini tüm API yapılandırması ve ilkeleri yönetmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="35fa6-108">These properties can be used to manage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="35fa6-109">Her bir özellik aşağıdaki özniteliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="35fa6-109">Each property has the following attributes.</span></span>

| <span data-ttu-id="35fa6-110">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="35fa6-110">Attribute</span></span> | <span data-ttu-id="35fa6-111">Tür</span><span class="sxs-lookup"><span data-stu-id="35fa6-111">Type</span></span> | <span data-ttu-id="35fa6-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="35fa6-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="35fa6-113">Ad</span><span class="sxs-lookup"><span data-stu-id="35fa6-113">Name</span></span> |<span data-ttu-id="35fa6-114">Dize</span><span class="sxs-lookup"><span data-stu-id="35fa6-114">string</span></span> |<span data-ttu-id="35fa6-115">Özelliğin adı.</span><span class="sxs-lookup"><span data-stu-id="35fa6-115">The name of the property.</span></span> <span data-ttu-id="35fa6-116">İçeren yalnızca harf, rakam, nokta, tire ve alt çizgi karakterleri.</span><span class="sxs-lookup"><span data-stu-id="35fa6-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="35fa6-117">Değer</span><span class="sxs-lookup"><span data-stu-id="35fa6-117">Value</span></span> |<span data-ttu-id="35fa6-118">Dize</span><span class="sxs-lookup"><span data-stu-id="35fa6-118">string</span></span> |<span data-ttu-id="35fa6-119">Özelliğin değeri.</span><span class="sxs-lookup"><span data-stu-id="35fa6-119">The value of the property.</span></span> <span data-ttu-id="35fa6-120">Bunu boş olamaz veya yalnızca boşluktan oluşamaz.</span><span class="sxs-lookup"><span data-stu-id="35fa6-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="35fa6-121">Gizli dizi</span><span class="sxs-lookup"><span data-stu-id="35fa6-121">Secret</span></span> |<span data-ttu-id="35fa6-122">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="35fa6-122">boolean</span></span> |<span data-ttu-id="35fa6-123">Değer bir parolası ve veya şifrelenmelidir olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="35fa6-123">Determines whether the value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="35fa6-124">Etiketler</span><span class="sxs-lookup"><span data-stu-id="35fa6-124">Tags</span></span> |<span data-ttu-id="35fa6-125">Dize dizisi</span><span class="sxs-lookup"><span data-stu-id="35fa6-125">array of string</span></span> |<span data-ttu-id="35fa6-126">İsteğe bağlı etiketleri, sağlandığında özellik listesini filtrelemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="35fa6-126">Optional tags that when provided can be used to filter the property list.</span></span> |

<span data-ttu-id="35fa6-127">Özellikleri yapılandırılır yayımcı portalında **özellikleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="35fa6-127">Properties are configured in the publisher portal on the **Properties** tab.</span></span> <span data-ttu-id="35fa6-128">Aşağıdaki örnekte, üç özellikleri yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="35fa6-128">In the following example, three properties are configured.</span></span>

![Özellikler][api-management-properties]

<span data-ttu-id="35fa6-130">Özellik değerlerini değişmez değer dizeleri içerebilir ve [ilke ifadelerini](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span><span class="sxs-lookup"><span data-stu-id="35fa6-130">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="35fa6-131">Aşağıdaki tabloda, önceki üç örnek özelliklerini ve onların öznitelikleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="35fa6-131">The following table shows the previous three sample properties and their attributes.</span></span> <span data-ttu-id="35fa6-132">Değeri `ExpressionProperty` geçerli tarih ve saati içeren bir dize döndürür bir ilke ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="35fa6-132">The value of `ExpressionProperty` is a policy expression that returns a string containing the current date and time.</span></span> <span data-ttu-id="35fa6-133">Özellik `ContosoHeaderValue` değerini gösterilmesi için gizlilik olarak işaretlenmiş.</span><span class="sxs-lookup"><span data-stu-id="35fa6-133">The property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="35fa6-134">Ad</span><span class="sxs-lookup"><span data-stu-id="35fa6-134">Name</span></span> | <span data-ttu-id="35fa6-135">Değer</span><span class="sxs-lookup"><span data-stu-id="35fa6-135">Value</span></span> | <span data-ttu-id="35fa6-136">Gizli dizi</span><span class="sxs-lookup"><span data-stu-id="35fa6-136">Secret</span></span> | <span data-ttu-id="35fa6-137">Etiketler</span><span class="sxs-lookup"><span data-stu-id="35fa6-137">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="35fa6-138">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="35fa6-138">ContosoHeader</span></span> |<span data-ttu-id="35fa6-139">İzleme kodu</span><span class="sxs-lookup"><span data-stu-id="35fa6-139">TrackingId</span></span> |<span data-ttu-id="35fa6-140">False</span><span class="sxs-lookup"><span data-stu-id="35fa6-140">False</span></span> |<span data-ttu-id="35fa6-141">Contoso</span><span class="sxs-lookup"><span data-stu-id="35fa6-141">Contoso</span></span> |
| <span data-ttu-id="35fa6-142">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="35fa6-142">ContosoHeaderValue</span></span> |<span data-ttu-id="35fa6-143">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="35fa6-143">••••••••••••••••••••••</span></span> |<span data-ttu-id="35fa6-144">True</span><span class="sxs-lookup"><span data-stu-id="35fa6-144">True</span></span> |<span data-ttu-id="35fa6-145">Contoso</span><span class="sxs-lookup"><span data-stu-id="35fa6-145">Contoso</span></span> |
| <span data-ttu-id="35fa6-146">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="35fa6-146">ExpressionProperty</span></span> |<span data-ttu-id="35fa6-147">@(DateTime.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="35fa6-147">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="35fa6-148">False</span><span class="sxs-lookup"><span data-stu-id="35fa6-148">False</span></span> | |

## <a name="to-use-a-property"></a><span data-ttu-id="35fa6-149">Bir özelliği kullanmak için</span><span class="sxs-lookup"><span data-stu-id="35fa6-149">To use a property</span></span>
<span data-ttu-id="35fa6-150">Bir ilke özelliği kullanmak için özellik adı gibi küme ayraçları çift çifti içinde yerleştirin `{{ContosoHeader}}`, aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="35fa6-150">To use a property in a policy, place the property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in the following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="35fa6-151">Bu örnekte, `ContosoHeader` bir üstbilgi adı olarak kullanılan bir `set-header` İlkesi ve `ContosoHeaderValue` Bu üstbilgi değeri olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="35fa6-151">In this example, `ContosoHeader` is used as the name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as the value of that header.</span></span> <span data-ttu-id="35fa6-152">Bu ilke bir istek veya yanıt API Yönetimi ağ geçidi olarak sırasında değerlendirildiğinde `{{ContosoHeader}}` ve `{{ContosoHeaderValue}}` ilgili özellik değerlerine ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="35fa6-152">When this policy is evaluated during a request or response to the API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="35fa6-153">Özellikler tam özniteliği ya da önceki örnekte gösterildiği gibi öğesi değerleri olarak kullanılabilir, ancak bunlar eklenen ya da aşağıdaki örnekte gösterildiği gibi bir metin ifadenin parçası birlikte:`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="35fa6-153">Properties can be used as complete attribute or element values as shown in the previous example, but they can also be inserted into or combined with part of a literal text expression as shown in the following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="35fa6-154">Özellikler de ilke ifadelerini içerebilir.</span><span class="sxs-lookup"><span data-stu-id="35fa6-154">Properties can also contain policy expressions.</span></span> <span data-ttu-id="35fa6-155">Aşağıdaki örnekte, `ExpressionProperty` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="35fa6-155">In the following example, the `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="35fa6-156">Bu ilke değerlendirildiğinde `{{ExpressionProperty}}` değeriyle değiştirilir: `@(DateTime.Now.ToString())`.</span><span class="sxs-lookup"><span data-stu-id="35fa6-156">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="35fa6-157">Değer bir ilke ifadesi olduğundan ifade değerlendirilir ve ilke yürütülmesinin ile devam eder.</span><span class="sxs-lookup"><span data-stu-id="35fa6-157">Since the value is a policy expression, the expression is evaluated and the policy proceeds with its execution.</span></span>

<span data-ttu-id="35fa6-158">Özelliklere sahip bir ilke kapsamında olan bir işlem çağırarak bu çıkış Geliştirici Portalı'nda test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35fa6-158">You can test this out in the developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="35fa6-159">Aşağıdaki örnekte, bir işlem iki önceki örnekle çağrılır `set-header` ilkeleri özelliklere sahip.</span><span class="sxs-lookup"><span data-stu-id="35fa6-159">In the following example, an operation is called with the two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="35fa6-160">Yanıt özellikleri ile ilkelerini kullanarak yapılandırılmış iki özel üstbilgi içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="35fa6-160">Note that the response contains two custom headers that were configured using policies with properties.</span></span>

![Geliştirici portalı][api-management-send-results]

<span data-ttu-id="35fa6-162">Bakarsanız [API denetçisi izleme](api-management-howto-api-inspector.md) iki önceki örnek ilkeleriyle özellikleri içeren bir arama iki görebilirsiniz `set-header` ilke ifadesi bulunan bir özellik için ilke ifade değerlendirmesi yanı sıra eklenen özellik değerlerini ilkeleriyle.</span><span class="sxs-lookup"><span data-stu-id="35fa6-162">If you look at the [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes the two previous sample policies with properties, you can see the two `set-header` policies with the property values inserted as well as the policy expression evaluation for the property that contained the policy expression.</span></span>

![API denetçisi izleme][api-management-api-inspector-trace]

<span data-ttu-id="35fa6-164">Özellik değerlerini ilke ifadelerini içerebilir olsa da, özellik değerleri diğer özellikleri içeremez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="35fa6-164">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="35fa6-165">Bir özellik referansı içeren metin gibi bir özellik değeri için kullanılıyorsa, `Property value text {{MyProperty}}`, bu özellik başvurusu değiştirilmesi olmaz ve özellik değerinin bir parçası olarak dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="35fa6-165">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of the property value.</span></span>

## <a name="to-create-a-property"></a><span data-ttu-id="35fa6-166">Bir özellik oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="35fa6-166">To create a property</span></span>
<span data-ttu-id="35fa6-167">Bir özellik oluşturmak için tıklatın **özellik ekleme** üzerinde **özellikleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="35fa6-167">To create a property, click **Add property** on the **Properties** tab.</span></span>

![Özellik ekleme][api-management-properties-add-property-menu]

<span data-ttu-id="35fa6-169">**Ad** ve **değeri** gerekli değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="35fa6-169">**Name** and **Value** are required values.</span></span> <span data-ttu-id="35fa6-170">Bu özellik değeri bir gizli anahtarı ise denetleyin **bu gizli olmadığından** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="35fa6-170">If this property value is a secret, check the **This is a secret** checkbox.</span></span> <span data-ttu-id="35fa6-171">Özelliklerinizi düzenleme ile yardımcı olmak için bir veya daha fazla isteğe bağlı etiketleri girin ve **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="35fa6-171">Enter one or more optional tags to help with organizing your properties, and click **Save**.</span></span>

![Özellik ekleme][api-management-properties-add-property]

<span data-ttu-id="35fa6-173">Yeni bir özellik kaydedildiğinde **arama özelliği** metin kutusuna yeni özellik adı ile doldurulur ve yeni özellik görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="35fa6-173">When a new property is saved, the **Search property** textbox is populated with the name of the new property and the new property is displayed.</span></span> <span data-ttu-id="35fa6-174">Tüm özellikleri görüntülemek için temizleyin **arama özelliği** textbox ve ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="35fa6-174">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![Özellikler][api-management-properties-property-saved]

<span data-ttu-id="35fa6-176">REST API kullanarak bir özelliği oluşturma hakkında daha fazla bilgi için bkz: [REST API kullanarak özellik oluşturma](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span><span class="sxs-lookup"><span data-stu-id="35fa6-176">For information on creating a property using the REST API, see [Create a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="to-edit-a-property"></a><span data-ttu-id="35fa6-177">Bir özellik düzenlemek için</span><span class="sxs-lookup"><span data-stu-id="35fa6-177">To edit a property</span></span>
<span data-ttu-id="35fa6-178">Bir özellik düzenlemek için tıklatın **Düzenle** düzenlemek için özellik yanında.</span><span class="sxs-lookup"><span data-stu-id="35fa6-178">To edit a property, click **Edit** beside the property to edit.</span></span>

![Özelliği Düzenle][api-management-properties-edit]

<span data-ttu-id="35fa6-180">İstediğiniz değişiklikleri yapın ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="35fa6-180">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="35fa6-181">Özellik adını değiştirirseniz, bu özellik başvuru ilkeleri yeni bir ad kullanmak için otomatik olarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="35fa6-181">If you change the property name, any policies that reference that property are automatically updated to use the new name.</span></span>

![Özelliği Düzenle][api-management-properties-edit-property]

<span data-ttu-id="35fa6-183">REST API kullanarak bir özellik düzenleme hakkında daha fazla bilgi için bkz: [REST API kullanarak bir özelliği Düzenle](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span><span class="sxs-lookup"><span data-stu-id="35fa6-183">For information on editing a property using the REST API, see [Edit a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="to-delete-a-property"></a><span data-ttu-id="35fa6-184">Bir özelliği silmek için</span><span class="sxs-lookup"><span data-stu-id="35fa6-184">To delete a property</span></span>
<span data-ttu-id="35fa6-185">Bir özellik silmek için tıklatın **silmek** silmek için özellik yanında.</span><span class="sxs-lookup"><span data-stu-id="35fa6-185">To delete a property, click **Delete** beside the property to delete.</span></span>

![Özellik Sil][api-management-properties-delete]

<span data-ttu-id="35fa6-187">Tıklatın **Evet, silmeden** onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="35fa6-187">Click **Yes, delete it** to confirm.</span></span>

![Silmeyi onayla][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="35fa6-189">Özellik hiçbir ilke tarafından başvurulduğunda başarıyla özelliğini kullanan tüm ilkelerden kaldırana kadar silemiyor olacaktır.</span><span class="sxs-lookup"><span data-stu-id="35fa6-189">If the property is referenced by any policies, you will be unable to successfully delete it until you remove the property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="35fa6-190">REST API kullanarak bir özelliği silmeye hakkında daha fazla bilgi için bkz: [REST API kullanarak bir özelliği silmeye](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span><span class="sxs-lookup"><span data-stu-id="35fa6-190">For information on deleting a property using the REST API, see [Delete a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="to-search-and-filter-properties"></a><span data-ttu-id="35fa6-191">Arama ve filtreleme için özellikleri</span><span class="sxs-lookup"><span data-stu-id="35fa6-191">To search and filter properties</span></span>
<span data-ttu-id="35fa6-192">**Özellikleri** sekmesi, arama ve filtreleme özelliklerinizi yönetmenize yardımcı olmak için özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="35fa6-192">The **Properties** tab includes searching and filtering capabilities to help you manage your properties.</span></span> <span data-ttu-id="35fa6-193">Özellik listesi özellik adına göre filtre uygulamak için bir arama terimi girmeniz **arama özelliği** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="35fa6-193">To filter the property list by property name, enter a search term in the **Search property** textbox.</span></span> <span data-ttu-id="35fa6-194">Tüm özellikleri görüntülemek için temizleyin **arama özelliği** textbox ve ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="35fa6-194">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![Arama][api-management-properties-search]

<span data-ttu-id="35fa6-196">Özellik listesi etiket değerlerine göre filtre uygulamak için bir veya daha fazla etiket içine girin **filtre etiketleriyle** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="35fa6-196">To filter the property list by tag values, enter one or more tags into the **Filter by tags** textbox.</span></span> <span data-ttu-id="35fa6-197">Tüm özellikleri görüntülemek için temizleyin **filtre etiketleriyle** textbox ve ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="35fa6-197">To display all properties, clear the **Filter by tags** textbox and press enter.</span></span>

![Filtre][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="35fa6-199">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="35fa6-199">Next steps</span></span>
* <span data-ttu-id="35fa6-200">İlkeleri ile çalışma hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="35fa6-200">Learn more about working with policies</span></span>
  * [<span data-ttu-id="35fa6-201">API Management ilkeleri</span><span class="sxs-lookup"><span data-stu-id="35fa6-201">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="35fa6-202">İlke başvurusu</span><span class="sxs-lookup"><span data-stu-id="35fa6-202">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="35fa6-203">İlke ifadeleri</span><span class="sxs-lookup"><span data-stu-id="35fa6-203">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="35fa6-204">Video genel izleyin</span><span class="sxs-lookup"><span data-stu-id="35fa6-204">Watch a video overview</span></span>
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

