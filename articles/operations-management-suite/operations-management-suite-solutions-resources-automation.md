---
title: "OMS çözümlerinde aaaAzure Automation kaynaklarını | Microsoft Docs"
description: "OMS çözümlerinde, toplama ve izleme verilerini işleme gibi Azure Otomasyonu tooautomate işlemlerde runbook'ları genellikle dahil edilir.  Bu makalede nasıl tooinclude runbook'ları ve ilgili kaynaklarını bir çözümde."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 82a156f89bf77ce25e52e5e4596261ec07a24dae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-automation-resources-tooan-oms-management-solution-preview"></a><span data-ttu-id="1155d-104">Azure Otomasyonu kaynakları tooan OMS yönetim çözümü (Önizleme) ekleme</span><span class="sxs-lookup"><span data-stu-id="1155d-104">Adding Azure Automation resources tooan OMS management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="1155d-105">Bu, şu anda önizlemede OMS yönetim çözümleri oluşturmak için başlangıç belgesidir.</span><span class="sxs-lookup"><span data-stu-id="1155d-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="1155d-106">Aşağıda açıklanan herhangi bir şema konu toochange ' dir.</span><span class="sxs-lookup"><span data-stu-id="1155d-106">Any schema described below is subject toochange.</span></span>   


<span data-ttu-id="1155d-107">[OMS yönetim çözümlerine](operations-management-suite-solutions.md) toplama ve izleme verilerini işleme gibi Azure Otomasyonu tooautomate işlemlerde runbook'ları tipik olarak içerecektir.</span><span class="sxs-lookup"><span data-stu-id="1155d-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation tooautomate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="1155d-108">Ayrıca toorunbooks, Automation hesaplarını içerir değişkenleri ve hello çözümde kullanılan hello runbook'ları destek zamanlamaları gibi varlıklar.</span><span class="sxs-lookup"><span data-stu-id="1155d-108">In addition toorunbooks, Automation accounts includes assets such as variables and schedules that support hello runbooks used in hello solution.</span></span>  <span data-ttu-id="1155d-109">Bu makalede nasıl tooinclude runbook'ları ve ilgili kaynaklarını bir çözümde.</span><span class="sxs-lookup"><span data-stu-id="1155d-109">This article describes how tooinclude runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="1155d-110">Merhaba bu makaledeki örnekler parametreleri ve ya da gerekli veya ortak toomanagement çözümleri ve açıklanan değişkenleri kullanma [Operations Management Suite (OMS) yönetimi çözümleri oluşturma](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="1155d-110">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="1155d-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1155d-111">Prerequisites</span></span>
<span data-ttu-id="1155d-112">Bu makale, zaten ile Merhaba aşağıdaki bilgilerle aşina olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="1155d-112">This article assumes that you're already familiar with hello following information.</span></span>

