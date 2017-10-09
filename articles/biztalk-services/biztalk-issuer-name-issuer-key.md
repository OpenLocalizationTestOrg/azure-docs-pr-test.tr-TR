---
title: "aaaIssuer adı ve verenin anahtarı BizTalk Services | Microsoft Docs"
description: "Bilgi tooretrieve verenle nasıl ve verenin anahtarı için hizmet veri yolu veya BizTalk Services erişim denetimi (ACS). MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a>BizTalk Services: Verenin Adı ve Verenin Anahtarı

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Azure BizTalk Services hello hizmet veri yolu verenin adı ve verenin anahtarı ve hello erişim denetimi verenin adı ve verenin anahtarı kullanır. Bu avantajlar şunlardır:

| Görev | Hangi verenin adı ve verenin anahtarı |
| --- | --- |
| Uygulamanızı Visual Studio'dan dağıtma |Erişim denetimi verenin adı ve verenin anahtarı |
| Hello Azure BizTalk Services portalı yapılandırma |Erişim denetimi verenin adı ve verenin anahtarı |
| LOB geçişler hello Visual Studio'da BizTalk Bağdaştırıcısı hizmetleri oluşturma |Hizmet veri yolu verenin adı ve verenin anahtarı |

Bu konu, hello adımları tooretrieve hello verenin adı ve verenin anahtarı listeler. 

## <a name="access-control-issuer-name-and-issuer-key"></a>Erişim denetimi verenin adı ve verenin anahtarı
Merhaba erişim denetimi verenin adı ve verenin anahtarı hello aşağıdaki tarafından kullanılır:

* Visual Studio'da oluşturulan Azure BizTalk hizmeti uygulamanız: toosuccessfully BizTalk hizmeti uygulamanızda Visual Studio tooAzure dağıtmak, hello erişim denetimi verenin adı ve verenin anahtarı girin. 
* Hello Azure BizTalk Services portalı: BizTalk hizmeti oluşturma ve hello BizTalk Services portalı, erişim denetimi veren adınızı açın ve verenin anahtarı, dağıtımlar için kayıtlı otomatik olarak aynı erişim denetimi değerleri hello.

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a>Alma erişim denetimi verenin adı ve verenin anahtarı hello

kimlik doğrulaması ve get toouse ACS Merhaba verenin adı ve verenin anahtarı değerlerini, hello genel adımları içerir:

1. Merhaba yüklemek [Azure Powershell cmdlet'lerini](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
2. Azure hesabınızda ekleyin:`Add-AzureAccount`
3. Abonelik adı döndürün:`get-azuresubscription`
4. Aboneliğinizi seçin:`select-azuresubscription <name of your subscription>` 
5. Yeni bir ad alanı oluşturun:`new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`

    Örnek:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`
      
5. Merhaba yeni ACS ad alanı (Bu, birkaç dakika sürebilir) oluşturulduğunda hello verenin adı ve verenin anahtarı değerlerini hello bağlantı dizesinde listelenmiştir: 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

toosummarize:  
Verenin adı SharedSecretIssuer =  
Verenin anahtarı SharedSecretKey =

Merhaba hakkında daha fazla [yeni AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet'i. 

## <a name="service-bus-issuer-name-and-issuer-key"></a>Hizmet veri yolu verenin adı ve verenin anahtarı
Hizmet veri yolu verenin adı ve verenin anahtarı BizTalk Bağdaştırıcısı Hizmetleri tarafından kullanılır. Visual Studio'da, BizTalk Services projenizdeki hello BizTalk Bağdaştırıcısı Hizmetleri tooconnect tooan şirket içi iş kolu (LOB) sistemine kullanın. tooconnect, hello LOB geçiş oluşturun ve LOB Sistem bilgilerinizi girin. Bunu yaparken hello hizmet veri yolu verenin adı ve verenin anahtarı da girin.

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a>tooretrieve hello hizmet veri yolu verenin adı ve verenin anahtarı
1. İçinde toohello oturum [Klasik Azure portalı](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Merhaba sol gezinti bölmesinde seçin **Service Bus**.
3. Ad alanınızı seçin. Merhaba görev çubuğunda seçin **bağlantı bilgilerini**. Bu hello görüntüler **varsayılan veren** (verenin adı) ve **varsayılan anahtar** (verenin anahtarı). Değerlerine kopyalanabilir.  

toosummarize:  
Verenin adı varsayılan veren =  
Verenin anahtarı = varsayılan anahtar

## <a name="next"></a>Sonraki
Ek Azure BizTalk Services konuları:

* [Hello Azure BizTalk Services SDK'sını yükleme](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [Öğretici: Azure BizTalk Hizmetleri](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [I Başlat'ı kullanarak Azure BizTalk Services SDK'sı nasıl hello](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Azure BizTalk Hizmetleri](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>Ayrıca Bkz.
* [Nasıl yapılır: kullanım ACS yönetim hizmeti tooConfigure hizmet kimlikleri](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [BizTalk Services: Geliştirici, temel, standart ve Premium sürümler grafiği](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [BizTalk Services: Klasik portalı kullanarak Azure hazırlama](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [BizTalk Services: Durum Grafiğini hazırlama](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [BizTalk Services: Pano, İzleyici ve Ölçek sekmeleri](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [BizTalk Services: Yedekleme ve Geri Yükleme](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [BizTalk Services: Azaltma](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

