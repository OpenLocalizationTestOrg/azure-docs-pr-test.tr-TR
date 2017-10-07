---
title: "aaaRunbook giriş parametreleri | Microsoft Docs"
description: "Runbook giriş parametreleri başlatıldığında toopass veri tooa runbook sağlayarak runbook'ların hello esnekliğini artırır. Bu makalede giriş parametreleri runbook'ları kullanıldığı farklı senaryolar anlatılmaktadır."
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
ms.openlocfilehash: f3abaf92382e7d41019616bafb14af23cf98dd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-input-parameters"></a><span data-ttu-id="3f282-104">Runbook giriş parametreleri</span><span class="sxs-lookup"><span data-stu-id="3f282-104">Runbook input parameters</span></span>
<span data-ttu-id="3f282-105">Runbook giriş parametreleri başlatıldığında toopass veri tooit sağlayarak runbook'ların hello esnekliğini artırır.</span><span class="sxs-lookup"><span data-stu-id="3f282-105">Runbook input parameters increase hello flexibility of runbooks by allowing you toopass data tooit when it is started.</span></span> <span data-ttu-id="3f282-106">Merhaba parametreler belirli senaryolar ve ortamlar için hedeflenen hello runbook eylemleri toobe olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="3f282-106">hello parameters allow hello runbook actions toobe targeted for specific scenarios and environments.</span></span> <span data-ttu-id="3f282-107">Bu makalede, biz farklı senaryolar üzerinden giriş parametreleri runbook'ları kullanıldığı anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3f282-107">In this article, we will walk you through different scenarios where input parameters are used in runbooks.</span></span>

