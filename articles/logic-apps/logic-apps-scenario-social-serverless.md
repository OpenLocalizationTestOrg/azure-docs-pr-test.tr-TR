---
title: "aaaScenario - müşteri öngörüleri Panosu Azure sunucusuz ile oluşturma | Microsoft Docs"
description: "Nasıl bir örnek bir Pano toomanage müşteri geri bildirim, sosyal veriler ve Azure Logic Apps ve Azure işlevleri ile daha fazla oluşturabilirsiniz."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: jehollan
ms.openlocfilehash: db175e895e37aa795a9c34bf4d65566bf68f8c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a>Azure işlevleri ve Azure Logic Apps ile gerçek zamanlı müşteri öngörüleri panosu oluşturun

Azure sunucusuz araçları altyapısıyla ilgili toothink gerek kalmadan güçlü özellikleri tooquickly hello bulutta yapı ve ana bilgisayar uygulamalarını sağlar.  Bu senaryoda, bir Pano tootrigger müşteri geri bildirimi oluşturur, machine learning ile geribildirim çözümlemek ve Power BI veya Azure Data Lake gibi bir kaynak Öngörüler yayımlama.

## <a name="overview-of-hello-scenario-and-tools-used"></a>Merhaba senaryo ve kullanılan Araçları'na genel bakış

