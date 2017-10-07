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
# <a name="passing-credentials-toohello-azure-dsc-extension-handler"></a><span data-ttu-id="2a70d-103">Kimlik bilgileri toohello Azure DSC uzantısı işleyici geçirme</span><span class="sxs-lookup"><span data-stu-id="2a70d-103">Passing credentials toohello Azure DSC extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="2a70d-104">Bu makalede, Azure için hello istenen durum yapılandırması uzantısı yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="2a70d-104">This article covers hello Desired State Configuration extension for Azure.</span></span> <span data-ttu-id="2a70d-105">Merhaba DSC uzantısı işleyicisi genel bir bakış bulunabilir [giriş toohello Azure istenen durum yapılandırması uzantısı işleyici](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2a70d-105">An overview of hello DSC extension handler can be found at [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="passing-in-credentials"></a><span data-ttu-id="2a70d-106">Kimlik bilgilerinde</span><span class="sxs-lookup"><span data-stu-id="2a70d-106">Passing in credentials</span></span>
<span data-ttu-id="2a70d-107">Merhaba yapılandırma işleminin bir parçası olarak tooset gerekebilir kullanıcı hesapları, Erişim Hizmetleri veya kullanıcı bağlamında bir program yüklemek.</span><span class="sxs-lookup"><span data-stu-id="2a70d-107">As a part of hello configuration process, you may need tooset up user accounts, access services, or install a program in a user context.</span></span> <span data-ttu-id="2a70d-108">toodo bu işlemleri tooprovide kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a70d-108">toodo these things, you need tooprovide credentials.</span></span> 

<span data-ttu-id="2a70d-109">DSC kimlik bilgileri, hello yapılandırma geçirilen ve güvenli bir şekilde MOF dosyasında depolanan parametreli yapılandırmalarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a70d-109">DSC allows for parameterized configurations in which credentials are passed into hello configuration and securely stored in MOF files.</span></span> <span data-ttu-id="2a70d-110">Hello Azure uzantısı işleyici sertifikaların otomatik yönetimi sağlayarak kimlik bilgileri yönetimi basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="2a70d-110">hello Azure Extension Handler simplifies credential management by providing automatic management of certificates.</span></span> 

<span data-ttu-id="2a70d-111">Merhaba belirtilen parola ile yerel bir kullanıcı hesabı oluşturur DSC yapılandırma betiği aşağıdaki hello göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="2a70d-111">Consider hello following DSC configuration script that creates a local user account with hello specified password:</span></span>

<span data-ttu-id="2a70d-112">*user_configuration.ps1*</span><span class="sxs-lookup"><span data-stu-id="2a70d-112">*user_configuration.ps1*</span></span>

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

<span data-ttu-id="2a70d-113">Önemli tooinclude olan *düğümü localhost* hello yapılandırmasının bir parçası olarak.</span><span class="sxs-lookup"><span data-stu-id="2a70d-113">It is important tooinclude *node localhost* as part of hello configuration.</span></span> <span data-ttu-id="2a70d-114">Bu bildirimi eksikse, hello uzantısı işleyici hello düğümü localhost deyimi için özel olarak göründüğü gibi hello aşağıdaki adımları çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="2a70d-114">If this statement is missing, hello following steps do not work as hello extension handler specifically looks for hello node localhost statement.</span></span> <span data-ttu-id="2a70d-115">Ayrıca tooinclude hello typecast önemlidir *[PsCredential]*gibi hello uzantısı tooencrypt hello kimlik bilgisi bu belirli tür tetikler.</span><span class="sxs-lookup"><span data-stu-id="2a70d-115">It is also important tooinclude hello typecast *[PsCredential]*, as this specific type triggers hello extension tooencrypt hello credential.</span></span> 

<span data-ttu-id="2a70d-116">Bu komut dosyası tooblob depolama yayımlayın:</span><span class="sxs-lookup"><span data-stu-id="2a70d-116">Publish this script tooblob storage:</span></span>

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

