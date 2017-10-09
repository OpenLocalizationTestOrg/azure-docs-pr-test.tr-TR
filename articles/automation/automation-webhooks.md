---
title: "bir Azure Otomasyonu runbook'u ile bir Web kancası aaaStarting | Microsoft Docs"
description: "Bir istemci toostart bir runbook'un Azure Otomasyonu'nda bir HTTP çağrısından veren bir Web kancası.  Bu makalede nasıl toocreate bir Web kancası ve nasıl toocall bir toostart bir runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: ca6cde66b3784ceb5d0bc5921cee87aea74cb150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="73b7a-104">Bir Web kancası ile bir Azure Otomasyonu runbook'u başlatma</span><span class="sxs-lookup"><span data-stu-id="73b7a-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="73b7a-105">A *Web kancası* toostart belirli bir runbook, Azure Otomasyonu'nda tek bir HTTP isteğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="73b7a-105">A *webhook* allows you toostart a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="73b7a-106">Bu Visual Studio Team Services, GitHub, Microsoft Operations Management Suite günlük analizi veya özel uygulamalar gibi dış hizmetler toostart runbook'ları hello Azure Otomasyon API kullanarak tam bir çözüm uygulama olmadan sağlar.</span><span class="sxs-lookup"><span data-stu-id="73b7a-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications toostart runbooks without implementing a full solution using hello Azure Automation API.</span></span>  
<span data-ttu-id="73b7a-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="73b7a-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="73b7a-108">Bir runbook'u başlatma Web kancalarını tooother yöntemleri karşılaştırabilirsiniz [Azure Otomasyonu runbook başlatma](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="73b7a-108">You can compare webhooks tooother methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="73b7a-109">Bir Web kancası ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="73b7a-109">Details of a webhook</span></span>
<span data-ttu-id="73b7a-110">Merhaba aşağıdaki tabloda, bir Web kancası için yapılandırmanız gerekir hello özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="73b7a-110">hello following table describes hello properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="73b7a-111">Özellik</span><span class="sxs-lookup"><span data-stu-id="73b7a-111">Property</span></span> | <span data-ttu-id="73b7a-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="73b7a-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="73b7a-113">Ad</span><span class="sxs-lookup"><span data-stu-id="73b7a-113">Name</span></span> |<span data-ttu-id="73b7a-114">Bu yana bir Web kancası için istediğiniz herhangi bir ad toohello istemci gösterilmeyen sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-114">You can provide any name you want for a webhook since this is not exposed toohello client.</span></span>  <span data-ttu-id="73b7a-115">Yalnızca, tooidentify hello Azure automation'da runbook için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="73b7a-115">It is only used for you tooidentify hello runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="73b7a-116">Bir en iyi uygulama olarak kullanacağı bir ad ilgili toohello istemci hello Web kancası vermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-116">As a best practice, you should give hello webhook a name related toohello client that will use it.</span></span> |
| <span data-ttu-id="73b7a-117">URL</span><span class="sxs-lookup"><span data-stu-id="73b7a-117">URL</span></span> |<span data-ttu-id="73b7a-118">Merhaba hello Web kancası hello benzersiz adresi bir istemci bir HTTP POST toostart hello runbook'la çağırır toohello Web kancası bağlı URL'sidir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-118">hello URL of hello webhook is hello unique address that a client calls with an HTTP POST toostart hello runbook linked toohello webhook.</span></span>  <span data-ttu-id="73b7a-119">Merhaba Web kancası oluşturduğunuzda otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="73b7a-119">It is automatically generated when you create hello webhook.</span></span>  <span data-ttu-id="73b7a-120">Özel bir URL belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="73b7a-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="73b7a-121">Merhaba URL, başka kimlik doğrulama ile üçüncü taraf sistemleri tarafından çağrılan hello runbook toobe veren bir güvenlik belirteci içeriyor.</span><span class="sxs-lookup"><span data-stu-id="73b7a-121">hello URL contains a security token that allows hello runbook toobe invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="73b7a-122">Bu nedenle, bir parola gibi değerlendirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="73b7a-123">Güvenlik nedenleriyle, yalnızca hello hello zaman hello Web kancası Azure portalında URL'de oluşturulan görünüm hello olabilir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-123">For security reasons, you can only view hello URL in hello Azure portal at hello time hello webhook is created.</span></span> <span data-ttu-id="73b7a-124">Gelecekte kullanım için güvenli bir konumda hello URL unutmamalısınız.</span><span class="sxs-lookup"><span data-stu-id="73b7a-124">You should note hello URL in a secure location for future use.</span></span> |
| <span data-ttu-id="73b7a-125">Sona erme tarihi</span><span class="sxs-lookup"><span data-stu-id="73b7a-125">Expiration date</span></span> |<span data-ttu-id="73b7a-126">Bir sertifika gibi her Web kancası aynı zamanda bu artık kullanılabilir bir sona erme tarihi vardır.</span><span class="sxs-lookup"><span data-stu-id="73b7a-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="73b7a-127">Bu süre sonu tarihi Hello Web kancası oluşturulduktan sonra değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-127">This expiration date can be modified after hello webhook is created.</span></span> |
| <span data-ttu-id="73b7a-128">Etkin</span><span class="sxs-lookup"><span data-stu-id="73b7a-128">Enabled</span></span> |<span data-ttu-id="73b7a-129">Bir Web kancası oluşturulduğunda varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="73b7a-130">TooDisabled ayarlamak sonra hiçbir istemci mümkün toouse olacaktır.</span><span class="sxs-lookup"><span data-stu-id="73b7a-130">If you set it tooDisabled, then no client will be able toouse it.</span></span>  <span data-ttu-id="73b7a-131">Merhaba ayarlayabilirsiniz **etkin** hello Web kancası veya dilediğiniz zaman bir kez oluşturduğunuzda özelliği oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="73b7a-131">You can set hello **Enabled** property when you create hello webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="73b7a-132">Parametreler</span><span class="sxs-lookup"><span data-stu-id="73b7a-132">Parameters</span></span>
<span data-ttu-id="73b7a-133">Bir Web kancası hello runbook o Web kancası tarafından çalıştırıldığında kullanılan runbook parametreleri için değerleri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73b7a-133">A webhook can define values for runbook parameters that are used when hello runbook is started by that webhook.</span></span> <span data-ttu-id="73b7a-134">Merhaba Web kancası hello runbook'un zorunlu parametreler için değerler içermelidir ve isteğe bağlı parametreler için değerler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-134">hello webhook must include values for any mandatory parameters of hello runbook and may include values for optional parameters.</span></span> <span data-ttu-id="73b7a-135">Bir parametre değeri yapılandırılmış tooa Web kancası hello webhoook oluşturduktan sonra bile değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-135">A parameter value configured tooa webhook can be modified even after creating hello webhoook.</span></span> <span data-ttu-id="73b7a-136">Birden çok bağlantılı Web kancalarını tooa tek runbook her farklı parametre değerlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73b7a-136">Multiple webhooks linked tooa single runbook can each use different parameter values.</span></span>

