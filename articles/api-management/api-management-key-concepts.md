---
title: "aaaAzure API Management genel bakış ve anahtar kavramları | Microsoft Docs"
description: "API'ler, ürünler, roller, gruplar ve diğer API Management temel kavramları hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: e71da405-835a-48f3-956f-45c1a85698d7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: a77b24b4632d868afa15bd6cf88060982046cb38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-api-management"></a>API Management nedir?
API Management API'leri tooexternal, iş ortağı ve iç geliştiricilere toounlock hello olasılığı kendi veri ve hizmet yayımlama kuruluşların yardımcı olur. İşletmeler her yerde bir dijital platform olarak işlemlerini tooextend arayan, yeni kanallar oluşturmak, yeni müşteriler bulmak ve mevcut müşterilerle daha derin etkileşimi yürüten. API Management hello çekirdek yetkinlikleri tooensure Geliştirici katılımı, iş öngörüleri, analizler, güvenlik ve koruma aracılığıyla başarılı bir API programı sağlar.

Video Azure API Management genel bir bakış için aşağıdaki hello izlemek ve nasıl toouse API Management tooadd birçok özellik tooyour API, erişim denetimi dahil olmak üzere oran sınırlaması, izleme, olay günlüğünü ve bölümünüzün minimum çabayla yanıt önbelleğe öğrenin.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-API-Management-Overview/player]
> 
> 

API Management toouse, yöneticiler API'ler oluşturur. Her API bir veya daha fazla işlemden oluşur ve her API tooone veya daha fazla ürün eklenebilir. bir API toouse, geliştiriciler bu API'yi içeren tooa ürün abone ve ardından hello API'nin işlemi, geçerli olabilecek konu tooany kullanım ilkeleri çağırabilirsiniz.

Bu konuda API Management temel kavramlarına ilişkin genel bir bakış verilmiştir.

