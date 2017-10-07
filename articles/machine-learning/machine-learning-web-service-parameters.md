---
title: Azure Machine Learning Web hizmeti parametreleri aaaUse | Microsoft Docs
description: "Nasıl toouse Azure Machine Learning Web hizmeti parametreleri toomodify hello modelinizi davranışını hello web hizmeti erişildiğinde."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c49187db-b976-4731-89d6-11a0bf653db1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2017
ms.author: raymondl;garye
ms.openlocfilehash: 214711eb819a6cea34db905abdf015da11e846d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-web-service-parameters"></a>Azure Machine Learning Web Hizmeti Parametrelerini kullanma
Bir Azure Machine Learning web hizmetini yapılandırılabilir parametrelerle modülleri içeren bir denemeyi yayımlayarak oluşturulur. Bazı durumlarda, Hello web hizmeti çalışırken toochange hello modülü davranışı isteyebilirsiniz. *Web hizmeti parametreleri* toodo izin bu görev. 

Yaygın bir örnek hello ayarı [veri içeri aktarma] [ reader] hello web hizmeti erişildiğinde web hizmeti, bu hello kullanıcıyı hello yayımlanan şekilde modülü farklı bir veri kaynağına belirtebilirsiniz. Veya hello yapılandırma [verileri dışa aktar] [ writer] modülü böylece farklı bir hedef belirtilebilir. Bazı diğer hello BITS hello sayısını değiştirme örnekler [özellik karma] [ feature-hashing] hello için istenen özelliklerini modül veya hello sayısı [filtre tabanlı özellik seçimi] [ filter-based-feature-selection] modülü. 

Web hizmeti parametreleri ayarlayabilir ve bunları bir veya daha fazla modülü parametrelerle denemenizde ilişkilendirmeyi ve gerekli veya isteğe bağlı oldukları belirtebilirsiniz. Merhaba web hizmetini çağırdığınızda hello kullanıcı hello web hizmetinin bu parametreler için değerler sonra sağlayabilir. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-tooset-and-use-web-service-parameters"></a>Nasıl tooset ve kullanım Web hizmeti parametreleri
Bir modül hello simgesi sonraki toohello parametresi tıklatıp "web hizmeti parametresi Ayarla" seçerek bir Web hizmeti parametre tanımlayın. Bu yeni bir Web hizmeti parametre oluşturur ve toothat modülü parametre bağlanır. Sonra hello web hizmeti erişildiğinde hello kullanıcı hello Web hizmeti parametresi için bir değer belirtebilirsiniz ve uygulanan toohello modülü parametresi bağlıdır.

Bir Web hizmeti parametresi tanımladıktan sonra kullanılabilir tooany olan hello deneme başka bir modül parametre. Bir modül için bir parametre ile ilişkili bir Web hizmeti parametresi tanımlarsanız, aynı değerini yazın hello hello parametre bekliyor sürece, aynı Web hizmeti parametresi diğer herhangi bir modül için kullanabilirsiniz. Merhaba Web hizmeti parametresi bir sayısal değer ise, örneğin, daha sonra yalnızca sayısal bir değer beklediğiniz modülü parametreleri için kullanılabilir. Merhaba kullanıcı hello Web hizmeti parametresi için bir değer ayarlar ilişkili uygulanan tooall modülü parametreleri olacaktır.

Karar verebilirsiniz tooprovide varsayılan hello Web hizmeti parametresi için değer olup olmadığını. Ardından Merhaba varsa parametre hello web hizmeti hello kullanıcı için isteğe bağlıdır. Varsayılan değer sağlamazsanız, hello web hizmeti erişildiğinde hello kullanıcı gerekli tooenter bir değer ise.

Merhaba hello web hizmeti için API belgeleri nasıl toospecify hello Web hizmeti parametresi program aracılığıyla hello web hizmeti erişirken üzerinde hello web hizmeti kullanıcı için bilgileri içerir.

