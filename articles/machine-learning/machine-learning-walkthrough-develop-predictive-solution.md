---
title: "Tahmine dayalı bir çözüm aaaA Machine Learning ile kredi riski için | Microsoft Docs"
description: "Gösteren ayrıntılı bir kılavuz nasıl toocreate kredi için Tahmine dayalı analiz çözümü risk değerlendirmesi Azure Machine Learning Studio'da."
keywords: "kredi riski, tahmine dayalı analiz çözümü, risk değerlendirmesi"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 43300854-a14e-4cd2-9bb1-c55c779e0e93
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 00ed39081e6952b8d03b37a8285d8dc3ddff2cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a>Kılavuz: Azure Machine Learning Studio'da kredi riski değerlendirmesi için tahmine dayalı bir analiz çözümü geliştirme

Bu kılavuzda, biz Machine Learning Studio'da Tahmine dayalı analiz çözümü geliştirme sürecini hello genişletilmiş bir göz atın. Biz Machine Learning Studio'da basit bir modeli geliştirmek ve hello modeli yeni verileri kullanarak tahminleri burada yapabilirsiniz bir Azure Machine Learning web hizmeti olarak dağıtabilir. 

Bu kılavuzda Machine Learning Studio'yu daha önce en az bir kere kullandığınız ve makine öğrenimi kavramlarıyla ilgili bir fikriniz olduğu kabul edilir. Bununla birlikte, bir uzman olduğunuz da varsayılmaz.

Hiç kullanmadıysanız **Azure Machine Learning Studio** toostart hello öğretici ile isteyebilirsiniz önce [ilk veri bilimi Azure Machine Learning Studio'da deneme oluşturma](machine-learning-create-experiment.md). Bu öğretici Machine Learning Studio ilk kez Merhaba gösterir. Size nasıl toodrag ve bırak modülleri, denemenize üzerine hello temelleri birbirine bağlamak, hello denemeyi çalıştırın ve hello sonuçlarına bakın gösterir. Başlarken için yararlı olabilecek başka bir Machine Learning Studio'nun hello özelliklerine genel bakış sağlayan bir diyagram aracıdır. Diyagramı şu sayfadan indirip yazdırabilirsiniz: [Azure Machine Learning Studio özelliklerine genel bakış diyagramı](machine-learning-studio-overview-diagram.md).
 
Machine learning genel yeni toohello alanına değilseniz, yararlı tooyou olabilecek bir video serisi yok. Çağrılır [yeni başlayanlar için veri bilimi](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) ve onu, gündelik dil ve kavramları kullanarak harika giriş toomachine öğrenme verebilirsiniz.


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="hello-problem"></a>Merhaba sorunu

Bir kişinin kredi riski kredi uygulamasında verdiği hello bilgileri temel alarak toopredict gerektiğini varsayalım.  

Kredi riski değerlendirmesi karmaşık bir sorun olsa da bu kılavuz için biraz basitleştirebiliriz. Microsoft Azure Machine Learning’i kullanarak nasıl tahmine dayalı analiz çözümü oluşturabileceğinizi gösteren bir örnek olarak kullanacağız. toodo Bu, Azure Machine Learning Studio ve Machine Learning web hizmeti kullanırız.  

## <a name="hello-solution"></a>Merhaba çözümü

Bu ayrıntılı kılavuzda, herkesin erişebileceği kredi riski verileriyle çalışmaya başlayarak bu verileri temel alan tahmine dayalı bir model geliştireceğiz ve modeli eğiteceğiz. Bunu başkaları tarafından kredi riski değerlendirmesi için kullanılacak şekilde ardından biz hello modeli bir web hizmeti olarak dağıtın.

toocreate bu kredi riski değerlendirme çözümü şu adımları izleyin:  

1. [Bir Machine Learning çalışma alanı oluşturma](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Mevcut verileri yükleme](machine-learning-walkthrough-2-upload-data.md)
3. [Deneme oluşturma](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Eğitmek ve hello modelleri değerlendir](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Merhaba web hizmetini dağıtma](machine-learning-walkthrough-5-publish-web-service.md)
6. [Erişim hello web hizmeti](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> Bu kılavuzda hello biz geliştirmek hello deneme çalışan bir kopyasını bulabilirsiniz [Cortana Intelligence Galerisi](https://gallery.cortanaintelligence.com). Çok Git**[izlenecek - kredi riski tahmini](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**  tıklatıp **Studio'da Aç** toodownload hello denemeyi Machine Learning Studio çalışma alanına bir kopyası.
> 
> Bu kılavuzda hello örnek denemesinin basitleştirilmiş bir sürümünü temel [ikili sınıflandırma: Kredi riski tahmini](http://go.microsoft.com/fwlink/?LinkID=525270), hello bulunan [galeri](http://gallery.cortanaintelligence.com/).