- <span data-ttu-id="1155d-113">Nasıl çok[bir yönetim çözümü oluşturma](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="1155d-113">How too[create a management solution](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="1155d-114">Merhaba yapısını bir [çözüm dosyasını](operations-management-suite-solutions-solution-file.md).</span><span class="sxs-lookup"><span data-stu-id="1155d-114">hello structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span></span>
- <span data-ttu-id="1155d-115">Nasıl çok[Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="1155d-115">How too[author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="1155d-116">Otomasyon hesabı</span><span class="sxs-lookup"><span data-stu-id="1155d-116">Automation account</span></span>
<span data-ttu-id="1155d-117">Azure Otomasyonu tüm kaynakları bulunan bir [Otomasyon hesabı](../automation/automation-security-overview.md#automation-account-overview).</span><span class="sxs-lookup"><span data-stu-id="1155d-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="1155d-118">Bölümünde açıklandığı gibi [OMS çalışma ve Automation hesabı](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello Otomasyon hesabı hello Yönetimi çözümünde dahil değildir ancak hello çözüm yüklenmeden önce mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1155d-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello Automation account isn't included in hello management solution but must exist before hello solution is installed.</span></span>  <span data-ttu-id="1155d-119">Kullanılabilir değilse, hello çözüm yükleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="1155d-119">If it isn't available, then hello solution install will fail.</span></span>

<span data-ttu-id="1155d-120">Her Otomasyon kaynağı Hello adını kendi Automation hesabı hello adını içerir.</span><span class="sxs-lookup"><span data-stu-id="1155d-120">hello name of each Automation resource includes hello name of its Automation account.</span></span>  <span data-ttu-id="1155d-121">Bu hello ile Merhaba çözümde yapılır **accountName** runbook kaynak örneği aşağıdaki hello olduğu gibi parametre.</span><span class="sxs-lookup"><span data-stu-id="1155d-121">This is done in hello solution with hello **accountName** parameter as in hello following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="1155d-122">Runbook'lar</span><span class="sxs-lookup"><span data-stu-id="1155d-122">Runbooks</span></span>
<span data-ttu-id="1155d-123">Merhaba çözüm yüklendiğinde, oluşturuldukları hello Çözüm dosyasındaki hello çözüm tarafından kullanılan tüm runbook içermelidir.</span><span class="sxs-lookup"><span data-stu-id="1155d-123">You should include any runbooks used by hello solution in hello solution file so that they're created when hello solution is installed.</span></span>  <span data-ttu-id="1155d-124">Yayımlama hello runbook tooa ortak konumu burada çözümünüzü yükleme herhangi bir kullanıcı tarafından erişilebilir şekilde hello şablon hello runbook'ta hello gövdesi yine de içeremez.</span><span class="sxs-lookup"><span data-stu-id="1155d-124">You cannot contain hello body of hello runbook in hello template though, so you should publish hello runbook tooa public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="1155d-125">[Azure Otomasyonu runbook'u](../automation/automation-runbook-types.md) kaynaklarınız türü **Microsoft.Automation/automationAccounts/runbooks** ve yapı izlenerek hello sahip.</span><span class="sxs-lookup"><span data-stu-id="1155d-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have hello following structure.</span></span> <span data-ttu-id="1155d-126">Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir.</span><span class="sxs-lookup"><span data-stu-id="1155d-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
        "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
        "type": "Microsoft.Automation/automationAccounts/runbooks",
        "apiVersion": "[variables('AutomationApiVersion')]",
        "dependsOn": [
        ],
        "location": "[parameters('regionId')]",
        "tags": { },
        "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
                "uri": "[variables('Runbook').Uri]",
                "version": [variables('Runbook').Version]"
            }
        }
    }


<span data-ttu-id="1155d-127">Aşağıdaki tablonun hello runbook'lar için Hello özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1155d-127">hello properties for runbooks are described in hello following table.</span></span>

| <span data-ttu-id="1155d-128">Özellik</span><span class="sxs-lookup"><span data-stu-id="1155d-128">Property</span></span> | <span data-ttu-id="1155d-129">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1155d-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1155d-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="1155d-130">runbookType</span></span> |<span data-ttu-id="1155d-131">Merhaba runbook Hello türlerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1155d-131">Specifies hello types of hello runbook.</span></span> <br><br> <span data-ttu-id="1155d-132">Komut dosyası - PowerShell komut dosyası</span><span class="sxs-lookup"><span data-stu-id="1155d-132">Script - PowerShell script</span></span> <br><span data-ttu-id="1155d-133">PowerShell - PowerShell iş akışı</span><span class="sxs-lookup"><span data-stu-id="1155d-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="1155d-134">GraphPowerShell - grafik PowerShell komut dosyası runbook</span><span class="sxs-lookup"><span data-stu-id="1155d-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="1155d-135">GraphPowerShellWorkflow - grafik PowerShell iş akışı runbook</span><span class="sxs-lookup"><span data-stu-id="1155d-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="1155d-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="1155d-136">logProgress</span></span> |<span data-ttu-id="1155d-137">Belirtir olup olmadığını [ilerleme kayıtlarını](../automation/automation-runbook-output-and-messages.md) hello runbook için oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1155d-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for hello runbook.</span></span> |
| <span data-ttu-id="1155d-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="1155d-138">logVerbose</span></span> |<span data-ttu-id="1155d-139">Belirtir olup olmadığını [ayrıntılı kayıtları](../automation/automation-runbook-output-and-messages.md) hello runbook için oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1155d-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for hello runbook.</span></span> |
| <span data-ttu-id="1155d-140">açıklama</span><span class="sxs-lookup"><span data-stu-id="1155d-140">description</span></span> |<span data-ttu-id="1155d-141">Merhaba runbook için isteğe bağlı bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="1155d-141">Optional description for hello runbook.</span></span> |
| <span data-ttu-id="1155d-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="1155d-142">publishContentLink</span></span> |<span data-ttu-id="1155d-143">Merhaba runbook Merhaba içeriğine belirtir.</span><span class="sxs-lookup"><span data-stu-id="1155d-143">Specifies hello content of hello runbook.</span></span> <br><br><span data-ttu-id="1155d-144">URI - URI toohello hello runbook'unun içeriğini.</span><span class="sxs-lookup"><span data-stu-id="1155d-144">uri - Uri toohello content of hello runbook.</span></span>  <span data-ttu-id="1155d-145">Bu, PowerShell ve komut dosyası runbook'lar için bir .ps1 dosyası ve bir grafik runbook'u dışarı aktarılan grafik runbook dosyası olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1155d-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="1155d-146">Sürüm - hello runbook kendi izleme için sürümü.</span><span class="sxs-lookup"><span data-stu-id="1155d-146">version - Version of hello runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="1155d-147">Otomasyon işleri</span><span class="sxs-lookup"><span data-stu-id="1155d-147">Automation jobs</span></span>
<span data-ttu-id="1155d-148">Azure Automation'da bir runbook başlattığınızda bir Otomasyonu işi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1155d-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="1155d-149">Merhaba yönetim çözümü yüklendiğinde bir runbook bir Otomasyon iş kaynak tooyour çözüm tooautomatically başlangıç ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1155d-149">You can add an automation job resource tooyour solution tooautomatically start a runbook when hello management solution is installed.</span></span>  <span data-ttu-id="1155d-150">Bu yöntem hello çözüm'in ilk yapılandırması için kullanılan genellikle kullanılan toostart runbook'ları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1155d-150">This method is typically used toostart runbooks that are used for initial configuration of hello solution.</span></span>  <span data-ttu-id="1155d-151">toostart düzenli aralıklarla bir runbook oluşturmak bir [zamanlama](#schedules) ve [iş zamanlaması](#job-schedules)</span><span class="sxs-lookup"><span data-stu-id="1155d-151">toostart a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="1155d-152">İş kaynaklarınız türü **Microsoft.Automation/automationAccounts/jobs** ve yapı izlenerek hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1155d-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have hello following structure.</span></span>  <span data-ttu-id="1155d-153">Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir.</span><span class="sxs-lookup"><span data-stu-id="1155d-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', parameters('Runbook').JobGuid)]",
      "type": "Microsoft.Automation/automationAccounts/jobs",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
      ],
      "tags": { },
      "properties": {
        "runbook": {
          "name": "[variables('Runbook').Name]"
        },
        "parameters": {
          "Parameter1": "[[variables('Runbook').Parameter1]",
          "Parameter2": "[[variables('Runbook').Parameter2]"
        }
      }
    }

<span data-ttu-id="1155d-154">Aşağıdaki tablonun hello Otomasyon işleri için Hello özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1155d-154">hello properties for automation jobs are described in hello following table.</span></span>

