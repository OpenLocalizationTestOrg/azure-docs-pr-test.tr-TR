---
title: "Sürekli teslimat ile uzaktan hata ayıklamayı etkinleştirme | Microsoft Docs"
description: "Azure'a dağıtmak için kesintisiz teslim kullanırken, uzaktan hata ayıklamayı etkinleştirme öğrenin"
services: cloud-services
documentationcenter: .net
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d423639-3b2f-4ca5-ac5a-9ac19a217c29
ms.service: cloud-services
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 7a8a853a93e3e9915f687a20c871444e6a0de50d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="enable-remote-debugging-when-using-continuous-delivery-to-publish-to-azure"></a><span data-ttu-id="22b1f-103">Azure'da yayımlamak için sürekli teslim kullanılırken uzaktan hata ayıklamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="22b1f-103">Enable remote debugging when using continuous delivery to publish to Azure</span></span>
<span data-ttu-id="22b1f-104">Kullandığınızda uzaktan Azure'da, bulut Hizmetleri ya da sanal makineleri için hata ayıklamayı etkinleştirebilirsiniz [kesintisiz teslim](cloud-services-dotnet-continuous-delivery.md) Azure için aşağıdaki adımları izleyerek yayımlamak için.</span><span class="sxs-lookup"><span data-stu-id="22b1f-104">You can enable remote debugging in Azure, for cloud services or virtual machines, when you use [continuous delivery](cloud-services-dotnet-continuous-delivery.md) to publish to Azure by following these steps.</span></span>

