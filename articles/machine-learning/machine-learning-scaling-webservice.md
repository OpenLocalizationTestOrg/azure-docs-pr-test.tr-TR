---
title: "bir Azure Machine Learning web hizmetini aaaHow tooincrease eşzamanlılığı | Microsoft Docs"
description: "Nasıl tooincrease eşzamanlılığı bir Azure Machine Learning web hizmeti ek uç noktaları ekleyerek öğrenin."
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: "azure machine Learning web hizmetlerini ölçeklendirme, uç nokta, eşzamanlılık operationalization"
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: e2ad16ec766820a64f36c31232f6a33a79196af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a>Ek uç noktaları ekleyerek bir Azure Machine Learning web hizmetini ölçeklendirme
> [!NOTE]
> Bu konu, geçerli tooa teknikleri açıklar **Klasik** Machine Learning Web hizmeti. 
> 
> 

Varsayılan olarak, her yayımlanan Web hizmeti yapılandırılmış toosupport 20 eş zamanlı istekler ve 200 eş zamanlı istekleri olarak yüksek olabilir. Hello Klasik Azure portalı bu değer bir şekilde tooset sağlarken, Azure Machine Learning otomatik olarak hello ayarı tooprovide hello en iyi performansı web hizmetiniz için en iyi duruma getirir ve hello portal değeri yoksayılır. 

Toocall hello API 200 en fazla eşzamanlı çağrıları değeri destekleyecek daha yüksek bir yük ile planlıyorsanız, birden çok uç nokta üzerinde hello oluşturmalısınız aynı Web hizmeti. Ardından rastgele yük bunların tümünün arasında dağıtabilirsiniz.

bir Web hizmeti Hello ölçeklendirme ortak bir görevdir. Bazı nedenlerden tooscale olan 200 eş zamanlı istekleri birden çok toosupport, birden fazla uç noktası aracılığıyla kullanılabilirliğini artırmak veya hello web hizmeti için ayrı uç noktaları sağlayın. Hello için ek uç noktaları ekleyerek hello ölçek artırabilir aynı Web hizmeti aracılığıyla [Klasik Azure portalı](https://manage.windowsazure.com/) veya hello [Azure Machine Learning Web hizmeti](https://services.azureml.net/) portal.

Yeni uç nokta ekleme hakkında daha fazla bilgi için bkz: [uç noktaları oluşturma](machine-learning-create-endpoint.md).

Bir yüksek eşzamanlılık sayısı kullanarak hello API gelenlere yüksek oranda ile arıyoruz değil, detrimental göz önünde bulundurun. Yüksek yük için yapılandırılmış bir API nispeten düşük yük yerleştirirseniz hello gecikme ara sıra zaman aşımları ve/veya ani görebilirsiniz.

Merhaba, zaman uyumlu API'leri, tipik olarak düşük gecikme süresi burada istenen durumlarda kullanılır. Burada gecikme gelir başlangıç saati hello API toocomplete bir istek için alır ve tüm ağ gecikme hesabı değil. 50-ms gecikme süresi ile bir API sahip varsayalım. toofully tüketen hello kullanılabilir kapasiteye sahip azaltma düzeyi yüksek ve en fazla eşzamanlı çağrıları = 20, bu API 20 * 1000 toocall ihtiyacınız / saniye başına 50 = 400 zaman. Bu daha fazla genişletme, en fazla eşzamanlı çağrıları 200, toocall hello API 4000 saniye başına alınabildiği 50-ms gecikme varsayarak, sağlar.

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