| <span data-ttu-id="1155d-155">Özellik</span><span class="sxs-lookup"><span data-stu-id="1155d-155">Property</span></span> | <span data-ttu-id="1155d-156">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1155d-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1155d-157">runbook</span><span class="sxs-lookup"><span data-stu-id="1155d-157">runbook</span></span> |<span data-ttu-id="1155d-158">Tek bir ad varlık hello runbook toostart hello adı.</span><span class="sxs-lookup"><span data-stu-id="1155d-158">Single name entity with hello name of hello runbook toostart.</span></span> |
| <span data-ttu-id="1155d-159">parametreler</span><span class="sxs-lookup"><span data-stu-id="1155d-159">parameters</span></span> |<span data-ttu-id="1155d-160">Varlık hello runbook tarafından gerekli her parametre değeri.</span><span class="sxs-lookup"><span data-stu-id="1155d-160">Entity for each parameter value required by hello runbook.</span></span> |

<span data-ttu-id="1155d-161">Merhaba iş hello runbook adı ve toohello runbook gönderilen tüm parametre değerleri toobe içerir.</span><span class="sxs-lookup"><span data-stu-id="1155d-161">hello job includes hello runbook name and any parameter values toobe sent toohello runbook.</span></span>  <span data-ttu-id="1155d-162">Merhaba iş gereken [bağımlı](operations-management-suite-solutions-solution-file.md#resources) bu yana hello runbook başlatma hello runbook, hello işten daha önce oluşturulmuş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1155d-162">hello job should [depend on](operations-management-suite-solutions-solution-file.md#resources) hello runbook that it's starting since hello runbook must be created before hello job.</span></span>  <span data-ttu-id="1155d-163">Başlatılması gereken birden çok runbook varsa, ilk çalışması gereken tüm diğer işler bağımlı bir iş sağlayarak sıralarına tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1155d-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="1155d-164">bir iş kaynağı Hello adı genellikle parametresi tarafından atanan bir GUID içermelidir.</span><span class="sxs-lookup"><span data-stu-id="1155d-164">hello name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="1155d-165">Daha fazla bilgiyi GUID parametreler hakkında [Operations Management Suite (OMS) çözümleri oluşturma](operations-management-suite-solutions-solution-file.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="1155d-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="1155d-166">Sertifikalar</span><span class="sxs-lookup"><span data-stu-id="1155d-166">Certificates</span></span>
<span data-ttu-id="1155d-167">[Azure Otomasyonu sertifika](../automation/automation-certificates.md) bir türüne sahip **Microsoft.Automation/automationAccounts/certificates** ve yapı izlenerek hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1155d-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have hello following structure.</span></span> <span data-ttu-id="1155d-168">Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir.</span><span class="sxs-lookup"><span data-stu-id="1155d-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
      "type": "Microsoft.Automation/automationAccounts/certificates",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "base64Value": "[variables('Certificate').Base64Value]",
        "thumbprint": "[variables('Certificate').Thumbprint]"
      }
    }



<span data-ttu-id="1155d-169">Aşağıdaki tablonun hello sertifikaları kaynakların Hello özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1155d-169">hello properties for Certificates resources are described in hello following table.</span></span>

| <span data-ttu-id="1155d-170">Özellik</span><span class="sxs-lookup"><span data-stu-id="1155d-170">Property</span></span> | <span data-ttu-id="1155d-171">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1155d-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1155d-172">base64value değeri</span><span class="sxs-lookup"><span data-stu-id="1155d-172">base64Value</span></span> |<span data-ttu-id="1155d-173">Merhaba sertifika Base 64 değeri.</span><span class="sxs-lookup"><span data-stu-id="1155d-173">Base 64 value for hello certificate.</span></span> |
| <span data-ttu-id="1155d-174">parmak izi</span><span class="sxs-lookup"><span data-stu-id="1155d-174">thumbprint</span></span> |<span data-ttu-id="1155d-175">Merhaba sertifika parmak izi.</span><span class="sxs-lookup"><span data-stu-id="1155d-175">Thumbprint for hello certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="1155d-176">Kimlik Bilgileri</span><span class="sxs-lookup"><span data-stu-id="1155d-176">Credentials</span></span>
<span data-ttu-id="1155d-177">[Azure Otomasyonu kimlik](../automation/automation-credentials.md) bir türüne sahip **Microsoft.Automation/automationAccounts/credentials** ve yapı izlenerek hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1155d-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have hello following structure.</span></span>  <span data-ttu-id="1155d-178">Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir.</span><span class="sxs-lookup"><span data-stu-id="1155d-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 


    {
      "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
      "type": "Microsoft.Automation/automationAccounts/credentials",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "userName": "[parameters('credentialUsername')]",
        "password": "[parameters('credentialPassword')]"
      }
    }

<span data-ttu-id="1155d-179">Aşağıdaki tablonun hello kimlik bilgisi kaynakların Hello özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1155d-179">hello properties for Credential resources are described in hello following table.</span></span>

| <span data-ttu-id="1155d-180">Özellik</span><span class="sxs-lookup"><span data-stu-id="1155d-180">Property</span></span> | <span data-ttu-id="1155d-181">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1155d-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1155d-182">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="1155d-182">userName</span></span> |<span data-ttu-id="1155d-183">Merhaba kimlik bilgisi için kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="1155d-183">User name for hello credential.</span></span> |
| <span data-ttu-id="1155d-184">password</span><span class="sxs-lookup"><span data-stu-id="1155d-184">password</span></span> |<span data-ttu-id="1155d-185">Merhaba kimlik bilgileri parolası.</span><span class="sxs-lookup"><span data-stu-id="1155d-185">Password for hello credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="1155d-186">Zamanlamalar</span><span class="sxs-lookup"><span data-stu-id="1155d-186">Schedules</span></span>
<span data-ttu-id="1155d-187">[Azure Otomasyon zamanlamaları](../automation/automation-schedules.md) bir türüne sahip **Microsoft.Automation/automationAccounts/schedules** ve yapı izlenerek hello hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1155d-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have hello hello following structure.</span></span> <span data-ttu-id="1155d-188">Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir.</span><span class="sxs-lookup"><span data-stu-id="1155d-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
      "type": "microsoft.automation/automationAccounts/schedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Schedule').Description]",
        "startTime": "[parameters('scheduleStartTime')]",
        "timeZone": "[parameters('scheduleTimeZone')]",
        "isEnabled": "[variables('Schedule').IsEnabled]",
        "interval": "[variables('Schedule').Interval]",
        "frequency": "[variables('Schedule').Frequency]"
      }
    }

