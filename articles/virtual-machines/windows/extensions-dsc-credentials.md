---
title: "DSC kullanarak Azure için kimlik bilgilerini geçirme | Microsoft Docs"
description: "PowerShell istenen durum yapılandırması kullanarak Azure sanal makineleri için kimlik bilgileri güvenli bir şekilde geçirme hakkında genel bakış"
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
ms.openlocfilehash: acd768c0219ec23c0453a65c575faf5213d9c616
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="passing-credentials-to-the-azure-dsc-extension-handler"></a><span data-ttu-id="11d07-103">Kimlik bilgileri Azure DSC uzantısı işleyicisine geçirme</span><span class="sxs-lookup"><span data-stu-id="11d07-103">Passing credentials to the Azure DSC extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="11d07-104">Bu makalede, Azure için istenen durum yapılandırması uzantısı yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="11d07-104">This article covers the Desired State Configuration extension for Azure.</span></span> <span data-ttu-id="11d07-105">DSC uzantı işleyicisi genel bir bakış bulunabilir [Azure istenen durum yapılandırması uzantısı işleyici giriş](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="11d07-105">An overview of the DSC extension handler can be found at [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="passing-in-credentials"></a><span data-ttu-id="11d07-106">Kimlik bilgilerinde</span><span class="sxs-lookup"><span data-stu-id="11d07-106">Passing in credentials</span></span>
<span data-ttu-id="11d07-107">Yapılandırma işleminin bir parçası olarak gerektiğinde kullanıcı hesaplarını, ayarlamak için hizmetlere erişmek veya kullanıcı bağlamında bir program yüklemek.</span><span class="sxs-lookup"><span data-stu-id="11d07-107">As a part of the configuration process, you may need to set up user accounts, access services, or install a program in a user context.</span></span> <span data-ttu-id="11d07-108">Bu işlemler yapmak için kimlik bilgilerini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="11d07-108">To do these things, you need to provide credentials.</span></span> 

<span data-ttu-id="11d07-109">DSC kimlik bilgileri, yapılandırmaya geçirilen ve güvenli bir şekilde MOF dosyasında depolanan parametreli yapılandırmalarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="11d07-109">DSC allows for parameterized configurations in which credentials are passed into the configuration and securely stored in MOF files.</span></span> <span data-ttu-id="11d07-110">Azure uzantısı işleyici sertifikaların otomatik yönetimi sağlayarak kimlik bilgileri yönetimi basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="11d07-110">The Azure Extension Handler simplifies credential management by providing automatic management of certificates.</span></span> 

<span data-ttu-id="11d07-111">Belirtilen parola ile yerel bir kullanıcı hesabı oluşturur aşağıdaki DSC yapılandırma betiği göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="11d07-111">Consider the following DSC configuration script that creates a local user account with the specified password:</span></span>

<span data-ttu-id="11d07-112">*user_configuration.ps1*</span><span class="sxs-lookup"><span data-stu-id="11d07-112">*user_configuration.ps1*</span></span>

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

<span data-ttu-id="11d07-113">Eklenmesi önemlidir *düğümü localhost* yapılandırmasının bir parçası olarak.</span><span class="sxs-lookup"><span data-stu-id="11d07-113">It is important to include *node localhost* as part of the configuration.</span></span> <span data-ttu-id="11d07-114">Bu bildirimi yoksa, uzantı işleyici düğümü localhost deyim için özel olarak göründüğü gibi aşağıdaki adımları çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="11d07-114">If this statement is missing, the following steps do not work as the extension handler specifically looks for the node localhost statement.</span></span> <span data-ttu-id="11d07-115">Typecast eklemek önemlidir *[PsCredential]*gibi belirli bu tür kimlik bilgilerini şifrelemek için uzantı tetikler.</span><span class="sxs-lookup"><span data-stu-id="11d07-115">It is also important to include the typecast *[PsCredential]*, as this specific type triggers the extension to encrypt the credential.</span></span> 

<span data-ttu-id="11d07-116">Bu komut dosyası blob depolama alanına yayımlayın:</span><span class="sxs-lookup"><span data-stu-id="11d07-116">Publish this script to blob storage:</span></span>

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

<span data-ttu-id="11d07-117">Azure DSC uzantısı ayarlayabilir ve kimlik bilgilerini girin:</span><span class="sxs-lookup"><span data-stu-id="11d07-117">Set the Azure DSC extension and provide the credential:</span></span>

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a><span data-ttu-id="11d07-118">Kimlik bilgileri güvenliği nasıl</span><span class="sxs-lookup"><span data-stu-id="11d07-118">How credentials are secured</span></span>
<span data-ttu-id="11d07-119">Bu kodu çalıştırmak için kimlik bilgilerini ister.</span><span class="sxs-lookup"><span data-stu-id="11d07-119">Running this code prompts for a credential.</span></span> <span data-ttu-id="11d07-120">Sağlanan sonra onu kısaca bellekte depolanır.</span><span class="sxs-lookup"><span data-stu-id="11d07-120">Once it is provided, it is stored in memory briefly.</span></span> <span data-ttu-id="11d07-121">Ne zaman onu yayımlanır ile `Set-AzureVmDscExtension` cmdlet, bu VM için HTTPS üzerinden iletilen, Azure burada depolar yerel VM sertifika kullanarak diskte şifrelenmiş.</span><span class="sxs-lookup"><span data-stu-id="11d07-121">When it is published with `Set-AzureVmDscExtension` cmdlet, it is transmitted over HTTPS to the VM, where Azure stores it encrypted on disk, using the local VM certificate.</span></span> <span data-ttu-id="11d07-122">Ardından bu kısaca bellekte şifresi çözülür ve DSC için geçirmek için yeniden şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="11d07-122">Then it is briefly decrypted in memory and re-encrypted to pass it to DSC.</span></span>

<span data-ttu-id="11d07-123">Bu davranış farklıdır [uzantısı işleyici olmadan güvenli yapılandırmaları kullanarak](https://msdn.microsoft.com/powershell/dsc/securemof).</span><span class="sxs-lookup"><span data-stu-id="11d07-123">This behavior is different than [using secure configurations without the extension handler](https://msdn.microsoft.com/powershell/dsc/securemof).</span></span> <span data-ttu-id="11d07-124">Azure ortamı yapılandırma verilerinin sertifikalar yoluyla güvenli bir şekilde iletmek için bir yöntem sunar.</span><span class="sxs-lookup"><span data-stu-id="11d07-124">The Azure environment gives a way to transmit configuration data securely via certificates.</span></span> <span data-ttu-id="11d07-125">DSC uzantı işleyici kullanırken, $CertificatePath veya bir $CertificateID sağlamak için gerek yoktur / ConfigurationData $Thumbprint girişi.</span><span class="sxs-lookup"><span data-stu-id="11d07-125">When using the DSC extension handler, there is no need to provide $CertificatePath or a $CertificateID / $Thumbprint entry in ConfigurationData.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11d07-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="11d07-126">Next steps</span></span>
<span data-ttu-id="11d07-127">Azure DSC uzantısı işleyici hakkında daha fazla bilgi için bkz: [Azure istenen durum yapılandırması uzantısı işleyici giriş](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="11d07-127">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="11d07-128">İncelemek [DSC uzantısı için Azure Resource Manager şablonu](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="11d07-128">Examine the [Azure Resource Manager template for the DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="11d07-129">PowerShell DSC hakkında daha fazla bilgi için [PowerShell Belge Merkezi ziyaret](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="11d07-129">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="11d07-130">PowerShell DSC ile yönetebileceğiniz ek işlevsellik bulmak için [PowerShell Galerisi Gözat](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) daha fazla DSC kaynakları için.</span><span class="sxs-lookup"><span data-stu-id="11d07-130">To find additional functionality you can manage with PowerShell DSC, [browse the PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

