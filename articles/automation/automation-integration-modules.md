---
title: "bir Azure Automation tümleştirme modülü aaaCreate | Microsoft Docs"
description: "Öğretici, Azure Automation tümleştirme modülleri hello oluşturma, test ve örnek kullanımı aracılığıyla yol göstermektedir."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 27798efb-08b9-45d9-9b41-5ad91a3df41e
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/13/2017
ms.author: magoedte
ms.openlocfilehash: d4064d8b106496f4dab442024131886c4affccab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-integration-modules"></a><span data-ttu-id="3e4c5-103">Azure Automation Tümleştirme Modülleri</span><span class="sxs-lookup"><span data-stu-id="3e4c5-103">Azure Automation Integration Modules</span></span>
<span data-ttu-id="3e4c5-104">PowerShell hello temel Azure Automation'un ardındaki teknolojidir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-104">PowerShell is hello fundamental technology behind Azure Automation.</span></span> <span data-ttu-id="3e4c5-105">Azure Automation PowerShell üzerine kurulu olmadığından, PowerShell modülleri Azure Automation'un genişletilmesinde anahtar toohello ' dir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-105">Since Azure Automation is built on PowerShell, PowerShell modules are key toohello extensibility of Azure Automation.</span></span> <span data-ttu-id="3e4c5-106">Bu makalede, biz PowerShell modülleri Azure Otomasyonu'nun kullanımını hello özellikleri yönlendirecek, tooas "Tümleştirme modülleri" denir ve bunlar tümleştirme modülü olarak çalışmalarını kendi PowerShell modülleri toomake oluşturmak için en iyi yöntemler Azure Otomasyonu.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-106">In this article, we will guide you through hello specifics of Azure Automation’s use of PowerShell modules, referred tooas “Integration Modules”, and best practices for creating your own PowerShell modules toomake sure they work as Integration Modules within Azure Automation.</span></span> 

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="3e4c5-107">PowerShell Modülü nedir?</span><span class="sxs-lookup"><span data-stu-id="3e4c5-107">What is a PowerShell Module?</span></span>
<span data-ttu-id="3e4c5-108">PowerShell modülü PowerShell cmdlet'leri gibi oluşan bir gruptur **Get-Date** veya **Copy-Item**kullanılabilecek hello PowerShell konsolunu, komut dosyaları, iş akışları, runbook'ları ve gibi PowerShell DSC kaynakları WindowsFeature veya PowerShell DSC kaynaklarından kullanılabilen dosya.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-108">A PowerShell module is a group of PowerShell cmdlets like **Get-Date** or **Copy-Item**, that can be used from hello PowerShell console, scripts, workflows, runbooks, and PowerShell DSC resources like WindowsFeature or File, that can be used from PowerShell DSC configurations.</span></span> <span data-ttu-id="3e4c5-109">PowerShell hello işlevlerin gösterilir cmdlet'ler ve DSC kaynakları ve her cmdlet/DSC kaynağı bir PowerShell modülü tarafından desteklenir, PowerShell ile birlikte birçoğu.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-109">All of hello functionality of PowerShell is exposed through cmdlets and DSC resources, and every cmdlet/DSC resource is backed by a PowerShell module, many of which ship with PowerShell itself.</span></span> <span data-ttu-id="3e4c5-110">Örneğin, hello **Get-Date** cmdlet hello Microsoft.PowerShell.Utility PowerShell modülünün bir parçasıdır ve **Copy-Item** cmdlet hello Microsoft.PowerShell.Management PowerShell modülünün bir parçasıdır ve Merhaba paket DSC kaynağı da PSDesiredStateConfiguration PowerShell modülünün hello bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-110">For example, hello **Get-Date** cmdlet is part of hello Microsoft.PowerShell.Utility PowerShell module, and **Copy-Item** cmdlet is part of hello Microsoft.PowerShell.Management PowerShell module and hello Package DSC resource is part of hello PSDesiredStateConfiguration PowerShell module.</span></span> <span data-ttu-id="3e4c5-111">Bu modüllerin her ikisi de PowerShell ile birlikte verilir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-111">Both of these modules ship with PowerShell.</span></span> <span data-ttu-id="3e4c5-112">Ancak çok sayıda PowerShell modülü PowerShell bir parçası olarak bulunmaz ve bunun yerine PowerShell Galerisi gibi yerlerde hello geniş PowerShell topluluğu tarafından veya System Center 2012 Configuration Manager gibi birinci veya üçüncü taraf ürünleri ile dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-112">But many PowerShell modules do not ship as part of PowerShell, and are instead distributed with first or third-party products like System Center 2012 Configuration Manager or by hello vast PowerShell community on places like PowerShell Gallery.</span></span>  <span data-ttu-id="3e4c5-113">karmaşık görevleri kapsüllenmiş işlevler aracılığıyla daha basit hale hello modülleri yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-113">hello modules are useful because they make complex tasks simpler through encapsulated functionality.</span></span>  <span data-ttu-id="3e4c5-114">Daha fazla bilgiyi [MSDN'de PowerShell modülleri](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx) konusunda bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-114">You can learn more about [PowerShell modules on MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span></span> 

## <a name="what-is-an-azure-automation-integration-module"></a><span data-ttu-id="3e4c5-115">Azure Automation Tümleştirme Modülü nedir?</span><span class="sxs-lookup"><span data-stu-id="3e4c5-115">What is an Azure Automation Integration Module?</span></span>
<span data-ttu-id="3e4c5-116">Tümleştirme Modülü, PowerShell modülünden çok farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-116">An Integration Module isn't very different from a PowerShell module.</span></span> <span data-ttu-id="3e4c5-117">Kendi isteğe bağlı olarak bir ek dosya - runbook'hello modülün cmdlet'leriyle ile kullanılan bir Azure Otomasyonu bağlantı türü toobe belirten bir meta veri dosyası içeren bir PowerShell modülüdür.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-117">Its simply a PowerShell module that optionally contains one additional file - a metadata file specifying an Azure Automation connection type toobe used with hello module's cmdlets in runbooks.</span></span> <span data-ttu-id="3e4c5-118">İsteğe bağlı dosya olsun veya olmasın bu PowerShell modülleri Azure Otomasyonu toomake kendi cmdlet'leri için kullanılabilir runbook'ları ve kullanılabilir, DSC kaynakları içinde DSC yapılandırmalarında kullanılacak kullanmak içine alınabilir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-118">Optional file or not, these PowerShell modules can be imported into Azure Automation toomake their cmdlets available for use within runbooks and their DSC resources available for use within DSC configurations.</span></span> <span data-ttu-id="3e4c5-119">Merhaba perde arkasında Azure Automation bu modülleri depolar ve runbook işi ve DSC derleme işi yürütme süresinde, bunları burada runbook'ların yürütüldüğü, DSC yapılandırmalarının derlenir hello Azure Automation korumalı alanlarına yükler.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-119">Behind hello scenes, Azure Automation stores these modules, and at runbook job and DSC compilation job execution time, loads them into hello Azure Automation sandboxes where runbooks are executed and DSC configurations are compiled.</span></span>  <span data-ttu-id="3e4c5-120">Böylece tooapply DSC yapılandırmaları çalışan makineler bunları çekebilir modüllerdeki DSC kaynakları hello Automation DSC çekme sunucusuna da otomatik olarak yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-120">Any DSC resources in modules are also automatically placed on hello Automation DSC pull server, so that they can be pulled by machines attempting tooapply DSC configurations.</span></span>  

<span data-ttu-id="3e4c5-121">Azure PowerShell modülleri sayısı hello kutusunda Azure Otomasyonu, toouse dışında Azure yönetim hemen başlayabilmeniz ancak ne olursa olsun sistemi, hizmet veya toointegrate ile istediğiniz aracı için PowerShell modülleri içeri aktarabilirsiniz gönderdiğimiz.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-121">We ship a number of Azure  PowerShell modules out of hello box in Azure Automation for you toouse so you can get started automating Azure management right away, but you can import PowerShell modules for whatever system, service, or tool you want toointegrate with.</span></span> 

> [!NOTE]
> <span data-ttu-id="3e4c5-122">Belirli modüller "Genel modülleri" Merhaba Otomasyon hizmeti olarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-122">Certain modules are shipped as “global modules” in hello Automation service.</span></span> <span data-ttu-id="3e4c5-123">Bu genel modüller, otomatik olarak onları tooyour Otomasyon hesabını iter automation hesabı oluşturma ve bunları bazen güncelleştiriyoruz kullanılabilir tooyou ' dir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-123">These global modules are available tooyou when you create an automation account, and we update them sometimes which automatically pushes them out tooyour automation account.</span></span> <span data-ttu-id="3e4c5-124">Bunları istemiyorsanız toobe otomatik güncelleştirilmiş-her zaman alabilir, hello aynı modülü kendiniz ve hello hizmetinde gönderdiğimiz bu modülü hello genel Modül sürümü, önceliğe sahip olur.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-124">If you don’t want them toobe auto-updated, you can always import hello same module yourself, and that will take precedence over hello global module version of that module that we ship in hello service.</span></span> 

<span data-ttu-id="3e4c5-125">Tümleştirme modülü paketini içeri aktarma hello aynı adı hello modülü ve bir .zip uzantısı hello sahip sıkıştırılmış bir dosya biçimidir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-125">hello format in which you import an Integration Module package is a compressed file with hello same name as hello module and a .zip extension.</span></span> <span data-ttu-id="3e4c5-126">Merhaba Windows PowerShell modülünü ve hello modülde varsa bildirim dosyası (.psd1) dahil olmak üzere tüm destek dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-126">It contains hello Windows PowerShell module and any supporting files, including a manifest file (.psd1) if hello module has one.</span></span>

<span data-ttu-id="3e4c5-127">Merhaba modülü bir Azure Otomasyonu bağlantı türü içermesi gerekiyorsa hello ada sahip bir dosya da içermelidir `<ModuleName>-Automation.json` hello bağlantı türü özelliklerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-127">If hello module should contain an Azure Automation connection type, it must also contain a file with hello name `<ModuleName>-Automation.json` that specifies hello connection type properties.</span></span> <span data-ttu-id="3e4c5-128">Bu sıkıştırılmış .zip dosyanızın hello modülü klasör içinde yerleştirilen bir json dosyasıdır ve hello alanları içeren bir "bağlantı" gerekli tooconnect toohello sistemi veya hizmet hello modülü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-128">This is a json file placed within hello module folder of your compressed .zip file, and contains hello fields of a “connection” that is required tooconnect toohello system or service hello module represents.</span></span> <span data-ttu-id="3e4c5-129">Bu sayede Azure Automation’da bağlantı türü oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-129">This will end up creating a connection type in Azure Automation.</span></span> <span data-ttu-id="3e4c5-130">Merhaba alan adları ayarlayabilirsiniz bu dosyayı kullanan türleri, hello alanların şifreli veya hello modülünün hello bağlantı türü için isteğe bağlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-130">Using this file you can set hello field names, types, and whether hello fields should be encrypted and / or optional, for hello connection type of hello module.</span></span> <span data-ttu-id="3e4c5-131">Merhaba, hello json dosyası biçiminde bir şablon verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="3e4c5-131">hello following is a template in hello json file format:</span></span>

```
{ 
   "ConnectionFields": [
   {
      "IsEncrypted":  false,
      "IsOptional":  false,
      "Name":  "ComputerName",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  false,
      "IsOptional":  true,
      "Name":  "Username",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  true,
      "IsOptional":  false,
      "Name":  "Password",
   "TypeName":  "System.String"
   }],
   "ConnectionTypeName":  "DataProtectionManager",
   "IntegrationModuleName":  "DataProtectionManager"
}
```

<span data-ttu-id="3e4c5-132">Service Management Automation dağıttıysanız ve Otomasyon runbook'larınız için tümleştirme modülü paketleri oluşturulan, bilgili tooyou görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-132">If you have deployed Service Management Automation and created Integration Modules packages for your automation runbooks, this should look very familiar tooyou.</span></span> 

## <a name="authoring-best-practices"></a><span data-ttu-id="3e4c5-133">Yazma En İyi Uygulamaları</span><span class="sxs-lookup"><span data-stu-id="3e4c5-133">Authoring Best Practices</span></span>
<span data-ttu-id="3e4c5-134">Tümleştirme modülleri temelde PowerShell modülleri olsa bile yoktur hala pek çok öneririz göz önünde bulundurun toomake bir PowerShell modülü yazarken, Azure Automation'da en kullanışlı.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-134">Even though Integration Modules are essentially PowerShell modules, there’s still a number of things we recommend you consider while authoring a PowerShell module, toomake it most usable in Azure Automation.</span></span> <span data-ttu-id="3e4c5-135">Bunlardan bazıları Azure Automation'a özeldir ve bunlardan bazıları modüllerinizi PowerShell iş akışında iyi iş yararlı yalnızca toomake olduğundan Otomasyon desteklemediğini kullandığınızdan bağımsız olarak.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-135">Some of these are Azure Automation specific, and some of them are useful just toomake your modules work well in PowerShell Workflow, regardless of whether or not you’re using Automation.</span></span> 

1. <span data-ttu-id="3e4c5-136">Merhaba modüldeki her cmdlet için Yardım URI ve bir Özet, açıklama, içerir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-136">Include a synopsis, description, and help URI for every cmdlet in hello module.</span></span> <span data-ttu-id="3e4c5-137">PowerShell'de hello ile kullanma hakkında bazı bilgiler cmdlet'leri tooallow hello kullanıcı tooreceive Yardım tanımlayabilirsiniz **Get-Help** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-137">In PowerShell, you can define certain help information for cmdlets tooallow hello user tooreceive help on using them with hello **Get-Help** cmdlet.</span></span> <span data-ttu-id="3e4c5-138">Örneğin, bir .psm1 dosyasında yazılan PowerShell modülü için bir yardım URI’sını ve özeti nasıl tanımlayacağınız aşağıda anlatılmıştır.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-138">For example, here’s how you can define a synopsis and help URI for a PowerShell module written in a .psm1 file.</span></span><br>  
   
    ```
    <#
        .SYNOPSIS
         Gets all outgoing phone numbers for this Twilio account 
    #>
    function Get-TwilioPhoneNumbers {
    [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
    HelpUri='http://www.twilio.com/docs/api/rest/outgoing-caller-ids')]
    param(
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AccountSid,
   
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AuthToken,
   
       [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [Hashtable]
       $Connection
    )
   
    $cred = CreateTwilioCredential -Connection $Connection -AccountSid $AccountSid -AuthToken $AuthToken
   
    $uri = "$TWILIO_BASE_URL/Accounts/" + $cred.UserName + "/IncomingPhoneNumbers"
   
    $response = Invoke-RestMethod -Method Get -Uri $uri -Credential $cred
   
    $response.TwilioResponse.IncomingPhoneNumbers.IncomingPhoneNumber
    }
    ```
   <br> <span data-ttu-id="3e4c5-139">Bu bilgileri sağlayarak yalnızca gösterilmez hello'ı kullanarak bu Yardım **Get-Help** cmdlet, PowerShell konsolunda Merhaba, ayrıca Azure automation'da bu Yardım işlevinin açığa çıkarır.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-139">Providing this info will not only show this help using hello **Get-Help** cmdlet in hello PowerShell console, it will also expose this help functionality within Azure Automation.</span></span>  <span data-ttu-id="3e4c5-140">Örneğin, runbook yazma sırasında etkinlik eklenirken.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-140">For example, when inserting activities during runbook authoring.</span></span> <span data-ttu-id="3e4c5-141">"Ayrıntılı Yardımı görüntüleyin" seçeneğinin tıklanması Itanium tabanlı sistemler için açık hello Yardım URI'hello başka bir sekmesinde tooaccess Azure Otomasyonu kullandığınız web tarayıcısında.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-141">Clicking “View detailed help” will open hello help URI in another tab of hello web browser you’re using tooaccess Azure Automation.</span></span><br><span data-ttu-id="3e4c5-142">![Tümleştirme Modülü Yardımı](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span><span class="sxs-lookup"><span data-stu-id="3e4c5-142">![Integration Module Help](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span></span>
2. <span data-ttu-id="3e4c5-143">Merhaba modül uzak bir sistemle bağlantılı çalıştırıyorsa,</span><span class="sxs-lookup"><span data-stu-id="3e4c5-143">If hello module runs against a remote system,</span></span>

    <span data-ttu-id="3e4c5-144">a.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-144">a.</span></span> <span data-ttu-id="3e4c5-145">Merhaba bağlantı türü de denir hello gerekli bilgileri tooconnect toothat uzak sistem, tanımlayan bir tümleştirme modülü meta veri dosyası içermelidir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-145">It should contain an Integration Module metadata file that defines hello information needed tooconnect toothat remote system, meaning hello connection type.</span></span>  
    <span data-ttu-id="3e4c5-146">b.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-146">b.</span></span> <span data-ttu-id="3e4c5-147">Merhaba modüldeki her cmdlet, parametre olarak mümkün tootake bir bağlantı nesnesi (ilgili bağlantı türünün bir örneği) olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-147">Each cmdlet in hello module should be able tootake in a connection object (an instance of that connection type) as a parameter.</span></span>  

    <span data-ttu-id="3e4c5-148">Merhaba modülündeki cmdlet'leri hello hello bağlantı türü alanlarının sahip bir nesne bir parametre toohello cmdlet'ini olarak geçirme izni verirseniz Azure automation'da daha kolay toouse haline gelir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-148">Cmdlets in hello module become easier toouse in Azure Automation if you allow passing an object with hello fields of hello connection type as a parameter toohello cmdlet.</span></span> <span data-ttu-id="3e4c5-149">Bu şekilde, kullanıcılar bir cmdlet'i her çağırdığında hello bağlantı varlık toohello cmdlet'in ilgili parametreleriyle toomap parametreleri yok.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-149">This way users don’t have toomap parameters of hello connection asset toohello cmdlet's corresponding parameters each time they call a cmdlet.</span></span> <span data-ttu-id="3e4c5-150">Yukarıdaki Hello runbook örneğinde bağlı olarak, bu CorpTwilio tooaccess Twilio adlı bir Twilio bağlantı varlığı kullanır ve hello hesaptaki tüm hello telefon numaraları döndürür.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-150">Based on hello runbook example above, it uses a Twilio connection asset called CorpTwilio tooaccess Twilio and return all hello phone numbers in hello account.</span></span>  <span data-ttu-id="3e4c5-151">Merhaba bağlantı toohello parametrelerini hello cmdlet'inin hello alanlarının nasıl eşlendiğini fark ettiniz mi?</span><span class="sxs-lookup"><span data-stu-id="3e4c5-151">Notice how it is mapping hello fields of hello connection toohello parameters of hello cmdlet?</span></span><br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    <span data-ttu-id="3e4c5-152">Bir ve daha kolay tooapproach bu hello bağlantı nesnesi toohello cmdlet doğrudan geçiyor-</span><span class="sxs-lookup"><span data-stu-id="3e4c5-152">An easier and better way tooapproach this is directly passing hello connection object toohello cmdlet -</span></span>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    <span data-ttu-id="3e4c5-153">Cmdlet'lerinizin, cmdlet'leri tooaccept bir bağlantı nesnesini parametrelerin bağlantı alanları yerine bir parametre olarak doğrudan vererek etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-153">You can enable behavior like this for your cmdlets by allowing them tooaccept a connection object directly as a parameter, instead of just connection fields for parameters.</span></span> <span data-ttu-id="3e4c5-154">Genellikle Azure Automation kullanmayan kullanıcılar cmdlet'lerinizi hashtable tooact hello bağlantı nesnesi olarak oluşturma olmadan çağırabilirsiniz böylece her biri için ayarlanmış bir parametre isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-154">Usually you’ll want a parameter set for each, so that a user not using Azure Automation can call your cmdlets without constructing a hashtable tooact as hello connection object.</span></span> <span data-ttu-id="3e4c5-155">Parametre kümesi **SpecifyConnectionFields** kullanılan toopass hello bağlantı alanı özelliklerini tek tek aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-155">Parameter set **SpecifyConnectionFields** below is used toopass hello connection field properties one by one.</span></span> <span data-ttu-id="3e4c5-156">**UseConnectionObject** geçirdiğiniz sağlar hello düz ile bağlantı.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-156">**UseConnectionObject** lets you pass hello connection straight through.</span></span> <span data-ttu-id="3e4c5-157">Gördüğünüz gibi hello içinde Send-TwilioSMS cmdlet'i hello [Twilio PowerShell modülündeki](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) iki şekilde sağlar:</span><span class="sxs-lookup"><span data-stu-id="3e4c5-157">As you can see, hello Send-TwilioSMS cmdlet in hello [Twilio PowerShell module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) allows passing either way:</span></span> 
   
    ```
    function Send-TwilioSMS {
      [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
      HelpUri='http://www.twilio.com/docs/api/rest/sending-sms')]
      param(
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AccountSid,
   
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AuthToken,
   
         [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [Hashtable]
         $Connection
   
       )
    }
    ```
   <br>
3. <span data-ttu-id="3e4c5-158">Hello modüldeki tüm cmdlet'ler için çıktı türünü tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-158">Define output type for all cmdlets in hello module.</span></span> <span data-ttu-id="3e4c5-159">Tasarım zamanında IntelliSense'in cmlet'i çıkış türünü tanımlamaya hello belirlemek toohelp yazma sırasında hello cmdlet özelliklerini çıktı.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-159">Defining an output type for a cmdlet allows design-time IntelliSense toohelp you determine hello output properties of hello cmdlet, for use during authoring.</span></span> <span data-ttu-id="3e4c5-160">Otomasyon runbook grafik, tasarım zamanı bilgisinin anahtar tooan kolay kullanıcı deneyimi, modülüyle olduğu yazma sırasında özellikle yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-160">It is especially helpful during Automation runbook graphical authoring, where design time knowledge is key tooan easy user experience with your module.</span></span><br><br> <span data-ttu-id="3e4c5-161">![Grafik Runbook’u Çıktı Türü](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span><span class="sxs-lookup"><span data-stu-id="3e4c5-161">![Graphical Runbook Output Type](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span></span><br> <span data-ttu-id="3e4c5-162">Bu, benzer bir cmdlet öğesinin toohello "İleri tür" işlevine animasyonun çıktı PowerShell ISE'de toorun gerek kalmadan.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-162">This is similar toohello "type ahead" functionality of a cmdlet's output in PowerShell ISE without having toorun it.</span></span><br><br> <span data-ttu-id="3e4c5-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span><span class="sxs-lookup"><span data-stu-id="3e4c5-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span></span><br>
4. <span data-ttu-id="3e4c5-164">Merhaba modüldeki cmdlet'ler parametreler için karmaşık nesne türlerini almamalıdır.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-164">Cmdlets in hello module should not take complex object types for parameters.</span></span> <span data-ttu-id="3e4c5-165">PowerShell İş Akışı, karmaşık türleri seri durumdan çıkarılmış biçimde depolaması nedeniyle PowerShell’den farklıdır.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-165">PowerShell Workflow is different from PowerShell in that it stores complex types in deserialized form.</span></span> <span data-ttu-id="3e4c5-166">İlkel türler temel olarak kalır, ancak halde temelde özellik paketi seri durumdan dönüştürülmüş tootheir sürümleri karmaşık türleridir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-166">Primitive types will stay as primitives, but complex types are converted tootheir deserialized versions, which are essentially property bags.</span></span> <span data-ttu-id="3e4c5-167">Örneğin, hello kullandıysanız **Get-Process** cmdlet'i bir runbook (veya bir PowerShell iş akışı bu), bu [Deserialized.System.Diagnostic.Process] türünde bir nesne döndürür, değil, beklenen [hello System.Diagnostic.Process] türü.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-167">For example, if you used hello **Get-Process** cmdlet in a runbook (or a PowerShell Workflow for that matter), it would return an object of type [Deserialized.System.Diagnostic.Process], not hello expected [System.Diagnostic.Process] type.</span></span> <span data-ttu-id="3e4c5-168">Bu tür tüm aynı özellikleri çıkarılmamış türle ancak hello yöntemlerin hiçbiri hello gibi hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-168">This type has all hello same properties as hello non-deserialized type, but none of hello methods.</span></span> <span data-ttu-id="3e4c5-169">Ve burada hello cmdlet Bu parametre için [System.Diagnostic.Process] değerini bekler, bir parametre tooa cmdlet'ini olarak, bu değer toopass denerseniz aşağıdaki hata hello alırsınız: *'işlem' parametresinde bağımsız değişken dönüşümü işlenemiyor . Hata: "hello"Deserialized.System.Diagnostics.Process"tootype"System.Diagnostics.Process"türündeki"System.Diagnostics.Process (CcmExec)"değeri dönüştürülemiyor.*</span><span class="sxs-lookup"><span data-stu-id="3e4c5-169">And if you try toopass this value as a parameter tooa cmdlet, where hello cmdlet expects a [System.Diagnostic.Process] value for this parameter, you’ll receive hello following error: *Cannot process argument transformation on parameter 'process'. Error: "Cannot convert hello "System.Diagnostics.Process (CcmExec)" value of type  "Deserialized.System.Diagnostics.Process" tootype "System.Diagnostics.Process".*</span></span>   <span data-ttu-id="3e4c5-170">Merhaba arasındaki bir tür uyuşmazlığı beklenen [System.Diagnostic.Process] türünü ve verilen [Deserialized.System.Diagnostic.Process] türü hello olduğundan budur.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-170">This is because there is a type mismatch between hello expected [System.Diagnostic.Process] type and hello given [Deserialized.System.Diagnostic.Process] type.</span></span> <span data-ttu-id="3e4c5-171">Merhaba bu soruna geçici bir çözüm modülünüzün tooensure hello cmdlet'ler parametreler için karmaşık türler almayan yoludur.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-171">hello way around this issue is tooensure hello cmdlets of your module do not take complex types for parameters.</span></span> <span data-ttu-id="3e4c5-172">Merhaba yanlış şekilde toodo İşte bunu.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-172">Here is hello wrong way toodo it.</span></span>
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    <span data-ttu-id="3e4c5-173">Burada da hello şekilde hello cmdlet tarafından dahili olarak kullanılabilmesi için bir temel alarak toograb karmaşık nesne hello ve bunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-173">And here is hello right way, taking in a primitive that can be used internally by hello cmdlet toograb hello complex object and use it.</span></span> <span data-ttu-id="3e4c5-174">Merhaba PowerShell bağlamında cmdlet'leri yürütme olduğundan değil PowerShell iş akışı hello cmdlet $process hello doğru [System.Diagnostic.Process] türünü haline gelir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-174">Since cmdlets execute in hello context of PowerShell, not PowerShell Workflow, inside hello cmdlet $process becomes hello correct [System.Diagnostic.Process] type.</span></span>  
   
    ```
    function Get-ProcessDescription {
      param (
            [String] $processName
      )
      $process = Get-Process -Name $processName
   
      $process.Description
    }
    ```
   <br>
   <span data-ttu-id="3e4c5-175">Runbook'lardaki bağlantı varlıkları karmaşık bir tür olan hashtable'da olan ve henüz bu hashtable'da cmdlet'lere toobe mümkün toobe göründüğü kendi – bağlantı parametresi mükemmel, herhangi bir cast özel durumu ile.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-175">Connection assets in runbooks are hashtables, which are a complex type, and yet these hashtables seem toobe able toobe passed into cmdlets for their –Connection parameter perfectly, with no cast exception.</span></span> <span data-ttu-id="3e4c5-176">Teknik olarak, bazı PowerShell türleri mümkün toocast kendi serileştirilmiş form seri durumdan tootheir formundan doğru olduğundan ve bu nedenle hello çıkarılmamış türle kabul eden parametrelerde cmdlet'lere geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-176">Technically, some PowerShell types are able toocast properly from their serialized form tootheir deserialized form, and hence can be passed into cmdlets for parameters accepting hello non-deserialized type.</span></span> <span data-ttu-id="3e4c5-177">Hashtable bunlardan biridir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-177">Hashtable is one of these.</span></span> <span data-ttu-id="3e4c5-178">Bir modül yazarının tanımlı türlerinin toobe, bunların düzgün şekilde de seri durumdan şekilde uygulanması mümkündür, ancak bazı dengelemeler tooconsider vardır.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-178">It’s possible for a module author’s defined types toobe implemented in a way that they can correctly deserialize as well, but there are some trade-offs tooconsider.</span></span> <span data-ttu-id="3e4c5-179">türü gereksinimlerini toohave varsayılan bir oluşturucu Merhaba, tüm alt özellikleri ortak ve bir pstypeconverter'ı olması.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-179">hello type needs toohave a default constructor, have all of its properties public, and have a PSTypeConverter.</span></span> <span data-ttu-id="3e4c5-180">Ancak, zaten tanımlı türler için o hello modül yazarına desteklemez kendi, Hayır çok "bunları Düzelt", bu nedenle öneri tooavoid parametrelerin tüm karmaşık türler hello yoktur.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-180">However, for already-defined types that hello module author does not own, there is no way too“fix” them, hence hello recommendation tooavoid complex types for parameters all together.</span></span> <span data-ttu-id="3e4c5-181">Runbook yazma İpucu: bazı cmdlet'lerinizi nedenden dolayı tootake karmaşık bir tür parametresi veya başkasının gerektiren bir karmaşık tür parametresi, PowerShell iş akışı runbook'hello geçici çözüm ve PowerShell iş akışları yerel modül kullanıyorsanız Powershell'dir hello karmaşık türü oluşturan toowrap hello cmdlet'ini ve hello hello karmaşık türü tüketen hello cmdlet'i aynı Inlinescript etkinliği.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-181">Runbook Authoring tip: If for some reason your cmdlets need tootake a complex type parameter, or you are using someone else’s module that requires a complex type parameter, hello workaround in PowerShell Workflow runbooks and PowerShell Workflows in local PowerShell, is toowrap hello cmdlet that generates hello complex type and hello cmdlet that consumes hello complex type in hello same InlineScript activity.</span></span> <span data-ttu-id="3e4c5-182">PowerShell iş akışı, hello karmaşık tür oluşturan hello cmdlet doğru türü msgıd yerine Inlinescript içeriğinin PowerShell yürütür. bu yana değil hello karmaşık tür serisi.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-182">Since InlineScript executes its contents as PowerShell rather than PowerShell Workflow, hello cmdlet generating hello complex type would produce that correct type, not hello deserialized complex type.</span></span>
5. <span data-ttu-id="3e4c5-183">Tüm cmdlet'ler hello modülünde durum bilgisiz hale getirin.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-183">Make all cmdlets in hello module stateless.</span></span> <span data-ttu-id="3e4c5-184">PowerShell iş akışı farklı bir oturumda hello iş akışında çağrılan her cmdlet'i çalışır.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-184">PowerShell Workflow runs every cmdlet called in hello workflow in a different session.</span></span> <span data-ttu-id="3e4c5-185">Bu, oluşturulan veya diğer Cmdlet'lerde aynı modülü PowerShell iş akışı runbook'larında çalışmaz hello değiştiren oturum durumuna bağlı cmdlet'lerin anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-185">This means any cmdlets that depend on session state created / modified by other cmdlets in hello same module will not work in PowerShell Workflow runbooks.</span></span>  <span data-ttu-id="3e4c5-186">Örneği ne toodo değil.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-186">Here is an example of what not toodo.</span></span>
   
    ```
    $globalNum = 0
    function Set-GlobalNum {
       param(
           [int] $num
       )
   
       $globalNum = $num
    }
    function Get-GlobalNumTimesTwo {
       $output = $globalNum * 2
   
       $output
    }
    ```
   <br>
6. <span data-ttu-id="3e4c5-187">Merhaba modülü tam olarak bir xcopy'ye pakette yer alan.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-187">hello module should be fully contained in an Xcopy-able package.</span></span> <span data-ttu-id="3e4c5-188">Runbook'ları tooexecute gerektiğinde Azure Automation modülleri dağıtılmış toohello Automation korumalı olduğundan, bunlar çalıştıran hello konak bağımsız olarak toowork ihtiyaç duyar.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-188">Because Azure Automation modules are distributed toohello Automation sandboxes when runbooks need tooexecute, they need toowork independently of hello host they are running on.</span></span> <span data-ttu-id="3e4c5-189">Bu, hello modülü paketi yukarı mümkün tooZip olması ise tooany taşımak, anlamı başka bir ana bilgisayarı ile aynı veya daha yeni PowerShell sürümü hello ve varsa, Bu konakta PowerShell ortamına içe aktarıldığında da normal çalışmasını.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-189">What this means is that you should be able tooZip up hello module package, move it tooany other host with hello same or newer PowerShell version, and have it function as normal when imported into that host’s PowerShell environment.</span></span> <span data-ttu-id="3e4c5-190">Bu toohappen için sırayla hello modülü değil hello modülü klasörünü (Azure Automation'a içeri aktarırken daraltılmış yukarı hello klasörü) dışındaki tüm dosyalara bağlı veya herhangi bir konaktaki benzersiz kayıt defteri ayarları üzerinde hello tarafından belirlenen gibi bir ürün yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-190">In order for that toohappen, hello module should not depend on any files outside hello module folder (hello folder that gets zipped up when importing into Azure Automation), or on any unique registry settings on a host, such as those set by hello install of a product.</span></span> <span data-ttu-id="3e4c5-191">Bu en iyi uygulama uyulmazsa hello modül Azure Automation'da kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="3e4c5-191">If this best practice is not followed, hello module will not be usable in Azure Automation.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="3e4c5-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3e4c5-192">Next steps</span></span>

* <span data-ttu-id="3e4c5-193">PowerShell iş akışı runbook'ları ile başlatılan tooget bakın [ilk PowerShell iş akışı runbook Uygulamam](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="3e4c5-193">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="3e4c5-194">PowerShell modülleri oluşturma hakkında daha fazla toolearn bakın [bir Windows PowerShell modülü yazma](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="3e4c5-194">toolearn more about creating PowerShell Modules, see [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span></span>

