---
title: PowerShell ile yeni Azure Machine Learning web hizmetine aaaRetrain | Microsoft Docs
description: "Nasıl tooprogrammatically yeniden eğitme bir model ve güncelleştirme hello web hizmeti toouse hello yeni eğitilen modeli hello makine öğrenme yönetim PowerShell cmdlet'lerini kullanarak Azure Machine Learning öğrenin."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3953a398-6174-4d2d-8bbd-e55cf1639415
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 5b77fa82cfe17f0b4e90007ef81c506ab712475b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-hello-machine-learning-management-powershell-cmdlets"></a>Merhaba makine öğrenme yönetim PowerShell cmdlet'lerini kullanarak yeni Resource Manager temelli web hizmeti yeniden eğitme
Yeni bir web hizmeti yeniden eğitme, hello Tahmine dayalı web hizmeti tanımı tooreference hello yeni eğitilen modeli güncelleştirin.  

## <a name="prerequisites"></a>Ön koşullar
Gösterildiği gibi bir eğitim denemenizi ve Tahmine dayalı denemeye ayarlamalısınız [yeniden eğitme Machine Learning modellerini programlama aracılığıyla](machine-learning-retrain-models-programmatically.md). 

> [!IMPORTANT]
> bir Azure Kaynak Yöneticisi'ni (yeni) dayalı machine learning web hizmeti Hello Tahmine dayalı denemeye dağıtılması gerekir. toodeploy yeni bir web hizmeti yeterli izniniz hello abonelik toowhich, hello web Hizmeti'ni dağıtma olması gerekir. Daha fazla bilgi için bkz: [hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir Web hizmeti yönetmek](machine-learning-manage-new-webservice.md). 

Web hizmetleri dağıtma hakkında ek bilgi için bkz: [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).

Bu işlem hello Azure Machine Learning cmdlet'leri yüklü gerekir. Merhaba Hello Machine Learning cmdlet'lerini yükleme daha fazla bilgi için bkz [Azure Machine Learning cmdlet'leri](https://msdn.microsoft.com/library/azure/mt767952.aspx) başvuru konusuna bakın.

Çıktı yeniden eğitme hello bilgisinden kopyalanan hello:

* BaseLocation
* RelativeLocation

hello adımlar şunlardır:

1. Tooyour Azure Resource Manager hesabı oturum açın.
2. Merhaba web hizmeti tanımının Al
3. Merhaba Web hizmeti tanımının JSON olarak dışarı aktarma
4. Merhaba başvuru toohello ilearner blob hello JSON güncelleştirin.
5. İçeri aktarma hello JSON Web hizmeti tanımının içinde
6. Yeni Web hizmeti tanımının ile Merhaba web hizmetini güncelleştirmek

## <a name="sign-in-tooyour-azure-resource-manager-account"></a>Tooyour Azure Resource Manager hesabı oturum
Tooyour hello PowerShell ortamında hello kullanarak Azure hesabından ilk imzalamalısınız [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet'i.

## <a name="get-hello-web-service-definition"></a>Merhaba Web hizmeti tanımının Al
Ardından, hello Web hizmeti arama hello tarafından alma [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet'i. Merhaba Web hizmeti tanımının hello eğitilen model hello web hizmetinin iç bir gösterimini ve doğrudan değiştirilebilir değil. Tahmine dayalı denemenizi ve değil eğitim denemenizi hello Web hizmeti tanımının alırsınız emin olun.

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

toodetermine hello kaynak grubu adı var olan bir web hizmeti, aboneliğinizdeki tüm parametreleri toodisplay hello web Hizmetleri olmadan hello Get-AzureRmMlWebService cmdlet'ini çalıştırın. Merhaba web hizmetini bulun ve sonra web hizmeti kimliğini arayın Hello hello kaynak grubunun adıdır hello dördüncü hello kimliği öğesinde yalnızca hello sonra *resourceGroups* öğesi. Aşağıdaki örneğine hello hello kaynak grubu adı varsayılan MachineLearning SouthCentralUS ' dir.

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

Alternatif olarak, toodetermine hello kaynak grubu adı varolan bir web hizmeti, günlük toohello Microsoft Azure Machine Learning Web Hizmetleri portalındaki. Merhaba web hizmeti seçin. Merhaba kaynak grubu adı öğedir hello beşinci hello hello web hizmeti URL'sini hemen sonra hello *resourceGroups* öğesi. Aşağıdaki örneğine hello hello kaynak grubu adı varsayılan MachineLearning SouthCentralUS ' dir.

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-as-json"></a>Merhaba Web hizmeti tanımının JSON olarak dışarı aktarma
toomodify hello tanımı toohello eğitilmiş model toouse Merhaba yeni eğitilen Model, ilk hello kullanmalısınız [verme AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport onu tooa JSON biçim dosyası.

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob-in-hello-json"></a>Merhaba başvuru toohello ilearner blob hello JSON güncelleştirin.
Merhaba [eğitilen model], güncelleştirme hello Hello varlıkları bulun *URI* hello değerinde *locationInfo* hello hello ilearner blob URI'si düğümle. Merhaba URI hello birleştirerek oluşturulan *BaseLocation* ve hello *RelativeLocation* hello BES yeniden eğitme çağrısı hello çıktısından. Merhaba yolu tooreference hello yeni eğitilen model güncelleştirir.

     "asset3": {
        "name": "Retrain Samp.le [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition"></a>İçeri aktarma hello JSON Web hizmeti tanımının içinde
Merhaba kullanmalısınız [alma AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello geri bir Web hizmeti tooupdate hello Web hizmeti tanımının kullanabileceğiniz tanımının JSON dosyasını değiştirdi.

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service-with-new-web-service-definition"></a>Yeni Web hizmeti tanımının ile Merhaba web hizmetini güncelleştirmek
Son olarak, kullandığınız [güncelleştirme AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello Web hizmeti tanımının.

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a>Özet
Hello Machine Learning PowerShell Yönetimi cmdlet'lerini kullanarak, Tahmine dayalı bir Web hizmeti gibi senaryoları etkinleştirme hello eğitilen modelini güncelleştirebilirsiniz:

* Yeni verilerle yeniden eğitme düzenli modeli.
* Kullanıcıların kendi verilerini kullanarak hello modeli yeniden eğitme yapmalarına izin hello amacı ile bir model toocustomers dağıtımı.

