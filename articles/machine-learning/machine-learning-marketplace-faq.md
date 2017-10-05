---
title: "(kullanım dışı) SSS - yayımlama ve Azure Marketi'nde Machine Learning uygulamaları kullanma | Microsoft Docs"
description: "(kullanım dışı) Azure Marketi'nde yayımlama Machine Learning uygulamaları hakkında sık sorulan sorular"
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: a4631dfeb2f817b3a3c612a8f6af48398e4f2ab9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-the-azure-marketplace-faq"></a>(kullanım dışı) Yayımlama ve Azure Marketi'nde Machine Learning uygulamaları kullanan: sık sorulan sorular

> [!NOTE]
> DataMarket ve Veri Hizmetleri Çekildi ve mevcut abonelikleri kullanımdan kaldırılır ve başlangıç iptal 31/3/2017. Sonuç olarak, bu makalede onaylanmaz. 
> 
> Alternatif olarak, Machine Learning denemelerini yayımlayabilirsiniz [Cortana Intelligence Galerisi](https://gallery.cortanaintelligence.com/) veri bilimi topluluk yararlanması. Daha fazla bilgi için bkz: [paylaşımı ve Cortana Intelligence Galerisi kaynakları bulmak](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).


## <a name="questions-about-consuming-from-marketplace"></a>Marketten kullanma hakkında sorular
**1. Giriş için web hizmeti girdiğinizde neden aşağıdaki hata iletisini alın:**

**İstek bir arka uç zaman aşımı veya arka uç hata ile sonuçlandı. Ekibi sorunu Araştırıyor. Verdiğimiz rahatsızlıktan dolayı özür dileriz. (500)**

Giriş parametreleri belirli web hizmeti için gerekli biçime uygun olmayabilir. Giriş parametreleri için doğru biçimde ve bu web Hizmeti'nin sınırlamaları bulmak için ilgili belgeleri bağlantısına bakın.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**2. "Araştır bu veri kümesi" sayfası ve hangi kimlik bilgileri başka bir tarayıcı penceresine gerektiği Yapıştır bkz web hizmeti API bağlantı kopyalarsanız, sonuçları erişmek için kullandığım ve nasıl bunları görüyorum?**

Market hesap parolası olarak kullanıcı adı ve birincil hesap anahtarı kullanmalısınız. Birincil hesap anahtarı bulunabilir **bu veri kümesi keşfedin** sayfasında web hizmeti açıklaması altında (tıklatın **Göster** düğmesi). Sonucu tarayıcıda görüntüleyebilir veya indirilebilir olabilir, hangi tarayıcıya bağlı olarak, kullanmakta olduğunuz.

**3. Giriş için web hizmeti "Araştır bu veri kümesi" sayfasında girdiğim sonra neden aşağıdaki hata iletisini alın:** 

**İsteğiniz işlenirken beklenmeyen bir hata oluştu. Lütfen yeniden deneyin.**

Web hizmeti bir veya daha fazla giriş parametreleri uzunluk sınırını aştı Market'te web hizmeti kullanırken **bu veri kümesi keşfedin** sayfası. Hizmetleri artık bir giriş uzunluğunda HTTP POST yöntemleri kullanılarak çağrılabilir. Örnekler için bkz: [örnek R Machine Learning kullanan çözümler ve Markete yayımlanan](machine-learning-r-csharp-web-service-examples.md).

**4. Her şeyi "API'si GEZGİNİ" sekmesini int Klasik Azure portalı deposunda görmemin nedeni değil mi?** 

Bu, Azure Klasik portalı Market ile bilinen bir sorundur. Bu sorunu çözmek için takım çalışıyor. 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a>Azure Machine Learning Market'te yayımlama hakkında sorular
**1. Neden my hareketleri logolar veya görüntüleri değil web Hizmetimi yenileme?** 

Logo ve görüntüleri yayımlama portalında önbelleğe alınır ve yeni logo veya portalda güncelleştirmek için görüntü için 10 güne kadar sürebilir.

**2. My web hizmeti bir hata iletisi gösteren Market'te "Ayrıntı" sekmesinde neden oluyor?**

Azure Machine Learning hizmetinin ayrıntılarını bağlanırken bilinen bir Market sorun yoktur. Bu sorunu çözmek için takım çalışıyor.

**3. Neden Azure Machine Learning web hizmetleri R örnek kodda pazarında web hizmetlerini tüketen çalışmıyor?**

Azure Machine Learning web hizmetleri doğrudan Market üzerinden bu web hizmetlerine bağlanma karşılaştırıldığında bağlanırken kimlik doğrulama sistemleriyle farklıdır. Market Hizmetleri'nde OData hizmetler ve GET veya POST yöntemleri ile çağrılabilir. 

**4. My web hizmetinin destek bağlantıları neden olan doğru bazı my teklifleri için güncelleştirilmezse sunar?**

Yayımcı başına, Teklif başına değil genel destek bağlantılardır. 

**5. Marketi'nde nasıl toplu işlem giriş modu web hizmetiyle yayımlanacak?**

Toplu işlem giriş modu Market web hizmetleri şu anda desteklenmiyor.

**6. Kimin ı verileri yayımcısı olma hakkında sorularınız varsa ya da sorunlar yayımlama sırasında varsa Yardım almak için iletişim kuralım?**

Azure Market Ekibi temasa < mailto:datamarketbd@microsoft.com > daha fazla bilgi için.

