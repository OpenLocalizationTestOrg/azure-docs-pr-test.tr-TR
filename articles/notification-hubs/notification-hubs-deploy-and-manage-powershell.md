---
title: "aaaDeploy ve Notification Hubs PowerShell kullanarak yönetme"
description: "Nasıl tooCreate yönetmek bildirim hub'ları PowerShell kullanarak ve Otomasyon"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 7c58f2c8-0399-42bc-9e1e-a7f073426451
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8835bdefa0d360354263eab8040259ad08281771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a>PowerShell kullanarak Notification Hubs’ı Dağıtma ve Yönetme
## <a name="overview"></a>Genel Bakış
Bu makalede nasıl toouse oluşturmak ve yönetmek Azure bildirim PowerShell kullanarak hub gösterilmektedir. ortak bir otomatikleştirme görevleri aşağıdaki hello Bu konu başlığı altında gösterilir.

* Bildirim hub'ı Oluştur
* Kimlik bilgilerini ayarlayın

Bildirim hub'larınız için de toocreate yeni bir hizmet veri yolu ad alanı gerekirse bkz [PowerShell ile yönetme Service Bus](../service-bus-messaging/service-bus-powershell-how-to-provision.md).

Bildirim hub'ları yönetme, doğrudan Azure PowerShell ile dahil hello cmdlet'leri tarafından desteklenmiyor. PowerShell Hello en iyi yaklaşımı tooreference hello Microsoft.Azure.NotificationHubs.dll derlemesidir. Merhaba derleme hello ile dağıtılmış [Microsoft Azure bildirim hub'ları NuGet paketini](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

## <a name="prerequisites"></a>Ön koşullar
Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:

* Azure aboneliği. Azure abonelik tabanlı bir platformdur. Bir aboneliği edinme hakkında daha fazla bilgi için bkz: [satın alma seçenekleri], [üye teklifleri], veya [ücretsiz deneme].
* Azure PowerShell ile bir bilgisayar. Yönergeler için bkz: [yükleyin ve Azure PowerShell yapılandırma].
* PowerShell komut dosyaları, NuGet paketlerini ve hello .NET Framework genel anlama.

## <a name="including-a-reference-toohello-net-assembly-for-service-bus"></a>Hizmet veri yolu için bir başvuru toohello .NET derleme dahil
Azure bildirim hub'ları yönetme henüz hello Azure PowerShell'de PowerShell cmdlet'leri ile dahil değildir. tooprovision bildirim hub'ları, kullanabileceğiniz hello sağlanan hello .NET istemci [Microsoft Azure bildirim hub'ları NuGet paketini](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Öncelikle, kodunuzu hello bulabilir emin olun **Microsoft.Azure.NotificationHubs.dll** Visual Studio projesi bir NuGet paketi olarak yüklü derleme. Esnek sipariş toobe içinde hello komut dosyası, aşağıdaki adımları gerçekleştirir:

1. Hangi çağrıldı hello yolu belirler.
2. Adlı bir klasör bulana kadar ilişkilerinden geçen hello yolu `packages`. Visual Studio projeleri için NuGet paketlerini yüklediğinizde bu klasör oluşturulur.
3. Özyinelemeli olarak arar hello `packages` adlı bir derleme için klasör **Microsoft.Azure.NotificationHubs.dll**.
4. Merhaba türleri daha sonra kullanmak için kullanılabilir olacak şekilde, derleme başvuruları hello.

İşte bu adımları bir PowerShell Betiği nasıl uygulanır:

``` powershell

try
{
    # WARNING: Make sure tooreference hello latest version of Microsoft.Azure.NotificationHubs.dll
    Write-Output "Adding hello [Microsoft.Azure.NotificationHubs.dll] assembly toohello script..."
    $scriptPath = Split-Path (Get-Variable MyInvocation -Scope 0).Value.MyCommand.Path
    $packagesFolder = (Split-Path $scriptPath -Parent) + "\packages"
    $assembly = Get-ChildItem $packagesFolder -Include "Microsoft.Azure.NotificationHubs.dll" -Recurse
    Add-Type -Path $assembly.FullName

    Write-Output "hello [Microsoft.Azure.NotificationHubs.dll] assembly has been successfully added toohello script."
}

catch [System.Exception]
{
    Write-Error("Could not add hello Microsoft.Azure.NotificationHubs.dll assembly toohello script. Make sure you build hello solution before running hello provisioning script.")
}
```

## <a name="create-hello-namespacemanager-class"></a>Merhaba NamespaceManager sınıfı oluşturma
tooprovision bildirim hub'ları oluşturma hello örneği [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) hello SDK sınıfından. 

Merhaba kullanabilirsiniz [Get-AzureSBAuthorizationRule] cmdlet ile Azure PowerShell tooretrieve tooprovide bir bağlantı dizesi kullanılmış bir yetkilendirme kuralı dahil. Bir başvuru toohello depolarız `NamespaceManager` hello örneğinde `$NamespaceManager` değişkeni. Kullanacağız `$NamespaceManager` tooprovision bir bildirim hub'ı.

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create hello NamespaceManager object toocreate hello hub
Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a>Yeni bir Notification Hub sağlama
tooprovision yeni bir notification hub kullanın hello [bildirim hub'ları için .NET API].

Merhaba betik bu bölümünde dört yerel değişkenleri ayarlayın. 

1. `$Namespace`: Bu toohello hello ad alanı toocreate istediğiniz bir bildirim hub'ı kümesinin adı.
2. `$Path`: Bu hello yeni bildirim hub'ı yol toohello adını ayarlayın.  Örneğin, "MyHub".    
3. `$WnsPackageSid`: Bu toohello paket SID'si için Windows uygulaması hello ayarladığınız [Windows Geliştirme Merkezi](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).
4. `$WnsSecretkey`: Bu toohello gizli anahtarı için Windows uygulaması hello ayarladığınız [Windows Geliştirme Merkezi](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).

Bu değişkenler kullanılan tooconnect tooyour ad ve yeni bir bildirim hub'ı yapılandırılmış toohandle Windows Bildirim Hizmetleri (WNS) bildirimleri WNS kimlik bilgileriyle için bir Windows uygulaması oluşturma. Merhaba alma hakkında bilgi için SID ve gizli anahtar bakın, hello paketini [Notification Hubs ile çalışmaya başlama](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) Öğreticisi. 

* Merhaba kod parçacığını kullanan hello `NamespaceManager` hello bildirim hub'ı tarafından tanımladıysanız toocheck toosee nesne `$Path` bulunmaktadır.
* Yoksa, hello betik oluşturacak bir `NotificationHubDescription` WNS ile kimlik bilgileri ve bu toohello geçirin `NamespaceManager` sınıfı `CreateNotificationHub` yöntemi.

``` powershell

$Namespace = "<Enter your namespace>"
$Path  = "<Enter a name for your notification hub>"
$WnsPackageSid = "<your package sid>"
$WnsSecretkey = "<enter your secret key>"

$WnsCredential = New-Object -TypeName Microsoft.Azure.NotificationHubs.WnsCredential -ArgumentList $WnsPackageSid,$WnsSecretkey

# Query hello namespace
$CurrentNamespace = Get-AzureSBNamespace -Name $Namespace

# Check if hello namespace already exists
if ($CurrentNamespace)
{
    Write-Output "hello namespace [$Namespace] in hello [$($CurrentNamespace.Region)] region was found."

    # Create hello NamespaceManager object used toocreate a new notification hub
    $sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
    Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
    $NamespaceManager = [Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
    Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."

    # Check toosee if hello Notification Hub already exists
    if ($NamespaceManager.NotificationHubExists($Path))
    {
        Write-Output "hello [$Path] notification hub already exists in hello [$Namespace] namespace."  
    }
    else
    {
        Write-Output "Creating hello [$Path] notification hub in hello [$Namespace] namespace."
        $NHDescription = New-Object -TypeName Microsoft.Azure.NotificationHubs.NotificationHubDescription -ArgumentList $Path;
        $NHDescription.WnsCredential = $WnsCredential;
        $NamespaceManager.CreateNotificationHub($NHDescription);
        Write-Output "hello [$Path] notification hub was created in hello [$Namespace] namespace."
    }
}
else
{
    Write-Host "hello [$Namespace] namespace does not exist."
}
```




## <a name="additional-resources"></a>Ek Kaynaklar
* [Service Bus PowerShell ile yönetme](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [Nasıl toocreate Service Bus kuyrukları, konuları ve abonelikleri bir PowerShell Betiği kullanılarak](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [Nasıl toocreate Service Bus Namespace ve bir Event Hub'ın bir PowerShell komut dosyası kullanma](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

Bazı hazır kodlar da indirme için kullanılabilir:

* [Hizmet veri yolu PowerShell betikleri](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[satın alma seçenekleri]: http://azure.microsoft.com/pricing/purchase-options/
[üye teklifleri]: http://azure.microsoft.com/pricing/member-offers/
[ücretsiz deneme]: http://azure.microsoft.com/pricing/free-trial/
[yükleyin ve Azure PowerShell yapılandırma]: /powershell/azureps-cmdlets-docs
[bildirim hub'ları için .NET API]: https://msdn.microsoft.com/library/azure/mt414893.aspx
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
[Get-AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx

