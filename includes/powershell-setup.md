---
services: virtual-machines
title: PowerShell ayarlama
author: JoeDavies-MSFT
solutions: 
manager: timlt
editor: tysonn
ms.service: virtual-machines
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/12/2015
ms.author: rasquill
ms.openlocfilehash: 19c704d965ff3e2fc9ac8c5b623aeb386cb0b974
ms.sourcegitcommit: e19f6a1709b0fe0f898386118fbef858d430e19d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/16/2018
---
## <a name="setting-up-powershell"></a>PowerShell ayarlama
Azure PowerShell kullanmadan önce aşağıdaki adımları izleyin.

### <a name="verify-powershell-versions"></a>PowerShell sürümlerini doğrulama
Windows PowerShell kullanabilmek için Windows PowerShell, sürüm 3.0 veya 4.0 olması gerekir. Windows PowerShell sürümü bulmak için Windows PowerShell komut isteminde bu komutu yazın.

    $PSVersionTable

Şöyle bir şey görmeniz gerekir.

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2

Doğrulayın değerini **PSVersion** 3.0 veya 4.0. Uyumlu bir sürümünü yüklemek için bkz: [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) veya [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).

Azure PowerShell sürüm 0.8.0 sahip olmalıdır veya sonraki bir sürümü. Azure PowerShell komut isteminde bu komutla yüklediğiniz Azure PowerShell sürümü kontrol edebilirsiniz.

    Get-Module azure | format-table version

Şöyle bir şey görmeniz gerekir.

    Version
    -------
    0.8.16.1

Yönergeler ve en son sürüme bir bağlantı için bkz: [yükleme ve yapılandırma Azure PowerShell](/powershell/azureps-cmdlets-docs).

### <a name="set-your-azure-account-and-subscription"></a>Azure hesabınızı ve aboneliğinizi ayarlama
Bir Azure aboneliği zaten sahip değilseniz, etkinleştirebilir, [MSDN abone Avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) veya kaydolun bir [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).

Bu komutla bir Azure PowerShell komut istemi ve Azure oturumunu açın.

    Add-AzureAccount

Birden çok Azure aboneliğiniz varsa, bu komutla, Azure aboneliklerinize listeleyebilirsiniz.

    Get-AzureSubscription

Aşağıdaki türde bilgiler alırsınız:

    SubscriptionId            : fd22919d-eaca-4f2b-841a-e4ac6770g92e
    SubscriptionName          : Visual Studio Ultimate with MSDN
    Environment               : AzureCloud
    SupportedModes            : AzureServiceManagement,AzureResourceManager
    DefaultAccount            : johndoe@contoso.com
    Accounts                  : {johndoe@contoso.com}
    IsDefault                 : True
    IsCurrent                 : True
    CurrentStorageAccountName : 
    TenantId                  : 32fa88b4-86f1-419f-93ab-2d7ce016dba7

Azure PowerShell komut isteminde şu komutları çalıştırarak geçerli Azure aboneliği ayarlayabilirsiniz. Dahil olmak üzere tırnak işaretleri içindeki her şeyi değiştirin < ve > karakterleri doğru ada sahip.

    $subscr="<SubscriptionName from the display of Get-AzureSubscription>"
    Select-AzureSubscription -SubscriptionName $subscr -Current    

Azure abonelikleri ve hesapları hakkında daha fazla bilgi için bkz: [nasıl yapılır: aboneliğinize bağlanma](/powershell/azureps-cmdlets-docs#Connect).

