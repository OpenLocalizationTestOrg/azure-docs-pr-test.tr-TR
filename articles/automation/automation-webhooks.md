---
title: "Bir Azure Otomasyonu runbook'u ile bir Web kancası başlangıç | Microsoft Docs"
description: "Bir HTTP çağrısından Azure Otomasyon runbook'u başlatmak bir istemci izin veren bir Web kancası.  Bu makalede, bir Web kancası oluşturma ve bir runbook'u başlatmak için bir çağrı açıklanmaktadır."
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
ms.openlocfilehash: 6c65427fcd18e41a90dfb872aa9525f758b17b87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="9ada4-104">Bir Web kancası ile bir Azure Otomasyonu runbook'u başlatma</span><span class="sxs-lookup"><span data-stu-id="9ada4-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="9ada4-105">A *Web kancası* , belirli bir runbook, tek bir HTTP isteği aracılığıyla Azure Otomasyonu'nda başlatmanıza olanak verir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-105">A *webhook* allows you to start a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="9ada4-106">Bu, Visual Studio Team Services, GitHub, Microsoft Operations Management Suite günlük analizi veya runbook'ları Azure Otomasyon API'sini kullanarak tam bir çözüm uygulama olmadan başlatmak için özel uygulamalar gibi dış hizmetler sağlar.</span><span class="sxs-lookup"><span data-stu-id="9ada4-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications to start runbooks without implementing a full solution using the Azure Automation API.</span></span>  
<span data-ttu-id="9ada4-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="9ada4-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="9ada4-108">Bir runbook'u başlatma diğer yöntemleri için Web kancası karşılaştırabilirsiniz [Azure Otomasyonu runbook başlatma](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="9ada4-108">You can compare webhooks to other methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="9ada4-109">Bir Web kancası ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="9ada4-109">Details of a webhook</span></span>
<span data-ttu-id="9ada4-110">Aşağıdaki tabloda, bir Web kancası için yapılandırmanız gerekir özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="9ada4-110">The following table describes the properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="9ada4-111">Özellik</span><span class="sxs-lookup"><span data-stu-id="9ada4-111">Property</span></span> | <span data-ttu-id="9ada4-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9ada4-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9ada4-113">Ad</span><span class="sxs-lookup"><span data-stu-id="9ada4-113">Name</span></span> |<span data-ttu-id="9ada4-114">Bu istemciye gösterilmez bu yana bir Web kancası için istediğiniz herhangi bir ad sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ada4-114">You can provide any name you want for a webhook since this is not exposed to the client.</span></span>  <span data-ttu-id="9ada4-115">Yalnızca sizin için Azure Automation runbook tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9ada4-115">It is only used for you to identify the runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="9ada4-116">En iyi uygulama, Web kancası kullanacağı istemcisiyle ilgili bir ad vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-116">As a best practice, you should give the webhook a name related to the client that will use it.</span></span> |
| <span data-ttu-id="9ada4-117">URL</span><span class="sxs-lookup"><span data-stu-id="9ada4-117">URL</span></span> |<span data-ttu-id="9ada4-118">Web kancası URL'si için Web kancası bağlı runbook'u başlatmak için bir HTTP POST ile bir istemci çağıran benzersiz adrestir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-118">The URL of the webhook is the unique address that a client calls with an HTTP POST to start the runbook linked to the webhook.</span></span>  <span data-ttu-id="9ada4-119">Web kancası oluşturduğunuzda otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9ada4-119">It is automatically generated when you create the webhook.</span></span>  <span data-ttu-id="9ada4-120">Özel bir URL belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ada4-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="9ada4-121">URL runbook'un başka kimlik doğrulama ile üçüncü taraf sistemleri tarafından çağrılan izin veren bir güvenlik belirteci içeriyor.</span><span class="sxs-lookup"><span data-stu-id="9ada4-121">The URL contains a security token that allows the runbook to be invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="9ada4-122">Bu nedenle, bir parola gibi değerlendirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="9ada4-123">Güvenlik nedeniyle, Web kancası oluşturulduğunda Azure portalında yalnızca URL görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ada4-123">For security reasons, you can only view the URL in the Azure portal at the time the webhook is created.</span></span> <span data-ttu-id="9ada4-124">Gelecekte kullanım için güvenli bir konumda URL unutmamalısınız.</span><span class="sxs-lookup"><span data-stu-id="9ada4-124">You should note the URL in a secure location for future use.</span></span> |
| <span data-ttu-id="9ada4-125">Sona erme tarihi</span><span class="sxs-lookup"><span data-stu-id="9ada4-125">Expiration date</span></span> |<span data-ttu-id="9ada4-126">Bir sertifika gibi her Web kancası aynı zamanda bu artık kullanılabilir bir sona erme tarihi vardır.</span><span class="sxs-lookup"><span data-stu-id="9ada4-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="9ada4-127">Web kancası oluşturulduktan sonra bu süre sonu tarihi değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-127">This expiration date can be modified after the webhook is created.</span></span> |
| <span data-ttu-id="9ada4-128">Etkin</span><span class="sxs-lookup"><span data-stu-id="9ada4-128">Enabled</span></span> |<span data-ttu-id="9ada4-129">Bir Web kancası oluşturulduğunda varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="9ada4-130">Devre dışı olarak ayarlarsanız, hiçbir istemci kullanmak mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9ada4-130">If you set it to Disabled, then no client will be able to use it.</span></span>  <span data-ttu-id="9ada4-131">Ayarlayabileceğiniz **etkin** Web kancası veya dilediğiniz zaman bir kez oluşturduğunuzda özelliği oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9ada4-131">You can set the **Enabled** property when you create the webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="9ada4-132">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9ada4-132">Parameters</span></span>
<span data-ttu-id="9ada4-133">Bir Web kancası runbook o Web kancası tarafından çalıştırıldığında kullanılan runbook parametreleri için değerleri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ada4-133">A webhook can define values for runbook parameters that are used when the runbook is started by that webhook.</span></span> <span data-ttu-id="9ada4-134">Web kancası runbook'un zorunlu parametreler için değerler içermelidir ve isteğe bağlı parametreler için değerler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-134">The webhook must include values for any mandatory parameters of the runbook and may include values for optional parameters.</span></span> <span data-ttu-id="9ada4-135">Bir Web kancası için yapılandırılmış bir parametre değeri webhoook oluşturduktan sonra bile değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-135">A parameter value configured to a webhook can be modified even after creating the webhoook.</span></span> <span data-ttu-id="9ada4-136">Tek bir runbook bağlı birden çok Web kancalarını her farklı parametre değerlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ada4-136">Multiple webhooks linked to a single runbook can each use different parameter values.</span></span>

<span data-ttu-id="9ada4-137">Bir istemciyi bir Web kancası kullanarak bir runbook'u başlattığında, Web kancası içinde tanımlanan parametre değerlerini geçersiz kılamaz.</span><span class="sxs-lookup"><span data-stu-id="9ada4-137">When a client starts a runbook using a webhook, it cannot override the parameter values defined in the webhook.</span></span>  <span data-ttu-id="9ada4-138">İstemciden veri almak için runbook adlı tek bir parametre kabul edebilir **$WebhookData** [object] türündeki POST isteğinde istemci içeren veri içermez.</span><span class="sxs-lookup"><span data-stu-id="9ada4-138">To receive data from the client, the runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that the client includes in the POST request.</span></span>

![Webhookdata özellikleri](media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="9ada4-140">**$WebhookData** nesnesi aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="9ada4-140">The **$WebhookData** object will have the following properties:</span></span>

| <span data-ttu-id="9ada4-141">Özellik</span><span class="sxs-lookup"><span data-stu-id="9ada4-141">Property</span></span> | <span data-ttu-id="9ada4-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9ada4-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9ada4-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="9ada4-143">WebhookName</span></span> |<span data-ttu-id="9ada4-144">Web kancası adı.</span><span class="sxs-lookup"><span data-stu-id="9ada4-144">The name of the webhook.</span></span> |
| <span data-ttu-id="9ada4-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="9ada4-145">RequestHeader</span></span> |<span data-ttu-id="9ada4-146">Gelen posta istek üstbilgileri içeren karma tablo.</span><span class="sxs-lookup"><span data-stu-id="9ada4-146">Hash table containing the headers of the incoming POST request.</span></span> |
| <span data-ttu-id="9ada4-147">RequestBody</span><span class="sxs-lookup"><span data-stu-id="9ada4-147">RequestBody</span></span> |<span data-ttu-id="9ada4-148">Gelen posta istek gövdesi.</span><span class="sxs-lookup"><span data-stu-id="9ada4-148">The body of the incoming POST request.</span></span>  <span data-ttu-id="9ada4-149">Bu herhangi bir dize gibi JSON, XML, biçimlendirme korur veya kodlanmış form verileri.</span><span class="sxs-lookup"><span data-stu-id="9ada4-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="9ada4-150">Runbook için beklenen veri biçimi ile çalışmak için yazılmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9ada4-150">The runbook must be written to work with the data format that is expected.</span></span> |

<span data-ttu-id="9ada4-151">Web kancası desteklemek için gerekli olan yapılandırma yok **$WebhookData** parametre ve runbook kabul etmek için gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9ada4-151">There is no configuration of the webhook required to support the **$WebhookData** parameter, and the runbook is not required to accept it.</span></span>  <span data-ttu-id="9ada4-152">Runbook parametresi tanımlamıyorsa, daha sonra istemci tarafından gönderilen istek, herhangi bir ayrıntıyı yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="9ada4-152">If the runbook does not define the parameter, then any details of the request sent from the client is ignored.</span></span>

<span data-ttu-id="9ada4-153">Web kancası oluşturduğunuzda, bir değer $WebhookData için Web kancası istemci POST isteğini verilerle runbook başlatıldığında, istemci istek gövdesinde herhangi bir veri içermez olsa bile değer kılınmadı olmasını belirtirseniz.</span><span class="sxs-lookup"><span data-stu-id="9ada4-153">If you specify a value for $WebhookData when you create the webhook, that value will be overriden when the webhook starts the runbook with the data from the client POST request, even if the client does not include any data in the request body.</span></span>  <span data-ttu-id="9ada4-154">Bir Web kancası dışında bir yöntem kullanılarak $WebhookData sahip bir runbook başlatırsanız, runbook tarafından tanınan $Webhookdata için bir değer sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by the runbook.</span></span>  <span data-ttu-id="9ada4-155">Bu değer bir nesne ile aynı olmalıdır [özellikleri](#details-of-a-webhook) $Webhookdata olarak böylece Web kancası tarafından geçirilen gerçek WebhookData çalıştığı gibi runbook düzgün ile çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ada4-155">This value should be an object with the same [properties](#details-of-a-webhook) as $Webhookdata so that the runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="9ada4-156">Aşağıdaki runbook Azure Portalı'ndan başladılar ve test etmek için bazı örnek WebhookData WebhookData bir nesne olduğundan geçirmek istediğiniz, örneğin, bu arabirimdeki JSON olarak geçirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-156">For example, if you are starting the following runbook from the Azure Portal and want to pass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in the UI.</span></span>

![UI WebhookData parametresinden](media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="9ada4-158">WebhookData parametresi için aşağıdaki özellikler varsa, yukarıdaki runbook için:</span><span class="sxs-lookup"><span data-stu-id="9ada4-158">For the above runbook, if you have the following properties for the WebhookData parameter:</span></span>

1. <span data-ttu-id="9ada4-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="9ada4-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="9ada4-160">RequestHeader: *= Test kullanıcıdan*</span><span class="sxs-lookup"><span data-stu-id="9ada4-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="9ada4-161">RequestBody: *["VM1", "VM2"]*</span><span class="sxs-lookup"><span data-stu-id="9ada4-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="9ada4-162">Daha sonra kullanıcı arabiriminde WebhookData parametresi için aşağıdaki JSON değeri geçirin:</span><span class="sxs-lookup"><span data-stu-id="9ada4-162">Then you would pass the following JSON value in the UI for the WebhookData parameter:</span></span>  

* <span data-ttu-id="9ada4-163">{"WebhookName": "MyWebhook", "RequestHeader": {"Kimden": "Test kullanıcı"}, "RequestBody": "[\"VM1\",\"VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="9ada4-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![Kullanıcı Arabirimi başlangıç WebhookData parametresi](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="9ada4-165">Tüm giriş parametrelerinin değerlerini runbook işi ile günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-165">The values of all input parameters are logged with the runbook job.</span></span>  <span data-ttu-id="9ada4-166">Herhangi bir deyişle Web kancası isteği istemci tarafından sağlanan giriş günlüğe kaydedilen ve Otomasyon iş erişimi olan herkes için kullanılabilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9ada4-166">This means that any input provided by the client in the webhook request will be logged and available to anyone with access to the automation job.</span></span>  <span data-ttu-id="9ada4-167">Bu nedenle, Web kancası çağrılarında hassas bilgiler dahil olmak üzere hakkında dikkatli olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="9ada4-168">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="9ada4-168">Security</span></span>
<span data-ttu-id="9ada4-169">Bir Web kancası güvenlik çağrılmasına izin veren bir güvenlik belirteci içeren URL'sini gizlilik kullanır.</span><span class="sxs-lookup"><span data-stu-id="9ada4-169">The security of a webhook relies on the privacy of its URL which contains a security token that allows it to be invoked.</span></span> <span data-ttu-id="9ada4-170">Azure otomasyonu için doğru URL'yi yapılan sürece herhangi bir kimlik doğrulaması isteği gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="9ada4-170">Azure Automation does not perform any authentication on the request as long as it is made to the correct URL.</span></span> <span data-ttu-id="9ada4-171">Bu nedenle, Web kancalarını isteği doğrulanırken bir alternatif şekillerini kullanmadan son derece hassas işlevleri gerçekleştirmek runbook'lar için kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="9ada4-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating the request.</span></span>

<span data-ttu-id="9ada4-172">Bunu denetleyerek bir Web kancası tarafından çağrıldı belirlemek için runbook mantık içerebilir **WebhookName** $WebhookData parametresinin özelliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="9ada4-172">You can include logic within the runbook to determine that it was called by a webhook by checking the **WebhookName** property of the $WebhookData parameter.</span></span> <span data-ttu-id="9ada4-173">Runbook daha fazla doğrulama belirli bilgileri arayarak gerçekleştirebilir **RequestHeader** veya **RequestBody** özellikleri.</span><span class="sxs-lookup"><span data-stu-id="9ada4-173">The runbook could perform further validation by looking for particular information in the **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="9ada4-174">Bir Web kancası isteği alındığında bir dış koşulun bazı doğrulama gerçekleştirmek runbook başka bir stratejisi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9ada4-174">Another strategy is to have the runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="9ada4-175">Örneğin, bir GitHub deposuna yeni bir yürütme olduğunda GitHub tarafından çağrılan bir runbook'u göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="9ada4-175">For example, consider a runbook that is called by GitHub whenever there is a new commit to a GitHub repository.</span></span>  <span data-ttu-id="9ada4-176">Runbook yeni bir yürütme gerçekte yalnızca devam etmeden önce oluştu olduğunu doğrulamak için GitHub bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-176">The runbook might connect to GitHub to validate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="9ada4-177">Bir Web kancası oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ada4-177">Creating a webhook</span></span>
<span data-ttu-id="9ada4-178">Azure Portalı'nda runbook'un bağlı yeni bir Web kancası oluşturmak için aşağıdaki yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9ada4-178">Use the following procedure to create a new webhook linked to a runbook in the Azure portal.</span></span>

1. <span data-ttu-id="9ada4-179">Gelen **Runbook'lar dikey** Azure portalında, ayrıntı dikey penceresini görüntülemek için Web kancası başlatacak ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ada4-179">From the **Runbooks blade** in the Azure portal, click the runbook that the webhook will start to view its detail blade.</span></span>
2. <span data-ttu-id="9ada4-180">Tıklatın **Web kancası** açmak için dikey pencerenin üstündeki **ekleme Web kancası** dikey.</span><span class="sxs-lookup"><span data-stu-id="9ada4-180">Click **Webhook** at the top of the blade to open the **Add Webhook** blade.</span></span> <br><span data-ttu-id="9ada4-181">
   ![Web kancası düğmesi](media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="9ada4-181">
![Webhooks button](media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="9ada4-182">Tıklatın **yeni Web kancası oluşturma** açmak için **oluşturma Web kancası dikey**.</span><span class="sxs-lookup"><span data-stu-id="9ada4-182">Click **Create new webhook** to open the **Create webhook blade**.</span></span>
4. <span data-ttu-id="9ada4-183">Belirtin bir **adı**, **sona erme tarihi** Web kancası ve olup etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-183">Specify a **Name**, **Expiration Date** for the webhook and whether it should be enabled.</span></span> <span data-ttu-id="9ada4-184">Bkz: [bir Web kancası ayrıntılarını](#details-of-a-webhook) daha fazla bilgi için bu özellikleri.</span><span class="sxs-lookup"><span data-stu-id="9ada4-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="9ada4-185">Kopyala simgesine tıklayın ve Web kancası URL'yi kopyalamak için Ctrl + C tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="9ada4-185">Click the copy icon and press Ctrl+C to copy the URL of the webhook.</span></span>  <span data-ttu-id="9ada4-186">Ardından güvenli bir yerde kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9ada4-186">Then record it in a safe place.</span></span>  <span data-ttu-id="9ada4-187">**Web kancası oluşturulduktan sonra URL'yi yeniden alınamıyor.**</span><span class="sxs-lookup"><span data-stu-id="9ada4-187">**Once you create the webhook, you cannot retrieve the URL again.**</span></span> <br><span data-ttu-id="9ada4-188">
   ![Web kancası URL'si](media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="9ada4-188">
![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="9ada4-189">Tıklatın **parametreleri** runbook parametreleri için değerler sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="9ada4-189">Click **Parameters** to provide values for the runbook parameters.</span></span>  <span data-ttu-id="9ada4-190">Runbook zorunlu parametreler varsa, daha sonra değerleri belirtilmediği sürece Web kancası oluşturmak mümkün olmaz.</span><span class="sxs-lookup"><span data-stu-id="9ada4-190">If the runbook has mandatory parameters, then you will not be able to create the webhook unless values are provided.</span></span>
7. <span data-ttu-id="9ada4-191">Tıklatın **oluşturma** Web kancası oluşturulamadı.</span><span class="sxs-lookup"><span data-stu-id="9ada4-191">Click **Create** to create the webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="9ada4-192">Bir Web kancası kullanma</span><span class="sxs-lookup"><span data-stu-id="9ada4-192">Using a webhook</span></span>
<span data-ttu-id="9ada4-193">Bir Web kancası oluşturulduktan sonra kullanmak için istemci uygulamanız bir Web kancası URL'si ile HTTP POST kesmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-193">To use a webhook after it has been created, your client application must issue an HTTP POST with the URL for the webhook.</span></span>  <span data-ttu-id="9ada4-194">Web kancası söz dizimi şu biçimde olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9ada4-194">The syntax of the webhook will be in the following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="9ada4-195">İstemci aşağıdaki dönüş kodları birini POST isteğini alır.</span><span class="sxs-lookup"><span data-stu-id="9ada4-195">The client will receive one of the following return codes from the POST request.</span></span>  

| <span data-ttu-id="9ada4-196">Kod</span><span class="sxs-lookup"><span data-stu-id="9ada4-196">Code</span></span> | <span data-ttu-id="9ada4-197">Metin</span><span class="sxs-lookup"><span data-stu-id="9ada4-197">Text</span></span> | <span data-ttu-id="9ada4-198">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9ada4-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="9ada4-199">202</span><span class="sxs-lookup"><span data-stu-id="9ada4-199">202</span></span> |<span data-ttu-id="9ada4-200">Kabul edildi</span><span class="sxs-lookup"><span data-stu-id="9ada4-200">Accepted</span></span> |<span data-ttu-id="9ada4-201">İstek kabul edildi ve runbook başarıyla sıraya alındı.</span><span class="sxs-lookup"><span data-stu-id="9ada4-201">The request was accepted, and the runbook was successfully queued.</span></span> |
| <span data-ttu-id="9ada4-202">400</span><span class="sxs-lookup"><span data-stu-id="9ada4-202">400</span></span> |<span data-ttu-id="9ada4-203">Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="9ada4-203">Bad Request</span></span> |<span data-ttu-id="9ada4-204">İstek aşağıdaki nedenlerden birinden dolayı kabul edilmedi.</span><span class="sxs-lookup"><span data-stu-id="9ada4-204">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="9ada4-205">Web kancası süresi doldu.</span><span class="sxs-lookup"><span data-stu-id="9ada4-205">The webhook has expired.</span></span></li> <li><span data-ttu-id="9ada4-206">Web kancası devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="9ada4-206">The webhook is disabled.</span></span></li> <li><span data-ttu-id="9ada4-207">URL'deki belirteci geçersiz.</span><span class="sxs-lookup"><span data-stu-id="9ada4-207">The token in the URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="9ada4-208">404</span><span class="sxs-lookup"><span data-stu-id="9ada4-208">404</span></span> |<span data-ttu-id="9ada4-209">Bulunamadı</span><span class="sxs-lookup"><span data-stu-id="9ada4-209">Not Found</span></span> |<span data-ttu-id="9ada4-210">İstek aşağıdaki nedenlerden birinden dolayı kabul edilmedi.</span><span class="sxs-lookup"><span data-stu-id="9ada4-210">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="9ada4-211">Web kancası bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="9ada4-211">The webhook was not found.</span></span></li> <li><span data-ttu-id="9ada4-212">Runbook bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="9ada4-212">The runbook was not found.</span></span></li> <li><span data-ttu-id="9ada4-213">Hesap bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="9ada4-213">The account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="9ada4-214">500</span><span class="sxs-lookup"><span data-stu-id="9ada4-214">500</span></span> |<span data-ttu-id="9ada4-215">İç sunucu hatası</span><span class="sxs-lookup"><span data-stu-id="9ada4-215">Internal Server Error</span></span> |<span data-ttu-id="9ada4-216">URL geçerli, ancak bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="9ada4-216">The URL was valid, but an error occurred.</span></span>  <span data-ttu-id="9ada4-217">Lütfen isteği yeniden gönderin.</span><span class="sxs-lookup"><span data-stu-id="9ada4-217">Please resubmit the request.</span></span> |

<span data-ttu-id="9ada4-218">İstek başarılı olduğunu varsayarak, Web kancası yanıt gibi JSON biçiminde iş kimliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-218">Assuming the request is successful, the webhook response contains the job id in JSON format as follows.</span></span> <span data-ttu-id="9ada4-219">Tek iş kimliği yer alır ancak JSON biçimi için gelecekteki olası geliştirmeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="9ada4-219">It will contain a single job id, but the JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="9ada4-220">İstemci, runbook işi tamamlandığında veya Web kancası gelen tamamlanma durumu belirlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="9ada4-220">The client cannot determine when the runbook job completes or its completion status from the webhook.</span></span>  <span data-ttu-id="9ada4-221">İş kimliği gibi başka bir yöntemle kullanarak bu bilgileri belirleyebilirsiniz [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) veya [Azure Otomasyon API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span><span class="sxs-lookup"><span data-stu-id="9ada4-221">It can determine this information using the job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or the [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="9ada4-222">Örnek</span><span class="sxs-lookup"><span data-stu-id="9ada4-222">Example</span></span>
<span data-ttu-id="9ada4-223">Aşağıdaki örnek, bir Web kancası ile bir runbook'u başlatmak için Windows PowerShell'i kullanır.</span><span class="sxs-lookup"><span data-stu-id="9ada4-223">The following example uses Windows PowerShell to start a runbook with a webhook.</span></span>  <span data-ttu-id="9ada4-224">Bir HTTP isteği yapabilen herhangi bir dil bir Web kancası kullanabileceğinizi unutmayın; Windows PowerShell yalnızca kullanılan burada bir örnek olarak.</span><span class="sxs-lookup"><span data-stu-id="9ada4-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="9ada4-225">Runbook istek gövdesinde JSON biçimli sanal makinelerin listesini bekliyor.</span><span class="sxs-lookup"><span data-stu-id="9ada4-225">The runbook is expecting a list of virtual machines formatted in JSON in the body of the request.</span></span> <span data-ttu-id="9ada4-226">Biz de istek üstbilgisinde başlatıldığına kimin runbook ve tarih ve saat başlatma hakkında bilgi dahil.</span><span class="sxs-lookup"><span data-stu-id="9ada4-226">We also are including information about who is starting the runbook and the date and time it is being started in the header of the request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="9ada4-227">Aşağıdaki resimde üst bilgileri gösterir (kullanarak bir [Fiddler](http://www.telerik.com/fiddler) izleme) bu istek.</span><span class="sxs-lookup"><span data-stu-id="9ada4-227">The following image shows the header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="9ada4-228">Bu, bir HTTP isteğinin özel tarih yanı sıra ve eklediğimiz başlıklarından standart üstbilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-228">This includes standard headers of an HTTP request in addition to the custom Date and From headers that we added.</span></span>  <span data-ttu-id="9ada4-229">Bu değerlerin her birini runbook için kullanılabilir **RequestHeaders** özelliği **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="9ada4-229">Each of these values is available to the runbook in the **RequestHeaders** property of **WebhookData**.</span></span>

![Web kancası düğmesi](media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="9ada4-231">İstek gövdesini aşağıdaki görüntüde gösterir (kullanarak bir [Fiddler](http://www.telerik.com/fiddler) izleme) runbook'a kullanılabilir **RequestBody** özelliği **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="9ada4-231">The following image shows the body of the request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available to the runbook in the **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="9ada4-232">İstek gövdesinde eklenmiştir biçimi olduğu için bu JSON olarak biçimlendirilir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-232">This is formatted as JSON because that was the format that was included in the body of the request.</span></span>     

![Web kancası düğmesi](media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="9ada4-234">Aşağıdaki resimde, Windows PowerShell ve sonuçta elde edilen yanıt gönderilen istek gösterilir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-234">The following image shows the request being sent from Windows PowerShell and the resulting response.</span></span>  <span data-ttu-id="9ada4-235">İş kimliği yanıttan ayıklanmış ve bir dizeye dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="9ada4-235">The job id is extracted from the response and converted to a string.</span></span>

![Web kancası düğmesi](media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="9ada4-237">Aşağıdaki örnek runbook'u önceki örnek isteğini kabul eder ve istek gövdesinde belirtilen sanal makineleri başlatır.</span><span class="sxs-lookup"><span data-stu-id="9ada4-237">The following sample runbook accepts the previous example request and starts the virtual machines specified in the request body.</span></span>

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

            # Authenticate to Azure resources
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
            Write-Error "Runbook mean to be started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-to-azure-alerts"></a><span data-ttu-id="9ada4-238">Azure uyarılara yanıt olarak runbook başlatılıyor</span><span class="sxs-lookup"><span data-stu-id="9ada4-238">Starting runbooks in response to Azure alerts</span></span>
<span data-ttu-id="9ada4-239">Web kancası etkin runbook'ları için tepki vermek için kullanılabilir [Azure uyarıları](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="9ada4-239">Webhook-enabled runbooks can be used to react to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="9ada4-240">Azure kaynaklarında performans, kullanılabilirlik ve Azure uyarıları yardımıyla kullanım istatistikleri toplayarak izlenebilir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-240">Resources in Azure can be monitored by collecting the statistics like performance, availability and usage with the help of Azure alerts.</span></span> <span data-ttu-id="9ada4-241">Ölçümleri izleme dayalı bir uyarı alabilirsiniz veya Azure kaynaklarınızı, şu anda Otomasyon hesapları için olaylar yalnızca ölçümleri destekler.</span><span class="sxs-lookup"><span data-stu-id="9ada4-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="9ada4-242">Belirtilen bir ölçüm değerini atanan eşiğini aştığında veya bir bildirim uyarıyı çözmek için gönderilir Hizmet Yöneticisi veya ortak yöneticileri sonra yapılandırılmış olay tetikleniyorsa, ölçümleri ve olaylar hakkında daha fazla bilgi için lütfen [Azure uyarıları](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="9ada4-242">When the value of a specified metric exceeds the threshold assigned or if the configured event is triggered then a notification is sent to the service admin or co-admins to resolve the alert, for more information on metrics and events please refer to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="9ada4-243">Azure Uyarıları Bildirim sistemi olarak kullanmanın yanı sıra, ayrıca uyarılara yanıt olarak runbook'ları devre dışı tetiklersiniz.</span><span class="sxs-lookup"><span data-stu-id="9ada4-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response to alerts.</span></span> <span data-ttu-id="9ada4-244">Azure Otomasyonu Web kancası etkin runbook'ları ile Azure uyarılar yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="9ada4-244">Azure Automation provides the capability to run webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="9ada4-245">Ölçüm aştığında, yapılandırılan eşik değeri sonra uyarı kuralı etkin hale gelir ve runbook sırayla yürütür Otomasyonu Web kancası tetikler.</span><span class="sxs-lookup"><span data-stu-id="9ada4-245">When a metric exceeds the configured threshold value then the alert rule becomes active and triggers the automation webhook which in turn executes the runbook.</span></span>

![Web kancaları](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="9ada4-247">Uyarı bağlamı</span><span class="sxs-lookup"><span data-stu-id="9ada4-247">Alert context</span></span>
<span data-ttu-id="9ada4-248">Bir sanal makine gibi bir Azure kaynağı düşünün, CPU kullanımı bu makinenin anahtar performans ölçüm biridir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of the key performance metric.</span></span> <span data-ttu-id="9ada4-249">CPU kullanımı % 100 veya belirli bir miktar fazla uzun süre, sorunu düzeltmek için sanal makineyi yeniden isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ada4-249">If the CPU utilization is 100% or more than a certain amount for long period of time, you might want to restart the virtual machine to fix the problem.</span></span> <span data-ttu-id="9ada4-250">Bu sanal makineye bir uyarı kuralı yapılandırarak çözülebilir ve bu kural CPU yüzdesi, ölçüm olarak alır.</span><span class="sxs-lookup"><span data-stu-id="9ada4-250">This can be solved by configuring an alert rule to the virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="9ada4-251">CPU yüzdesi burada yalnızca bir örnek olarak alınır ancak Azure kaynaklarınızı yapılandırabileceğiniz birçok ölçümleri vardır ve sanal makinenin yeniden başlatılması bu sorunu gidermek için gerçekleştirilecek bir eylem, diğer işlemler için runbook yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ada4-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure to your Azure resources and restarting the virtual machine is an action that is taken to fix this issue, you can configure the runbook to take other actions.</span></span>

<span data-ttu-id="9ada4-252">Bu uyarı kuralının etkin hale gelir ve tetikler Web kancası etkin runbook uyarı bağlamı runbook'a gönderir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-252">When this the alert rule becomes active and triggers the webhook-enabled runbook, it sends the alert context to the runbook.</span></span> <span data-ttu-id="9ada4-253">[Uyarı bağlamı](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) dahil olmak üzere ayrıntılarını içeren **Subscriptionıd**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** ve **zaman damgası** üzerinde bu göz önünde bulundurarak eylem kaynağı tanımlamak runbook için gerekli olan.</span><span class="sxs-lookup"><span data-stu-id="9ada4-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for the runbook to identify the resource on which it will be taking action.</span></span> <span data-ttu-id="9ada4-254">Bağlam içinde gövde bölümü katıştırılmış uyarı **WebhookData** runbook ve onu gönderilen nesnesi ile erişilebilir **Webhook.RequestBody** özelliği</span><span class="sxs-lookup"><span data-stu-id="9ada4-254">Alert context is embedded in the body part of the **WebhookData** object sent to the runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="9ada4-255">Örnek</span><span class="sxs-lookup"><span data-stu-id="9ada4-255">Example</span></span>
<span data-ttu-id="9ada4-256">Bir Azure sanal makinesi, abonelik ve ilişkilendirme oluşturma bir [CPU yüzdesi ölçüm izlemek için uyarı](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="9ada4-256">Create an Azure virtual machine in your subscription and associate an [alert to monitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="9ada4-257">Uyarı oluşturulurken Web kancası oluşturulurken oluşturulan Web kancası URL'si ile Web kancası alanını doldurmak emin olun.</span><span class="sxs-lookup"><span data-stu-id="9ada4-257">While creating the alert make sure you populate the webhook field with the URL of the webhook which was generated while creating the webhook.</span></span>

<span data-ttu-id="9ada4-258">Aşağıdaki örnek runbook'u uyarı kuralı etkin hale gelir ve runbook üzerinde bu eylemi gerçekleştirmeden kaynağı tanımlamak gerekli olan uyarı bağlam parametreleri toplar geldiğinde tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="9ada4-258">The following sample runbook is triggered when the alert rule becomes active and it collects the Alert context parameters which are required for the runbook to identify the resource on which it will be taking action.</span></span>

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

            # Outputs information on the webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain the WebhookBody containing the AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain the AlertContext     
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

            # Act on the AlertContext data, in our case restarting the VM.
            # Authenticate to your Azure subscription using Organization ID to be able to restart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check the status property of the VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart the VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant to only be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="9ada4-259">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9ada4-259">Next steps</span></span>
* <span data-ttu-id="9ada4-260">Bir runbook'u başlatmak için çeşitli yollar hakkında daha fazla bilgi için bkz [Runbook başlatma](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="9ada4-260">For details on different ways to start a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="9ada4-261">Bir Runbook işinin durumunu görüntüleme hakkında daha fazla bilgi için bkz [Azure Otomasyonu Runbook yürütme](automation-runbook-execution.md).</span><span class="sxs-lookup"><span data-stu-id="9ada4-261">For information on viewing the Status of a Runbook Job, refer to [Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="9ada4-262">Azure Uyarıları'üzerinde eyleme geçmek için Azure Otomasyonu kullanmayı öğrenmek için bkz: [Otomasyon runbook'ları ile Azure VM uyarıları düzeltmek](automation-azure-vm-alert-integration.md).</span><span class="sxs-lookup"><span data-stu-id="9ada4-262">To learn how to use Azure Automation to take action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>
