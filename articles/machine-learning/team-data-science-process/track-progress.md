---
title: "Veri bilimi projeleri - Azure Machine Learning yürütülmesi | Microsoft Docs"
description: "Nasıl veri Bilimcisi veri bilimi proje ilerlemesini izleyebilirsiniz."
documentationcenter: 
author: bradsev
manager: cgronlun
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2017
ms.author: bradsev;
ms.openlocfilehash: c8e1882570a8cfcb4a75f0904a2138d007e0bc5b
ms.sourcegitcommit: cfd1ea99922329b3d5fab26b71ca2882df33f6c2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/30/2017
---
# <a name="track-progress-of-data-science-projects"></a>Veri bilimi projeleri ilerlemesini izlemek

Veri bilimi grup yöneticileri, takım müşteri adayları ve takım projelerini ilerlemesini izlemek için Proje müşteri adayları gereksinimi, hangi iş bunlardaki ve kim tarafından yapılır ve yapılacaklar listelerinde üzerinde kalır. 

## <a name="vsts-dashboards"></a>VSTS panoları
Visual Studio Team Services (VSTS) kullanıyorsanız, derleme panoları etkinliklerini ve verilen Çevik proje ile ilişkili iş öğelerini izlemek için kullanabilirsiniz. 

Oluşturma ve panolar ve Visual Studio Team Services pencere öğeleri özelleştirme hakkında daha fazla bilgi için aşağıdaki yönergeleri bakın:

- [Ekleme ve panolar yönetme](https://docs.microsoft.com/vsts/report/dashboards/dashboards)
- [Bir Pano pencere öğeleri ekleyin](https://docs.microsoft.com/vsts/report/dashboards/add-widget-to-dashboard).

## <a name="example-dashboard"></a>Örnek Pano

Burada, ilişkili depoları yürütme sayısı yanı sıra, Çevik veri bilimi projesinde sprint etkinliklerini izlemek için yerleşik bir basit bir örnek Pano verilmiştir. **Üst sol** panel gösterir:

- geri sayım geçerli oturumla 
- Son 7 gün içinde her depo yürütme sayısı
- belirli kullanıcılar için iş öğesi. 

Kalan paneller toplu akış diyagramı (CFD), burndown ve bir proje için burnup göster:

- **Sol alt**: mavi renkte kaydedilen ve yeşil bitti gri onaylanan gösteren CFD belirli bir durumda iş miktarı.
- **Sağ üst**: burndown grafik karşı kalan süre tamamlamak için kalan çalışma).
- **Sağ alt**: burnup grafik toplam çalışma miktarı karşı tamamlanmış iş.

![pano](./media/track-progress/dashboard.png)

Bu grafikler oluşturma açıklaması için bkz: quickstarts ve öğreticiler adresindeki [panolar](https://docs.microsoft.com/vsts/report/dashboards/).
 
## <a name="next-steps"></a>Sonraki adımlar

İşlem için tüm adımları gösteren talimatlara **belirli senaryolar** de sağlanır. Listelenen ve küçük resim açıklamasında ile bağlantılı [örnek izlenecek yollar](walkthroughs.md) makalesi. Bunlar, bulut, şirket içi araçları ve Hizmetleri bir iş akışı veya akıllı bir uygulama oluşturmak için ardışık düzen birleştirmek nasıl koruduğu gösterilmiştir. 
