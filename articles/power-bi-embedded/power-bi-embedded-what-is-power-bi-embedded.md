---
title: Microsoft Power BI Embedded aaaWhat mi?
description: "Böylece, toobuild özel çözümler power BI Embedded toointegrate Power BI raporları web veya mobil uygulamaları sağlar."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 03649b72-b7d7-40ca-b077-12356d72d4f3
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/20/2017
ms.author: asaxton
ms.openlocfilehash: 0353938b6cdd9bb58b123b250f45f76b8cc7abe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-microsoft-power-bi-embedded"></a>Microsoft Power BI Embedded nedir?
İle **Power BI Embedded**, Power BI raporları sağ web veya mobil uygulamaları tümleştirebilirsiniz.

![](media/powerbi-embedded-whats-is/what-is.png)

Power BI Embedded olan bir **Azure hizmeti** ISV'ler sağlayan ve uygulama geliştiricileri toosurface Power BI veri uygulamalarını içinde karşılaştığında. Bir geliştirici olarak uygulamaları oluşturuncaya ve bu uygulamaları kendi kullanıcılar ve ayrı bir dizi özellik sahiptir. Bu uygulamalar ayrıca grafikleri ve artık Microsoft Power BI Embedded tarafından kapatılabilir raporları gibi bazı yerleşik veri öğeler toohave ortaya çıkabilir. Power BI hesabına toouse uygulamanız gerekmez. Önceden, olduğu gibi tooyour uygulamada toosign devam görüntüleyebilir ve herhangi bir ek lisans gerek kalmadan hello Power BI raporlama deneyimi ile etkileşim.

