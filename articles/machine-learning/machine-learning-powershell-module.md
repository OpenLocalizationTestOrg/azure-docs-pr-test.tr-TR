---
title: "Machine Learning için aaaPowerShell Modülü | Microsoft Docs"
description: "Azure Machine Learning için Hello PowerShell modülü genel önizleme modunda kullanılabilir. PowerShell toocreate kullanın ve çalışma alanları, denemeler, web hizmetleri ve daha fazlasını yönetebilirsiniz."
keywords: "deneme,doğrusal regresyon,makine öğrenimi algoritmaları,makine öğrenimi öğreticisi,tahmine dayalı modelleme teknikleri,veri bilimi deneyi"
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: a9001cc2-3aa0-47e1-b175-1f76408ba1d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: garye;haining
ms.openlocfilehash: 59362027356b86bf286b7c07380db677ae1d71c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-module-for-microsoft-azure-machine-learning"></a>Microsoft Azure Machine Learning için PowerShell modülü
Azure Machine Learning için Hello PowerShell modülü toouse Windows PowerShell toomanage çalışma alanları, denemeler, veri kümeleri, Klasik web hizmetleri ve daha fazla bilgi sağlayan güçlü bir araçtır.

Merhaba belgeleri görüntülemek ve adresindeki hello tam kaynak kodu ile birlikte hello modülünü indirin [https://aka.ms/amlps](https://aka.ms/amlps). 

> [!NOTE]
> Hello Azure Machine Learning PowerShell modülü şu anda Önizleme modundadır. Merhaba modülü geliştirilmiş ve bu Önizleme dönemi boyunca genişletilmiş toobe devam eder. Merhaba üzerinde takip [Cortana Intelligence ve makine öğrenme Blog](https://blogs.technet.microsoft.com/machinelearning/) Haberler ve bilgiler için.

## <a name="what-is-hello-machine-learning-powershell-module"></a>Merhaba Machine Learning PowerShell Modülü nedir?
Merhaba Machine Learning PowerShell modülüdür bir. NET tabanlı toofully sağlayan DLL modülü, Windows Powershell'den Azure Machine Learning çalışma alanları, denemeler, veri kümeleri, Klasik web hizmetleri ve klasik web hizmeti uç noktalarını yönetin. 

Merhaba modülü ile birlikte düzgün bir şekilde ayrılmış içeren hello tam kaynak kodu indirebilirsiniz [C# API katmanı](https://github.com/hning86/azuremlps/blob/master/code/AzureMLSDK.cs). Bu DLL kendi .NET projeden başvuru ve Azure Machine Learning .NET kod üzerinden yönetebilirsiniz. Ayrıca, doğrudan sık kullanılan istemcinizden kullanabileceğiniz temel REST API'leri hello DLL bağlıdır.

## <a name="what-can-i-do-with-hello-powershell-module"></a>Merhaba PowerShell modülü ile ne yapabilirim?
Bu PowerShell modülü ile gerçekleştirebileceğiniz hello görevler bazıları aşağıda verilmiştir. Merhaba denetleyin [tam belgelerine](https://aka.ms/amlps) bunlar ve çok daha fazla işlev.

* Yönetim sertifikası kullanarak yeni bir çalışma alanı sağlama ([New-AmlWorkspace](https://github.com/hning86/azuremlps#new-amlworkspace))
* Bir deneme grafiğini temsil eden bir JSON dosyasını içeri ve dışarı aktarma ([Export-AmlExperimentGraph](https://github.com/hning86/azuremlps#export-amlexperimentgraph) ve [Import-AmlExperimentGraph](https://github.com/hning86/azuremlps#import-amlexperimentgraph))
* Bir deneme çalıştırma ([Start-AmlExperiment](https://github.com/hning86/azuremlps#start-amlexperiment))
* Tahmine daalı bir denemeden bir web hizmeti oluşturma ([New-AmlWebService](https://github.com/hning86/azuremlps#new-amlwebservice))
* Yayımlanan web hizmetini temel bir uç noktası oluşturma ([Ekle AmlWebServiceEndpoint](https://github.com/hning86/azuremlps#add-amlwebserviceendpoint))
* Bir RRS ve/veya BES web hizmeti uç noktasını çağırma ([Invoke-AmlWebServiceRRSEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) ve [Invoke-AmlWebServicBESEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint))

PowerShell toorun var olan bir denemeyi kullanarak hızlı bir örnek aşağıda verilmiştir:

        #Find hello first Experiment named “xyz”
        $exp = (Get-AmlExperiment | where Description -eq ‘xyz’)[0]
        #Run hello Experiment
        Start-AmlExperiment -ExperimentId $exp.ExperimentId 

Hello PowerShell modülü tooautomate sık istenen görev kullanma hakkında daha ayrıntılı bir kullanım örneği için bu makaleye bakın: [birçok Machine Learning modellerini ve web hizmeti uç noktalarını PowerShell kullanarak bir deneme oluşturma](machine-learning-create-models-and-endpoints-with-powershell.md).

## <a name="how-do-i-get-started"></a>Nasıl kullanmaya başlayabilirim?
tooget başlatılan makine öğrenme PowerShell ile hello yükleme [yayın paketine](https://github.com/hning86/azuremlps/releases) GitHub ve izleme hello gelen [yüklemesi için yönergeler](https://github.com/hning86/azuremlps/blob/master/README.md). Merhaba yönergeleri nasıl toounblock hello indirilen/DLL sıkıştırması açılmış açıklayabilir ve PowerShell ortamınıza içeri aktarın. Merhaba çalışma alanı kimliği, hello çalışma yetkilendirme belirtecini sağlayın ve çalışma hello Azure bölgesi hello cmdlet'leri gerektiren hello çoğunu konusu. Varsayılan config.json dosyası aracılığıyla Hello en basit yolu tooprovide hello değerleri var. Merhaba yönergeler de açıklayan nasıl tooconfigure bu dosya. 

Ve isterseniz, hello git ağaç kopyalama, hello kodu değiştirin, yerel olarak Visual Studio kullanarak derleyin.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba tam hello PowerShell modülü için bulabilirsiniz [https://aka.ms/amlps](https://aka.ms/amlps). 

Nasıl toouse hello gerçek dünya senaryoları modülünde bir genişletilmiş örnek için ayrıntılı hello kullanıma kullanım örneği, [birçok Machine Learning modellerini ve web hizmeti uç noktalarını PowerShell kullanarak bir deneme oluşturma](machine-learning-create-models-and-endpoints-with-powershell.md).
