---
title: aaaPass bir JSON nesnesi tooan Azure Otomasyonu runbook | Microsoft Docs
description: "Nasıl bir JSON nesnesi olarak toopass parametreleri tooa runbook"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: PowerShell runbook, json, azure Otomasyonu
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 8229a16015d549927ead5496c70e9fb391d35498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="pass-a-json-object-tooan-azure-automation-runbook"></a><span data-ttu-id="2ff37-104">Bir JSON nesnesi tooan Azure Otomasyon runbook'u geçirin</span><span class="sxs-lookup"><span data-stu-id="2ff37-104">Pass a JSON object tooan Azure Automation runbook</span></span>

<span data-ttu-id="2ff37-105">Bir JSON dosyası toopass tooa runbook'ta istediğiniz yararlı toostore verileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="2ff37-105">It can be useful toostore data that you want toopass tooa runbook in a JSON file.</span></span>
<span data-ttu-id="2ff37-106">Örneğin, tüm başlangıç parametreleri içeren bir JSON dosyası oluşturabilirsiniz toopass tooa runbook istiyor.</span><span class="sxs-lookup"><span data-stu-id="2ff37-106">For example, you might create a JSON file that contains all of hello parameters you want toopass tooa runbook.</span></span>
<span data-ttu-id="2ff37-107">toodo bunu tooconvert hello JSON tooa dizesine sahip ve ardından, içeriği toohello runbook geçirmeden önce hello dize tooa PowerShell nesnesi dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="2ff37-107">toodo this, you have tooconvert hello JSON tooa string and then convert hello string tooa PowerShell object before passing its contents toohello runbook.</span></span>

