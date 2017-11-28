---
title: "Azure Otomasyonu aaaVariable varlıkları | Microsoft Docs"
description: "Değişken varlıkları kullanılabilir tooall runbook'ları ve Azure Otomasyonu DSC yapılandırmalarında değerlerdir.  Bu makale, değişkenleri hello ayrıntılarını açıklar ve nasıl metinsel ve grafik yazma içinde toowork onlarla."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: b880c15f-46f5-4881-8e98-e034cc5a66ec
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/09/2017
ms.author: magoedte;bwren
ms.openlocfilehash: f9daa49fc1dc883ffb218a9adf26e36df1d6bb27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="variable-assets-in-azure-automation"></a><span data-ttu-id="bfcc9-104">Azure Otomasyonu değişken varlıkları</span><span class="sxs-lookup"><span data-stu-id="bfcc9-104">Variable assets in Azure Automation</span></span>

<span data-ttu-id="bfcc9-105">Değişken varlıkları kullanılabilir tooall runbook'ları ve Otomasyon hesabınızda DSC yapılandırmaları değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-105">Variable assets are values that are available tooall runbooks and DSC configurations in your automation account.</span></span> <span data-ttu-id="bfcc9-106">Bunlar oluşturulan, değiştirilebilir ve hello Azure portalı, Windows PowerShell ve içinden alınan bir runbook veya DSC yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-106">They can be created, modified, and retrieved from hello Azure portal, Windows PowerShell, and from within a runbook or DSC configuration.</span></span> <span data-ttu-id="bfcc9-107">Otomasyon değişkenleri senaryoları aşağıdaki hello için yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="bfcc9-107">Automation variables are useful for hello following scenarios:</span></span>

- <span data-ttu-id="bfcc9-108">Birden çok runbook'ları veya DSC yapılandırması arasında bir değer paylaşır.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-108">Share a value between multiple runbooks or DSC configurations.</span></span>

- <span data-ttu-id="bfcc9-109">Bir değeri hello birden çok iş arasında paylaştırma aynı runbook veya DSC yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-109">Share a value between multiple jobs from hello same runbook or DSC configuration.</span></span>

- <span data-ttu-id="bfcc9-110">Bir değer hello portalından veya runbook'lar veya bir dizi ortak yapılandırma öğelerinin belirli listesi gibi VM adları, belirli bir kaynak grubunun, bir AD etki alanı adı, vb. gibi DSC yapılandırmaları tarafından kullanılan hello Windows PowerShell komut satırından yönetme.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-110">Manage a value from hello portal or from hello Windows PowerShell command line that is used by runbooks or DSC configurations, such as a set of common configuration items like specific list of VM names, a specific resource group,  an AD domain name, etc.</span></span>  

<span data-ttu-id="bfcc9-111">Otomasyon değişkenleri böylece Hello runbook veya DSC yapılandırması başarısız olsa bile kullanıcılar toobe kullanılabilir devam kalıcıdır.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-111">Automation variables are persisted so that they continue toobe available even if hello runbook or DSC configuration fails.</span></span>  <span data-ttu-id="bfcc9-112">Bu da ardından bir başkası tarafından kullanılan veya hello tarafından kullanılan bir runbook tarafından ayarlanan değer toobe sağlar aynı runbook veya DSC yapılandırma Merhaba, İleri çalıştırıldığında.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-112">This also allows a value toobe set by one runbook that is then used by another, or is used by hello same runbook or DSC configuration hello next time that it is run.</span></span>