## <a name="configure-input-parameters"></a><span data-ttu-id="3f282-108">Giriş Parametrelerini Yapılandır</span><span class="sxs-lookup"><span data-stu-id="3f282-108">Configure input parameters</span></span>
<span data-ttu-id="3f282-109">Giriş parametreleri PowerShell, PowerShell iş akışı ve grafik runbook'lar yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="3f282-109">Input parameters can be configured in PowerShell, PowerShell Workflow, and graphical runbooks.</span></span> <span data-ttu-id="3f282-110">Bir runbook farklı veri türleriyle birden çok parametre ya da hiç parametre hiç olabilir.</span><span class="sxs-lookup"><span data-stu-id="3f282-110">A runbook can have multiple parameters with different data types, or no parameters at all.</span></span> <span data-ttu-id="3f282-111">Giriş parametreleri zorunlu veya isteğe bağlı olabilir ve isteğe bağlı parametreler için varsayılan bir değer atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f282-111">Input parameters can be mandatory or optional, and you can assign a default value for optional parameters.</span></span> <span data-ttu-id="3f282-112">Merhaba kullanılabilir yöntemlerin biri aracılığıyla başlattığınızda, bir runbook'un giriş parametreleri toohello değerler atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f282-112">You can assign values toohello input parameters for a runbook when you start it through one of hello available methods.</span></span> <span data-ttu-id="3f282-113">Bu yöntemler, bir runbook hello portalı veya web hizmeti başlatılıyor içerir.</span><span class="sxs-lookup"><span data-stu-id="3f282-113">These methods include starting  a runbook from hello portal  or a web service.</span></span> <span data-ttu-id="3f282-114">Başka bir runbook'u satır içi olarak adlandırılan bir alt runbook'u olarak da başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f282-114">You can also start one as a child runbook that is called inline in another runbook.</span></span>

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a><span data-ttu-id="3f282-115">Giriş parametreleri PowerShell ve PowerShell iş akışı runbook'ları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3f282-115">Configure input parameters in PowerShell and PowerShell Workflow runbooks</span></span>
<span data-ttu-id="3f282-116">PowerShell ve [PowerShell iş akışı runbook'ları](automation-first-runbook-textual.md) Azure Otomasyonu'nda öznitelikleri aşağıdaki hello tanımlanan giriş parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="3f282-116">PowerShell and [PowerShell Workflow runbooks](automation-first-runbook-textual.md) in Azure Automation support input parameters that are defined through hello following attributes.</span></span>  

| <span data-ttu-id="3f282-117">**Özellik**</span><span class="sxs-lookup"><span data-stu-id="3f282-117">**Property**</span></span> | <span data-ttu-id="3f282-118">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="3f282-118">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="3f282-119">Tür</span><span class="sxs-lookup"><span data-stu-id="3f282-119">Type</span></span> |<span data-ttu-id="3f282-120">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="3f282-120">Required.</span></span> <span data-ttu-id="3f282-121">Merhaba veri türü için Hello parametre değeri bekleniyor.</span><span class="sxs-lookup"><span data-stu-id="3f282-121">hello data type expected for hello parameter value.</span></span> <span data-ttu-id="3f282-122">Herhangi bir .NET türü geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="3f282-122">Any .NET type is valid.</span></span> |
| <span data-ttu-id="3f282-123">Ad</span><span class="sxs-lookup"><span data-stu-id="3f282-123">Name</span></span> |<span data-ttu-id="3f282-124">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="3f282-124">Required.</span></span> <span data-ttu-id="3f282-125">Merhaba parametresinin Hello adı.</span><span class="sxs-lookup"><span data-stu-id="3f282-125">hello name of hello parameter.</span></span> <span data-ttu-id="3f282-126">Bu gerekir hello runbook içinde benzersiz olmalıdır ve yalnızca harf, sayı içeren veya alt çizgi karakterleri.</span><span class="sxs-lookup"><span data-stu-id="3f282-126">This must be unique within hello runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="3f282-127">Bir harf ile başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="3f282-127">It must start with a letter.</span></span> |
| <span data-ttu-id="3f282-128">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="3f282-128">Mandatory</span></span> |<span data-ttu-id="3f282-129">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="3f282-129">Optional.</span></span> <span data-ttu-id="3f282-130">Bir değer hello parametresi için sağlanan olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="3f282-130">Specifies whether a value must be provided for hello parameter.</span></span> <span data-ttu-id="3f282-131">Bu çok ayarlarsanız,**$true**, sonra da hello runbook başlatılırken bir değer sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3f282-131">If you set this too**$true**, then a value must be provided when hello runbook is started.</span></span> <span data-ttu-id="3f282-132">Bu çok ayarlarsanız,**$false**, sonra da bir değer isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="3f282-132">If you set this too**$false**, then a value is optional.</span></span> |
| <span data-ttu-id="3f282-133">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="3f282-133">Default value</span></span> |<span data-ttu-id="3f282-134">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="3f282-134">Optional.</span></span>  <span data-ttu-id="3f282-135">Merhaba runbook başlatılırken bir değer değil geçtiyse hello parametresi için kullanılan bir değeri belirtir.</span><span class="sxs-lookup"><span data-stu-id="3f282-135">Specifies a value that will be used for hello parameter if a value is not passed in when hello runbook is started.</span></span> <span data-ttu-id="3f282-136">Varsayılan değer otomatik olarak hello parametre hello zorunlu ayarı bağımsız olarak isteğe bağlı hale getirir ve herhangi bir parametre için ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f282-136">A default value can be set for any parameter and will automatically make hello parameter optional regardless of hello Mandatory setting.</span></span> |

<span data-ttu-id="3f282-137">Windows PowerShell giriş parametreleri burada doğrulama gibi diğer adlar, listelenenler ve parametre kümeleri çok daha fazla özniteliklerini destekler.</span><span class="sxs-lookup"><span data-stu-id="3f282-137">Windows PowerShell supports more attributes of input parameters than those listed here, like validation, aliases, and parameter sets.</span></span> <span data-ttu-id="3f282-138">Ancak, Azure Automation şu anda yukarıda listelenen yalnızca hello giriş parametreleri destekler.</span><span class="sxs-lookup"><span data-stu-id="3f282-138">However, Azure Automation currently supports only hello input parameters listed above.</span></span>

<span data-ttu-id="3f282-139">PowerShell iş akışı runbook'ları bir parametre tanımı burada birden çok parametre virgülle ayrılır genel form, aşağıdaki hello içeriyor.</span><span class="sxs-lookup"><span data-stu-id="3f282-139">A parameter definition in PowerShell Workflow runbooks has hello following general form, where multiple parameters are separated by commas.</span></span>

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
> <span data-ttu-id="3f282-140">Ne zaman tanımladığınız parametreler hello belirtmezseniz **zorunlu** özniteliği sonra varsayılan olarak, hello parametre isteğe bağlı olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="3f282-140">When you're defining parameters, if you don’t specify hello **Mandatory** attribute, then by default, hello parameter is considered optional.</span></span> <span data-ttu-id="3f282-141">PowerShell iş akışı runbook'ları bir parametre için varsayılan bir değer ayarlarsanız, ayrıca, bu PowerShell tarafından hello bağımsız olarak isteğe bağlı bir parametre olarak kabul edilecek **zorunlu** öznitelik değeri.</span><span class="sxs-lookup"><span data-stu-id="3f282-141">Also, if you set a default value for a parameter in PowerShell Workflow runbooks, it will be treated by PowerShell as an optional parameter, regardless of hello **Mandatory** attribute value.</span></span>
> 
> 

<span data-ttu-id="3f282-142">Örnek olarak, sanal makineler, tek bir VM veya bir kaynak grubundaki tüm sanal makineleri ayrıntılarını çıkarır bir PowerShell iş akışı runbook giriş parametreleri hello yapılandıralım.</span><span class="sxs-lookup"><span data-stu-id="3f282-142">As an example, let’s configure hello input parameters for a PowerShell Workflow runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="3f282-143">Bu runbook hello ekran aşağıdaki gösterildiği gibi iki parametreye sahiptir: sanal makine ve hello hello kaynak grubunun adını hello adı.</span><span class="sxs-lookup"><span data-stu-id="3f282-143">This runbook has two parameters as shown in hello following screenshot: hello name of virtual machine and hello name of hello resource group.</span></span>

![Automation PowerShell iş akışı](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

<span data-ttu-id="3f282-145">Bu parametre tanımında parametreleri hello **$VMName** ve **$resourceGroupName** dize türünde basit parametreleridir.</span><span class="sxs-lookup"><span data-stu-id="3f282-145">In this parameter definition, hello parameters **$VMName** and **$resourceGroupName** are simple parameters of type string.</span></span> <span data-ttu-id="3f282-146">Bununla birlikte, PowerShell ve PowerShell iş akışı runbook'ları tüm basit türleri ve karmaşık türler gibi destek **nesne** veya **PSCredential** giriş parametreleri için.</span><span class="sxs-lookup"><span data-stu-id="3f282-146">However, PowerShell and PowerShell Workflow runbooks support all simple types and complex types, such as **object** or **PSCredential** for input parameters.</span></span>

<span data-ttu-id="3f282-147">Runbook'unuz bir nesne türü giriş parametresi varsa, sonra kullanın (adı, değer) içeren bir PowerShell hashtable toopass bir değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="3f282-147">If your runbook has an object type input parameter, then use a PowerShell hashtable with (name,value) pairs toopass in a value.</span></span> <span data-ttu-id="3f282-148">Örneğin, bir runbook'ta parametresi aşağıdaki hello varsa:</span><span class="sxs-lookup"><span data-stu-id="3f282-148">For example, if you have hello following parameter in a runbook:</span></span>

     [Parameter (Mandatory = $true)]
     [object] $FullName

<span data-ttu-id="3f282-149">Ardından değer toohello parametresi aşağıdaki hello geçirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3f282-149">Then you can pass hello following value toohello parameter:</span></span>

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a><span data-ttu-id="3f282-150">Giriş parametreleri grafik runbook'ları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3f282-150">Configure input parameters in graphical runbooks</span></span>
<span data-ttu-id="3f282-151">çok[grafik runbook yapılandırma](automation-first-runbook-graphical.md) giriş parametreleri ile sanal makineleri ayrıntılarını ya da çıkarır bir grafik runbook tek bir VM veya bir kaynak grubundaki tüm sanal makineleri oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="3f282-151">too[configure a graphical runbook](automation-first-runbook-graphical.md) with input parameters, let’s create a graphical runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="3f282-152">Bir runbook yapılandırma, aşağıda açıklandığı gibi iki ana etkinliklerini oluşur.</span><span class="sxs-lookup"><span data-stu-id="3f282-152">Configuring a runbook consists of two major activities, as described below.</span></span>

<span data-ttu-id="3f282-153">[**Runbook'ları Azure farklı çalıştır hesabıyla kimlik doğrulaması** ](automation-sec-configure-azure-runas-account.md) tooauthenticate Azure ile.</span><span class="sxs-lookup"><span data-stu-id="3f282-153">[**Authenticate Runbooks with Azure Run As account**](automation-sec-configure-azure-runas-account.md) tooauthenticate with Azure.</span></span>

<span data-ttu-id="3f282-154">[**Get-AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) sanal makinelerin tooget hello özellikleri.</span><span class="sxs-lookup"><span data-stu-id="3f282-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) tooget hello properties of a virtual machines.</span></span>

<span data-ttu-id="3f282-155">Merhaba kullanabilirsiniz [ **Write-Output** ](https://technet.microsoft.com/library/hh849921.aspx) etkinlik toooutput hello adlarını sanal makinelerin.</span><span class="sxs-lookup"><span data-stu-id="3f282-155">You can use hello [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) activity toooutput hello names of virtual machines.</span></span> <span data-ttu-id="3f282-156">Merhaba etkinlik **Get-AzureRmVm** iki parametre hello kabul **sanal makine adı** ve hello **kaynak grubu adı**.</span><span class="sxs-lookup"><span data-stu-id="3f282-156">hello activity **Get-AzureRmVm** accepts two parameters, hello **virtual machine name** and hello **resource group name**.</span></span> <span data-ttu-id="3f282-157">Bu parametreler hello runbook her başlattığınızda farklı değerler gerektirebilir olduğundan, giriş parametreleri tooyour runbook ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f282-157">Since these parameters could require different values each time you start hello runbook, you can add input parameters tooyour runbook.</span></span> <span data-ttu-id="3f282-158">Merhaba adımları tooadd giriş parametreleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3f282-158">Here are hello steps tooadd input parameters:</span></span>

1. <span data-ttu-id="3f282-159">Select hello hello grafik runbook'tan **Runbook'lar** dikey ve ardından [ **Düzenle** ](automation-graphical-authoring-intro.md) onu.</span><span class="sxs-lookup"><span data-stu-id="3f282-159">Select hello graphical runbook from hello **Runbooks** blade and then click [**Edit**](automation-graphical-authoring-intro.md) it.</span></span>
2. <span data-ttu-id="3f282-160">Merhaba runbook Düzenleyicisi'nden tıklatın **giriş ve çıkış** tooopen hello **giriş ve çıkış** dikey.</span><span class="sxs-lookup"><span data-stu-id="3f282-160">From hello runbook editor, click **Input and output** tooopen hello **Input and output** blade.</span></span>
   
    ![Otomasyon grafik runbook](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. <span data-ttu-id="3f282-162">Merhaba **giriş ve çıkış** dikey penceresinde hello runbook için tanımlanan giriş parametreleri listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="3f282-162">hello **Input and output** blade displays a list of input parameters that are defined for hello runbook.</span></span> <span data-ttu-id="3f282-163">Bu dikey penceresinde, yeni bir giriş parametresi eklemek veya var olan bir giriş parametresi hello yapılandırmasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="3f282-163">On this blade, you can either add a new input parameter or edit hello configuration of an existing input parameter.</span></span> <span data-ttu-id="3f282-164">tooadd hello runbook için yeni bir parametre tıklatın **giriş Ekle** tooopen hello **Runbook giriş parametresi** dikey.</span><span class="sxs-lookup"><span data-stu-id="3f282-164">tooadd a new parameter for hello runbook, click **Add input** tooopen hello **Runbook input parameter** blade.</span></span> <span data-ttu-id="3f282-165">Burada, şu parametreler hello yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3f282-165">There, you can configure hello following parameters:</span></span>
   
   | <span data-ttu-id="3f282-166">**Özellik**</span><span class="sxs-lookup"><span data-stu-id="3f282-166">**Property**</span></span> | <span data-ttu-id="3f282-167">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="3f282-167">**Description**</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="3f282-168">Ad</span><span class="sxs-lookup"><span data-stu-id="3f282-168">Name</span></span> |<span data-ttu-id="3f282-169">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="3f282-169">Required.</span></span>  <span data-ttu-id="3f282-170">Merhaba parametresinin Hello adı.</span><span class="sxs-lookup"><span data-stu-id="3f282-170">hello name of hello parameter.</span></span> <span data-ttu-id="3f282-171">Bu gerekir hello runbook içinde benzersiz olmalıdır ve yalnızca harf, sayı içeren veya alt çizgi karakterleri.</span><span class="sxs-lookup"><span data-stu-id="3f282-171">This must be unique within hello runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="3f282-172">Bir harf ile başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="3f282-172">It must start with a letter.</span></span> |
   | <span data-ttu-id="3f282-173">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3f282-173">Description</span></span> |<span data-ttu-id="3f282-174">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="3f282-174">Optional.</span></span> <span data-ttu-id="3f282-175">Giriş parametresi hello amacı hakkında açıklama.</span><span class="sxs-lookup"><span data-stu-id="3f282-175">Description about hello purpose of input parameter.</span></span> |
   | <span data-ttu-id="3f282-176">Tür</span><span class="sxs-lookup"><span data-stu-id="3f282-176">Type</span></span> |<span data-ttu-id="3f282-177">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="3f282-177">Optional.</span></span> <span data-ttu-id="3f282-178">Merhaba parametre değeri için beklenen veri türü hello.</span><span class="sxs-lookup"><span data-stu-id="3f282-178">hello data type that's expected for hello parameter value.</span></span> <span data-ttu-id="3f282-179">Desteklenen parametre türleri **dize**, **Int32**, **Int64**, **ondalık**, **Boolean**, **DateTime**, ve **nesne**.</span><span class="sxs-lookup"><span data-stu-id="3f282-179">Supported parameter types are **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime**, and **Object**.</span></span> <span data-ttu-id="3f282-180">Bir veri türü seçili değilse, çok varsayılanları**dize**.</span><span class="sxs-lookup"><span data-stu-id="3f282-180">If a data type is not selected, it defaults too**String**.</span></span> |
   | <span data-ttu-id="3f282-181">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="3f282-181">Mandatory</span></span> |<span data-ttu-id="3f282-182">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="3f282-182">Optional.</span></span> <span data-ttu-id="3f282-183">Bir değer hello parametresi için sağlanan olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="3f282-183">Specifies whether a value must be provided for hello parameter.</span></span> <span data-ttu-id="3f282-184">Seçerseniz **Evet**, sonra da hello runbook başlatılırken bir değer sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3f282-184">If you choose **yes**, then a value must be provided when hello runbook is started.</span></span> <span data-ttu-id="3f282-185">Seçerseniz **hiçbir**, bir değer hello runbook başlatıldığında ve varsayılan bir değer ayarlanabilir gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="3f282-185">If you choose **no**, then a value is not required when hello runbook is started, and a default value may be set.</span></span> |
   | <span data-ttu-id="3f282-186">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="3f282-186">Default Value</span></span> |<span data-ttu-id="3f282-187">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="3f282-187">Optional.</span></span> <span data-ttu-id="3f282-188">Merhaba runbook başlatılırken bir değer değil geçtiyse hello parametresi için kullanılan bir değeri belirtir.</span><span class="sxs-lookup"><span data-stu-id="3f282-188">Specifies a value that will be used for hello parameter if a value is not passed in when hello runbook is started.</span></span> <span data-ttu-id="3f282-189">Varsayılan değer, zorunlu olmayan bir parametre için ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="3f282-189">A default value can be set for a parameter that's not mandatory.</span></span> <span data-ttu-id="3f282-190">Varsayılan değer, tooset seçin **özel**.</span><span class="sxs-lookup"><span data-stu-id="3f282-190">tooset a default value, choose **Custom**.</span></span> <span data-ttu-id="3f282-191">Merhaba runbook başlatılırken başka bir değer sağlanmadığı sürece bu değer kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3f282-191">This value is used unless another value is provided when hello runbook is started.</span></span> <span data-ttu-id="3f282-192">Seçin **hiçbiri** tooprovide istemiyorsanız, herhangi bir varsayılan değer.</span><span class="sxs-lookup"><span data-stu-id="3f282-192">Choose **None** if you don’t want tooprovide any default value.</span></span> |
   
    ![Yeni giriş Ekle](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. <span data-ttu-id="3f282-194">Merhaba aşağıdaki hello tarafından kullanılacak olan özelliklere sahip iki parametre Oluştur **Get-AzureRmVm** etkinlik:</span><span class="sxs-lookup"><span data-stu-id="3f282-194">Create two parameters with hello following properties that will be used by hello **Get-AzureRmVm** activity:</span></span>
   
   * <span data-ttu-id="3f282-195">**Parametre1:**</span><span class="sxs-lookup"><span data-stu-id="3f282-195">**Parameter1:**</span></span>
     
     * <span data-ttu-id="3f282-196">Ad - VMName</span><span class="sxs-lookup"><span data-stu-id="3f282-196">Name - VMName</span></span>
     * <span data-ttu-id="3f282-197">-Dize türünde</span><span class="sxs-lookup"><span data-stu-id="3f282-197">Type - String</span></span>
     * <span data-ttu-id="3f282-198">Zorunlu - yok</span><span class="sxs-lookup"><span data-stu-id="3f282-198">Mandatory - No</span></span>
   * <span data-ttu-id="3f282-199">**Parametre2:**</span><span class="sxs-lookup"><span data-stu-id="3f282-199">**Parameter2:**</span></span>
     
     * <span data-ttu-id="3f282-200">Ad - resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="3f282-200">Name - resourceGroupName</span></span>
     * <span data-ttu-id="3f282-201">-Dize türünde</span><span class="sxs-lookup"><span data-stu-id="3f282-201">Type - String</span></span>
     * <span data-ttu-id="3f282-202">Zorunlu - yok</span><span class="sxs-lookup"><span data-stu-id="3f282-202">Mandatory - No</span></span>
     * <span data-ttu-id="3f282-203">Varsayılan değer - özel</span><span class="sxs-lookup"><span data-stu-id="3f282-203">Default value - Custom</span></span>
     * <span data-ttu-id="3f282-204">Özel varsayılan değer - \<hello sanal makineleri içeren hello kaynak grubu adı ></span><span class="sxs-lookup"><span data-stu-id="3f282-204">Custom default value - \<Name of hello resource group that contains hello virtual machines></span></span>
5. <span data-ttu-id="3f282-205">Merhaba parametreleri ekledikten sonra tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3f282-205">Once you add hello parameters, click **OK**.</span></span>  <span data-ttu-id="3f282-206">Bunları artık hello görüntüleyebilirsiniz **giriş ve çıkış dikey**.</span><span class="sxs-lookup"><span data-stu-id="3f282-206">You can now view them in hello **Input and output blade**.</span></span> <span data-ttu-id="3f282-207">Tıklatın **Tamam** yeniden ve ardından **kaydetmek** ve **Yayımla** runbook'unuz.</span><span class="sxs-lookup"><span data-stu-id="3f282-207">Click **OK** again, and then click **Save** and **Publish** your runbook.</span></span>

## <a name="assign-values-tooinput-parameters-in-runbooks"></a><span data-ttu-id="3f282-208">Runbook'ları tooinput parametrelerinde değerler atayın</span><span class="sxs-lookup"><span data-stu-id="3f282-208">Assign values tooinput parameters in runbooks</span></span>
<span data-ttu-id="3f282-209">Runbook'larında senaryoları aşağıdaki hello tooinput parametre değerlerinin geçmesini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f282-209">You can pass values tooinput parameters in runbooks in hello following scenarios.</span></span>

### <a name="start-a-runbook-and-assign-parameters"></a><span data-ttu-id="3f282-210">Bir runbook başlatın ve parametreleri atayın</span><span class="sxs-lookup"><span data-stu-id="3f282-210">Start a runbook and assign parameters</span></span>
<span data-ttu-id="3f282-211">Bir runbook birçok yolu başlatılabilir: hello bir Web kancası ile PowerShell cmdlet'leri ile hello REST API ile veya hello SDK ile Azure portal aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="3f282-211">A runbook can be started many ways: through hello Azure portal, with a webhook, with PowerShell cmdlets, with hello REST API, or with hello SDK.</span></span> <span data-ttu-id="3f282-212">Aşağıda bir runbook'u başlatma ve parametreleri atamak için farklı yöntemler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3f282-212">Below we discuss different methods for starting a runbook and assigning parameters.</span></span>

#### <a name="start-a-published-runbook-by-using-hello-azure-portal-and-assign-parameters"></a><span data-ttu-id="3f282-213">Hello Azure portal kullanarak yayımlanan bir runbook başlatın ve parametreleri atayın</span><span class="sxs-lookup"><span data-stu-id="3f282-213">Start a published runbook by using hello Azure portal and assign parameters</span></span>
<span data-ttu-id="3f282-214">Olduğunda, [hello runbook'u başlatmak](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **Runbook'u Başlat** dikey penceresi açılır ve yeni oluşturduğunuz hello parametreleri için değerleri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f282-214">When you [start hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **Start Runbook** blade opens and you can configure values for hello parameters that you just created.</span></span>

![Merhaba portalı kullanmaya başlama](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

<span data-ttu-id="3f282-216">Merhaba giriş kutusu altındaki Hello etiketinde hello parametresi için belirlenen hello öznitelikleri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f282-216">In hello label beneath hello input box, you can see hello attributes that have been set for hello parameter.</span></span> <span data-ttu-id="3f282-217">Öznitelikler, zorunlu veya isteğe bağlı, türü ve varsayılan değeri içerir.</span><span class="sxs-lookup"><span data-stu-id="3f282-217">Attributes include mandatory or optional, type, and  default value.</span></span> <span data-ttu-id="3f282-218">Merhaba Yardım balonu sonraki toohello parametre adı, parametre giriş değerleri toomake kararlardan gereksinim duyduğunuz tüm hello anahtar bilgileri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f282-218">In hello help balloon next toohello parameter name, you can see all hello key information you need toomake decisions about parameter input values.</span></span> <span data-ttu-id="3f282-219">Bir parametre zorunlu veya isteğe bağlı olup, bu bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="3f282-219">This information includes whether a parameter is mandatory or optional.</span></span> <span data-ttu-id="3f282-220">Ayrıca hello türü ve varsayılan değer (varsa) ve diğer yararlı notlar içerir.</span><span class="sxs-lookup"><span data-stu-id="3f282-220">It also includes hello type and default value (if any), and other helpful notes.</span></span>

![Yardım balonu](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> <span data-ttu-id="3f282-222">Dize türü parametreleri desteği **boş** dize değerleri.</span><span class="sxs-lookup"><span data-stu-id="3f282-222">String type parameters support **Empty** String values.</span></span>  <span data-ttu-id="3f282-223">Girme **[oluşması]** hello giriş parametresi boş dize toohello parametre kutusunu geçer.</span><span class="sxs-lookup"><span data-stu-id="3f282-223">Entering **[EmptyString]** in hello input parameter box will pass an empty string toohello parameter.</span></span> <span data-ttu-id="3f282-224">Ayrıca, dize türü parametreleri desteklemeyen **Null** geçirilen değerleri.</span><span class="sxs-lookup"><span data-stu-id="3f282-224">Also, String type parameters don’t support **Null** values being passed.</span></span> <span data-ttu-id="3f282-225">Ardından PowerShell herhangi bir değer toohello dize parametre geçirmezseniz boş olarak görürler.</span><span class="sxs-lookup"><span data-stu-id="3f282-225">If you don’t pass any value toohello String parameter, then PowerShell will interpret it as null.</span></span>
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a><span data-ttu-id="3f282-226">Yayımlanan bir runbook'ta PowerShell cmdlet'lerini kullanarak başlatmak ve parametreleri atayın</span><span class="sxs-lookup"><span data-stu-id="3f282-226">Start a published runbook by using PowerShell cmdlets and assign parameters</span></span>
* <span data-ttu-id="3f282-227">**Azure Resource Manager cmdlet'lerini:** bir kaynak grubunda kullanılarak oluşturulmuş bir Otomasyon runbook'u başlatabilirsiniz [başlangıç AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f282-227">**Azure Resource Manager cmdlets:** You can start an Automation runbook that was created in a resource group by using [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span></span>
  
  <span data-ttu-id="3f282-228">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3f282-228">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* <span data-ttu-id="3f282-229">**Azure Hizmet Yönetimi cmdlet'lerini:** bir varsayılan kaynak grubunda kullanılarak oluşturulmuş bir Otomasyon runbook'u başlatabilirsiniz [başlangıç AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f282-229">**Azure Service Management cmdlets:** You can start an automation runbook that was created in a default resource group by using [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span></span>
  
  <span data-ttu-id="3f282-230">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3f282-230">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> <span data-ttu-id="3f282-231">PowerShell cmdlet'lerini, varsayılan parametre kullanarak bir runbook'u başlattığınızda **MicrosoftApplicationManagementStartedBy** hello değeri ile oluşturulan **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="3f282-231">When you start a runbook by using PowerShell cmdlets, a default parameter, **MicrosoftApplicationManagementStartedBy** is created with hello value **PowerShell**.</span></span> <span data-ttu-id="3f282-232">Bu parametre hello görüntüleyebilirsiniz **iş ayrıntıları** dikey.</span><span class="sxs-lookup"><span data-stu-id="3f282-232">You can view this parameter in hello **Job details** blade.</span></span>  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a><span data-ttu-id="3f282-233">Bir SDK kullanarak bir runbook'u başlatmak ve parametreleri atayın</span><span class="sxs-lookup"><span data-stu-id="3f282-233">Start a runbook by using an SDK and assign parameters</span></span>
* <span data-ttu-id="3f282-234">**Azure Resource Manager yöntemi:** hello bir programlama dili SDK kullanarak bir runbook'u başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f282-234">**Azure Resource Manager method:** You can start a runbook by using hello SDK of a programming language.</span></span> <span data-ttu-id="3f282-235">Otomasyon hesabınızda bir runbook'u başlatmak için C# kod parçacığı aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="3f282-235">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="3f282-236">Tüm hello kodu görüntüleyebilirsiniz bizim [GitHub deposunu](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="3f282-236">You can view all hello code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>  
  
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
* <span data-ttu-id="3f282-237">**Azure hizmet yönetimi yöntemi:** hello bir programlama dili SDK kullanarak bir runbook'u başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f282-237">**Azure Service Management method:** You can start a runbook by using hello SDK of a programming language.</span></span> <span data-ttu-id="3f282-238">Otomasyon hesabınızda bir runbook'u başlatmak için C# kod parçacığı aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="3f282-238">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="3f282-239">Tüm hello kodu görüntüleyebilirsiniz bizim [GitHub deposunu](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="3f282-239">You can view all hello code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>
  
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
  
  <span data-ttu-id="3f282-240">toostart bu yöntem bir sözlük toostore hello runbook parametreleri oluşturmak **VMName** ve **resourceGroupName**ve değerleri.</span><span class="sxs-lookup"><span data-stu-id="3f282-240">toostart this method, create a dictionary toostore hello runbook parameters, **VMName** and  **resourceGroupName**, and their values.</span></span> <span data-ttu-id="3f282-241">Daha sonra hello runbook başlatın.</span><span class="sxs-lookup"><span data-stu-id="3f282-241">Then start hello runbook.</span></span> <span data-ttu-id="3f282-242">Merhaba C# kod parçacığını yukarıda tanımlanan hello yöntemi çağırmak için aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="3f282-242">Below is hello C# code snippet for calling hello method that's defined above.</span></span>
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters toohello dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call hello StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-hello-rest-api-and-assign-parameters"></a><span data-ttu-id="3f282-243">Merhaba REST API kullanarak bir runbook'u başlatmak ve parametreleri atayın</span><span class="sxs-lookup"><span data-stu-id="3f282-243">Start a runbook by using hello REST API and assign parameters</span></span>
<span data-ttu-id="3f282-244">Bir runbook işi oluşturulur ve Azure Automation REST API hello ile Merhaba kullanmaya **PUT** aşağıdaki hello yöntemiyle istek URI.</span><span class="sxs-lookup"><span data-stu-id="3f282-244">A runbook job can be created and started with hello Azure Automation REST API by using hello **PUT** method with hello following request URI.</span></span>

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

<span data-ttu-id="3f282-245">Merhaba istek URI'Sİ'da, şu parametreler hello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="3f282-245">In hello request URI, replace hello following parameters:</span></span>

* <span data-ttu-id="3f282-246">**Abonelik kimliği:** Azure abonelik kimliğinizi</span><span class="sxs-lookup"><span data-stu-id="3f282-246">**subscription-id:** Your Azure subscription ID.</span></span>  
* <span data-ttu-id="3f282-247">**Bulut hizmet adı:** hello bulut hizmeti toowhich hello isteği hello adını gönderilmeyecek.</span><span class="sxs-lookup"><span data-stu-id="3f282-247">**cloud-service-name:** hello name of hello cloud service toowhich hello request should be sent.</span></span>  
* <span data-ttu-id="3f282-248">**Otomasyon hesabı adı:** bulut hizmeti belirtilen hello içinde barındırılan automation hesabınız hello adı.</span><span class="sxs-lookup"><span data-stu-id="3f282-248">**automation-account-name:** hello name of your automation account that's hosted within hello specified cloud service.</span></span>  
* <span data-ttu-id="3f282-249">**İş Kimliği:** hello işi için GUID hello.</span><span class="sxs-lookup"><span data-stu-id="3f282-249">**job-id:** hello GUID for hello job.</span></span> <span data-ttu-id="3f282-250">PowerShell'de GUID'ler hello kullanarak oluşturulabilir **[GUID]::NewGuid(). ToString()** komutu.</span><span class="sxs-lookup"><span data-stu-id="3f282-250">GUIDs in PowerShell can be created by using hello **[GUID]::NewGuid().ToString()** command.</span></span>

<span data-ttu-id="3f282-251">Sipariş toopass parametreleri toohello runbook işi içinde hello istek gövdesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="3f282-251">In order toopass parameters toohello runbook job, use hello request body.</span></span> <span data-ttu-id="3f282-252">Aşağıdaki JSON biçiminde sağlanan iki özelliklere hello alır:</span><span class="sxs-lookup"><span data-stu-id="3f282-252">It takes hello following two properties provided in JSON format:</span></span>

* <span data-ttu-id="3f282-253">**Runbook adı:** gerekli.</span><span class="sxs-lookup"><span data-stu-id="3f282-253">**Runbook name:** Required.</span></span> <span data-ttu-id="3f282-254">Merhaba iş toostart hello runbook adı Hello.</span><span class="sxs-lookup"><span data-stu-id="3f282-254">hello name of hello runbook for hello job toostart.</span></span>  
* <span data-ttu-id="3f282-255">**Runbook parametreleri:** isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="3f282-255">**Runbook parameters:** Optional.</span></span> <span data-ttu-id="3f282-256">Hello parametre listesi (adı, değer) sözlüğü biçiminde burada adı dize türünde olmalıdır ve değer geçerli bir JSON değeri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3f282-256">A dictionary of hello parameter list in (name, value) format where name should be of String type and value can be any valid JSON value.</span></span>

<span data-ttu-id="3f282-257">Toostart hello istiyorsanız **Get-AzureVMTextual** daha önce oluşturulmuş runbook **VMName** ve **resourceGroupName** hello JSON biçimi aşağıdaki parametreleri olarak kullanma Merhaba istek gövdesi.</span><span class="sxs-lookup"><span data-stu-id="3f282-257">If you want toostart hello **Get-AzureVMTextual** runbook that was created earlier with **VMName** and **resourceGroupName** as parameters, use hello following JSON format for hello request body.</span></span>

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

<span data-ttu-id="3f282-258">Merhaba işi başarıyla oluşturulduysa 201 HTTP durum kodu döndürülür.</span><span class="sxs-lookup"><span data-stu-id="3f282-258">A HTTP status code 201 is returned if hello job is successfully created.</span></span> <span data-ttu-id="3f282-259">Yanıt Üstbilgileri ve hello yanıt gövdesi ile ilgili daha fazla bilgi için ilgili toohello makale çok başvurun[hello REST API kullanarak bir runbook işi oluşturun.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span><span class="sxs-lookup"><span data-stu-id="3f282-259">For more information on response headers and hello response body, refer toohello article about how too[create a runbook job by using hello REST API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span></span>

### <a name="test-a-runbook-and-assign-parameters"></a><span data-ttu-id="3f282-260">Bir runbook'u test ve parametreleri atayın</span><span class="sxs-lookup"><span data-stu-id="3f282-260">Test a runbook and assign parameters</span></span>
<span data-ttu-id="3f282-261">Olduğunda, [runbook'unuzu test hello taslak sürümünü](automation-testing-runbook.md) hello test seçeneğini kullanarak hello **Test** dikey penceresi açılır ve yeni oluşturduğunuz hello parametreleri için değerleri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f282-261">When you [test hello draft version of your runbook](automation-testing-runbook.md) by using hello test option, hello **Test** blade opens and you can configure values for hello parameters that you just created.</span></span>

![Test ve ata parametreleri](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-tooa-runbook-and-assign-parameters"></a><span data-ttu-id="3f282-263">Bir zamanlama tooa runbook bağlamak ve parametreleri atayın</span><span class="sxs-lookup"><span data-stu-id="3f282-263">Link a schedule tooa runbook and assign parameters</span></span>
<span data-ttu-id="3f282-264">Yapabilecekleriniz [bir zamanlama Bağla](automation-schedules.md) tooyour runbook için belirli bir süre boyunca bu hello runbook başlatır.</span><span class="sxs-lookup"><span data-stu-id="3f282-264">You can [link a schedule](automation-schedules.md) tooyour runbook so that hello runbook starts at a specific time.</span></span> <span data-ttu-id="3f282-265">Giriş parametreleri hello zamanlama oluştururken ve hello zamanlamaya uygun olarak başlatıldı hello runbook bu değerleri için kullanacağı atayın.</span><span class="sxs-lookup"><span data-stu-id="3f282-265">You assign input parameters when you create hello schedule, and hello runbook will use these values when it is started by hello schedule.</span></span> <span data-ttu-id="3f282-266">Tüm zorunlu parametre değerleri sağlanana kadar hello zamanlaması kaydedilemiyor.</span><span class="sxs-lookup"><span data-stu-id="3f282-266">You can’t save hello schedule until all mandatory parameter values are provided.</span></span>

![Zamanlama ve parametreleri atama](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a><span data-ttu-id="3f282-268">Bir runbook için bir Web kancası oluşturun ve parametreleri atayın</span><span class="sxs-lookup"><span data-stu-id="3f282-268">Create a webhook for a runbook and assign parameters</span></span>
<span data-ttu-id="3f282-269">Oluşturabileceğiniz bir [Web kancası](automation-webhooks.md) runbook'unuzu için ve runbook giriş parametreleri yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3f282-269">You can create a [webhook](automation-webhooks.md) for your runbook and configure runbook input parameters.</span></span> <span data-ttu-id="3f282-270">Tüm zorunlu parametre değerleri sağlanana kadar hello Web kancası kaydedilemiyor.</span><span class="sxs-lookup"><span data-stu-id="3f282-270">You can’t save hello webhook until all mandatory parameter values are provided.</span></span>

![Web kancası oluşturun ve parametreleri atayın](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

<span data-ttu-id="3f282-272">Bir Web kancası kullanarak bir runbook'u yürüttüğünüzde hello giriş parametresi önceden tanımlanmış  **[Webhookdata](automation-webhooks.md#details-of-a-webhook)**  tanımladığınız hello giriş parametreleri birlikte gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3f282-272">When you execute a runbook by using a webhook, hello predefined input parameter **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** is sent, along with hello input parameters that you defined.</span></span> <span data-ttu-id="3f282-273">Tooexpand hello tıklayabilirsiniz **WebhookData** daha fazla ayrıntı için parametre.</span><span class="sxs-lookup"><span data-stu-id="3f282-273">You can click tooexpand hello **WebhookData** parameter for more details.</span></span>

![WebhookData parametresi](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a><span data-ttu-id="3f282-275">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3f282-275">Next steps</span></span>
* <span data-ttu-id="3f282-276">Runbook giriş ve çıkış hakkında daha fazla bilgi için bkz: [Azure Automation: runbook giriş, çıkış ve iç içe runbook](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span><span class="sxs-lookup"><span data-stu-id="3f282-276">For more information on runbook input and output, see [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span></span>
* <span data-ttu-id="3f282-277">Farklı şekillerde toostart bir runbook hakkında daha fazla ayrıntı için bkz: [runbook başlatma](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="3f282-277">For details about different ways toostart a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="3f282-278">tooedit metin biçiminde runbook başvurmak çok[metinsel runbook'ları düzenleme](automation-edit-textual-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="3f282-278">tooedit a textual runbook, refer too[Editing textual runbooks](automation-edit-textual-runbook.md).</span></span>
* <span data-ttu-id="3f282-279">tooedit grafik runbook başvurmak çok[Azure Automation'da grafik yazma](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="3f282-279">tooedit a graphical runbook, refer too[Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

