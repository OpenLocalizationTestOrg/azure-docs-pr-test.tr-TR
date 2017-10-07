---
title: "hello Azure AD grafik API'si için aaaQuickstart | Microsoft Docs"
description: "Hello Azure Active Directory grafik API'sini OData REST API uç noktaları yoluyla programlı erişim tooAzure AD sağlar. Uygulamalar hello grafik API'si tooperform kullanabilir oluşturma, okuma, güncelleştirme ve (CRUD) işlemleridir dizin verileri ve nesneleri silme."
services: active-directory
documentationcenter: n/a
author: viv-liu
manager: mbaldwin
editor: 
tags: 
ms.assetid: 9dc268a9-32e8-402c-a43f-02b183c295c5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: viviali
ms.custom: aaddev
ms.openlocfilehash: b4d3c57f06d212b1d095578f19bb86c932dbcc33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-hello-azure-ad-graph-api"></a>Hello Azure AD grafik API'si için hızlı başlangıç
Hello Azure Active Directory (AD) grafik API'si OData REST API uç noktaları yoluyla programlı erişim tooAzure AD sağlar. Uygulamalar hello grafik API'si tooperform kullanabilir oluşturma, okuma, güncelleştirme ve (CRUD) işlemleridir dizin verileri ve nesneleri silme. Örneğin, hello grafik API'si toocreate yeni bir kullanıcı görünümü kullanın veya kullanıcının özelliklerini güncelleştirmek, kullanıcı parolasını değiştirmeniz, yapabilirsiniz rol tabanlı erişim, devre dışı bırakma veya silme hello kullanıcı grubu üyeliğini kontrol edin. Merhaba grafik API'si özellikler ve uygulama senaryoları hakkında daha fazla bilgi için bkz: [Azure AD Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) ve [Azure AD Graph API Önkoşullar](https://msdn.microsoft.com/library/hh974476.aspx). 

> [!IMPORTANT]
> Kullanmanız önerilir [Microsoft Graph](https://developer.microsoft.com/graph) Azure AD Graph API tooaccess Azure Active Directory kaynakları yerine. Geliştirme çalışmalarımız şu anda Microsoft Graph üzerine yoğunlaşmıştır ve Azure AD Grafik API'si için başka bir geliştirme planlanmamaktadır. Senaryolar için Azure AD Graph API hala uygun olabilir, çok sınırlı sayıda vardır; Merhaba daha fazla bilgi için bkz: [Microsoft Graph veya hello Azure AD grafik](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) hello Office Geliştirici Merkezi blog postasına.
> 
> 

## <a name="how-tooconstruct-a-graph-api-url"></a>Nasıl tooconstruct bir grafik API'si URL
Grafik API'si, tooaccess dizin verileri ve tooperform CRUD işlemleri karşı istediğiniz nesneleri (diğer bir deyişle, kaynakları veya varlıklar), açık veri (OData) protokolü hello üzerinde göre URL'leri kullanabilirsiniz. Merhaba grafik API'si kullanılan URL'leri dört ana bölümden oluşur: hizmet kök, Kiracı tanıtıcısı, kaynak yol ve sorgu dizesi seçenekleri: `https://graph.windows.net/{tenant-identifier}/{resource-path}?[query-parameters]`. URL aşağıdaki hello Hello örneği ele: `https://graph.windows.net/contoso.com/groups?api-version=1.6`.

* **Hizmet kök**: Azure AD Graph API, hello hizmeti her zaman https://graph.windows.net köküdür.
* **Kiracı tanımlayıcı**: Bu bölümde doğrulanmış (kayıtlı) etki alanı adının, örnek, önceki hello olabilir contoso.com. Bu aynı zamanda bir kiracı nesne kimliği veya hello "myorganization" veya "benim" diğer adı olabilir. Daha fazla bilgi için bkz: [adresleme varlıkları ve hello grafik API'si işlemlerinde](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-operations-overview)).
* **Kaynak yolu**: hello kaynağı bir URL bu bölümünü tanımlayan toobe kurduğunda (kullanıcılar, gruplar, belirli bir kullanıcı veya bir özel grup, vb. ile) Merhaba yukarıdaki örnekte, kaynak ayarlanmış hello üst düzey "gruplarını" tooaddress değil. Örneğin belirli bir varlık karşılayabilirsiniz "kullanıcılar / {objectID}" veya "kullanıcıların/userPrincipalName".
* **Sorgu parametreleri**: hello kaynak yolu bölümü hello sorgu parametreleri bölümünden bir soru işareti (?) ayırır. Merhaba "api-version" sorgu parametresi hello grafik API'si de tüm istekler gereklidir. Merhaba grafik API'si de OData sorgu seçeneklerini aşağıdaki hello destekler: **$filter**, **$orderby**, **$expand**, **$top**ve **$format**. Sorgu seçenekleri aşağıdaki hello şu anda desteklenmemektedir: **$count**, **$inlinecount**, ve **$skip**. Daha fazla bilgi için bkz: [desteklenen sorguları, filtreleri ve Azure AD Graph API disk belleği seçeneklerinde](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options).

## <a name="graph-api-versions"></a>Grafik API'si sürümleri
Bir grafik API'si isteği için hello sürüm hello "api-version" sorgu parametresi belirtin. 1.5 ve daha sonraki sürümü için bir sayısal sürüm değeri kullanın; API sürümü 1.6 =. Önceki sürümler için toohello biçimi YYYY-AA-GG aynılarını bir tarih dizesi kullanın; Örneğin, API sürümü 2013-11-08 =. Merhaba dizesi "beta"; Önizleme özellikleri için kullanın Örneğin, API sürümü beta =. Grafik API'si sürümleri arasındaki farklar hakkında daha fazla bilgi için bkz: [Azure AD Graph API sürümü oluşturma](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-versioning).

## <a name="graph-api-metadata"></a>Grafik API'si meta verileri
tooreturn hello grafik API'si meta veri dosyası, Ekle "$metadata" Merhaba segment hello Kiracı tanımlayıcı hello URL için örnekte, sonra hello URL döndürür meta verilerinin bir tanıtım şirket için aşağıdaki: `https://graph.windows.net/GraphDir1.OnMicrosoft.com/$metadata?api-version=1.6`. Bu URL bir web tarayıcısı toosee hello meta verilerin adres çubuğuna hello girebilirsiniz. Merhaba döndürülen CSDL meta veri belgesi hello varlıkları ve karmaşık türler, özelliklerini ve hello işlevleri ve grafik API'si, istenen hello sürümü tarafından kullanıma sunulan eylemleri açıklar. Merhaba api-version parametresi atlama hello en son sürüm için meta verileri döndürür.

## <a name="common-queries"></a>Genel sorgular
[Azure AD Graph API Genel sorgular](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-supported-queries-filters-and-paging-options#CommonQueries) hello kullanılan tooaccess en üst düzey dizin ve sorguları tooperform işlemlerinizin dizininizde kaynaklarında olabilir sorguları da dahil, Azure AD grafik ile kullanılan genel sorgular listeler.

Örneğin, `https://graph.windows.net/contoso.com/tenantDetails?api-version=1.6` döndürür şirket bilgileri dizin contoso.com.

Veya `https://graph.windows.net/contoso.com/users?api-version=1.6` hello contoso.com directory tüm kullanıcı nesneleri listeler.

## <a name="using-hello-graph-explorer"></a>Merhaba Graph Explorer'a kullanma
Uygulamanızı oluşturmak gibi hello Graph Explorer'a hello Azure AD Graph API tooquery hello dizin verilerini kullanabilirsiniz.

Merhaba, toonavigate toohello Graph Explorer'a olup olmadığını görmek, oturum açın ve girin hello çıkışı aşağıdadır `https://graph.windows.net/GraphDir1.OnMicrosoft.com/users?api-version=1.6` tüm kullanıcılar hello toodisplay hello oturum açmış olan kullanıcının dizini:

![Azure AD grafik api'si Gezgini](./media/active-directory-graph-api-quickstart/graph_explorer.png)

**Yük hello Graph Explorer'a**: tooload hello aracı, çok gidin[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/). Tıklatın **oturum açma** ve kiracınız karşı Graph Explorer'a hello ile oturum açma, Azure AD hesabının kimlik bilgilerini toorun. Kendi Kiracı karşı Graph Explorer'a çalıştırırsanız, oturum açma sırasında tooconsent siz veya yöneticiniz gerekir. Bir Office 365 aboneliğiniz varsa, otomatik olarak Azure AD kiracısı gerekir. Merhaba kimlik tooOffice 365 toosign kullanın, aslında, Azure AD hesapları ve bu kimlik bilgileri grafik Explorer ile birlikte kullanabilirsiniz.

**Bir sorgu çalıştırın**: toorun bir sorgu yazın sorgunuzu hello isteği metin kutusu ve tıklatın **almak** veya hello **girin** anahtarı. Merhaba sonuçlar hello yanıt kutusunda görüntülenir. Örneğin, `https://graph.windows.net/myorganization/groups?api-version=1.6` hello oturum açmış kullanıcının dizininde tüm Grup nesnelerini listeler.

Not hello aşağıdaki özellikler ve hello Graph Explorer'a sınırlamaları:

* Kaynak üzerinde otomatik tamamlama özelliğini ayarlar. Bu işlevsellik, hello tıklatın toosee (Merhaba şirket URL'si göründüğü) metin kutusu isteyin. Merhaba açılır listeden ayarlanmış bir kaynak seçebilirsiniz.
* Destekler "benim" ve "diğer adlar adresleme myorganization" Merhaba. Örneğin, kullanabileceğiniz `https://graph.windows.net/me?api-version=1.6` tooreturn hello kullanıcı hello oturum açmış kullanıcı nesnesinin veya `https://graph.windows.net/myorganization/users?api-version=1.6` tooreturn hello geçerli dizindeki tüm kullanıcılar.
* Yanıt Üstbilgileri bölümü. Bu bölümde kullanılan toohelp sorgu çalıştırırken ortaya çıkan sorunları giderme.
* Genişletme ve daraltma özellikleriyle hello yanıt için bir JSON Görüntüleyici.
* Küçük resim fotoğrafı görüntüleme için destek yok.

## <a name="using-fiddler-toowrite-toohello-directory"></a>Fiddler toowrite toohello directory kullanma
Bu Hızlı Başlangıç Kılavuzu Hello amaçlarıyla 'yazma işlemlerinin Azure AD dizininizi karşı' gerçekleştirme hello Fiddler Web hata ayıklayıcı toopractice kullanabilirsiniz. Daha fazla bilgi ve tooinstall Fiddler için bkz: [http://www.telerik.com/fiddler](http://www.telerik.com/fiddler).

Merhaba aşağıdaki örnekte, Azure AD dizininizi Fiddler Web hata ayıklayıcı toocreate yeni bir güvenlik grubu 'MyTestGroup' kullanın.

**Bir erişim belirteci edinmek**: Azure AD grafik tooaccess istemcileridir gerekli toosuccessfully tooAzure AD ilk kimlik doğrulaması. Daha fazla bilgi için bkz: [Azure AD için kimlik doğrulama senaryoları](active-directory-authentication-scenarios.md).

**Oluşturma ve bir sorgu çalıştırın**: aşağıdaki adımları tam hello:

1. Fiddler Web hata ayıklayıcı açın ve toohello geçiş **Oluşturucu** sekmesi.
2. Yeni bir güvenlik grubu toocreate istediğinden seçin **Post** HTTP yöntemini hello aşağı açılır menüden hello gibi. Bir grup nesnesi işlemleri ve izinleri hakkında daha fazla bilgi için bkz: [grup](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#GroupEntity) hello içinde [Azure AD Graph REST API Başvurusu](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).
3. Sonraki Hello alan çok**Post**, istek URL'si hello gibi hello aşağıdakileri yazın: `https://graph.windows.net/mytenantdomain/groups?api-version=1.6`.
   
   > [!NOTE]
   > Merhaba etki alanı adıyla kendi Azure AD dizini mytenantdomain yerine gerekir.
   > 
   > 
4. Hemen altına Post aşağı Hello alanında hello aşağıdaki komutu yazın:
   
    ```
   Host: graph.windows.net
   Authorization: Bearer <your access token>
   Content-Type: application/json
   ```
   
   > [!NOTE]
   > Yedek, &lt;erişim belirtecinizi&gt; hello Azure AD dizininiz için erişim belirteci ile.
   > 
   > 
5. Merhaba, **istek gövdesinde** alan, hello aşağıdakileri yazın:
   
    ```
        {
            "displayName":"MyTestGroup",
            "mailNickname":"MyTestGroup",
            "mailEnabled":"false",
            "securityEnabled": true
        }
   ```
   
    Grupları oluşturma hakkında daha fazla bilgi için bkz: [Grup Oluştur](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#CreateGroup).

Azure AD varlıkları ve grafik tarafından sunulan türleri hakkında daha fazla bilgi ve bunlar üzerinde grafik ile gerçekleştirilebilir hello işlemleri hakkında bilgi için bkz: [Azure AD Graph REST API Başvurusu](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba hakkında daha fazla bilgi [Azure AD grafik API'si](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog)
* Daha fazla bilgi edinmek [Azure AD grafik API'si izin kapsamları](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-permission-scopes)