> [!NOTE]
> Merhaba sağlanan bir Klasik web hizmeti için API belgelerine hello **API Yardım sayfası** hello web hizmeti bağlantı **PANO** Machine Learning Studio'da. Yeni bir web hizmeti ile Merhaba sağlanan için API belgelerine hello [Azure Machine Learning Web Hizmetleri](https://services.azureml.net/Quickstart) hello portalını **Tüket** ve **Swagger API'si** için sayfaları, Web hizmeti.
> 
> 

## <a name="example"></a>Örnek
Bir örnek, bir deneme ile sahibiz varsayalım bir [verileri dışa aktar] [ writer] bilgi tooAzure blob depolamaya gönderir modülü. Web hizmeti "yol Blob" adlı bir parametre tanımlama olasılığınız yüksektir hello hizmet erişildiğinde hello web hizmeti kullanıcı toochange hello yolu toohello blob depolama veren.

1. Machine Learning Studio'da hello tıklatın [verileri dışa aktar] [ writer] modülü tooselect. Itanium tabanlı sistemler için hello Özellikler bölmesinde toohello hello deneme tuvalinin sağında içinde özelliklerini gösterilmektedir.
2. Merhaba depolama türünü belirtin:
   
   * Altında **Lütfen verileri hedef belirtin**, "Azure Blob Storage" seçin.
   * Altında **Lütfen kimlik doğrulama türünü belirtin**, "Hesap" seçin.
   * Hello Azure blob depolama için Hello hesap bilgilerini girin. 
     <p />
3.Merhaba simgesi toohello hello sağına tıklayın **kapsayıcı parametresi tooblob başlayan yol**. Şöyle görünür:
   
   ![Web hizmeti parametresi simgesi][icon]
   
   "Web hizmeti parametresi Ayarla" seçin.
   
   Bir giriş altında eklenen **Web hizmeti parametreleri** hello Özellikler bölmesinde hello adı "yol tooblob ile başlayan kapsayıcı" Merhaba sonundaki. Merhaba artık Web hizmeti parametresi budur bununla ilişkili [verileri dışa aktar] [ writer] modülü parametresi.
4. toorename Web hizmeti parametresi Merhaba, hello adına tıklayın, "yol Blob" girin ve basın hello **Enter** anahtarı. 
5. tooprovide hello Web hizmeti parametresi için varsayılan bir değer hello simgesi toohello hello adını sağ tıklatın, "varsayılan değer sağla" seçin, bir değer (örneğin, "container1/output1.csv") girin ve basın hello **Enter** anahtarı.
   
   ![Web hizmeti parametresi][parameter]
6. **Çalıştır**’a tıklayın. 
7. Tıklatın **Web hizmeti Dağıt** seçip **Web hizmeti Dağıt [Klasik]** veya **Web hizmeti dağıtma [Yeni]** toodeploy hello web hizmeti.

> [!NOTE] 
> toodeploy yeni bir web hizmeti yeterli izniniz hello abonelik toowhich, hello web Hizmeti'ni dağıtma olması gerekir. Daha fazla bilgi için [hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir Web hizmeti yönetmek](machine-learning-manage-new-webservice.md). 

Merhaba web hizmetinin Hello kullanıcı artık hello için yeni bir hedef belirtin [verileri dışa aktar] [ writer] hello web hizmeti erişirken modülü.

## <a name="more-information"></a>Daha fazla bilgi
Merhaba daha ayrıntılı bir örnek için bkz: [Web hizmeti parametreleri](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) hello girişi [Machine Learning Blog](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).

Machine Learning web hizmetine erişim ile ilgili daha fazla bilgi için bkz: [nasıl tooconsume bir Azure Machine Learning Web hizmeti](machine-learning-consume-web-services.md).

<!-- Images -->
[icon]: ./media/machine-learning-web-service-parameters/icon.png
[parameter]: ./media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/

