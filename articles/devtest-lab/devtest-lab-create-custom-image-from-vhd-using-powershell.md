---
title: "PowerShell kullanarak bir VHD dosyasının bir Azure DevTest Labs özel görüntüden aaaCreate | Microsoft Docs"
description: "Azure DevTest Labs PowerShell kullanarak bir VHD'yi dosyasından özel görüntü oluşturulmasını otomatik hale getirme"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 39b4005fa46cdf86cf0800ca376128134bcfb650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a><span data-ttu-id="4d748-103">PowerShell kullanarak bir VHD'yi dosyasından özel bir görüntü oluşturun</span><span class="sxs-lookup"><span data-stu-id="4d748-103">Create a custom image from a VHD file using PowerShell</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="4d748-104">Adım adım yönergeler</span><span class="sxs-lookup"><span data-stu-id="4d748-104">Step-by-step instructions</span></span>

<span data-ttu-id="4d748-105">Merhaba aşağıdaki adımlar, özel bir görüntü PowerShell kullanarak bir VHD'yi dosyasından oluşturmada size yol:</span><span class="sxs-lookup"><span data-stu-id="4d748-105">hello following steps walk you through creating a custom image from a VHD file using PowerShell:</span></span>

1. <span data-ttu-id="4d748-106">Bir PowerShell komut isteminde, tooyour Azure hesabı çağrı toohello aşağıdaki hello ile oturum **Login-AzureRmAccount** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="4d748-106">At a PowerShell prompt, log in tooyour Azure account with hello following call toohello **Login-AzureRmAccount** cmdlet.</span></span>  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  <span data-ttu-id="4d748-107">Select hello tarafından arama hello Azure aboneliği istenen **Select-AzureRmSubscription** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="4d748-107">Select hello desired Azure subscription by calling hello **Select-AzureRmSubscription** cmdlet.</span></span> <span data-ttu-id="4d748-108">Hello için yer tutucu aşağıdaki hello yerine **$subscriptionId** geçerli Azure aboneliği ID'ye sahip değişken</span><span class="sxs-lookup"><span data-stu-id="4d748-108">Replace hello following placeholder for hello **$subscriptionId** variable with a valid Azure subscription ID.</span></span> 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  <span data-ttu-id="4d748-109">Merhaba Laboratuvar nesnesi tarafından arama hello elde **Get-AzureRmResource** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="4d748-109">Get hello lab object by calling hello **Get-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="4d748-110">Merhaba yer tutucular aşağıdaki hello yerine **$labRg** ve **$labName** hello değişkenlerin değerleri, ortamınız için uygun.</span><span class="sxs-lookup"><span data-stu-id="4d748-110">Replace hello following placeholders for hello **$labRg** and **$labName** variables with hello appropriate values for your environment.</span></span> 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  <span data-ttu-id="4d748-111">Merhaba Laboratuvar depolama hesabı ve Laboratuvar depolama hesabı anahtar değerleri hello Laboratuvar nesnesinden alır.</span><span class="sxs-lookup"><span data-stu-id="4d748-111">Get hello lab storage account and lab storage account key values from hello lab object.</span></span> 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  <span data-ttu-id="4d748-112">Hello için yer tutucu aşağıdaki hello yerine **$vhdUri** hello URI ile değişken tooyour VHD dosyasını karşıya.</span><span class="sxs-lookup"><span data-stu-id="4d748-112">Replace hello following placeholder for hello **$vhdUri** variable with hello URI tooyour uploaded VHD file.</span></span> <span data-ttu-id="4d748-113">Merhaba VHD dosyasının URI hello Azure portal'ın hello depolama hesabının blob dikey penceresinden alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d748-113">You can get hello VHD file's URI from hello storage account's blob blade in hello Azure portal.</span></span>

    ```PowerShell
    $vhdUri = '<Specify hello VHD URI here>'
    ```

1.  <span data-ttu-id="4d748-114">Hello kullanarak hello özel görüntü oluşturma **New-AzureRmResourceGroupDeployment** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="4d748-114">Create hello custom image using hello **New-AzureRmResourceGroupDeployment** cmdlet.</span></span> <span data-ttu-id="4d748-115">Merhaba yer tutucular aşağıdaki hello yerine **$customImageName** ve **$customImageDescription** ortamınız için değişkenleri toomeaningful adları.</span><span class="sxs-lookup"><span data-stu-id="4d748-115">Replace hello following placeholders for hello **$customImageName** and **$customImageDescription** variables toomeaningful names for your environment.</span></span>

    ```PowerShell
    $customImageName = '<Specify hello custom image name>'
    $customImageDescription = '<Specify hello custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-toocreate-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="4d748-116">PowerShell komut dosyası toocreate bir VHD dosyasında özel bir görüntü</span><span class="sxs-lookup"><span data-stu-id="4d748-116">PowerShell script toocreate a custom image from a VHD file</span></span>

<span data-ttu-id="4d748-117">PowerShell Betiği aşağıdaki hello kullanılan toocreate bir VHD dosyasında özel bir görüntü olabilir.</span><span class="sxs-lookup"><span data-stu-id="4d748-117">hello following PowerShell script can be used toocreate a custom image from a VHD file.</span></span> <span data-ttu-id="4d748-118">(Başlangıç ve köşeli parantez ile biten) hello yer tutucuları hello gereksinimlerinize uygun değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4d748-118">Replace hello placeholders (starting and ending with angle brackets) with hello appropriate values for your needs.</span></span> 

```PowerShell
# Log in tooyour Azure account.  
Login-AzureRmAccount

# Select hello desired Azure subscription. 
$subscriptionId = '<Specify your subscription ID here>'
Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Get hello lab object.
$labRg = '<Specify your lab resource group name here>'
$labName = '<Specify your lab name here>'
$lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)

# Get hello lab storage account and lab storage account key values.
$labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
$labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value

# Set hello URI of hello VHD file.  
$vhdUri = '<Specify hello VHD URI here>'

# Set hello custom image name and description values.
$customImageName = '<Specify hello custom image name>'
$customImageDescription = '<Specify hello custom image description>'

# Set up hello parameters object.
$parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

# Create hello custom image. 
New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
```

## <a name="related-blog-posts"></a><span data-ttu-id="4d748-119">İlgili blog gönderileri</span><span class="sxs-lookup"><span data-stu-id="4d748-119">Related blog posts</span></span>

- [<span data-ttu-id="4d748-120">Özel resimler veya formüller?</span><span class="sxs-lookup"><span data-stu-id="4d748-120">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="4d748-121">Azure DevTest Labs arasında özel resimler kopyalama</span><span class="sxs-lookup"><span data-stu-id="4d748-121">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="4d748-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4d748-122">Next steps</span></span>

- [<span data-ttu-id="4d748-123">VM tooyour Laboratuvar ekleme</span><span class="sxs-lookup"><span data-stu-id="4d748-123">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