<span data-ttu-id="73b7a-137">Bir istemciyi bir Web kancası kullanarak bir runbook'u başlattığında, hello Web kancası içinde tanımlanan hello parametre değerleri geçersiz kılamaz.</span><span class="sxs-lookup"><span data-stu-id="73b7a-137">When a client starts a runbook using a webhook, it cannot override hello parameter values defined in hello webhook.</span></span>  <span data-ttu-id="73b7a-138">tooreceive verileri hello istemcisinden hello runbook kabul edebileceği adlı tek bir parametre **$WebhookData** veri içeren türünü [object] hello istemci hello POST isteğinde içerir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-138">tooreceive data from hello client, hello runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that hello client includes in hello POST request.</span></span>

![Webhookdata özellikleri](media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="73b7a-140">Merhaba **$WebhookData** nesne hello aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="73b7a-140">hello **$WebhookData** object will have hello following properties:</span></span>

| <span data-ttu-id="73b7a-141">Özellik</span><span class="sxs-lookup"><span data-stu-id="73b7a-141">Property</span></span> | <span data-ttu-id="73b7a-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="73b7a-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="73b7a-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="73b7a-143">WebhookName</span></span> |<span data-ttu-id="73b7a-144">Merhaba Web kancası Hello adı.</span><span class="sxs-lookup"><span data-stu-id="73b7a-144">hello name of hello webhook.</span></span> |
| <span data-ttu-id="73b7a-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="73b7a-145">RequestHeader</span></span> |<span data-ttu-id="73b7a-146">Hello gelen POST isteğinin Hello üstbilgiler içeren karma tablo.</span><span class="sxs-lookup"><span data-stu-id="73b7a-146">Hash table containing hello headers of hello incoming POST request.</span></span> |
| <span data-ttu-id="73b7a-147">RequestBody</span><span class="sxs-lookup"><span data-stu-id="73b7a-147">RequestBody</span></span> |<span data-ttu-id="73b7a-148">Merhaba hello gelen POST isteğinin gövdesi.</span><span class="sxs-lookup"><span data-stu-id="73b7a-148">hello body of hello incoming POST request.</span></span>  <span data-ttu-id="73b7a-149">Bu herhangi bir dize gibi JSON, XML, biçimlendirme korur veya kodlanmış form verileri.</span><span class="sxs-lookup"><span data-stu-id="73b7a-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="73b7a-150">Merhaba runbook toowork beklenen hello veri biçimi ile yazılmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="73b7a-150">hello runbook must be written toowork with hello data format that is expected.</span></span> |

<span data-ttu-id="73b7a-151">Merhaba Web kancası gerekli toosupport Merhaba, yapılandırma yok **$WebhookData** parametresi ve hello runbook gerekli tooaccept değil.</span><span class="sxs-lookup"><span data-stu-id="73b7a-151">There is no configuration of hello webhook required toosupport hello **$WebhookData** parameter, and hello runbook is not required tooaccept it.</span></span>  <span data-ttu-id="73b7a-152">Merhaba runbook hello parametre tanımlamıyorsa, ardından hello istemciden gönderilen hello isteğinin herhangi bir ayrıntıyı yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="73b7a-152">If hello runbook does not define hello parameter, then any details of hello request sent from hello client is ignored.</span></span>

<span data-ttu-id="73b7a-153">Merhaba Web kancası oluşturduğunuzda $WebhookData için bir değer belirtirseniz, hello Web kancası hello istemci POST isteğini hello verilerle hello runbook başlatıldığında hello istemci hello istek gövdesinde herhangi bir veri içermez olsa bile bu değer kılınmadı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="73b7a-153">If you specify a value for $WebhookData when you create hello webhook, that value will be overriden when hello webhook starts hello runbook with hello data from hello client POST request, even if hello client does not include any data in hello request body.</span></span>  <span data-ttu-id="73b7a-154">Bir Web kancası dışında bir yöntem kullanılarak $WebhookData sahip bir runbook başlatırsanız, hello runbook tarafından tanınan $Webhookdata için bir değer sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by hello runbook.</span></span>  <span data-ttu-id="73b7a-155">Bu değer hello sahip bir nesne olmalıdır aynı [özellikleri](#details-of-a-webhook) bir Web kancası tarafından geçirilen gerçek WebhookData çalıştığı gibi bu hello runbook düzgün çalışabilmesi için $Webhookdata olarak.</span><span class="sxs-lookup"><span data-stu-id="73b7a-155">This value should be an object with hello same [properties](#details-of-a-webhook) as $Webhookdata so that hello runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="73b7a-156">Runbook hello Azure Portalı ' aşağıdaki hello başlatma ve WebhookData bir nesne olduğundan, test etmek için bazı WebhookData örnek toopass istediğiniz, örneğin, bunu JSON olarak hello UI geçirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-156">For example, if you are starting hello following runbook from hello Azure Portal and want toopass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in hello UI.</span></span>

![UI WebhookData parametresinden](media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="73b7a-158">Aşağıdaki özelliklere hello WebhookData parametresi için hello varsa runbook yukarıda Hello için:</span><span class="sxs-lookup"><span data-stu-id="73b7a-158">For hello above runbook, if you have hello following properties for hello WebhookData parameter:</span></span>

1. <span data-ttu-id="73b7a-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="73b7a-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="73b7a-160">RequestHeader: *= Test kullanıcıdan*</span><span class="sxs-lookup"><span data-stu-id="73b7a-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="73b7a-161">RequestBody: *["VM1", "VM2"]*</span><span class="sxs-lookup"><span data-stu-id="73b7a-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="73b7a-162">Ardından aşağıdaki JSON değeri hello UI hello WebhookData parametresi için de hello geçip geçmeyeceğini:</span><span class="sxs-lookup"><span data-stu-id="73b7a-162">Then you would pass hello following JSON value in hello UI for hello WebhookData parameter:</span></span>  

* <span data-ttu-id="73b7a-163">{"WebhookName": "MyWebhook", "RequestHeader": {"Kimden": "Test kullanıcı"}, "RequestBody": "[\"VM1\",\"VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="73b7a-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![Kullanıcı Arabirimi başlangıç WebhookData parametresi](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="73b7a-165">Tüm giriş parametreleri Hello değerlerini hello runbook işi ile günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-165">hello values of all input parameters are logged with hello runbook job.</span></span>  <span data-ttu-id="73b7a-166">Herhangi bir deyişle giriş hello Web kancası isteği hello istemci tarafından sağlanan erişim toohello Otomasyonu işi ile günlüğe kaydedilen ve kullanılabilir tooanyone olacaktır.</span><span class="sxs-lookup"><span data-stu-id="73b7a-166">This means that any input provided by hello client in hello webhook request will be logged and available tooanyone with access toohello automation job.</span></span>  <span data-ttu-id="73b7a-167">Bu nedenle, Web kancası çağrılarında hassas bilgiler dahil olmak üzere hakkında dikkatli olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="73b7a-168">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="73b7a-168">Security</span></span>
<span data-ttu-id="73b7a-169">bir Web kancası Hello güvenliğini, çağrılan toobe veren bir güvenlik belirteci içeren URL'sini hello gizliliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="73b7a-169">hello security of a webhook relies on hello privacy of its URL which contains a security token that allows it toobe invoked.</span></span> <span data-ttu-id="73b7a-170">Azure Otomasyonu toohello doğru URL'yi yapılan sürece hello isteği herhangi bir kimlik doğrulaması gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="73b7a-170">Azure Automation does not perform any authentication on hello request as long as it is made toohello correct URL.</span></span> <span data-ttu-id="73b7a-171">Bu nedenle, Web kancası hello isteği doğrulanırken bir alternatif şekillerini kullanmadan son derece hassas işlevleri gerçekleştirmek runbook'lar için kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="73b7a-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating hello request.</span></span>

<span data-ttu-id="73b7a-172">Bunu hello denetleyerek bir Web kancası tarafından çağrıldı hello runbook toodetermine mantık içerebilir **WebhookName** hello $WebhookData parametresinin özelliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="73b7a-172">You can include logic within hello runbook toodetermine that it was called by a webhook by checking hello **WebhookName** property of hello $WebhookData parameter.</span></span> <span data-ttu-id="73b7a-173">Merhaba runbook gerçekleştirebilir daha fazla doğrulama hello belirli bilgileri arayarak **RequestHeader** veya **RequestBody** özellikleri.</span><span class="sxs-lookup"><span data-stu-id="73b7a-173">hello runbook could perform further validation by looking for particular information in hello **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="73b7a-174">Başka bir strateji toohave olup hello runbook bir Web kancası isteği alındığında bazı doğrulama dış bir koşulun gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="73b7a-174">Another strategy is toohave hello runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="73b7a-175">Örneğin, yeni bir yürütme tooa GitHub havuz olduğunda GitHub tarafından çağrılan bir runbook'u göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="73b7a-175">For example, consider a runbook that is called by GitHub whenever there is a new commit tooa GitHub repository.</span></span>  <span data-ttu-id="73b7a-176">Merhaba runbook yeni bir yürütme devam etmeden önce gerçekte yalnızca oluştu tooGitHub toovalidate bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-176">hello runbook might connect tooGitHub toovalidate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="73b7a-177">Bir Web kancası oluşturma</span><span class="sxs-lookup"><span data-stu-id="73b7a-177">Creating a webhook</span></span>
<span data-ttu-id="73b7a-178">Aşağıdaki yordam toocreate hello Azure portalında yeni bir Web kancası bağlı tooa runbook'ta hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="73b7a-178">Use hello following procedure toocreate a new webhook linked tooa runbook in hello Azure portal.</span></span>

1. <span data-ttu-id="73b7a-179">Hello gelen **Runbook'lar dikey** hello Azure portal'ı tıklatın, ayrıntı dikey Web kancası hello hello runbook tooview başlayacak.</span><span class="sxs-lookup"><span data-stu-id="73b7a-179">From hello **Runbooks blade** in hello Azure portal, click hello runbook that hello webhook will start tooview its detail blade.</span></span>
2. <span data-ttu-id="73b7a-180">Tıklatın **Web kancası** hello dikey tooopen hello hello üstündeki **ekleme Web kancası** dikey.</span><span class="sxs-lookup"><span data-stu-id="73b7a-180">Click **Webhook** at hello top of hello blade tooopen hello **Add Webhook** blade.</span></span> <br><span data-ttu-id="73b7a-181">
   ![Web kancası düğmesi](media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="73b7a-181">
![Webhooks button](media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="73b7a-182">Tıklatın **yeni Web kancası oluşturma** tooopen hello **oluşturma Web kancası dikey**.</span><span class="sxs-lookup"><span data-stu-id="73b7a-182">Click **Create new webhook** tooopen hello **Create webhook blade**.</span></span>
4. <span data-ttu-id="73b7a-183">Belirtin bir **adı**, **sona erme tarihi** hello Web kancası ve olup etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-183">Specify a **Name**, **Expiration Date** for hello webhook and whether it should be enabled.</span></span> <span data-ttu-id="73b7a-184">Bkz: [bir Web kancası ayrıntılarını](#details-of-a-webhook) daha fazla bilgi için bu özellikleri.</span><span class="sxs-lookup"><span data-stu-id="73b7a-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="73b7a-185">Merhaba Kopyala simgesine tıklayın ve toocopy hello URL'sini hello Web kancası Ctrl + C tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="73b7a-185">Click hello copy icon and press Ctrl+C toocopy hello URL of hello webhook.</span></span>  <span data-ttu-id="73b7a-186">Ardından güvenli bir yerde kaydedin.</span><span class="sxs-lookup"><span data-stu-id="73b7a-186">Then record it in a safe place.</span></span>  <span data-ttu-id="73b7a-187">**Merhaba Web kancası oluşturulduktan sonra hello URL yeniden alınamıyor.**</span><span class="sxs-lookup"><span data-stu-id="73b7a-187">**Once you create hello webhook, you cannot retrieve hello URL again.**</span></span> <br><span data-ttu-id="73b7a-188">
   ![Web kancası URL'si](media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="73b7a-188">
![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="73b7a-189">Tıklatın **parametreleri** hello runbook parametreleri için tooprovide değerleri.</span><span class="sxs-lookup"><span data-stu-id="73b7a-189">Click **Parameters** tooprovide values for hello runbook parameters.</span></span>  <span data-ttu-id="73b7a-190">Merhaba runbook zorunlu parametreler varsa, değerleri belirtilmediği sürece sonra mümkün toocreate hello Web kancası olmaz.</span><span class="sxs-lookup"><span data-stu-id="73b7a-190">If hello runbook has mandatory parameters, then you will not be able toocreate hello webhook unless values are provided.</span></span>
7. <span data-ttu-id="73b7a-191">Tıklatın **oluşturma** toocreate hello Web kancası.</span><span class="sxs-lookup"><span data-stu-id="73b7a-191">Click **Create** toocreate hello webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="73b7a-192">Bir Web kancası kullanma</span><span class="sxs-lookup"><span data-stu-id="73b7a-192">Using a webhook</span></span>
<span data-ttu-id="73b7a-193">toouse bir Web kancası oluşturulduktan sonra istemci uygulamanız bir HTTP POST hello Web kancası için hello URL'siyle kesmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-193">toouse a webhook after it has been created, your client application must issue an HTTP POST with hello URL for hello webhook.</span></span>  <span data-ttu-id="73b7a-194">Merhaba Web kancası Hello sözdizimi biçimini izleyen hello olacaktır.</span><span class="sxs-lookup"><span data-stu-id="73b7a-194">hello syntax of hello webhook will be in hello following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="73b7a-195">Merhaba istemci hello POST isteğinden dönüş kodları aşağıdaki hello birini alır.</span><span class="sxs-lookup"><span data-stu-id="73b7a-195">hello client will receive one of hello following return codes from hello POST request.</span></span>  

| <span data-ttu-id="73b7a-196">Kod</span><span class="sxs-lookup"><span data-stu-id="73b7a-196">Code</span></span> | <span data-ttu-id="73b7a-197">Metin</span><span class="sxs-lookup"><span data-stu-id="73b7a-197">Text</span></span> | <span data-ttu-id="73b7a-198">Açıklama</span><span class="sxs-lookup"><span data-stu-id="73b7a-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="73b7a-199">202</span><span class="sxs-lookup"><span data-stu-id="73b7a-199">202</span></span> |<span data-ttu-id="73b7a-200">Kabul edildi</span><span class="sxs-lookup"><span data-stu-id="73b7a-200">Accepted</span></span> |<span data-ttu-id="73b7a-201">Merhaba istek kabul edildi ve hello runbook başarıyla sıraya alındı.</span><span class="sxs-lookup"><span data-stu-id="73b7a-201">hello request was accepted, and hello runbook was successfully queued.</span></span> |
| <span data-ttu-id="73b7a-202">400</span><span class="sxs-lookup"><span data-stu-id="73b7a-202">400</span></span> |<span data-ttu-id="73b7a-203">Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="73b7a-203">Bad Request</span></span> |<span data-ttu-id="73b7a-204">Merhaba isteği hello aşağıdaki nedenlerden birinden dolayı kabul edilmedi.</span><span class="sxs-lookup"><span data-stu-id="73b7a-204">hello request was not accepted for one of hello following reasons.</span></span> <ul> <li><span data-ttu-id="73b7a-205">Merhaba Web kancası süresi doldu.</span><span class="sxs-lookup"><span data-stu-id="73b7a-205">hello webhook has expired.</span></span></li> <li><span data-ttu-id="73b7a-206">Merhaba Web kancası devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="73b7a-206">hello webhook is disabled.</span></span></li> <li><span data-ttu-id="73b7a-207">Merhaba URL'de Hello belirteci geçersiz.</span><span class="sxs-lookup"><span data-stu-id="73b7a-207">hello token in hello URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="73b7a-208">404</span><span class="sxs-lookup"><span data-stu-id="73b7a-208">404</span></span> |<span data-ttu-id="73b7a-209">Bulunamadı</span><span class="sxs-lookup"><span data-stu-id="73b7a-209">Not Found</span></span> |<span data-ttu-id="73b7a-210">Merhaba isteği hello aşağıdaki nedenlerden birinden dolayı kabul edilmedi.</span><span class="sxs-lookup"><span data-stu-id="73b7a-210">hello request was not accepted for one of hello following reasons.</span></span> <ul> <li><span data-ttu-id="73b7a-211">Merhaba Web kancası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="73b7a-211">hello webhook was not found.</span></span></li> <li><span data-ttu-id="73b7a-212">Merhaba runbook bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="73b7a-212">hello runbook was not found.</span></span></li> <li><span data-ttu-id="73b7a-213">Merhaba hesabı bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="73b7a-213">hello account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="73b7a-214">500</span><span class="sxs-lookup"><span data-stu-id="73b7a-214">500</span></span> |<span data-ttu-id="73b7a-215">İç sunucu hatası</span><span class="sxs-lookup"><span data-stu-id="73b7a-215">Internal Server Error</span></span> |<span data-ttu-id="73b7a-216">Merhaba URL geçerli, ancak bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="73b7a-216">hello URL was valid, but an error occurred.</span></span>  <span data-ttu-id="73b7a-217">Lütfen hello isteği yeniden gönderin.</span><span class="sxs-lookup"><span data-stu-id="73b7a-217">Please resubmit hello request.</span></span> |

<span data-ttu-id="73b7a-218">Merhaba istek başarılı olduğunu varsayarak, hello Web kancası yanıt gibi JSON biçiminde hello iş kimliği içerir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-218">Assuming hello request is successful, hello webhook response contains hello job id in JSON format as follows.</span></span> <span data-ttu-id="73b7a-219">Tek iş kimliği yer alır ancak hello JSON biçimi için gelecekteki olası geliştirmeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="73b7a-219">It will contain a single job id, but hello JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="73b7a-220">Merhaba istemci hello runbook işi tamamlandığında veya hello Web kancası gelen tamamlanma durumu belirlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="73b7a-220">hello client cannot determine when hello runbook job completes or its completion status from hello webhook.</span></span>  <span data-ttu-id="73b7a-221">Merhaba iş kimliği gibi başka bir yöntemle kullanarak bu bilgileri belirleyebilirsiniz [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) veya hello [Azure Otomasyon API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span><span class="sxs-lookup"><span data-stu-id="73b7a-221">It can determine this information using hello job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or hello [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="73b7a-222">Örnek</span><span class="sxs-lookup"><span data-stu-id="73b7a-222">Example</span></span>
<span data-ttu-id="73b7a-223">Merhaba örnek aşağıdaki Windows PowerShell toostart bir runbook ile bir Web kancası kullanır.</span><span class="sxs-lookup"><span data-stu-id="73b7a-223">hello following example uses Windows PowerShell toostart a runbook with a webhook.</span></span>  <span data-ttu-id="73b7a-224">Bir HTTP isteği yapabilen herhangi bir dil bir Web kancası kullanabileceğinizi unutmayın; Windows PowerShell yalnızca kullanılan burada bir örnek olarak.</span><span class="sxs-lookup"><span data-stu-id="73b7a-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="73b7a-225">Merhaba runbook hello hello istek gövdesinde JSON biçimli sanal makinelerin listesini bekliyor.</span><span class="sxs-lookup"><span data-stu-id="73b7a-225">hello runbook is expecting a list of virtual machines formatted in JSON in hello body of hello request.</span></span> <span data-ttu-id="73b7a-226">Biz de hello hello istek üstbilgisinde başlatıldığına kimin hello runbook'u ve başlangıç tarihi ve saati başlatma hakkında bilgi dahil.</span><span class="sxs-lookup"><span data-stu-id="73b7a-226">We also are including information about who is starting hello runbook and hello date and time it is being started in hello header of hello request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="73b7a-227">Merhaba aşağıdaki görüntüde hello üstbilgi bilgileri gösterir (kullanarak bir [Fiddler](http://www.telerik.com/fiddler) izleme) bu istek.</span><span class="sxs-lookup"><span data-stu-id="73b7a-227">hello following image shows hello header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="73b7a-228">Bu standart bir HTTP istek üstbilgilerinin toplama toohello içerir özel tarih ve eklediğimiz üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="73b7a-228">This includes standard headers of an HTTP request in addition toohello custom Date and From headers that we added.</span></span>  <span data-ttu-id="73b7a-229">Bu değerlerin her birini hello kullanılabilir toohello runbook'ta olan **RequestHeaders** özelliği **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="73b7a-229">Each of these values is available toohello runbook in hello **RequestHeaders** property of **WebhookData**.</span></span>

![Web kancası düğmesi](media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="73b7a-231">Merhaba aşağıdaki resimde gösterilmiştir hello hello istek gövdesi (kullanarak bir [Fiddler](http://www.telerik.com/fiddler) izleme) olan kullanılabilir toohello runbook'ta hello **RequestBody** özelliği **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="73b7a-231">hello following image shows hello body of hello request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available toohello runbook in hello **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="73b7a-232">Merhaba hello istek gövdesinde eklenmiştir hello biçimi olduğu için bu JSON olarak biçimlendirilir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-232">This is formatted as JSON because that was hello format that was included in hello body of hello request.</span></span>     

![Web kancası düğmesi](media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="73b7a-234">Merhaba aşağıdaki görüntüde Windows PowerShell ve hello elde edilen yanıt gönderilen hello istek gösterilir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-234">hello following image shows hello request being sent from Windows PowerShell and hello resulting response.</span></span>  <span data-ttu-id="73b7a-235">Merhaba iş kimliği hello yanıt ve dönüştürülen tooa dize ayıklanır.</span><span class="sxs-lookup"><span data-stu-id="73b7a-235">hello job id is extracted from hello response and converted tooa string.</span></span>

![Web kancası düğmesi](media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="73b7a-237">Merhaba aşağıdaki örnek runbook'u hello önceki örnek isteğini kabul eder ve hello sanal makineleri hello istek gövdesinde belirtilen başlatır.</span><span class="sxs-lookup"><span data-stu-id="73b7a-237">hello following sample runbook accepts hello previous example request and starts hello virtual machines specified in hello request body.</span></span>

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate tooAzure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean toobe started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-tooazure-alerts"></a><span data-ttu-id="73b7a-238">Başlangıç runbook'larda yanıt tooAzure uyarıları</span><span class="sxs-lookup"><span data-stu-id="73b7a-238">Starting runbooks in response tooAzure alerts</span></span>
<span data-ttu-id="73b7a-239">Web kancası etkin runbook'ları olabilir kullanılan tooreact çok[Azure uyarıları](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="73b7a-239">Webhook-enabled runbooks can be used tooreact too[Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="73b7a-240">Azure kaynaklarında performans, kullanılabilirlik ve kullanım hello Yardım Azure uyarıları gibi hello istatistikleri toplama tarafından izlenebilir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-240">Resources in Azure can be monitored by collecting hello statistics like performance, availability and usage with hello help of Azure alerts.</span></span> <span data-ttu-id="73b7a-241">Ölçümleri izleme dayalı bir uyarı alabilirsiniz veya Azure kaynaklarınızı, şu anda Otomasyon hesapları için olaylar yalnızca ölçümleri destekler.</span><span class="sxs-lookup"><span data-stu-id="73b7a-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="73b7a-242">Atanan hello eşiği veya yapılandırılmış hello olay tetiklenir sonra toohello Hizmet Yöneticisi veya ortak yöneticileri tooresolve hello uyarı ölçümleri hakkında daha fazla bilgi için bir bildirim gönderilir ve olayları başvurun çok belirtilen bir ölçüm hello değerini aştığında[ Azure uyarıları](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="73b7a-242">When hello value of a specified metric exceeds hello threshold assigned or if hello configured event is triggered then a notification is sent toohello service admin or co-admins tooresolve hello alert, for more information on metrics and events please refer too[Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="73b7a-243">Azure Uyarıları Bildirim sistemi olarak kullanmanın yanı sıra, ayrıca yanıt tooalerts runbook'ları devre dışı tetiklersiniz.</span><span class="sxs-lookup"><span data-stu-id="73b7a-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response tooalerts.</span></span> <span data-ttu-id="73b7a-244">Azure Otomasyonu hello yetenek toorun Web kancası etkin runbook'ları Azure uyarılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="73b7a-244">Azure Automation provides hello capability toorun webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="73b7a-245">Ölçüm aştığında hello eşik değeri hello uyarı kuralı etkin hale gelir ve Tetikleyicileri hello runbook sırayla yürüten Otomasyonu Web kancası hello yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="73b7a-245">When a metric exceeds hello configured threshold value then hello alert rule becomes active and triggers hello automation webhook which in turn executes hello runbook.</span></span>

![Web kancaları](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="73b7a-247">Uyarı bağlamı</span><span class="sxs-lookup"><span data-stu-id="73b7a-247">Alert context</span></span>
<span data-ttu-id="73b7a-248">Bir sanal makine gibi bir Azure kaynağı düşünün, CPU kullanımı bu makinenin hello anahtar performans ölçüm biridir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of hello key performance metric.</span></span> <span data-ttu-id="73b7a-249">Merhaba CPU kullanımı % 100 veya belirli bir miktar fazla uzun süre ise toorestart hello sanal makine toofix hello sorun isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73b7a-249">If hello CPU utilization is 100% or more than a certain amount for long period of time, you might want toorestart hello virtual machine toofix hello problem.</span></span> <span data-ttu-id="73b7a-250">Bu bir uyarı kuralı toohello sanal makine yapılandırarak çözülebilir ve bu kural CPU yüzdesi, ölçüm olarak alır.</span><span class="sxs-lookup"><span data-stu-id="73b7a-250">This can be solved by configuring an alert rule toohello virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="73b7a-251">CPU yüzdesi burada yalnızca bir örnek olarak alınır ancak tooyour Azure yapılandırabileceğiniz birçok ölçümleri vardır kaynakları ve hello sanal makinenin yeniden başlatılması olan bir eylemi toofix bu sorunu gerçekleştirilen diğer eylemler hello runbook tootake yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73b7a-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure tooyour Azure resources and restarting hello virtual machine is an action that is taken toofix this issue, you can configure hello runbook tootake other actions.</span></span>

<span data-ttu-id="73b7a-252">Bu hello uyarı kuralı etkin hale gelir ve Web kancası etkin runbook Tetikleyicileri hello zaman hello uyarı bağlamı toohello runbook gönderir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-252">When this hello alert rule becomes active and triggers hello webhook-enabled runbook, it sends hello alert context toohello runbook.</span></span> <span data-ttu-id="73b7a-253">[Uyarı bağlamı](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) dahil olmak üzere ayrıntılarını içeren **Subscriptionıd**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** ve **zaman damgası** üzerinde bu göz önünde bulundurarak eylem hello runbook tooidentify hello kaynağı için gerekli olan.</span><span class="sxs-lookup"><span data-stu-id="73b7a-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for hello runbook tooidentify hello resource on which it will be taking action.</span></span> <span data-ttu-id="73b7a-254">Bağlam içinde hello hello gövde bölümü katıştırılmış uyarı **WebhookData** gönderilen toohello runbook nesne ve ile erişilebilir **Webhook.RequestBody** özelliği</span><span class="sxs-lookup"><span data-stu-id="73b7a-254">Alert context is embedded in hello body part of hello **WebhookData** object sent toohello runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="73b7a-255">Örnek</span><span class="sxs-lookup"><span data-stu-id="73b7a-255">Example</span></span>
<span data-ttu-id="73b7a-256">Bir Azure sanal makinesi, abonelik ve ilişkilendirme oluşturma bir [uyarı toomonitor CPU yüzdesi ölçüm](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="73b7a-256">Create an Azure virtual machine in your subscription and associate an [alert toomonitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="73b7a-257">Merhaba uyarı oluşturulurken hello Web kancası oluşturulurken oluşturulan hello Web kancası hello URL'si ile Merhaba Web kancası alanını doldurmak emin olun.</span><span class="sxs-lookup"><span data-stu-id="73b7a-257">While creating hello alert make sure you populate hello webhook field with hello URL of hello webhook which was generated while creating hello webhook.</span></span>

<span data-ttu-id="73b7a-258">Merhaba aşağıdaki örnek runbook'u hello uyarı kuralı etkin hale gelir ve hello runbook tooidentify hello kaynak üzerinde bu eylemi gerçekleştirmeden gereken hello uyarı bağlam parametreleri toplar geldiğinde tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="73b7a-258">hello following sample runbook is triggered when hello alert rule becomes active and it collects hello Alert context parameters which are required for hello runbook tooidentify hello resource on which it will be taking action.</span></span>

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on hello webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain hello WebhookBody containing hello AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain hello AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on hello AlertContext data, in our case restarting hello VM.
            # Authenticate tooyour Azure subscription using Organization ID toobe able toorestart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check hello status property of hello VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart hello VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant tooonly be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="73b7a-259">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="73b7a-259">Next steps</span></span>
* <span data-ttu-id="73b7a-260">Farklı şekillerde toostart bir runbook hakkında daha fazla bilgi için bkz: [Runbook başlatma](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="73b7a-260">For details on different ways toostart a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="73b7a-261">Bir Runbook işinin durumunu görüntüleme hello hakkında daha fazla bilgi için çok başvuran[Azure Otomasyonu Runbook yürütme](automation-runbook-execution.md).</span><span class="sxs-lookup"><span data-stu-id="73b7a-261">For information on viewing hello Status of a Runbook Job, refer too[Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="73b7a-262">nasıl toouse Azure Otomasyonu tootake eylem Azure uyarılar hakkında bkz toolearn [Otomasyon runbook'ları ile Azure VM uyarıları düzeltmek](automation-azure-vm-alert-integration.md).</span><span class="sxs-lookup"><span data-stu-id="73b7a-262">toolearn how toouse Azure Automation tootake action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>