> [!NOTE]
> Merhaba daha fazla bilgi için bkz: [bulut tabanlı API Management: gücünden hello güç API'ları,](http://j.mp/ms-apim-whitepaper) PDF teknik incelemesi. API Management hakkında CITO Research tarafından hazırlanan tanıtım amaçlı bu teknik inceleme şunları içerir: 
> 
> * Yaygın API gereksinimleri ve sorunları
> * API'leri ayırma ve cepheleri sunma
> * Geliştiricilerin hızla hazır olmalarını sağlama
> * Erişimi güvenli hale getirme
> * Analizler ve ölçümler
> * API Management platformuyla denetim ve öngörü elde etme
> * Bulut ile şirket içi çözüm kullanımının karşılaştırması
> * Azure API Management
> 
> 

## <a name="apis"> </a>API’ler ve işlemler
API'ler bir API Management hizmet örneğinin hello temelidir. Her API işlemleri mevcut toodevelopers kümesini temsil eder. Her API hello API'yi uygulayan bir başvuru toohello arka uç hizmeti içerir ve işlemlerini hello arka uç hizmeti tarafından uygulanan toohello işlemleri eşleyin. API Management işlemleri; URL eşleme, sorgu ve yol parametreleri, istek ve yanıt içeriği ve işlem yanıtını önbelleğe alma üzerinde sahip olunan denetim sayesinde yüksek oranda yapılandırılabilir niteliktedir. Hız sınırı, kotalar ve IP kısıtlama ilkeleri, ayrıca hello API veya tek işlem düzeyinde uygulanabilir.

Daha fazla bilgi için bkz: [nasıl toocreate API'leri] [ How toocreate APIs] ve [nasıl tooadd işlemleri tooan API][How tooadd operations tooan API].

## <a name="products"> </a> Ürünler
Ürün API'leri ortaya toodevelopers şeklini değil. API Management ürünleri bir ya da daha fazla API’ye sahiptir. Başlık, açıklama ve kullanım koşulları ile yapılandırılırlar. Ürünler **Açık** veya **Korumalı** olabilir. Korumalı ürünleri, bunlar kullanılabilir, açıkken abone toobefore olmalıdır ürünler abonelik olmadan kullanılabilir. Bir ürün geliştiriciler tarafından kullanılmaya hazır olduğunda yayımlanabilir. Yayımlandıktan görüntülenebilmesi için (ve korumalı ürünleri durumunun hello abone sonra) geliştiriciler tarafından. Abonelik onayı hello ürün düzeyinde yapılandırılır ve yönetici onayı iste veya otomatik olarak onaylanır.

Kullanılan toomanage hello ürünleri toodevelopers görünürlüğünü gruplarıdır. Ürünler görünürlük toogroups vermek ve geliştiricilerin görüntülemek ve, ait oldukları görünür toohello grupları toohello ürünleri abone. 

Daha fazla bilgi için bkz: [nasıl toocreate ürün ve yayımlama] [ How toocreate and publish a product] ve hello video.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

## <a name="groups"> </a> Gruplar
Kullanılan toomanage hello ürünleri toodevelopers görünürlüğünü gruplarıdır. API Management aşağıdaki sabit sistem gruplarına hello sahiptir.

* **Yöneticiler**: Azure aboneliği yöneticileri bu grubun üyesidir. Yöneticiler API Management hizmet örneklerini yönetir API'leri, işlemleri ve geliştiriciler tarafından kullanılan ürünleri hello oluşturma.
* **Geliştiriciler**: Kimliği doğrulanmış geliştirici portalı kullanıcıları bu gruba girer. Geliştiriciler, Apı'lerinizi kullanan uygulamalar oluşturmak hello müşterilerdir. Geliştiriciler erişim toohello Geliştirici Portalı verilir ve hello bir API'nin işlemlerini çağıran uygulamalar oluşturun.
* **Konuklar** -kimliği doğrulanmamış Geliştirici portalı kullanıcıları, bu gruba bir API Management örneği sonbaharda hello Geliştirici portalını ziyaret eden olası müşteriler gibi. Bunlar hello özelliği tooview API'leri gibi bazı salt okunur erişim hakkı verilebilir, ancak çağıramama.

Toplama toothese sistem gruplarında yöneticiler özel gruplar oluşturabilir veya [ilişkili Azure Active Directory kiracılarındaki dış grupları yararlanan](api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group). Özel ve dış gruplar tooAPI ürünleri erişmek ve geliştiricilere görünürlük vererek sistem grupları yanında kullanılabilir. Örneğin, özel bir grup oluşturmak için belirli bir ile ilişkili Geliştiriciler iş ortağı kuruluş ve erişim izni yalnızca ilgili API'leri içeren bir üründen toohello API'leri. Bir kullanıcı birden fazla grubun üyesi olabilir.

Daha fazla bilgi için bkz: [nasıl toocreate ve kullanım grupları][How toocreate and use groups].

## <a name="developers"> </a> Geliştiriciler
Geliştiriciler API Management hizmet örneğindeki hello kullanıcı hesapları temsil eder. Geliştiriciler oluşturulabilir veya davet toojoin yöneticiler tarafından veya bunlar hello kaydolabilirsiniz [Geliştirici Portalı][Developer portal]. Her geliştirici bir veya daha fazla grup üyesi olan ve görünürlük toothose grupları vermek toohello ürünleri abone olabilir.

Geliştiriciler tooa ürün abone olduğunuzda bunların hello ürün hello birincil ve ikincil anahtar verilir. Bu anahtar hello ürün API'lerine çağrılar yapılırken kullanılır.

Daha fazla bilgi için bkz: [nasıl toocreate veya davet geliştiriciler] [ How toocreate or invite developers] ve [nasıl tooassociate geliştiricilere grupları][How tooassociate groups with developers].

## <a name="policies"> </a> İlkeler
Güçlü bir özellik toochange hello davranışını yapılandırma yoluyla hello API hello publisher izin API Management ilkelerdir. Merhaba istek üzerinde sırayla yürütülen deyimlerin bir koleksiyon veya bir API yanıtını ilkelerdir. XML tooJSON ve çağrı hızı toorestrict hello tutar bir geliştiriciden gelen çağrıların sayısını sınırlandırma biçimi dönüştürme popüler deyimleri ekleyin ve diğer birçok ilkeleri kullanılabilir.

Merhaba ilke aksini belirtmedikçe ilke ifadelerini öznitelik değerleri ya da metin değerleri hello API Management ilkeleri olarak kullanılabilir. Hello gibi bazı ilkeler [kontrol akışı](https://msdn.microsoft.com/library/azure/dn894085.aspx#choose) ve [değişken Ayarla](https://msdn.microsoft.com/library/azure/dn894085.aspx#set-variable) ilkeler ilke ifadelerini temel alarak. Daha fazla bilgi için bkz: [ilkeleri Gelişmiş](https://msdn.microsoft.com/library/azure/dn894085.aspx#AdvancedPolicies), [ilke ifadelerini](https://msdn.microsoft.com/library/azure/dn910913.aspx), izleme hello videoyu izleyerek.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

API Management ilkelerinin tam listesi için bkz. [İlke başvurusu][Policy reference]. İlkeleri yapılandırma ve kullanma hakkında daha fazla bilgi için bkz. [API Management ilkeleri][API Management policies]. Hız sınırı ve kota ilkeleri içeren bir ürün oluşturmaya ilişkin öğretici için bkz. [Gelişmiş ürün ayarları oluşturma ve yapılandırma][How create and configure advanced product settings]. Gösteri için video aşağıdaki hello bakın.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

## <a name="developer-portal"> </a> Geliştirici portalı
Merhaba Geliştirici Portalı burada geliştiriciler API'ları, Görünüm ve arama işlemleri hakkında bilgi edinin ve tooproducts abone ' dir. Müşteri adayları hello Geliştirici Portalı ziyaret API'lerle işlemleri görüntüleyebilir ve ve kaydolun. Geliştirici portalınızın Hello URL'si, API Management hizmet örneğinizin Klasik Azure portalı hello hello panosunda yer alır.

Özel içerik ekleyerek, stilleri özelleştirerek ve marka bilgilerinizi ekleyerek, geliştirici portalınızın hello Görünüm ve yapısını özelleştirebilirsiniz.

## <a name="api-management-and-hello-api-economy"></a>API Management ve hello API ekonomisi
toolearn API Management, sunu hello Microsoft Ignite 2015 Konferanstan aşağıdaki izleme hello hakkında daha fazla bilgi.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3708/player]
> 
> 

[APIs and operations]: #apis
[Products]: #products
[Groups]: #groups
[Developers]: #developers
[Policies]: #policies
[Developer portal]: #developer-portal

[How toocreate APIs]: api-management-howto-create-apis.md
[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer
[How create and configure advanced product settings]: api-management-howto-product-with-rules.md
[How toocreate or invite developers]: api-management-howto-create-or-invite-developers.md
[Policy reference]: api-management-policy-reference.md
[API Management policies]: api-management-howto-policies.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance




