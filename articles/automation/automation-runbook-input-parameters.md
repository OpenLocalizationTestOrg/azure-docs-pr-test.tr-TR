---
title: "Runbook giriş parametreleri | Microsoft Docs"
description: "Runbook giriş parametreleri başlatıldığında bir runbook'a veri iletmek sağlayarak runbook'lar esnekliğini artırır. Bu makalede giriş parametreleri runbook'ları kullanıldığı farklı senaryolar anlatılmaktadır."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 4d3dff2c-1f55-498d-9a0e-eee497e5bedb
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: sngun
ms.openlocfilehash: 1ebf32338f5242e72eb2e2daa2da50d231f4b683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="runbook-input-parameters"></a><span data-ttu-id="b273e-104">Runbook giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="b273e-104">Runbook input parameters</span></span>
<span data-ttu-id="b273e-105">Runbook giriş parametreleri başlatıldığında veri ona geçirmek izin vererek runbook'lar esnekliğini artırır.</span><span class="sxs-lookup"><span data-stu-id="b273e-105">Runbook input parameters increase the flexibility of runbooks by allowing you to pass data to it when it is started.</span></span> <span data-ttu-id="b273e-106">Parametreleri runbook eylemlerin belirli senaryolar ve ortamlar için hedeflenen sağlar.</span><span class="sxs-lookup"><span data-stu-id="b273e-106">The parameters allow the runbook actions to be targeted for specific scenarios and environments.</span></span> <span data-ttu-id="b273e-107">Bu makalede, biz farklı senaryolar üzerinden giriş parametreleri runbook'ları kullanıldığı anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b273e-107">In this article, we will walk you through different scenarios where input parameters are used in runbooks.</span></span>