<span data-ttu-id="1155d-189">Aşağıdaki tablonun hello zamanlama kaynakların Hello özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1155d-189">hello properties for schedule resources are described in hello following table.</span></span>

| <span data-ttu-id="1155d-190">Özellik</span><span class="sxs-lookup"><span data-stu-id="1155d-190">Property</span></span> | <span data-ttu-id="1155d-191">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1155d-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1155d-192">açıklama</span><span class="sxs-lookup"><span data-stu-id="1155d-192">description</span></span> |<span data-ttu-id="1155d-193">Merhaba zamanlama için isteğe bağlı bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="1155d-193">Optional description for hello schedule.</span></span> |
| <span data-ttu-id="1155d-194">startTime</span><span class="sxs-lookup"><span data-stu-id="1155d-194">startTime</span></span> |<span data-ttu-id="1155d-195">Merhaba başlangıç zamanı, zamanlamanın bir DateTime nesnesi olarak belirtir.</span><span class="sxs-lookup"><span data-stu-id="1155d-195">Specifies hello start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="1155d-196">Dönüştürülen tooa olabiliyorsa bir dize sağlanabilir geçerli tarih saat.</span><span class="sxs-lookup"><span data-stu-id="1155d-196">A string can be provided if it can be converted tooa valid DateTime.</span></span> |
| <span data-ttu-id="1155d-197">IsEnabled</span><span class="sxs-lookup"><span data-stu-id="1155d-197">isEnabled</span></span> |<span data-ttu-id="1155d-198">Merhaba zamanlama etkinleştirilip etkinleştirilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1155d-198">Specifies whether hello schedule is enabled.</span></span> |
| <span data-ttu-id="1155d-199">interval</span><span class="sxs-lookup"><span data-stu-id="1155d-199">interval</span></span> |<span data-ttu-id="1155d-200">Merhaba tür hello zamanlaması için aralık.</span><span class="sxs-lookup"><span data-stu-id="1155d-200">hello type of interval for hello schedule.</span></span><br><br><span data-ttu-id="1155d-201">günü</span><span class="sxs-lookup"><span data-stu-id="1155d-201">day</span></span><br><span data-ttu-id="1155d-202">saat</span><span class="sxs-lookup"><span data-stu-id="1155d-202">hour</span></span> |
| <span data-ttu-id="1155d-203">frequency</span><span class="sxs-lookup"><span data-stu-id="1155d-203">frequency</span></span> |<span data-ttu-id="1155d-204">Zamanlama hello sıklığı gün veya saat cinsinden harekete.</span><span class="sxs-lookup"><span data-stu-id="1155d-204">Frequency that hello schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="1155d-205">Zamanlama başlangıç zamanı geçerli saati hello büyük bir değere sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1155d-205">Schedules must have a start time with a value greater than hello current time.</span></span>  <span data-ttu-id="1155d-206">Devam eden toobe yüklü olduğunda bilmesinin yolu yoktur olduğundan bu değer sahip bir değişken sağlayamaz.</span><span class="sxs-lookup"><span data-stu-id="1155d-206">You cannot provide this value with a variable since you would have no way of knowing when it's going toobe installed.</span></span>

<span data-ttu-id="1155d-207">İki stratejileri zamanlama kaynakları bir çözümde kullanırken aşağıdaki hello birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1155d-207">Use one of hello following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="1155d-208">Bir parametre hello başlangıç zamanı hello zamanlama için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1155d-208">Use a parameter for hello start time of hello schedule.</span></span>  <span data-ttu-id="1155d-209">Merhaba çözüm yüklediğinizde bu hello kullanıcı tooprovide bir değer ister.</span><span class="sxs-lookup"><span data-stu-id="1155d-209">This will prompt hello user tooprovide a value when they install hello solution.</span></span>  <span data-ttu-id="1155d-210">Birden çok zamanlama varsa, tek bir parametre birden fazla bunlardan biri için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1155d-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="1155d-211">Merhaba çözüm yüklendiğinde başlayan bir runbook ile Merhaba zamanlamalar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1155d-211">Create hello schedules using a runbook that starts when hello solution is installed.</span></span>  <span data-ttu-id="1155d-212">Bu bir saat, ancak içeremez hello kullanıcı toospecify hello gereksinimini kaldırır çözümünüzdeki hello çözüm kaldırıldığında kaldırılacak şekilde hello zamanlama.</span><span class="sxs-lookup"><span data-stu-id="1155d-212">This removes hello requirement of hello user toospecify a time, but you can't contain hello schedule in your solution so it will be removed when hello solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="1155d-213">İş zamanlamaları</span><span class="sxs-lookup"><span data-stu-id="1155d-213">Job schedules</span></span>
<span data-ttu-id="1155d-214">İş zamanlaması kaynakları runbook zamanlama ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="1155d-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="1155d-215">Bir türüne sahip **Microsoft.Automation/automationAccounts/jobSchedules** ve yapı izlenerek hello hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1155d-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have hello hello following structure.</span></span>  <span data-ttu-id="1155d-216">Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir.</span><span class="sxs-lookup"><span data-stu-id="1155d-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
      "type": "microsoft.automation/automationAccounts/jobSchedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
        "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
      ],
      "tags": {
      },
      "properties": {
        "schedule": {
          "name": "[variables('Schedule').Name]"
        },
        "runbook": {
          "name": "[variables('Runbook').Name]"
        }
      }
    }


