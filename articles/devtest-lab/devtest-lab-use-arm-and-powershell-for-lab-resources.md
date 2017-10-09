---
title: "aaaCreate veya PowerShell ile otomatik olarak Azure Resource Manager şablonları kullanarak labs değiştirme | Microsoft Docs"
description: "Öğrenin nasıl toouse Azure Resource Manager şablonları PowerShell toocreate ile veya otomatik olarak DevTest lab labs değiştirme"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: dad9944c-0b20-48be-ba80-8f4aa0950903
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: 29c8bc67caaec17b1f8926dde4e5d9d314b06600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-modify-labs-automatically-using-azure-resource-manager-templates-and-powershell"></a>Oluşturun veya Azure Resource Manager şablonları ve PowerShell kullanılarak otomatik olarak labs değiştirin.

DevTest Labs birçok Azure Resource Manager şablonları ve hızlı bir şekilde Yardım ve otomatik olarak yeni labs oluşturmak veya var olan Laboratuarları değiştirebilir ve ardından bu kaynakları dağıtabilirsiniz PowerShell komut dosyaları sağlar.

Bu makalede, bu şablonları ve komut dosyaları tooautomate hello oluşturulması, değiştirilmesi ve, labs dağıtımını kullanarak hello işleminde size kılavuzluk yardımcı olur. Bu makalede ayrıca nasıl toouse PowerShell tooperform DevTest Labs'de bazı ortak görevler hakkında daha fazla bilgi bulabileceği yerler gösterilmektedir.

## <a name="step-1-gather-your-templates-and-scripts"></a>Adım 1: şablonları ve komut dosyaları toplama
Önceden yapılan bulabilir [Azure Resource Manager şablonları](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) ve [PowerShell komut dosyalarını](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) ortak adresindeki [Github deposunu](https://github.com/Azure/azure-devtestlab). Bunları kullanın-olan veya gereksinimlerinize göre özelleştirmek ve bunları kendi içinde depolamak [özel Git deposuna](devtest-lab-add-artifact-repo.md). 

## <a name="step-2-modify-your-azure-resource-manager-template"></a>2. adım: Azure Resource Manager şablonunu değiştirme
Merhaba adımları izleyin [, ilk Azure Resource Manager şablonu oluşturma](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) hiçbir zaman önce bir şablon oluşturduysanız.

Ayrıca, [en iyi uygulamalar Azure Resource Manager şablonları oluşturmak için](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) birçok kılavuzları ve önerileri toohelp sunar güvenilir ve kolay toouse olan Azure Resource Manager şablonları oluşturun. Genellikle, bir çeşitlemesi hello yaklaşımlardan birini kullanın veya örnekler sağlanan ve şablonunuzu gereksinimleriniz için değiştirin.

## <a name="step-3-deploy-resources-with-powershell"></a>Adım 3: PowerShell kaynaklarla dağıtma
Şablonlar ve komut dosyalarınız özelleştirdikten sonra hello gerekli çok adımları[Resource Manager şablonları ve Azure PowerShell ile kaynakları dağıtmak](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy). Merhaba makale kaynakları tooAzure Azure Resource Manager şablonları toodeploy ile Azure PowerShell'i kullanma hakkında genel bilgi sağlar.


## <a name="common-tasks-you-can-perform-in-devtest-labs-using-powershell"></a>PowerShell kullanarak DevTest Labs'de gerçekleştirdiğiniz ortak görevler
PowerShell kullanarak otomatikleştirebilirsiniz birçok diğer ortak görevler vardır. Merhaba aşağıdaki bölümlerde hello belgelerin hello adımları gerekli tooperform bu görevler verilmiştir.

* [PowerShell kullanarak bir VHD'yi dosyasından özel bir görüntü oluşturun](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
* [PowerShell kullanarak VHD dosyasını toolab ait depolama hesabı karşıya yükle](devtest-lab-upload-vhd-using-powershell.md)
* [PowerShell kullanarak bir dış kullanıcı tooa Laboratuvar ekleme](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell)
* [PowerShell kullanarak bir lab özel rolü oluşturun](devtest-lab-grant-user-permissions-to-specific-lab-policies.md#creating-a-lab-custom-role-using-powershell)

### <a name="next-steps"></a>Sonraki adımlar
* Bilgi nasıl toocreate bir [özel Git deposu](devtest-lab-add-artifact-repo.md) depolayacağınız özelleştirilmiş şablonları veya komut dosyaları.
* Merhaba keşfedin [Azure Resource Manager şablonları Azure hızlı başlangıç Şablon Galerisinden](https://github.com/Azure/azure-quickstart-templates).
