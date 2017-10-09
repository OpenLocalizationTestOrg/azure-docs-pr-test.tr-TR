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
# <a name="enable-remote-debugging-when-using-continuous-delivery-toopublish-tooazure"></a>Kesintisiz teslim toopublish tooAzure kullanırken uzaktan hata ayıklamayı etkinleştirme
Kullandığınızda uzaktan Azure'da, bulut Hizmetleri ya da sanal makineleri için hata ayıklamayı etkinleştirebilirsiniz [kesintisiz teslim](cloud-services-dotnet-continuous-delivery.md) aşağıdaki adımları izleyerek toopublish tooAzure.

## <a name="enabling-remote-debugging-for-cloud-services"></a>Bulut Hizmetleri için uzaktan hata ayıklama etkinleştirme
1. Merhaba ilk ortamı için Azure kısmında özetlendiği gibi Hello yapı aracısında ayarlamak [komut satırı derleme Azure](http://msdn.microsoft.com/library/hh535755.aspx).
2. Merhaba Hello uzaktan hata ayıklama çalışma zamanı (msvsmon.exe) hello paketi için gerekli olmadığından yükleme **uzak araçlar Visual Studio için**.

    * [Visual Studio 2017 için Uzak araçları](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [Visual Studio 2015 için Uzak araçları](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [Visual Studio 2013 güncelleştirme 5 için Uzak araçları](https://www.microsoft.com/download/details.aspx?id=48156)
    
    Alternatif olarak, Visual Studio yüklü olan bir sistemden hello uzaktan hata ayıklama ikili dosyalarının kopyalayabilirsiniz.

3. Kısmında özetlendiği gibi bir sertifika oluşturmak [Azure Cloud Services sertifikalarına genel bakış](cloud-services-certs-create.md). Merhaba .pfx ve RDP sertifikası parmak izi tutmak ve hello sertifika toohello hedef bulut hizmeti yükleyin.
4. Etkin uzaktan hata ayıklama ile Merhaba MSBuild komut satırında toobuild ve paket seçenekleri aşağıdaki hello kullanın. (Merhaba açı ayraçlı öğeleri için gerçek yolları tooyour sistem ve proje dosyalarını değiştirin.)
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of hello certificate added toohello cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path tooyour VS solution file>"
   
    `VSX64RemoteDebuggerPath`Merhaba yol toohello klasörünü msvsmon.exe hello uzak araçlar Visual Studio için içeren.
    `RemoteDebuggerConnectorVersion`Bulut hizmetinizde Hello Azure SDK sürümüdür. Ayrıca Visual Studio ile yüklenen hello sürümüyle eşleşmesi gerekir.
5. Toohello hedef bulut hizmeti hello önceki adımda oluşturulan hello paket ve .cscfg dosyasını kullanarak yayımlayın.
6. Yüklü .NET için Azure SDK ile Visual Studio olan hello sertifika (.pfx dosyası) toohello makineyi içeri aktarırsınız. Tooimport toohello emin olun `CurrentUser\My` Visual Studio'da bağlanmasını toohello hata ayıklayıcı Aksi takdirde başarısız olur sertifika deposu.

## <a name="enabling-remote-debugging-for-virtual-machines"></a>Sanal makineler için uzaktan hata ayıklama etkinleştirme
1. Bir Azure sanal makine oluşturun. Bkz: [Windows Server çalıştıran bir sanal makine oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) veya [Visual Studio'da Azure sanal makineler oluşturun ve yönetin](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
2. Merhaba üzerinde [Azure Klasik portal sayfası](http://go.microsoft.com/fwlink/p/?LinkID=269851), hello sanal makinenin Pano toosee hello sanal makinenin görüntülemek **RDP sertifikası parmak İZİ**. Bu değer için hello kullanılır `ServerThumbprint` hello uzantısı yapılandırma değeri.
3. Belirtilen bir istemci sertifikası oluşturma [Azure Cloud Services sertifikalarına genel bakış](cloud-services-certs-create.md) (Merhaba .pfx ve RDP sertifikası parmak izi tutun).
4. Azure PowerShell'i yükleyin (sürüm 0.7.4 veya sonrası) kısmında özetlendiği gibi [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).
5. Betik tooenable hello RemoteDebug uzantısı aşağıdaki hello çalıştırın. Merhaba yolları ve kişisel veriler kendi abonelik adı, hizmet adı ve parmak izi gibi değiştirin.
   
   > [!NOTE]
   > Bu komut dosyasını Visual Studio 2015 için yapılandırılır. Visual Studio 2013 veya Visual Studio 2017 kullanıyorsanız hello değiştirin `$referenceName` ve `$extensionName` atamaları aşağıdaki çok`RemoteDebugVS2013` veya `RemoteDebugVS2017`.

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

6. Yüklü .NET için Azure SDK ile Visual Studio olan hello sertifika (.pfx) toohello makineyi içeri aktarırsınız.

