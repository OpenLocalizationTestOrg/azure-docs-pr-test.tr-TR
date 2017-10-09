---
title: Azure API Management'te aaaPolicies | Microsoft Docs
description: "Nasıl toocreate, düzenlemek ve API yönetimi ilkelerini yapılandırma öğrenin."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 537e5caf-708b-430e-a83f-72b70af28aa9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 9ab0f884a655004cb10c05085034df1795f512e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="policies-in-azure-api-management"></a>Azure API Management ilkeleri
Azure API Management'te hello publisher toochange hello davranışını yapılandırma yoluyla hello API izin hello sisteminin güçlü bir özellik ilkelerdir. Merhaba istek üzerinde sırayla yürütülen deyimlerin bir koleksiyon veya bir API yanıtını ilkelerdir. Sık kullanılan deyimler XML tooJSON biçimi dönüştürme içerir ve bir geliştiriciden gelen çağrıların toorestrict hello miktarını sınırlamak oranı çağırın. Çok daha fazla ilke hello kutu dışı kullanılabilir.

Merhaba bkz [İlkesi başvurusu] [ Policy Reference] ilke deyimleri ve ayarlarının tam listesi için.

İlkeler, yönetilen hello API hello API tüketici arasında bulunur hello ağ geçidi içinde uygulanır. Merhaba ağ geçidi tüm istekleri alır ve bunları değiştirilmemiş genellikle iletir API temel toohello. Ancak bir ilke değişiklikleri tooboth hello gelen istek ve giden yanıt uygulayabilirsiniz.

Merhaba ilke aksini belirtmedikçe ilke ifadelerini öznitelik değerleri ya da metin değerleri hello API Management ilkeleri olarak kullanılabilir. Hello gibi bazı ilkeler [kontrol akışı] [ Control flow] ve [değişken Ayarla] [ Set variable] ilkeler ilke ifadelerini temel alarak. Daha fazla bilgi için bkz: [ilkeleri Gelişmiş] [ Advanced policies] ve [ilke ifadelerini][Policy expressions].

## <a name="scopes"></a>Nasıl tooconfigure ilkeleri
Genel veya hello kapsamını ilkeleri yapılandırılabilir bir [ürün][Product], [API] [ API] veya [işlemi] [Operation]. bir ilke tooconfigure toohello ilkeleri Düzenleyicisi'nde hello yayımcı portalına gidin.

![İlkeleri menüsü][policies-menu]

Merhaba ilkeleri Düzenleyicisi üç ana bölümden oluşur: Merhaba burada ilkeleri düzenlenmesi (soldaki) ve hello deyimleri listesinde (sağdaki) ilke kapsamı (üst) hello İlkesi tanımı:

![İlke Düzenleyicisi][policies-editor]

önce hangi hello İlkesi uygulamalıdır hello kapsam seçmeniz gerekir. bir ilke yapılandırma toobegin. Merhaba ekran görüntüsü aşağıda hello **Starter** ürün seçilidir. Bu hello kare simgesi sonraki toohello ilkesi adı bir ilke zaten bu düzeyde uygulandığını gösterir unutmayın.

![Kapsam][policies-scope]

Bir ilke uygulanmış olduğundan, hello yapılandırma hello tanımı görünümünde gösterilir.

![Yapılandırma][policies-configure]

salt okunur Hello İlkesi görüntülenen ilk. Sipariş tooedit hello tanımı tıklatın hello **ilkesini yapılandırma** eylem.

![Düzenle][policies-edit]

Merhaba ilke tanımı gelen ve giden ifadeler tanımlayan basit bir XML dosyasıdır. doğrudan hello tanımı penceresinde Hello XML düzenlenebilir. Deyimleri listesini sağ toohello ve deyimleri geçerli toohello geçerli kapsam etkin ve vurgulanmış sağlanır; Merhaba tarafından gösterildiği gibi **çağrı hızını sınırla** hello ekran yukarıdaki deyiminde.

Etkin bir deyimi tıklatarak ekleyecek hello imlecin hello tanımı görünümünde hello konumda uygun XML hello. 

> [!NOTE]
> Tooadd istediğiniz hello ilkesi etkin değilse, bu ilkeye hello doğru kapsamında olduğundan emin olun. Her ilke bildirimi, bazı kapsamlar ve ilke bölümler kullanılmak üzere tasarlanmıştır. tooreview hello İlkesi bölümler için bir ilke kapsamı denetleyip hello **kullanım** bölüm hello söz konusu ilkenin [İlkesi başvurusu][Policy Reference].
> 
> 

İlke deyimleri tam listesi ve ayarlarına hello kullanılabilir [İlkesi başvurusu][Policy Reference].

