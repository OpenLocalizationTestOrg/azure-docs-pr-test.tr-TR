---
title: "6. adım: Hello Machine Learning Web hizmetine erişim | Microsoft Docs"
description: "6. adımını hello geliştirmek Tahmine dayalı bir çözüm izlenecek yol: etkin bir Azure Machine Learning Web hizmetine erişim."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a65c89a-40ab-4673-8dd8-8eee0a150e3b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 211de0294092c6a6b5e6eb608d5d3b88107674c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-6-access-hello-azure-machine-learning-web-service"></a>Gözden geçirme adım 6: hello Azure Machine Learning web hizmetine erişim

Merhaba kılavuzun hello son adım budur [Azure Machine learning'de Tahmine dayalı analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Bir Machine Learning çalışma alanı oluşturma](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Mevcut verileri yükleme](machine-learning-walkthrough-2-upload-data.md)
3. [Yeni bir deneme oluşturma](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Eğitmek ve hello modelleri değerlendir](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Merhaba Web hizmetini dağıtma](machine-learning-walkthrough-5-publish-web-service.md)
6. **Merhaba Web hizmetine erişim**

- - -
Bu kılavuzda hello önceki adımda bizim kredi riskini tahmin modelini kullanan bir web hizmeti dağıttığımız. Artık kullanıcılar mümkün toosend veri tooit ve sonuçları alırsınız. 

Merhaba Web hizmetini alabilen ve iki yoldan biriyle REST API'lerini kullanarak verileri döndürmek bir Azure web hizmetidir:  

* **İstek/yanıt** - hello kullanıcı bir gönderir veya kredi veri toohello daha fazla satır hizmeti bir HTTP protokolünü kullanarak ve hello sonuçlarının bir veya daha fazla kümeleriyle hizmet yanıt verir.
* **Toplu yürütme** - hello kullanıcı depolayan bir veya daha fazla satır kredi Azure blob ve hello blob konumu toohello hizmetine gönderir. Giriş blob tüm satır hello hello hizmet puanları Merhaba, bu kapsayıcı URL'sini hello başka bir blob'a sonuçlanır ve döndürür depolarını hello.  

Klasik web hizmeti hello olan hızlı ve kolay bir yol tooaccess hello [Azure ML istek-yanıt hizmeti Web uygulaması](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) veya [Azure ML toplu iş yürütme hizmeti Web uygulaması şablonu](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).

Bu web uygulaması şablonlar web hizmetinizin giriş verilerini ve ne döndürülecek bilir bir özel web uygulaması oluşturabilirsiniz. Tek toodo ihtiyacınız olan erişim tooyour web hizmeti ve verileri sağlar ve hello şablon rest hello.

Merhaba web uygulama şablonları kullanma hakkında daha fazla bilgi için bkz: [bir Azure Machine Learning Web hizmeti bir web uygulaması şablonu kullanmak](machine-learning-consume-web-service-with-web-app-template.md).

R, C# ve Python programlama dilleri, için sağlanan starter kod kullanarak bir özel uygulama tooaccess hello web hizmeti de geliştirebilirsiniz.

Tam ayrıntıları bulabilirsiniz [nasıl tooconsume bir Azure Machine Learning Web hizmeti](machine-learning-consume-web-services.md).