<span data-ttu-id="1155d-217">İş zamanlamaları Hello özelliklerini aşağıdaki tablonun hello açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1155d-217">hello properties for job schedules are described in hello following table.</span></span>

| <span data-ttu-id="1155d-218">Özellik</span><span class="sxs-lookup"><span data-stu-id="1155d-218">Property</span></span> | <span data-ttu-id="1155d-219">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1155d-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1155d-220">Zamanlama adı</span><span class="sxs-lookup"><span data-stu-id="1155d-220">schedule name</span></span> |<span data-ttu-id="1155d-221">Tek **adı** hello tablosunun hello adı olan varlık.</span><span class="sxs-lookup"><span data-stu-id="1155d-221">Single **name** entity with hello name of hello schedule.</span></span> |
| <span data-ttu-id="1155d-222">runbook adı</span><span class="sxs-lookup"><span data-stu-id="1155d-222">runbook name</span></span>  |<span data-ttu-id="1155d-223">Tek **adı** hello runbook'un hello ada sahip varlık.</span><span class="sxs-lookup"><span data-stu-id="1155d-223">Single **name** entity with hello name of hello runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="1155d-224">Değişkenler</span><span class="sxs-lookup"><span data-stu-id="1155d-224">Variables</span></span>
<span data-ttu-id="1155d-225">[Azure Otomasyon değişkenleri](../automation/automation-variables.md) bir türüne sahip **Microsoft.Automation/automationAccounts/variables** ve yapı izlenerek hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1155d-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have hello following structure.</span></span>  <span data-ttu-id="1155d-226">Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir.</span><span class="sxs-lookup"><span data-stu-id="1155d-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
      "type": "microsoft.automation/automationAccounts/variables",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Variable').Description]",
        "isEncrypted": "[variables('Variable').Encrypted]",
        "type": "[variables('Variable').Type]",
        "value": "[variables('Variable').Value]"
      }
    }

<span data-ttu-id="1155d-227">Aşağıdaki tablonun hello değişken kaynakların Hello özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1155d-227">hello properties for variable resources are described in hello following table.</span></span>

| <span data-ttu-id="1155d-228">Özellik</span><span class="sxs-lookup"><span data-stu-id="1155d-228">Property</span></span> | <span data-ttu-id="1155d-229">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1155d-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1155d-230">açıklama</span><span class="sxs-lookup"><span data-stu-id="1155d-230">description</span></span> | <span data-ttu-id="1155d-231">Merhaba değişkeni için isteğe bağlı bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="1155d-231">Optional description for hello variable.</span></span> |
| <span data-ttu-id="1155d-232">Isencrypted</span><span class="sxs-lookup"><span data-stu-id="1155d-232">isEncrypted</span></span> | <span data-ttu-id="1155d-233">Merhaba değişkeni şifrelenmesi gerekip gerekmediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1155d-233">Specifies whether hello variable should be encrypted.</span></span> |
| <span data-ttu-id="1155d-234">type</span><span class="sxs-lookup"><span data-stu-id="1155d-234">type</span></span> | <span data-ttu-id="1155d-235">Bu özellik şu anda hiçbir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="1155d-235">This property currently has no effect.</span></span>  <span data-ttu-id="1155d-236">Hello hello değişkeninin veri türü hello ilk değeri tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="1155d-236">hello data type of hello variable will be determined by hello initial value.</span></span> |
| <span data-ttu-id="1155d-237">değer</span><span class="sxs-lookup"><span data-stu-id="1155d-237">value</span></span> | <span data-ttu-id="1155d-238">Merhaba değişken değeri.</span><span class="sxs-lookup"><span data-stu-id="1155d-238">Value for hello variable.</span></span> |

> [!NOTE]
> <span data-ttu-id="1155d-239">Merhaba **türü** özelliği şu anda hiçbir etkisi oluşturulmakta hello değişkeni.</span><span class="sxs-lookup"><span data-stu-id="1155d-239">hello **type** property currently has no effect on hello variable being created.</span></span>  <span data-ttu-id="1155d-240">Merhaba veri türü hello değişkeni için hello değeri tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="1155d-240">hello data type for hello variable will be determined by hello value.</span></span>  

<span data-ttu-id="1155d-241">Merhaba değişken hello ilk değeri ayarlarsanız, hello doğru veri türü olarak yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1155d-241">If you set hello initial value for hello variable, it must be configured as hello correct data type.</span></span>  <span data-ttu-id="1155d-242">Aşağıdaki tablonun hello hello farklı veri türlerine izin verilen ve bunların sözdizimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1155d-242">hello following table provides hello different data types allowable and their syntax.</span></span>  <span data-ttu-id="1155d-243">JSON değerlerde beklenen tooalways olduğunu unutmayın hello tırnak işareti içinde özel karakterler ile tırnak içine alınması.</span><span class="sxs-lookup"><span data-stu-id="1155d-243">Note that values in JSON are expected tooalways be enclosed in quotes with any special characters within hello quotes.</span></span>  <span data-ttu-id="1155d-244">Örneğin, bir dize değeri hello dize tırnak tarafından belirtilmesi (Merhaba kaçış karakteri kullanarak (\\)) sırada sayısal bir değer tek tırnak işareti kümesiyle belirtilmesi.</span><span class="sxs-lookup"><span data-stu-id="1155d-244">For example, a string value would be specified by quotes around hello string (using hello escape character (\\)) while a numeric value would be specified with one set of quotes.</span></span>