Örneğin, toospecified IP adreslerini tooadd yeni bir deyim toorestrict gelen istekleri, yalnızca hello Merhaba içeriğine içinde hello imleci `inbound` XML öğesi ve tıklatın hello **sınırla çağıran IP'leri** deyimi.

![Kısıtlama ilkeleri][policies-restrict]

Bu bir XML parçacığını toohello ekler `inbound` öğesi nasıl tooconfigure hello üzerinde deyimi rehberlik sağlar.

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

toolimit istekleri Gelen ve kabul yalnızca bir IP adresinden, 1.2.3.4 hello XML aşağıdaki gibi değiştirin:

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Kaydet][policies-save]

Tamamlandığında hello deyimleri hello ilkesi için yapılandırma, tıklayın **kaydetmek** ve hello değişiklikleri yayılan toohello API Yönetimi ağ geçidi hemen.

## <a name="sections"></a>Anlama ilkesi yapılandırma
Bir ilke için bir istek ve yanıt sırayla yürütmek deyimleri dizisidir. Merhaba yapılandırma bölündüğü uygun şekilde `inbound`, `backend`, `outbound`, ve `on-error` bölümler hello yapılandırma aşağıdaki gösterildiği gibi.

```xml
<policies>
  <inbound>
    <!-- statements toobe applied toohello request go here -->
  </inbound>
  <backend>
    <!-- statements toobe applied before hello request is forwarded too
         hello backend service go here -->
  </backend>
  <outbound>
    <!-- statements toobe applied toohello response go here -->
  </outbound>
  <on-error>
    <!-- statements toobe applied if there is an error condition go here -->
  </on-error>
</policies> 
```

Merhaba bir isteğin işlenmesi sırasında bir hata varsa, tüm kalan hello adımları `inbound`, `backend`, veya `outbound` bölümleri atlanır ve yürütme atlar hello toohello deyimlerinde `on-error` bölümü. Hello İlkesi deyimleri yerleştirerek `on-error` gözden geçirebileceğiniz hello hata hello kullanarak bölüm `context.LastError` özelliği, inceleyin ve hello kullanarak hello hata yanıtı özelleştirme `set-body` İlkesi ve bir hata oluşursa ne olacağını yapılandırın. Hata kodları yerleşik adımları ve ilke deyimleri hello işlenmesi sırasında oluşabilecek hatalar için vardır. Daha fazla bilgi için bkz: [hata API Management ilkeleri işleme](https://msdn.microsoft.com/library/azure/mt629506.aspx).

İlkeleri farklı düzeylerde (Genel, ürün, API ve işlem) belirtilebilir beri hello yapılandırma yolu sizin için toospecify hello sipariş hello ilke tanımının deyimlerini saygı toohello üst ilkesiyle yürütmek sağlar. 

İlke kapsamları sırasının hello değerlendirilir.

1. Genel kapsamlı
2. Ürün kapsamı
3. API kapsamı
4. İşlem kapsamı

Merhaba deyimleri bunları içinde hello toohello yerleşimini göre değerlendirilir `base` varsa, öğesi. Genel ilke sahip hiç üst İlkesi ve hello kullanarak `<base>` öğesi içindeki etkisi yoktur.

Merhaba genel düzeyinde ve bir API için yapılandırılmış bir ilke bir ilke varsa, API'nin kullanıldığı her Örneğin, ardından her iki ilke uygulanır. API Management belirleyici hello temel öğe aracılığıyla birleşik İlkesi deyimlerinin sıralama için sağlar. 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

Merhaba örnek ilke tanımı'nda yukarıdaki, hello `cross-domain` deyimini yürütün, sırayla misiniz tüm yüksek ilkeleri uyulması önce hello tarafından `find-and-replace` ilkesi. 

hello İlkesi Düzenleyicisi'nde hello geçerli kapsamdaki toosee hello ilkeleri **yeniden hesapla seçili kapsam için etkin ilke**.

## <a name="next-steps"></a>Sonraki adımlar
İlke ifadelerini temel video aşağıdaki çıkışı denetleyin.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Policy Reference]: api-management-policy-reference.md
[Product]: api-management-howto-add-products.md
[API]: api-management-howto-add-products.md#add-apis 
[Operation]: api-management-howto-add-operations.md

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx

[policies-menu]: ./media/api-management-howto-policies/api-management-policies-menu.png
[policies-editor]: ./media/api-management-howto-policies/api-management-policies-editor.png
[policies-scope]: ./media/api-management-howto-policies/api-management-policies-scope.png
[policies-configure]: ./media/api-management-howto-policies/api-management-policies-configure.png
[policies-edit]: ./media/api-management-howto-policies/api-management-policies-edit.png
[policies-restrict]: ./media/api-management-howto-policies/api-management-policies-restrict.png
[policies-save]: ./media/api-management-howto-policies/api-management-policies-save.png