## <a name="licensing-for-microsoft-power-bi-embedded"></a>Microsoft Power BI lisansı katıştırılmış
Merhaba, **Microsoft Power BI Embedded** için Power BI hello sorumluluğu hello son kullanıcı lisans kullanım modeli.  Bunun yerine, **oturumları** hello görselleri tüketen hello uygulama hello geliştirici tarafından satın ve bu kaynakları sahibi toohello abonelik ücretlendirilirsiniz. Merhaba hakkında ek bilgiler bulunabilir [fiyatlandırma sayfası](https://azure.microsoft.com/en-us/pricing/details/power-bi-embedded/).

## <a name="microsoft-power-bi-embedded-conceptual-model"></a>Microsoft Power BI Embedded kavramsal model

![](media/powerbi-embedded-whats-is/model.png)

Herhangi diğer hizmetinde gibi Azure kaynakları için Power BI Embedded hello sağlanan [Azure Resource Manager API'leri](https://msdn.microsoft.com/library/mt712306.aspx). Bu durumda, sağladığınız hello kaynaktır bir **Power BI çalışma alanı koleksiyonu**.

## <a name="workspace-collection"></a>Çalışma alanı koleksiyonu
A **çalışma alanı koleksiyonu** 0 veya daha çok içeren hello en üst düzey Azure kaynakları için kapsayıcıdır **çalışma alanları**.  A **çalışma** **koleksiyonu** tüm hello standart Azure özelliklerinin yanı sıra hello aşağıdakileri içerir:

* **Erişim tuşları** – güvenli bir şekilde çağrılırken kullanılan anahtarları hello Power BI API'lerini (sonraki bölümde açıklanmıştır).
* **Kullanıcıların** – hello Azure portalında veya Azure Kaynak Yöneticisi API'si aracılığıyla yönetici hakları toomanage olan Azure Active Directory (AAD) kullanıcılar hello Power BI çalışma alanı koleksiyonu.
* **Bölge** – sağlama bir parçası olarak bir **çalışma alanı koleksiyonu**, derlemenizde bölge toobe seçebilirsiniz. Daha fazla bilgi için bkz: [Azure bölgeleri](https://azure.microsoft.com/regions/).

## <a name="workspace"></a>Çalışma alanı
A **çalışma** , bir Power BI veri kümelerini ve raporları aşağıdakileri içeren içerik, kapsayıcısıdır. A **çalışma** ilk oluşturduğunuz sırada boştur. Power BI Desktop kullanarak içerik yazmak ve program aracılığıyla hello PBIX hello kullanarak çalışma alanınıza dağıtacaksınız [Power BI içeri aktarma API'si](https://msdn.microsoft.com/library/mt711504.aspx). Program aracılığıyla da kümenizi oluşturun ve sonra Power BI Desktop kullanmak yerine, uygulamanızda raporlar oluşturun.

## <a name="using-workspace-collections-and-workspaces"></a>Çalışma alanı koleksiyonu ve çalışma alanlarını kullanma
**Çalışma alanı koleksiyonları** ve **çalışma alanları** kullanılan ve oluşturduğunuz Merhaba uygulaması hello tasarımını hangi şekilde en iyi sığacak düzenlenmiş içeriğinin kapsayıcılardır. Bunların hello içeriklerini düzenleme birçok farklı yolu olacaktır. Bir çalışma alanı içindeki tüm içeriği tooput seçebilir ve ardından sonraki kullanım uygulama belirteçleri toofurther ayırabilir müşterilerinizin arasında hello içeriği. Bunlar arasında bazı ayrımı olmasını sağlamak, ayrıca tooput tüm müşterilerinizin ayrı çalışma alanlarında seçebilirsiniz. Ya da bölgeye göre yerine müşteri tarafından tooorganize kullanıcıların tercih edebilirsiniz. Bu esnek tasarım toochoose hello en iyi şekilde tooorganize içerik da sağlar.

## <a name="cached-datasets"></a>Önbelleğe alınmış veri kümeleri
Önbelleğe alınan veri kümelerini kullanılabilir.  Ancak, içine yüklendikten sonra önbelleğe alınan veriler yenilenemiyor **Microsoft Power BI Embedded**. Önbelleğe alınan bir veri kümesi DirectQuery kullanmak yerine, Power BI Desktop'a hello veri aktardığınız anlamına gelir.

## <a name="authentication-and-authorization-with-app-tokens"></a>Kimlik doğrulama ve yetkilendirme uygulama belirteçleri ile
**Microsoft Power BI Embedded** tooyour uygulama tooperform tüm hello gerekli kullanıcı kimlik doğrulaması ve yetkilendirme erteler. Son kullanıcılarınızın Azure Active Directory (Azure AD) müşterileri olmasını açık gereksinimi yoktur.  Bunun yerine, uygulamanızın çok ifade**Microsoft Power BI Embedded** yetkilendirme toorender kullanarak bir Power BI raporu **uygulama kimlik doğrulama belirteçleri (uygulama belirteçleri)**.  Bunlar **uygulama belirteçleri** uygulamanızı toorender bir rapor istediğinde gerektiği şekilde oluşturulur.

![](media/powerbi-embedded-whats-is/app-tokens.png)

**Uygulama kimlik doğrulama belirteçleri (uygulama belirteçleri)** karşı kullanılan tooauthenticate olan **Microsoft Power BI Embedded**.  Üç tür vardır **uygulama belirteçleri**:

1. Yeni bir sağlama sırasında kullanılan belirteçleri - sağlama **çalışma** içine bir **çalışma alanı koleksiyonu**
2. Geliştirme belirteçleri - yapma doğrudan toohello çağırdığında kullanılan **Power BI REST API'leri**
3. Belirteçleri - çağrıları toorender yapılırken kullanılan katıştırma IFRAME hello rapora katıştırılmış

Bu belirteçler etkileşimlerinizi çeşitli aşamaları için hello kullanılan **Microsoft Power BI Embedded**.  Merhaba belirteçleri, uygulama tooPower BI izinleri verebilirsiniz şekilde tasarlanmıştır. Daha fazla bilgi için bkz: [uygulama belirteci akışı](power-bi-embedded-app-token-flow.md).

## <a name="create-or-edit-reports-within-your-application"></a>Oluşturma veya düzenleme uygulamanızdaki raporları

Düzen raporları mevcut veya toouse Power BI Desktop gerek kalmadan doğrudan uygulamanızda yeni raporlar oluşturmak artık kullanabilirsiniz. Bu, bir veri kümesi içinde çalışma alanınızı bulunmasını gerektirir.

## <a name="see-also"></a>Ayrıca bkz.

[Microsoft Power BI Embedded senaryoları](power-bi-embedded-scenarios.md)  
[Microsoft Power BI Embedded ile çalışmaya başlama](power-bi-embedded-get-started.md)  
[Bir örnek ile kullanmaya başlama](power-bi-embedded-get-started-sample.md)  
[Rapor ekleme](power-bi-embedded-embed-report.md)  
[Power BI Embedded ile kimlik doğrulaması ve yetkilendirme](power-bi-embedded-app-token-flow.md)  
[JavaScript Örnek Ekleme](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[Powerbı CSharp Git deposu](https://github.com/Microsoft/PowerBI-CSharp)  
[Powerbı düğümlü Git deposu](https://github.com/Microsoft/PowerBI-Node)  
Başka sorunuz mu var? [Merhaba Power BI topluluk deneyin](http://community.powerbi.com/)
