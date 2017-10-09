---
title: "Machine Learning toplu yürütme hizmeti işleri için kapasite aaaDedicated | Microsoft Docs"
description: "Machine Learning işleri için Azure Batch hizmetlerine genel bakış."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: bba7970bb31c50e5b0b9d5f4ff4f0d2dacf942e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a>Machine Learning işleri için Azure Batch hizmeti

Machine Learning Batch havuzundaki işlem müşteri tarafından yönetilen ölçek hello Azure Machine Learning toplu yürütme hizmeti sağlar. Klasik toplu işleme Machine learning için ilk olarak ilk çıkar temelinde kuyruğa alınan hangi sınırları hello gönderebilir ve işleri eşzamanlı iş sayısı bir ortamda çok kiracılı, gerçekleşir. Bu belirsizlik, doğru şekilde işinizi ne zaman çalışacağını tahmin edilemez olduğunu anlamına gelir.

Batch havuzu işleme toocreate havuzları toplu işleri gönderme sağlar. Merhaba havuzu hello boyutunu denetlemek ve toowhich havuzu hello iş gönderilir. BES işinizi kendi alanı sağlamak işleme tahmin edilebilir işlem performansı ve gönderdiğiniz toohello işleme yükünü karşılık hello özelliği toocreate kaynak havuzları çalışır.

## <a name="how-toouse-batch-pool-processing"></a>Nasıl toouse Batch havuzu işleme

Havuz toplu işleme yapılandırması hello Azure portal şu anda kullanılabilir değil. toouse Batch havuzundaki işlem yapmanız gerekir:

-   Batch havuzu hesabı CSS toocreate çağırın ve bir havuz hizmet URL'si ve bir yetkilendirme anahtarı edinin
-   Yeni kaynak tabanlı Manager web hizmeti ve fatura planı oluşturma

toocreate hesabınızı Microsoft Müşteri Hizmetleri ve desteği (CSS) arayın ve abonelik kimliğinizi girin CSS, toodetermine hello uygun kapasiteli senaryonuz için çalışır. CSS hesabınızı oluşturun ve her havuzda yerleştirebilirsiniz sanal makineler (VM) sayısı hello havuzları hello sayısı ardından yapılandırır. Hesabınızı yapılandırıldıktan sonra havuzu hizmet URL'niz ve bir yetkilendirme anahtarı sağlanır.

Hesabınızı oluşturduktan sonra hello havuz hizmet URL'si ve yetkilendirme anahtar tooperform havuzu yönetim işlemlerini Batch havuzu kullanın.

![Batch havuzu hizmet mimarisi.](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

Bu sağlanan CSS tooyou hello havuzu hizmeti URL'si hello havuzu oluştur işlemi çağırarak havuzları oluşturun. Bir havuz oluşturduğunuzda, Machine Learning web hizmeti VM'ler ve hello swagger.json Yeni Kaynak Yöneticisi'nin hello URL'sini hello sayısına dayalı belirtin. Bu web Hizmeti'nin tooestablish hello fatura ilişkilendirme sağlanır. Hello Batch havuzu hizmeti ile bir faturalandırma planı hello swagger.json tooassociate hello havuzu kullanır. Klasik, hello havuzunda seçtiğiniz ve web hizmeti, iki yeni Resource Manager temelli herhangi BES çalıştırabilirsiniz.

Tüm yeni Resource Manager temelli web hizmetini kullanır, ancak hello faturalama hello işleri için ücretlendirilirsiniz, hizmetle ilişkili hello fatura planı karşı unutmayın. Özellikle Batch havuzu işlerini çalıştırmak için bir web hizmeti ve yeni faturalandırma planı toocreate isteyebilirsiniz.

Web hizmetleri oluşturma hakkında daha fazla bilgi için bkz: [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).

Bir havuzu oluşturduktan sonra hello BES gönderme işlemini kullanarak toplu istekleri URL hello web hizmeti için hello. Toosubmit seçebilirsiniz, tooa havuzu veya tooclassic toplu işleme. bir iş tooBatch havuzu işleme toosubmit, parametre toohello iş gönderme istek gövdesi aşağıdaki hello ekleyin:

"AzureBatchPoolId": "&lt;kimliği havuzu&gt;"

Merhaba parametresini eklemezseniz hello iş hello Klasik toplu işlem ortamında çalıştırılır. Merhaba havuzu kullanılabilir kaynakları varsa hello iş çalıştırdıktan hemen başlar. Merhaba havuzu kaynakları serbest bırakmak yoksa, bir kaynak kullanılabilir hale gelene kadar işinizi sıraya alındı.

Düzenli olarak, havuzlarınızı hello kapasitesini ulaşmak ve artan kapasite gerektiğini fark ederseniz, CSS çağırın ve, kotaları temsilcisi tooincrease ile çalışır.

Örnek isteği:

https://ussouthcentral.Services.azureml.NET/Subscriptions/80c77c7674ba4c8c82294c3b2957990c/Services/9fe659022c9747e3b9b7b923c3830623/Jobs?api-Version=2.0

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a>Batch havuzundaki işlem kullanmayla ilgili konular

Havuz toplu işleme bir her zaman açık Faturalanabilir hizmetidir ve Resource Manager ile fatura planı temel tooassociate olmasını gerektirir. İşlem saatleri hello havuzu çalıştıran hello sayısı için yalnızca faturalandırılır; o zaman havuzunu sırasında çalıştırmak işlerin sayısı Hello bağımsız olarak. Bir havuzu oluşturursanız, hello havuzu silinene kadar toplu iş hello havuzunda çalıştırıyor olsanız bile, her sanal makinenin hello havuzunda hello işlem saatleri için faturalandırılır. Merhaba sanal makineler için fatura sağlama bittiğinde, başlatır ve silinmiş zaman durdurur. Merhaba planı üzerinde hello bulunamadı birini kullanabilirsiniz [Machine Learning fiyatlandırması sayfa](https://azure.microsoft.com/pricing/details/machine-learning/).

Faturalama örnek:

2 sanal makinelerle Batch havuzu oluşturma ve 24 saat sonra silerseniz, faturalandırma planınıza 48 işlem saatleri düşülür; kaç tane işleri bağımsız olarak, bu süre boyunca çalıştırılmadı.

4 sanal makinelerle Batch havuzu oluşturma ve 12 saat sonra silerseniz, faturalandırma planınıza ayrıca borç kaydedilen 48 işlem saattir.

İşlerini tamamladığınızda hello iş durumu toodetermine yoklamak öneririz. Çalışan tüm işleri tamamladığınızda hello boyutlandırma havuzu işlemi tooset hello sanal makine sayısı hello havuzu toozero çağırın. Çalışan tüm işleri tamamladığınızda havuzu kaynaklardaki kısa ve toocreate yeni bir havuz örneğin farklı bir fatura planı karşı toobill ihtiyacınız varsa hello havuzu yerine silebilirsiniz.


| **Batch havuzundaki işlemesini kullanın**    | **Klasik toplu ne zaman işleme kullanın**  |
|---|---|
|Toorun çok sayıda işleri gerekir<br>Veya<br/>İşleriniz hemen çalışacak tooknow gerekir<br/>Veya<br/>Garantili işleme gerekir. Örneğin, toorun işleri belirli bir zaman çerçevesi içinde bir dizi gereksinim ve tooscale, işlem kaynakları toomeet gereksinimlerinizi istiyor.    | Yalnızca birkaç işleri çalıştırma<br/>Ve<br/> Merhaba işleri toorun hemen gerekmez |
