---
title: "PowerShell toocreate hello Market için bir VM yukarı aaaSet | Microsoft Docs"
description: "Azure PowerShell ayarlama ve isteğe bağlı bir işlem olarak kullanmak için yönergeler toocreate VM görüntüleri toodeploy için akış ve üzerinde satmak, Azure Marketi hello"
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
ms.openlocfilehash: cd2ebad7472248b8f921706e1a8c82d41f33b9cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-powershell-toocreate-an-offer-for-hello-azure-marketplace"></a>Azure PowerShell toocreate hello Azure Marketi teklifi ayarlayın
Hakkında ayrıntılı bilgi için Azure PowerShell'de yukarı tooset bkz [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview). Basit bir yaklaşım indirir ve kimlik doğrulaması için gerekli olan bir sertifika alır toouse hello sertifika yöntemidir. tooobtain hello, sertifika hello kullan **Get-AzurePublishSettingsFile** cmdlet'i. İstendiğinde hello dosyasını kaydedin. bir PowerShell oturumuna kullanım hello tooimport hello sertifika **Import-AzurePublishSettingsFile** cmdlet'i.

tooconfigure ve deposu hello genel Microsoft Azure abonelik ayarlarını hello PowerShell oturumunda, kullanmak hello **Set-AzureSubscription** ve **Select-AzureSubscription** cmdlet:

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

Merhaba ilk komut varsayılan depolama hesabı (bazı VM sağlama işlemleri için gereklidir) hello aboneliğiyle ilişkilendirir.  Merhaba, ikinci (diğer cmdlet'leri tarafından tanınan) geçerli bir hello hello abonelik yapar.

## <a name="see-also"></a>Ayrıca bkz.
* [Başlarken: nasıl toopublish bir teklif toohello Azure Market](marketplace-publishing-getting-started.md)
* [Merhaba Market için bir sanal makine görüntüsü oluşturma](marketplace-publishing-vm-image-creation.md)

