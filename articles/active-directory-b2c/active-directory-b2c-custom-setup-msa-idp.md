---
title: "Azure Active Directory B2C: Microsoft hesabı (MSA) özel ilkelerini kullanarak bir kimlik sağlayıcısı ekleyin."
description: "Openıd Connect (OIDC) protokolünü kullanarak kimlik sağlayıcısı Microsoft kullanılarak örnek"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 577ac612f69015e6790f2fa9f2cfb42c2b524b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a><span data-ttu-id="711f0-103">Azure Active Directory B2C: Microsoft hesabı (MSA) özel ilkelerini kullanarak bir kimlik sağlayıcısı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="711f0-103">Azure Active Directory B2C: Add Microsoft Account (MSA) as an identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="711f0-104">Bu makale size nasıl tooenable oturum açmak için Microsoft hesabı (MSA) kullanıcılardan hello kullanımını gösterir [özel ilkeler](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="711f0-104">This article shows you how tooenable sign-in for users from Microsoft account (MSA) through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="711f0-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="711f0-105">Prerequisites</span></span>
<span data-ttu-id="711f0-106">Tam hello adımları hello [özel ilkeleri ile çalışmaya başlama](active-directory-b2c-get-started-custom.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="711f0-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="711f0-107">Bu adımlar şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="711f0-107">These steps include:</span></span>

1.  <span data-ttu-id="711f0-108">Bir Microsoft hesabı uygulaması oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="711f0-108">Creating a Microsoft account application.</span></span>
2.  <span data-ttu-id="711f0-109">Merhaba Microsoft hesabı uygulama anahtar tooAzure AD B2C ekleme</span><span class="sxs-lookup"><span data-stu-id="711f0-109">Adding hello Microsoft account application key tooAzure AD B2C</span></span>
3.  <span data-ttu-id="711f0-110">Talep sağlayıcı tooa ilkesi ekleme</span><span class="sxs-lookup"><span data-stu-id="711f0-110">Adding claims provider tooa policy</span></span>
4.  <span data-ttu-id="711f0-111">Merhaba Microsoft Account talep sağlayıcısı tooa kullanıcı gezisine kaydetme</span><span class="sxs-lookup"><span data-stu-id="711f0-111">Registering hello Microsoft Account claims provider tooa user journey</span></span>
5.  <span data-ttu-id="711f0-112">Kiracı Hello İlkesi tooan Azure AD B2C karşıya yükleme ve test</span><span class="sxs-lookup"><span data-stu-id="711f0-112">Uploading hello policy tooan Azure AD B2C tenant and test it</span></span>

## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="711f0-113">Bir Microsoft hesabı uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="711f0-113">Create a Microsoft account application</span></span>
<span data-ttu-id="711f0-114">toouse Microsoft hesabı kimlik sağlayıcısı Azure Active Directory (Azure AD) B2C içinde hello doğru parametrelerle tedarik ve toocreate bir Microsoft hesabı uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="711f0-114">toouse Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Microsoft account application and supply it with hello right parameters.</span></span> <span data-ttu-id="711f0-115">Bir Microsoft hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="711f0-115">You need a Microsoft account.</span></span> <span data-ttu-id="711f0-116">Yoksa, ziyaret [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="711f0-116">If you don’t have one, visit [https://www.live.com/](https://www.live.com/).</span></span>

1.  <span data-ttu-id="711f0-117">Toohello Git [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ve Microsoft hesabı kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="711f0-117">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2.  <span data-ttu-id="711f0-118">Tıklatın **bir uygulama ekleyin**.</span><span class="sxs-lookup"><span data-stu-id="711f0-118">Click **Add an app**.</span></span>

    ![Microsoft hesabı - bir uygulama ekleyin](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  <span data-ttu-id="711f0-120">Sağlamak bir **adı** , uygulamanız için **kişi e-posta**, seçeneğinin işaretini kaldırın **başlamanıza yardım bize** tıklatıp **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="711f0-120">Provide a **Name** for your application, **Contact email**, uncheck **Let us help you get started** and click **Create**.</span></span>

    ![Microsoft hesabı - uygulamanızı kaydetme](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  <span data-ttu-id="711f0-122">Merhaba değerini kopyalayın **uygulama kimliği**. Tooconfigure Microsoft hesabı kimlik sağlayıcısı olarak kiracınızda ihtiyacınız.</span><span class="sxs-lookup"><span data-stu-id="711f0-122">Copy hello value of **Application Id**. You need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span>

    ![Microsoft hesabı - kopyalama hello değeri uygulama kimliği](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  <span data-ttu-id="711f0-124">Tıklayın **Ekle platformu**</span><span class="sxs-lookup"><span data-stu-id="711f0-124">Click on **Add platform**</span></span>

    ![Microsoft hesabı - platform ekleme](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  <span data-ttu-id="711f0-126">Merhaba platform listeden seçin **Web**.</span><span class="sxs-lookup"><span data-stu-id="711f0-126">From hello platform list, choose **Web**.</span></span>

    ![Microsoft hesabı - hello platform listeden Web seçin](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  <span data-ttu-id="711f0-128">Girin `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello içinde **yeniden yönlendirme URI'ler** alan.</span><span class="sxs-lookup"><span data-stu-id="711f0-128">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** field.</span></span> <span data-ttu-id="711f0-129">Değiştir **{tenant}** , kiracının adlı (örneğin, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="711f0-129">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>

    ![Microsoft hesabı - kümesi yeniden yönlendirme URL'leri](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  <span data-ttu-id="711f0-131">Tıklayın **yeni bir parola oluşturmak** hello altında **uygulama parolaları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="711f0-131">Click on **Generate New Password** under hello **Application Secrets** section.</span></span> <span data-ttu-id="711f0-132">Ekranda görüntülenen hello yeni parolayı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="711f0-132">Copy hello new password displayed on screen.</span></span> <span data-ttu-id="711f0-133">Tooconfigure Microsoft hesabı kimlik sağlayıcısı olarak kiracınızda ihtiyacınız.</span><span class="sxs-lookup"><span data-stu-id="711f0-133">You need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="711f0-134">Bu parolayı bir önemli güvenlik kimlik bilgisidir.</span><span class="sxs-lookup"><span data-stu-id="711f0-134">This password is an important security credential.</span></span>

    ![Microsoft hesabı - yeni bir parola oluştur](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Microsoft hesabı - kopyalama hello yeni parola](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  <span data-ttu-id="711f0-137">Bildiren hello kutuyu **Live SDK'sı desteği** hello altında **Gelişmiş Seçenekler** bölümü.</span><span class="sxs-lookup"><span data-stu-id="711f0-137">Check hello box that says **Live SDK support** under hello **Advanced Options** section.</span></span> <span data-ttu-id="711f0-138">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="711f0-138">Click **Save**.</span></span>

    ![Microsoft hesabı - Live SDK'sı desteği](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-hello-microsoft-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="711f0-140">Merhaba Microsoft hesabı uygulama anahtar tooAzure AD B2C ekleme</span><span class="sxs-lookup"><span data-stu-id="711f0-140">Add hello Microsoft account application key tooAzure AD B2C</span></span>
<span data-ttu-id="711f0-141">Microsoft hesapları ile Federasyon istemci parolasını hello uygulama adına Microsoft hesabı tootrust Azure AD B2C gerektirir.</span><span class="sxs-lookup"><span data-stu-id="711f0-141">Federation with Microsoft accounts requires a client secret for Microsoft account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="711f0-142">Azure AD B2C kiracısı içinde Microsoft hesabı uygulama secert toostore gerekir:</span><span class="sxs-lookup"><span data-stu-id="711f0-142">You need toostore your Microsoft account application secert in Azure AD B2C tenant:</span></span>   

1.  <span data-ttu-id="711f0-143">Tooyour Azure AD B2C Kiracı gidip seçin **B2C ayarlarını** > **kimlik deneyimi Framework**</span><span class="sxs-lookup"><span data-stu-id="711f0-143">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="711f0-144">Seçin **İlkesi anahtarları** tooview hello anahtarları kiracınızda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="711f0-144">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="711f0-145">Tıklatın **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="711f0-145">Click **+Add**.</span></span>
4.  <span data-ttu-id="711f0-146">İçin **seçenekleri**, kullanın **el ile**.</span><span class="sxs-lookup"><span data-stu-id="711f0-146">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="711f0-147">İçin **adı**, kullanmak `MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="711f0-147">For **Name**, use `MSASecret`.</span></span>  
    <span data-ttu-id="711f0-148">Merhaba önek `B2C_1A_` otomatik olarak eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="711f0-148">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="711f0-149">Merhaba, **gizli** kutusuna, https://apps.dev.microsoft.com Microsoft uygulama gizli anahtarı girin</span><span class="sxs-lookup"><span data-stu-id="711f0-149">In hello **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="711f0-150">İçin **anahtar kullanımı**, kullanın **imza**.</span><span class="sxs-lookup"><span data-stu-id="711f0-150">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="711f0-151">**Oluştur**'a tıklayın</span><span class="sxs-lookup"><span data-stu-id="711f0-151">Click **Create**</span></span>
9.  <span data-ttu-id="711f0-152">Başlangıç anahtarı oluşturduğunuz onaylayın `B2C_1A_MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="711f0-152">Confirm that you've created hello key `B2C_1A_MSASecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="711f0-153">Bir talep sağlayıcı uzantısı ilkenizde ekleme</span><span class="sxs-lookup"><span data-stu-id="711f0-153">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="711f0-154">Kullanıcıların toosign Microsoft Account kullanarak isterseniz, bir talep sağlayıcısı olarak toodefine Microsoft Account gerekir.</span><span class="sxs-lookup"><span data-stu-id="711f0-154">If you want users toosign in by using Microsoft Account, you need toodefine Microsoft Account as a claims provider.</span></span> <span data-ttu-id="711f0-155">Diğer bir deyişle, Azure AD B2C ile iletişim kuran bir uç nokta toospecify gerekir.</span><span class="sxs-lookup"><span data-stu-id="711f0-155">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="711f0-156">Merhaba endpoint belirli bir kullanıcı doğrulaması Azure AD B2C tooverify tarafından kullanılan talepler kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="711f0-156">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="711f0-157">Microsoft Account ekleyerek bir talep sağlayıcısı olarak tanımlamak `<ClaimsProvider>` İlkesi uzantısının düğümünde:</span><span class="sxs-lookup"><span data-stu-id="711f0-157">Define Microsoft Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="711f0-158">Hello İlkesi uzantısının (TrustFrameworkExtensions.xml) çalışma dizininizi açın.</span><span class="sxs-lookup"><span data-stu-id="711f0-158">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="711f0-159">Bir XML Düzenleyici, gerekirse [Visual Studio Code deneyin](https://code.visualstudio.com/download), basit bir platformlar arası Düzenleyici.</span><span class="sxs-lookup"><span data-stu-id="711f0-159">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="711f0-160">Hello bulur `<ClaimsProviders>` bölümü</span><span class="sxs-lookup"><span data-stu-id="711f0-160">Find hello `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="711f0-161">Aşağıdaki XML parçacığını hello altında ekleyin `ClaimsProviders` öğe:</span><span class="sxs-lookup"><span data-stu-id="711f0-161">Add following XML snippet under hello `ClaimsProviders` element:</span></span>

    ```xml
<ClaimsProvider>
    <Domain>live.com</Domain>
    <DisplayName>Microsoft Account</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="MSA-OIDC">
        <DisplayName>Microsoft Account</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <Metadata>
        <Item Key="ProviderName">https://login.live.com</Item>
        <Item Key="METADATA">https://login.live.com/.well-known/openid-configuration</Item>
        <Item Key="response_types">code</Item>
        <Item Key="response_mode">form_post</Item>
        <Item Key="scope">openid profile email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Microsoft application client id</Item>
        </Metadata>
    <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_MSASecret" />
    </CryptographicKeys>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="email" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

4.  <span data-ttu-id="711f0-162">Değiştir `client_id` Microsoft Account uygulama istemci kimliği değeri</span><span class="sxs-lookup"><span data-stu-id="711f0-162">Replace `client_id` value with your Microsoft Account application client Id</span></span>

5.  <span data-ttu-id="711f0-163">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="711f0-163">Save hello file.</span></span>

## <a name="register-hello-microsoft-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="711f0-164">Merhaba Microsoft Account talep sağlayıcısı tooSign yukarı veya oturum açma kullanıcı gezisine kaydetme</span><span class="sxs-lookup"><span data-stu-id="711f0-164">Register hello Microsoft Account claims provider tooSign up or Sign-in user journey</span></span>

<span data-ttu-id="711f0-165">Bu noktada, hello kimlik sağlayıcısı ayarlandı, ancak hello oturumu-up/oturum açma ekranları hiçbirinde kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="711f0-165">At this point, hello identity provider has been set up, but it’s not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="711f0-166">Tooadd hello Microsoft Account kimlik sağlayıcısı tooyour user gereksinim artık `SignUpOrSignIn` kullanıcı gezisine.</span><span class="sxs-lookup"><span data-stu-id="711f0-166">Now you need tooadd hello Microsoft Account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="711f0-167">toomake kullanılabilir, biz var olan bir şablonu kullanıcı gezisine bir kopyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="711f0-167">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="711f0-168">Daha sonra hello Microsoft Account kimlik sağlayıcısı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="711f0-168">Then we add hello Microsoft Account identity provider:</span></span>

> [!NOTE]
>
><span data-ttu-id="711f0-169">Daha önce hello kopyaladıysanız `<UserJourneys>` İlkesi toohello uzantısının temel dosyanın öğesinden `TrustFrameworkExtensions.xml`, toothis bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="711f0-169">If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file `TrustFrameworkExtensions.xml`, you can skip toothis section.</span></span>

1.  <span data-ttu-id="711f0-170">Merhaba temel dosyanın ilkenizin (örneğin, TrustFrameworkBase.xml) açın.</span><span class="sxs-lookup"><span data-stu-id="711f0-170">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="711f0-171">Hello bulur `<UserJourneys>` öğesi ve kopyalama hello tüm içeriği `<UserJourneys>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="711f0-171">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="711f0-172">Merhaba uzantısının (örneğin, TrustFrameworkExtensions.xml) açın ve hello bulur `<UserJourneys>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="711f0-172">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="711f0-173">Merhaba öğe yoksa, ekleyin.</span><span class="sxs-lookup"><span data-stu-id="711f0-173">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="711f0-174">Merhaba tüm içeriğini yapıştırın `<UserJournesy>` hello alt sitesi olarak kopyaladığınız düğümü `<UserJourneys>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="711f0-174">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="711f0-175">Görüntü hello düğmesi</span><span class="sxs-lookup"><span data-stu-id="711f0-175">Display hello button</span></span>
<span data-ttu-id="711f0-176">Merhaba `<ClaimsProviderSelections>` öğe, Talep sağlayıcı seçme seçenekleri hello listesi ve bunların sırası tanımlar.</span><span class="sxs-lookup"><span data-stu-id="711f0-176">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="711f0-177">`<ClaimsProviderSelection>`benzer tooan kimlik sağlayıcısı düğmesi oturumu-up/oturum açma sayfasında bir öğedir.</span><span class="sxs-lookup"><span data-stu-id="711f0-177">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="711f0-178">Eklerseniz bir `<ClaimsProviderSelection>` öğesi Microsoft hesabı için yeni bir düğme görüntülenir hello sayfasında bir kullanıcı adlandırıldığını olduğunda.</span><span class="sxs-lookup"><span data-stu-id="711f0-178">If you add a `<ClaimsProviderSelection>` element for Microsoft account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="711f0-179">tooadd bu öğe:</span><span class="sxs-lookup"><span data-stu-id="711f0-179">tooadd this element:</span></span>

1.  <span data-ttu-id="711f0-180">Hello bulur `<UserJourney>` içeren düğüm `Id="SignUpOrSignIn"` kopyaladığınız hello kullanıcı gezisine içinde.</span><span class="sxs-lookup"><span data-stu-id="711f0-180">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="711f0-181">Merhaba bulun `<OrchestrationStep>` içeren düğümü`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="711f0-181">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="711f0-182">Aşağıdaki XML parçacığını altında ekleyin `<ClaimsProviderSelections>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="711f0-182">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="711f0-183">Bağlantı hello düğmesi tooan eylemi</span><span class="sxs-lookup"><span data-stu-id="711f0-183">Link hello button tooan action</span></span>
<span data-ttu-id="711f0-184">Yerinde bir düğmeye sahip olduğunuza göre toolink gerekir, tooan eylem.</span><span class="sxs-lookup"><span data-stu-id="711f0-184">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="711f0-185">Merhaba, bu durumda, Microsoft Account tooreceive ile Azure AD B2C toocommunicate için bir belirteç eylemdir.</span><span class="sxs-lookup"><span data-stu-id="711f0-185">hello action, in this case, is for Azure AD B2C toocommunicate with Microsoft Account tooreceive a token.</span></span> <span data-ttu-id="711f0-186">Merhaba düğmesi tooan eylemi, Microsoft Account talep sağlayıcısı hello teknik profili bağlayarak Bağla:</span><span class="sxs-lookup"><span data-stu-id="711f0-186">Link hello button tooan action by linking hello technical profile for your Microsoft Account claims provider:</span></span>

1.  <span data-ttu-id="711f0-187">Hello bulur `<OrchestrationStep>` içeren `Order="2"` hello içinde `<UserJourney>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="711f0-187">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="711f0-188">Aşağıdaki XML parçacığını altında ekleyin `<ClaimsExchanges>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="711f0-188">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * <span data-ttu-id="711f0-189">Hello sağlamak `Id` hello aynı değeri aynı olan `TargetClaimsExchangeId` bölüm önceki hello içinde</span><span class="sxs-lookup"><span data-stu-id="711f0-189">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section</span></span>
>   * <span data-ttu-id="711f0-190">Olun `TechnicalProfileReferenceId` önceki (MSA-OIDC) oluşturulmuş toohello teknik profili kümesi kimliği.</span><span class="sxs-lookup"><span data-stu-id="711f0-190">Ensure `TechnicalProfileReferenceId` ID is set toohello technical profile you created earlier (MSA-OIDC).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="711f0-191">Hello İlkesi tooyour Kiracı karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="711f0-191">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="711f0-192">Merhaba, [Azure portal](https://portal.azure.com), geçiş hello [bağlamı Azure AD B2C kiracınızın](active-directory-b2c-navigate-to-b2c-context.md)ve açık hello **Azure AD B2C** dikey.</span><span class="sxs-lookup"><span data-stu-id="711f0-192">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="711f0-193">Seçin **kimlik deneyimi Framework**.</span><span class="sxs-lookup"><span data-stu-id="711f0-193">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="711f0-194">Açık hello **tüm ilkeler** dikey.</span><span class="sxs-lookup"><span data-stu-id="711f0-194">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="711f0-195">Seçin **karşıya İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="711f0-195">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="711f0-196">Denetleme **varsa hello ilkesi üzerine** kutusu.</span><span class="sxs-lookup"><span data-stu-id="711f0-196">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="711f0-197">**Karşıya yükleme** TrustFrameworkExtensions.xml ve hello doğrulama başlayabildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="711f0-197">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="711f0-198">Şimdi Çalıştır kullanarak Hello özel ilkesini test</span><span class="sxs-lookup"><span data-stu-id="711f0-198">Test hello custom policy by using Run Now</span></span>

1.  <span data-ttu-id="711f0-199">Açık **Azure AD B2C ayarlarını** ve çok Git**kimlik deneyimi Framework**.</span><span class="sxs-lookup"><span data-stu-id="711f0-199">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
> [!NOTE]
>
><span data-ttu-id="711f0-200">**Şimdi Çalıştır** en az bir uygulama toobe preregistered hello Kiracı'gerektirir.</span><span class="sxs-lookup"><span data-stu-id="711f0-200">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> <span data-ttu-id="711f0-201">tooregister uygulamaları nasıl görürüm toolearn hello Azure AD B2C [başlama](active-directory-b2c-get-started.md) makale veya hello [uygulama kaydı](active-directory-b2c-app-registration.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="711f0-201">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>
2.  <span data-ttu-id="711f0-202">Açık **B2C_1A_signup_signin**, karşıya yüklediğiniz bağlı olan taraf (RP) özel ilke hello.</span><span class="sxs-lookup"><span data-stu-id="711f0-202">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="711f0-203">Seçin **Şimdi Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="711f0-203">Select **Run now**.</span></span>
3.  <span data-ttu-id="711f0-204">Microsoft hesabı kullanarak mümkün toosign olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="711f0-204">You should be able toosign in using Microsoft account.</span></span>

## <a name="optional-register-hello-microsoft-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="711f0-205">[İsteğe bağlı] Merhaba Microsoft Account talep sağlayıcısı tooProfile düzenleme kullanıcı gezisine kaydetme</span><span class="sxs-lookup"><span data-stu-id="711f0-205">[Optional] Register hello Microsoft Account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="711f0-206">Tooadd hello Microsoft Account kimlik sağlayıcısı tooyour kullanıcı da isteyebilir `ProfileEdit` kullanıcı gezisine.</span><span class="sxs-lookup"><span data-stu-id="711f0-206">You may want tooadd hello Microsoft Account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="711f0-207">toomake, biz hello yineleyin kullanılabilir en son iki adımı:</span><span class="sxs-lookup"><span data-stu-id="711f0-207">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="711f0-208">Görüntü hello düğmesi</span><span class="sxs-lookup"><span data-stu-id="711f0-208">Display hello button</span></span>
1.  <span data-ttu-id="711f0-209">Merhaba uzantısının ilkenizin (örneğin, TrustFrameworkExtensions.xml) açın.</span><span class="sxs-lookup"><span data-stu-id="711f0-209">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="711f0-210">Hello bulur `<UserJourney>` içeren düğüm `Id="ProfileEdit"` kopyaladığınız hello kullanıcı gezisine içinde.</span><span class="sxs-lookup"><span data-stu-id="711f0-210">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="711f0-211">Merhaba bulun `<OrchestrationStep>` içeren düğümü`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="711f0-211">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="711f0-212">Aşağıdaki XML parçacığını altında ekleyin `<ClaimsProviderSelections>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="711f0-212">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="711f0-213">Bağlantı hello düğmesi tooan eylemi</span><span class="sxs-lookup"><span data-stu-id="711f0-213">Link hello button tooan action</span></span>
1.  <span data-ttu-id="711f0-214">Hello bulur `<OrchestrationStep>` içeren `Order="2"` hello içinde `<UserJourney>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="711f0-214">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="711f0-215">Aşağıdaki XML parçacığını altında ekleyin `<ClaimsExchanges>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="711f0-215">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="711f0-216">Şimdi Çalıştır kullanarak Hello özel profil Düzenleme İlkesi test</span><span class="sxs-lookup"><span data-stu-id="711f0-216">Test hello custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="711f0-217">Açık **Azure AD B2C ayarlarını** ve çok Git**kimlik deneyimi Framework**.</span><span class="sxs-lookup"><span data-stu-id="711f0-217">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="711f0-218">Açık **B2C_1A_ProfileEdit**, karşıya yüklediğiniz bağlı olan taraf (RP) özel ilke hello.</span><span class="sxs-lookup"><span data-stu-id="711f0-218">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="711f0-219">Seçin **Şimdi Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="711f0-219">Select **Run now**.</span></span>
3.  <span data-ttu-id="711f0-220">Microsoft hesabı kullanarak mümkün toosign olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="711f0-220">You should be able toosign in using Microsoft account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="711f0-221">Merhaba tam ilke dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="711f0-221">Download hello complete policy files</span></span>
<span data-ttu-id="711f0-222">İsteğe bağlı: Özel ilkeleri ile çalışmaya başlama size yol Bu örnek dosyalarını kullanmak yerine hello tamamladıktan sonra kendi özel ilke dosyaları kullanarak senaryonuz yapı öneririz.</span><span class="sxs-lookup"><span data-stu-id="711f0-222">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="711f0-223">Başvuru için örnek ilke dosyaları</span><span class="sxs-lookup"><span data-stu-id="711f0-223">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