Bu çözüm tooimplement sipariş, Azure içinde sunucusuz uygulamaların hello iki anahtar bileşenleri özelliğinden yararlanır: [Azure işlevleri](https://azure.microsoft.com/services/functions/) ve [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).

Logic Apps hello bulutta sunucusuz iş akışı altyapısıdır.  Orchestration sunucusuz bileşenlerinde sağlar ve ayrıca tooover 100 Hizmetleri ve API bağlanır.  Bu senaryoda, müşterilerin görüşleri üzerinde bir mantıksal uygulama tootrigger oluşturacağız.  Tanımlandığında toocustomer geri bildirim yardımcı olabilecek hello bağlayıcılar Outlook.com, Office 365, anket Monkey, Twitter ve bir HTTP isteği bazıları [bir web formundan](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).  Merhaba iş akışı için aşağıdaki biz diyez Twitter'da izlenir.

İşlevler hello bulutta sunucusuz işlem sağlar.  Bu senaryoda, bir dizi önceden tanımlanmış anahtar sözcükleri dayalı müşterilerden Azure işlevleri tooflag tweet'leri kullanacağız.

çözümün tamamında Hello olabilir [Visual Studio'da derleme](logic-apps-deploy-from-vs.md) ve [kaynak şablon bir parçası olarak dağıtılan](logic-apps-create-deploy-template.md).  Ayrıca videosu hello senaryonun olan [Channel 9](http://aka.ms/logicappsdemo).

## <a name="build-hello-logic-app-tootrigger-on-customer-data"></a>Müşteri verilerine Hello mantığı uygulama tootrigger derleme

Sonra [bir mantıksal uygulama oluşturma](logic-apps-create-a-logic-app.md) Visual Studio veya hello Azure portalı:

1. İçin bir tetikleyici eklemek **üzerinde yeni Tweet'leri** Twitter gelen
2. Merhaba tetikleyici toolisten tootweets bir anahtar sözcüğü veya diyez yapılandırın.

   > [!NOTE]
   > Merhaba yinelenme hello tetikleyici özellikte yoklama tabanlı tetikleyiciler üzerinde yeni öğeler için hello mantıksal uygulama hangi sıklıkta denetleyeceğini belirler

   ![Twitter tetikleyici örneği][1]

Bu uygulama artık tüm yeni tweet'leri ateşlenir.  Biz sonra tweet verileri alabilir ve ifade hello düşünceleri daha iyi anlamak.  Merhaba bu için kullandığımız [Azure Bilişsel hizmeti](https://azure.microsoft.com/services/cognitive-services/) toodetect düşünceleri metin.

1. Tıklatın **yeni adım**
1. Seçin veya arama Merhaba **metin analizi** Bağlayıcısı
1. Select hello **algılamak düşünceleri** işlemi
1. İstenirse, hello metin Analytics hizmeti için geçerli bir Bilişsel hizmetler anahtarı sağlayın
1. Merhaba eklemek **Tweet metin** metin tooanalyze hello gibi.

Biz hello tweet veri ve öngörü hello tweet üzerinde sahip olduğunuza göre diğer bağlayıcıları çeşitli uygun olabilir:
* Power BI - satırları tooStreaming veri kümesi ekleyin: görünümü tweet'leri gerçek zamanlı bir Power BI Panoda.
* Azure Data Lake - dosya ekleme: müşteri verileri tooan Azure Data Lake dataset tooinclude analytics işleri ekleyin.
* SQL - satırları ekleyin: deposundaki verileri sonraki alma için bir veritabanı.
* Boşluk - iletisi gönderin: Eylemler gerektirir olumsuz görüşler slack kanalda uyar.

Bir Azure işlevi de daha fazla özel işlem hello veri üzerinde kullanılan toodo olabilir.

## <a name="enriching-hello-data-with-an-azure-function"></a>Merhaba verilerle zenginleştirmek bir Azure işlevi

Bir işlev oluşturabilmeniz için önce kimliğinizi uygulamamız Azure aboneliğimiz toohave bir işlev uygulaması gerekiyor.  Merhaba portalında bir Azure işlevi oluşturma ile ilgili ayrıntılar için [bulunabilir burada](../azure-functions/functions-create-first-azure-function-azure-portal.md)

Doğrudan mantığı uygulamadan adlı bir işlev toobe için bunu ihtiyaçlarını toohave bir HTTP tetiklemek bağlama.  Merhaba kullanmanızı öneririz **HttpTrigger** şablonu.

Bu senaryoda, hello Azure işlevi hello istek gövdesi hello tweet metin olacaktır.  Bir anahtar sözcük veya tümcecik Hello tweet metin içeriyorsa, hello işlevi kodda mantığı üzerinde yalnızca tanımlayın.  Merhaba işlevi kendisi kadar basit veya karmaşık hello senaryo için gerektiği şekilde tutulması.

Merhaba işlevi Hello sonunda, yalnızca bir yanıt toohello mantıksal uygulama bazı verilerle döndür.  Bu basit bir Boole değeri olabilir (örneğin `containsKeyword`), veya karmaşık bir nesne.

![Yapılandırılmış Azure işlevi adım][2]

> [!TIP]
> Karmaşık bir yanıt bir mantıksal uygulama bir işlevden erişirken hello ayrıştırma JSON eylemini kullanın.

Merhaba işlevi kaydedildikten sonra yukarıda oluşturduğunuz hello mantıksal uygulama içine eklenebilir.  Merhaba mantıksal uygulama içinde:

1. Tooadd tıklatın bir **yeni adım**
1. Select hello **Azure işlevleri** Bağlayıcısı
1. Toochoose var olan işlevi seçin ve oluşturulan toohello işlevi Gözat
1. Hello Gönder **Tweet metin** hello için **istek gövdesi**

## <a name="running-and-monitoring-hello-solution"></a>Çalıştıran ve izleme hello çözümü

Logic Apps içinde sunucusuz düzenlemelerin yazma hello avantajları hello zengin hata ayıklama ve izleme kapasiteleri biridir.  Tüm çalışma (geçerli veya geçmiş) Visual Studio'dan hello Azure portal veya hello REST API ve SDK aracılığıyla görüntülenebilir.

Merhaba en kolay yolu tootest bir mantıksal uygulama birini kullanarak hello **çalıştırmak** hello Tasarımcısı'nda düğmesi.  Tıklatarak **çalıştırmak** toopoll hello tetikleyici bir olay algılandığında kadar her 5 saniyede devam edecek ve dinamik bir görünüm Çalıştır hello ilerledikçe verin.

Önceki çalıştırma geçmişlerini hello genel bakış dikey penceresinde hello Azure portal veya hello Visual Studio Cloud Explorer kullanılarak görüntülenebilir.

## <a name="creating-a-deployment-template-for-automated-deployments"></a>Otomatik dağıtımları için dağıtım şablonu oluşturma

Bir çözüm geliştirilen sonra yakalanan ve Azure dağıtım şablonu tooany Merhaba Dünya Azure bölgesinde aracılığıyla dağıtılır.  Bu parametre için de değiştirme bu iş akışı farklı sürümleri için aynı zamanda bu çözümü derleme ve sürüm ardışık düzeninde tümleştirmek için kullanışlıdır.  Bir dağıtım şablonu oluşturma hakkında ayrıntılar bulunabilir [bu makalede](logic-apps-create-deploy-template.md).

Merhaba tüm çözümü tüm bağımlılıkları tek bir şablon olarak yönetilecek şekilde azure işlevleri de hello dağıtım şablonunda - birleştirilebilir.  Bir işlev dağıtım şablonu örneği hello bulunabilir [Azure Hızlı Başlangıç şablonu deposu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).

## <a name="next-steps"></a>Sonraki adımlar

* [Diğer örnekleri ve senaryoları Azure Logic Apps için bkz.](logic-apps-examples-and-scenarios.md)
* [Bu çözüm uçtan uca Oluşturma videosu izleme](http://aka.ms/logicappsdemo)
* [Bilgi nasıl bir mantıksal uygulama içinde toohandle ve catch özel durumları](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: ./media/logic-apps-scenario-social-serverless/twitter.png
[2]: ./media/logic-apps-scenario-social-serverless/function.png