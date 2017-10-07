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
# <a name="how-toouse-properties-in-azure-api-management-policies"></a>Nasıl toouse özelliklerinde Azure API Management ilkeleri
API Management, güçlü bir özellik toochange hello davranışını yapılandırma yoluyla hello API hello publisher izin hello sisteminin ilkelerdir. Merhaba istek üzerinde sırayla yürütülen deyimlerin bir koleksiyon veya bir API yanıtını ilkelerdir. İlke deyimleri metin değerleri, ilke ifadelerini ve özellikleri kullanarak oluşturulabilir. 

Her API Management hizmeti örneği genel toohello hizmet örneği anahtar/değer çiftleri özellikleri koleksiyonu vardır. Bu özellikler, tüm API yapılandırması ve ilkeleri kullanılan toomanage sabit dize değerleri olabilir. Her bir özellik öznitelikleri aşağıdaki hello sahiptir.

| Öznitelik | Tür | Açıklama |
| --- | --- | --- |
| Ad |Dize |Merhaba özelliğinin Hello adı. İçeren yalnızca harf, rakam, nokta, tire ve alt çizgi karakterleri. |
| Değer |Dize |Merhaba özelliğinin Hello değeri. Bunu boş olamaz veya yalnızca boşluktan oluşamaz. |
| Gizli dizi |Boole değeri |Merhaba değeri gizli olmadığından ve veya şifrelenmelidir olup olmadığını belirler. |
| Etiketler |Dize dizisi |İsteğe bağlı etiketleri, sağlandığında kullanılan toofilter hello özellik listesi olabilir. |

Özellikler hello hello yayımcı portalında yapılandırılır **özellikleri** sekmesi. Aşağıdaki örneğine hello üç özellikleri yapılandırılır.

![Özellikler][api-management-properties]

