---
title: "(kullanım dışı) Machine learning yayımlama web hizmeti Azure Marketi'nde | Microsoft Docs"
description: "(kullanım dışı) Azure Machine Learning Web hizmetinizi Azure Marketinde yayımlama"
services: machine-learning
documentationcenter: 
author: BharathS
manager: jhubbard
editor: cgronlun
ms.assetid: 68e908be-3a99-4cd7-9517-e2b5f2f341b8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: machine-learning-gallery-experiments
redirect_document_id: TRUE
ms.openlocfilehash: 3e3420872f0c604e027d1f309a6de6f52a5a788c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-to-the-azure-marketplace"></a>(kullanım dışı) Azure Machine Learning Web hizmeti Azure Marketi'nde yayımlama

> [!NOTE]
> DataMarket ve Veri Hizmetleri Çekildi ve mevcut abonelikleri kullanımdan kaldırılır ve başlangıç iptal 31/3/2017. Sonuç olarak, bu makalede onaylanmaz. 
> 
> Alternatif olarak, Machine Learning denemelerini yayımlayabilirsiniz [Cortana Intelligence Galerisi](https://gallery.cortanaintelligence.com/) veri bilimi topluluk yararlanması. Daha fazla bilgi için bkz: [paylaşımı ve Cortana Intelligence Galerisi kaynakları bulmak](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).

Azure Market Ücretli gibi Azure Machine Learning web hizmetleri yayımlamak ya da dış müşterilere göre tüketimi için Hizmetleri serbest özelliği sağlar. Bu makalede başlamanıza yardımcı olacak yönergeler için bağlantılar ile birlikte bu işlemine genel bakış sağlar. Bu işlemi kullanarak, web hizmetlerinizi diğer geliştiricilerin uygulamalarında kullanmak kullanılabilir yapabilirsiniz.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-the-publishing-process"></a>Yayımlama işlemine genel bakış
Bir Azure Machine Learning web hizmeti Azure Marketinde yayımlama için adımlar şunlardır:

1. Oluşturma ve makine öğrenme istek-yanıt hizmeti (RRS) yayımlama
2. Hizmeti üretime dağıtmak ve API anahtarı ve OData uç nokta bilgileri alın.
3. Yayımlamak için yayımlanan web hizmetinin URL'sini kullanın [Azure Marketi (veri Pazar)](https://publish.windowsazure.com/workspace/) 
4. Sonra gönderildi, teklifiniz incelenir ve müşterilerinizin önce onaylanması, satın almayı başlatmak için. Yayımlama işlemi birkaç iş gün sürebilir. 

## <a name="walk-through"></a>İzlenecek yol
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a>1. adım: Oluşturma ve makine öğrenme istek-yanıt hizmeti (RRS) yayımlama
 Siz bunu zaten yapmadıysanız, lütfen bu göz atın [size yol](machine-learning-walkthrough-5-publish-web-service.md).

### <a name="step-2-deploy-the-service-to-production-and-obtain-the-api-key-and-odata-endpoint-information"></a>Adım 2: hizmeti üretime dağıtmak ve API anahtarı ve OData uç nokta bilgileri elde etmek
1. Gelen [Klasik Azure portalı](http://manage.windowsazure.com)seçin **MACHINE LEARNING** seçeneği sol gezinti çubuğu'ndan ve çalışma alanınızı seçin. 
2. Tıklayın **WEB Hizmetleri** sekmesini tıklatın ve Market'te yayımlamak istediğiniz web hizmetini seçin.
   
    ![Azure Market][workspace]
3. Tüketen Market olmasını istediğiniz uç nokta seçin. Ek uç nokta oluşturmadıysanız, seçebileceğiniz **varsayılan** uç noktası.
4. Uç noktada tıklattıktan sonra görmeye olacaktır **API anahtarı**. Bu parça gerekir adım 3'te daha sonra daha fazla bilgi için bu nedenle bir kopyasını oluşturun.
   
    ![Azure Market][apikey]
5. Tıklayın **istek/yanıt** değil destekliyoruz Marketi'nde yayımlama toplu iş yürütme Hizmetleri bu noktada yöntemi. Sizi istek/yanıt yöntemi için API yardım sayfasına götürür.
6. Kopya **OData uç noktası adresi**, adım 3'te daha sonra bu bilgilere ihtiyacınız olacaktır.
   
    ![Azure Market][odata]

Hizmet üretime dağıtma.

### <a name="step-3-use-the-url-of-the-published-web-service-to-publish-to-azure-marketplace-datamarket"></a>3. adım: Azure Marketi (DataMarket) yayımlamak için yayımlanan web hizmetinin URL'sini kullanın.
1. Gidin [Azure Market (veri Pazar)](http://datamarket.azure.com/home) 
2. Tıklayın **Yayımla** sayfanın üst kısmındaki bağlantı. Bu, olanak sürecek [Microsoft Azure yayımlama portalında](https://publish.windowsazure.com)
3. Tıklayın **yayımcılar** bir yayımcı olarak kaydetmek için bölüm.
4. Yeni bir teklif oluştururken seçin **Veri Hizmetleri**, ardından **yeni bir veri hizmeti oluşturma**. 
   
   ![Azure Market][image1]
   
   <br />
5. Altında **planları** fiyatlandırma planı dahil olmak üzere, teklifi hakkında bilgi sağlar. Boş ya da Ücretli bir hizmet sunacaktır varsa karar verin. Ücretli için Banka ve vergi bilgilerinizi gibi ödeme bilgilerini sağlayın.
6. Altında **pazarlama** başlığı ve açıklamayı teklifiniz için gibi teklifiniz hakkında bilgi sağlar.
7. Altında **fiyatlandırma** planlarınızı belirli ülkeler için fiyat ayarlamak veya "autoprice" Sistem teklifiniz olanak tanır.
8. Üzerinde **veri hizmeti** sekmesini tıklatın, **Web hizmeti** olarak **veri kaynağı**.
   
    ![Azure Market][image2]
9. Yukarıdaki 2. adımda açıklandığı gibi web hizmeti URL'sini ve API anahtarını Azure Klasik portalından alın.
10. OData uç nokta adresine Market veri hizmeti Kurulumu iletişim kutusuna yapıştırın **hizmeti URL'si** metin kutusu.
11. İçin **kimlik doğrulaması**, seçin **üstbilgi** olarak **kimlik doğrulama düzeni**.
    
    * "Yetkilendirme" girin **üstbilgi adı**.
    * İçin **üstbilgi değeri**, "Bearer" (tırnak işaretleri olmadan) girin, tıklatın **alanı** çubuk ve API anahtarını yapıştırın.
    * Seçin **bu hizmetidir OData** onay kutusu.
    * Tıklatın **Bağlantıyı Sına** test edin.
12. Altında **kategorileri**, olun **Machine Learning** seçilir.
13. İşiniz bittiğinde, teklif hakkında tüm meta veri girme tıklatın **Yayımla**ve ardından **anında hazırlık**. Bu noktada, düzeltmek için gereken tüm kalan sorunlarını bildirilir.
14. Tüm bekleyen sorunları tamamlanmasından doğruladıktan sonra tıklatın **üretime gönderme için onay isteği**. Yayımlama işlemi birkaç iş gün sürebilir. 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

