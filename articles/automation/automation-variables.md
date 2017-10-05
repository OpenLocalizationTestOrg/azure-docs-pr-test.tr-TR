---
title: "Azure Otomasyonu değişken varlıkları | Microsoft Docs"
description: "Değişken varlıkları tüm runbook'lar ve Azure Otomasyonu DSC yapılandırmalarında kullanılabilen değerlerdir.  Bu makalede, değişkenlerin ve bunlarla metinsel ve grafik yazma çalışma konusunda ayrıntılar açıklanmaktadır."
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
ms.openlocfilehash: dc00e1e5fa8df5cb55e7e2672137d1df44133773
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="variable-assets-in-azure-automation"></a><span data-ttu-id="5f2cf-104">Azure Otomasyonu değişken varlıkları</span><span class="sxs-lookup"><span data-stu-id="5f2cf-104">Variable assets in Azure Automation</span></span>

<span data-ttu-id="5f2cf-105">Değişken varlıkları tüm runbook'lar ve Otomasyon hesabınızda DSC yapılandırmaları kullanılabilen değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-105">Variable assets are values that are available to all runbooks and DSC configurations in your automation account.</span></span> <span data-ttu-id="5f2cf-106">Bunlar oluşturulan, değiştirilebilir ve Windows PowerShell, Azure portalından ve içinden alınan bir runbook veya DSC yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-106">They can be created, modified, and retrieved from the Azure portal, Windows PowerShell, and from within a runbook or DSC configuration.</span></span> <span data-ttu-id="5f2cf-107">Otomasyon değişkenleri aşağıdaki senaryolarda kullanışlıdır:</span><span class="sxs-lookup"><span data-stu-id="5f2cf-107">Automation variables are useful for the following scenarios:</span></span>

- <span data-ttu-id="5f2cf-108">Birden çok runbook'ları veya DSC yapılandırması arasında bir değer paylaşır.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-108">Share a value between multiple runbooks or DSC configurations.</span></span>

- <span data-ttu-id="5f2cf-109">Bir değeri aynı runbook veya DSC yapılandırması birden çok iş arasında paylaştırma.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-109">Share a value between multiple jobs from the same runbook or DSC configuration.</span></span>

- <span data-ttu-id="5f2cf-110">Bir değeri portalından veya runbook'lar veya bir dizi ortak yapılandırma öğelerinin belirli listesi gibi VM adları, belirli bir kaynak grubunun, bir AD etki alanı adı, vb. gibi DSC yapılandırmaları tarafından kullanılan Windows PowerShell komut satırından yönetme.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-110">Manage a value from the portal or from the Windows PowerShell command line that is used by runbooks or DSC configurations, such as a set of common configuration items like specific list of VM names, a specific resource group,  an AD domain name, etc.</span></span>  

<span data-ttu-id="5f2cf-111">Böylece runbook veya DSC yapılandırma başarısız olsa bile kullanılabilir olmaya devam Otomasyon değişkenleri kalıcıdır.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-111">Automation variables are persisted so that they continue to be available even if the runbook or DSC configuration fails.</span></span>  <span data-ttu-id="5f2cf-112">Bu DSC yapılandırması bu İleri çalıştırıldığında ve aynı runbook tarafından kullanılan veya bir başkası tarafından sonra kullanılan bir runbook tarafından ayarlamak için bir değer de sağlar.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-112">This also allows a value to be set by one runbook that is then used by another, or is used by the same runbook or DSC configuration the next time that it is run.</span></span>