Özellik değerlerini değişmez değer dizeleri içerebilir ve [ilke ifadelerini](https://msdn.microsoft.com/library/azure/dn910913.aspx). Merhaba aşağıdaki tabloda hello önceki üç örnek özelliklerini ve bunların öznitelikleri gösterir. Merhaba değerini `ExpressionProperty` içeren bir dize döndürür bir ilke ifadesi hello geçerli tarih ve saat değil. Merhaba özelliği `ContosoHeaderValue` değerini gösterilmesi için gizlilik olarak işaretlenmiş.

| Ad | Değer | Gizli dizi | Etiketler |
| --- | --- | --- | --- |
| ContosoHeader |İzleme kodu |False |Contoso |
| ContosoHeaderValue |•••••••••••••••••••••• |True |Contoso |
| ExpressionProperty |@(DateTime.Now.ToString()) |False | |

## <a name="toouse-a-property"></a>toouse özelliği
bir çift çift köşeli parantez içinde yer hello özellik adı toouse bir ilke özelliği, ister `{{ContosoHeader}}`hello aşağıdaki örnekte gösterildiği gibi.

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

Bu örnekte, `ContosoHeader` başlığı hello adı olarak kullanılan bir `set-header` İlkesi ve `ContosoHeaderValue` bu başlığı hello değeri olarak kullanılır. Bu ilke bir istek veya yanıt toohello API Yönetimi ağ geçidi sırasında değerlendirildiğinde `{{ContosoHeader}}` ve `{{ContosoHeaderValue}}` ilgili özellik değerlerine ile değiştirilir.

Özellikler tam özniteliği ya da hello önceki örnekte gösterildiği gibi öğesi değerleri olarak kullanılabilir, ancak bunlar da yüklenebilir eklenen veya hello aşağıdaki örnekte gösterildiği gibi bir metin ifadenin bir parçası birleştirilmiş:`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`

Özellikler de ilke ifadelerini içerebilir. Aşağıdaki örneğine hello hello `ExpressionProperty` kullanılır.

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

Bu ilke değerlendirildiğinde `{{ExpressionProperty}}` değeriyle değiştirilir: `@(DateTime.Now.ToString())`. Merhaba değeri bir ilke ifadesi olduğundan hello ifade değerlendirilir ve hello İlkesi yürütülmesinin ile devam eder.

Bu sorunu anlamak hello Geliştirici Portalı'nda özelliklere sahip bir ilke kapsamında olan bir işlem çağırarak test edebilirsiniz. Aşağıdaki örneğine hello hello iki önceki örnekle bir işlem çağrılır `set-header` ilkeleri özelliklere sahip. Merhaba yanıt özelliklere sahip ilkeleri kullanarak yapılandırılmış iki özel üstbilgi içerdiğine dikkat edin.

![Geliştirici portalı][api-management-send-results]

Merhaba bakarsanız [API denetçisi izleme](api-management-howto-api-inspector.md) hello önceki örnek sahip iki ilke özellikleri içeren bir arama hello iki görebilirsiniz `set-header` hello özellik değerlerinin yanı sıra hello İlkesi ifade eklenen ilkeleriyle Değerlendirme hello İlkesi ifade bulunan hello özelliği.

![API denetçisi izleme][api-management-api-inspector-trace]

Özellik değerlerini ilke ifadelerini içerebilir olsa da, özellik değerleri diğer özellikleri içeremez unutmayın. Bir özellik referansı içeren metin gibi bir özellik değeri için kullanılıyorsa, `Property value text {{MyProperty}}`, Özellik Başvurusu değiştirilmesi olmaz ve hello özellik değerinin bir parçası olarak dahil edilir.

## <a name="toocreate-a-property"></a>toocreate özelliği
toocreate bir özellik tıklatın **özellik ekleme** hello üzerinde **özellikleri** sekmesi.

![Özellik ekleme][api-management-properties-add-property-menu]

**Ad** ve **değeri** gerekli değerlerdir. Bu özellik değeri bir gizli anahtarı ise hello denetleyin **bu gizli olmadığından** onay kutusu. Özelliklerinizi düzenleme ile bir veya daha fazla isteğe bağlı etiketleri toohelp girin ve **kaydetmek**.

![Özellik ekleme][api-management-properties-add-property]

Yeni bir özellik kaydedildiğinde hello **arama özelliği** textbox hello hello yeni bir özellik adıyla doldurulur ve hello yeni özellik görüntülenir. Tüm özellikleri toodisplay temizleyin hello **arama özelliği** textbox ve ENTER tuşuna basın.

![Özellikler][api-management-properties-property-saved]

Merhaba REST API kullanarak bir özelliği oluşturma hakkında daha fazla bilgi için bkz: [hello REST API kullanarak özellik oluşturma](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).

## <a name="tooedit-a-property"></a>tooedit özelliği
tooedit bir özellik tıklatın **Düzenle** hello özelliği tooedit yanında.

![Özelliği Düzenle][api-management-properties-edit]

İstediğiniz değişiklikleri yapın ve tıklatın **kaydetmek**. Merhaba özellik adını değiştirirseniz, bu özellik başvuran tüm otomatik olarak güncelleştirilen toouse hello yeni adı ilkelerdir.

![Özelliği Düzenle][api-management-properties-edit-property]

Merhaba REST API kullanarak özellik düzenleme hakkında daha fazla bilgi için bkz: [hello REST API kullanarak özellik Düzenle](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).

## <a name="toodelete-a-property"></a>toodelete özelliği
toodelete bir özellik tıklatın **silmek** hello özelliği toodelete yanında.

![Özellik Sil][api-management-properties-delete]

Tıklatın **Evet, silmeden** tooconfirm.

![Silmeyi onayla][api-management-delete-confirm]

> [!IMPORTANT]
> Merhaba özelliği hiçbir ilke tarafından başvurulduğunda, bağlanamayacak toosuccessfully silin hello özelliğini kullanan tüm ilkelerden kaldırana kadar.
> 
> 

Merhaba REST API kullanarak bir özelliği silme hakkında daha fazla bilgi için bkz: [hello REST API kullanarak bir özelliği silmeye](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).

## <a name="toosearch-and-filter-properties"></a>toosearch ve filtre özellikleri
Merhaba **özellikleri** sekmesi, arama ve filtreleme yetenekleri toohelp özelliklerinizi yönettiğiniz içerir. özellik adı tarafından toofilter hello özellik listesi hello bir arama terimi girin **arama özelliği** metin kutusu. Tüm özellikleri toodisplay temizleyin hello **arama özelliği** textbox ve ENTER tuşuna basın.

![Arama][api-management-properties-search]

Etiket değerlerine göre toofilter hello özellik listesi hello bir veya daha fazla etiket girin **filtre etiketleriyle** metin kutusu. Tüm özellikleri toodisplay temizleyin hello **filtre etiketleriyle** textbox ve ENTER tuşuna basın.

![Filtre][api-management-properties-filter]

## <a name="next-steps"></a>Sonraki adımlar
* İlkeleri ile çalışma hakkında daha fazla bilgi edinin
  * [API Management ilkeleri](api-management-howto-policies.md)
  * [İlke başvurusu](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [İlke ifadeleri](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a>Video genel izleyin
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

