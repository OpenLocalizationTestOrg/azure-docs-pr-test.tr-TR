---
title: "AAA(deprecated) SSS - yayımlama ve Azure Marketi'nde Machine Learning uygulamaları kullanma | Microsoft Docs"
description: "(kullanım dışı) Yayımlama hello Azure Marketi Machine Learning uygulamaları hakkında sık sorulan sorular"
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
redirect_document_id: True
ms.openlocfilehash: b3ae45dfff211fe9baccaf54faaf360a8309c780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-hello-azure-marketplace-faq"></a>(kullanım dışı) Yayımlama ve Machine Learning uygulamaları hello Azure Marketi kullanma: sık sorulan sorular

> [!NOTE]
> DataMarket ve Veri Hizmetleri Çekildi ve mevcut abonelikleri kullanımdan kaldırılır ve başlangıç iptal 31/3/2017. Sonuç olarak, bu makalede onaylanmaz. 
> 
> Alternatif olarak, Machine Learning denemeleri toohello yayımlayabilirsiniz [Cortana Intelligence Galerisi](https://gallery.cortanaintelligence.com/) hello veri bilimi topluluğunun hello avantajı için. Daha fazla bilgi için bkz: [paylaşımı ve hello Cortana Intelligence Galerisi kaynakları bulmak](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).


## <a name="questions-about-consuming-from-marketplace"></a>Marketten kullanma hakkında sorular
**1. Giriş hello web hizmeti için girdiğinizde hata iletisi aşağıdaki hello neden alın:**

**Merhaba isteği bir arka uç zaman aşımı veya arka uç hata ile sonuçlandı. Merhaba takım hello sorunu Araştırıyor. Merhaba rahatsızlıktan dolayı özür dileriz. (500)**

Giriş parametreleri toohello gerekli biçime hello belirli web hizmeti için uygun olmayabilir. Lütfen toohello karşılık gelen belgeleri bağlantı toofind hello doğru biçim giriş parametreleri ve bu web Hizmeti'nin hello sınırlamaları için bakın.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**2. Bunları görüyorum hello API bağlantı üzerinde "Araştır bu veri kümesi" sayfası hello ve başka bir tarayıcı penceresine, hangi kimlik bilgileri ı tooaccess hello sonuçları kullanın ve nasıl yapıştırın görüyorum hello web hizmeti kopyalarsanız?**

Market hesabınızı hello kullanıcı adı ve hello birincil hesap anahtarı hello parola olarak kullanmanız gerekir. Hello birincil hesap anahtarı hello üzerinde bulunabilir **bu veri kümesi keşfedin** sayfasında hello hello web hizmeti açıklaması altında (hello tıklatın **Göster** düğmesi). Merhaba sonuç hello tarayıcıda görüntüleyebilir veya çok kullanılabilir olabilir hangi tarayıcıya bağlı olarak kullanmakta olduğunuz yükleme.

**3. I hello giriş hello web hizmeti için hello "Araştır bu veri kümesi" sayfasında girdikten sonra aşağıdaki hata iletisini hello neden alın:** 

**İsteğiniz işlenirken beklenmeyen bir hata oluştu. Lütfen yeniden deneyin.**

Web hizmeti bir veya daha fazla giriş parametreleri sınırı aştı hello uzunluk sınırını hello web hizmeti hello Market'te kullanırken **bu veri kümesi keşfedin** sayfası. Merhaba Hizmetleri artık bir giriş uzunluğunda HTTP POST yöntemleri kullanılarak çağrılabilir. Örnekler için bkz: [örnek R Machine Learning ve yayımlanan tooMarketplace kullanan çözümler](machine-learning-r-csharp-web-service-examples.md).

**4. Her şeyi hello "API'si GEZGİNİ" sekmesini int hello deposu hello Klasik Azure portalı görmemin nedeni değil mi?** 

Bu, Azure Klasik portalı Market hello ile bilinen bir sorundur. Merhaba takım tooresolve bu sorunu çalışmaktadır. 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a>Azure Machine Learning Market'te yayımlama hakkında sorular
**1. Neden my hareketleri logolar veya görüntüleri değil web Hizmetimi yenileme?** 

Logo ve görüntüleri yayımlama hello Portalı'nda önbelleğe alınır ve too10 günlerini hello yeni logo veya görüntü tooupdate hello portalındaki sürebilir.

**2. My web hizmeti bir hata iletisi gösteren Market'te hello "Ayrıntı" sekmesinde neden oluyor?**

Hizmet ayrıntıları için Machine Learning tooAzure bağlanırken bilinen bir Market sorun yoktur. Merhaba takım tooresolve bu sorunu çalışmaktadır.

**3. Neden Market Süren hello web hizmetleri için hello R örnek kodda hello Azure Machine Learning web hizmetleri çalışmıyor?**

tooAzure Machine Learning web hizmetleri doğrudan bağlanma tooconnecting toothese web hizmetleri hello Market üzerinden karşılaştırıldığında hello kimlik doğrulama sistemleriyle farklıdır. Market Hello Hizmetleri'nde OData hizmetler ve GET veya POST yöntemleri ile çağrılabilir. 

**4. Merhaba destek bağlantıları my web hizmetinin neden olan doğru bazı my teklifleri için güncelleştirilmezse sunar?**

Merhaba destek bağlantıları genel yayımcı başına, Teklif başına değil. 

**5. Marketi'nde nasıl toplu işlem giriş modu web hizmetiyle yayımlanacak?**

Merhaba toplu giriş modu Market web hizmetleri şu anda desteklenmiyor.

**6. Kimin t ile irtibata geçmelidir tooget Yardım verileri yayımcısı olma hakkında sorularınız varsa veya sorunları yayımlama sırasında varsa?**

Hello Azure Market Ekibi temasa < mailto:datamarketbd@microsoft.com > daha fazla bilgi için.

