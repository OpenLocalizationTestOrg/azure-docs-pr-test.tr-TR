---
title: "Machine Learning aaaCreating Web Hizmeti uç noktalarını | Microsoft Docs"
description: "Azure Machine Learning Web Hizmeti uç noktaları oluşturma"
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a>Uç Nokta Oluşturma
> [!NOTE]
>  Bu konu, geçerli tooa teknikleri açıklar **Klasik** Machine Learning Web hizmeti.
> 
> 

İleriye doğru tooyour müşteriler satmak Web Hizmetleri oluşturduğunuzda, hangi hello Web hizmeti oluşturuldu hala bağlı toohello deneme olan tooprovide eğitilmiş modeller tooeach müşteri gerekir. Ayrıca, toohello deneme olması gereken herhangi bir güncelleştirme seçmeli olarak tooan endpoint hello özelleştirmeleri yazmadan uygulanır.

tooaccomplish Bu, Azure Machine Learning toocreate verir dağıtılan Web hizmeti için birden çok uç nokta. Merhaba Web hizmeti içindeki her bir uç nokta bağımsız olarak ele, kısıtlanan yönetilen ve. Her uç tooyour müşteriler dağıtabilirsiniz benzersiz bir URL ve yetkilendirme anahtar noktadır.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a>Uç noktaları tooa Web hizmeti ekleme
Bir Web Hizmeti uç noktası tooa üç yolu tooadd vardır.

* Programlama yoluyla
* Hello Azure Machine Learning Web Hizmetleri Portalı aracılığıyla
* Yine de klasik Azure portalı hello

Merhaba uç nokta oluşturulduktan sonra zaman uyumlu API'leri, batch API'leri aracılığıyla kullanabilir ve excel çalışma sayfaları. Ayrıca tooadding uç noktaları bu kullanıcı Arabirimi aracılığıyla da kullanabilirsiniz hello uç nokta Yönetimi API'leri tooprogrammatically uç noktaları ekleyin.

> [!NOTE]
> Ek uç noktaları toohello Web hizmeti eklediyseniz, hello varsayılan uç silemezsiniz.
> 
> 

## <a name="adding-an-endpoint-programmatically"></a>Bir uç nokta programlı olarak ekleme
Program aracılığıyla hello kullanarak bir uç nokta tooyour Web hizmeti Ekle [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) örnek kodu.

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a>Hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir uç nokta ekleme
1. Machine Learning Studio'da hello sol gezinti sütuna, Web Hizmetleri'ı tıklatın.
2. Merhaba Web hizmeti Pano Hello altındaki tıklatın **uç yönetin**. Hello Azure Machine Learning Web Hizmetleri portalı toohello hello Web hizmeti için uç noktaları sayfası açılır.
3. **Yeni**’ye tıklayın.
4. Bir ad ve hello yeni uç noktası için bir açıklama yazın. Uç nokta adları 24 karakter veya daha az uzunlukta olmalı ve küçük harfler veya numaraların yapılmalıdır. Merhaba günlüğe kaydetme düzeyi ve örnek verileri etkinleştirilip etkinleştirilmediğini seçin. Günlüğe kaydetme hakkında daha fazla bilgi için bkz: [Machine Learning Web Hizmetleri için günlüğe kaydetmeyi etkinleştirmek](machine-learning-web-services-logging.md).

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a>Merhaba Klasik Azure portalı kullanarak bir uç nokta ekleme
1. İçinde toohello oturum [Klasik Azure portalı](http://manage.windowsazure.com), tıklatın **Machine Learning** hello sol sütunda. Merhaba Web hizmeti, ilgilendiğiniz içeren hello çalışma alanını tıklatın.
   
    ![Tooworkspace gidin](./media/machine-learning-create-endpoint/figure-1.png)
2. Tıklatın **Web Hizmetleri**.
   
    ![TooWeb Hizmetleri gidin](./media/machine-learning-create-endpoint/figure-2.png)
3. Merhaba Web hizmeti toosee hello listesinde kullanılabilir uç noktaları ilgilendiğiniz'ı tıklatın.
   
    ![Tooendpoint gidin](./media/machine-learning-create-endpoint/figure-3.png)
4. Merhaba sayfasının Hello altında tıklatın **uç nokta Ekle**. Bir ad ve açıklama yazın, aynı ad bu Web hizmeti hello ile diğer uç nokta olmadığından emin olun. Özel gereksinimleriniz olmadıkça hello kısıtlama düzeyini varsayılan değerini bırakın. Azaltma, hakkında daha fazla toolearn bkz [ölçeklendirme API uç noktaları](machine-learning-scaling-webservice.md).
   
    ![Uç noktası oluşturma](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a>Sonraki Adımlar
[Nasıl tooconsume bir Azure Machine Learning Web hizmeti](machine-learning-consume-web-services.md).

