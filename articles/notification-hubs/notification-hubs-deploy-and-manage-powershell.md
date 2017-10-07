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
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a><span data-ttu-id="03e52-103">PowerShell kullanarak Notification Hubs’ı Dağıtma ve Yönetme</span><span class="sxs-lookup"><span data-stu-id="03e52-103">Deploy and Manage Notification Hubs using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="03e52-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="03e52-104">Overview</span></span>
<span data-ttu-id="03e52-105">Bu makalede nasıl toouse oluşturmak ve yönetmek Azure bildirim PowerShell kullanarak hub gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="03e52-105">This article shows you how toouse Create and Manage Azure Notification Hubs using PowerShell.</span></span> <span data-ttu-id="03e52-106">ortak bir otomatikleştirme görevleri aşağıdaki hello Bu konu başlığı altında gösterilir.</span><span class="sxs-lookup"><span data-stu-id="03e52-106">hello following common automation tasks are shown in this topic.</span></span>

* <span data-ttu-id="03e52-107">Bildirim hub'ı Oluştur</span><span class="sxs-lookup"><span data-stu-id="03e52-107">Create a Notification Hub</span></span>
* <span data-ttu-id="03e52-108">Kimlik bilgilerini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="03e52-108">Set Credentials</span></span>

<span data-ttu-id="03e52-109">Bildirim hub'larınız için de toocreate yeni bir hizmet veri yolu ad alanı gerekirse bkz [PowerShell ile yönetme Service Bus](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span><span class="sxs-lookup"><span data-stu-id="03e52-109">If you also need toocreate a new service bus namespace for your notification hubs, see [Manage Service Bus with PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span></span>

