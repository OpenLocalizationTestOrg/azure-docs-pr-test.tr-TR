---
title: "kayıt ve ürün aaaHow toodelegate kullanıcı aboneliği"
description: "Nasıl toodelegate kullanıcı kayıt ve ürün abonelik tooa üçüncü taraf Azure API Management'te öğrenin."
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
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a><span data-ttu-id="15d6d-103">Nasıl toodelegate kullanıcı kayıt ve ürün aboneliği</span><span class="sxs-lookup"><span data-stu-id="15d6d-103">How toodelegate user registration and product subscription</span></span>
<span data-ttu-id="15d6d-104">Temsilci toouse sağlayan Geliştirici oturum-açma/kaydolma ve abonelik tooproducts olarak işlemek için varolan Web sitenizi toousing hello hello Geliştirici Portalı'nda yerleşik bir işlevi değil.</span><span class="sxs-lookup"><span data-stu-id="15d6d-104">Delegation allows you toouse your existing website for handling developer sign-in/sign-up and subscription tooproducts as opposed toousing hello built-in functionality in hello developer portal.</span></span> <span data-ttu-id="15d6d-105">Bu Web sitesi tooown hello kullanıcı verilerinizi sağlar ve özel bir şekilde hello doğrulama bu adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="15d6d-105">This enables your website tooown hello user data and perform hello validation of these steps in a custom way.</span></span>

## <span data-ttu-id="15d6d-106"><a name="delegate-signin-up"></a>İçin temsilci seçme Geliştirici oturum açma ve kaydolma</span><span class="sxs-lookup"><span data-stu-id="15d6d-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="15d6d-107">Merhaba API Management Geliştirici Portalı'ndan başlatılan böyle bir istek için giriş noktası hello gibi davranır, sitenizde toocreate özel temsilci endpoint gerekir toodelegate Geliştirici oturum açma ve kaydolma tooyour varolan Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="15d6d-107">toodelegate developer sign-in and sign-up tooyour existing website you will need toocreate a special delegation endpoint on your site that acts as hello entry-point for any such request initiated from hello API Management developer portal.</span></span>

<span data-ttu-id="15d6d-108">Merhaba son iş akışı şu şekilde olacaktır:</span><span class="sxs-lookup"><span data-stu-id="15d6d-108">hello final workflow will be as follows:</span></span>

1. <span data-ttu-id="15d6d-109">Geliştirici hello API Management Geliştirici Portalı hello oturum açma veya kaydolma bağlantısına tıklar</span><span class="sxs-lookup"><span data-stu-id="15d6d-109">Developer clicks on hello sign-in or sign-up link at hello API Management developer portal</span></span>
2. <span data-ttu-id="15d6d-110">Yeniden yönlendirilen toohello temsilci endpoint tarayıcısıdır</span><span class="sxs-lookup"><span data-stu-id="15d6d-110">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="15d6d-111">Temsilci endpoint iade tooor sunar UI soran kullanıcı toosign açma veya kaydolma yönlendirir</span><span class="sxs-lookup"><span data-stu-id="15d6d-111">Delegation endpoint in return redirects tooor presents UI asking user toosign-in or sign-up</span></span>
4. <span data-ttu-id="15d6d-112">Başarılıysa hello kullanıcı bunlar başlattığınız yeniden yönlendirilen geri toohello API Management Geliştirici portal sayfasıdır</span><span class="sxs-lookup"><span data-stu-id="15d6d-112">On success, hello user is redirected back toohello API Management developer portal page they started from</span></span>

<span data-ttu-id="15d6d-113">toobegin, ilk kurulum API Management tooroute temsilci uç noktanızı şimdi ister.</span><span class="sxs-lookup"><span data-stu-id="15d6d-113">toobegin, let's first set-up API Management tooroute requests via your delegation endpoint.</span></span> <span data-ttu-id="15d6d-114">Merhaba API Management yayımcı Portalı'nda tıklatın **güvenlik** ve hello ardından **temsilci** sekmesi. Merhaba onay kutusunu tooenable 'Temsilci oturum açma ve kaydolma' tıklayın.</span><span class="sxs-lookup"><span data-stu-id="15d6d-114">In hello API Management publisher portal, click on **Security** and then click hello **Delegation** tab. Click hello checkbox tooenable 'Delegate sign-in & sign-up'.</span></span>

![Temsilci seçme sayfası][api-management-delegation-signin-up]

* <span data-ttu-id="15d6d-116">Hangi özel temsilci uç noktanızı hello URL'sini ve olması hello girin karar **temsilci uç nokta URL'si** alan.</span><span class="sxs-lookup"><span data-stu-id="15d6d-116">Decide what hello URL of your special delegation endpoint will be and enter it in hello **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="15d6d-117">Merhaba içinde **temsilci kimlik doğrulama anahtarı** alan isteği hello doğrulama tooensure için sağlanan imza tooyou gerçekten Azure API Yönetimi'nden gelen kullanılan toocompute olacak bir gizlilik girin.</span><span class="sxs-lookup"><span data-stu-id="15d6d-117">Within hello **Delegation authentication key** field enter a secret that will be used toocompute a signature provided tooyou for verification tooensure that hello request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="15d6d-118">Merhaba tıklayabilirsiniz **oluşturmak** düğmesini toohave API yönetim rastgele oluşturmak bir anahtarı sizin için.</span><span class="sxs-lookup"><span data-stu-id="15d6d-118">You can click hello **generate** button toohave API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="15d6d-119">Toocreate hello gereksinim artık **temsilci endpoint**.</span><span class="sxs-lookup"><span data-stu-id="15d6d-119">Now you need toocreate hello **delegation endpoint**.</span></span> <span data-ttu-id="15d6d-120">Tooperform çeşitli eylemleri içerir:</span><span class="sxs-lookup"><span data-stu-id="15d6d-120">It has tooperform a number of actions:</span></span>

1. <span data-ttu-id="15d6d-121">Bir istek form aşağıdaki hello alırsınız:</span><span class="sxs-lookup"><span data-stu-id="15d6d-121">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="15d6d-122">*http://www.yourwebsite.com/apimdelegation?Operation=SignIn&returnUrl= {kaynak sayfasının URL'sini} & salt = {dize} & SIG = {dize}*</span><span class="sxs-lookup"><span data-stu-id="15d6d-122">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="15d6d-123">Sorgu parametreleri hello oturum açma / kaydolma çalışması için:</span><span class="sxs-lookup"><span data-stu-id="15d6d-123">Query parameters for hello sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="15d6d-124">**işlem**: olduğu - yalnızca olabilir temsilci istek türünü tanımlayan **Signın** bu durumda</span><span class="sxs-lookup"><span data-stu-id="15d6d-124">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="15d6d-125">**returnUrl**: hello kullanıcı bir oturum açma veya kaydolma bağlantısına tıklattığınız hello sayfasının URL'sini hello</span><span class="sxs-lookup"><span data-stu-id="15d6d-125">**returnUrl**: hello URL of hello page where hello user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="15d6d-126">**Salt**: güvenlik karma hesaplama için kullanılan özel bir salt dizesi</span><span class="sxs-lookup"><span data-stu-id="15d6d-126">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="15d6d-127">**SIG**: kendi karşılaştırma tooyour için kullanılan bir hesaplanmış güvenlik karma toobe hesaplanan karma</span><span class="sxs-lookup"><span data-stu-id="15d6d-127">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="15d6d-128">Bu hello istek Azure API Yönetimi'nden (isteğe bağlı, ancak güvenlik için önerilen yüksek oranda) gelen doğrulayın</span><span class="sxs-lookup"><span data-stu-id="15d6d-128">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="15d6d-129">Merhaba üzerinde dayalı bir dize HMAC SHA512 karmasını işlem **returnUrl** ve **salt** sorgu parametreleri ([aşağıda sağlanan örnek kod]):</span><span class="sxs-lookup"><span data-stu-id="15d6d-129">Compute an HMAC-SHA512 hash of a string based on hello **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="15d6d-130">HMAC (**salt** + '\n' + **returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="15d6d-130">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="15d6d-131">Merhaba yukarıda hesaplanan karma toohello hello değerini karşılaştırın **SIG** sorgu parametresi.</span><span class="sxs-lookup"><span data-stu-id="15d6d-131">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="15d6d-132">Merhaba iki karmalar eşleşiyorsa toohello sonraki adımda taşıdığınızda, aksi takdirde hello isteği reddedecek.</span><span class="sxs-lookup"><span data-stu-id="15d6d-132">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="15d6d-133">Sign-ın/oturum-yukarı için bir istek aldığını onaylayın: Merhaba **işlemi** sorgu parametresi çok ayarlanacak "**Signın**".</span><span class="sxs-lookup"><span data-stu-id="15d6d-133">Verify that you are receiving a request for sign-in/sign-up: hello **operation** query parameter will be set too"**SignIn**".</span></span>
4. <span data-ttu-id="15d6d-134">Kullanıcı Arabirimi toosign açma veya kaydolma ile mevcut hello kullanıcı</span><span class="sxs-lookup"><span data-stu-id="15d6d-134">Present hello user with UI toosign-in or sign-up</span></span>
5. <span data-ttu-id="15d6d-135">Merhaba kullanıcı kaydolduğunuz ise, toocreate karşılık gelen bir hesap için API Management'te sağlayın.</span><span class="sxs-lookup"><span data-stu-id="15d6d-135">If hello user is signing-up you have toocreate a corresponding account for them in API Management.</span></span> <span data-ttu-id="15d6d-136">[Bir kullanıcı oluşturmak] hello API Management REST API ile.</span><span class="sxs-lookup"><span data-stu-id="15d6d-136">[Create a user] with hello API Management REST API.</span></span> <span data-ttu-id="15d6d-137">Bunu yaparken, aynı kullanıcı deponuzda olduğu veya, izlemek tooan kimliği hello kullanıcı kimliği toohello ayarlamak emin olun.</span><span class="sxs-lookup"><span data-stu-id="15d6d-137">When doing so, ensure that you set hello user ID toohello same it is in your user store or tooan ID that you can keep track of.</span></span>
6. <span data-ttu-id="15d6d-138">Ne zaman hello kullanıcı başarıyla kimlik doğrulaması:</span><span class="sxs-lookup"><span data-stu-id="15d6d-138">When hello user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="15d6d-139">[bir çoklu oturum açma (SSO) belirteci isteği] hello API Management REST API aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="15d6d-139">[request a single-sign-on (SSO) token] via hello API Management REST API</span></span>
   * <span data-ttu-id="15d6d-140">returnUrl sorgu parametresi toohello SSO hello API çağrısından yukarıdaki aldığınız URL Ekle:</span><span class="sxs-lookup"><span data-stu-id="15d6d-140">append a returnUrl query parameter toohello SSO URL you have received from hello API call above:</span></span>
     
     > <span data-ttu-id="15d6d-141">Örneğin https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span><span class="sxs-lookup"><span data-stu-id="15d6d-141">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="15d6d-142">URL yeniden yönlendirme hello kullanıcı toohello yukarıdaki üretilen</span><span class="sxs-lookup"><span data-stu-id="15d6d-142">redirect hello user toohello above produced URL</span></span>

<span data-ttu-id="15d6d-143">Toplama toohello içinde **Signın** işlemi de gerçekleştirebilirsiniz hesap yönetimi aşağıdaki hello önceki adımları ve işlemleri aşağıdaki hello birini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="15d6d-143">In addition toohello **SignIn** operation, you can also perform account management by following hello previous steps and using one of hello following operations.</span></span>

* <span data-ttu-id="15d6d-144">**Parola değiştirme**</span><span class="sxs-lookup"><span data-stu-id="15d6d-144">**ChangePassword**</span></span>
* <span data-ttu-id="15d6d-145">**ChangeProfile**</span><span class="sxs-lookup"><span data-stu-id="15d6d-145">**ChangeProfile**</span></span>
* <span data-ttu-id="15d6d-146">**CloseAccount**</span><span class="sxs-lookup"><span data-stu-id="15d6d-146">**CloseAccount**</span></span>

<span data-ttu-id="15d6d-147">Hesap yönetimi işlemleri için sorgu parametreleri aşağıdaki hello geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="15d6d-147">You must pass hello following query parameters for account management operations.</span></span>

* <span data-ttu-id="15d6d-148">**işlem**: (parola değiştirme, ChangeProfile veya CloseAccount) için temsilci seçme isteği türünü tanımlar</span><span class="sxs-lookup"><span data-stu-id="15d6d-148">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="15d6d-149">**UserId**: hello hesap toomanage hello kullanıcı kimliği</span><span class="sxs-lookup"><span data-stu-id="15d6d-149">**userId**: hello user id of hello account toomanage</span></span>
* <span data-ttu-id="15d6d-150">**Salt**: güvenlik karma hesaplama için kullanılan özel bir salt dizesi</span><span class="sxs-lookup"><span data-stu-id="15d6d-150">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="15d6d-151">**SIG**: kendi karşılaştırma tooyour için kullanılan bir hesaplanmış güvenlik karma toobe hesaplanan karma</span><span class="sxs-lookup"><span data-stu-id="15d6d-151">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>

