---
title: BizTalk Services tooAzure Logic Apps aaaMove uygulamalardan | Microsoft Docs
description: "Taşıma veya Azure BizTalk Services MABS tooLogic uygulamaları geçirme"
services: logic-apps
documentationcenter: 
author: jonfancey
manager: anneta
editor: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: ladocs; jonfan; mandia
ms.openlocfilehash: b3b065b90a37002f72305b0fc866c24231fb5f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-from-biztalk-services-toologic-apps"></a>BizTalk Services tooLogic uygulamaları taşıma

Microsoft Azure BizTalk Services'ı (MABS) devre dışı bırakılıyor. Bu konuda toomove MABS tümleştirme çözümleri tooAzure Logic Apps kullanın. 

## <a name="overview"></a>Genel Bakış

BizTalk Services iki alt hizmetinden oluşur:

1.  Karma bağlantılar Microsoft BizTalk Hizmetleri
2.  EAI ve EDI köprüsü tabanlı tümleştirmesi

Toomove karma bağlantılar, ardından arıyorsanız [Azure App Service karma bağlantılar](../app-service/app-service-hybrid-connections.md) hello değişiklikleri ve bu hizmetin özelliklerini açıklar. Karma bağlantılar Azure BizTalk Services karma bağlantılar değiştirir. Azure karma bağlantılar, Azure App Service ile kullanılabilir ve hello Azure portalında sunulur. İçinde oluşturduğunuz yeni karma bağlantılar portal hello ve Azure karma bağlantılar da BizTalk Services karma bağlantılar var olan yeni bir karma Bağlantı Yöneticisi toomanage sağlar. Azure App Service karma bağlantı genel olarak kullanılabilir (GA) sayısıdır.

EAI ve EDI köprüsü tabanlı tümleştirmesi için Logic Apps hello yerini alır. Logic Apps tüm BizTalk Services ve daha fazlasını olarak aynı yetenekleri hello sağlar. Logic Apps bulut ölçekli tooquickly ve kolay bir tarayıcı veya Visual Studio içinde araçları kullanarak karmaşık tümleştirme çözümlerini derlemeye izin tüketim tabanlı iş akışı ve düzenleme özellikleri sağlar.

Aşağıdaki tablonun hello tooLogic uygulamaları BizTalk Services özelliklerinin bir eşleme sağlar.

| BizTalk Services   | Logic Apps            | Amaç                  |
| ------------------ | --------------------- | ---------------------------- |
| Bağlayıcı          | Bağlayıcı             | Veri gönderme ve alma   |
| Köprüsü             | Logic App             | Ardışık Düzen işlemci           |
| Aşama doğrula     | XML doğrulaması eylemi      | Bir XML belgesi bir şemaya karşı doğrulama             |
| Aşama zenginleştirmek       | Veri belirteçleri      | İletilere veya yönlendirme kararları için özelliklerini Yükselt             |
| Aşama dönüştürme    | Eylem dönüştürme      | Bir biçim tooanother XML iletileri Dönüştür             |
| Aşama kod çözme       | Düz dosya kod çözme eylemi      | Düz dosya tooXML Dönüştür             |
| Aşama kodlama       |  Düz dosya kodlamak eylemi      | XML tooflat dosyasından Dönüştür             |
| İleti denetçisi       |  Azure işlevleri veya API uygulamaları      | Özel kod, tümleştirmeler çalıştırın             |
| Rota eylem      |  Koşul veya anahtar      | Merhaba, rota iletileri tooone bağlayıcılar belirtilen             |

BizTalk Services yapı farklı türlerde mevcuttur.

## <a name="connectors"></a>Bağlayıcılar
BizTalk Services bağlayıcıları köprüleri toosend izin ve HTTP tabanlı istek/yanıt etkileşimleri etkin iki yönlü köprüleri dahil verileri alabilirsiniz. Logic Apps içinde hello aynı terimler kullanılır. Bağlayıcılar mantıksal uygulamalar'ın aynı amaçla ve ayrıca üzerinde teknolojileri ve Hizmetleri geniş dizisi tooa bağlanabilir 140 dahil hello hizmet, hem kullanarak şirket içi veri ağ geçidi (Merhaba BizTalk bağdaştırıcı hizmeti BizTalk Services tarafından kullanılan değiştirme) Merhaba, ve OneDrive, Office365, Dynamics CRM ve diğerleri gibi SaaS ve PaaS Hizmetleri bulut.