## <a name="configure-input-parameters"></a><span data-ttu-id="b273e-108">Giriş Parametrelerini Yapılandır</span><span class="sxs-lookup"><span data-stu-id="b273e-108">Configure input parameters</span></span>
<span data-ttu-id="b273e-109">Giriş parametreleri PowerShell, PowerShell iş akışı ve grafik runbook'lar yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="b273e-109">Input parameters can be configured in PowerShell, PowerShell Workflow, and graphical runbooks.</span></span> <span data-ttu-id="b273e-110">Bir runbook farklı veri türleriyle birden çok parametre ya da hiç parametre hiç olabilir.</span><span class="sxs-lookup"><span data-stu-id="b273e-110">A runbook can have multiple parameters with different data types, or no parameters at all.</span></span> <span data-ttu-id="b273e-111">Giriş parametreleri zorunlu veya isteğe bağlı olabilir ve isteğe bağlı parametreler için varsayılan bir değer atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b273e-111">Input parameters can be mandatory or optional, and you can assign a default value for optional parameters.</span></span> <span data-ttu-id="b273e-112">Kullanılabilir yöntemlerin biri aracılığıyla başlattığınızda, bir runbook'un giriş parametreleri için değerler atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b273e-112">You can assign values to the input parameters for a runbook when you start it through one of the available methods.</span></span> <span data-ttu-id="b273e-113">Bu yöntemler, portalı veya web hizmetinden bir runbook'u başlatma içerir.</span><span class="sxs-lookup"><span data-stu-id="b273e-113">These methods include starting  a runbook from the portal  or a web service.</span></span> <span data-ttu-id="b273e-114">Başka bir runbook'u satır içi olarak adlandırılan bir alt runbook'u olarak da başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b273e-114">You can also start one as a child runbook that is called inline in another runbook.</span></span>

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a><span data-ttu-id="b273e-115">Giriş parametreleri PowerShell ve PowerShell iş akışı runbook'ları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b273e-115">Configure input parameters in PowerShell and PowerShell Workflow runbooks</span></span>
<span data-ttu-id="b273e-116">PowerShell ve [PowerShell iş akışı runbook'ları](automation-first-runbook-textual.md) Azure Otomasyonu'nda aşağıdaki öznitelikler tanımlanan giriş parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="b273e-116">PowerShell and [PowerShell Workflow runbooks](automation-first-runbook-textual.md) in Azure Automation support input parameters that are defined through the following attributes.</span></span>  

| <span data-ttu-id="b273e-117">**Özellik**</span><span class="sxs-lookup"><span data-stu-id="b273e-117">**Property**</span></span> | <span data-ttu-id="b273e-118">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b273e-118">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="b273e-119">Tür</span><span class="sxs-lookup"><span data-stu-id="b273e-119">Type</span></span> |<span data-ttu-id="b273e-120">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="b273e-120">Required.</span></span> <span data-ttu-id="b273e-121">Parametre değeri beklenen veri türü.</span><span class="sxs-lookup"><span data-stu-id="b273e-121">The data type expected for the parameter value.</span></span> <span data-ttu-id="b273e-122">Herhangi bir .NET türü geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="b273e-122">Any .NET type is valid.</span></span> |
| <span data-ttu-id="b273e-123">Ad</span><span class="sxs-lookup"><span data-stu-id="b273e-123">Name</span></span> |<span data-ttu-id="b273e-124">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="b273e-124">Required.</span></span> <span data-ttu-id="b273e-125">Parametrenin adı.</span><span class="sxs-lookup"><span data-stu-id="b273e-125">The name of the parameter.</span></span> <span data-ttu-id="b273e-126">Bu gerekir runbook içinde benzersiz olmalıdır ve yalnızca harf, sayı içeren veya alt çizgi karakterleri.</span><span class="sxs-lookup"><span data-stu-id="b273e-126">This must be unique within the runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="b273e-127">Bir harf ile başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="b273e-127">It must start with a letter.</span></span> |
| <span data-ttu-id="b273e-128">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="b273e-128">Mandatory</span></span> |<span data-ttu-id="b273e-129">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="b273e-129">Optional.</span></span> <span data-ttu-id="b273e-130">Bir değer parametresi için sağlanan olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b273e-130">Specifies whether a value must be provided for the parameter.</span></span> <span data-ttu-id="b273e-131">Bu ayar, **$true**, sonra da runbook başlatılırken bir değer sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b273e-131">If you set this to **$true**, then a value must be provided when the runbook is started.</span></span> <span data-ttu-id="b273e-132">Bu ayar, **$false**, sonra da bir değer isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b273e-132">If you set this to **$false**, then a value is optional.</span></span> |
| <span data-ttu-id="b273e-133">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="b273e-133">Default value</span></span> |<span data-ttu-id="b273e-134">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="b273e-134">Optional.</span></span>  <span data-ttu-id="b273e-135">Runbook başlatılırken bir değer değil geçtiyse parametresi için kullanılan bir değeri belirtir.</span><span class="sxs-lookup"><span data-stu-id="b273e-135">Specifies a value that will be used for the parameter if a value is not passed in when the runbook is started.</span></span> <span data-ttu-id="b273e-136">Varsayılan değer otomatik olarak parametresi zorunlu ayarından bağımsız olarak isteğe bağlı hale getirir ve herhangi bir parametre için ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b273e-136">A default value can be set for any parameter and will automatically make the parameter optional regardless of the Mandatory setting.</span></span> |

<span data-ttu-id="b273e-137">Windows PowerShell giriş parametreleri burada doğrulama gibi diğer adlar, listelenenler ve parametre kümeleri çok daha fazla özniteliklerini destekler.</span><span class="sxs-lookup"><span data-stu-id="b273e-137">Windows PowerShell supports more attributes of input parameters than those listed here, like validation, aliases, and parameter sets.</span></span> <span data-ttu-id="b273e-138">Ancak, Azure Automation şu anda yalnızca yukarıda listelenen giriş parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="b273e-138">However, Azure Automation currently supports only the input parameters listed above.</span></span>

<span data-ttu-id="b273e-139">PowerShell iş akışı runbook'ları parametre tanımında burada birden çok parametre virgülle ayrılır aşağıdaki genel biçime sahiptir.</span><span class="sxs-lookup"><span data-stu-id="b273e-139">A parameter definition in PowerShell Workflow runbooks has the following general form, where multiple parameters are separated by commas.</span></span>

   ```
     Param
     (
         [Parameter (Mandatory= $true/$false)]
         [Type] Name1 = <Default value>,

         [Parameter (Mandatory= $true/$false)]
         [Type] Name2 = <Default value>
     )
   ```

> [!NOTE]
> <span data-ttu-id="b273e-140">Ne zaman tanımladığınız parametreler belirtmediyseniz **zorunlu** özniteliği sonra varsayılan olarak, parametre isteğe bağlı olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="b273e-140">When you're defining parameters, if you don’t specify the **Mandatory** attribute, then by default, the parameter is considered optional.</span></span> <span data-ttu-id="b273e-141">PowerShell iş akışı runbook'ları bir parametre için varsayılan bir değer ayarlarsanız, ayrıca, bu PowerShell tarafından isteğe bağlı bir parametre öğesinden bağımsız olarak kabul edilir **zorunlu** öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="b273e-141">Also, if you set a default value for a parameter in PowerShell Workflow runbooks, it will be treated by PowerShell as an optional parameter, regardless of the **Mandatory** attribute value.</span></span>
> 
> 

<span data-ttu-id="b273e-142">Örnek olarak, sanal makineler, tek bir VM veya bir kaynak grubundaki tüm sanal makineleri ayrıntılarını çıkarır bir PowerShell iş akışı runbook giriş parametreleri yapılandıralım.</span><span class="sxs-lookup"><span data-stu-id="b273e-142">As an example, let’s configure the input parameters for a PowerShell Workflow runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="b273e-143">Aşağıdaki ekran görüntüsünde gösterildiği gibi bu runbook iki parametreye sahiptir: adını sanal makine ve kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="b273e-143">This runbook has two parameters as shown in the following screenshot: the name of virtual machine and the name of the resource group.</span></span>

![Automation PowerShell iş akışı](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

<span data-ttu-id="b273e-145">Bu parametre tanımında parametreleri **$VMName** ve **$resourceGroupName** dize türünde basit parametreleridir.</span><span class="sxs-lookup"><span data-stu-id="b273e-145">In this parameter definition, the parameters **$VMName** and **$resourceGroupName** are simple parameters of type string.</span></span> <span data-ttu-id="b273e-146">Bununla birlikte, PowerShell ve PowerShell iş akışı runbook'ları tüm basit türleri ve karmaşık türler gibi destek **nesne** veya **PSCredential** giriş parametreleri için.</span><span class="sxs-lookup"><span data-stu-id="b273e-146">However, PowerShell and PowerShell Workflow runbooks support all simple types and complex types, such as **object** or **PSCredential** for input parameters.</span></span>

<span data-ttu-id="b273e-147">Runbook'unuz bir nesne türü giriş parametresi varsa, (adı, değer) içeren bir PowerShell hashtable kullanmak bir değer geçirmek için çiftleri.</span><span class="sxs-lookup"><span data-stu-id="b273e-147">If your runbook has an object type input parameter, then use a PowerShell hashtable with (name,value) pairs to pass in a value.</span></span> <span data-ttu-id="b273e-148">Örneğin, bir runbook'ta aşağıdaki parametre varsa:</span><span class="sxs-lookup"><span data-stu-id="b273e-148">For example, if you have the following parameter in a runbook:</span></span>

     [Parameter (Mandatory = $true)]
     [object] $FullName

<span data-ttu-id="b273e-149">Ardından parametresi şu değer geçirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b273e-149">Then you can pass the following value to the parameter:</span></span>

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a><span data-ttu-id="b273e-150">Giriş parametreleri grafik runbook'ları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b273e-150">Configure input parameters in graphical runbooks</span></span>
<span data-ttu-id="b273e-151">İçin [grafik runbook yapılandırma](automation-first-runbook-graphical.md) giriş parametreleri ile sanal makineleri ayrıntılarını ya da çıkarır bir grafik runbook tek bir VM veya bir kaynak grubundaki tüm sanal makineleri oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="b273e-151">To [configure a graphical runbook](automation-first-runbook-graphical.md) with input parameters, let’s create a graphical runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="b273e-152">Bir runbook yapılandırma, aşağıda açıklandığı gibi iki ana etkinliklerini oluşur.</span><span class="sxs-lookup"><span data-stu-id="b273e-152">Configuring a runbook consists of two major activities, as described below.</span></span>

<span data-ttu-id="b273e-153">[**Runbook'ları Azure farklı çalıştır hesabıyla kimlik doğrulaması** ](automation-sec-configure-azure-runas-account.md) Azure kimlik doğrulaması için.</span><span class="sxs-lookup"><span data-stu-id="b273e-153">[**Authenticate Runbooks with Azure Run As account**](automation-sec-configure-azure-runas-account.md) to authenticate with Azure.</span></span>

<span data-ttu-id="b273e-154">[**Get-AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) sanal makinelerin özellikleri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="b273e-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) to get the properties of a virtual machines.</span></span>

<span data-ttu-id="b273e-155">Kullanabileceğiniz [ **Write-Output** ](https://technet.microsoft.com/library/hh849921.aspx) sanal makinelerin adlarını çıktısını almak için etkinlik.</span><span class="sxs-lookup"><span data-stu-id="b273e-155">You can use the [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) activity to output the names of virtual machines.</span></span> <span data-ttu-id="b273e-156">Etkinlik **Get-AzureRmVm** iki parametre kabul eden **sanal makine adı** ve **kaynak grubu adı**.</span><span class="sxs-lookup"><span data-stu-id="b273e-156">The activity **Get-AzureRmVm** accepts two parameters, the **virtual machine name** and the **resource group name**.</span></span> <span data-ttu-id="b273e-157">Bu parametreler, runbook'u her başlattığınızda farklı değerler gerektirebilir olduğundan, giriş parametreleri runbook'a ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b273e-157">Since these parameters could require different values each time you start the runbook, you can add input parameters to your runbook.</span></span> <span data-ttu-id="b273e-158">Giriş parametreleri ekleme adımları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b273e-158">Here are the steps to add input parameters:</span></span>

1. <span data-ttu-id="b273e-159">Grafik runbook'tan seçin **Runbook'lar** dikey ve ardından [ **Düzenle** ](automation-graphical-authoring-intro.md) onu.</span><span class="sxs-lookup"><span data-stu-id="b273e-159">Select the graphical runbook from the **Runbooks** blade and then click [**Edit**](automation-graphical-authoring-intro.md) it.</span></span>
2. <span data-ttu-id="b273e-160">Runbook Düzenleyicisi'nden tıklatın **giriş ve çıkış** açmak için **giriş ve çıkış** dikey.</span><span class="sxs-lookup"><span data-stu-id="b273e-160">From the runbook editor, click **Input and output** to open the **Input and output** blade.</span></span>
   
    ![Otomasyon grafik runbook](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. <span data-ttu-id="b273e-162">**Giriş ve çıkış** dikey runbook için tanımlanan giriş parametreleri listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b273e-162">The **Input and output** blade displays a list of input parameters that are defined for the runbook.</span></span> <span data-ttu-id="b273e-163">Bu dikey penceresinde, yeni bir giriş parametresi eklemek veya var olan bir giriş parametresi yapılandırmasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="b273e-163">On this blade, you can either add a new input parameter or edit the configuration of an existing input parameter.</span></span> <span data-ttu-id="b273e-164">Runbook için yeni bir parametre eklemek için tıklatın **giriş Ekle** açmak için **Runbook giriş parametresi** dikey.</span><span class="sxs-lookup"><span data-stu-id="b273e-164">To add a new parameter for the runbook, click **Add input** to open the **Runbook input parameter** blade.</span></span> <span data-ttu-id="b273e-165">Burada, aşağıdaki parametreleri yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b273e-165">There, you can configure the following parameters:</span></span>
   
   | <span data-ttu-id="b273e-166">**Özellik**</span><span class="sxs-lookup"><span data-stu-id="b273e-166">**Property**</span></span> | <span data-ttu-id="b273e-167">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b273e-167">**Description**</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b273e-168">Ad</span><span class="sxs-lookup"><span data-stu-id="b273e-168">Name</span></span> |<span data-ttu-id="b273e-169">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="b273e-169">Required.</span></span>  <span data-ttu-id="b273e-170">Parametrenin adı.</span><span class="sxs-lookup"><span data-stu-id="b273e-170">The name of the parameter.</span></span> <span data-ttu-id="b273e-171">Bu gerekir runbook içinde benzersiz olmalıdır ve yalnızca harf, sayı içeren veya alt çizgi karakterleri.</span><span class="sxs-lookup"><span data-stu-id="b273e-171">This must be unique within the runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="b273e-172">Bir harf ile başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="b273e-172">It must start with a letter.</span></span> |
   | <span data-ttu-id="b273e-173">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b273e-173">Description</span></span> |<span data-ttu-id="b273e-174">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="b273e-174">Optional.</span></span> <span data-ttu-id="b273e-175">Giriş parametresi amacı hakkında açıklama.</span><span class="sxs-lookup"><span data-stu-id="b273e-175">Description about the purpose of input parameter.</span></span> |
   | <span data-ttu-id="b273e-176">Tür</span><span class="sxs-lookup"><span data-stu-id="b273e-176">Type</span></span> |<span data-ttu-id="b273e-177">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="b273e-177">Optional.</span></span> <span data-ttu-id="b273e-178">Parametre değeri beklenen veri türü.</span><span class="sxs-lookup"><span data-stu-id="b273e-178">The data type that's expected for the parameter value.</span></span> <span data-ttu-id="b273e-179">Desteklenen parametre türleri **dize**, **Int32**, **Int64**, **ondalık**, **Boolean**, **DateTime**, ve **nesne**.</span><span class="sxs-lookup"><span data-stu-id="b273e-179">Supported parameter types are **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime**, and **Object**.</span></span> <span data-ttu-id="b273e-180">Bir veri türü seçili değilse, varsayılan olarak **dize**.</span><span class="sxs-lookup"><span data-stu-id="b273e-180">If a data type is not selected, it defaults to **String**.</span></span> |
   | <span data-ttu-id="b273e-181">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="b273e-181">Mandatory</span></span> |<span data-ttu-id="b273e-182">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="b273e-182">Optional.</span></span> <span data-ttu-id="b273e-183">Bir değer parametresi için sağlanan olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b273e-183">Specifies whether a value must be provided for the parameter.</span></span> <span data-ttu-id="b273e-184">Seçerseniz **Evet**, sonra da runbook başlatılırken bir değer sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b273e-184">If you choose **yes**, then a value must be provided when the runbook is started.</span></span> <span data-ttu-id="b273e-185">Seçerseniz **hiçbir**, bir değer runbook başlatıldığında ve varsayılan bir değer ayarlanabilir gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="b273e-185">If you choose **no**, then a value is not required when the runbook is started, and a default value may be set.</span></span> |
   | <span data-ttu-id="b273e-186">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="b273e-186">Default Value</span></span> |<span data-ttu-id="b273e-187">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="b273e-187">Optional.</span></span> <span data-ttu-id="b273e-188">Runbook başlatılırken bir değer değil geçtiyse parametresi için kullanılan bir değeri belirtir.</span><span class="sxs-lookup"><span data-stu-id="b273e-188">Specifies a value that will be used for the parameter if a value is not passed in when the runbook is started.</span></span> <span data-ttu-id="b273e-189">Varsayılan değer, zorunlu olmayan bir parametre için ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="b273e-189">A default value can be set for a parameter that's not mandatory.</span></span> <span data-ttu-id="b273e-190">Varsayılan bir değer ayarlamak için seçin **özel**.</span><span class="sxs-lookup"><span data-stu-id="b273e-190">To set a default value, choose **Custom**.</span></span> <span data-ttu-id="b273e-191">Runbook başlatılırken başka bir değer sağlanmadığı sürece bu değer kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b273e-191">This value is used unless another value is provided when the runbook is started.</span></span> <span data-ttu-id="b273e-192">Seçin **hiçbiri** herhangi bir varsayılan değer sağlamak istemiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="b273e-192">Choose **None** if you don’t want to provide any default value.</span></span> |
   
    ![Yeni giriş Ekle](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. <span data-ttu-id="b273e-194">Tarafından kullanılan aşağıdaki özelliklere sahip iki parametre oluşturma **Get-AzureRmVm** etkinlik:</span><span class="sxs-lookup"><span data-stu-id="b273e-194">Create two parameters with the following properties that will be used by the **Get-AzureRmVm** activity:</span></span>
   
   * <span data-ttu-id="b273e-195">**Parametre1:**</span><span class="sxs-lookup"><span data-stu-id="b273e-195">**Parameter1:**</span></span>
     
     * <span data-ttu-id="b273e-196">Ad - VMName</span><span class="sxs-lookup"><span data-stu-id="b273e-196">Name - VMName</span></span>
     * <span data-ttu-id="b273e-197">-Dize türünde</span><span class="sxs-lookup"><span data-stu-id="b273e-197">Type - String</span></span>
     * <span data-ttu-id="b273e-198">Zorunlu - yok</span><span class="sxs-lookup"><span data-stu-id="b273e-198">Mandatory - No</span></span>
   * <span data-ttu-id="b273e-199">**Parametre2:**</span><span class="sxs-lookup"><span data-stu-id="b273e-199">**Parameter2:**</span></span>
     
     * <span data-ttu-id="b273e-200">Ad - resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="b273e-200">Name - resourceGroupName</span></span>
     * <span data-ttu-id="b273e-201">-Dize türünde</span><span class="sxs-lookup"><span data-stu-id="b273e-201">Type - String</span></span>
     * <span data-ttu-id="b273e-202">Zorunlu - yok</span><span class="sxs-lookup"><span data-stu-id="b273e-202">Mandatory - No</span></span>
     * <span data-ttu-id="b273e-203">Varsayılan değer - özel</span><span class="sxs-lookup"><span data-stu-id="b273e-203">Default value - Custom</span></span>
     * <span data-ttu-id="b273e-204">Özel varsayılan değer - \<sanal makineleri içeren kaynak grubu adı ></span><span class="sxs-lookup"><span data-stu-id="b273e-204">Custom default value - \<Name of the resource group that contains the virtual machines></span></span>
5. <span data-ttu-id="b273e-205">Parametreleri ekledikten sonra tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="b273e-205">Once you add the parameters, click **OK**.</span></span>  <span data-ttu-id="b273e-206">Bunları artık görüntüleyebilirsiniz **giriş ve çıkış dikey**.</span><span class="sxs-lookup"><span data-stu-id="b273e-206">You can now view them in the **Input and output blade**.</span></span> <span data-ttu-id="b273e-207">Tıklatın **Tamam** yeniden ve ardından **kaydetmek** ve **Yayımla** runbook'unuz.</span><span class="sxs-lookup"><span data-stu-id="b273e-207">Click **OK** again, and then click **Save** and **Publish** your runbook.</span></span>

## <a name="assign-values-to-input-parameters-in-runbooks"></a><span data-ttu-id="b273e-208">Giriş runbook parametreleri için değerleri atayın</span><span class="sxs-lookup"><span data-stu-id="b273e-208">Assign values to input parameters in runbooks</span></span>
<span data-ttu-id="b273e-209">Giriş aşağıdaki senaryolarda runbook parametreleri için değerleri geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b273e-209">You can pass values to input parameters in runbooks in the following scenarios.</span></span>

### <a name="start-a-runbook-and-assign-parameters"></a><span data-ttu-id="b273e-210">Bir runbook başlatın ve parametreleri atayın</span><span class="sxs-lookup"><span data-stu-id="b273e-210">Start a runbook and assign parameters</span></span>
<span data-ttu-id="b273e-211">Bir runbook birçok yolu başlatılabilir: bir Web kancası ile PowerShell cmdlet'leri ile REST API ile veya SDK'sı Azure Portalı aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="b273e-211">A runbook can be started many ways: through the Azure portal, with a webhook, with PowerShell cmdlets, with the REST API, or with the SDK.</span></span> <span data-ttu-id="b273e-212">Aşağıda bir runbook'u başlatma ve parametreleri atamak için farklı yöntemler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b273e-212">Below we discuss different methods for starting a runbook and assigning parameters.</span></span>

#### <a name="start-a-published-runbook-by-using-the-azure-portal-and-assign-parameters"></a><span data-ttu-id="b273e-213">Azure portalını kullanarak yayımlanan bir runbook başlatın ve parametreleri atayın</span><span class="sxs-lookup"><span data-stu-id="b273e-213">Start a published runbook by using the Azure portal and assign parameters</span></span>
<span data-ttu-id="b273e-214">Olduğunda, [runbook'u başlatmak](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), **Runbook'u Başlat** dikey penceresi açılır ve yeni oluşturduğunuz parametre değerlerini yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b273e-214">When you [start the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), the **Start Runbook** blade opens and you can configure values for the parameters that you just created.</span></span>

![Portalı kullanmaya başlama](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

<span data-ttu-id="b273e-216">Giriş kutusuna altındaki etiketinde parametresi için belirlenen öznitelikleri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b273e-216">In the label beneath the input box, you can see the attributes that have been set for the parameter.</span></span> <span data-ttu-id="b273e-217">Öznitelikler, zorunlu veya isteğe bağlı, türü ve varsayılan değeri içerir.</span><span class="sxs-lookup"><span data-stu-id="b273e-217">Attributes include mandatory or optional, type, and  default value.</span></span> <span data-ttu-id="b273e-218">Parametre adının yanındaki Yardım balonu parametre giriş değerleri hakkında kararlar gereken tüm anahtar bilgileri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b273e-218">In the help balloon next to the parameter name, you can see all the key information you need to make decisions about parameter input values.</span></span> <span data-ttu-id="b273e-219">Bir parametre zorunlu veya isteğe bağlı olup, bu bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="b273e-219">This information includes whether a parameter is mandatory or optional.</span></span> <span data-ttu-id="b273e-220">Ayrıca, türü ve varsayılan değer (varsa) ve diğer yararlı notlar içerir.</span><span class="sxs-lookup"><span data-stu-id="b273e-220">It also includes the type and default value (if any), and other helpful notes.</span></span>

![Yardım balonu](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> <span data-ttu-id="b273e-222">Dize türü parametreleri desteği **boş** dize değerleri.</span><span class="sxs-lookup"><span data-stu-id="b273e-222">String type parameters support **Empty** String values.</span></span>  <span data-ttu-id="b273e-223">Girme **[oluşması]** giriş parametresinde kutusu boş bir dize parametresi geçer.</span><span class="sxs-lookup"><span data-stu-id="b273e-223">Entering **[EmptyString]** in the input parameter box will pass an empty string to the parameter.</span></span> <span data-ttu-id="b273e-224">Ayrıca, dize türü parametreleri desteklemeyen **Null** geçirilen değerleri.</span><span class="sxs-lookup"><span data-stu-id="b273e-224">Also, String type parameters don’t support **Null** values being passed.</span></span> <span data-ttu-id="b273e-225">Ardından PowerShell herhangi bir değer dizesi parametresi geçirmezseniz boş olarak görürler.</span><span class="sxs-lookup"><span data-stu-id="b273e-225">If you don’t pass any value to the String parameter, then PowerShell will interpret it as null.</span></span>
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a><span data-ttu-id="b273e-226">Yayımlanan bir runbook'ta PowerShell cmdlet'lerini kullanarak başlatmak ve parametreleri atayın</span><span class="sxs-lookup"><span data-stu-id="b273e-226">Start a published runbook by using PowerShell cmdlets and assign parameters</span></span>
* <span data-ttu-id="b273e-227">**Azure Resource Manager cmdlet'lerini:** bir kaynak grubunda kullanılarak oluşturulmuş bir Otomasyon runbook'u başlatabilirsiniz [başlangıç AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span><span class="sxs-lookup"><span data-stu-id="b273e-227">**Azure Resource Manager cmdlets:** You can start an Automation runbook that was created in a resource group by using [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span></span>
  
  <span data-ttu-id="b273e-228">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="b273e-228">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* <span data-ttu-id="b273e-229">**Azure Hizmet Yönetimi cmdlet'lerini:** bir varsayılan kaynak grubunda kullanılarak oluşturulmuş bir Otomasyon runbook'u başlatabilirsiniz [başlangıç AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span><span class="sxs-lookup"><span data-stu-id="b273e-229">**Azure Service Management cmdlets:** You can start an automation runbook that was created in a default resource group by using [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span></span>
  
  <span data-ttu-id="b273e-230">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="b273e-230">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> <span data-ttu-id="b273e-231">PowerShell cmdlet'lerini, varsayılan parametre kullanarak bir runbook'u başlattığınızda **MicrosoftApplicationManagementStartedBy** değeri ile oluşturulan **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b273e-231">When you start a runbook by using PowerShell cmdlets, a default parameter, **MicrosoftApplicationManagementStartedBy** is created with the value **PowerShell**.</span></span> <span data-ttu-id="b273e-232">Bu parametrede görüntüleyebilirsiniz **iş ayrıntıları** dikey.</span><span class="sxs-lookup"><span data-stu-id="b273e-232">You can view this parameter in the **Job details** blade.</span></span>  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a><span data-ttu-id="b273e-233">Bir SDK kullanarak bir runbook'u başlatmak ve parametreleri atayın</span><span class="sxs-lookup"><span data-stu-id="b273e-233">Start a runbook by using an SDK and assign parameters</span></span>
* <span data-ttu-id="b273e-234">**Azure Resource Manager yöntemi:** bir programlama dili SDK'yi kullanarak bir runbook'u başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b273e-234">**Azure Resource Manager method:** You can start a runbook by using the SDK of a programming language.</span></span> <span data-ttu-id="b273e-235">Otomasyon hesabınızda bir runbook'u başlatmak için C# kod parçacığı aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="b273e-235">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="b273e-236">Tüm koda görüntüleyebilirsiniz bizim [GitHub deposunu](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="b273e-236">You can view all the code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>  
  
  ```
   public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
      {
        var response = AutomationClient.Jobs.Create(resourceGroupName, automationAccount, new JobCreateParameters
         {
            Properties = new JobCreateProperties
             {
                Runbook = new RunbookAssociationProperty
                 {
                   Name = runbookName
                 },
                   Parameters = parameters
             }
         });
      return response.Job;
      }
  ```
* <span data-ttu-id="b273e-237">**Azure hizmet yönetimi yöntemi:** bir programlama dili SDK'yi kullanarak bir runbook'u başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b273e-237">**Azure Service Management method:** You can start a runbook by using the SDK of a programming language.</span></span> <span data-ttu-id="b273e-238">Otomasyon hesabınızda bir runbook'u başlatmak için C# kod parçacığı aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="b273e-238">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="b273e-239">Tüm koda görüntüleyebilirsiniz bizim [GitHub deposunu](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="b273e-239">You can view all the code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>
  
  ```      
  public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
    {
      var response = AutomationClient.Jobs.Create(automationAccount, new JobCreateParameters
    {
      Properties = new JobCreateProperties
         {
           Runbook = new RunbookAssociationProperty
         {
           Name = runbookName
              },
                Parameters = parameters
              }
       });
      return response.Job;
    }
  ```
  
  <span data-ttu-id="b273e-240">Bu yöntem başlatmak için runbook parametreleri depolamak için Sözlük oluşturma **VMName** ve **resourceGroupName**ve değerleri.</span><span class="sxs-lookup"><span data-stu-id="b273e-240">To start this method, create a dictionary to store the runbook parameters, **VMName** and  **resourceGroupName**, and their values.</span></span> <span data-ttu-id="b273e-241">Daha sonra runbook'u başlatın.</span><span class="sxs-lookup"><span data-stu-id="b273e-241">Then start the runbook.</span></span> <span data-ttu-id="b273e-242">Yukarıda tanımlanan yöntemi çağırmak için C# kod parçacığı aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b273e-242">Below is the C# code snippet for calling the method that's defined above.</span></span>
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters to the dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call the StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-the-rest-api-and-assign-parameters"></a><span data-ttu-id="b273e-243">REST API kullanarak bir runbook'u başlatmak ve parametreleri atayın</span><span class="sxs-lookup"><span data-stu-id="b273e-243">Start a runbook by using the REST API and assign parameters</span></span>
<span data-ttu-id="b273e-244">Bir runbook işi oluşturulur ve kullanarak Azure Otomasyon REST API'si ile çalışmaya **PUT** yöntemi aşağıdaki istek URI'si ile.</span><span class="sxs-lookup"><span data-stu-id="b273e-244">A runbook job can be created and started with the Azure Automation REST API by using the **PUT** method with the following request URI.</span></span>

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

<span data-ttu-id="b273e-245">İstek URI'si aşağıdaki parametreleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b273e-245">In the request URI, replace the following parameters:</span></span>

* <span data-ttu-id="b273e-246">**Abonelik kimliği:** Azure abonelik kimliğinizi</span><span class="sxs-lookup"><span data-stu-id="b273e-246">**subscription-id:** Your Azure subscription ID.</span></span>  
* <span data-ttu-id="b273e-247">**Bulut hizmet adı:** bulut adını hizmet isteği hangi gönderilmelidir için.</span><span class="sxs-lookup"><span data-stu-id="b273e-247">**cloud-service-name:** The name of the cloud service to which the request should be sent.</span></span>  
* <span data-ttu-id="b273e-248">**Otomasyon hesabı adı:** içinde belirtilen bulut hizmeti barındırılan Otomasyon hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="b273e-248">**automation-account-name:** The name of your automation account that's hosted within the specified cloud service.</span></span>  
* <span data-ttu-id="b273e-249">**İş Kimliği:** iş için GUID.</span><span class="sxs-lookup"><span data-stu-id="b273e-249">**job-id:** The GUID for the job.</span></span> <span data-ttu-id="b273e-250">PowerShell'de GUID'ler kullanarak oluşturulabilir **[GUID]::NewGuid(). ToString()** komutu.</span><span class="sxs-lookup"><span data-stu-id="b273e-250">GUIDs in PowerShell can be created by using the **[GUID]::NewGuid().ToString()** command.</span></span>

<span data-ttu-id="b273e-251">Runbook işi parametreleri geçirmek için istek gövdesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b273e-251">In order to pass parameters to the runbook job, use the request body.</span></span> <span data-ttu-id="b273e-252">JSON biçiminde sağlanan aşağıdaki iki özelliklerini alır:</span><span class="sxs-lookup"><span data-stu-id="b273e-252">It takes the following two properties provided in JSON format:</span></span>

* <span data-ttu-id="b273e-253">**Runbook adı:** gerekli.</span><span class="sxs-lookup"><span data-stu-id="b273e-253">**Runbook name:** Required.</span></span> <span data-ttu-id="b273e-254">Runbook başlatma işinin adıdır.</span><span class="sxs-lookup"><span data-stu-id="b273e-254">The name of the runbook for the job to start.</span></span>  
* <span data-ttu-id="b273e-255">**Runbook parametreleri:** isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="b273e-255">**Runbook parameters:** Optional.</span></span> <span data-ttu-id="b273e-256">(Adı, değer) parametre listesinde sözlüğü biçiminde burada adı dize türünde olmalıdır ve değer geçerli bir JSON değeri olabilir.</span><span class="sxs-lookup"><span data-stu-id="b273e-256">A dictionary of the parameter list in (name, value) format where name should be of String type and value can be any valid JSON value.</span></span>

<span data-ttu-id="b273e-257">Başlatmak istiyorsanız **Get-AzureVMTextual** daha önce oluşturulmuş runbook **VMName** ve **resourceGroupName** parametre olarak istek gövdesi için şu JSON biçimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b273e-257">If you want to start the **Get-AzureVMTextual** runbook that was created earlier with **VMName** and **resourceGroupName** as parameters, use the following JSON format for the request body.</span></span>

   ```
    {
      "properties":{
        "runbook":{
        "name":"Get-AzureVMTextual"},
      "parameters":{
         "VMName":"WSVMClassic",
         "resourceGroupName":”WSCS1”}
        }
    }
   ```

<span data-ttu-id="b273e-258">İş başarıyla oluşturulduysa 201 HTTP durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="b273e-258">A HTTP status code 201 is returned if the job is successfully created.</span></span> <span data-ttu-id="b273e-259">Yanıt Üstbilgileri ve yanıt gövdesi hakkında daha fazla bilgi için ilgili makaleye başvurun [REST API kullanarak bir runbook işi oluşturun.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span><span class="sxs-lookup"><span data-stu-id="b273e-259">For more information on response headers and the response body, refer to the article about how to [create a runbook job by using the REST API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span></span>

### <a name="test-a-runbook-and-assign-parameters"></a><span data-ttu-id="b273e-260">Bir runbook'u test ve parametreleri atayın</span><span class="sxs-lookup"><span data-stu-id="b273e-260">Test a runbook and assign parameters</span></span>
<span data-ttu-id="b273e-261">Olduğunda, [, runbook'un taslak sürümünü test](automation-testing-runbook.md) test seçeneğini kullanarak **Test** dikey penceresi açılır ve yeni oluşturduğunuz parametre değerlerini yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b273e-261">When you [test the draft version of your runbook](automation-testing-runbook.md) by using the test option, the **Test** blade opens and you can configure values for the parameters that you just created.</span></span>

![Test ve ata parametreleri](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-to-a-runbook-and-assign-parameters"></a><span data-ttu-id="b273e-263">Bir zamanlamayı runbook'a bağlamak ve parametreleri atayın</span><span class="sxs-lookup"><span data-stu-id="b273e-263">Link a schedule to a runbook and assign parameters</span></span>
<span data-ttu-id="b273e-264">Yapabilecekleriniz [bir zamanlama Bağla](automation-schedules.md) runbook'unuzu için böylece runbook belirli bir zamanda başlatır.</span><span class="sxs-lookup"><span data-stu-id="b273e-264">You can [link a schedule](automation-schedules.md) to your runbook so that the runbook starts at a specific time.</span></span> <span data-ttu-id="b273e-265">Giriş parametreleri, zamanlamayı oluşturduğunuzda ve runbook zamanlama tarafından başlatıldığında bu değerleri kullanacağı atayın.</span><span class="sxs-lookup"><span data-stu-id="b273e-265">You assign input parameters when you create the schedule, and the runbook will use these values when it is started by the schedule.</span></span> <span data-ttu-id="b273e-266">Tüm zorunlu parametre değerleri sağlanana kadar zamanlaması kaydedilemiyor.</span><span class="sxs-lookup"><span data-stu-id="b273e-266">You can’t save the schedule until all mandatory parameter values are provided.</span></span>

![Zamanlama ve parametreleri atama](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a><span data-ttu-id="b273e-268">Bir runbook için bir Web kancası oluşturun ve parametreleri atayın</span><span class="sxs-lookup"><span data-stu-id="b273e-268">Create a webhook for a runbook and assign parameters</span></span>
<span data-ttu-id="b273e-269">Oluşturabileceğiniz bir [Web kancası](automation-webhooks.md) runbook'unuzu için ve runbook giriş parametreleri yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b273e-269">You can create a [webhook](automation-webhooks.md) for your runbook and configure runbook input parameters.</span></span> <span data-ttu-id="b273e-270">Tüm zorunlu parametre değerleri sağlanana kadar Web kancası kaydedilemiyor.</span><span class="sxs-lookup"><span data-stu-id="b273e-270">You can’t save the webhook until all mandatory parameter values are provided.</span></span>

![Web kancası oluşturun ve parametreleri atayın](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

<span data-ttu-id="b273e-272">Bir Web kancası, önceden tanımlanmış giriş parametresi kullanılarak bir runbook yürütülürken  **[Webhookdata](automation-webhooks.md#details-of-a-webhook)**  tanımlanan giriş parametreleri birlikte gönderilir.</span><span class="sxs-lookup"><span data-stu-id="b273e-272">When you execute a runbook by using a webhook, the predefined input parameter **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** is sent, along with the input parameters that you defined.</span></span> <span data-ttu-id="b273e-273">Genişletmek için tıklatın **WebhookData** daha fazla ayrıntı için parametre.</span><span class="sxs-lookup"><span data-stu-id="b273e-273">You can click to expand the **WebhookData** parameter for more details.</span></span>

![WebhookData parametresi](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a><span data-ttu-id="b273e-275">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b273e-275">Next steps</span></span>
* <span data-ttu-id="b273e-276">Runbook giriş ve çıkış hakkında daha fazla bilgi için bkz: [Azure Automation: runbook giriş, çıkış ve iç içe runbook](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span><span class="sxs-lookup"><span data-stu-id="b273e-276">For more information on runbook input and output, see [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span></span>
* <span data-ttu-id="b273e-277">Bir runbook'u başlatmak için çeşitli yollar hakkında daha fazla ayrıntı için bkz: [runbook başlatma](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="b273e-277">For details about different ways to start a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="b273e-278">Bir metinsel runbook'u düzenlemek için başvurmak [metinsel runbook'ları düzenleme](automation-edit-textual-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="b273e-278">To edit a textual runbook, refer to [Editing textual runbooks](automation-edit-textual-runbook.md).</span></span>
* <span data-ttu-id="b273e-279">Bir grafik runbook'u düzenlemek için başvurmak [Azure Automation'da grafik yazma](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="b273e-279">To edit a graphical runbook, refer to [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