## <span data-ttu-id="15d6d-152"><a name="delegate-product-subscription"></a>Ürün aboneliği için temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="15d6d-152"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="15d6d-153">Ürün aboneliği için temsilci seçme toodelegating kullanıcı oturum açma/yukarı benzer şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="15d6d-153">Delegating product subscription works similarly toodelegating user sign-in/-up.</span></span> <span data-ttu-id="15d6d-154">Merhaba son iş akışı aşağıdaki gibi olur:</span><span class="sxs-lookup"><span data-stu-id="15d6d-154">hello final workflow would be as follows:</span></span>

1. <span data-ttu-id="15d6d-155">Geliştirici hello API Management Geliştirici Portalı'nda bir ürün seçer ve hello abone ol düğmesini tıklattığında</span><span class="sxs-lookup"><span data-stu-id="15d6d-155">Developer selects a product in hello API Management developer portal and clicks on hello Subscribe button</span></span>
2. <span data-ttu-id="15d6d-156">Yeniden yönlendirilen toohello temsilci endpoint tarayıcısıdır</span><span class="sxs-lookup"><span data-stu-id="15d6d-156">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="15d6d-157">Temsilci endpoint gerekli ürün abonelik adımları gerçekleştirir - bu tooyou ve faturalama bilgileri, ek sorular sormak veya yalnızca hello bilgilerini depolamak ve herhangi bir kullanıcı eylemi gerektirmeyen yeniden yönlendirme tooanother sayfa toorequest gerektirdiği</span><span class="sxs-lookup"><span data-stu-id="15d6d-157">Delegation endpoint performs required product subscription steps - this is up tooyou and may entail redirecting tooanother page toorequest billing information, asking additional questions, or simply storing hello information and not requiring any user action</span></span>

<span data-ttu-id="15d6d-158">Merhaba üzerinde tooenable hello işlevselliği **temsilci** sayfasında **temsilci ürün aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="15d6d-158">tooenable hello functionality, on hello **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="15d6d-159">Ardından hello temsilci endpoint hello aşağıdaki eylemleri gerçekleştirir emin olun:</span><span class="sxs-lookup"><span data-stu-id="15d6d-159">Then ensure hello delegation endpoint performs hello following actions:</span></span>

1. <span data-ttu-id="15d6d-160">Bir istek form aşağıdaki hello alırsınız:</span><span class="sxs-lookup"><span data-stu-id="15d6d-160">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="15d6d-161">*{işlemi} http://www.yourwebsite.com/apimdelegation?Operation= & ProductID {ürün toosubscribe} = & UserID = {isteği yapan kullanıcı} & salt = {dize} & SIG = {dize}*</span><span class="sxs-lookup"><span data-stu-id="15d6d-161">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product toosubscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="15d6d-162">Sorgu parametreleri hello ürün abonelik çalışması için:</span><span class="sxs-lookup"><span data-stu-id="15d6d-162">Query parameters for hello product subscription case:</span></span>
   
   * <span data-ttu-id="15d6d-163">**işlem**: olmasından temsilci istek türünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="15d6d-163">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="15d6d-164">Ürün abonelik için istekleri hello geçerli seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="15d6d-164">For product subscription requests hello valid options are:</span></span>
     * <span data-ttu-id="15d6d-165">"Abone": ürünle birlikte verilen bir istek toosubscribe hello kullanıcı tooa sağlanan kimliği (aşağıya bakın)</span><span class="sxs-lookup"><span data-stu-id="15d6d-165">"Subscribe": a request toosubscribe hello user tooa given product with provided ID (see below)</span></span>
     * <span data-ttu-id="15d6d-166">"Aboneliği": İstek toounsubscribe bir ürün kullanıcıdan</span><span class="sxs-lookup"><span data-stu-id="15d6d-166">"Unsubscribe": a request toounsubscribe a user from a product</span></span>
     * <span data-ttu-id="15d6d-167">"Yenile": requst toorenew (örneğin erecek) bir abonelik</span><span class="sxs-lookup"><span data-stu-id="15d6d-167">"Renew": a requst toorenew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="15d6d-168">**ProductID**: hello hello ürün hello kullanıcının Kimliğini istenen toosubscribe için</span><span class="sxs-lookup"><span data-stu-id="15d6d-168">**productId**: hello ID of hello product hello user requested toosubscribe to</span></span>
   * <span data-ttu-id="15d6d-169">**UserId**: kendisi için hello istek yapıldığında hello kullanıcının Kimliğini hello</span><span class="sxs-lookup"><span data-stu-id="15d6d-169">**userId**: hello ID of hello user for whom hello request is made</span></span>
   * <span data-ttu-id="15d6d-170">**Salt**: güvenlik karma hesaplama için kullanılan özel bir salt dizesi</span><span class="sxs-lookup"><span data-stu-id="15d6d-170">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="15d6d-171">**SIG**: kendi karşılaştırma tooyour için kullanılan bir hesaplanmış güvenlik karma toobe hesaplanan karma</span><span class="sxs-lookup"><span data-stu-id="15d6d-171">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="15d6d-172">Bu hello istek Azure API Yönetimi'nden (isteğe bağlı, ancak güvenlik için önerilen yüksek oranda) gelen doğrulayın</span><span class="sxs-lookup"><span data-stu-id="15d6d-172">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="15d6d-173">HMAC SHA512 üzerinde hello dayalı bir dizenin işlem **ProductID**, **UserID** ve **salt** sorgu parametreleri:</span><span class="sxs-lookup"><span data-stu-id="15d6d-173">Compute an HMAC-SHA512 of a string based on hello **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="15d6d-174">HMAC (**salt** + '\n' + **ProductID** + '\n' + **UserID**)</span><span class="sxs-lookup"><span data-stu-id="15d6d-174">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="15d6d-175">Merhaba yukarıda hesaplanan karma toohello hello değerini karşılaştırın **SIG** sorgu parametresi.</span><span class="sxs-lookup"><span data-stu-id="15d6d-175">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="15d6d-176">Merhaba iki karmalar eşleşiyorsa toohello sonraki adımda taşıdığınızda, aksi takdirde hello isteği reddedecek.</span><span class="sxs-lookup"><span data-stu-id="15d6d-176">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="15d6d-177">İçinde istenen işlemi hello türüne göre herhangi bir ürün Abonelik işlem gerçekleştirme **işlemi** -örn: faturalandırma, ayrıntılı sorular, vb..</span><span class="sxs-lookup"><span data-stu-id="15d6d-177">Perform any product subscription processing based on hello type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="15d6d-178">Merhaba kullanıcı toohello ürün, tarafında başarıyla abone üzerinde hello kullanıcı toohello API Management ürün abone [ürün abonelik için REST API çağırma hello].</span><span class="sxs-lookup"><span data-stu-id="15d6d-178">On successfully subscribing hello user toohello product on your side, subscribe hello user toohello API Management product by [calling hello REST API for product subscription].</span></span>

## <span data-ttu-id="15d6d-179"><a name="delegate-example-code"></a> Örnek kod</span><span class="sxs-lookup"><span data-stu-id="15d6d-179"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="15d6d-180">Bu kod örnekleri Göster nasıl tootake hello *temsilci doğrulama anahtarı*hello yayımcı portalının temsilci ekranında hello ayarlayın, toocreate sonra olan bir HMAC kullanılan hello hello geçerliliğini kanıtlayan toovalidate hello imza geçirilen returnUrl.</span><span class="sxs-lookup"><span data-stu-id="15d6d-180">These code samples show how tootake hello *delegation validation key*, which is set in hello Delegation screen of hello publisher portal, toocreate a HMAC which is then used toovalidate hello signature, proving hello validity of hello passed returnUrl.</span></span> <span data-ttu-id="15d6d-181">Merhaba hello ProductID ve küçük değişiklik kullanıcı kimliği için aynı kodu çalışır.</span><span class="sxs-lookup"><span data-stu-id="15d6d-181">hello same code works for hello productId and userId with slight modification.</span></span>

<span data-ttu-id="15d6d-182">**C# kod toogenerate karmasını returnUrl**</span><span class="sxs-lookup"><span data-stu-id="15d6d-182">**C# code toogenerate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

<span data-ttu-id="15d6d-183">**NodeJS kod toogenerate returnUrl karmasını**</span><span class="sxs-lookup"><span data-stu-id="15d6d-183">**NodeJS code toogenerate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="15d6d-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="15d6d-184">Next steps</span></span>
<span data-ttu-id="15d6d-185">Temsilci seçme hakkında daha fazla bilgi için video aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="15d6d-185">For more information on delegation, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[bir çoklu oturum açma (SSO) belirteci isteği]: http://go.microsoft.com/fwlink/?LinkId=507409
[bir kullanıcı oluşturun]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[ürün abonelik için REST API çağırma hello]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[aşağıda sağlanan örnek kod]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
