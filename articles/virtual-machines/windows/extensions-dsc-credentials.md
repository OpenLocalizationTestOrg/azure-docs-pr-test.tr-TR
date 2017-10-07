---
title: aaaPassing tooAzure DSC kullanarak kimlik bilgileri | Microsoft Docs
description: "PowerShell istenen durum yapılandırması kullanarak tooAzure sanal makineleri kimlik bilgilerini güvenli bir şekilde geçirme hakkında genel bakış"
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: ea76b7e8-b576-445a-8107-88ea2f3876b9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: 306ecd3fd481f49a0beca5052fc7531a52999330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="passing-credentials-toohello-azure-dsc-extension-handler"></a>Kimlik bilgileri toohello Azure DSC uzantısı işleyici geçirme
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Bu makalede, Azure için hello istenen durum yapılandırması uzantısı yer almaktadır. Merhaba DSC uzantısı işleyicisi genel bir bakış bulunabilir [giriş toohello Azure istenen durum yapılandırması uzantısı işleyici](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="passing-in-credentials"></a>Kimlik bilgilerinde
Merhaba yapılandırma işleminin bir parçası olarak tooset gerekebilir kullanıcı hesapları, Erişim Hizmetleri veya kullanıcı bağlamında bir program yüklemek. toodo bu işlemleri tooprovide kimlik bilgileri gerekir. 

DSC kimlik bilgileri, hello yapılandırma geçirilen ve güvenli bir şekilde MOF dosyasında depolanan parametreli yapılandırmalarını sağlar. Hello Azure uzantısı işleyici sertifikaların otomatik yönetimi sağlayarak kimlik bilgileri yönetimi basitleştirir. 

Merhaba belirtilen parola ile yerel bir kullanıcı hesabı oluşturur DSC yapılandırma betiği aşağıdaki hello göz önünde bulundurun:

*user_configuration.ps1*

```
configuration Main
{
    param(
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PSCredential]
        $Credential
    )    
    Node localhost {       
        User LocalUserAccount
        {
            Username = $Credential.UserName
            Password = $Credential
            Disabled = $false
            Ensure = "Present"
            FullName = "Local User Account"
            Description = "Local User Account"
            PasswordNeverExpires = $true
        } 
    }  
} 
```

Önemli tooinclude olan *düğümü localhost* hello yapılandırmasının bir parçası olarak. Bu bildirimi eksikse, hello uzantısı işleyici hello düğümü localhost deyimi için özel olarak göründüğü gibi hello aşağıdaki adımları çalışmaz. Ayrıca tooinclude hello typecast önemlidir *[PsCredential]*gibi hello uzantısı tooencrypt hello kimlik bilgisi bu belirli tür tetikler. 

Bu komut dosyası tooblob depolama yayımlayın:

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

Hello Azure DSC uzantısı ayarlayabilir ve hello kimlik bilgilerini girin:

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a>Kimlik bilgileri güvenliği nasıl
Bu kodu çalıştırmak için kimlik bilgilerini ister. Sağlanan sonra onu kısaca bellekte depolanır. Ne zaman onu yayımlanır ile `Set-AzureVmDscExtension` cmdlet, bunu HTTPS toohello VM aktarılan, Azure burada depolar hello yerel VM sertifika kullanarak diskte şifrelenmiş. Bellek ve yeniden şifrelenmiş toopass kısaca şifresi çözülmüş sonra onu tooDSC.

Bu davranış farklıdır [hello uzantısı işleyici olmadan güvenli yapılandırmaları kullanarak](https://msdn.microsoft.com/powershell/dsc/securemof). Hello Azure ortamı sertifikalar yoluyla güvenli şekilde tootransmit yapılandırma verilerini sağlar. Merhaba DSC uzantısı işleyici kullanırken hiçbir gerek tooprovide $CertificatePath veya bir $CertificateID yoktur / ConfigurationData $Thumbprint girişi.

## <a name="next-steps"></a>Sonraki adımlar
Hello Azure DSC uzantısı işleyici hakkında daha fazla bilgi için bkz: [giriş toohello Azure istenen durum yapılandırması uzantısı işleyici](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Merhaba inceleyin [hello DSC uzantısı için Azure Resource Manager şablonu](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

PowerShell DSC hakkında daha fazla bilgi için [hello PowerShell Belge Merkezi ziyaret](https://msdn.microsoft.com/powershell/dsc/overview). 

PowerShell DSC ile yönetebileceğiniz toofind işlevsellikler [hello PowerShell Galerisi Gözat](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) daha fazla DSC kaynakları için.

