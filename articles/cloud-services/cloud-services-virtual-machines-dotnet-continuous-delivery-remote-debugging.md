---
title: "Uzaktan hata ayıklama ile sürekli teslim aaaEnable | Microsoft Docs"
description: "Bilgi nasıl tooenable uzaktan kesintisiz teslim toodeploy tooAzure kullanılırken hata ayıklama"
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
ms.openlocfilehash: d9d9d1cfe5304c9526586a9164f172746a448e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-debugging-when-using-continuous-delivery-toopublish-tooazure"></a><span data-ttu-id="8a359-103">Kesintisiz teslim toopublish tooAzure kullanırken uzaktan hata ayıklamayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="8a359-103">Enable remote debugging when using continuous delivery toopublish tooAzure</span></span>
<span data-ttu-id="8a359-104">Kullandığınızda uzaktan Azure'da, bulut Hizmetleri ya da sanal makineleri için hata ayıklamayı etkinleştirebilirsiniz [kesintisiz teslim](cloud-services-dotnet-continuous-delivery.md) aşağıdaki adımları izleyerek toopublish tooAzure.</span><span class="sxs-lookup"><span data-stu-id="8a359-104">You can enable remote debugging in Azure, for cloud services or virtual machines, when you use [continuous delivery](cloud-services-dotnet-continuous-delivery.md) toopublish tooAzure by following these steps.</span></span>

