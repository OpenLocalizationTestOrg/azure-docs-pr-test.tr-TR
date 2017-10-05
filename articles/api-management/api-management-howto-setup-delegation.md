---
title: "Kullanıcı kaydı ve ürün aboneliği nasıl"
description: "Azure API Management'te üçüncü bir tarafa kullanıcı kayıt ve ürün aboneliği temsilci öğrenin."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 2637ab6405f2d4ea1da84981295a144874dfa4f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-delegate-user-registration-and-product-subscription"></a><span data-ttu-id="d701b-103">Kullanıcı kaydı ve ürün aboneliği nasıl</span><span class="sxs-lookup"><span data-stu-id="d701b-103">How to delegate user registration and product subscription</span></span>
<span data-ttu-id="d701b-104">Temsilci seçme, geliştirici oturum-açma/kaydolma ve abonelik Geliştirici Portalı'nda yerleşik işlevini kullanarak aksine ürünlere işlemek için varolan Web sitenizi kullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d701b-104">Delegation allows you to use your existing website for handling developer sign-in/sign-up and subscription to products as opposed to using the built-in functionality in the developer portal.</span></span> <span data-ttu-id="d701b-105">Bu kullanıcı verileri kendi ve özel bir biçimde adımları doğrulama gerçekleştirmek Web sitenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="d701b-105">This enables your website to own the user data and perform the validation of these steps in a custom way.</span></span>

## <span data-ttu-id="d701b-106"><a name="delegate-signin-up"></a>İçin temsilci seçme Geliştirici oturum açma ve kaydolma</span><span class="sxs-lookup"><span data-stu-id="d701b-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="d701b-107">Geliştirici temsilci seçmek için oturum açma ve kaydolma varolan Web sitesine, bir özel temsilci uç noktası sitenizdeki API Management Geliştirici Portalı'ndan başlatılan böyle bir istek için giriş noktası görevi gören oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d701b-107">To delegate developer sign-in and sign-up to your existing website you will need to create a special delegation endpoint on your site that acts as the entry-point for any such request initiated from the API Management developer portal.</span></span>

<span data-ttu-id="d701b-108">Son iş akışı şu şekilde olacaktır:</span><span class="sxs-lookup"><span data-stu-id="d701b-108">The final workflow will be as follows:</span></span>

1. <span data-ttu-id="d701b-109">API Management Geliştirici Portalı oturum açma veya kaydolma bağlantıda Geliştirici tıklar</span><span class="sxs-lookup"><span data-stu-id="d701b-109">Developer clicks on the sign-in or sign-up link at the API Management developer portal</span></span>
2. <span data-ttu-id="d701b-110">Tarayıcı temsilci uç noktasına yönlendirilir</span><span class="sxs-lookup"><span data-stu-id="d701b-110">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="d701b-111">Temsilci uç noktası iade yönlendirir veya kullanıcı oturum açma veya kaydolma isteyen kullanıcı Arabirimi gösterir</span><span class="sxs-lookup"><span data-stu-id="d701b-111">Delegation endpoint in return redirects to or presents UI asking user to sign-in or sign-up</span></span>
4. <span data-ttu-id="d701b-112">Başarı, kullanıcı bunlar başlattığınız API Management Geliştirici Portalı sayfasına geri yönlendirilir</span><span class="sxs-lookup"><span data-stu-id="d701b-112">On success, the user is redirected back to the API Management developer portal page they started from</span></span>

<span data-ttu-id="d701b-113">Başlamak için şimdi ilk kurulum API yönlendirmek için yönetim temsilci uç noktanızı ister.</span><span class="sxs-lookup"><span data-stu-id="d701b-113">To begin, let's first set-up API Management to route requests via your delegation endpoint.</span></span> <span data-ttu-id="d701b-114">API Management yayımcı Portalı'nda tıklatın **güvenlik** ve ardından **temsilci** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d701b-114">In the API Management publisher portal, click on **Security** and then click the **Delegation** tab.</span></span> <span data-ttu-id="d701b-115">'Temsilci oturum açma ve kaydolma' etkinleştirmek için onay kutusuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d701b-115">Click the checkbox to enable 'Delegate sign-in & sign-up'.</span></span>

![Temsilci seçme sayfası][api-management-delegation-signin-up]

* <span data-ttu-id="d701b-117">Hangi özel temsilci uç nokta URL'sini ve olması içinde girin karar **temsilci uç nokta URL'si** alan.</span><span class="sxs-lookup"><span data-stu-id="d701b-117">Decide what the URL of your special delegation endpoint will be and enter it in the **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="d701b-118">İçinde **temsilci kimlik doğrulama anahtarı** alan doğrulama isteği Azure API Yönetimi'nden gerçekten geldiğinden emin olun, sağlanan imza hesaplamak için kullanılan bir gizli anahtarı girin.</span><span class="sxs-lookup"><span data-stu-id="d701b-118">Within the **Delegation authentication key** field enter a secret that will be used to compute a signature provided to you for verification to ensure that the request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="d701b-119">Tıklayabilirsiniz **oluşturmak** API yönetim sizin için rastgele bir anahtar oluşturmak için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d701b-119">You can click the **generate** button to have API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="d701b-120">Oluşturmanıza gerek artık **temsilci endpoint**.</span><span class="sxs-lookup"><span data-stu-id="d701b-120">Now you need to create the **delegation endpoint**.</span></span> <span data-ttu-id="d701b-121">Çeşitli eylemleri gerçekleştirmek şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="d701b-121">It has to perform a number of actions:</span></span>

1. <span data-ttu-id="d701b-122">Bir isteği şu biçimde alırsınız:</span><span class="sxs-lookup"><span data-stu-id="d701b-122">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="d701b-123">*http://www.yourwebsite.com/apimdelegation?Operation=SignIn&returnUrl= {kaynak sayfasının URL'sini} & salt = {dize} & SIG = {dize}*</span><span class="sxs-lookup"><span data-stu-id="d701b-123">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="d701b-124">Sorgu parametreleri oturum açma / kaydolma örneği için:</span><span class="sxs-lookup"><span data-stu-id="d701b-124">Query parameters for the sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="d701b-125">**işlem**: olduğu - yalnızca olabilir temsilci istek türünü tanımlayan **Signın** bu durumda</span><span class="sxs-lookup"><span data-stu-id="d701b-125">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="d701b-126">**returnUrl**: kullanıcı bir oturum açma veya kaydolma bağlantısına tıklattığınız sayfasının URL'si</span><span class="sxs-lookup"><span data-stu-id="d701b-126">**returnUrl**: the URL of the page where the user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="d701b-127">**Salt**: güvenlik karma hesaplama için kullanılan özel bir salt dizesi</span><span class="sxs-lookup"><span data-stu-id="d701b-127">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="d701b-128">**SIG**: kendi karşılaştırma için kullanılacak bir hesaplanmış güvenlik karma karma hesaplanır</span><span class="sxs-lookup"><span data-stu-id="d701b-128">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="d701b-129">İstek Azure API Yönetimi'nden (isteğe bağlı, ancak güvenlik için önerilen yüksek oranda) geldiğini doğrulamak</span><span class="sxs-lookup"><span data-stu-id="d701b-129">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="d701b-130">Temel bir dize HMAC SHA512 karmasını işlem **returnUrl** ve **salt** sorgu parametreleri ([aşağıda sağlanan örnek kod]):</span><span class="sxs-lookup"><span data-stu-id="d701b-130">Compute an HMAC-SHA512 hash of a string based on the **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="d701b-131">HMAC (**salt** + '\n' + **returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="d701b-131">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="d701b-132">Yukarıdaki hesaplanan karma değerini karşılaştırmak **SIG** sorgu parametresi.</span><span class="sxs-lookup"><span data-stu-id="d701b-132">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="d701b-133">İki karmalar eşleşiyorsa, sonraki adıma geçin, aksi takdirde isteği reddeder.</span><span class="sxs-lookup"><span data-stu-id="d701b-133">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="d701b-134">Sign-ın/oturum-yukarı için bir istek aldığını onaylayın: **işlemi** sorgu parametresi ayarlanacak "**Signın**".</span><span class="sxs-lookup"><span data-stu-id="d701b-134">Verify that you are receiving a request for sign-in/sign-up: the **operation** query parameter will be set to "**SignIn**".</span></span>
4. <span data-ttu-id="d701b-135">Kullanıcının oturum açma veya kaydolma için kullanıcı Arabirimi ile sunması</span><span class="sxs-lookup"><span data-stu-id="d701b-135">Present the user with UI to sign-in or sign-up</span></span>
5. <span data-ttu-id="d701b-136">Kullanıcı kaydolduğunuz ise karşılık gelen bir hesap için API Management'te oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d701b-136">If the user is signing-up you have to create a corresponding account for them in API Management.</span></span> <span data-ttu-id="d701b-137">[Bir kullanıcı oluşturmak] API Management REST API ile.</span><span class="sxs-lookup"><span data-stu-id="d701b-137">[Create a user] with the API Management REST API.</span></span> <span data-ttu-id="d701b-138">Bunu yaparken, kullanıcı kimliği, kullanıcı deposunda olan aynı veya, izlemek bir kimlik olarak ayarlayın emin olun.</span><span class="sxs-lookup"><span data-stu-id="d701b-138">When doing so, ensure that you set the user ID to the same it is in your user store or to an ID that you can keep track of.</span></span>
6. <span data-ttu-id="d701b-139">Ne zaman kullanıcı başarıyla kimlik doğrulaması:</span><span class="sxs-lookup"><span data-stu-id="d701b-139">When the user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="d701b-140">[bir çoklu oturum açma (SSO) belirteci isteği] API Management REST API aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="d701b-140">[request a single-sign-on (SSO) token] via the API Management REST API</span></span>
   * <span data-ttu-id="d701b-141">API çağrısından alınan SSO URL'ye returnUrl sorgu parametresi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d701b-141">append a returnUrl query parameter to the SSO URL you have received from the API call above:</span></span>
     
     > <span data-ttu-id="d701b-142">Örneğin https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span><span class="sxs-lookup"><span data-stu-id="d701b-142">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="d701b-143">kullanıcı için yukarıdaki üretilen URL'sini yeniden yönlendirme</span><span class="sxs-lookup"><span data-stu-id="d701b-143">redirect the user to the above produced URL</span></span>

<span data-ttu-id="d701b-144">Ek olarak **Signın** işlemi de gerçekleştirebilirsiniz hesap yönetimi önceki adımları izleyerek ve aşağıdaki işlemlerden birini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="d701b-144">In addition to the **SignIn** operation, you can also perform account management by following the previous steps and using one of the following operations.</span></span>

* <span data-ttu-id="d701b-145">**Parola değiştirme**</span><span class="sxs-lookup"><span data-stu-id="d701b-145">**ChangePassword**</span></span>
* <span data-ttu-id="d701b-146">**ChangeProfile**</span><span class="sxs-lookup"><span data-stu-id="d701b-146">**ChangeProfile**</span></span>
* <span data-ttu-id="d701b-147">**CloseAccount**</span><span class="sxs-lookup"><span data-stu-id="d701b-147">**CloseAccount**</span></span>

<span data-ttu-id="d701b-148">Hesap yönetimi işlemleri için aşağıdaki sorgu parametreleri geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="d701b-148">You must pass the following query parameters for account management operations.</span></span>

* <span data-ttu-id="d701b-149">**işlem**: (parola değiştirme, ChangeProfile veya CloseAccount) için temsilci seçme isteği türünü tanımlar</span><span class="sxs-lookup"><span data-stu-id="d701b-149">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="d701b-150">**UserId**: yönetmek için hesabının kullanıcı kimliği</span><span class="sxs-lookup"><span data-stu-id="d701b-150">**userId**: the user id of the account to manage</span></span>
* <span data-ttu-id="d701b-151">**Salt**: güvenlik karma hesaplama için kullanılan özel bir salt dizesi</span><span class="sxs-lookup"><span data-stu-id="d701b-151">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="d701b-152">**SIG**: kendi karşılaştırma için kullanılacak bir hesaplanmış güvenlik karma karma hesaplanır</span><span class="sxs-lookup"><span data-stu-id="d701b-152">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>

## <span data-ttu-id="d701b-153"><a name="delegate-product-subscription"></a>Ürün aboneliği için temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="d701b-153"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="d701b-154">Ürün aboneliği için temsilci seçme, benzer şekilde kullanıcı oturum açma/yukarı için temsilci seçme için çalışır.</span><span class="sxs-lookup"><span data-stu-id="d701b-154">Delegating product subscription works similarly to delegating user sign-in/-up.</span></span> <span data-ttu-id="d701b-155">Son iş akışını aşağıdaki gibi olur:</span><span class="sxs-lookup"><span data-stu-id="d701b-155">The final workflow would be as follows:</span></span>

1. <span data-ttu-id="d701b-156">Geliştirici API Management Geliştirici Portalı'nda bir ürün seçer ve abone ol düğmesini tıklattığında</span><span class="sxs-lookup"><span data-stu-id="d701b-156">Developer selects a product in the API Management developer portal and clicks on the Subscribe button</span></span>
2. <span data-ttu-id="d701b-157">Tarayıcı temsilci uç noktasına yönlendirilir</span><span class="sxs-lookup"><span data-stu-id="d701b-157">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="d701b-158">Temsilci endpoint gerekli ürün abonelik adımları gerçekleştirir - Bu size kalmıştır ve ek sorular sormak veya yalnızca bilgilerini depolamak ve herhangi bir kullanıcı eylemi gerektirmeyen fatura bilgi istemek için başka bir sayfasına yeniden yönlendirmeye gerektirdiği</span><span class="sxs-lookup"><span data-stu-id="d701b-158">Delegation endpoint performs required product subscription steps - this is up to you and may entail redirecting to another page to request billing information, asking additional questions, or simply storing the information and not requiring any user action</span></span>

<span data-ttu-id="d701b-159">İşlevselliğini etkinleştirmek için **temsilci** sayfasında **temsilci ürün aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="d701b-159">To enable the functionality, on the **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="d701b-160">Ardından temsilci uç noktası aşağıdaki eylemleri gerçekleştirir emin olun:</span><span class="sxs-lookup"><span data-stu-id="d701b-160">Then ensure the delegation endpoint performs the following actions:</span></span>

1. <span data-ttu-id="d701b-161">Bir isteği şu biçimde alırsınız:</span><span class="sxs-lookup"><span data-stu-id="d701b-161">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="d701b-162">*{işlemi} http://www.yourwebsite.com/apimdelegation?Operation= & ProductID {abone olmak için ürün} = & UserID = {isteği yapan kullanıcı} & salt = {dize} & SIG = {dize}*</span><span class="sxs-lookup"><span data-stu-id="d701b-162">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product to subscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="d701b-163">Sorgu parametreleri ürün abonelik örneği için:</span><span class="sxs-lookup"><span data-stu-id="d701b-163">Query parameters for the product subscription case:</span></span>
   
   * <span data-ttu-id="d701b-164">**işlem**: olmasından temsilci istek türünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d701b-164">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="d701b-165">Ürün abonelik için istekleri geçerli seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d701b-165">For product subscription requests the valid options are:</span></span>
     * <span data-ttu-id="d701b-166">"Abone": kullanıcı ile belirli bir ürüne abone olmak için bir istek sağlanan kimliği (aşağıya bakın)</span><span class="sxs-lookup"><span data-stu-id="d701b-166">"Subscribe": a request to subscribe the user to a given product with provided ID (see below)</span></span>
     * <span data-ttu-id="d701b-167">"Aboneliği": bir kullanıcı bir üründen aboneliğinizi iptal etmek için bir istek</span><span class="sxs-lookup"><span data-stu-id="d701b-167">"Unsubscribe": a request to unsubscribe a user from a product</span></span>
     * <span data-ttu-id="d701b-168">"Yenile": bir requst (örneğin erecek) bir aboneliği yenilemek için</span><span class="sxs-lookup"><span data-stu-id="d701b-168">"Renew": a requst to renew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="d701b-169">**ProductID**: kullanıcının istenen abone olmak için ürün kimliği</span><span class="sxs-lookup"><span data-stu-id="d701b-169">**productId**: the ID of the product the user requested to subscribe to</span></span>
   * <span data-ttu-id="d701b-170">**UserId**: kendisi için istek yapıldığında kullanıcının kimliği</span><span class="sxs-lookup"><span data-stu-id="d701b-170">**userId**: the ID of the user for whom the request is made</span></span>
   * <span data-ttu-id="d701b-171">**Salt**: güvenlik karma hesaplama için kullanılan özel bir salt dizesi</span><span class="sxs-lookup"><span data-stu-id="d701b-171">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="d701b-172">**SIG**: kendi karşılaştırma için kullanılacak bir hesaplanmış güvenlik karma karma hesaplanır</span><span class="sxs-lookup"><span data-stu-id="d701b-172">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="d701b-173">İstek Azure API Yönetimi'nden (isteğe bağlı, ancak güvenlik için önerilen yüksek oranda) geldiğini doğrulamak</span><span class="sxs-lookup"><span data-stu-id="d701b-173">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="d701b-174">HMAC SHA512 dayalı bir dizenin işlem **ProductID**, **UserID** ve **salt** sorgu parametreleri:</span><span class="sxs-lookup"><span data-stu-id="d701b-174">Compute an HMAC-SHA512 of a string based on the **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="d701b-175">HMAC (**salt** + '\n' + **ProductID** + '\n' + **UserID**)</span><span class="sxs-lookup"><span data-stu-id="d701b-175">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="d701b-176">Yukarıdaki hesaplanan karma değerini karşılaştırmak **SIG** sorgu parametresi.</span><span class="sxs-lookup"><span data-stu-id="d701b-176">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="d701b-177">İki karmalar eşleşiyorsa, sonraki adıma geçin, aksi takdirde isteği reddeder.</span><span class="sxs-lookup"><span data-stu-id="d701b-177">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="d701b-178">İçinde istenen işlem türüne göre herhangi bir ürün Abonelik işlem gerçekleştirme **işlemi** -örn: faturalandırma, ayrıntılı sorular, vb..</span><span class="sxs-lookup"><span data-stu-id="d701b-178">Perform any product subscription processing based on the type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="d701b-179">Başarıyla abone olma, tarafındaki ürün kullanıcıya üzerinde kullanıcı tarafından API Management ürüne abone [ürün abonelik için REST API çağırmayı].</span><span class="sxs-lookup"><span data-stu-id="d701b-179">On successfully subscribing the user to the product on your side, subscribe the user to the API Management product by [calling the REST API for product subscription].</span></span>

## <span data-ttu-id="d701b-180"><a name="delegate-example-code"></a> Örnek kod</span><span class="sxs-lookup"><span data-stu-id="d701b-180"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="d701b-181">Bu kod örnekleri nasıl alınacağını Göster *temsilci doğrulama anahtarı*, ayarlanmış yayımcı portalına temsilci ekranda geçirilen returnUrl geçerliliğini kanıtlayan sonra imzayı doğrulamak için kullanılan bir HMAC oluşturmak için .</span><span class="sxs-lookup"><span data-stu-id="d701b-181">These code samples show how to take the *delegation validation key*, which is set in the Delegation screen of the publisher portal, to create a HMAC which is then used to validate the signature, proving the validity of the passed returnUrl.</span></span> <span data-ttu-id="d701b-182">Küçük değişiklik kullanıcı kimliği ve ProductID için aynı kodu çalışır.</span><span class="sxs-lookup"><span data-stu-id="d701b-182">The same code works for the productId and userId with slight modification.</span></span>

<span data-ttu-id="d701b-183">**ReturnUrl karmasını oluşturmak için C# kodu**</span><span class="sxs-lookup"><span data-stu-id="d701b-183">**C# code to generate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature to sig query parameter
}
```

<span data-ttu-id="d701b-184">**NodeJS kod returnUrl karmasını oluşturmak için**</span><span class="sxs-lookup"><span data-stu-id="d701b-184">**NodeJS code to generate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature to sig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="d701b-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d701b-185">Next steps</span></span>
<span data-ttu-id="d701b-186">Temsilci seçme hakkında daha fazla bilgi için aşağıdaki videoya bakın.</span><span class="sxs-lookup"><span data-stu-id="d701b-186">For more information on delegation, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
<span data-ttu-id="d701b-187">[bir çoklu oturum açma (SSO) belirteci isteği]: http://go.microsoft.com/fwlink/?LinkId=507409</span><span class="sxs-lookup"><span data-stu-id="d701b-187">[request a single-sign-on (SSO) token]: http://go.microsoft.com/fwlink/?LinkId=507409</span></span>
<span data-ttu-id="d701b-188">[bir kullanıcı oluşturun]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser</span><span class="sxs-lookup"><span data-stu-id="d701b-188">[create a user]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser</span></span>
<span data-ttu-id="d701b-189">[ürün abonelik için REST API çağırmayı]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO</span><span class="sxs-lookup"><span data-stu-id="d701b-189">[calling the REST API for product subscription]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO</span></span>
[Next steps]: #next-steps
<span data-ttu-id="d701b-190">[aşağıda sağlanan örnek kod]: #delegate-example-code</span><span class="sxs-lookup"><span data-stu-id="d701b-190">[example code provided below]: #delegate-example-code</span></span>

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
