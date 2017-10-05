---
title: "PowerShell kullanarak Azure Cloud Services rolünde için Uzak Masaüstü Bağlantısı etkinleştir"
description: "Uzak Masaüstü bağlantılara izin vermek için PowerShell kullanarak azure bulut hizmeti uygulamanızı yapılandırma"
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
ms.openlocfilehash: 171f27c92ee9de14301ebb664e9ba3bcd98c394d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="d8bb2-103">PowerShell kullanarak Azure Cloud Services rolünde için Uzak Masaüstü Bağlantısı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="d8bb2-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8bb2-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="d8bb2-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="d8bb2-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="d8bb2-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="d8bb2-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8bb2-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="d8bb2-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d8bb2-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="d8bb2-108">Uzak Masaüstü, Azure'da çalışan rolü Masaüstü erişmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="d8bb2-109">Uzak Masaüstü Bağlantısı çalışırken, uygulamanızın sorunları tanılamak ve gidermek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="d8bb2-110">Bu makalede, Uzak Masaüstü'nü PowerShell kullanarak, bulut hizmeti rollerinizi etkinleştirmek açıklar.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-110">This article describes how to enable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="d8bb2-111">Bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview) Bu makale için gereken önkoşulları için.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-111">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span> <span data-ttu-id="d8bb2-112">Uygulama dağıtıldıktan sonra Uzak Masaüstü'nü etkinleştirmek için PowerShell Uzak Masaüstü uzantısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-112">PowerShell utilizes the Remote Desktop Extension so you can enable Remote Desktop after the application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="d8bb2-113">Uzak Masaüstü PowerShell üzerinden yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="d8bb2-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="d8bb2-114">[Kümesi AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet'i belirtilen roller veya Bulut hizmeti dağıtımınızın tüm roller üzerinde Uzak Masaüstü etkinleştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-114">The [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet allows you to enable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="d8bb2-115">Cmdlet'i Uzak Masaüstü kullanıcı için kullanıcı adı ve parola belirtmenize olanak tanır *kimlik bilgisi* bir PSCredential nesnesi kabul parametresi.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-115">The cmdlet lets you specify the Username and Password for the remote desktop user through the *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="d8bb2-116">PowerShell etkileşimli olarak kullanıyorsanız, kolayca PSCredential nesnesinin çağırarak ayarlayabilirsiniz [Get-kimlik bilgilerinin](https://technet.microsoft.com/library/hh849815.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-116">If you are using PowerShell interactively, you can easily set the PSCredential object by calling the [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="d8bb2-117">Bu komut, güvenli bir şekilde uzak kullanıcı için kullanıcı adı ve parola girmesini sağlayan bir iletişim kutusu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-117">This command displays a dialog box allowing you to enter the username and password for the remote user in a secure manner.</span></span>

<span data-ttu-id="d8bb2-118">PowerShell Otomasyon senaryolarda yardımcı olduğundan, ayrıca ayarlayabilirsiniz **PSCredential** , kullanıcı etkileşimi gerektirmeyen şekilde nesnesi.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-118">Since PowerShell helps in automation scenarios, you can also set up the **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="d8bb2-119">İlk olarak, güvenli bir parola ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-119">First, you need to set up a secure password.</span></span> <span data-ttu-id="d8bb2-120">Düz metinli bir parola dönüştürür kullanarak bir güvenli dize belirterek başlamadan [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8bb2-120">You begin with specifying a plain text password convert it to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="d8bb2-121">Bir şifrelenmiş standart dize kullanarak bu güvenli dize dönüştürmeniz gerekir sonraki [ConvertFrom SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8bb2-121">Next you need to convert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="d8bb2-122">Bu şifreli bir standart dize kullanarak bir dosyaya kaydedebilirsiniz [kümesi içeriği](https://technet.microsoft.com/library/ee176959.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8bb2-122">Now you can save this encrypted standard string to a file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="d8bb2-123">Böylece her zaman parola yazmak zorunda kalmazsınız güvenli parola dosyası da oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-123">You can also create a secure password file so that you don't have to type in the password every time.</span></span> <span data-ttu-id="d8bb2-124">Ayrıca, güvenli parola dosyasına düz metin dosyasından daha iyidir.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="d8bb2-125">Güvenli parola dosyası oluşturmak için aşağıdaki PowerShell kullanın:</span><span class="sxs-lookup"><span data-stu-id="d8bb2-125">Use the following PowerShell to create a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> <span data-ttu-id="d8bb2-126">Parolayı ayarlarken, karşıladığından emin olun [karmaşıklık gereksinimlerini](https://technet.microsoft.com/library/cc786468.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8bb2-126">When setting the password, make sure that you meet the [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).</span></span>
>
>

<span data-ttu-id="d8bb2-127">Güvenli parola dosyasından kimlik bilgisi nesnesi oluşturmak için dosya içeriğini okumak ve bunları geri bir güvenli dize kullanmaya Dönüştür [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8bb2-127">To create the credential object from the secure password file, you must read the file contents and convert them back to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="d8bb2-128">[Kümesi AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet'ini de kabul eder bir *sona erme* belirten parametresi bir **DateTime** hangi kullanıcı hesabının süresi sırasında.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-128">The [Set-AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which the user account expires.</span></span> <span data-ttu-id="d8bb2-129">Örneğin, geçerli tarih ve saat birkaç gün süresi dolacak şekilde hesabı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-129">For example, you could set the account to expire a few days from the current date and time.</span></span>

<span data-ttu-id="d8bb2-130">Bu PowerShell örnek bir bulut hizmeti Uzak Masaüstü uzantısı kümesi gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="d8bb2-130">This PowerShell example shows you how to set the Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="d8bb2-131">Dağıtım yuvası ve Uzak Masaüstü'nü etkinleştirmek istediğiniz rolleri Ayrıca isteğe bağlı olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-131">You can also optionally specify the deployment slot and roles that you want to enable remote desktop on.</span></span> <span data-ttu-id="d8bb2-132">Bu parametre belirtilmezse, Uzak Masaüstü'nü tüm rollerde cmdlet sağlar **üretim** dağıtım yuvası.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-132">If these parameters are not specified, the cmdlet enables remote desktop on all roles in the **Production** deployment slot.</span></span>

<span data-ttu-id="d8bb2-133">Dağıtımla ilişkili Uzak Masaüstü uzantısıdır.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-133">The Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="d8bb2-134">Hizmeti için yeni bir dağıtım oluşturursanız, bu dağıtımda, Uzak Masaüstü'nü etkinleştirin sahip.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-134">If you create a new deployment for the service, you have to enable remote desktop on that deployment.</span></span> <span data-ttu-id="d8bb2-135">Her zaman Uzak Masaüstü etkin olmasını istiyorsanız, PowerShell komut dosyalarını iş akışınıza dağıtım tümleştirme düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-135">If you always want to have remote desktop enabled, then you should consider integrating the PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="d8bb2-136">Rol örneği içine Uzak Masaüstü</span><span class="sxs-lookup"><span data-stu-id="d8bb2-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="d8bb2-137">[Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet'tir kullanılan Uzak Masaüstü bulut hizmetinizin belirli rol örneği başlatın.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-137">The [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet is used to remote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="d8bb2-138">Kullanabileceğiniz *LocalPath* RDP indirmek için parametre dosyası yerel olarak.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-138">You can use the *LocalPath* parameter to download the RDP file locally.</span></span> <span data-ttu-id="d8bb2-139">Veya kullanabilirsiniz *başlatma* doğrudan bulut Hizmeti rol örneğine erişmek için Uzak Masaüstü Bağlantısı iletişim kutusunu başlatmak için parametre.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-139">Or you can use the *Launch* parameter to directly launch the Remote Desktop Connection dialog to access the cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="d8bb2-140">Uzak Masaüstü uzantısı'nda bir hizmeti etkin olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="d8bb2-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="d8bb2-141">[Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet görüntüler Uzak Masaüstü etkin veya bir hizmet dağıtımı için devre dışı.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-141">The [Get-AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="d8bb2-142">Cmdlet Uzak Masaüstü kullanıcı ve Uzak Masaüstü uzantısı için etkin rolleri için kullanıcı adını döndürür.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-142">The cmdlet returns the username for the remote desktop user and the roles that the remote desktop extension is enabled for.</span></span> <span data-ttu-id="d8bb2-143">Varsayılan olarak, bu dağıtım yuvasına gerçekleşir ve hazırlama yuvası kullanmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-143">By default, this happens on the deployment slot and you can choose to use the staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="d8bb2-144">Uzak Masaüstü uzantısı bir hizmetten kaldırın</span><span class="sxs-lookup"><span data-stu-id="d8bb2-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="d8bb2-145">Uzak Masaüstü uzantısı bir dağıtımda zaten etkinleştirdiyseniz ve uzak masaüstü ayarlarını güncelleştirmek ihtiyacınız varsa, ilk uzantısını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-145">If you have already enabled the remote desktop extension on a deployment, and need to update the remote desktop settings, first remove the extension.</span></span> <span data-ttu-id="d8bb2-146">Ve yeni ayarlarla yeniden etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-146">And enable it again with the new settings.</span></span> <span data-ttu-id="d8bb2-147">Örneğin, uzak kullanıcı hesabı için yeni bir parola ayarlayın veya hesabın süresi istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-147">For example, if you want to set a new password for the remote user account, or the account expired.</span></span> <span data-ttu-id="d8bb2-148">Bunun yapılması, etkin Uzak Masaüstü uzantısına sahip var olan dağıtımlar üzerinde gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-148">Doing this is required on existing deployments that have the remote desktop extension enabled.</span></span> <span data-ttu-id="d8bb2-149">Yeni dağıtımlar için yalnızca uzantısı doğrudan uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-149">For new deployments, you can simply apply the extension directly.</span></span>

<span data-ttu-id="d8bb2-150">Uzak Masaüstü uzantısı dağıtımından kaldırmak için kullanabileceğiniz [Kaldır AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-150">To remove the remote desktop extension from the deployment, you can use the [Remove-AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="d8bb2-151">Dağıtım yuvası ve Uzak Masaüstü uzantıyı kaldırmak istediğiniz rol Ayrıca isteğe bağlı olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-151">You can also optionally specify the deployment slot and role from which you want to remove the remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> <span data-ttu-id="d8bb2-152">Uzantı yapılandırması tamamen kaldırmak için çağırmalıdır *kaldırmak* cmdlet'iyle **UninstallConfiguration** parametresi.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-152">To completely remove the extension configuration, you should call the *remove* cmdlet with the **UninstallConfiguration** parameter.</span></span>
>
> <span data-ttu-id="d8bb2-153">**UninstallConfiguration** parametresi hizmetine uygulanan herhangi bir uzantı yapılandırma kaldırır.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-153">The **UninstallConfiguration** parameter uninstalls any extension configuration that is applied to the service.</span></span> <span data-ttu-id="d8bb2-154">Hizmet yapılandırmasıyla ilişkili her uzantı yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-154">Every extension configuration is associated with the service configuration.</span></span> <span data-ttu-id="d8bb2-155">Çağırma *kaldırmak* cmdlet olmadan **UninstallConfiguration** keser <mark>dağıtım</mark> uzantısı yapılandırmasından nedenle etkili bir şekilde kaldırılıyor uzantı.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-155">Calling the *remove* cmdlet without **UninstallConfiguration** disassociates the <mark>deployment</mark> from the extension configuration, thus effectively removing the extension.</span></span> <span data-ttu-id="d8bb2-156">Ancak, uzantısı Yapılandırma hizmeti ile ilişkili olarak kalır.</span><span class="sxs-lookup"><span data-stu-id="d8bb2-156">However, the extension configuration remains associated with the service.</span></span>
>
>

## <a name="additional-resources"></a><span data-ttu-id="d8bb2-157">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d8bb2-157">Additional resources</span></span>

<span data-ttu-id="d8bb2-158">[Bulut hizmetleri yapılandırmak için nasıl](cloud-services-how-to-configure.md)
[bulut SSS - Uzak Masaüstü Hizmetleri](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="d8bb2-158">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