## <a name="enabling-remote-debugging-for-cloud-services"></a><span data-ttu-id="8a359-105">Bulut Hizmetleri için uzaktan hata ayıklama etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="8a359-105">Enabling remote debugging for cloud services</span></span>
1. <span data-ttu-id="8a359-106">Merhaba ilk ortamı için Azure kısmında özetlendiği gibi Hello yapı aracısında ayarlamak [komut satırı derleme Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span><span class="sxs-lookup"><span data-stu-id="8a359-106">On hello build agent, set up hello initial environment for Azure as outlined in [Command-Line Build for Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span></span>
2. <span data-ttu-id="8a359-107">Merhaba Hello uzaktan hata ayıklama çalışma zamanı (msvsmon.exe) hello paketi için gerekli olmadığından yükleme **uzak araçlar Visual Studio için**.</span><span class="sxs-lookup"><span data-stu-id="8a359-107">Because hello remote debug runtime (msvsmon.exe) is required for hello package, install hello **Remote Tools for Visual Studio**.</span></span>

    * [<span data-ttu-id="8a359-108">Visual Studio 2017 için Uzak araçları</span><span class="sxs-lookup"><span data-stu-id="8a359-108">Remote Tools for Visual Studio 2017</span></span>](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [<span data-ttu-id="8a359-109">Visual Studio 2015 için Uzak araçları</span><span class="sxs-lookup"><span data-stu-id="8a359-109">Remote Tools for Visual Studio 2015</span></span>](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [<span data-ttu-id="8a359-110">Visual Studio 2013 güncelleştirme 5 için Uzak araçları</span><span class="sxs-lookup"><span data-stu-id="8a359-110">Remote Tools for Visual Studio 2013 Update 5</span></span>](https://www.microsoft.com/download/details.aspx?id=48156)
    
    <span data-ttu-id="8a359-111">Alternatif olarak, Visual Studio yüklü olan bir sistemden hello uzaktan hata ayıklama ikili dosyalarının kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a359-111">As an alternative, you can copy hello remote debug binaries from a system that has Visual Studio installed.</span></span>

3. <span data-ttu-id="8a359-112">Kısmında özetlendiği gibi bir sertifika oluşturmak [Azure Cloud Services sertifikalarına genel bakış](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="8a359-112">Create a certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="8a359-113">Merhaba .pfx ve RDP sertifikası parmak izi tutmak ve hello sertifika toohello hedef bulut hizmeti yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8a359-113">Keep hello .pfx and RDP certificate thumbprint and upload hello certificate toohello target cloud service.</span></span>
4. <span data-ttu-id="8a359-114">Etkin uzaktan hata ayıklama ile Merhaba MSBuild komut satırında toobuild ve paket seçenekleri aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="8a359-114">Use hello following options in hello MSBuild command line toobuild and package with remote debug enabled.</span></span> <span data-ttu-id="8a359-115">(Merhaba açı ayraçlı öğeleri için gerçek yolları tooyour sistem ve proje dosyalarını değiştirin.)</span><span class="sxs-lookup"><span data-stu-id="8a359-115">(Substitute actual paths tooyour system and project files for hello angle-bracketed items.)</span></span>
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of hello certificate added toohello cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path tooyour VS solution file>"
   
    <span data-ttu-id="8a359-116">`VSX64RemoteDebuggerPath`Merhaba yol toohello klasörünü msvsmon.exe hello uzak araçlar Visual Studio için içeren.</span><span class="sxs-lookup"><span data-stu-id="8a359-116">`VSX64RemoteDebuggerPath` is hello path toohello folder containing msvsmon.exe in hello Remote Tools for Visual Studio.</span></span>
    <span data-ttu-id="8a359-117">`RemoteDebuggerConnectorVersion`Bulut hizmetinizde Hello Azure SDK sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="8a359-117">`RemoteDebuggerConnectorVersion` is hello Azure SDK version in your cloud service.</span></span> <span data-ttu-id="8a359-118">Ayrıca Visual Studio ile yüklenen hello sürümüyle eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a359-118">It should also match hello version installed with Visual Studio.</span></span>
5. <span data-ttu-id="8a359-119">Toohello hedef bulut hizmeti hello önceki adımda oluşturulan hello paket ve .cscfg dosyasını kullanarak yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="8a359-119">Publish toohello target cloud service by using hello package and .cscfg file generated in hello previous step.</span></span>
6. <span data-ttu-id="8a359-120">Yüklü .NET için Azure SDK ile Visual Studio olan hello sertifika (.pfx dosyası) toohello makineyi içeri aktarırsınız.</span><span class="sxs-lookup"><span data-stu-id="8a359-120">Import hello certificate (.pfx file) toohello machine that has Visual Studio with Azure SDK for .NET installed.</span></span> <span data-ttu-id="8a359-121">Tooimport toohello emin olun `CurrentUser\My` Visual Studio'da bağlanmasını toohello hata ayıklayıcı Aksi takdirde başarısız olur sertifika deposu.</span><span class="sxs-lookup"><span data-stu-id="8a359-121">Make sure tooimport toohello `CurrentUser\My` certificate store, otherwise attaching toohello debugger in Visual Studio will fail.</span></span>

## <a name="enabling-remote-debugging-for-virtual-machines"></a><span data-ttu-id="8a359-122">Sanal makineler için uzaktan hata ayıklama etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="8a359-122">Enabling remote debugging for virtual machines</span></span>
1. <span data-ttu-id="8a359-123">Bir Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8a359-123">Create an Azure virtual machine.</span></span> <span data-ttu-id="8a359-124">Bkz: [Windows Server çalıştıran bir sanal makine oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) veya [Visual Studio'da Azure sanal makineler oluşturun ve yönetin](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8a359-124">See [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Create and Manage Azure Virtual Machines in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
2. <span data-ttu-id="8a359-125">Merhaba üzerinde [Azure Klasik portal sayfası](http://go.microsoft.com/fwlink/p/?LinkID=269851), hello sanal makinenin Pano toosee hello sanal makinenin görüntülemek **RDP sertifikası parmak İZİ**.</span><span class="sxs-lookup"><span data-stu-id="8a359-125">On hello [Azure classic portal page](http://go.microsoft.com/fwlink/p/?LinkID=269851), view hello virtual machine's dashboard toosee hello virtual machine’s **RDP CERTIFICATE THUMBPRINT**.</span></span> <span data-ttu-id="8a359-126">Bu değer için hello kullanılır `ServerThumbprint` hello uzantısı yapılandırma değeri.</span><span class="sxs-lookup"><span data-stu-id="8a359-126">This value is used for hello `ServerThumbprint` value in hello extension configuration.</span></span>
3. <span data-ttu-id="8a359-127">Belirtilen bir istemci sertifikası oluşturma [Azure Cloud Services sertifikalarına genel bakış](cloud-services-certs-create.md) (Merhaba .pfx ve RDP sertifikası parmak izi tutun).</span><span class="sxs-lookup"><span data-stu-id="8a359-127">Create a client certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md) (keep hello .pfx and RDP certificate thumbprint).</span></span>
4. <span data-ttu-id="8a359-128">Azure PowerShell'i yükleyin (sürüm 0.7.4 veya sonrası) kısmında özetlendiği gibi [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8a359-128">Install Azure Powershell (version 0.7.4 or later) as outlined in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
5. <span data-ttu-id="8a359-129">Betik tooenable hello RemoteDebug uzantısı aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8a359-129">Run hello following script tooenable hello RemoteDebug extension.</span></span> <span data-ttu-id="8a359-130">Merhaba yolları ve kişisel veriler kendi abonelik adı, hizmet adı ve parmak izi gibi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8a359-130">Replace hello paths and personal data with your own, such as your subscription name, service name, and thumbprint.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8a359-131">Bu komut dosyasını Visual Studio 2015 için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="8a359-131">This script is configured for Visual Studio 2015.</span></span> <span data-ttu-id="8a359-132">Visual Studio 2013 veya Visual Studio 2017 kullanıyorsanız hello değiştirin `$referenceName` ve `$extensionName` atamaları aşağıdaki çok`RemoteDebugVS2013` veya `RemoteDebugVS2017`.</span><span class="sxs-lookup"><span data-stu-id="8a359-132">If you’re using Visual Studio 2013 or Visual Studio 2017, modify hello `$referenceName` and `$extensionName` assignments below too`RemoteDebugVS2013` or `RemoteDebugVS2017`.</span></span>

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

6. <span data-ttu-id="8a359-133">Yüklü .NET için Azure SDK ile Visual Studio olan hello sertifika (.pfx) toohello makineyi içeri aktarırsınız.</span><span class="sxs-lookup"><span data-stu-id="8a359-133">Import hello certificate (.pfx) toohello machine that has Visual Studio with Azure SDK for .NET installed.</span></span>