## <a name="enabling-remote-debugging-for-cloud-services"></a><span data-ttu-id="22b1f-105">Bulut Hizmetleri için uzaktan hata ayıklama etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="22b1f-105">Enabling remote debugging for cloud services</span></span>
1. <span data-ttu-id="22b1f-106">Yapı aracısında kısmında özetlendiği gibi ilk ortamını Azure için ayarlayamıyor [komut satırı derleme Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span><span class="sxs-lookup"><span data-stu-id="22b1f-106">On the build agent, set up the initial environment for Azure as outlined in [Command-Line Build for Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span></span>
2. <span data-ttu-id="22b1f-107">Uzaktan hata ayıklama çalışma zamanı (msvsmon.exe) paket için gerekli olmadığından yükleme **uzak araçlar Visual Studio için**.</span><span class="sxs-lookup"><span data-stu-id="22b1f-107">Because the remote debug runtime (msvsmon.exe) is required for the package, install the **Remote Tools for Visual Studio**.</span></span>

    * [<span data-ttu-id="22b1f-108">Visual Studio 2017 için Uzak araçları</span><span class="sxs-lookup"><span data-stu-id="22b1f-108">Remote Tools for Visual Studio 2017</span></span>](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [<span data-ttu-id="22b1f-109">Visual Studio 2015 için Uzak araçları</span><span class="sxs-lookup"><span data-stu-id="22b1f-109">Remote Tools for Visual Studio 2015</span></span>](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [<span data-ttu-id="22b1f-110">Visual Studio 2013 güncelleştirme 5 için Uzak araçları</span><span class="sxs-lookup"><span data-stu-id="22b1f-110">Remote Tools for Visual Studio 2013 Update 5</span></span>](https://www.microsoft.com/download/details.aspx?id=48156)
    
    <span data-ttu-id="22b1f-111">Alternatif olarak, Visual Studio yüklü olan bir sistemden uzaktan hata ayıklama ikili dosyalarının kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22b1f-111">As an alternative, you can copy the remote debug binaries from a system that has Visual Studio installed.</span></span>

3. <span data-ttu-id="22b1f-112">Kısmında özetlendiği gibi bir sertifika oluşturmak [Azure Cloud Services sertifikalarına genel bakış](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="22b1f-112">Create a certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="22b1f-113">RDP sertifikası parmak izi ve .pfx tutmak ve hedef bulut hizmetine sertifika yükleyin.</span><span class="sxs-lookup"><span data-stu-id="22b1f-113">Keep the .pfx and RDP certificate thumbprint and upload the certificate to the target cloud service.</span></span>
4. <span data-ttu-id="22b1f-114">Derleme ve etkin uzaktan hata ayıklama ile paket için MSBuild komut satırında aşağıdaki seçenekleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="22b1f-114">Use the following options in the MSBuild command line to build and package with remote debug enabled.</span></span> <span data-ttu-id="22b1f-115">(Sistem ve proje dosyalarınıza açı ayraçlı öğeleri için gerçek yolları değiştirin.)</span><span class="sxs-lookup"><span data-stu-id="22b1f-115">(Substitute actual paths to your system and project files for the angle-bracketed items.)</span></span>
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of the certificate added to the cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path to your VS solution file>"
   
    <span data-ttu-id="22b1f-116">`VSX64RemoteDebuggerPath`klasörün yolunu msvsmon.exe uzak araçlar Visual Studio için içeren.</span><span class="sxs-lookup"><span data-stu-id="22b1f-116">`VSX64RemoteDebuggerPath` is the path to the folder containing msvsmon.exe in the Remote Tools for Visual Studio.</span></span>
    <span data-ttu-id="22b1f-117">`RemoteDebuggerConnectorVersion`Bulut hizmetinizde Azure SDK sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="22b1f-117">`RemoteDebuggerConnectorVersion` is the Azure SDK version in your cloud service.</span></span> <span data-ttu-id="22b1f-118">Ayrıca Visual Studio ile yüklenen sürümüyle eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="22b1f-118">It should also match the version installed with Visual Studio.</span></span>
5. <span data-ttu-id="22b1f-119">Hedef bulut hizmetine, önceki adımda oluşturulan paket ve .cscfg dosyasını kullanarak yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="22b1f-119">Publish to the target cloud service by using the package and .cscfg file generated in the previous step.</span></span>
6. <span data-ttu-id="22b1f-120">Sertifikayı (.pfx dosyası) yüklü .NET için Azure SDK ile Visual Studio bulunduğu makineyi içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="22b1f-120">Import the certificate (.pfx file) to the machine that has Visual Studio with Azure SDK for .NET installed.</span></span> <span data-ttu-id="22b1f-121">Alınacak emin olun `CurrentUser\My` sertifika deposu, aksi takdirde Visual Studio hata ayıklayıcısı ekleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="22b1f-121">Make sure to import to the `CurrentUser\My` certificate store, otherwise attaching to the debugger in Visual Studio will fail.</span></span>

## <a name="enabling-remote-debugging-for-virtual-machines"></a><span data-ttu-id="22b1f-122">Sanal makineler için uzaktan hata ayıklama etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="22b1f-122">Enabling remote debugging for virtual machines</span></span>
1. <span data-ttu-id="22b1f-123">Bir Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="22b1f-123">Create an Azure virtual machine.</span></span> <span data-ttu-id="22b1f-124">Bkz: [Windows Server çalıştıran bir sanal makine oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) veya [Visual Studio'da Azure sanal makineler oluşturun ve yönetin](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="22b1f-124">See [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Create and Manage Azure Virtual Machines in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
2. <span data-ttu-id="22b1f-125">Üzerinde [Azure Klasik portal sayfası](http://go.microsoft.com/fwlink/p/?LinkID=269851), sanal makinenin görmek için sanal makinenin Panoyu görebilmek **RDP sertifikası parmak İZİ**.</span><span class="sxs-lookup"><span data-stu-id="22b1f-125">On the [Azure classic portal page](http://go.microsoft.com/fwlink/p/?LinkID=269851), view the virtual machine's dashboard to see the virtual machine’s **RDP CERTIFICATE THUMBPRINT**.</span></span> <span data-ttu-id="22b1f-126">Bu değer için kullanılan `ServerThumbprint` uzantısı yapılandırma değeri.</span><span class="sxs-lookup"><span data-stu-id="22b1f-126">This value is used for the `ServerThumbprint` value in the extension configuration.</span></span>
3. <span data-ttu-id="22b1f-127">Belirtilen bir istemci sertifikası oluşturma [Azure Cloud Services sertifikalarına genel bakış](cloud-services-certs-create.md) (.pfx ve RDP sertifikası parmak izi tutun).</span><span class="sxs-lookup"><span data-stu-id="22b1f-127">Create a client certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md) (keep the .pfx and RDP certificate thumbprint).</span></span>
4. <span data-ttu-id="22b1f-128">Azure PowerShell'i yükleyin (sürüm 0.7.4 veya sonrası) kısmında özetlendiği gibi [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="22b1f-128">Install Azure Powershell (version 0.7.4 or later) as outlined in [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
5. <span data-ttu-id="22b1f-129">RemoteDebug uzantısını etkinleştirmek için aşağıdaki betiği çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="22b1f-129">Run the following script to enable the RemoteDebug extension.</span></span> <span data-ttu-id="22b1f-130">Kişisel veri ve yolları kendi abonelik adı, hizmet adı ve parmak izi gibi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="22b1f-130">Replace the paths and personal data with your own, such as your subscription name, service name, and thumbprint.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="22b1f-131">Bu komut dosyasını Visual Studio 2015 için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="22b1f-131">This script is configured for Visual Studio 2015.</span></span> <span data-ttu-id="22b1f-132">Visual Studio 2013 veya Visual Studio 2017 kullanıyorsanız değiştirin `$referenceName` ve `$extensionName` aşağıda atamalar `RemoteDebugVS2013` veya `RemoteDebugVS2017`.</span><span class="sxs-lookup"><span data-stu-id="22b1f-132">If you’re using Visual Studio 2013 or Visual Studio 2017, modify the `$referenceName` and `$extensionName` assignments below to `RemoteDebugVS2013` or `RemoteDebugVS2017`.</span></span>

    ```powershell   
    Add-AzureAccount

    Select-AzureSubscription "My Microsoft Subscription"

    $vm = Get-AzureVM -ServiceName "mytestvm1" -Name "mytestvm1"

    $endpoints = @(
                    ,@{Name="RDConnVS2013"; PublicPort=30400; PrivatePort=30398}
                    ,@{Name="RDFwdrVS2013"; PublicPort=31400; PrivatePort=31398}
                )

    foreach($endpoint in $endpoints)
    {
        Add-AzureEndpoint -VM $vm -Name $endpoint.Name -Protocol tcp -PublicPort $endpoint.PublicPort -LocalPort $endpoint.PrivatePort
    }

    $referenceName = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug.RemoteDebugVS2015"
    $publisher = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug"
    $extensionName = "RemoteDebugVS2015"
    $version = "1.*"
    $publicConfiguration = "<PublicConfig><Connector.Enabled>true</Connector.Enabled><ClientThumbprint>56D7D1B25B472268E332F7FC0C87286458BFB6B2</ClientThumbprint><ServerThumbprint>E7DCB00CB916C468CC3228261D6E4EE45C8ED3C6</ServerThumbprint><ConnectorPort>30398</ConnectorPort><ForwarderPort>31398</ForwarderPort></PublicConfig>"

    $vm | Set-AzureVMExtension -ReferenceName $referenceName -Publisher $publisher -ExtensionName $extensionName -Version $version -PublicConfiguration $publicConfiguration

    foreach($extension in $vm.VM.ResourceExtensionReferences)
    {
        if(($extension.ReferenceName -eq $referenceName) `
        -and ($extension.Publisher -eq $publisher) `
        -and ($extension.Name -eq $extensionName) `
        -and ($extension.Version -eq $version))
        {
            $extension.ResourceExtensionParameterValues[0].Key = 'config.txt'
            break
        }
    }

    $vm | Update-AzureVM
    ```

6. <span data-ttu-id="22b1f-133">Sertifika (.pfx) yüklü .NET için Azure SDK ile Visual Studio bulunduğu makineyi içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="22b1f-133">Import the certificate (.pfx) to the machine that has Visual Studio with Azure SDK for .NET installed.</span></span>