<span data-ttu-id="2a70d-117">Hello Azure DSC uzantısı ayarlayabilir ve hello kimlik bilgilerini girin:</span><span class="sxs-lookup"><span data-stu-id="2a70d-117">Set hello Azure DSC extension and provide hello credential:</span></span>

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a><span data-ttu-id="2a70d-118">Kimlik bilgileri güvenliği nasıl</span><span class="sxs-lookup"><span data-stu-id="2a70d-118">How credentials are secured</span></span>
<span data-ttu-id="2a70d-119">Bu kodu çalıştırmak için kimlik bilgilerini ister.</span><span class="sxs-lookup"><span data-stu-id="2a70d-119">Running this code prompts for a credential.</span></span> <span data-ttu-id="2a70d-120">Sağlanan sonra onu kısaca bellekte depolanır.</span><span class="sxs-lookup"><span data-stu-id="2a70d-120">Once it is provided, it is stored in memory briefly.</span></span> <span data-ttu-id="2a70d-121">Ne zaman onu yayımlanır ile `Set-AzureVmDscExtension` cmdlet, bunu HTTPS toohello VM aktarılan, Azure burada depolar hello yerel VM sertifika kullanarak diskte şifrelenmiş.</span><span class="sxs-lookup"><span data-stu-id="2a70d-121">When it is published with `Set-AzureVmDscExtension` cmdlet, it is transmitted over HTTPS toohello VM, where Azure stores it encrypted on disk, using hello local VM certificate.</span></span> <span data-ttu-id="2a70d-122">Bellek ve yeniden şifrelenmiş toopass kısaca şifresi çözülmüş sonra onu tooDSC.</span><span class="sxs-lookup"><span data-stu-id="2a70d-122">Then it is briefly decrypted in memory and re-encrypted toopass it tooDSC.</span></span>

<span data-ttu-id="2a70d-123">Bu davranış farklıdır [hello uzantısı işleyici olmadan güvenli yapılandırmaları kullanarak](https://msdn.microsoft.com/powershell/dsc/securemof).</span><span class="sxs-lookup"><span data-stu-id="2a70d-123">This behavior is different than [using secure configurations without hello extension handler](https://msdn.microsoft.com/powershell/dsc/securemof).</span></span> <span data-ttu-id="2a70d-124">Hello Azure ortamı sertifikalar yoluyla güvenli şekilde tootransmit yapılandırma verilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a70d-124">hello Azure environment gives a way tootransmit configuration data securely via certificates.</span></span> <span data-ttu-id="2a70d-125">Merhaba DSC uzantısı işleyici kullanırken hiçbir gerek tooprovide $CertificatePath veya bir $CertificateID yoktur / ConfigurationData $Thumbprint girişi.</span><span class="sxs-lookup"><span data-stu-id="2a70d-125">When using hello DSC extension handler, there is no need tooprovide $CertificatePath or a $CertificateID / $Thumbprint entry in ConfigurationData.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a70d-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2a70d-126">Next steps</span></span>
<span data-ttu-id="2a70d-127">Hello Azure DSC uzantısı işleyici hakkında daha fazla bilgi için bkz: [giriş toohello Azure istenen durum yapılandırması uzantısı işleyici](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2a70d-127">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="2a70d-128">Merhaba inceleyin [hello DSC uzantısı için Azure Resource Manager şablonu](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2a70d-128">Examine hello [Azure Resource Manager template for hello DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="2a70d-129">PowerShell DSC hakkında daha fazla bilgi için [hello PowerShell Belge Merkezi ziyaret](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="2a70d-129">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="2a70d-130">PowerShell DSC ile yönetebileceğiniz toofind işlevsellikler [hello PowerShell Galerisi Gözat](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) daha fazla DSC kaynakları için.</span><span class="sxs-lookup"><span data-stu-id="2a70d-130">toofind additional functionality you can manage with PowerShell DSC, [browse hello PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