<span data-ttu-id="03e52-110">Bildirim hub'ları yönetme, doğrudan Azure PowerShell ile dahil hello cmdlet'leri tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="03e52-110">Managing Notifications Hubs is not supported directly by hello cmdlets included with Azure PowerShell.</span></span> <span data-ttu-id="03e52-111">PowerShell Hello en iyi yaklaşımı tooreference hello Microsoft.Azure.NotificationHubs.dll derlemesidir.</span><span class="sxs-lookup"><span data-stu-id="03e52-111">hello best approach from PowerShell is tooreference hello Microsoft.Azure.NotificationHubs.dll assembly.</span></span> <span data-ttu-id="03e52-112">Merhaba derleme hello ile dağıtılmış [Microsoft Azure bildirim hub'ları NuGet paketini](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="03e52-112">hello assembly is distributed with hello [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03e52-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="03e52-113">Prerequisites</span></span>
<span data-ttu-id="03e52-114">Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="03e52-114">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="03e52-115">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="03e52-115">An Azure subscription.</span></span> <span data-ttu-id="03e52-116">Azure abonelik tabanlı bir platformdur.</span><span class="sxs-lookup"><span data-stu-id="03e52-116">Azure is a subscription-based platform.</span></span> <span data-ttu-id="03e52-117">Bir aboneliği edinme hakkında daha fazla bilgi için bkz: [satın alma seçenekleri], [üye teklifleri], veya [ücretsiz deneme].</span><span class="sxs-lookup"><span data-stu-id="03e52-117">For more information about obtaining a subscription, see [Purchase Options], [Member Offers], or [Free Trial].</span></span>
* <span data-ttu-id="03e52-118">Azure PowerShell ile bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="03e52-118">A computer with Azure PowerShell.</span></span> <span data-ttu-id="03e52-119">Yönergeler için bkz: [yükleyin ve Azure PowerShell yapılandırma].</span><span class="sxs-lookup"><span data-stu-id="03e52-119">For instructions, see [Install and configure Azure PowerShell].</span></span>
* <span data-ttu-id="03e52-120">PowerShell komut dosyaları, NuGet paketlerini ve hello .NET Framework genel anlama.</span><span class="sxs-lookup"><span data-stu-id="03e52-120">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="including-a-reference-toohello-net-assembly-for-service-bus"></a><span data-ttu-id="03e52-121">Hizmet veri yolu için bir başvuru toohello .NET derleme dahil</span><span class="sxs-lookup"><span data-stu-id="03e52-121">Including a reference toohello .NET assembly for Service Bus</span></span>
<span data-ttu-id="03e52-122">Azure bildirim hub'ları yönetme henüz hello Azure PowerShell'de PowerShell cmdlet'leri ile dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="03e52-122">Managing Azure Notification Hubs is not yet included with hello PowerShell cmdlets in Azure PowerShell.</span></span> <span data-ttu-id="03e52-123">tooprovision bildirim hub'ları, kullanabileceğiniz hello sağlanan hello .NET istemci [Microsoft Azure bildirim hub'ları NuGet paketini](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="03e52-123">tooprovision notification hubs, you can use hello .NET client provided in hello [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="03e52-124">Öncelikle, kodunuzu hello bulabilir emin olun **Microsoft.Azure.NotificationHubs.dll** Visual Studio projesi bir NuGet paketi olarak yüklü derleme.</span><span class="sxs-lookup"><span data-stu-id="03e52-124">First, make sure your script can locate hello **Microsoft.Azure.NotificationHubs.dll** assembly, which is installed as a NuGet package in a Visual Studio project.</span></span> <span data-ttu-id="03e52-125">Esnek sipariş toobe içinde hello komut dosyası, aşağıdaki adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="03e52-125">In order toobe flexible, hello script performs these steps:</span></span>

1. <span data-ttu-id="03e52-126">Hangi çağrıldı hello yolu belirler.</span><span class="sxs-lookup"><span data-stu-id="03e52-126">Determines hello path at which it was invoked.</span></span>
2. <span data-ttu-id="03e52-127">Adlı bir klasör bulana kadar ilişkilerinden geçen hello yolu `packages`.</span><span class="sxs-lookup"><span data-stu-id="03e52-127">Traverses hello path until it finds a folder named `packages`.</span></span> <span data-ttu-id="03e52-128">Visual Studio projeleri için NuGet paketlerini yüklediğinizde bu klasör oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="03e52-128">This folder is created when you install NuGet packages for Visual Studio projects.</span></span>
3. <span data-ttu-id="03e52-129">Özyinelemeli olarak arar hello `packages` adlı bir derleme için klasör **Microsoft.Azure.NotificationHubs.dll**.</span><span class="sxs-lookup"><span data-stu-id="03e52-129">Recursively searches hello `packages` folder for an assembly named **Microsoft.Azure.NotificationHubs.dll**.</span></span>
4. <span data-ttu-id="03e52-130">Merhaba türleri daha sonra kullanmak için kullanılabilir olacak şekilde, derleme başvuruları hello.</span><span class="sxs-lookup"><span data-stu-id="03e52-130">References hello assembly so that hello types are available for later use.</span></span>

<span data-ttu-id="03e52-131">İşte bu adımları bir PowerShell Betiği nasıl uygulanır:</span><span class="sxs-lookup"><span data-stu-id="03e52-131">Here's how these steps are implemented in a PowerShell script:</span></span>

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

## <a name="create-hello-namespacemanager-class"></a><span data-ttu-id="03e52-132">Merhaba NamespaceManager sınıfı oluşturma</span><span class="sxs-lookup"><span data-stu-id="03e52-132">Create hello NamespaceManager class</span></span>
<span data-ttu-id="03e52-133">tooprovision bildirim hub'ları oluşturma hello örneği [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) hello SDK sınıfından.</span><span class="sxs-lookup"><span data-stu-id="03e52-133">tooprovision Notification Hubs, create an instance of hello [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) class from hello SDK.</span></span> 

<span data-ttu-id="03e52-134">Merhaba kullanabilirsiniz [Get-AzureSBAuthorizationRule] cmdlet ile Azure PowerShell tooretrieve tooprovide bir bağlantı dizesi kullanılmış bir yetkilendirme kuralı dahil.</span><span class="sxs-lookup"><span data-stu-id="03e52-134">You can use hello [Get-AzureSBAuthorizationRule] cmdlet included with Azure PowerShell tooretrieve an authorization rule that's used tooprovide a connection string.</span></span> <span data-ttu-id="03e52-135">Bir başvuru toohello depolarız `NamespaceManager` hello örneğinde `$NamespaceManager` değişkeni.</span><span class="sxs-lookup"><span data-stu-id="03e52-135">We'll store a reference toohello `NamespaceManager` instance in hello `$NamespaceManager` variable.</span></span> <span data-ttu-id="03e52-136">Kullanacağız `$NamespaceManager` tooprovision bir bildirim hub'ı.</span><span class="sxs-lookup"><span data-stu-id="03e52-136">We will use `$NamespaceManager` tooprovision a notification hub.</span></span>

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create hello NamespaceManager object toocreate hello hub
Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a><span data-ttu-id="03e52-137">Yeni bir Notification Hub sağlama</span><span class="sxs-lookup"><span data-stu-id="03e52-137">Provisioning a new Notification Hub</span></span>
<span data-ttu-id="03e52-138">tooprovision yeni bir notification hub kullanın hello [bildirim hub'ları için .NET API].</span><span class="sxs-lookup"><span data-stu-id="03e52-138">tooprovision a new notification hub, use hello [.NET API for Notification Hubs].</span></span>

<span data-ttu-id="03e52-139">Merhaba betik bu bölümünde dört yerel değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="03e52-139">In this part of hello script you set up four local variables.</span></span> 

1. <span data-ttu-id="03e52-140">`$Namespace`: Bu toohello hello ad alanı toocreate istediğiniz bir bildirim hub'ı kümesinin adı.</span><span class="sxs-lookup"><span data-stu-id="03e52-140">`$Namespace` : Set this toohello name of hello namespace where you want toocreate a notification hub.</span></span>
2. <span data-ttu-id="03e52-141">`$Path`: Bu hello yeni bildirim hub'ı yol toohello adını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="03e52-141">`$Path` : Set this path toohello name of hello new notification hub.</span></span>  <span data-ttu-id="03e52-142">Örneğin, "MyHub".</span><span class="sxs-lookup"><span data-stu-id="03e52-142">For example, "MyHub".</span></span>    
3. <span data-ttu-id="03e52-143">`$WnsPackageSid`: Bu toohello paket SID'si için Windows uygulaması hello ayarladığınız [Windows Geliştirme Merkezi](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="03e52-143">`$WnsPackageSid` : Set this toohello package SID for you Windows App from hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>
4. <span data-ttu-id="03e52-144">`$WnsSecretkey`: Bu toohello gizli anahtarı için Windows uygulaması hello ayarladığınız [Windows Geliştirme Merkezi](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="03e52-144">`$WnsSecretkey`: Set this toohello secret key for you Windows App from hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>

<span data-ttu-id="03e52-145">Bu değişkenler kullanılan tooconnect tooyour ad ve yeni bir bildirim hub'ı yapılandırılmış toohandle Windows Bildirim Hizmetleri (WNS) bildirimleri WNS kimlik bilgileriyle için bir Windows uygulaması oluşturma.</span><span class="sxs-lookup"><span data-stu-id="03e52-145">These variables are used tooconnect tooyour namespace and create a new Notification Hub configured toohandle Windows Notification Services (WNS) notifications with WNS credentials for a Windows App.</span></span> <span data-ttu-id="03e52-146">Merhaba alma hakkında bilgi için SID ve gizli anahtar bakın, hello paketini [Notification Hubs ile çalışmaya başlama](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="03e52-146">For information on obtaining hello package SID and secret key see, hello [Getting Started with Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span> 

* <span data-ttu-id="03e52-147">Merhaba kod parçacığını kullanan hello `NamespaceManager` hello bildirim hub'ı tarafından tanımladıysanız toocheck toosee nesne `$Path` bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="03e52-147">hello script snippet uses hello `NamespaceManager` object toocheck toosee if hello Notification Hub identified by `$Path` exists.</span></span>
* <span data-ttu-id="03e52-148">Yoksa, hello betik oluşturacak bir `NotificationHubDescription` WNS ile kimlik bilgileri ve bu toohello geçirin `NamespaceManager` sınıfı `CreateNotificationHub` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="03e52-148">If it does not exist, hello script will create an `NotificationHubDescription` with WNS credentials and pass that toohello `NamespaceManager` class `CreateNotificationHub` method.</span></span>

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




## <a name="additional-resources"></a><span data-ttu-id="03e52-149">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="03e52-149">Additional Resources</span></span>
* [<span data-ttu-id="03e52-150">Service Bus PowerShell ile yönetme</span><span class="sxs-lookup"><span data-stu-id="03e52-150">Manage Service Bus with PowerShell</span></span>](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="03e52-151">Nasıl toocreate Service Bus kuyrukları, konuları ve abonelikleri bir PowerShell Betiği kullanılarak</span><span class="sxs-lookup"><span data-stu-id="03e52-151">How toocreate Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="03e52-152">Nasıl toocreate Service Bus Namespace ve bir Event Hub'ın bir PowerShell komut dosyası kullanma</span><span class="sxs-lookup"><span data-stu-id="03e52-152">How toocreate a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

<span data-ttu-id="03e52-153">Bazı hazır kodlar da indirme için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="03e52-153">Some ready-made scripts are also available for download:</span></span>

* [<span data-ttu-id="03e52-154">Hizmet veri yolu PowerShell betikleri</span><span class="sxs-lookup"><span data-stu-id="03e52-154">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[satın alma seçenekleri]: http://azure.microsoft.com/pricing/purchase-options/
[üye teklifleri]: http://azure.microsoft.com/pricing/member-offers/
[ücretsiz deneme]: http://azure.microsoft.com/pricing/free-trial/
[yükleyin ve Azure PowerShell yapılandırma]: /powershell/azureps-cmdlets-docs
[bildirim hub'ları için .NET API]: https://msdn.microsoft.com/library/azure/mt414893.aspx
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
[Get-AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx

