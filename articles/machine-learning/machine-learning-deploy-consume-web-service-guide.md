---
title: "Azure Machine Learning Web Hizmetleri: Dağıtım ve kullanım | Microsoft Docs"
description: "Dağıtma ve web hizmetlerini tüketen kaynaklar."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 539c2abb053a0f981be0374defe45cf4d96b740b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a>Azure Machine Learning Web Hizmetleri: Dağıtım ve kullanım
Azure Machine Learning toodeploy machine learning iş akışları ve modelleri web Hizmetleri olarak kullanabilirsiniz. Bu web hizmetleri hello Internet toodo tahminlerin gerçek zamanlı veya toplu iş modunda üzerinden kullanılan toocall hello machine learning modellerini uygulamalardan sonra olabilir. Merhaba web hizmetleri RESTful olduğundan, bunları çeşitli programlama dillerini ve .NET ve Java gibi platformları ve Excel gibi uygulamalardan çağırabilirsiniz.

bağlantılar toowalkthroughs, kodu ve belgeler toohelp başlamanıza yardımcı Hello sonraki bölümlerde verilmiştir.

## <a name="deploy-a-web-service"></a>Bir web hizmetini dağıtma
### <a name="with-azure-machine-learning-studio"></a>Azure Machine Learning Studio ile
Machine Learning Studio ve hello Microsoft Azure Machine Learning Web Hizmetleri portalı dağıtmak ve bir web hizmeti kod yazmadan yönetmenize yardımcı olur.

Merhaba aşağıdaki bağlantılar sağlar hakkında genel bilgi toodeploy yeni bir web hizmeti:

* Azure kaynak yöneticiyi temel alan yeni bir web hizmeti toodeploy nasıl görürüm hakkında genel bir bakış için [yeni bir web hizmetini dağıtma](machine-learning-webservice-deploy-a-web-service.md).
* Gözden geçirme konusunda toodeploy bir web hizmeti bkz [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).
* Tam bir gözden geçirme konusunda toocreate ve bir web hizmetini dağıtma, bkz: [gözden geçirme adım 1: Machine Learning çalışma alanı oluşturma](machine-learning-walkthrough-1-create-ml-workspace.md).
* Bir web hizmetini dağıtma belirli örnekler için bkz:

  * [Gözden geçirme adım 5: hello Azure Machine Learning web hizmetini dağıtma](machine-learning-walkthrough-5-publish-web-service.md)
  * [Nasıl toodeploy bir web hizmeti toomultiple bölgeleri](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a>Web Hizmetleri kaynak sağlayıcı API'leri (Azure Resource Manager API'leri)
web hizmetleri için Hello Azure Machine Learning kaynak sağlayıcısı REST API çağrısı kullanarak dağıtım ve Yönetim web hizmetleri sağlar. Daha fazla bilgi için bkz: [Machine Learning Web hizmeti (REST)](/rest/api/machinelearning/index) başvurusu.

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a>PowerShell cmdlet'leri ile
Azure Machine Learning kaynak sağlayıcısı web hizmetleri için dağıtım ve Yönetim web hizmetleri PowerShell cmdlet'lerini kullanarak etkinleştirir.

toouse hello cmdlet'leri, gerekir ilk tooyour hello PowerShell ortamında Azure hesabından hello kullanarak oturum [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet'i. İle hakkında bilginiz yoksa, nasıl toocall PowerShell komutları dayalı kaynak yöneticisi için bkz: [Azure PowerShell kullanarak Azure Resource Manager ile](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).

tooexport, Tahmine dayalı denemeler, kullanın [Bu örnek kod](https://github.com/ritwik20/AzureML-WebServices). Merhaba koddan hello .exe dosyasını oluşturduktan sonra yazabilirsiniz:

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

Merhaba uygulaması çalıştıran bir web hizmeti JSON şablonu oluşturur. toouse hello şablonu toodeploy bir web hizmeti, aşağıdaki bilgilerle hello eklemeniz gerekir:

* Depolama hesabı adı ve anahtar

    Ya da hello hello depolama hesabı adı ve anahtarınızı edinin [Azure portal](https://portal.azure.com/) veya hello [Klasik Azure portalı](http://manage.windowsazure.com/).
* Taahhüt plan kimliği

    Hello hello planı kodu alabilirsiniz [Azure Machine Learning Web Hizmetleri](https://services.azureml.net) oturum açma ve bir plan adı tıklatarak portal.

Bunları toohello JSON şablonunu hello alt öğeleri olarak Ekle *özellikleri* hello düğümde aynı düzeydeki hello *MachineLearningWorkspace* düğümü.

Örnek aşağıda verilmiştir:

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

Makaleler hello bakın ve kod ek ayrıntılar için örnek:

* [Azure Machine Learning cmdlet'lerini](https://msdn.microsoft.com/library/azure/mt767952.aspx) MSDN'de başvurusu
* Örnek [izlenecek](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) github'da

## <a name="consume-hello-web-services"></a>Merhaba web hizmetlerini kullanma
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a>Azure Machine Learning Web Hizmetleri kullanıcı Arabirimi (test) Hello
Web hizmetiniz hello Azure Machine Learning Web Hizmetleri Portalı'ndan test edebilirsiniz. Bu test hello istek-yanıt hizmeti (RRS) içerir ve toplu yürütme hizmeti (BES) arabirimleri.

* [Yeni bir web hizmeti dağıtma](machine-learning-webservice-deploy-a-web-service.md)
* [Bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md)
* [Gözden geçirme adım 5: hello Azure Machine Learning web hizmetini dağıtma](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a>Excel'den
Merhaba web hizmeti tüketen Excel şablonunu indirebilirsiniz:

* [Bir Azure Machine Learning web hizmetini Excel'den kullanma](machine-learning-consuming-from-excel.md)
* [Azure Machine Learning Web Hizmetleri için Excel Eklentisi](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a>REST tabanlı bir istemciden
Azure Machine Learning Web Hizmetleri RESTful API'lerini ' dir. .NET, Python, R, Java, vb. hello gibi çeşitli platformlarda bu API'lerden tüketebileceği **Tüket** hello üzerinde web hizmeti için sayfa [Microsoft Azure Machine Learning Web Hizmetleri portalı](https://services.azureml.net) örnek içeriyor yardımcı olabilecek kod Başlarken. Daha fazla bilgi için bkz: [nasıl tooconsume bir Azure Machine Learning Web hizmeti](machine-learning-consume-web-services.md).