<span data-ttu-id="2ff37-108">Bu örnekte, çağıran bir PowerShell komut dosyası oluşturacağız [başlangıç AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart hello JSON toohello runbook Merhaba içeriğine geçirme bir PowerShell runbook.</span><span class="sxs-lookup"><span data-stu-id="2ff37-108">In this example, we'll create a PowerShell script that calls [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart a PowerShell runbook, passing hello contents of hello JSON toohello runbook.</span></span>
<span data-ttu-id="2ff37-109">Merhaba PowerShell runbook hello geçirildi JSON öğesinden Merhaba VM hello parametreler alınırken bir Azure VM başlatır.</span><span class="sxs-lookup"><span data-stu-id="2ff37-109">hello PowerShell runbook starts an Azure VM, getting hello parameters for hello VM from hello JSON that was passed in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ff37-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2ff37-110">Prerequisites</span></span>
<span data-ttu-id="2ff37-111">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2ff37-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="2ff37-112">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="2ff37-112">Azure subscription.</span></span> <span data-ttu-id="2ff37-113">Henüz bir aboneliğiniz yoksa [MSDN abone avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ya da <a href="/pricing/free-account/" target="_blank">[ücretsiz hesap için kaydolabilirsiniz](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="2ff37-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="2ff37-114">[Otomasyon hesabı](automation-sec-configure-azure-runas-account.md) toohold runbook hello ve tooAzure kaynakları kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="2ff37-114">[Automation account](automation-sec-configure-azure-runas-account.md) toohold hello runbook and authenticate tooAzure resources.</span></span>  <span data-ttu-id="2ff37-115">Bu hesap, izin toostart sahip ve hello sanal makineyi durdurun.</span><span class="sxs-lookup"><span data-stu-id="2ff37-115">This account must have permission toostart and stop hello virtual machine.</span></span>
* <span data-ttu-id="2ff37-116">Azure sanal makinesi.</span><span class="sxs-lookup"><span data-stu-id="2ff37-116">An Azure virtual machine.</span></span> <span data-ttu-id="2ff37-117">Bu makineyi durdurup başlatacağımız için makinenin üretime yönelik bir VM olmaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ff37-117">We stop and start this machine so it should not be a production VM.</span></span>
* <span data-ttu-id="2ff37-118">Azure Powershell yerel makine üzerinde yüklü.</span><span class="sxs-lookup"><span data-stu-id="2ff37-118">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="2ff37-119">Bkz [yükleyin ve Azure Powershell yapılandırma](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) hakkında bilgi için Azure PowerShell tooget.</span><span class="sxs-lookup"><span data-stu-id="2ff37-119">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how tooget Azure PowerShell.</span></span>

## <a name="create-hello-json-file"></a><span data-ttu-id="2ff37-120">Merhaba JSON dosyası oluşturun</span><span class="sxs-lookup"><span data-stu-id="2ff37-120">Create hello JSON file</span></span>

<span data-ttu-id="2ff37-121">Türü hello aşağıdakileri bir metin dosyasına test ve olarak kaydedin `test.json` yerel bilgisayarınızdaki herhangi bir yerde.</span><span class="sxs-lookup"><span data-stu-id="2ff37-121">Type hello following test in a text file, and save it as `test.json` somewhere on your local computer.</span></span>

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-hello-runbook"></a><span data-ttu-id="2ff37-122">Merhaba runbook oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ff37-122">Create hello runbook</span></span>

<span data-ttu-id="2ff37-123">"Test-Json" Azure Automation adlı yeni bir PowerShell runbook oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2ff37-123">Create a new PowerShell runbook named "Test-Json" in Azure Automation.</span></span>
<span data-ttu-id="2ff37-124">toocreate yeni bir PowerShell runbook nasıl görürüm toolearn [ilk PowerShell runbook'um](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2ff37-124">toolearn how toocreate a new PowerShell runbook, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>

<span data-ttu-id="2ff37-125">tooaccept hello JSON verilerini hello runbook giriş parametresi olarak bir nesne almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ff37-125">tooaccept hello JSON data, hello runbook must take an object as an input parameter.</span></span>

<span data-ttu-id="2ff37-126">Merhaba runbook sonra hello JSON tanımlanan hello özelliklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ff37-126">hello runbook can then use hello properties defined in hello JSON.</span></span>

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect tooAzure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object tooactual JSON
$json = $json | ConvertFrom-Json

# Use hello values from hello JSON object as hello parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 <span data-ttu-id="2ff37-127">Kaydedin ve bu runbook Otomasyon hesabınızda yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="2ff37-127">Save and publish this runbook in your Automation account.</span></span>

## <a name="call-hello-runbook-from-powershell"></a><span data-ttu-id="2ff37-128">PowerShell hello runbook'tan çağrı</span><span class="sxs-lookup"><span data-stu-id="2ff37-128">Call hello runbook from PowerShell</span></span>

<span data-ttu-id="2ff37-129">Artık Azure PowerShell kullanarak yerel makinenizden hello runbook çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ff37-129">Now you can call hello runbook from your local machine by using Azure PowerShell.</span></span>
<span data-ttu-id="2ff37-130">Merhaba aşağıdaki PowerShell komutlarını çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2ff37-130">Run hello following PowerShell commands:</span></span>

1. <span data-ttu-id="2ff37-131">İçinde tooAzure oturum:</span><span class="sxs-lookup"><span data-stu-id="2ff37-131">Log in tooAzure:</span></span>
   ```powershell
   Login-AzureRmAccount
   ```
    <span data-ttu-id="2ff37-132">Azure kimlik bilgileriniz istendiğinde tooenter şunlardır.</span><span class="sxs-lookup"><span data-stu-id="2ff37-132">You are prompted tooenter your Azure credentials.</span></span>
1. <span data-ttu-id="2ff37-133">Merhaba hello JSON dosyasının içeriğini alın ve tooa dize Dönüştür:</span><span class="sxs-lookup"><span data-stu-id="2ff37-133">Get hello contents of hello JSON file and convert it tooa string:</span></span>
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    <span data-ttu-id="2ff37-134">`JsonPath`Merhaba JSON dosyasını kaydettiğiniz hello yolu değil.</span><span class="sxs-lookup"><span data-stu-id="2ff37-134">`JsonPath` is hello path where you saved hello JSON file.</span></span>
1. <span data-ttu-id="2ff37-135">Merhaba dize içeriğini Dönüştür `$json` tooa PowerShell nesnesi:</span><span class="sxs-lookup"><span data-stu-id="2ff37-135">Convert hello string contents of `$json` tooa PowerShell object:</span></span>
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. <span data-ttu-id="2ff37-136">Merhaba parametreleri için bir karma tablosu oluşturma `Start-AzureRmAutomstionRunbook`:</span><span class="sxs-lookup"><span data-stu-id="2ff37-136">Create a hashtable for hello parameters for `Start-AzureRmAutomstionRunbook`:</span></span>
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   <span data-ttu-id="2ff37-137">Merhaba değerini ayarlama fark `Parameters` hello JSON dosyası hello değerleri içeren toohello PowerShell nesnesi.</span><span class="sxs-lookup"><span data-stu-id="2ff37-137">Notice that you are setting hello value of `Parameters` toohello PowerShell object that contains hello values from hello JSON file.</span></span> 
1. <span data-ttu-id="2ff37-138">Merhaba runbook başlatın</span><span class="sxs-lookup"><span data-stu-id="2ff37-138">Start hello runbook</span></span>
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

<span data-ttu-id="2ff37-139">Merhaba runbook hello JSON dosyasını toostart VM hello değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="2ff37-139">hello runbook uses hello values from hello JSON file toostart a VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ff37-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2ff37-140">Next steps</span></span>

* <span data-ttu-id="2ff37-141">bir metin düzenleyicisiyle PowerShell ve PowerShell iş akışı runbook'ları düzenleme hakkında daha fazla toolearn bakın [Azure Otomasyonu'nda metinsel runbook'lar düzenleme](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="2ff37-141">toolearn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span> 
* <span data-ttu-id="2ff37-142">oluşturma ve runbook'ları, içeri aktarma hakkında daha fazla toolearn bakın [oluşturma veya bir Azure Otomasyonu runbook'u içeri aktarma](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="2ff37-142">toolearn more about creating and importing runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>


