---
title: "Machine Learning web hizmetleri için aaaLogging | Microsoft Docs"
description: "Bilgi nasıl tooenable günlüğü için Machine Learning web hizmetleri. Günlük toohelp hello API'leri sorun giderme ek bilgi sağlar."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: ed23933d52d2151af658af2307d7df8743071f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a>Machine Learning web hizmetleri için günlüğe kaydetmeyi etkinleştirme
Bu belge Machine Learning web hizmetlerini yeteneğini günlüğü hello hakkında bilgi sağlar. Günlük yalnızca bir hata numarası ve, Machine Learning API çağrıları toohello gidermenize yardımcı olabilecek bir ileti ötesinde ek bilgi sağlar.  

## <a name="how-tooenable-logging-for-a-web-service"></a>Nasıl bir Web hizmeti için tooenable günlüğü

Merhaba günlüğe etkinleştirmek [Azure Machine Learning Web Hizmetleri](https://services.azureml.net) portal. 

1. Toohello Azure Machine Learning Web Hizmetleri portalında oturum [https://services.azureml.net](https://services.azureml.net). Klasik web hizmeti, ayrıca toohello portal tıklayarak alabilirsiniz **yeni Web Hizmetleri deneyiminizin** Machine Learning Studio'da hello Machine Learning Web Hizmetleri sayfasında.

   ![Yeni Web Hizmetleri deneyiminizin bağlantısı](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. Merhaba üst menü çubuğunda **Web Hizmetleri** için yeni web hizmeti veya tıklatın **Klasik Web Hizmetleri** için Klasik web hizmeti.

   ![Yeni veya Klasik web hizmetleri seçin](media/machine-learning-web-services-logging/select-web-service.png)

3. Yeni bir web hizmeti için hello web hizmeti adına tıklayın. Klasik web hizmeti hello web hizmeti adına tıklayın ve hello uygun endpoint hello sonraki sayfada'ı tıklatın.

4. Merhaba üst menü çubuğunda **yapılandırma**.

5. Set hello **Enable Logging** çok seçenek*hata* (toolog yalnızca hatalar) veya *tüm* (için tam günlük kaydı).

   ![Günlük düzeyini seçin](media/machine-learning-web-services-logging/enable-logging.png)

6. **Kaydet** düğmesine tıklayın.

7. Klasik web hizmetleri için hello oluşturmanız **ml tanılama** kapsayıcı.

   Tüm web hizmeti günlükleri adlı blob kapsayıcısında tutulur **ml tanılama** hello depolama hesabındaki hello web hizmeti ile ilişkilendirilmiş. Yeni web hizmetleri için bu kapsayıcı hello web hizmetine erişim ilk kez hello oluşturulur. Klasik web hizmetleri için zaten yoksa toocreate hello kapsayıcı gerekir. 

   1. Merhaba, [Azure portal](https://portal.azure.com)gidin hello web hizmeti ile ilişkili toohello depolama hesabı.

   2. Altında **Blob hizmeti**, tıklatın **kapsayıcıları**.

   3. Varsa hello kapsayıcı **ml tanılama** mevcut değil,'ı tıklatın **+ kapsayıcı**hello kapsayıcı hello adı "ml-Tanılama" verin ve seçin hello **erişim türüne** "Blob" olarak. **Tamam** düğmesine tıklayın.

      ![Günlük düzeyini seçin](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> Klasik web hizmeti, hello Web Hizmetleri Pano Machine Learning Studio'da bir geçiş tooenable günlük de vardır. Ancak, günlük şimdi hello Web Hizmetleri Portalı aracılığıyla yönetildiğinden dolayı bu makalesinde açıklandığı gibi hello portal üzerinden oturum tooenable gerekir. Studio'da oturum zaten etkinleştirilmişse hello Web Hizmetleri portalı, günlüğü devre dışı bırakın ve yeniden etkinleştirin.


## <a name="hello-effects-of-enabling-logging"></a>Merhaba etkilerini günlüğünü etkinleştirme
Günlük kaydı etkinleştirildiğinde, hello tanılama ve hello web hizmeti uç noktası hatalarından hello kaydedilir **ml tanılama** hello Azure depolama hesabı blob kapsayıcısında hello kullanıcının çalışma ile bağlantılı. Bu kapsayıcıdaki tüm hello web hizmeti uç noktaları için bu depolama hesabıyla ilişkili tüm hello çalışma alanları için tüm hello tanılama bilgileri tutar.

Merhaba günlükleri hello birini çeşitli araçlar kullanılabilir tooexplore Azure Storage hesabını kullanarak görüntülenebilir. Hello kolay toonavigate toohello depolama hesabında hello Azure portal olması, tıklatın **kapsayıcıları**ve ardından hello kapsayıcı **ml tanılama**.  

## <a name="log-blob-detail-information"></a>Günlük blob ayrıntı bilgileri
Merhaba kapsayıcıdaki her blob tam olarak bir eylemler aşağıdaki hello hello tanılama bilgilerini içerir:

* Merhaba toplu iş yürütme yönteminin yürütülmesi  
* Bir yürütme hello istek-yanıt yöntemi  
* İstek-yanıt kapsayıcı başlatma

Her bir blob Hello adını form aşağıdaki hello öneki vardır: 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


Burada _oturum türü_ değerleri aşağıdaki hello biridir:  

* Toplu işlem  
* puan/istekleri  
* puan/başlatma  

