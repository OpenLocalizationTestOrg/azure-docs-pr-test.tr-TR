---
title: "Web hizmeti tooAzure Market öğrenme aaa(deprecated) Yayımla makine | Microsoft Docs"
description: "(kullanım dışı) Nasıl toopublish, Azure Machine Learning Web hizmeti toohello Azure Market"
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
redirect_document_id: True
ms.openlocfilehash: 149abc3df9b79c1b37d233d5e85e803592ff1020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-toohello-azure-marketplace"></a>(kullanım dışı) Azure Machine Learning Web hizmeti toohello Azure Marketi'nde yayımlama

> [!NOTE]
> DataMarket ve Veri Hizmetleri Çekildi ve mevcut abonelikleri kullanımdan kaldırılır ve başlangıç iptal 31/3/2017. Sonuç olarak, bu makalede onaylanmaz. 
> 
> Alternatif olarak, Machine Learning denemeleri toohello yayımlayabilirsiniz [Cortana Intelligence Galerisi](https://gallery.cortanaintelligence.com/) hello veri bilimi topluluğunun hello avantajı için. Daha fazla bilgi için bkz: [paylaşımı ve hello Cortana Intelligence Galerisi kaynakları bulmak](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).

Hello Azure Marketi hello toopublish Azure Machine Learning web hizmetleri ücretli olarak sağlayabilir veya dış müşterilere göre tüketimi için Hizmetleri boşaltın. Bu makalede başlattığınız bağlantılar tooguidelines tooget bu işlemine genel bakış sağlar. Bu işlemi kullanarak, web hizmetlerinizi diğer geliştiriciler tooconsume için kullanılabilir uygulamalarında yapabilirsiniz.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-hello-publishing-process"></a>İşlem yayımlama hello genel bakış
Merhaba, bir Azure Machine Learning web hizmeti tooAzure Market yayımlama hello adımları şunlardır:

1. Oluşturma ve makine öğrenme istek-yanıt hizmeti (RRS) yayımlama
2. Merhaba hizmet tooproduction dağıtmak ve hello API anahtarı ve OData uç nokta bilgileri alın.
3. Hello kullan hello URL'sini yayımlanan web hizmeti toopublish çok[Azure Marketi (veri Pazar)](https://publish.windowsazure.com/workspace/) 
4. Sonra gönderildi, teklifiniz incelenir ve bu satın alma, müşterilerinizin önce onaylanan toobe başlatabilirsiniz. Merhaba yayımlama işlemi birkaç iş gün sürebilir. 

## <a name="walk-through"></a>İzlenecek yol
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a>1. adım: Oluşturma ve makine öğrenme istek-yanıt hizmeti (RRS) yayımlama
 Siz bunu zaten yapmadıysanız, lütfen bu göz atın [size yol](machine-learning-walkthrough-5-publish-web-service.md).

### <a name="step-2-deploy-hello-service-tooproduction-and-obtain-hello-api-key-and-odata-endpoint-information"></a>2. adım: hello hizmet tooproduction dağıtmak ve hello API anahtarı ve OData uç nokta bilgileri alın
1. Merhaba gelen [Klasik Azure portalı](http://manage.windowsazure.com)seçin hello **MACHINE LEARNING** seçeneği hello sol gezinti çubuğunda ve çalışma alanınızı seçin. 
2. Tıklatın hello üzerinde **WEB Hizmetleri** sekmesi ve toopublish toohello Market istediğinizi seçin hello web hizmeti.
   
    ![Azure Market][workspace]
3. Select hello uç noktası, toohave hello Market gibi kullanır. Ek uç nokta oluşturmadıysanız hello seçebilirsiniz **varsayılan** uç noktası.
4. Merhaba noktadaki tıklattıktan sonra mümkün toosee hello olacaktır **API anahtarı**. Bu parça gerekir adım 3'te daha sonra daha fazla bilgi için bu nedenle bir kopyasını oluşturun.
   
    ![Azure Market][apikey]
5. Tıklatın hello üzerinde **istek/yanıt** değil destekliyoruz yayımlama toplu iş yürütme bu noktada yöntemi toohello Market Hizmetleri. Sizi hello istek/yanıt yöntemi yönelik toohello API yardım sayfasına götürür.
6. Kopya hello **OData uç noktası adresi**, adım 3'te daha sonra bu bilgilere ihtiyacınız olacaktır.
   
    ![Azure Market][odata]

Merhaba hizmeti üretime dağıtma.

### <a name="step-3-use-hello-url-of-hello-published-web-service-toopublish-tooazure-marketplace-datamarket"></a>3. adım: Web hizmeti toopublish tooAzure Market (DataMarket) hello kullan hello URL'sini yayımlanan
1. Çok gidin[Azure Marketi (veri Pazar)](http://datamarket.azure.com/home) 
2. Tıklatın hello üzerinde **Yayımla** hello sayfanın üst kısmındaki hello bağlantı. Bu toohello sürecek [Microsoft Azure yayımlama portalında](https://publish.windowsazure.com)
3. Tıklatın hello üzerinde **yayımcılar** bölüm tooregister bir yayımcı olarak.
4. Yeni bir teklif oluştururken seçin **Veri Hizmetleri**, ardından **yeni bir veri hizmeti oluşturma**. 
   
   ![Azure Market][image1]
   
   <br />
5. Altında **planları** fiyatlandırma planı dahil olmak üzere, teklifi hakkında bilgi sağlar. Boş ya da Ücretli bir hizmet sunacaktır varsa karar verin. Ücretli, tooget banka ve vergi bilgilerinizi gibi ödeme bilgilerini sağlar.
6. Altında **pazarlama** teklifiniz için hello başlık ve açıklama gibi teklifiniz hakkında bilgi sağlar.
7. Altında **fiyatlandırma** planlarınızı belirli ülkeler için için hello fiyat ayarlayabilir veya hello sistem "autoprice" teklifiniz olanak tanır.
8. Merhaba üzerinde **veri hizmeti** sekmesini tıklatın, **Web hizmeti** hello olarak **veri kaynağı**.
   
    ![Azure Market][image2]
9. Merhaba, web hizmeti URL'sini ve API anahtarını yukarıda 2. adımda açıklandığı gibi Klasik Azure portalı, hello alın.
10. Merhaba Market veri hizmeti Kurulumu iletişim kutusunda, hello OData uç noktası adresi hello yapıştırma **hizmeti URL'si** metin kutusu.
11. İçin **kimlik doğrulaması**, seçin **üstbilgi** hello olarak **kimlik doğrulama düzeni**.
    
    * "Yetkilendirme" Merhaba girin **üstbilgi adı**.
    * Hello için **üstbilgi değeri**, "Bearer" (Merhaba tırnak işaretleri olmadan) girin, hello tıklatın **alanı** çubuk ve hello API anahtarını yapıştırın.
    * Select hello **bu hizmetidir OData** onay kutusu.
    * Tıklatın **Bağlantıyı Sına** tootest hello bağlantı.
12. Altında **kategorileri**, olun **Machine Learning** seçilir.
13. İşiniz bittiğinde meta verileri hello tüm girme teklifiniz hakkında tıklayın **Yayımla**ve ardından **anında tooStaging**. Bu noktada, tüm kalan sorunlarını toofix gerektiğini bildirilir.
14. Tüm hello bekleyen sorunları tamamlanmasından doğruladıktan sonra tıklatın **isteği onay toopush tooProduction**. Merhaba yayımlama işlemi birkaç iş gün sürebilir. 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