<span data-ttu-id="bfcc9-113">Bir değişken oluşturulduğunda depolanmasını belirtebilirsiniz şifrelenmiş.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-113">When a variable is created, you can specify that it be stored encrypted.</span></span>  <span data-ttu-id="bfcc9-114">Bir değişken şifrelendiğinde, Azure Automation'da güvenli bir şekilde depolanır ve değeri hello alınamıyor [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) hello Azure PowerShell modülünün bir parçası olarak gönderilen cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-114">When a variable is encrypted, it is stored securely in Azure Automation, and its value cannot be retrieved from hello [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet that ships as part of hello Azure PowerShell module.</span></span>  <span data-ttu-id="bfcc9-115">Merhaba şifrelenmiş değer alınabilir yalnızca hello yoludur **Get-AutomationVariable** etkinliğini runbook veya DSC yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-115">hello only way that an encrypted value can be retrieved is from hello **Get-AutomationVariable** activity in a runbook or DSC configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="bfcc9-116">Azure Automation güvenli varlıkların kimlik bilgileri, sertifikalar, bağlantıları ve şifrelenmiş değişkenler içerir.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="bfcc9-117">Bu varlıklar şifrelenir ve hello Azure her Otomasyon hesabı için oluşturulan benzersiz bir anahtar kullanarak otomasyon depolanır.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-117">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="bfcc9-118">Bu anahtarı bir sertifika tarafından şifrelenir ve Azure Otomasyonu'nda depolanır.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-118">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="bfcc9-119">Güvenli bir varlık depolamak önce hello Otomasyon hesabının hello anahtarı hello ana sertifikayı kullanarak şifresi çözülür ve tooencrypt hello varlık kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-119">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>

## <a name="variable-types"></a><span data-ttu-id="bfcc9-120">Değişken türleri</span><span class="sxs-lookup"><span data-stu-id="bfcc9-120">Variable types</span></span>

<span data-ttu-id="bfcc9-121">Hello Azure portal ile bir değişkeni oluşturduğunuzda, hello portal hello hello değişken değeri girmek için uygun denetimi görüntüleyebilmesi hello aşağı açılan listeden bir veri türü belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-121">When you create a variable with hello Azure portal, you must specify a data type from hello drop-down list so hello portal can display hello appropriate control for entering hello variable value.</span></span> <span data-ttu-id="bfcc9-122">Merhaba değişken kısıtlı toothis veri değil türü, ancak hello değişkeni toospecify istiyorsanız, Windows PowerShell kullanarak bir değere ayarlamalısınız, farklı bir tür.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-122">hello variable is not restricted toothis data type, but you must set hello variable using Windows PowerShell if you want toospecify a value of a different type.</span></span> <span data-ttu-id="bfcc9-123">Belirtirseniz **tanımlanmamış**, hello hello değişkenin değerini çok ayarlayın, sonra da**$null**, ve hello hello değerle ayarlamanız gerekir [kümesi AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet'ini veya **Set-AutomationVariable** etkinlik.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-123">If you specify **Not defined**, then hello value of hello variable will be set too**$null**, and you must set hello value with hello [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet or **Set-AutomationVariable** activity.</span></span>  <span data-ttu-id="bfcc9-124">Oluşturma veya karmaşık değişken türü hello portalında hello değerini değiştirin, ancak Windows PowerShell kullanarak herhangi bir türde bir değer sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-124">You cannot create or change hello value for a complex variable type in hello portal, but you can provide a value of any type using Windows PowerShell.</span></span> <span data-ttu-id="bfcc9-125">Karmaşık türler olarak döndürülecek bir [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="bfcc9-125">Complex types will be returned as a [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span></span>

<span data-ttu-id="bfcc9-126">Birden çok değer tooa tek değişken bir dizi ya da karma oluşturma ve toohello değişkeni kaydetme depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-126">You can store multiple values tooa single variable by creating an array or hashtable and saving it toohello variable.</span></span>

<span data-ttu-id="bfcc9-127">Merhaba, Otomasyon kullanılabilir değişken türlerinin bir listesini şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bfcc9-127">hello following are a list of variable types available in Automation:</span></span>

* <span data-ttu-id="bfcc9-128">Dize</span><span class="sxs-lookup"><span data-stu-id="bfcc9-128">String</span></span>
* <span data-ttu-id="bfcc9-129">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="bfcc9-129">Integer</span></span>
* <span data-ttu-id="bfcc9-130">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="bfcc9-130">DateTime</span></span>
* <span data-ttu-id="bfcc9-131">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="bfcc9-131">Boolean</span></span>
* <span data-ttu-id="bfcc9-132">Null</span><span class="sxs-lookup"><span data-stu-id="bfcc9-132">Null</span></span>

## <a name="cmdlets-and-workflow-activities"></a><span data-ttu-id="bfcc9-133">Cmdlet'ler ve iş akışı etkinlikleri</span><span class="sxs-lookup"><span data-stu-id="bfcc9-133">Cmdlets and workflow activities</span></span>

<span data-ttu-id="bfcc9-134">Aşağıdaki tablonun hello Hello cmdlet'leri kullanılan toocreate olan ve Windows PowerShell ile Otomasyon değişkenleri yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-134">hello cmdlets in hello following table are used toocreate and manage Automation variables with Windows PowerShell.</span></span> <span data-ttu-id="bfcc9-135">Merhaba bir parçası olarak sevk [Azure PowerShell Modülü](../powershell-install-configure.md) olduğu Automation runbook'ları ve DSC yapılandırması için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-135">They ship as part of hello [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configuration.</span></span>

|<span data-ttu-id="bfcc9-136">Cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="bfcc9-136">Cmdlets</span></span>|<span data-ttu-id="bfcc9-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bfcc9-137">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="bfcc9-138">Get-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="bfcc9-138">Get-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603849.aspx)|<span data-ttu-id="bfcc9-139">Mevcut bir değişken Hello değerini alır.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-139">Retrieves hello value of an existing variable.</span></span>|
|[<span data-ttu-id="bfcc9-140">AzureRmAutomationVariable yeni</span><span class="sxs-lookup"><span data-stu-id="bfcc9-140">New-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603613.aspx)|<span data-ttu-id="bfcc9-141">Yeni bir değişken oluşturur ve değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-141">Creates a new variable and sets its value.</span></span>|
|[<span data-ttu-id="bfcc9-142">Remove-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="bfcc9-142">Remove-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt619354.aspx)|<span data-ttu-id="bfcc9-143">Mevcut bir değişken kaldırır.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-143">Removes an existing variable.</span></span>|
|[<span data-ttu-id="bfcc9-144">Set-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="bfcc9-144">Set-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603601.aspx)|<span data-ttu-id="bfcc9-145">Mevcut bir değişken için başlangıç değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-145">Sets hello value for an existing variable.</span></span>|

<span data-ttu-id="bfcc9-146">Aşağıdaki tablonun hello Hello iş akışı etkinlikleri kullanılan tooaccess Otomasyon değişkenleri bir runbook'ta ' dir.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-146">hello workflow activities in hello following table are used tooaccess Automation variables in a runbook.</span></span> <span data-ttu-id="bfcc9-147">Bunlar yalnızca runbook ya da DSC yapılandırması kullanmak için kullanılabilir ve hello Azure PowerShell modülünün bir parçası olarak bulunmaz.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-147">They are only available for use in a runbook or DSC configuration, and do not ship as part of hello Azure PowerShell module.</span></span>

|<span data-ttu-id="bfcc9-148">İş akışı etkinlikleri</span><span class="sxs-lookup"><span data-stu-id="bfcc9-148">Workflow Activities</span></span>|<span data-ttu-id="bfcc9-149">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bfcc9-149">Description</span></span>|
|:---|:---|
|<span data-ttu-id="bfcc9-150">Get-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="bfcc9-150">Get-AutomationVariable</span></span>|<span data-ttu-id="bfcc9-151">Mevcut bir değişken Hello değerini alır.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-151">Retrieves hello value of an existing variable.</span></span>|
|<span data-ttu-id="bfcc9-152">Set-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="bfcc9-152">Set-AutomationVariable</span></span>|<span data-ttu-id="bfcc9-153">Mevcut bir değişken için başlangıç değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-153">Sets hello value for an existing variable.</span></span>|

> [!NOTE] 
> <span data-ttu-id="bfcc9-154">Değişkenleri yapmaktan kaçınmalısınız hello – Name parametresinde **Get-AutomationVariable** runbook veya runbook'ları veya DSC yapılandırması ve Otomasyon arasındaki bağımlılıkları getirebileceğinden DSC yapılandırması Tasarım zamanında değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-154">You should avoid using variables in hello –Name parameter of **Get-AutomationVariable**  in a runbook or DSC configuration since this can complicate discovering dependencies between runbooks or DSC configuration, and Automation variables at design time.</span></span>

## <a name="creating-a-new-automation-variable"></a><span data-ttu-id="bfcc9-155">Yeni Otomasyon değişkeni oluşturma</span><span class="sxs-lookup"><span data-stu-id="bfcc9-155">Creating a new Automation variable</span></span>

### <a name="toocreate-a-new-variable-with-hello-azure-portal"></a><span data-ttu-id="bfcc9-156">toocreate hello Azure portalı ile yeni bir değişken</span><span class="sxs-lookup"><span data-stu-id="bfcc9-156">toocreate a new variable with hello Azure portal</span></span>

1. <span data-ttu-id="bfcc9-157">Otomasyon hesabınızdan hello tıklatın **varlıklar** döşeme ve ardından hello **varlıklar** dikey penceresinde, select **değişkenleri**.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-157">From your Automation account, click hello **Assets** tile and then on hello **Assets** blade, select **Variables**.</span></span>
2. <span data-ttu-id="bfcc9-158">Merhaba üzerinde **değişkenleri** kutucuğu, select **değişken Ekle**.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-158">On hello **Variables** tile, select **Add a variable**.</span></span>
3. <span data-ttu-id="bfcc9-159">Tamamlamak hello hello seçenekleri **yeni değişken** tıklayın ve dikey **Oluştur** hello yeni değişken kaydedin.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-159">Complete hello options on hello **New Variable** blade and click **Create** save hello new variable.</span></span>

### <a name="toocreate-a-new-variable-with-windows-powershell"></a><span data-ttu-id="bfcc9-160">Windows PowerShell ile yeni bir değişken toocreate</span><span class="sxs-lookup"><span data-stu-id="bfcc9-160">toocreate a new variable with Windows PowerShell</span></span>

<span data-ttu-id="bfcc9-161">Merhaba [yeni AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet'i yeni bir değişken oluşturur ve ilk değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-161">hello [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet creates a new variable and sets its initial value.</span></span> <span data-ttu-id="bfcc9-162">Değer hello kullanarak alabilirsiniz [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span><span class="sxs-lookup"><span data-stu-id="bfcc9-162">You can retrieve hello value using [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span></span> <span data-ttu-id="bfcc9-163">Merhaba değer basit bir tür ise, bu türdeki döndürülür.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-163">If hello value is a simple type, then that same type is returned.</span></span> <span data-ttu-id="bfcc9-164">Karmaşık bir tür ise sonra bir **PSCustomObject** döndürülür.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-164">If it’s a complex type, then a **PSCustomObject** is returned.</span></span>

<span data-ttu-id="bfcc9-165">Merhaba aşağıdaki örnek komutlar Göster nasıl toocreate türünde bir değişken dize ve değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-165">hello following sample commands show how toocreate a variable of type string and then return its value.</span></span>

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

<span data-ttu-id="bfcc9-166">Merhaba aşağıdaki örnek komutlar Göster nasıl toocreate karmaşık sahip bir değişken yazın ve ardından özelliklerini geri dönün.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-166">hello following sample commands show how toocreate a variable with a complex type and then return its properties.</span></span> <span data-ttu-id="bfcc9-167">Bir sanal makine bu durumda, nesne **Get-AzureRmVm** kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-167">In this case, a virtual machine object from **Get-AzureRmVm** is used.</span></span>

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a><span data-ttu-id="bfcc9-168">Bir runbook veya DSC yapılandırması bir değişken kullanma</span><span class="sxs-lookup"><span data-stu-id="bfcc9-168">Using a variable in a runbook or DSC configuration</span></span>

<span data-ttu-id="bfcc9-169">Kullanım hello **Set-AutomationVariable** etkinlik tooset hello değişkenin değeri olarak bir Otomasyon runbook'u veya DSC yapılandırması ve hello **Get-AutomationVariable** tooretrieve onu.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-169">Use hello **Set-AutomationVariable** activity tooset hello value of an Automation variable in a runbook or DSC configuration, and hello **Get-AutomationVariable** tooretrieve it.</span></span>  <span data-ttu-id="bfcc9-170">Merhaba kullanmamanız **kümesi AzureAutomationVariable** veya **Get-AzureAutomationVariable** cmdlet'leri runbook veya hello iş akışı etkinlikleri az verimli olduğundan DSC yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-170">You shouldn't use hello **Set-AzureAutomationVariable** or  **Get-AzureAutomationVariable** cmdlets in a runbook or DSC configuration since they are less efficient than hello workflow activities.</span></span>  <span data-ttu-id="bfcc9-171">Güvenli değişkenlerle hello değeri alınamıyor **Get-AzureAutomationVariable**.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-171">You also cannot retrieve hello value of secure variables with **Get-AzureAutomationVariable**.</span></span>  <span data-ttu-id="bfcc9-172">yalnızca yol toocreate bir runbook içindeki yeni bir değişken hello veya DSC yapılandırma toouse hello [yeni AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-172">hello only way toocreate a new variable from within a runbook or DSC configuration is toouse hello [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx)  cmdlet.</span></span>


### <a name="textual-runbook-samples"></a><span data-ttu-id="bfcc9-173">Metin biçiminde runbook örnekleri</span><span class="sxs-lookup"><span data-stu-id="bfcc9-173">Textual runbook samples</span></span>

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a><span data-ttu-id="bfcc9-174">Basit bir değer bir değişkeninden alma ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="bfcc9-174">Setting and retrieving a simple value from a variable</span></span>

<span data-ttu-id="bfcc9-175">Merhaba aşağıdaki örnek komutlar Göster nasıl tooset ve metin biçiminde runbook bir değişkende alır.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-175">hello following sample commands show how tooset and retrieve a variable in a textual runbook.</span></span> <span data-ttu-id="bfcc9-176">Bu örnekte, Tamsayı türünde değişkenleri adlı görünür duruma varsayılır *Numberofıterations* ve *NumberOfRunnings* ve adlı dize türünde bir değişken *SampleMessage* zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-176">In this sample, it is assumed that variables of type integer named *NumberOfIterations* and *NumberOfRunnings* and a variable of type string named *SampleMessage* have already been created.</span></span>

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a><span data-ttu-id="bfcc9-177">Karmaşık bir nesne, bir değişkende alma ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="bfcc9-177">Setting and retrieving a complex object in a variable</span></span>

<span data-ttu-id="bfcc9-178">Merhaba aşağıdaki örnek kod gösterir nasıl tooupdate metin biçiminde runbook karmaşık bir değere sahip bir değişken.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-178">hello following sample code shows how tooupdate a variable with a complex value in a textual runbook.</span></span> <span data-ttu-id="bfcc9-179">Bu örnekte, bir Azure sanal makinesi ile alınan **Get-AzureVM** ve kaydedilmiş tooan var olan Otomasyon değişkeni.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-179">In this sample, an Azure virtual machine is retrieved with **Get-AzureVM** and saved tooan existing Automation variable.</span></span>  <span data-ttu-id="bfcc9-180">İçinde anlatıldığı gibi [değişken türleri](#variable-types), bu PSCustomObject depolanır.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-180">As explained in [Variable types](#variable-types), this is stored as a PSCustomObject.</span></span>

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


<span data-ttu-id="bfcc9-181">Koddan hello hello değeri hello değişken ve kullanılan toostart hello sanal makineden alınır.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-181">In hello following code, hello value is retrieved from hello variable and used toostart hello virtual machine.</span></span>

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a><span data-ttu-id="bfcc9-182">Bir değişken koleksiyonunda alma ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="bfcc9-182">Setting and retrieving a collection in a variable</span></span>

<span data-ttu-id="bfcc9-183">Merhaba aşağıdaki örnek kod gösterir nasıl toouse metinsel bir runbook'ta karmaşık değerler koleksiyonu sahip bir değişken.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-183">hello following sample code shows how toouse a variable with a collection of complex values in a textual runbook.</span></span> <span data-ttu-id="bfcc9-184">Bu örnekte, birden fazla Azure sanal makineler ile alınan **Get-AzureVM** ve kaydedilmiş tooan var olan Otomasyon değişkeni.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-184">In this sample, multiple Azure virtual machines are retrieved with **Get-AzureVM** and saved tooan existing Automation variable.</span></span>  <span data-ttu-id="bfcc9-185">İçinde anlatıldığı gibi [değişken türleri](#variable-types), bu PSCustomObjects koleksiyonu olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-185">As explained in [Variable types](#variable-types), this is stored as a collection of PSCustomObjects.</span></span>

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

<span data-ttu-id="bfcc9-186">Koddan hello hello koleksiyonu hello değişkeninden alınır ve her sanal makine toostart kullanılan.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-186">In hello following code, hello collection is retrieved from hello variable and used toostart each virtual machine.</span></span>

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a><span data-ttu-id="bfcc9-187">Grafik runbook örnekleri</span><span class="sxs-lookup"><span data-stu-id="bfcc9-187">Graphical runbook samples</span></span>

<span data-ttu-id="bfcc9-188">Bir grafik runbook'ta hello eklemek **Get-AutomationVariable** veya **Set-AutomationVariable** hello değişkeni hello grafik Düzenleyicisi hello Kitaplık bölmesinde sağ tıklayarak ve hello seçme istediğiniz etkinliği.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-188">In a graphical runbook, you add hello **Get-AutomationVariable** or **Set-AutomationVariable** by right-clicking on hello variable in hello Library pane of hello graphical editor and selecting hello activity you want.</span></span>

![Değişken toocanvas Ekle](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a><span data-ttu-id="bfcc9-190">Bir değişkende değerleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="bfcc9-190">Setting values in a variable</span></span>
<span data-ttu-id="bfcc9-191">Hello aşağıdaki görüntüde örnek etkinlikleri tooupdate bir değere sahip bir değişken basit bir grafik runbook'u gösterir.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-191">hello following image shows sample activities tooupdate a variable with a simple value in a graphical runbook.</span></span> <span data-ttu-id="bfcc9-192">Bu örnekte, tek bir Azure sanal makine ile alınan **Get-AzureRmVM** ve hello bilgisayar adı bir dize türü ile tooan var olan Otomasyon değişkeni kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-192">In this sample, a single Azure virtual machine is retrieved with **Get-AzureRmVM** and hello computer name is saved tooan existing Automation variable with a type of String.</span></span>  <span data-ttu-id="bfcc9-193">Hello olup olmadığını önemli değildir [bağlantıdır bir ardışık düzen veya dizisi](automation-graphical-authoring-intro.md#links-and-workflow) bu yana yalnızca tek bir nesne hello çıktısında bekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="bfcc9-193">It doesn't matter whether hello [link is a pipeline or sequence](automation-graphical-authoring-intro.md#links-and-workflow) since we only expect a single object in hello output.</span></span>

![Basit değişken Ayarla](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a><span data-ttu-id="bfcc9-195">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="bfcc9-195">Next Steps</span></span>

* <span data-ttu-id="bfcc9-196">Grafik yazma etkinlikleri birbirine bağlama hakkında daha fazla toolearn bakın [grafik yazma içindeki bağlantılar](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="bfcc9-196">toolearn more about connecting activities together in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="bfcc9-197">Grafik runbook'ları ile çalışmaya tooget bakın [ilk grafik runbook Uygulamam](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="bfcc9-197">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span> 