BizTalk Services sınırlı tooFTP, SFTP ve hizmet veri yolu kuyruğu ya da konu aboneliği kaynaklardır.

![](media/logic-apps-move-from-mabs/sources.png)

Her köprüsü hello çalışma zamanı adresi ve hello köprüsü hello göreli adres özellikleri ile yapılandırılmış varsayılan olarak bir HTTP uç noktası vardır. tooachieve hello aynı kullanım hello Logic Apps ile [istek ve yanıt](../connectors/connectors-native-reqres.md) eylemler.

## <a name="xml-processing-and-bridges"></a>XML işleme ve köprüleri
BizTalk Services köprü benzer tooa işleme ardışık ' dir. Köprü Bağlayıcısı'ndan alınan verileri alabilir ve bazı hello verilerle çalışmak ve tooanother sistem gönderin. Logic Apps aynı aynı ardışık düzen tabanlı etkileşim BizTalk Services düzenleri ve ayrıca bir desenlerinin diğer tümleştirme sağlar hello destekleyerek hello. Merhaba [XML istek-yanıt köprüsü](https://msdn.microsoft.com/library/azure/hh689781.aspx) BizTalk Services'da gerçekleştirebileceğiniz aşamaları oluşan bir VETER ardışık düzeni bilinir:

* (V) doğrulama
* (E) zenginleştirmek
* (T) dönüştürme
* (E) zenginleştirmek
* (R) yolu

Görüntü aşağıdaki hello görüldüğü gibi hello işleme isteği ve yanıtlama arasında bölünür ve yanıt yolları (örneğin her biri için farklı haritalar kullanılarak ayrı ayrı) hello istek ve hello üzerinde denetim sağlar:

![](media/logic-apps-move-from-mabs/xml-request-reply.png)

Ayrıca, bir XML tek yönlü köprüsü kod çözme ve kodla aşamaları hello başında ve sonunda işleme ekler ve hello doğrudan köprüsü tek bir Enrich aşamasını içerir.

### <a name="message-processing-and-decodingencoding"></a>İleti işleme ve kod çözme ve kodlama
BizTalk Services, farklı türlerde XML iletileri almasına ve hello eşleşen şema hello ileti için belirleyin. Bu hello gerçekleştirilir **ileti türlerini** hello aşaması işleme ardışık alırsınız. Ardından, hello kod çözme aşama algılanan hello ileti türü toodecode sağlanan hello şeması kullanarak kullanır. Merhaba şema Yataydosya şema ise hello gelen Yataydosya tooXML dönüştürür. 

Logic Apps benzer yetenekleri sağlar. Çok sayıda hello farklı bağlayıcı Tetikleyicileri (dosya sistemi, FTP, HTTP vb.) kullanarak farklı protokoller bir Yataydosya almak ve hello kullan [düz dosya kod çözme](../logic-apps/logic-apps-enterprise-integration-flatfile.md) eylem tooconvert hello gelen veri tooXML. Herhangi bir gerektirmeden toologic uygulamaları değiştirir ve şemaları tooyour tümleştirme hesabını karşıya yükleme doğrudan varolan düz dosya şemaları taşıyabilirsiniz.

### <a name="validation"></a>Doğrulama
Merhaba gelen veri dönüştürülmüş tooXML (veya XML hello ileti biçimi alındı olup olmadığını) olduktan sonra selamlama iletisine tooyour XSD şema aynılarını toodetermine doğrulama çalıştırır. toodo bu Logic Apps, kullanım hello [XML doğrulama](../logic-apps/logic-apps-enterprise-integration-xml-validation.md) eylem. Tekrar kullanabilirsiniz hello şemalar BizTalk hizmetlerinden herhangi bir değişiklik yapılmadan.

### <a name="transform-messages"></a>İletileri dönüştürme
BizTalk Services ' bir XML tabanlı ileti biçimi tooanother hello dönüştürme aşaması dönüştürür. Bu, hello TRFM tabanlı Eşleyici kullanan bir harita uygulanarak yapılır. Logic Apps içinde hello işlemi benzer. Merhaba dönüştürme eylem bir harita tümleştirme hesabınızdan yürütür. Merhaba temel fark Logic Apps eşlemelerinin XSLT biçiminde olmasıdır. XSLT XSLT, İşlevsiler içeren BizTalk Server için oluşturulan eşlemeleri dahil olmak üzere zaten varolan hello özelliği tooreuse içerir. 

### <a name="routing-rules"></a>Yönlendirme kuralları
BizTalk Services hangi uç nokta/bağlayıcı toosend gelen iletileri/verileri bir yönlendirme karar verir. Merhaba özelliği tooselect önceden yapılandırılmış uç noktalarının sayısını birini hello yönlendirme filtre seçeneğini kullanarak mümkündür:

![](media/logic-apps-move-from-mabs/route-filter.png)

Logic Apps ile daha karmaşık mantığı yetenekleri sağlar [koşulu](../logic-apps/logic-apps-use-logic-app-features.md) ve [anahtar](../logic-apps/logic-apps-switch-case.md), Gelişmiş denetim akışı etkinleştirme ve yönlendirme. BizTalk Services yönlendirme filtreleri dönüştürme en iyi sonucu elde edilir kullanarak bir **koşulu** *varsa* yalnızca iki seçenek vardır. Varsa ikiden daha sonra kullanmak bir **geçiş**.

### <a name="enrich"></a>Zenginleştirmek
Merhaba Enrich aşamasında BizTalk Services işleme alınan hello verilerle ilişkili özellikler toohello ileti bağlamı ekler. Örneğin, (aşağıda bir veritabanı araması veya bir XPath ifadesi kullanarak bir değer ayıklanıyor tarafından ele) yönlendirmesi için bir özellik toouse yükseltme. Logic Apps sağlar erişim tooall bağlamsal verileri çıkışları Eylemler önceki gelen aynı davranışı hello basit tooreplicate yapma. Örneğin, hello kullanarak `Get Row` SQL bağlantı eylem dönmek bir SQL Server veritabanından veri ve kullanım hello veri yönlendirme karar eylem. Benzer şekilde, gelen Service Bus özelliklerini Tetikleyici tarafından sıraya alınan iletileri hello xpath iş akışı tanımı dili ifade kullanılarak XPath yanı sıra olan adreslenebilir.

### <a name="use-custom-code"></a>Özel kod kullanın
BizTalk hizmetleri sağlayan hello özelliği çok[özel kodu çalıştırmak](https://msdn.microsoft.com/library/azure/dn232389.aspx) kendi derlemelerde karşıya yüklendi. Bu hello tarafından uygulanan [IMessageInspector](https://msdn.microsoft.com/library/microsoft.biztalk.services.imessageinspector.aspx) arabirimi. Hello köprüsü her aşamada bu arabirimi gerçekleştiren oluşturduğunuz hello .net türü sağlayın iki özellikleri (üzerinde denetçisi girin ve üzerinde çıkış denetçisi) içerir. Özel kod tooperform daha karmaşık yeniden var olan kodu ortak iş mantığını gerçekleştirirler derlemelerde yanı sıra hello veri işleme da sağlar. 

Logic Apps tooexecute özel kod iki birincil yol sağlar: Azure işlevleri ve API Apps. Azure işlevleri oluşturulur ve mantığı uygulamalardan çağrılır. Bkz: [ekleme ve Azure işlevleri aracılığıyla mantıksal uygulamalar için çalışma özel kod](../logic-apps/logic-apps-azure-functions.md). API uygulamaları, Azure App Service, toocreate parçası kendi tetikleyiciler ve Eylemler kullanın. Daha fazla bilgi edinmek [Logic Apps ile özel bir API toouse oluşturma](../logic-apps/logic-apps-create-api-app.md). 

BizTalk Services çağrı assmeblies özel kod varsa, ya da bu taşıyabilirsiniz tooAzure işlevleri kod veya özel API API uygulamaları ile; oluşturma ne, uygulama bağlı olarak. Örneğin, başka bir service Logic Apps bağlayıcı yok sarmalar kodu varsa, API uygulaması oluşturma sonra mantıksal uygulamanızı içinde API uygulamanızı sağlar hello eylemlerini kullanın. Yardımcı işlevleri veya kitaplıkları varsa, Azure işlevleri büyük olasılıkla hello en uygun olur.

### <a name="edi-processing-and-trading-partner-management"></a>İşleme ve ticari ortak Yönetimi EDI
BizTalk Services EDI ve B2B işleme AS2 desteği içerir (Uygulanabilirlik deyimi 2) X12 ve EDIFACT. Bu nedenle Logic Apps yapar. BizTalk Services, EDI köprüleri oluşturma ve yönetme oluşturun/ticari ortaklar ve hello ayrılmış izleme ve Yönetim Portalı'nda anlaşmaları.

Logic Apps içinde bu işlevselliği ile Merhaba dahil edilmiştir [Kurumsal tümleştirme paketi](../logic-apps/logic-apps-enterprise-integration-overview.md). Bu, EDI ve B2B işleme hello tümleştirme hesabı ve B2B Eylemler oluşur. Merhaba [tümleştirme hesabını](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) kullanılan toocreate olduğu ve yönetme [ticaret ortakları](../logic-apps/logic-apps-enterprise-integration-partners.md) ve [anlaşmaları](../logic-apps/logic-apps-enterprise-integration-agreements.md). Bir tümleştirme hesabı oluşturduktan sonra bir veya daha fazla logic apps toohello hesabı ilişkilendirebilirsiniz. İlişkili sonra iş ortağı bilgileri mantıksal uygulama içinde ticaret hello B2B Eylemler tooaccess kullanabilirsiniz. Aşağıdaki eylemler hello sağlanır:

* AS2 kodlama
* AS2 kod çözme
* X12 kodlama
* X12 kod çözme
* EDIFACT kodlama
* EDIFACT kod çözme

BizTalk Services, bu eylemleri hello aktarım protokollerinden birbirinden ayrılır. Bu nedenle mantıksal uygulamalarınızı oluşturduğunuzda, hangi bağlayıcılar üzerinde toosend kullanın ve veri alma daha fazla esnekliğe sahip olursunuz. Örneğin, bu e-posta ekleri olarak olası tooreceive X12 dosyaysa ve bir mantıksal uygulama'te bu dosyaların işlem. 

## <a name="manage-and-monitor"></a>Yönetme ve izleme
Ticari ortak Yönetimi yanı sıra hello portal BizTalk Services için sağlanan ayrılmış özellikleri toomonitor izleme ve sorunlarını giderme. 

Logic Apps daha zengin izleme ve izleme kapasiteleri hello içinde sağlar [Azure portal](../logic-apps/logic-apps-monitor-your-logic-apps.md)ile Merhaba [Operations Management Suite B2B çözümü](../logic-apps/logic-apps-monitor-b2b-message.md)da dahil olmak üzere bir göz şeylere tutmak için bir mobil uygulama Merhaba üzerinde olduğunuzda taşıyın.

## <a name="high-availability"></a>Yüksek kullanılabilirlik
tooachieve BizTalk Services yüksek kullanılabilirlik (HA), bir verilen bölge tooshare hello işleme yükünü birden fazla örneği kullanın. Logic apps ile bölge içinde HA yerleşiktir ve hiçbir ek maliyetlerine neden olur. BizTalk Services B2B işlemek için bölge olağanüstü durum kurtarma için bir yedekleme ve geri yükleme işlemi gereklidir. Logic Apps, çapraz bölge Etkin/pasif olarak [DR yetenek](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md) sağlanır; iş sürekliliği için farklı bölgelerdeki tümleştirme hesapları arasında hello verilerinin eşitlemesine ilişkin B2B veren.

## <a name="next"></a>Sonraki
* [Logic Apps nedir?](logic-apps-what-are-logic-apps.md)
* [İlk mantıksal uygulamanızı oluşturun](logic-apps-create-a-logic-app.md) veya [önceden oluşturulmuş bir şablon](logic-apps-use-logic-app-templates.md) kullanarak hızlı şekilde çalışmaya başlayın  
* [Tüm kullanılabilir bağlayıcılar hello Görünüm](../connectors/apis-list.md) bir mantıksal uygulama kullanabilirsiniz
