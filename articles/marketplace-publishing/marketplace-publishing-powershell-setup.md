---
title: "Market bir VM oluşturmak için PowerShell ayarlama | Microsoft Docs"
description: "Azure PowerShell ayarlama ve isteğe bağlı bir işlem olarak kullanmak için yönergeler dağıtmak için VM görüntüleri oluşturmak için akış ve Azure Market, satış"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e19d6cda-76df-4e42-be84-c9fe47a636db
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/04/2016
ms.author: hascipio
ms.openlocfilehash: bbcce5093d2bbd5326523063db7d0e565fe4de6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-azure-powershell-to-create-an-offer-for-the-azure-marketplace"></a>Azure Market teklifi oluşturmak için Azure PowerShell ayarlayın
Azure PowerShell'de ayarlama konusunda ayrıntılı bilgi için bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview). Basit bir yaklaşım indirir ve kimlik doğrulaması için gerekli olan bir sertifika alır sertifika yöntemini kullanmaktır. Gerekli sertifikayı almak için kullanın **Get-AzurePublishSettingsFile** cmdlet'i. İstendiğinde dosyayı kaydedin. Sertifika bir PowerShell oturumuna içeri aktarmak için kullanın **Import-AzurePublishSettingsFile** cmdlet'i.

Yapılandırma ve PowerShell oturumu için genel Microsoft Azure abonelik ayarlarını depolamak için kullanmak **Set-AzureSubscription** ve **Select-AzureSubscription** cmdlet:

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

İlk komut bir varsayılan depolama hesabı (bazı VM sağlama işlemleri için gereklidir) aboneliğiyle ilişkilendirir.  İkinci (diğer cmdlet'leri tarafından tanınan) geçerli bir abonelik yapar.

## <a name="see-also"></a>Ayrıca bkz.
* [Başlarken: bir teklifi Azure Marketinde yayımlama](marketplace-publishing-getting-started.md)
* [Market bir sanal makine görüntüsü oluşturma](marketplace-publishing-vm-image-creation.md)

