---
title: "Azure Active Directory B2C: özel ilkeler kullanarak bir Azure AD Sağlayıcısı Ekle | Microsoft Docs"
description: "Azure Active Directory B2C özel ilkeleri hakkında bilgi edinin"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 31f0dfe5-1ad0-4a25-a53b-8acc71bcea72
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: 9b0c32086cebc171d91da2e7bfb48136723ccd4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a><span data-ttu-id="e90f6-103">Azure Active Directory B2C: Azure AD hesapları kullanarak oturum açın</span><span class="sxs-lookup"><span data-stu-id="e90f6-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="e90f6-104">Bu makalede nasıl tooenable oturum açmak için kullanıcılar hello kullanımı aracılığıyla belirli bir Azure Active Directory (Azure AD) kuruluştan gösterilmektedir [özel ilkeler](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="e90f6-104">This article shows you how tooenable sign-in for users from a specific Azure Active Directory (Azure AD) organization through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e90f6-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e90f6-105">Prerequisites</span></span>

<span data-ttu-id="e90f6-106">Tam hello adımları hello [özel ilkeleri ile çalışmaya başlama](active-directory-b2c-get-started-custom.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="e90f6-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="e90f6-107">Bu adımlar şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="e90f6-107">These steps include:</span></span>

1. <span data-ttu-id="e90f6-108">Bir Azure Active Directory B2C oluşturma (Azure AD B2C) Kiracı.</span><span class="sxs-lookup"><span data-stu-id="e90f6-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
2. <span data-ttu-id="e90f6-109">Bir Azure AD B2C uygulaması oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="e90f6-109">Creating an Azure AD B2C application.</span></span>
3. <span data-ttu-id="e90f6-110">İki ilke altyapısı uygulama kaydediliyor.</span><span class="sxs-lookup"><span data-stu-id="e90f6-110">Registering two policy-engine applications.</span></span>
4. <span data-ttu-id="e90f6-111">Anahtarları ayarlama.</span><span class="sxs-lookup"><span data-stu-id="e90f6-111">Setting up keys.</span></span>
5. <span data-ttu-id="e90f6-112">Merhaba başlangıç paketi ayarlama.</span><span class="sxs-lookup"><span data-stu-id="e90f6-112">Setting up hello starter pack.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="e90f6-113">Bir Azure AD uygulaması oluştur</span><span class="sxs-lookup"><span data-stu-id="e90f6-113">Create an Azure AD app</span></span>

<span data-ttu-id="e90f6-114">tooenable oturum açma belirli kullanıcılar için Azure AD kuruluş tooregister hello kuruluş Azure AD Kiracı içinde bir uygulama gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="e90f6-114">tooenable sign-in for users from a specific Azure AD organization, you need tooregister an application within hello organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="e90f6-115">"Contoso.com" Merhaba kuruluş Azure AD Kiracı ve "fabrikamb2c.onmicrosoft.com" için yönergeleri izleyerek hello hello Azure AD B2C Kiracı olarak kullanırız.</span><span class="sxs-lookup"><span data-stu-id="e90f6-115">We use "contoso.com" for hello organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as hello Azure AD B2C tenant in hello following instructions.</span></span>

1. <span data-ttu-id="e90f6-116">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e90f6-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="e90f6-117">Merhaba üst çubuğunda hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="e90f6-117">On hello top bar, select your account.</span></span> <span data-ttu-id="e90f6-118">Merhaba gelen **Directory** listesinde, uygulamanız (contoso.com) hello kuruluş Azure AD Kiracı tooregister istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="e90f6-118">From hello **Directory** list, choose hello organizational Azure AD tenant where you want tooregister your application (contoso.com).</span></span>
1. <span data-ttu-id="e90f6-119">Seçin **daha fazla hizmet** hello sol bölmesinde ve "Uygulama kayıtlar" için arama</span><span class="sxs-lookup"><span data-stu-id="e90f6-119">Select **More services** in hello left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="e90f6-120">Seçin **yeni uygulama kaydı**.</span><span class="sxs-lookup"><span data-stu-id="e90f6-120">Select **New application registration**.</span></span>
1. <span data-ttu-id="e90f6-121">Uygulamanız için bir ad girin (örneğin, `Azure AD B2C App`).</span><span class="sxs-lookup"><span data-stu-id="e90f6-121">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="e90f6-122">Seçin **Web uygulaması / API** hello uygulama türü için.</span><span class="sxs-lookup"><span data-stu-id="e90f6-122">Select **Web app / API** for hello application type.</span></span>
1. <span data-ttu-id="e90f6-123">İçin **oturum açma URL'si**, URL, aşağıdaki hello girin nerede `yourtenant` hello Azure AD B2C kiracınızın adıyla değiştirilen (`fabrikamb2c.onmicrosoft.com`):</span><span class="sxs-lookup"><span data-stu-id="e90f6-123">For **Sign-on URL**, enter hello following URL, where `yourtenant` is replaced by hello name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="e90f6-124">Kaydet Hello uygulama kimliği.</span><span class="sxs-lookup"><span data-stu-id="e90f6-124">Save hello application ID.</span></span>
1. <span data-ttu-id="e90f6-125">Yeni oluşturulan hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="e90f6-125">Select hello newly created application.</span></span>
1. <span data-ttu-id="e90f6-126">Merhaba altında **ayarları** dikey penceresinde, select **anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="e90f6-126">Under hello **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="e90f6-127">Yeni bir anahtar oluşturun ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e90f6-127">Create a new key, and save it.</span></span> <span data-ttu-id="e90f6-128">Merhaba sonraki bölümde hello adımlarda kullanır.</span><span class="sxs-lookup"><span data-stu-id="e90f6-128">You will use it in hello steps in hello next section.</span></span>

## <a name="add-hello-azure-ad-key-tooazure-ad-b2c"></a><span data-ttu-id="e90f6-129">Hello Azure AD anahtar tooAzure AD B2C ekleme</span><span class="sxs-lookup"><span data-stu-id="e90f6-129">Add hello Azure AD key tooAzure AD B2C</span></span>

<span data-ttu-id="e90f6-130">Azure AD B2C kiracınızda toostore hello contoso.com uygulama anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="e90f6-130">You need toostore hello contoso.com application key in your Azure AD B2C tenant.</span></span> <span data-ttu-id="e90f6-131">toodo bu:</span><span class="sxs-lookup"><span data-stu-id="e90f6-131">toodo this:</span></span>
1. <span data-ttu-id="e90f6-132">Tooyour Azure AD B2C Kiracı gidip seçin **B2C ayarlarını** > **kimlik deneyimi Framework** > **İlkesi anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="e90f6-132">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="e90f6-133">Seçin **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e90f6-133">Select **+Add**.</span></span>
1. <span data-ttu-id="e90f6-134">Bu seçenekler girin veya seçin:</span><span class="sxs-lookup"><span data-stu-id="e90f6-134">Select or enter these options:</span></span>
   * <span data-ttu-id="e90f6-135">Seçin **el ile**.</span><span class="sxs-lookup"><span data-stu-id="e90f6-135">Select **Manual**.</span></span>
   * <span data-ttu-id="e90f6-136">İçin **adı**, Azure AD Kiracı adı ile eşleşen bir ad seçin (örneğin, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="e90f6-136">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span></span>  <span data-ttu-id="e90f6-137">Merhaba önek `B2C_1A_` anahtarınızı toohello adını otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="e90f6-137">hello prefix `B2C_1A_` is added automatically toohello name of your key.</span></span>
   * <span data-ttu-id="e90f6-138">Uygulama anahtarınızı hello Yapıştır **gizli** kutusu.</span><span class="sxs-lookup"><span data-stu-id="e90f6-138">Paste your application key in hello **Secret** box.</span></span>
   * <span data-ttu-id="e90f6-139">Seçin **imza**.</span><span class="sxs-lookup"><span data-stu-id="e90f6-139">Select **Signature**.</span></span>
1. <span data-ttu-id="e90f6-140">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="e90f6-140">Select **Create**.</span></span>
1. <span data-ttu-id="e90f6-141">Başlangıç anahtarı oluşturduğunuz onaylayın `B2C_1A_ContosoAppSecret`.</span><span class="sxs-lookup"><span data-stu-id="e90f6-141">Confirm that you've created hello key `B2C_1A_ContosoAppSecret`.</span></span>


## <a name="add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="e90f6-142">Bir talep sağlayıcı temel ilkenizde ekleme</span><span class="sxs-lookup"><span data-stu-id="e90f6-142">Add a claims provider in your base policy</span></span>

<span data-ttu-id="e90f6-143">Kullanıcıların toosign Azure AD kullanarak istiyorsanız, Talep sağlayıcı olarak Azure AD toodefine gerekir.</span><span class="sxs-lookup"><span data-stu-id="e90f6-143">If you want users toosign in by using Azure AD, you need toodefine Azure AD as a claims provider.</span></span> <span data-ttu-id="e90f6-144">Diğer bir deyişle, Azure AD B2C ile iletişim kuracak bir uç nokta toospecify gerekir.</span><span class="sxs-lookup"><span data-stu-id="e90f6-144">In other words, you need toospecify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="e90f6-145">Merhaba endpoint belirli bir kullanıcı doğrulaması Azure AD B2C tooverify tarafından kullanılan talepler kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="e90f6-145">hello endpoint will provide a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span> 

<span data-ttu-id="e90f6-146">Azure AD toohello ekleyerek bir talep sağlayıcısı olarak Azure AD tanımlayabilirsiniz `<ClaimsProvider>` ilkenizin hello uzantısı dosyasında düğümü:</span><span class="sxs-lookup"><span data-stu-id="e90f6-146">You can define Azure AD as a claims provider by adding Azure AD toohello `<ClaimsProvider>` node in hello extension file of your policy:</span></span>

1. <span data-ttu-id="e90f6-147">Merhaba uzantısının (TrustFrameworkExtensions.xml) çalışma dizininizi açın.</span><span class="sxs-lookup"><span data-stu-id="e90f6-147">Open hello extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="e90f6-148">Hello bulur `<ClaimsProviders>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="e90f6-148">Find hello `<ClaimsProviders>` section.</span></span> <span data-ttu-id="e90f6-149">Yoksa, hello kök düğümü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e90f6-149">If it does not exist, add it under hello root node.</span></span>
1. <span data-ttu-id="e90f6-150">Yeni bir ekleme `<ClaimsProvider>` şekilde düğümü:</span><span class="sxs-lookup"><span data-stu-id="e90f6-150">Add a new `<ClaimsProvider>` node as follows:</span></span>

    ```XML
    <ClaimsProvider>
        <Domain>Contoso</Domain>
        <DisplayName>Login using Contoso</DisplayName>
        <TechnicalProfiles>
            <TechnicalProfile Id="ContosoProfile">
                <DisplayName>Contoso Employee</DisplayName>
                <Description>Login with your Contoso account</Description>
                <Protocol Name="OpenIdConnect"/>
                <OutputTokenFormat>JWT</OutputTokenFormat>
                <Metadata>
                    <Item Key="METADATA">https://login.windows.net/contoso.com/.well-known/openid-configuration</Item>
                    <Item Key="ProviderName">https://sts.windows.net/00000000-0000-0000-0000-000000000000/</Item>
                    <Item Key="client_id">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="IdTokenAudience">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="response_types">id_token</Item>
                    <Item Key="UsePolicyInRedirectUri">false</Item>
                </Metadata>
                <CryptographicKeys>
                    <Key Id="client_secret" StorageReferenceId="B2C_1A_ContosoAppSecret"/>
                </CryptographicKeys>
                <OutputClaims>
                    <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="oid"/>
                    <OutputClaim ClaimTypeReferenceId="tenantId" PartnerClaimType="tid"/>
                    <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
                    <OutputClaim ClaimTypeReferenceId="surName" PartnerClaimType="family_name" />
                    <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
                    <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="contosoAuthentication" />
                    <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="AzureADContoso" />
                </OutputClaims>
                <OutputClaimsTransformations>
                    <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
                    <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
                    <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
                    <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
                </OutputClaimsTransformations>
                <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
            </TechnicalProfile>
        </TechnicalProfiles>
    </ClaimsProvider>
    ```

1. <span data-ttu-id="e90f6-151">Merhaba altında `<ClaimsProvider>` düğümü, güncelleştirme hello değeri `<Domain>` kullanılan toodistinguish olabilir benzersiz bir değer tooa bu diğer kimlik sağlayıcılardan gelen.</span><span class="sxs-lookup"><span data-stu-id="e90f6-151">Under hello `<ClaimsProvider>` node, update hello value for `<Domain>` tooa unique value that can be used toodistinguish it from other identity providers.</span></span>
1. <span data-ttu-id="e90f6-152">Merhaba altında `<ClaimsProvider>` düğümü, güncelleştirme hello değeri `<DisplayName>` hello için kolay ad tooa talep sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="e90f6-152">Under hello `<ClaimsProvider>` node, update hello value for `<DisplayName>` tooa friendly name for hello claims provider.</span></span> <span data-ttu-id="e90f6-153">Bu değer şu anda kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="e90f6-153">This value is not currently used.</span></span>

### <a name="update-hello-technical-profile"></a><span data-ttu-id="e90f6-154">Merhaba teknik profilini güncelleştir</span><span class="sxs-lookup"><span data-stu-id="e90f6-154">Update hello technical profile</span></span>

<span data-ttu-id="e90f6-155">tooget hello Azure AD uç noktasından bir belirteç, toodefine hello protokolleri Azure AD B2C Azure AD ile toocommunicate kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e90f6-155">tooget a token from hello Azure AD endpoint, you need toodefine hello protocols that Azure AD B2C should use toocommunicate with Azure AD.</span></span> <span data-ttu-id="e90f6-156">Bu hello içinde yapılır `<TechnicalProfile>` öğesinin `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="e90f6-156">This is done inside hello `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span></span>
1. <span data-ttu-id="e90f6-157">Merhaba Hello Kimliğini güncelleştirme `<TechnicalProfile>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="e90f6-157">Update hello ID of hello `<TechnicalProfile>` node.</span></span> <span data-ttu-id="e90f6-158">Bu kimliği kullanılan toorefer toothis hello İlkesi diğer kısımlarından teknik profilidir.</span><span class="sxs-lookup"><span data-stu-id="e90f6-158">This ID is used toorefer toothis technical profile from other parts of hello policy.</span></span>
1. <span data-ttu-id="e90f6-159">Merhaba değeri güncelleştirme `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="e90f6-159">Update hello value for `<DisplayName>`.</span></span> <span data-ttu-id="e90f6-160">Bu değer, oturum açma hello düğmesine oturum açma ekranında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e90f6-160">This value will be displayed on hello sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="e90f6-161">Merhaba değeri güncelleştirme `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="e90f6-161">Update hello value for `<Description>`.</span></span>
1. <span data-ttu-id="e90f6-162">Azure AD hello Openıd Connect protokolünü kullanır, böylece bu hello değeri sağlamak `<Protocol>` olan `"OpenIdConnect"`.</span><span class="sxs-lookup"><span data-stu-id="e90f6-162">Azure AD uses hello OpenID Connect protocol, so ensure that hello value for `<Protocol>` is `"OpenIdConnect"`.</span></span>

<span data-ttu-id="e90f6-163">Tooupdate hello gereksinim `<Metadata>` hello XML dosyasındaki bölümünde başvurulan tooearlier tooreflect hello yapılandırma ayarları için özel Azure AD kiracısı.</span><span class="sxs-lookup"><span data-stu-id="e90f6-163">You need tooupdate hello `<Metadata>` section in hello XML file referred tooearlier tooreflect hello configuration settings for your specific Azure AD tenant.</span></span> <span data-ttu-id="e90f6-164">Merhaba XML dosyasında hello meta veri değerleri şu şekilde güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="e90f6-164">In hello XML file, update hello metadata values as follows:</span></span>

1. <span data-ttu-id="e90f6-165">Ayarlama `<Item Key="METADATA">` çok`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, burada `yourAzureADtenant` Azure AD Kiracı adınız (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="e90f6-165">Set `<Item Key="METADATA">` too`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span></span>
1. <span data-ttu-id="e90f6-166">Tarayıcı ve Git toohello açmak `METADATA` güncelleştirdiğiniz URL.</span><span class="sxs-lookup"><span data-stu-id="e90f6-166">Open your browser and go toohello `METADATA` URL that you just updated.</span></span>
1. <span data-ttu-id="e90f6-167">Merhaba tarayıcıda hello 'dağıtımcı' nesnesi için konum ve değerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="e90f6-167">In hello browser, look for hello 'issuer' object and copy its value.</span></span> <span data-ttu-id="e90f6-168">Merhaba aşağıdaki gibi görünmelidir: `https://sts.windows.net/{tenantId}/`.</span><span class="sxs-lookup"><span data-stu-id="e90f6-168">It should look like hello following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="e90f6-169">Yapıştırmak için hello değer `<Item Key="ProviderName">` hello XML dosyasında.</span><span class="sxs-lookup"><span data-stu-id="e90f6-169">Paste hello value for `<Item Key="ProviderName">` in hello XML file.</span></span>
1. <span data-ttu-id="e90f6-170">Ayarlama `<Item Key="client_id">` hello uygulama kaydı toohello uygulama kimliği.</span><span class="sxs-lookup"><span data-stu-id="e90f6-170">Set `<Item Key="client_id">` toohello application ID from hello app registration.</span></span>
1. <span data-ttu-id="e90f6-171">Ayarlama `<Item Key="IdTokenAudience">` hello uygulama kaydı toohello uygulama kimliği.</span><span class="sxs-lookup"><span data-stu-id="e90f6-171">Set `<Item Key="IdTokenAudience">` toohello application ID from hello app registration.</span></span>
1. <span data-ttu-id="e90f6-172">Emin `<Item Key="response_types">` çok ayarlanır`id_token`.</span><span class="sxs-lookup"><span data-stu-id="e90f6-172">Ensure that `<Item Key="response_types">` is set too`id_token`.</span></span>
1. <span data-ttu-id="e90f6-173">Emin `<Item Key="UsePolicyInRedirectUri">` çok ayarlanır`false`.</span><span class="sxs-lookup"><span data-stu-id="e90f6-173">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set too`false`.</span></span>

<span data-ttu-id="e90f6-174">Ayrıca, Azure AD B2C Kiracı toohello Azure AD kayıtlı toolink hello Azure AD parola gerekir `<ClaimsProvider>` bilgi:</span><span class="sxs-lookup"><span data-stu-id="e90f6-174">You also need toolink hello Azure AD secret that you registered in your Azure AD B2C tenant toohello Azure AD `<ClaimsProvider>` information:</span></span>

* <span data-ttu-id="e90f6-175">Merhaba, `<CryptographicKeys>` hello XML dosyası önceki bölümünde, güncelleştirmek için hello değer `StorageReferenceId` tanımladığınız hello gizli toohello başvuru kimliği (örneğin, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="e90f6-175">In hello `<CryptographicKeys>` section in hello preceding XML file, update hello value for `StorageReferenceId` toohello reference ID of hello secret that you defined (for example, `ContosoAppSecret`).</span></span>

### <a name="upload-hello-extension-file-for-verification"></a><span data-ttu-id="e90f6-176">Doğrulama Hello uzantısı dosyasını karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="e90f6-176">Upload hello extension file for verification</span></span>

<span data-ttu-id="e90f6-177">Artık, böylece Azure AD B2C bilir ilkeniz yapılandırmış olduğunuz nasıl toocommunicate Azure AD dizininizi ile.</span><span class="sxs-lookup"><span data-stu-id="e90f6-177">By now, you have configured your policy so that Azure AD B2C knows how toocommunicate with your Azure AD directory.</span></span> <span data-ttu-id="e90f6-178">Bu sorunları kadar sahip olmadığı için ilke yalnızca tooconfirm Hello uzantısı dosyasını karşıya yüklemeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="e90f6-178">Try uploading hello extension file of your policy just tooconfirm that it doesn't have any issues so far.</span></span> <span data-ttu-id="e90f6-179">toodo için:</span><span class="sxs-lookup"><span data-stu-id="e90f6-179">toodo so:</span></span>

1. <span data-ttu-id="e90f6-180">Açık hello **tüm ilkeler** dikey penceresinde, Azure AD B2C kiracısı.</span><span class="sxs-lookup"><span data-stu-id="e90f6-180">Open hello **All Policies** blade in your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="e90f6-181">Merhaba denetleyin **varsa hello ilkesi üzerine** kutusu.</span><span class="sxs-lookup"><span data-stu-id="e90f6-181">Check hello **Overwrite hello policy if it exists** box.</span></span>
1. <span data-ttu-id="e90f6-182">Merhaba uzantısının (TrustFrameworkExtensions.xml) karşıya yükleyin ve hello doğrulama başlayabildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="e90f6-182">Upload hello extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail hello validation.</span></span>

## <a name="register-hello-azure-ad-claims-provider-tooa-user-journey"></a><span data-ttu-id="e90f6-183">Hello Azure AD talep sağlayıcısı tooa kullanıcı gezisine kaydetme</span><span class="sxs-lookup"><span data-stu-id="e90f6-183">Register hello Azure AD claims provider tooa user journey</span></span>

<span data-ttu-id="e90f6-184">Şimdi tooadd hello Azure AD kimlik sağlayıcısı tooone kullanıcı Yolculuklar biri gerekir.</span><span class="sxs-lookup"><span data-stu-id="e90f6-184">You now need tooadd hello Azure AD identity provider tooone of your user journeys.</span></span> <span data-ttu-id="e90f6-185">Bu noktada, hello kimlik sağlayıcısı ayarlandı, ancak hello oturumu-up/oturum açma ekranları hiçbirinde kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="e90f6-185">At this point, hello identity provider has been set up, but it’s not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="e90f6-186">toomake, kullanılabilir var olan bir şablonu kullanıcı gezisine bir kopyasını oluşturur ve ardından değiştirin hello Azure AD kimlik sağlayıcısı de vardır:</span><span class="sxs-lookup"><span data-stu-id="e90f6-186">toomake it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has hello Azure AD identity provider:</span></span>

1. <span data-ttu-id="e90f6-187">Merhaba temel dosyanın ilkenizin (örneğin, TrustFrameworkBase.xml) açın.</span><span class="sxs-lookup"><span data-stu-id="e90f6-187">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="e90f6-188">Hello bulur `<UserJourneys>` öğesi ve kopyalama hello tüm `<UserJourney>` içeren düğüm `Id="SignUpOrSignIn"`.</span><span class="sxs-lookup"><span data-stu-id="e90f6-188">Find hello `<UserJourneys>` element and copy hello entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="e90f6-189">Merhaba uzantısının (örneğin, TrustFrameworkExtensions.xml) açın ve hello bulur `<UserJourneys>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="e90f6-189">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="e90f6-190">Merhaba öğe yoksa, ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e90f6-190">If hello element doesn't exist, add one.</span></span>
1. <span data-ttu-id="e90f6-191">Yapıştır hello tüm `<UserJourney>` hello alt sitesi olarak kopyaladığınız düğümü `<UserJourneys>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="e90f6-191">Paste hello entire `<UserJourney>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="e90f6-192">Merhaba yeni kullanıcı gezisine Hello Kimliğini yeniden adlandırın (örneğin, olarak yeniden adlandırın `SignUpOrSignUsingContoso`).</span><span class="sxs-lookup"><span data-stu-id="e90f6-192">Rename hello ID of hello new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="e90f6-193">Görüntü hello "button"</span><span class="sxs-lookup"><span data-stu-id="e90f6-193">Display hello "button"</span></span>

<span data-ttu-id="e90f6-194">Merhaba `<ClaimsProviderSelection>` benzer tooan kimlik sağlayıcısı düğmesi oturumu-up/oturum açma ekranında bir öğedir.</span><span class="sxs-lookup"><span data-stu-id="e90f6-194">hello `<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="e90f6-195">Eklerseniz bir `<ClaimsProviderSelection>` öğesi Azure AD için yeni bir düğme görüntülenir hello sayfasında bir kullanıcı adlandırıldığını olduğunda.</span><span class="sxs-lookup"><span data-stu-id="e90f6-195">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="e90f6-196">tooadd bu öğe:</span><span class="sxs-lookup"><span data-stu-id="e90f6-196">tooadd this element:</span></span>

1. <span data-ttu-id="e90f6-197">Hello bulur `<OrchestrationStep>` içeren düğüm `Order="1"` oluşturduğunuz hello kullanıcı gezisine içinde.</span><span class="sxs-lookup"><span data-stu-id="e90f6-197">Find hello `<OrchestrationStep>` node that includes `Order="1"` in hello user journey that you just created.</span></span>
1. <span data-ttu-id="e90f6-198">Merhaba aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e90f6-198">Add hello following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. <span data-ttu-id="e90f6-199">Ayarlama `TargetClaimsExchangeId` tooan uygun değeri.</span><span class="sxs-lookup"><span data-stu-id="e90f6-199">Set `TargetClaimsExchangeId` tooan appropriate value.</span></span> <span data-ttu-id="e90f6-200">Aşağıdaki hello aynı öneririz başkalarının olarak kuralı:  *\[ClaimProviderName\]Exchange*.</span><span class="sxs-lookup"><span data-stu-id="e90f6-200">We recommend following hello same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="e90f6-201">Bağlantı hello düğmesi tooan eylemi</span><span class="sxs-lookup"><span data-stu-id="e90f6-201">Link hello button tooan action</span></span>

<span data-ttu-id="e90f6-202">Yerinde bir düğmeye sahip olduğunuza göre toolink gerekir, tooan eylem.</span><span class="sxs-lookup"><span data-stu-id="e90f6-202">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="e90f6-203">Merhaba, bu durumda, Azure AD tooreceive ile Azure AD B2C toocommunicate için bir belirteç eylemdir.</span><span class="sxs-lookup"><span data-stu-id="e90f6-203">hello action, in this case, is for Azure AD B2C toocommunicate with Azure AD tooreceive a token.</span></span> <span data-ttu-id="e90f6-204">Merhaba düğmesi tooan eylemi, Azure AD talep sağlayıcısı hello teknik profili bağlayarak Bağla:</span><span class="sxs-lookup"><span data-stu-id="e90f6-204">Link hello button tooan action by linking hello technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="e90f6-205">Hello bulur `<OrchestrationStep>` içeren `Order="2"` hello içinde `<UserJourney>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="e90f6-205">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
1. <span data-ttu-id="e90f6-206">Merhaba aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e90f6-206">Add hello following:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. <span data-ttu-id="e90f6-207">Güncelleştirme `Id` aynı değer aynı toohello `TargetClaimsExchangeId` bölüm önceki hello içinde.</span><span class="sxs-lookup"><span data-stu-id="e90f6-207">Update `Id` toohello same value as that of `TargetClaimsExchangeId` in hello preceding section.</span></span>
1. <span data-ttu-id="e90f6-208">Güncelleştirme `TechnicalProfileReferenceId` hello teknik toohello Kimliğini profil daha önce oluşturduğunuz (ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="e90f6-208">Update `TechnicalProfileReferenceId` toohello ID of hello technical profile you created earlier (ContosoProfile).</span></span>

### <a name="upload-hello-updated-extension-file"></a><span data-ttu-id="e90f6-209">Merhaba güncelleştirilmiş uzantısı dosyasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="e90f6-209">Upload hello updated extension file</span></span>

<span data-ttu-id="e90f6-210">Değiştirme hello uzantısının yapılır.</span><span class="sxs-lookup"><span data-stu-id="e90f6-210">You are done modifying hello extension file.</span></span> <span data-ttu-id="e90f6-211">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e90f6-211">Save it.</span></span> <span data-ttu-id="e90f6-212">Merhaba dosyasını karşıya yükleyin ve tüm doğrulamaları başarılı olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e90f6-212">Then upload hello file, and ensure that all validations succeed.</span></span>

### <a name="update-hello-rp-file"></a><span data-ttu-id="e90f6-213">Merhaba RP dosyasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="e90f6-213">Update hello RP file</span></span>

<span data-ttu-id="e90f6-214">Şimdi yeni oluşturduğunuz hello kullanıcı gezisine başlatacaktır tooupdate hello bağlı olan taraf (RP) dosya gerekir:</span><span class="sxs-lookup"><span data-stu-id="e90f6-214">You now need tooupdate hello relying party (RP) file that will initiate hello user journey that you just created:</span></span>

1. <span data-ttu-id="e90f6-215">Çalışma dizininizi SignUpOrSignIn.xml bir kopyasını oluşturun ve yeniden adlandırın (örneğin, tooSignUpOrSignInWithAAD.xml yeniden adlandırmadan).</span><span class="sxs-lookup"><span data-stu-id="e90f6-215">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it tooSignUpOrSignInWithAAD.xml).</span></span>
1. <span data-ttu-id="e90f6-216">Açık hello yeni dosya ve güncelleştirme hello `PolicyId` için öznitelik `<TrustFrameworkPolicy>` benzersiz bir değerle (örneğin, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="e90f6-216">Open hello new file and update hello `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <br> <span data-ttu-id="e90f6-217">Bu ilkenizin hello ad olacaktır (örneğin, B2C\_1A\_SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="e90f6-217">This will be hello name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span>
1. <span data-ttu-id="e90f6-218">Merhaba değiştirme `ReferenceId` özniteliğini `<DefaultUserJourney>` hello (SignUpOrSignUsingContoso) oluşturulan yeni kullanıcı gezisine toomatch hello kimliği.</span><span class="sxs-lookup"><span data-stu-id="e90f6-218">Modify hello `ReferenceId` attribute in `<DefaultUserJourney>` toomatch hello ID of hello new user journey that you created (SignUpOrSignUsingContoso).</span></span>
1. <span data-ttu-id="e90f6-219">Yaptığınız değişiklikleri kaydedin ve hello dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e90f6-219">Save your changes, and upload hello file.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e90f6-220">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="e90f6-220">Troubleshooting</span></span>

<span data-ttu-id="e90f6-221">Test yalnızca kendi dikey penceresini açıp tıklatarak karşıya hello özel ilke **Şimdi Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="e90f6-221">Test hello custom policy that you just uploaded by opening its blade and clicking **Run now**.</span></span> <span data-ttu-id="e90f6-222">Okuma toodiagnose sorunları hakkında [sorun giderme](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="e90f6-222">toodiagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e90f6-223">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e90f6-223">Next steps</span></span>

<span data-ttu-id="e90f6-224">Çok görüş[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e90f6-224">Provide feedback too[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
