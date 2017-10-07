---
title: PowerShell kullanarak bir Azure Analysis Services sunucusuna aaaCreate | Microsoft Docs
description: "Toocreate Azure Analiz Hizmetleri nasıl öğrenin PowerShell kullanarak sunucu"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/01/2017
ms.author: owend
ms.custom: mvc
ms.openlocfilehash: 269b78983410f773d47c4cea34d6d353b19f9e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a>PowerShell kullanarak bir Azure Analysis Services sunucusu oluşturma

Bir Azure Analysis Services sunucusuna hello komut satırı toocreate PowerShell kullanarak bu hızlı başlangıç açıklar bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) Azure aboneliğinizde.

Bu görev için Azure PowerShell modülünün 4.0 veya daha sonraki bir sürümü gerekir. çalıştırma toofind hello sürüm ` Get-Module -ListAvailable AzureRM`. bkz: tooinstall veya yükseltme, [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps). 

> [!NOTE]
> Sunucu oluşturulması ek hizmet ücretlerine neden olabilir. toolearn daha, fazla [Analysis Services fiyatlandırma](https://azure.microsoft.com/pricing/details/analysis-services/).

## <a name="prerequisites"></a>Ön koşullar
toocomplete Bu Hızlı Başlangıç, gerekir:

* **Azure aboneliği**: ziyaret [Azure ücretsiz deneme sürümü](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate bir hesap.
* **Azure Active Directory**: Aboneliğinizin bir Azure Active Directory Kiracısı ile ilişkilendirilmiş olması ve ilgili dizinde bir hesabınızın olması gerekir. toolearn daha, fazla [kimlik doğrulaması ve kullanıcı izinleri](analysis-services-manage-users.md).

## <a name="import-azurermanalysisservices-module"></a>AzureRm.AnalysisServices modülünü içeri aktarın
toocreate aboneliğinizde bir sunucu, kullandığınız hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) Bileşen Modülü. Merhaba AzureRm.AnalysisServices modülü PowerShell oturumunuza yükleyin.

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-tooazure"></a>İçinde tooAzure oturum

Tooyour Azure aboneliği hello kullanarak oturum [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) komutu. Merhaba ekrandaki yönergeleri izleyin.

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma
 
[Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md), Azure kaynaklarının grup olarak dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. Sunucunuzu oluşturduğunuzda, aboneliğinizde bir kaynak grubu belirtmeniz gerekir. Bir kaynak grubu zaten yoksa, hello kullanarak yeni bir tane oluşturabilirsiniz [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) komutu. Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello Batı ABD bölgesindeki.

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a>Sunucu oluşturma

Hello kullanarak yeni bir sunucu oluşturmak [yeni AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) komutu. Merhaba aşağıdaki örnek hello D1 katmanı adresindeki hello Batı ABD bölgesindeki myResourceGroup myServer adlı bir sunucu oluşturur ve belirtir philipc@adventureworks.com sunucu yöneticisi olarak.

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a>Kaynakları temizleme

Hello kullanarak aboneliğinizden hello sunucu kaldırabilirsiniz [Kaldır AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) komutu. Bu koleksiyondaki diğer hızlı başlangıçları ve öğreticileri kullanacaksanız sunucunuzu kaldırmayın. Merhaba aşağıdaki örnek hello önceki adımda oluşturduğunuz hello sunucusunu kaldırır.


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a>Sonraki adımlar
[Azure Analysis Services’ı PowerShell ile yönetme](analysis-services-powershell.md)   
[SSDT’den model dağıtma](analysis-services-deploy.md)   
[Azure portalında bir model oluşturma](analysis-services-create-model-portal.md)