| <span data-ttu-id="1155d-245">Veri türü</span><span class="sxs-lookup"><span data-stu-id="1155d-245">Data type</span></span> | <span data-ttu-id="1155d-246">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1155d-246">Description</span></span> | <span data-ttu-id="1155d-247">Örnek</span><span class="sxs-lookup"><span data-stu-id="1155d-247">Example</span></span> | <span data-ttu-id="1155d-248">Çok çözümler</span><span class="sxs-lookup"><span data-stu-id="1155d-248">Resolves too</span></span>|
|:--|:--|:--|:--|
| <span data-ttu-id="1155d-249">Dize</span><span class="sxs-lookup"><span data-stu-id="1155d-249">string</span></span>   | <span data-ttu-id="1155d-250">Değeri çift tırnak içine alın.</span><span class="sxs-lookup"><span data-stu-id="1155d-250">Enclose value in double quotes.</span></span>  | <span data-ttu-id="1155d-251">"\"Merhaba Dünya\""</span><span class="sxs-lookup"><span data-stu-id="1155d-251">"\"Hello world\""</span></span> | <span data-ttu-id="1155d-252">"Hello world"</span><span class="sxs-lookup"><span data-stu-id="1155d-252">"Hello world"</span></span> |
| <span data-ttu-id="1155d-253">sayısal</span><span class="sxs-lookup"><span data-stu-id="1155d-253">numeric</span></span>  | <span data-ttu-id="1155d-254">Tek tırnak sahip bir sayısal değer.</span><span class="sxs-lookup"><span data-stu-id="1155d-254">Numeric value with single quotes.</span></span>| <span data-ttu-id="1155d-255">"64"</span><span class="sxs-lookup"><span data-stu-id="1155d-255">"64"</span></span> | <span data-ttu-id="1155d-256">64</span><span class="sxs-lookup"><span data-stu-id="1155d-256">64</span></span> |
| <span data-ttu-id="1155d-257">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="1155d-257">boolean</span></span>  | <span data-ttu-id="1155d-258">**doğru** veya **false** tırnak.</span><span class="sxs-lookup"><span data-stu-id="1155d-258">**true** or **false** in quotes.</span></span>  <span data-ttu-id="1155d-259">Bu değer küçük harfli olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1155d-259">Note that this value must be lowercase.</span></span> | <span data-ttu-id="1155d-260">"true"</span><span class="sxs-lookup"><span data-stu-id="1155d-260">"true"</span></span> | <span data-ttu-id="1155d-261">TRUE</span><span class="sxs-lookup"><span data-stu-id="1155d-261">true</span></span> |
| <span data-ttu-id="1155d-262">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="1155d-262">datetime</span></span> | <span data-ttu-id="1155d-263">Serileştirilmiş tarih değeri.</span><span class="sxs-lookup"><span data-stu-id="1155d-263">Serialized date value.</span></span><br><span data-ttu-id="1155d-264">Bu değer için belirli bir tarih PowerShell toogenerate hello ConvertTo-Json cmdlet'ini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1155d-264">You can use hello ConvertTo-Json cmdlet in PowerShell toogenerate this value for a particular date.</span></span><br><span data-ttu-id="1155d-265">Örnek: get-date "24/5/2017 13:14:57" \\</span><span class="sxs-lookup"><span data-stu-id="1155d-265">Example: get-date "5/24/2017 13:14:57" \\</span></span>| <span data-ttu-id="1155d-266">ConvertTo-Json</span><span class="sxs-lookup"><span data-stu-id="1155d-266">ConvertTo-Json</span></span> | <span data-ttu-id="1155d-267">"\\/Date(1495656897378)\\/"</span><span class="sxs-lookup"><span data-stu-id="1155d-267">"\\/Date(1495656897378)\\/"</span></span> | <span data-ttu-id="1155d-268">2017-05-24 13:14:57</span><span class="sxs-lookup"><span data-stu-id="1155d-268">2017-05-24 13:14:57</span></span> |

## <a name="modules"></a><span data-ttu-id="1155d-269">Modüller</span><span class="sxs-lookup"><span data-stu-id="1155d-269">Modules</span></span>
<span data-ttu-id="1155d-270">Yönetim çözümünüzü toodefine gerekmez [genel modülleri](../automation/automation-integration-modules.md) bunlar her zaman Otomasyon hesabınızda kullanılabilir olacağından, runbook'lar tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1155d-270">Your management solution does not need toodefine [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="1155d-271">Runbook'lar tarafından kullanılan başka bir modül için bir kaynak tooinclude gerekir.</span><span class="sxs-lookup"><span data-stu-id="1155d-271">You do need tooinclude a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="1155d-272">[Tümleştirme modülleri](../automation/automation-integration-modules.md) bir türüne sahip **Microsoft.Automation/automationAccounts/modules** ve yapı izlenerek hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1155d-272">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have hello following structure.</span></span>  <span data-ttu-id="1155d-273">Kopyalayabilir ve çözüm dosyanıza Bu kod parçacığını yapıştırın ve hello parametre adlarını değiştirmek için bu ortak değişkenleri ve parametreleri içerir.</span><span class="sxs-lookup"><span data-stu-id="1155d-273">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
      "type": "Microsoft.Automation/automationAccounts/modules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "dependsOn": [
      ],
      "properties": {
        "contentLink": {
          "uri": "[variables('Module').Uri]"
        }
      }
    }


<span data-ttu-id="1155d-274">Aşağıdaki tablonun hello modülü kaynakların Hello özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1155d-274">hello properties for module resources are described in hello following table.</span></span>

