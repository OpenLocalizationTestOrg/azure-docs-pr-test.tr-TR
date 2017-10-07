---
title: "aaaRetrain makine öğrenimi modeline | Microsoft Docs"
description: "Web hizmeti toouse hello yeni eğitilen modeli Azure Machine learning'de tooretrain bir model ve güncelleştirme nasıl hello öğrenin."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: d1cb6088-4f7c-4c32-94f2-f7523dad9059
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 342bb9954105339b4b634ff20968a64f4f9f750e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-machine-learning-model"></a>Machine Learning modelini çağırma
Azure Machine Learning makine öğrenimi modellerinin operationalization hello sürecinin bir parçası olarak, modelinizi eğitilmiş ve kaydedilir. Ardından toocreate predicative bir Web hizmetini kullanırsınız. Merhaba Web hizmeti web siteleri, panolar ve mobil uygulamaları tüketilebilir. 

Machine Learning kullanarak oluşturduğunuz modelleri genellikle statik değildir. Yeni veriler kullanılabilir olduğunda ya da hello API hello tüketicisi varsa, kendi veri hello modeli retrained toobe gerekir. 

Yeniden eğitme sık oluşabilir. Merhaba programlı yeniden eğitme API özelliğiyle hello yeniden eğitme API'lerini ve güncelleştirme hello Web hizmeti ile Merhaba yeni eğitilen modeli kullanarak hello modeli program aracılığıyla yeniden eğitme. 

Bu belge, işlemi yeniden eğitme hello açıklar ve nasıl toouse hello yeniden eğitme API'lerini gösterir.

## <a name="why-retrain-defining-hello-problem"></a>Neden yeniden eğitme: hello sorunu tanımlama
İşlem eğitim hello machine learning bir parçası olarak, bir model veri kümesini kullanarak eğitildi. Machine Learning kullanarak oluşturduğunuz modelleri genellikle statik değildir. Yeni veriler kullanılabilir olduğunda ya da hello API hello tüketicisi varsa, kendi veri hello modeli retrained toobe gerekir.

Bu senaryolarda, siz veya hello programlı bir API uygun şekilde tooallow sağlar, API toocreate bir kerelik veya normal temelinde hello modeli kullanarak kendi verileri yeniden eğitme bir istemci tüketici. Bunlar daha sonra yeniden eğitme hello sonuçlarını değerlendirmek ve hello Web hizmeti API toouse hello yeni eğitilen modeli güncelleştirin.

> [!NOTE]
> Varolan eğitim denemenizi ve yeni Web hizmeti varsa, varolan bir Tahmine dayalı Web hizmeti bölümden hello belirtildiği aşağıdaki hello yönergeler yerine Retrain çıkışı toocheck isteyebilirsiniz.
> 
> 

## <a name="end-to-end-workflow"></a>Uçtan uca iş akışı
Merhaba işlemi içerir bileşenleri aşağıdaki hello: A eğitim denemenizi ve Tahmine dayalı denemeye bir Web hizmeti olarak yayımladı. tooenable eğitilen modeli, hello eğitim denemenizi yeniden eğitme eğitilen bir modelin hello çıktıyla bir Web hizmeti olarak yayımlanmalıdır. Bu yeniden eğitme için API erişim toohello modeli sağlar. 

tooboth yeni ve Klasik Web Hizmetleri hello aşağıdaki adımları uygulayın:

Merhaba ilk Tahmine dayalı Web hizmeti oluşturun:

* Eğitim denemenizi oluşturma
* Tahmine dayalı web deneme oluşturma
* Tahmine dayalı web hizmetini dağıtma

Merhaba Web hizmeti yeniden eğitme:

* Yeniden eğitme için eğitim deneme tooallow güncelleştir
* Web hizmeti yeniden eğitme hello dağıtma
* Merhaba toplu yürütme hizmeti kod tooretrain hello modeli kullanın

Önceki adımları hello bir anlatım için bkz: [yeniden eğitme Machine Learning modellerini programlama aracılığıyla](machine-learning-retrain-models-programmatically.md).

> [!NOTE] 
> toodeploy yeni bir web hizmeti yeterli izniniz hello abonelik toowhich, hello web Hizmeti'ni dağıtma olması gerekir. Daha fazla bilgi için [hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir Web hizmeti yönetmek](machine-learning-manage-new-webservice.md). 

Klasik Web hizmeti dağıttıysanız:

* Tahmine dayalı Web hizmeti hello üzerinde yeni bir uç noktası oluşturma
* Merhaba düzeltme eki URL ve kodu alın
* Kullanım hello düzeltme eki URL toopoint hello yeni uç noktada hello retrained modeli 

Önceki adımları hello bir anlatım için bkz: [Klasik Web hizmeti yeniden eğitme](machine-learning-retrain-a-classic-web-service.md).

Klasik Web hizmeti yeniden eğitme zorluklar çalıştırırsanız, bkz: [hello bir Azure Machine Learning Klasik Web hizmeti yeniden eğitme sorun giderme](machine-learning-troubleshooting-retraining-models.md).

Yeni Web hizmeti dağıttıysanız:

* Tooyour Azure Resource Manager hesabı oturum
* Merhaba Web hizmeti tanımının Al
* Merhaba Web hizmeti tanımının JSON olarak dışarı aktarma
* Merhaba başvuru toohello güncelleştirme `ilearner` hello JSON blob
* İçeri aktarma hello JSON Web hizmeti tanımının içinde
* Yeni Web hizmeti tanımının ile Merhaba Web hizmetini güncelleştirmek

Önceki adımları hello bir anlatım için bkz: [hello makine öğrenme yönetim PowerShell cmdlet'lerini kullanarak yeni Web hizmeti yeniden eğitme](machine-learning-retrain-new-web-service-using-powershell.md).

Klasik Web hizmeti yeniden eğitme yukarı ayarlamak için hello işlemi hello aşağıdaki adımları içerir:

![Yeniden eğitme işlemine genel bakış][1]

Yeni Web hizmeti yeniden eğitme yukarı ayarlamak için hello işlemi hello aşağıdaki adımları içerir:

![Yeniden eğitme işlemine genel bakış][7]

## <a name="other-resources"></a>Diğer Kaynaklar
* [Azure Data Factory ile güncelleştirme Azure Machine Learning yeniden eğitme ve modelleri](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)
* [Birçok Machine Learning modellerini ve web hizmeti uç noktalarını PowerShell kullanarak bir deneme oluşturma](machine-learning-create-models-and-endpoints-with-powershell.md)
* Merhaba [AML yeniden eğitme modelleri kullanarak API'lerini](https://www.youtube.com/watch?v=wwjglA8xllg) video gösterir, yeniden eğitme API'lerini ve PowerShell tooretrain Machine Learning modellerini hello kullanarak Azure Machine Learning ile nasıl oluşturuldu.

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

