---
title: "aaaTechnical hello Market için veri hizmeti oluşturmak için ön koşullar | Microsoft Docs"
description: "Veri Hizmeti toodeploy oluşturmak için hello gereksinimleri anlamak ve Azure Marketi hello üzerinde satmak"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: aaff609a-1cd1-4146-98f4-d04166b0fce0
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 2bba4282473fed63c3fcab43043a97e179705844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-pre-requisites-for-creating-a-data-service-offer-for-hello-azure-marketplace"></a>Veri Hizmeti oluşturmak için teknik ön koşullar hello Azure Marketi teklifi
> [!IMPORTANT]
> **Şu anda artık ekleme duyuyoruz herhangi yeni veri hizmeti yayımcılar. Yeni dataservices listesine onaylanmamış.** Bir SaaS iş uygulaması varsa toopublish istediğiniz AppSource hakkında daha fazla bilgi bulabilirsiniz [burada](https://appsource.microsoft.com/partners). Bir Iaas uygulamalar varsa veya Geliştirici hizmeti misiniz Azure Market'te toopublish gibi daha fazla bilgi bulabilirsiniz [burada](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Merhaba işlemi başlamadan önce baştan sona okuyun ve nerede ve neden her adım gerçekleştirilir anlayın. Mümkün olduğunca, şirket bilgilerinizi ve diğer verileri hazırlama, gerekli Araçları'nı indirmek ve/veya teknik bileşenleri hello teklif oluşturma işlemi başlamadan önce oluşturun.

Merhaba aşağıdaki öğelerindeki hello işlemine başlamadan önce hazır olması gerekir:

## <a name="make-a-decision-on-what-technology-will-be-used-toopublish-your-data-service-offer"></a>Hangi teknolojisi kullanılan toopublish olacaktır üzerinde bir veri hizmeti teklifiniz kararı
Bir yayımcı veri hizmeti Azure Marketi'nde yayımlama sırasında birden çok teknolojileri arasında karar verebilirsiniz. aşağıda açıklanan desteklenen hello ana teknolojileri. Ne olursa olsun hangi teknolojisi kullanılan toopublish hello veri hizmeti, hello son kullanıcı tüketir hello hello verilerine **OData akışı** Azure Market servisi tarafından açılmış. Tam üzerinde Bul OData hizmeti hakkında bilgi [http://www.odata.org/](http://www.odata.org/)

## <a name="sql-azure-database"></a>SQL Azure veritabanı
Veri kümesi SQL Azure içinde hazır olan yayımcının sorumluluğundadır. Toosubscribe tooAzure gerekir veritabanı uygun boyutta sağlamak ve verilerinizi SQL Azure Veritabanına yükleyin. Yayımcı de sorumlu tookeep güncelleştirmesini her zaman güncel veridir. Üzerinde bulabilirsiniz tooAzure Hizmetleri abone olma hakkında daha fazla bilgi [https://azure.microsoft.com/services/sql-database/](https://azure.microsoft.com/services/sql-database/)

Merhaba veri SQL Azure taşırken hello Azure Marketi tabloları ve görünümleri getirebilir. Merhaba yayımcı hangi tabloları/görünümlerini ve sütunların gösterilen toohello son kullanıcı olduğunu belirtebilirsiniz. Daha fazla hello içerik sağlayıcı hello son kullanıcı tarafından hangi sütunların sorgulanabilir ve hangilerinin yalnızca hello yükünde döndürülen de belirtebilirsiniz. Bu yüksek düzeyde bir hakkında hello veritabanındaki verileri açılmamalıdır esneklik sağlar. Bir veya daha fazla veritabanı dizinlerini tarafından yedeklenen toobe sorgulanabilir sütunları gerekir.

## <a name="rest-based-web-service"></a>REST tabanlı web hizmeti
Desteklenen protokolü: **yalnızca HTTPS**

Varolan REST tabanlı hizmetler hello Azure Market gösterilebilir. Bir OData akışı olarak hello Azure Marketi hizmet hello veri kümesi her zaman gösterilen toohello son kullanıcı olduğundan toobe mümkün toomap hizmet tooa göre OData hizmeti hello. uç noktaları Hello REST tabanlı şekilde toodo tüm parametreleri tooexpose HTTP parametre olarak gerekir.

Merhaba yükü bir ATOM yanıtına eşlenebilir. bir biçimde toobe gerekir. Bu nedenle hello Hizmetleri hello yanıttan toobe XML biçiminde olmalıdır ve yalnızca hello yükü değerleri (ör. kayıt kümesi) içeren bir yinelenen öğe içerebilir. Hello Azure Marketi hizmet hello girişi düğümü içinde özellik düğümleri içine düğümü toohello girişi düğümü ATOM ve hello yükü değerleri yinelenen hello eşler.

Bir HTTP parametre olarak ya da hello HTTP üstbilgisinde (anahtar değer çifti) – temel kimlik doğrulaması da desteklenir sağlanan yetkilendirme bilgilerini (örneğin, kimlik doğrulama belirteci, vb. anahtar, API) toobe gerekir. Sağlanan toobe geçerli bir anahtar gerektiriyor ve bu anahtar tüm istekleri Azure Market üzerinden yapılan. İzleme ve faturalama kullanıcı hello Azure Marketi katmanında olur.

Merhaba hizmeti tarafından döndürülen hataları, HTTP durum kodları eşlenen toobe gerekir. Merhaba hata içeren bir XML Hello hizmet verir durumda bunlar hello Azure Marketi hizmet tooHTTP durum kodları tarafından eşlenen toobe adımıdır.

## <a name="soap-based-web-services"></a>SOAP tabanlı web Hizmetleri
Protokol: **yalnızca HTTPS**

aynı hello REST tabanlı hizmet bölümü olduğu gibi hello Hello gereksinimleri verilmiştir. Merhaba yalnızca parametreleri toohello Publisher'ın hizmeti ile Azure Market üzerinden yapılan her isteği gönderiliyor bir XML gövdesinde de girilebilir farktır. Başka bir deyişle, HTTP parametreleri hello kullanıcı XML öğelerine hello isteği toohello içerik sağlayıcının web hizmetiyle gönderilen XML belgesinin çevrilen hello ön uç sağlar.

## <a name="odata-based-web-services"></a>OData tabanlı web Hizmetleri
Protokol: **yalnızca HTTPS**

Verileri bir OData hizmeti tooAzure Market gösterilebilir. Merhaba sisteminiz giderek toopass hello hizmeti aracılığıyla ve hello hizmetinin hello kökü hello Azure Marketi hizmet kök – Azure Market üzerinden tüm sonraki çağrılar Git tooensure ile değiştirir.

OData hizmetlerini yalnızca hello arka uç veritabanı karşı toogo gerek yoktur. OData herhangi bir depolama veya iş mantığı toodrive hello hizmet türünü destekler.

## <a name="next-steps"></a>Sonraki Adımlar
Merhaba önkoşulları gözden geçirdikten ve tamamlanan hello gerekli görevler artık, ileriye doğru veri hizmeti teklifiniz içinde ayrıntılı hello olarak oluşturma hello ile taşıyabilirsiniz [veri hizmeti yayımlama Kılavuzu](marketplace-publishing-data-service-creation.md).

Veya tooreview hello genel işlem ve hello ilgili makaleler her aşama yayımlama hello için isterseniz, lütfen hello makale ziyaret [Başlarken: nasıl toopublish bir teklif toohello Azure Marketi](marketplace-publishing-getting-started.md).

[link-acct]:marketplace-publishing-accounts-creation-registration.md