| <span data-ttu-id="1155d-275">Özellik</span><span class="sxs-lookup"><span data-stu-id="1155d-275">Property</span></span> | <span data-ttu-id="1155d-276">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1155d-276">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1155d-277">contentLink</span><span class="sxs-lookup"><span data-stu-id="1155d-277">contentLink</span></span> |<span data-ttu-id="1155d-278">Merhaba modülü Merhaba içeriğine belirtir.</span><span class="sxs-lookup"><span data-stu-id="1155d-278">Specifies hello content of hello module.</span></span> <br><br><span data-ttu-id="1155d-279">URI - hello modülü URI toohello içeriği.</span><span class="sxs-lookup"><span data-stu-id="1155d-279">uri - Uri toohello content of hello module.</span></span>  <span data-ttu-id="1155d-280">Bu, PowerShell ve komut dosyası runbook'lar için bir .ps1 dosyası ve bir grafik runbook'u dışarı aktarılan grafik runbook dosyası olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1155d-280">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="1155d-281">Sürüm - hello modülü kendi izleme sürümü.</span><span class="sxs-lookup"><span data-stu-id="1155d-281">version - Version of hello module for your own tracking.</span></span> |

<span data-ttu-id="1155d-282">Merhaba runbook hello runbook önce oluşturduğu hello modülü kaynak tooensure bağlı.</span><span class="sxs-lookup"><span data-stu-id="1155d-282">hello runbook should depend on hello module resource tooensure that it's created before hello runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="1155d-283">Modülleri güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="1155d-283">Updating modules</span></span>
<span data-ttu-id="1155d-284">Bir zamanlama kullanan bir runbook içeren bir yönetim çözümü güncelleştirin ve bu runbook tarafından kullanılan yeni bir modül çözümünüzün hello yeni sürüme sahip hello runbook hello modülü eski sürümü hello kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="1155d-284">If you update a management solution that includes a runbook that uses a schedule, and hello new version of your solution has a new module used by that runbook, then hello runbook may use hello old version of hello module.</span></span>  <span data-ttu-id="1155d-285">Runbook'ları çözümünüzdeki aşağıdaki hello içerir ve iş toorun oluşturmak diğer runbook'lar önce.</span><span class="sxs-lookup"><span data-stu-id="1155d-285">You should include hello following runbooks in your solution and create a job toorun them before any other runbooks.</span></span>  <span data-ttu-id="1155d-286">Bu, herhangi bir modül runbook'lar yüklenen önce gerekli hello güncelleştirildiğini güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="1155d-286">This will ensure that any modules are updated as required before hello runbooks are loaded.</span></span>

* <span data-ttu-id="1155d-287">[Güncelleştirme ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) tüm runbook'ları çözümünüzdeki tarafından kullanılan hello modülleri hello en son sürümü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="1155d-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of hello modules used by runbooks in your solution are hello latest version.</span></span>  
* <span data-ttu-id="1155d-288">[ReRegisterAutomationSchedule MS Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) tüm hello runbook'ları kullanmak hello son modüllerle toothem bağlı hello zamanlama kaynakları tooensure yeniden kaydettirin.</span><span class="sxs-lookup"><span data-stu-id="1155d-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of hello schedule resources tooensure that hello runbooks linked toothem with use hello latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="1155d-289">Örnek</span><span class="sxs-lookup"><span data-stu-id="1155d-289">Sample</span></span>
<span data-ttu-id="1155d-290">Aşağıdaki kaynakları izleyerek hello içeren içeren bir çözüm örneğidir:</span><span class="sxs-lookup"><span data-stu-id="1155d-290">Following is a sample of a solution that include that includes hello following resources:</span></span>

