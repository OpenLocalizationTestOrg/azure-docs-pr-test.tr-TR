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
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a>PowerShell kullanarak bir VHD'yi dosyasından özel bir görüntü oluşturun

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a>Adım adım yönergeler

Merhaba aşağıdaki adımlar, özel bir görüntü PowerShell kullanarak bir VHD'yi dosyasından oluşturmada size yol:

1. Bir PowerShell komut isteminde, tooyour Azure hesabı çağrı toohello aşağıdaki hello ile oturum **Login-AzureRmAccount** cmdlet'i.  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  Select hello tarafından arama hello Azure aboneliği istenen **Select-AzureRmSubscription** cmdlet'i. Hello için yer tutucu aşağıdaki hello yerine **$subscriptionId** geçerli Azure aboneliği ID'ye sahip değişken 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  Merhaba Laboratuvar nesnesi tarafından arama hello elde **Get-AzureRmResource** cmdlet'i. Merhaba yer tutucular aşağıdaki hello yerine **$labRg** ve **$labName** hello değişkenlerin değerleri, ortamınız için uygun. 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  Merhaba Laboratuvar depolama hesabı ve Laboratuvar depolama hesabı anahtar değerleri hello Laboratuvar nesnesinden alır. 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  Hello için yer tutucu aşağıdaki hello yerine **$vhdUri** hello URI ile değişken tooyour VHD dosyasını karşıya. Merhaba VHD dosyasının URI hello Azure portal'ın hello depolama hesabının blob dikey penceresinden alabilirsiniz.

    ```PowerShell
    $vhdUri = '<Specify hello VHD URI here>'
    ```

1.  Hello kullanarak hello özel görüntü oluşturma **New-AzureRmResourceGroupDeployment** cmdlet'i. Merhaba yer tutucular aşağıdaki hello yerine **$customImageName** ve **$customImageDescription** ortamınız için değişkenleri toomeaningful adları.

    ```PowerShell
    $customImageName = '<Specify hello custom image name>'
    $customImageDescription = '<Specify hello custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-toocreate-a-custom-image-from-a-vhd-file"></a>PowerShell komut dosyası toocreate bir VHD dosyasında özel bir görüntü

PowerShell Betiği aşağıdaki hello kullanılan toocreate bir VHD dosyasında özel bir görüntü olabilir. (Başlangıç ve köşeli parantez ile biten) hello yer tutucuları hello gereksinimlerinize uygun değerlerle değiştirin. 

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

## <a name="related-blog-posts"></a>İlgili blog gönderileri

- [Özel resimler veya formüller?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Azure DevTest Labs arasında özel resimler kopyalama](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Sonraki adımlar

- [VM tooyour Laboratuvar ekleme](./devtest-lab-add-vm-with-artifacts.md)
