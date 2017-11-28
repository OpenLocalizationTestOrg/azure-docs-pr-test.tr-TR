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
# <a name="retrain-a-new-resource-manager-based-web-service-using-hello-machine-learning-management-powershell-cmdlets"></a><span data-ttu-id="bde06-103">Merhaba makine öğrenme yönetim PowerShell cmdlet'lerini kullanarak yeni Resource Manager temelli web hizmeti yeniden eğitme</span><span class="sxs-lookup"><span data-stu-id="bde06-103">Retrain a New Resource Manager based web service using hello Machine Learning Management PowerShell cmdlets</span></span>
<span data-ttu-id="bde06-104">Yeni bir web hizmeti yeniden eğitme, hello Tahmine dayalı web hizmeti tanımı tooreference hello yeni eğitilen modeli güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="bde06-104">When you retrain a New web service, you update hello predictive web service definition tooreference hello new trained model.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="bde06-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bde06-105">Prerequisites</span></span>
<span data-ttu-id="bde06-106">Gösterildiği gibi bir eğitim denemenizi ve Tahmine dayalı denemeye ayarlamalısınız [yeniden eğitme Machine Learning modellerini programlama aracılığıyla](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="bde06-106">You must set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="bde06-107">bir Azure Kaynak Yöneticisi'ni (yeni) dayalı machine learning web hizmeti Hello Tahmine dayalı denemeye dağıtılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bde06-107">hello predictive experiment must be deployed as an Azure Resource Manager (New) based machine learning web service.</span></span> <span data-ttu-id="bde06-108">toodeploy yeni bir web hizmeti yeterli izniniz hello abonelik toowhich, hello web Hizmeti'ni dağıtma olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bde06-108">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="bde06-109">Daha fazla bilgi için bkz: [hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir Web hizmeti yönetmek](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="bde06-109">For more information, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="bde06-110">Web hizmetleri dağıtma hakkında ek bilgi için bkz: [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="bde06-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="bde06-111">Bu işlem hello Azure Machine Learning cmdlet'leri yüklü gerekir.</span><span class="sxs-lookup"><span data-stu-id="bde06-111">This process requires that you have installed hello Azure Machine Learning Cmdlets.</span></span> <span data-ttu-id="bde06-112">Merhaba Hello Machine Learning cmdlet'lerini yükleme daha fazla bilgi için bkz [Azure Machine Learning cmdlet'leri](https://msdn.microsoft.com/library/azure/mt767952.aspx) başvuru konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="bde06-112">For information installing hello Machine Learning cmdlets, see hello [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN.</span></span>

<span data-ttu-id="bde06-113">Çıktı yeniden eğitme hello bilgisinden kopyalanan hello:</span><span class="sxs-lookup"><span data-stu-id="bde06-113">Copied hello following information from hello retraining output:</span></span>

* <span data-ttu-id="bde06-114">BaseLocation</span><span class="sxs-lookup"><span data-stu-id="bde06-114">BaseLocation</span></span>
* <span data-ttu-id="bde06-115">RelativeLocation</span><span class="sxs-lookup"><span data-stu-id="bde06-115">RelativeLocation</span></span>

<span data-ttu-id="bde06-116">hello adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bde06-116">hello steps you take are:</span></span>

1. <span data-ttu-id="bde06-117">Tooyour Azure Resource Manager hesabı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="bde06-117">Sign in tooyour Azure Resource Manager account.</span></span>
2. <span data-ttu-id="bde06-118">Merhaba web hizmeti tanımının Al</span><span class="sxs-lookup"><span data-stu-id="bde06-118">Get hello web service definition</span></span>
3. <span data-ttu-id="bde06-119">Merhaba Web hizmeti tanımının JSON olarak dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="bde06-119">Export hello Web Service Definition as JSON</span></span>
4. <span data-ttu-id="bde06-120">Merhaba başvuru toohello ilearner blob hello JSON güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="bde06-120">Update hello reference toohello ilearner blob in hello JSON.</span></span>
5. <span data-ttu-id="bde06-121">İçeri aktarma hello JSON Web hizmeti tanımının içinde</span><span class="sxs-lookup"><span data-stu-id="bde06-121">Import hello JSON into a Web Service Definition</span></span>
6. <span data-ttu-id="bde06-122">Yeni Web hizmeti tanımının ile Merhaba web hizmetini güncelleştirmek</span><span class="sxs-lookup"><span data-stu-id="bde06-122">Update hello web service with new Web Service Definition</span></span>

## <a name="sign-in-tooyour-azure-resource-manager-account"></a><span data-ttu-id="bde06-123">Tooyour Azure Resource Manager hesabı oturum</span><span class="sxs-lookup"><span data-stu-id="bde06-123">Sign in tooyour Azure Resource Manager account</span></span>
<span data-ttu-id="bde06-124">Tooyour hello PowerShell ortamında hello kullanarak Azure hesabından ilk imzalamalısınız [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bde06-124">You must first sign in tooyour Azure account from within hello PowerShell environment using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-hello-web-service-definition"></a><span data-ttu-id="bde06-125">Merhaba Web hizmeti tanımının Al</span><span class="sxs-lookup"><span data-stu-id="bde06-125">Get hello Web Service Definition</span></span>
<span data-ttu-id="bde06-126">Ardından, hello Web hizmeti arama hello tarafından alma [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bde06-126">Next, get hello Web Service by calling hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="bde06-127">Merhaba Web hizmeti tanımının hello eğitilen model hello web hizmetinin iç bir gösterimini ve doğrudan değiştirilebilir değil.</span><span class="sxs-lookup"><span data-stu-id="bde06-127">hello Web Service Definition is an internal representation of hello trained model of hello web service and is not directly modifiable.</span></span> <span data-ttu-id="bde06-128">Tahmine dayalı denemenizi ve değil eğitim denemenizi hello Web hizmeti tanımının alırsınız emin olun.</span><span class="sxs-lookup"><span data-stu-id="bde06-128">Make sure that you are retrieving hello Web Service Definition for your Predictive experiment and not your training experiment.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="bde06-129">toodetermine hello kaynak grubu adı var olan bir web hizmeti, aboneliğinizdeki tüm parametreleri toodisplay hello web Hizmetleri olmadan hello Get-AzureRmMlWebService cmdlet'ini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bde06-129">toodetermine hello resource group name of an existing web service, run hello Get-AzureRmMlWebService cmdlet without any parameters toodisplay hello web services in your subscription.</span></span> <span data-ttu-id="bde06-130">Merhaba web hizmetini bulun ve sonra web hizmeti kimliğini arayın</span><span class="sxs-lookup"><span data-stu-id="bde06-130">Locate hello web service, and then look at its web service ID.</span></span> <span data-ttu-id="bde06-131">Hello hello kaynak grubunun adıdır hello dördüncü hello kimliği öğesinde yalnızca hello sonra *resourceGroups* öğesi.</span><span class="sxs-lookup"><span data-stu-id="bde06-131">hello name of hello resource group is hello fourth element in hello ID, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="bde06-132">Aşağıdaki örneğine hello hello kaynak grubu adı varsayılan MachineLearning SouthCentralUS ' dir.</span><span class="sxs-lookup"><span data-stu-id="bde06-132">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="bde06-133">Alternatif olarak, toodetermine hello kaynak grubu adı varolan bir web hizmeti, günlük toohello Microsoft Azure Machine Learning Web Hizmetleri portalındaki.</span><span class="sxs-lookup"><span data-stu-id="bde06-133">Alternatively, toodetermine hello resource group name of an existing web service, log on toohello Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="bde06-134">Merhaba web hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="bde06-134">Select hello web service.</span></span> <span data-ttu-id="bde06-135">Merhaba kaynak grubu adı öğedir hello beşinci hello hello web hizmeti URL'sini hemen sonra hello *resourceGroups* öğesi.</span><span class="sxs-lookup"><span data-stu-id="bde06-135">hello resource group name is hello fifth element of hello URL of hello web service, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="bde06-136">Aşağıdaki örneğine hello hello kaynak grubu adı varsayılan MachineLearning SouthCentralUS ' dir.</span><span class="sxs-lookup"><span data-stu-id="bde06-136">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-as-json"></a><span data-ttu-id="bde06-137">Merhaba Web hizmeti tanımının JSON olarak dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="bde06-137">Export hello Web Service Definition as JSON</span></span>
<span data-ttu-id="bde06-138">toomodify hello tanımı toohello eğitilmiş model toouse Merhaba yeni eğitilen Model, ilk hello kullanmalısınız [verme AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport onu tooa JSON biçim dosyası.</span><span class="sxs-lookup"><span data-stu-id="bde06-138">toomodify hello definition toohello trained model toouse hello newly Trained Model, you must first use hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport it tooa JSON format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob-in-hello-json"></a><span data-ttu-id="bde06-139">Merhaba başvuru toohello ilearner blob hello JSON güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="bde06-139">Update hello reference toohello ilearner blob in hello JSON.</span></span>
<span data-ttu-id="bde06-140">Merhaba [eğitilen model], güncelleştirme hello Hello varlıkları bulun *URI* hello değerinde *locationInfo* hello hello ilearner blob URI'si düğümle.</span><span class="sxs-lookup"><span data-stu-id="bde06-140">In hello assets, locate hello [trained model], update hello *uri* value in hello *locationInfo* node with hello URI of hello ilearner blob.</span></span> <span data-ttu-id="bde06-141">Merhaba URI hello birleştirerek oluşturulan *BaseLocation* ve hello *RelativeLocation* hello BES yeniden eğitme çağrısı hello çıktısından.</span><span class="sxs-lookup"><span data-stu-id="bde06-141">hello URI is generated by combining hello *BaseLocation* and hello *RelativeLocation* from hello output of hello BES retraining call.</span></span> <span data-ttu-id="bde06-142">Merhaba yolu tooreference hello yeni eğitilen model güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="bde06-142">This updates hello path tooreference hello new trained model.</span></span>

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

## <a name="import-hello-json-into-a-web-service-definition"></a><span data-ttu-id="bde06-143">İçeri aktarma hello JSON Web hizmeti tanımının içinde</span><span class="sxs-lookup"><span data-stu-id="bde06-143">Import hello JSON into a Web Service Definition</span></span>
<span data-ttu-id="bde06-144">Merhaba kullanmalısınız [alma AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello geri bir Web hizmeti tooupdate hello Web hizmeti tanımının kullanabileceğiniz tanımının JSON dosyasını değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="bde06-144">You must use hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modified JSON file back into a Web Service Definition that you can use tooupdate hello Web Service Definition.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service-with-new-web-service-definition"></a><span data-ttu-id="bde06-145">Yeni Web hizmeti tanımının ile Merhaba web hizmetini güncelleştirmek</span><span class="sxs-lookup"><span data-stu-id="bde06-145">Update hello web service with new Web Service Definition</span></span>
<span data-ttu-id="bde06-146">Son olarak, kullandığınız [güncelleştirme AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello Web hizmeti tanımının.</span><span class="sxs-lookup"><span data-stu-id="bde06-146">Finally, you use [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello Web Service Definition.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a><span data-ttu-id="bde06-147">Özet</span><span class="sxs-lookup"><span data-stu-id="bde06-147">Summary</span></span>
<span data-ttu-id="bde06-148">Hello Machine Learning PowerShell Yönetimi cmdlet'lerini kullanarak, Tahmine dayalı bir Web hizmeti gibi senaryoları etkinleştirme hello eğitilen modelini güncelleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bde06-148">Using hello Machine Learning PowerShell management cmdlets, you can update hello trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="bde06-149">Yeni verilerle yeniden eğitme düzenli modeli.</span><span class="sxs-lookup"><span data-stu-id="bde06-149">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="bde06-150">Kullanıcıların kendi verilerini kullanarak hello modeli yeniden eğitme yapmalarına izin hello amacı ile bir model toocustomers dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="bde06-150">Distribution of a model toocustomers with hello goal of letting them retrain hello model using their own data.</span></span>