- <span data-ttu-id="1155d-291">Runbook.</span><span class="sxs-lookup"><span data-stu-id="1155d-291">Runbook.</span></span>  <span data-ttu-id="1155d-292">Ortak bir GitHub deposunda bulunan bir örnek runbook budur.</span><span class="sxs-lookup"><span data-stu-id="1155d-292">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="1155d-293">Merhaba çözüm yüklendiğinde hello runbook başlatır Otomasyonu işi.</span><span class="sxs-lookup"><span data-stu-id="1155d-293">Automation job that starts hello runbook when hello solution is installed.</span></span>
- <span data-ttu-id="1155d-294">Zamanlama ve iş toostart hello runbook düzenli aralıklarla zamanlayın.</span><span class="sxs-lookup"><span data-stu-id="1155d-294">Schedule and job schedule toostart hello runbook at regular intervals.</span></span>
- <span data-ttu-id="1155d-295">Sertifika.</span><span class="sxs-lookup"><span data-stu-id="1155d-295">Certificate.</span></span>
- <span data-ttu-id="1155d-296">Kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="1155d-296">Credential.</span></span>
- <span data-ttu-id="1155d-297">Değişkeni.</span><span class="sxs-lookup"><span data-stu-id="1155d-297">Variable.</span></span>
- <span data-ttu-id="1155d-298">Modül.</span><span class="sxs-lookup"><span data-stu-id="1155d-298">Module.</span></span>  <span data-ttu-id="1155d-299">Merhaba budur [OMSIngestionAPI Modülü](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) veri tooLog Analytics yazma.</span><span class="sxs-lookup"><span data-stu-id="1155d-299">This is hello [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data tooLog Analytics.</span></span> 

<span data-ttu-id="1155d-300">Merhaba örnek kullanır [standart çözüm parametreleri](operations-management-suite-solutions-solution-file.md#parameters) bir çözüm olarak, yaygın olarak kullanılacak değişkenleri toohardcoding değerleri hello kaynak tanımlarında değil.</span><span class="sxs-lookup"><span data-stu-id="1155d-300">hello sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed toohardcoding values in hello resource definitions.</span></span>


    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "workspaceName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Log Analytics workspace."
          }
        },
        "accountName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Automation account."
          }
        },
        "workspaceregionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Log Analytics workspace."
          }
        },
        "regionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Automation account."
          }
        },
        "pricingTier": {
          "type": "string",
          "metadata": {
            "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account."
          }
        },
        "certificateBase64Value": {
          "type": "string",
          "metadata": {
            "Description": "Base 64 value for certificate."
          }
        },
        "certificateThumbprint": {
          "type": "securestring",
          "metadata": {
            "Description": "Thumbprint for certificate."
          }
        },
        "credentialUsername": {
          "type": "string",
          "metadata": {
            "Description": "Username for credential."
          }
        },
        "credentialPassword": {
          "type": "securestring",
          "metadata": {
            "Description": "Password for credential."
          }
        },
        "scheduleStartTime": {
          "type": "string",
          "metadata": {
            "Description": "Start time for shedule."
          }
        },
        "scheduleTimeZone": {
          "type": "string",
          "metadata": {
            "Description": "Time zone for schedule."
          }
        },
        "scheduleLinkGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello schedule link toorunbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello runbook job.",
            "control": "guid"
          }
        }
      },
      "variables": {
        "SolutionName": "MySolution",
        "SolutionVersion": "1.0",
        "SolutionPublisher": "Contoso",
        "ProductName": "SampleSolution",
    
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31",
    
        "Runbook": {
          "Name": "MyRunbook",
          "Description": "Sample runbook",
          "Type": "PowerShell",
          "Uri": "https://raw.githubusercontent.com/user/myrepo/master/samples/MyRunbook.ps1",
          "JobGuid": "[parameters('runbookJobGuid')]"
        },
    
        "Certificate": {
          "Name": "MyCertificate",
          "Base64Value": "[parameters('certificateBase64Value')]",
          "Thumbprint": "[parameters('certificateThumbprint')]"
        },
    
        "Credential": {
          "Name": "MyCredential",
          "UserName": "[parameters('credentialUsername')]",
          "Password": "[parameters('credentialPassword')]"
        },
    
        "Schedule": {
          "Name": "MySchedule",
          "Description": "Sample schedule",
          "IsEnabled": "true",
          "Interval": "1",
          "Frequency": "hour",
          "StartTime": "[parameters('scheduleStartTime')]",
          "TimeZone": "[parameters('scheduleTimeZone')]",
          "LinkGuid": "[parameters('scheduleLinkGuid')]"
        },
    
        "Variable": {
          "Name": "MyVariable",
          "Description": "Sample variable",
          "Encrypted": 0,
          "Type": "string",
          "Value": "'This is my string value.'"
        },
    
        "Module": {
          "Name": "OMSIngestionAPI",
          "Uri": "https://devopsgallerystorage.blob.core.windows.net/packages/omsingestionapi.1.3.0.nupkg"
        }
      },
      "resources": [
        {
          "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
          "location": "[parameters('workspaceRegionId')]",
          "tags": { },
          "type": "Microsoft.OperationsManagement/solutions",
          "apiVersion": "[variables('LogAnalyticsApiVersion')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
            "referencedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
            ],
            "containedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]"
            ]
          },
          "plan": {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
            "Version": "[variables('SolutionVersion')]",
            "product": "[variables('ProductName')]",
            "publisher": "[variables('SolutionPublisher')]",
            "promotionCode": ""
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
          "type": "Microsoft.Automation/automationAccounts/runbooks",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "location": "[parameters('regionId')]",
          "tags": { },
          "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
              "uri": "[variables('Runbook').Uri]",
              "version": "1.0.0.0"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').JobGuid)]",
          "type": "Microsoft.Automation/automationAccounts/jobs",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
          ],
          "tags": { },
          "properties": {
            "runbook": {
              "name": "[variables('Runbook').Name]"
            },
            "parameters": {
              "targetSubscriptionId": "[subscription().subscriptionId]",
              "resourcegroup": "[resourceGroup().name]",
              "automationaccount": "[parameters('accountName')]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
          "type": "Microsoft.Automation/automationAccounts/certificates",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "Base64Value": "[variables('Certificate').Base64Value]",
            "Thumbprint": "[variables('Certificate').Thumbprint]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
          "type": "Microsoft.Automation/automationAccounts/credentials",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "userName": "[variables('Credential').UserName]",
            "password": "[variables('Credential').Password]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
          "type": "microsoft.automation/automationAccounts/schedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Schedule').Description]",
            "startTime": "[variables('Schedule').StartTime]",
            "timeZone": "[variables('Schedule').TimeZone]",
            "isEnabled": "[variables('Schedule').IsEnabled]",
            "interval": "[variables('Schedule').Interval]",
            "frequency": "[variables('Schedule').Frequency]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
          "type": "microsoft.automation/automationAccounts/jobSchedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
          ],
          "tags": {
          },
          "properties": {
            "schedule": {
              "name": "[variables('Schedule').Name]"
            },
            "runbook": {
              "name": "[variables('Runbook').Name]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
          "type": "microsoft.automation/automationAccounts/variables",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Variable').Description]",
            "isEncrypted": "[variables('Variable').Encrypted]",
            "type": "[variables('Variable').Type]",
            "value": "[variables('Variable').Value]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
          "type": "Microsoft.Automation/automationAccounts/modules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "properties": {
            "contentLink": {
              "uri": "[variables('Module').Uri]"
            }
          }
        }
    
      ],
      "outputs": { }
    }




## <a name="next-steps"></a><span data-ttu-id="1155d-301">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1155d-301">Next steps</span></span>
* <span data-ttu-id="1155d-302">[Görünüm tooyour çözüm eklemek](operations-management-suite-solutions-resources-views.md) toovisualize toplanan verileri.</span><span class="sxs-lookup"><span data-stu-id="1155d-302">[Add a view tooyour solution](operations-management-suite-solutions-resources-views.md) toovisualize collected data.</span></span>