<span data-ttu-id="5f2cf-113">Bir değişken oluşturulduğunda depolanmasını belirtebilirsiniz şifrelenmiş.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-113">When a variable is created, you can specify that it be stored encrypted.</span></span>  <span data-ttu-id="5f2cf-114">Bir değişken şifrelendiğinde, Azure Automation'da güvenli bir şekilde depolanır ve değeri alınamaz [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) Azure PowerShell modülünün bir parçası olarak gönderilen cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-114">When a variable is encrypted, it is stored securely in Azure Automation, and its value cannot be retrieved from the [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet that ships as part of the Azure PowerShell module.</span></span>  <span data-ttu-id="5f2cf-115">Şifrelenmiş değer alınabilir tek yolu **Get-AutomationVariable** etkinliğini runbook veya DSC yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-115">The only way that an encrypted value can be retrieved is from the **Get-AutomationVariable** activity in a runbook or DSC configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="5f2cf-116">Azure Automation güvenli varlıkların kimlik bilgileri, sertifikalar, bağlantıları ve şifrelenmiş değişkenler içerir.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="5f2cf-117">Bu varlıklar şifrelenir ve her Otomasyon hesabı için oluşturulan benzersiz bir anahtar kullanarak Azure Automation depolanır.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-117">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="5f2cf-118">Bu anahtarı bir sertifika tarafından şifrelenir ve Azure Otomasyonu'nda depolanır.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-118">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="5f2cf-119">Güvenli bir varlık depolamak önce anahtar Otomasyon hesabı için sertifika aracılığıyla çözülür ve varlık şifrelemek için kullanılan.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-119">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>

## <a name="variable-types"></a><span data-ttu-id="5f2cf-120">Değişken türleri</span><span class="sxs-lookup"><span data-stu-id="5f2cf-120">Variable types</span></span>

<span data-ttu-id="5f2cf-121">Azure portal ile bir değişkeni oluşturduğunuzda, portal değişken değeri girmek için uygun denetimi görüntüleyebilmesi aşağı açılan listeden bir veri türü belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-121">When you create a variable with the Azure portal, you must specify a data type from the drop-down list so the portal can display the appropriate control for entering the variable value.</span></span> <span data-ttu-id="5f2cf-122">Değişkeni bu veri türü için sınırlı değildir, ancak farklı türde bir değer belirtmek istiyorsanız Windows PowerShell kullanarak değişkenini ayarlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-122">The variable is not restricted to this data type, but you must set the variable using Windows PowerShell if you want to specify a value of a different type.</span></span> <span data-ttu-id="5f2cf-123">Belirtirseniz **tanımlanmamış**, değişkenin değeri ayarlanacak sonra **$null**, ve değerle ayarlamanız gerekir [kümesi AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet'ini veya **Set-AutomationVariable** etkinlik.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-123">If you specify **Not defined**, then the value of the variable will be set to **$null**, and you must set the value with the [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet or **Set-AutomationVariable** activity.</span></span>  <span data-ttu-id="5f2cf-124">Oluşturma veya karmaşık değişken türü portalında değerini değiştirin, ancak Windows PowerShell kullanarak herhangi bir türde bir değer sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-124">You cannot create or change the value for a complex variable type in the portal, but you can provide a value of any type using Windows PowerShell.</span></span> <span data-ttu-id="5f2cf-125">Karmaşık türler olarak döndürülecek bir [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="5f2cf-125">Complex types will be returned as a [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span></span>

<span data-ttu-id="5f2cf-126">Bir dizi ya da karma tablosu oluşturarak ve değişkenine kaydetme birden çok değeri tek bir değişkende depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-126">You can store multiple values to a single variable by creating an array or hashtable and saving it to the variable.</span></span>

<span data-ttu-id="5f2cf-127">Değişken türleri Otomasyon kullanılabilir bir listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5f2cf-127">The following are a list of variable types available in Automation:</span></span>

* <span data-ttu-id="5f2cf-128">Dize</span><span class="sxs-lookup"><span data-stu-id="5f2cf-128">String</span></span>
* <span data-ttu-id="5f2cf-129">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="5f2cf-129">Integer</span></span>
* <span data-ttu-id="5f2cf-130">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="5f2cf-130">DateTime</span></span>
* <span data-ttu-id="5f2cf-131">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="5f2cf-131">Boolean</span></span>
* <span data-ttu-id="5f2cf-132">Null</span><span class="sxs-lookup"><span data-stu-id="5f2cf-132">Null</span></span>

## <a name="cmdlets-and-workflow-activities"></a><span data-ttu-id="5f2cf-133">Cmdlet'ler ve iş akışı etkinlikleri</span><span class="sxs-lookup"><span data-stu-id="5f2cf-133">Cmdlets and workflow activities</span></span>

<span data-ttu-id="5f2cf-134">Aşağıdaki tabloda yer alan cmdlet'ler oluşturmak ve Otomasyon değişkenleri Windows PowerShell ile yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-134">The cmdlets in the following table are used to create and manage Automation variables with Windows PowerShell.</span></span> <span data-ttu-id="5f2cf-135">Bir parçası olarak sevk [Azure PowerShell Modülü](../powershell-install-configure.md) olduğu Automation runbook'ları ve DSC yapılandırması için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-135">They ship as part of the [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configuration.</span></span>

|<span data-ttu-id="5f2cf-136">Cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="5f2cf-136">Cmdlets</span></span>|<span data-ttu-id="5f2cf-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5f2cf-137">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="5f2cf-138">Get-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="5f2cf-138">Get-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603849.aspx)|<span data-ttu-id="5f2cf-139">Mevcut bir değişken değerini alır.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-139">Retrieves the value of an existing variable.</span></span>|
|[<span data-ttu-id="5f2cf-140">AzureRmAutomationVariable yeni</span><span class="sxs-lookup"><span data-stu-id="5f2cf-140">New-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603613.aspx)|<span data-ttu-id="5f2cf-141">Yeni bir değişken oluşturur ve değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-141">Creates a new variable and sets its value.</span></span>|
|[<span data-ttu-id="5f2cf-142">Remove-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="5f2cf-142">Remove-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt619354.aspx)|<span data-ttu-id="5f2cf-143">Mevcut bir değişken kaldırır.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-143">Removes an existing variable.</span></span>|
|[<span data-ttu-id="5f2cf-144">Set-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="5f2cf-144">Set-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603601.aspx)|<span data-ttu-id="5f2cf-145">Mevcut bir değişken için değeri ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-145">Sets the value for an existing variable.</span></span>|

<span data-ttu-id="5f2cf-146">Aşağıdaki tabloda iş akışı etkinlikleri Otomasyon bir runbook'ta değişkenlere erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-146">The workflow activities in the following table are used to access Automation variables in a runbook.</span></span> <span data-ttu-id="5f2cf-147">Bunlar yalnızca runbook ya da DSC yapılandırması kullanmak için kullanılabilir ve Azure PowerShell modülünün bir parçası olarak bulunmaz.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-147">They are only available for use in a runbook or DSC configuration, and do not ship as part of the Azure PowerShell module.</span></span>

|<span data-ttu-id="5f2cf-148">İş akışı etkinlikleri</span><span class="sxs-lookup"><span data-stu-id="5f2cf-148">Workflow Activities</span></span>|<span data-ttu-id="5f2cf-149">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5f2cf-149">Description</span></span>|
|:---|:---|
|<span data-ttu-id="5f2cf-150">Get-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="5f2cf-150">Get-AutomationVariable</span></span>|<span data-ttu-id="5f2cf-151">Mevcut bir değişken değerini alır.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-151">Retrieves the value of an existing variable.</span></span>|
|<span data-ttu-id="5f2cf-152">Set-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="5f2cf-152">Set-AutomationVariable</span></span>|<span data-ttu-id="5f2cf-153">Mevcut bir değişken için değeri ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-153">Sets the value for an existing variable.</span></span>|

> [!NOTE] 
> <span data-ttu-id="5f2cf-154">Yapmaktan kaçınmalısınız – Name parametresinde **Get-AutomationVariable** runbook veya bu runbook'ları veya DSC yapılandırması ve Otomasyon değişkenleri arasındaki bağımlılıkları tasarım zamanında getirebileceğinden DSC yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-154">You should avoid using variables in the –Name parameter of **Get-AutomationVariable**  in a runbook or DSC configuration since this can complicate discovering dependencies between runbooks or DSC configuration, and Automation variables at design time.</span></span>

## <a name="creating-a-new-automation-variable"></a><span data-ttu-id="5f2cf-155">Yeni Otomasyon değişkeni oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f2cf-155">Creating a new Automation variable</span></span>

### <a name="to-create-a-new-variable-with-the-azure-portal"></a><span data-ttu-id="5f2cf-156">Azure portalı ile yeni bir değişken oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="5f2cf-156">To create a new variable with the Azure portal</span></span>

1. <span data-ttu-id="5f2cf-157">Otomasyon hesabınızdan tıklatın **varlıklar** döşeme ve daha sonra **varlıklar** dikey penceresinde, select **değişkenleri**.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-157">From your Automation account, click the **Assets** tile and then on the **Assets** blade, select **Variables**.</span></span>
2. <span data-ttu-id="5f2cf-158">Üzerinde **değişkenleri** kutucuğu, select **değişken Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-158">On the **Variables** tile, select **Add a variable**.</span></span>
3. <span data-ttu-id="5f2cf-159">Seçenekleri tamamlayın **yeni değişken** tıklayın ve dikey **oluşturma** yeni değişkeni kaydetmek.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-159">Complete the options on the **New Variable** blade and click **Create** save the new variable.</span></span>

### <a name="to-create-a-new-variable-with-windows-powershell"></a><span data-ttu-id="5f2cf-160">Windows PowerShell ile yeni bir değişken oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="5f2cf-160">To create a new variable with Windows PowerShell</span></span>

<span data-ttu-id="5f2cf-161">[Yeni AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet'i yeni bir değişken oluşturur ve ilk değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-161">The [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet creates a new variable and sets its initial value.</span></span> <span data-ttu-id="5f2cf-162">Değer kullanarak alabilirsiniz [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span><span class="sxs-lookup"><span data-stu-id="5f2cf-162">You can retrieve the value using [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span></span> <span data-ttu-id="5f2cf-163">Değer basit bir tür ise, bu türdeki döndürülür.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-163">If the value is a simple type, then that same type is returned.</span></span> <span data-ttu-id="5f2cf-164">Karmaşık bir tür ise sonra bir **PSCustomObject** döndürülür.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-164">If it’s a complex type, then a **PSCustomObject** is returned.</span></span>

<span data-ttu-id="5f2cf-165">Aşağıdaki örnek komutlar dize türünde bir değişken oluşturma ve değerini döndür göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-165">The following sample commands show how to create a variable of type string and then return its value.</span></span>

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

<span data-ttu-id="5f2cf-166">Aşağıdaki örnek komutlar bir karmaşık türü ile bir değişken oluşturun ve özelliklerini dönmek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-166">The following sample commands show how to create a variable with a complex type and then return its properties.</span></span> <span data-ttu-id="5f2cf-167">Bir sanal makine bu durumda, nesne **Get-AzureRmVm** kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-167">In this case, a virtual machine object from **Get-AzureRmVm** is used.</span></span>

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a><span data-ttu-id="5f2cf-168">Bir runbook veya DSC yapılandırması bir değişken kullanma</span><span class="sxs-lookup"><span data-stu-id="5f2cf-168">Using a variable in a runbook or DSC configuration</span></span>

<span data-ttu-id="5f2cf-169">Kullanım **Set-AutomationVariable** bir runbook veya DSC yapılandırması, bir Otomasyon değişkenin değerini ayarlamak için etkinlik ve **Get-AutomationVariable** bunu almak için.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-169">Use the **Set-AutomationVariable** activity to set the value of an Automation variable in a runbook or DSC configuration, and the **Get-AutomationVariable** to retrieve it.</span></span>  <span data-ttu-id="5f2cf-170">Kullanmamanız **kümesi AzureAutomationVariable** veya **Get-AzureAutomationVariable** cmdlet'leri runbook veya iş akışı etkinlikleri az verimli olduğundan DSC yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-170">You shouldn't use the **Set-AzureAutomationVariable** or  **Get-AzureAutomationVariable** cmdlets in a runbook or DSC configuration since they are less efficient than the workflow activities.</span></span>  <span data-ttu-id="5f2cf-171">Güvenli değişkenlerle değeri alınamıyor **Get-AzureAutomationVariable**.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-171">You also cannot retrieve the value of secure variables with **Get-AzureAutomationVariable**.</span></span>  <span data-ttu-id="5f2cf-172">Bir runbook veya DSC yapılandırması içinde yeni bir değişken oluşturmak için tek yolu kullanmaktır [yeni AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-172">The only way to create a new variable from within a runbook or DSC configuration is to use the [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx)  cmdlet.</span></span>


### <a name="textual-runbook-samples"></a><span data-ttu-id="5f2cf-173">Metin biçiminde runbook örnekleri</span><span class="sxs-lookup"><span data-stu-id="5f2cf-173">Textual runbook samples</span></span>

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a><span data-ttu-id="5f2cf-174">Basit bir değer bir değişkeninden alma ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="5f2cf-174">Setting and retrieving a simple value from a variable</span></span>

<span data-ttu-id="5f2cf-175">Aşağıdaki örnek komutlar ayarlamak ve metin biçiminde runbook bir değişkende almak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-175">The following sample commands show how to set and retrieve a variable in a textual runbook.</span></span> <span data-ttu-id="5f2cf-176">Bu örnekte, Tamsayı türünde değişkenleri adlı görünür duruma varsayılır *Numberofıterations* ve *NumberOfRunnings* ve adlı dize türünde bir değişken *SampleMessage* zaten oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-176">In this sample, it is assumed that variables of type integer named *NumberOfIterations* and *NumberOfRunnings* and a variable of type string named *SampleMessage* have already been created.</span></span>

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a><span data-ttu-id="5f2cf-177">Karmaşık bir nesne, bir değişkende alma ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="5f2cf-177">Setting and retrieving a complex object in a variable</span></span>

<span data-ttu-id="5f2cf-178">Aşağıdaki örnek kod, metin biçiminde runbook karmaşık bir değere sahip bir değişken güncelleştirme gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-178">The following sample code shows how to update a variable with a complex value in a textual runbook.</span></span> <span data-ttu-id="5f2cf-179">Bu örnekte, bir Azure sanal makinesi ile alınan **Get-AzureVM** ve varolan bir Otomasyon değişkeni kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-179">In this sample, an Azure virtual machine is retrieved with **Get-AzureVM** and saved to an existing Automation variable.</span></span>  <span data-ttu-id="5f2cf-180">İçinde anlatıldığı gibi [değişken türleri](#variable-types), bu PSCustomObject depolanır.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-180">As explained in [Variable types](#variable-types), this is stored as a PSCustomObject.</span></span>

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


<span data-ttu-id="5f2cf-181">Aşağıdaki kodda değeri değişkeninden alınır ve sanal makineyi başlatmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-181">In the following code, the value is retrieved from the variable and used to start the virtual machine.</span></span>

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a><span data-ttu-id="5f2cf-182">Bir değişken koleksiyonunda alma ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="5f2cf-182">Setting and retrieving a collection in a variable</span></span>

<span data-ttu-id="5f2cf-183">Aşağıdaki örnek kod bir metinsel runbook'ta karmaşık değerler koleksiyonu ile bir değişken kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-183">The following sample code shows how to use a variable with a collection of complex values in a textual runbook.</span></span> <span data-ttu-id="5f2cf-184">Bu örnekte, birden fazla Azure sanal makineler ile alınan **Get-AzureVM** ve varolan bir Otomasyon değişkeni kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-184">In this sample, multiple Azure virtual machines are retrieved with **Get-AzureVM** and saved to an existing Automation variable.</span></span>  <span data-ttu-id="5f2cf-185">İçinde anlatıldığı gibi [değişken türleri](#variable-types), bu PSCustomObjects koleksiyonu olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-185">As explained in [Variable types](#variable-types), this is stored as a collection of PSCustomObjects.</span></span>

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

<span data-ttu-id="5f2cf-186">Aşağıdaki kodda, koleksiyon değişkeninden alınır ve her sanal makineyi başlatmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-186">In the following code, the collection is retrieved from the variable and used to start each virtual machine.</span></span>

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a><span data-ttu-id="5f2cf-187">Grafik runbook örnekleri</span><span class="sxs-lookup"><span data-stu-id="5f2cf-187">Graphical runbook samples</span></span>

<span data-ttu-id="5f2cf-188">Bir grafik runbook'ta eklediğiniz **Get-AutomationVariable** veya **Set-AutomationVariable** grafik düzenleyicisini Kitaplık bölmesinde değişkeni sağ tıklatın ve istediğiniz etkinliği seçerek.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-188">In a graphical runbook, you add the **Get-AutomationVariable** or **Set-AutomationVariable** by right-clicking on the variable in the Library pane of the graphical editor and selecting the activity you want.</span></span>

![Tuvale değişken Ekle](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a><span data-ttu-id="5f2cf-190">Bir değişkende değerleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="5f2cf-190">Setting values in a variable</span></span>
<span data-ttu-id="5f2cf-191">Aşağıdaki resimde bir grafik runbook basit bir değere sahip bir değişken güncelleştirmek için örnek etkinliklerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-191">The following image shows sample activities to update a variable with a simple value in a graphical runbook.</span></span> <span data-ttu-id="5f2cf-192">Bu örnekte, tek bir Azure sanal makine ile alınan **Get-AzureRmVM** ve varolan bir Otomasyon değişkeni dize türünde bir bilgisayar adı kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-192">In this sample, a single Azure virtual machine is retrieved with **Get-AzureRmVM** and the computer name is saved to an existing Automation variable with a type of String.</span></span>  <span data-ttu-id="5f2cf-193">Önemli değildir olup olmadığını [bağlantıdır bir ardışık düzen veya dizisi](automation-graphical-authoring-intro.md#links-and-workflow) bu yana yalnızca tek bir nesne çıktıda bekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="5f2cf-193">It doesn't matter whether the [link is a pipeline or sequence](automation-graphical-authoring-intro.md#links-and-workflow) since we only expect a single object in the output.</span></span>

![Basit değişken Ayarla](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a><span data-ttu-id="5f2cf-195">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="5f2cf-195">Next Steps</span></span>

* <span data-ttu-id="5f2cf-196">Grafik yazma etkinlikleri birbirine bağlama hakkında daha fazla bilgi için bkz: [grafik yazma içindeki bağlantılar](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="5f2cf-196">To learn more about connecting activities together in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="5f2cf-197">Grafik runbook'ları kullanmaya başlamak için bkz. [İlk grafik runbook uygulamam](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="5f2cf-197">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span> 

