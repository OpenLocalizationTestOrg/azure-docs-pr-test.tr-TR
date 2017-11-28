---
title: "aaaEnable PowerShell kullanarak Azure Cloud Services rolünde için Uzak Masaüstü Bağlantısı"
description: "Nasıl tooconfigure azure bulut hizmeti uygulaması PowerShell tooallow Uzak Masaüstü bağlantıları kullanma"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: bf2f70a4-20dc-4302-a91a-38cd7a2baa62
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 3f46b014f29f1c0be0e1b485d2f0152424162bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="b574a-103">PowerShell kullanarak Azure Cloud Services rolünde için Uzak Masaüstü Bağlantısı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="b574a-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b574a-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="b574a-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="b574a-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="b574a-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="b574a-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b574a-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="b574a-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b574a-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="b574a-108">Uzak Masaüstü tooaccess hello Masaüstü Azure'da çalışan bir rolün sağlar.</span><span class="sxs-lookup"><span data-stu-id="b574a-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="b574a-109">Çalışırken uygulamanız ile sorunları tanılamak ve Uzak Masaüstü Bağlantısı tootroubleshoot kullanın.</span><span class="sxs-lookup"><span data-stu-id="b574a-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="b574a-110">Bu makalede nasıl tooenable Uzak Masaüstü'nü PowerShell kullanarak, bulut hizmeti rollerinizi.</span><span class="sxs-lookup"><span data-stu-id="b574a-110">This article describes how tooenable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="b574a-111">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) için bu makalede gerekli hello Önkoşullar için.</span><span class="sxs-lookup"><span data-stu-id="b574a-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span> <span data-ttu-id="b574a-112">Merhaba uygulama dağıtıldıktan sonra Uzak Masaüstü'nü etkinleştirmek için PowerShell hello Uzak Masaüstü uzantısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="b574a-112">PowerShell utilizes hello Remote Desktop Extension so you can enable Remote Desktop after hello application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="b574a-113">Uzak Masaüstü PowerShell üzerinden yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="b574a-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="b574a-114">Merhaba [kümesi AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet'i belirtilen roller veya Bulut hizmeti dağıtımınızın tüm roller üzerinde Uzak Masaüstü tooenable sağlar.</span><span class="sxs-lookup"><span data-stu-id="b574a-114">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet allows you tooenable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="b574a-115">Merhaba cmdlet hello Uzak Masaüstü kullanıcı hello aracılığıyla hello kullanıcı adı ve parola belirtmenize olanak sağlar *kimlik bilgisi* bir PSCredential nesnesi kabul parametresi.</span><span class="sxs-lookup"><span data-stu-id="b574a-115">hello cmdlet lets you specify hello Username and Password for hello remote desktop user through hello *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="b574a-116">PowerShell etkileşimli olarak kullanıyorsanız, hello PSCredential nesnesinin arama hello tarafından kolayca ayarlayabilirsiniz [Get-kimlik bilgilerinin](https://technet.microsoft.com/library/hh849815.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="b574a-116">If you are using PowerShell interactively, you can easily set hello PSCredential object by calling hello [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="b574a-117">Bu komut, tooenter hello kullanıcı adı ve parola hello uzak kullanıcı için güvenli bir şekilde sağlayan bir iletişim kutusu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b574a-117">This command displays a dialog box allowing you tooenter hello username and password for hello remote user in a secure manner.</span></span>

<span data-ttu-id="b574a-118">PowerShell Otomasyon senaryolarda yardımcı olduğundan, hello de ayarlayabilirsiniz **PSCredential** , kullanıcı etkileşimi gerektirmeyen şekilde nesnesi.</span><span class="sxs-lookup"><span data-stu-id="b574a-118">Since PowerShell helps in automation scenarios, you can also set up hello **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="b574a-119">İlk olarak, tooset güvenli bir parola gerekir.</span><span class="sxs-lookup"><span data-stu-id="b574a-119">First, you need tooset up a secure password.</span></span> <span data-ttu-id="b574a-120">Düz metinli bir parola tooa güvenli dize dönüştürür belirterek başlamadan kullanarak [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="b574a-120">You begin with specifying a plain text password convert it tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="b574a-121">Sonraki tooconvert güvenli Bu dize bir şifrelenmiş standart dize kullanarak gereksinim duyduğunuz [ConvertFrom SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span><span class="sxs-lookup"><span data-stu-id="b574a-121">Next you need tooconvert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="b574a-122">Bu şifreli standart dize tooa dosyasını kullanarak kaydedebilirsiniz [kümesi içeriği](https://technet.microsoft.com/library/ee176959.aspx).</span><span class="sxs-lookup"><span data-stu-id="b574a-122">Now you can save this encrypted standard string tooa file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="b574a-123">Böylece her zaman hello Parolada tootype yok güvenli parola dosyası da oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b574a-123">You can also create a secure password file so that you don't have tootype in hello password every time.</span></span> <span data-ttu-id="b574a-124">Ayrıca, güvenli parola dosyasına düz metin dosyasından daha iyidir.</span><span class="sxs-lookup"><span data-stu-id="b574a-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="b574a-125">PowerShell toocreate güvenli parola dosyasına aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="b574a-125">Use hello following PowerShell toocreate a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> <span data-ttu-id="b574a-126">Merhaba parolayı ayarlarken hello karşıladığından emin olun [karmaşıklık gereksinimlerini](https://technet.microsoft.com/library/cc786468.aspx).</span><span class="sxs-lookup"><span data-stu-id="b574a-126">When setting hello password, make sure that you meet hello [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).</span></span>
>
>

<span data-ttu-id="b574a-127">toocreate hello kimlik bilgisi nesnesinin hello güvenli parola dosyasından gerekir hello dosya içeriklerini okuma ve bunları dönüştürmeniz geri tooa güvenli bir dize kullanarak [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="b574a-127">toocreate hello credential object from hello secure password file, you must read hello file contents and convert them back tooa secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="b574a-128">Merhaba [kümesi AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet'ini de kabul eder bir *sona erme* belirten parametresi bir **DateTime** hello kullanıcı hesabının süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="b574a-128">hello [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which hello user account expires.</span></span> <span data-ttu-id="b574a-129">Örneğin, birkaç gün hello hesap tooexpire geçerli tarih ve saat hello ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b574a-129">For example, you could set hello account tooexpire a few days from hello current date and time.</span></span>

<span data-ttu-id="b574a-130">Bu PowerShell örnek nasıl tooset hello Uzak Masaüstü uzantısı'nda bir bulut hizmeti gösterir:</span><span class="sxs-lookup"><span data-stu-id="b574a-130">This PowerShell example shows you how tooset hello Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="b574a-131">Merhaba dağıtım yuvası ve tooenable Uzak Masaüstü'nü istediğiniz rolleri Ayrıca isteğe bağlı olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b574a-131">You can also optionally specify hello deployment slot and roles that you want tooenable remote desktop on.</span></span> <span data-ttu-id="b574a-132">Bu parametre belirtilmezse, Uzak Masaüstü'nü hello tüm rollerde hello cmdlet sağlar **üretim** dağıtım yuvası.</span><span class="sxs-lookup"><span data-stu-id="b574a-132">If these parameters are not specified, hello cmdlet enables remote desktop on all roles in hello **Production** deployment slot.</span></span>

<span data-ttu-id="b574a-133">Uzak Masaüstü uzantısı Hello dağıtımı ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="b574a-133">hello Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="b574a-134">Merhaba hizmeti için yeni bir dağıtım oluşturursanız, bu dağıtım üzerinde tooenable Uzak Masaüstü sahip.</span><span class="sxs-lookup"><span data-stu-id="b574a-134">If you create a new deployment for hello service, you have tooenable remote desktop on that deployment.</span></span> <span data-ttu-id="b574a-135">Ardından, her zaman etkin toohave Uzak Masaüstü istiyorsanız, dağıtım iş akışınıza hello PowerShell betikleri tümleştirme düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="b574a-135">If you always want toohave remote desktop enabled, then you should consider integrating hello PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="b574a-136">Rol örneği içine Uzak Masaüstü</span><span class="sxs-lookup"><span data-stu-id="b574a-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="b574a-137">Merhaba [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet'tir kullanılan tooremote Desktop'a bulut hizmetinizin belirli rol örneği.</span><span class="sxs-lookup"><span data-stu-id="b574a-137">hello [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet is used tooremote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="b574a-138">Merhaba kullanabilirsiniz *LocalPath* parametresi toodownload hello RDP dosyasını yerel olarak.</span><span class="sxs-lookup"><span data-stu-id="b574a-138">You can use hello *LocalPath* parameter toodownload hello RDP file locally.</span></span> <span data-ttu-id="b574a-139">Veya hello kullanabilirsiniz *başlatma* parametresi toodirectly başlatma hello Uzak Masaüstü Bağlantısı iletişim tooaccess hello bulut hizmet rolü örneği.</span><span class="sxs-lookup"><span data-stu-id="b574a-139">Or you can use hello *Launch* parameter toodirectly launch hello Remote Desktop Connection dialog tooaccess hello cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="b574a-140">Uzak Masaüstü uzantısı'nda bir hizmeti etkin olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="b574a-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="b574a-141">Merhaba [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet görüntüler Uzak Masaüstü etkin veya bir hizmet dağıtımı için devre dışı.</span><span class="sxs-lookup"><span data-stu-id="b574a-141">hello [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="b574a-142">Merhaba cmdlet hello Uzak Masaüstü kullanıcı ve hello Uzak Masaüstü uzantısı için etkin hello rolleri için hello kullanıcı adını döndürür.</span><span class="sxs-lookup"><span data-stu-id="b574a-142">hello cmdlet returns hello username for hello remote desktop user and hello roles that hello remote desktop extension is enabled for.</span></span> <span data-ttu-id="b574a-143">Varsayılan olarak, bu hello dağıtım yuvasına gerçekleşir ve bunun yerine hazırlık yuvasındaki toouse hello seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b574a-143">By default, this happens on hello deployment slot and you can choose toouse hello staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="b574a-144">Uzak Masaüstü uzantısı bir hizmetten kaldırın</span><span class="sxs-lookup"><span data-stu-id="b574a-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="b574a-145">Merhaba Uzak Masaüstü uzantısı bir dağıtımda zaten etkinleştirdiyseniz ve uzak masaüstü ayarlarını tooupdate hello, ilk hello uzantısını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="b574a-145">If you have already enabled hello remote desktop extension on a deployment, and need tooupdate hello remote desktop settings, first remove hello extension.</span></span> <span data-ttu-id="b574a-146">Ve hello yeni ayarlarla yeniden etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="b574a-146">And enable it again with hello new settings.</span></span> <span data-ttu-id="b574a-147">Örneğin, tooset istiyorsanız hello uzak kullanıcı hesabı veya hello hesabı için yeni bir parola süresi.</span><span class="sxs-lookup"><span data-stu-id="b574a-147">For example, if you want tooset a new password for hello remote user account, or hello account expired.</span></span> <span data-ttu-id="b574a-148">Bunun yapılması hello Uzak Masaüstü uzantısı etkin olan mevcut dağıtımlarında gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b574a-148">Doing this is required on existing deployments that have hello remote desktop extension enabled.</span></span> <span data-ttu-id="b574a-149">Yeni dağıtımlar için yalnızca hello uzantısı doğrudan uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b574a-149">For new deployments, you can simply apply hello extension directly.</span></span>

<span data-ttu-id="b574a-150">tooremove hello Uzak Masaüstü uzantısı hello dağıtımından, kullanabileceğiniz hello [Kaldır AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="b574a-150">tooremove hello remote desktop extension from hello deployment, you can use hello [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="b574a-151">Ayrıca isteğe bağlı olarak, hello dağıtım yuvası ve tooremove hello Uzak Masaüstü uzantısı istediğiniz rolü de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b574a-151">You can also optionally specify hello deployment slot and role from which you want tooremove hello remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> <span data-ttu-id="b574a-152">toocompletely Kaldır hello uzantı yapılandırması hello çağrı *kaldırmak* hello cmdlet'iyle **UninstallConfiguration** parametresi.</span><span class="sxs-lookup"><span data-stu-id="b574a-152">toocompletely remove hello extension configuration, you should call hello *remove* cmdlet with hello **UninstallConfiguration** parameter.</span></span>
>
> <span data-ttu-id="b574a-153">Merhaba **UninstallConfiguration** parametresi kaldırır herhangi bir uzantı yapılandırma diğer bir deyişle uygulanan toohello hizmet.</span><span class="sxs-lookup"><span data-stu-id="b574a-153">hello **UninstallConfiguration** parameter uninstalls any extension configuration that is applied toohello service.</span></span> <span data-ttu-id="b574a-154">Merhaba hizmet yapılandırmasıyla ilişkili her uzantı yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="b574a-154">Every extension configuration is associated with hello service configuration.</span></span> <span data-ttu-id="b574a-155">Arama hello *kaldırmak* cmdlet olmadan **UninstallConfiguration** hello keser <mark>dağıtım</mark> hello uzantısı yapılandırmasından nedenle etkili bir şekilde kaldırılıyor Merhaba uzantısı.</span><span class="sxs-lookup"><span data-stu-id="b574a-155">Calling hello *remove* cmdlet without **UninstallConfiguration** disassociates hello <mark>deployment</mark> from hello extension configuration, thus effectively removing hello extension.</span></span> <span data-ttu-id="b574a-156">Ancak, hello uzantı yapılandırması hello hizmeti ile ilişkili olarak kalır.</span><span class="sxs-lookup"><span data-stu-id="b574a-156">However, hello extension configuration remains associated with hello service.</span></span>
>
>

## <a name="additional-resources"></a><span data-ttu-id="b574a-157">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b574a-157">Additional resources</span></span>

<span data-ttu-id="b574a-158">[Nasıl tooConfigure bulut Hizmetleri](cloud-services-how-to-configure.md)
[bulut SSS - Uzak Masaüstü Hizmetleri](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="b574a-158">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
