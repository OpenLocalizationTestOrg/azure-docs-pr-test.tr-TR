---
title: "Azure Active Directory B2C: Özel ilkelerini kullanma OAuth2 kimlik sağlayıcısı Google + Ekle"
description: "Örnek Google + OAuth2 protokolünü kullanarak kimlik sağlayıcısı kullanma"
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
ms.openlocfilehash: 4feff21979c9c3b3b12c7a1cae4db0121d1bd79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a><span data-ttu-id="20bca-103">Azure Active Directory B2C: Özel ilkelerini kullanma OAuth2 kimlik sağlayıcısı Google + Ekle</span><span class="sxs-lookup"><span data-stu-id="20bca-103">Azure Active Directory B2C: Add Google+ as an OAuth2 identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="20bca-104">Bu kılavuz size nasıl tooenable oturum açma için Google + hello kullanımını hesabıyla kullanıcılardan gösterir [özel ilkeler](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="20bca-104">This guide shows you how tooenable sign-in for users from Google+ account through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20bca-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="20bca-105">Prerequisites</span></span>

<span data-ttu-id="20bca-106">Tam hello adımları hello [özel ilkeleri ile çalışmaya başlama](active-directory-b2c-get-started-custom.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="20bca-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="20bca-107">Bu adımlar şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="20bca-107">These steps include:</span></span>

1.  <span data-ttu-id="20bca-108">Google + hesabı uygulaması oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="20bca-108">Creating a Google+ account application.</span></span>
2.  <span data-ttu-id="20bca-109">Merhaba Google + hesap uygulama anahtar tooAzure AD B2C ekleme</span><span class="sxs-lookup"><span data-stu-id="20bca-109">Adding hello Google+ account application key tooAzure AD B2C</span></span>
3.  <span data-ttu-id="20bca-110">Talep sağlayıcı tooa ilkesi ekleme</span><span class="sxs-lookup"><span data-stu-id="20bca-110">Adding claims provider tooa policy</span></span>
4.  <span data-ttu-id="20bca-111">Merhaba Google + hesap talep sağlayıcısı tooa kullanıcı gezisine kaydetme</span><span class="sxs-lookup"><span data-stu-id="20bca-111">Registering hello Google+ account claims provider tooa user journey</span></span>
5.  <span data-ttu-id="20bca-112">Kiracı Hello İlkesi tooan Azure AD B2C karşıya yükleme ve test</span><span class="sxs-lookup"><span data-stu-id="20bca-112">Uploading hello policy tooan Azure AD B2C tenant and test it</span></span>

## <a name="create-a-google-account-application"></a><span data-ttu-id="20bca-113">Google + hesabı uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="20bca-113">Create a Google+ account application</span></span>
<span data-ttu-id="20bca-114">toouse Google + Azure Active Directory (Azure AD) B2C içinde kimlik sağlayıcısı, toocreate Google + uygulama gerekir ve hello doğru parametrelerle sağlayın.</span><span class="sxs-lookup"><span data-stu-id="20bca-114">toouse Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Google+ application and supply it with hello right parameters.</span></span> <span data-ttu-id="20bca-115">Bir Google + uygulama burada kaydedebilirsiniz: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span><span class="sxs-lookup"><span data-stu-id="20bca-115">You can register a Google+ application here: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span></span>

1.  <span data-ttu-id="20bca-116">Toohello Git [Google geliştiriciler konsol](https://console.developers.google.com/) ve Google + hesabı kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="20bca-116">Go toohello [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2.  <span data-ttu-id="20bca-117">Tıklatın **proje oluştur**, girin bir **proje adı**ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="20bca-117">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>

3.  <span data-ttu-id="20bca-118">Tıklatın hello üzerinde **projeleri menü**.</span><span class="sxs-lookup"><span data-stu-id="20bca-118">Click on hello **Projects menu**.</span></span>

    ![Google + hesabı - proje'yi seçin](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  <span data-ttu-id="20bca-120">Tıklatın hello üzerinde  **+**  düğmesi.</span><span class="sxs-lookup"><span data-stu-id="20bca-120">Click on hello **+** button.</span></span>

    ![Google + hesap - yeni proje oluşturma](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  <span data-ttu-id="20bca-122">Girin bir **proje adı**ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="20bca-122">Enter a **Project name**, and then click **Create**.</span></span>

    ![Google + hesabı - yeni proje](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  <span data-ttu-id="20bca-124">Hello proje hazır olana kadar bekleyin ve hello üzerinde tıklatın **projeleri menü**.</span><span class="sxs-lookup"><span data-stu-id="20bca-124">Wait until hello project is ready and click on hello **Projects menu**.</span></span>

    ![Google + hesabı - yeni proje hazır toouse olana kadar bekleyin](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  <span data-ttu-id="20bca-126">Proje adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="20bca-126">Click on your project name.</span></span>

    ![Google + hesabı - Select hello yeni proje](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  <span data-ttu-id="20bca-128">Tıklatın **API Yöneticisi** ve ardından **kimlik bilgileri** sol gezinti hello içinde.</span><span class="sxs-lookup"><span data-stu-id="20bca-128">Click **API Manager** and then click **Credentials** in hello left navigation.</span></span>
9.  <span data-ttu-id="20bca-129">Merhaba tıklatın **OAuth izni ekran** sekmesini hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="20bca-129">Click hello **OAuth consent screen** tab at hello top.</span></span>

    ![Google + hesabı - ayarlamak OAuth onay ekranı](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  <span data-ttu-id="20bca-131">Seçin veya geçerli bir belirtin **e-posta adresi**, sağlayan bir **ürün adı**, tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="20bca-131">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>

    ![Google + - uygulama kimlik bilgileri](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  <span data-ttu-id="20bca-133">Tıklatın **yeni kimlik bilgileri** ve ardından **OAuth istemci kimliği**.</span><span class="sxs-lookup"><span data-stu-id="20bca-133">Click **New credentials** and then choose **OAuth client ID**.</span></span>

    ![Google + - yeni uygulama kimlik bilgileri oluşturun](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  <span data-ttu-id="20bca-135">Altında **uygulama türü**seçin **Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="20bca-135">Under **Application type**, select **Web application**.</span></span>

    ![Google + - uygulama türünü seçme](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  <span data-ttu-id="20bca-137">Sağlamak bir **adı** , uygulamanız için girin `https://login.microsoftonline.com` hello içinde **yetkili JavaScript çıkış** alan, ve `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello içinde **yetkili URI'leryenidenyönlendirme**alan.</span><span class="sxs-lookup"><span data-stu-id="20bca-137">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in hello **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URIs** field.</span></span> <span data-ttu-id="20bca-138">Değiştir **{tenant}** , kiracının adlı (örneğin, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="20bca-138">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="20bca-139">Merhaba **{tenant}** duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="20bca-139">hello **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="20bca-140">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="20bca-140">Click **Create**.</span></span>

    ![Google + - yetkili JavaScript çıkış sağlayın ve URI'ler yeniden yönlendirme](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  <span data-ttu-id="20bca-142">Merhaba değerlerini kopyalamayı **istemci kimliği** ve **gizli**.</span><span class="sxs-lookup"><span data-stu-id="20bca-142">Copy hello values of **Client Id** and **Client secret**.</span></span> <span data-ttu-id="20bca-143">Her iki tooconfigure Google + kimlik sağlayıcısı olarak kiracınızda gerekir.</span><span class="sxs-lookup"><span data-stu-id="20bca-143">You need both tooconfigure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="20bca-144">**İstemci parolası** önemli güvenlik kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="20bca-144">**Client secret** is an important security credential.</span></span>

    ![Google + - istemci kimliği ve istemci gizli kopya hello değerleri](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-hello-google-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="20bca-146">Merhaba Google + hesap uygulama anahtar tooAzure AD B2C ekleme</span><span class="sxs-lookup"><span data-stu-id="20bca-146">Add hello Google+ account application key tooAzure AD B2C</span></span>
<span data-ttu-id="20bca-147">Google + hesaplarıyla Federasyon istemci parolasını Google + hesap tootrust için Azure AD B2C hello uygulama adına gerektirir.</span><span class="sxs-lookup"><span data-stu-id="20bca-147">Federation with Google+ accounts requires a client secret for Google+ account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="20bca-148">Azure AD B2C kiracısı içinde Google + uygulama gizli toostore gerekir:</span><span class="sxs-lookup"><span data-stu-id="20bca-148">You need toostore your Google+ application secret in Azure AD B2C tenant:</span></span>  

1.  <span data-ttu-id="20bca-149">Tooyour Azure AD B2C Kiracı gidip seçin **B2C ayarlarını** > **kimlik deneyimi Framework**</span><span class="sxs-lookup"><span data-stu-id="20bca-149">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="20bca-150">Seçin **İlkesi anahtarları** tooview hello anahtarları kiracınızda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="20bca-150">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="20bca-151">Tıklatın **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="20bca-151">Click **+Add**.</span></span>
4.  <span data-ttu-id="20bca-152">İçin **seçenekleri**, kullanın **el ile**.</span><span class="sxs-lookup"><span data-stu-id="20bca-152">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="20bca-153">İçin **adı**, kullanmak `GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="20bca-153">For **Name**, use `GoogleSecret`.</span></span>  
    <span data-ttu-id="20bca-154">Merhaba önek `B2C_1A_` otomatik olarak eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="20bca-154">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="20bca-155">Merhaba, **gizli** kutusuna, https://apps.dev.microsoft.com Microsoft uygulama gizli anahtarı girin</span><span class="sxs-lookup"><span data-stu-id="20bca-155">In hello **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="20bca-156">İçin **anahtar kullanımı**, kullanın **imza**.</span><span class="sxs-lookup"><span data-stu-id="20bca-156">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="20bca-157">**Oluştur**'a tıklayın</span><span class="sxs-lookup"><span data-stu-id="20bca-157">Click **Create**</span></span>
9.  <span data-ttu-id="20bca-158">Başlangıç anahtarı oluşturduğunuz onaylayın `B2C_1A_GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="20bca-158">Confirm that you've created hello key `B2C_1A_GoogleSecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="20bca-159">Bir talep sağlayıcı uzantısı ilkenizde ekleme</span><span class="sxs-lookup"><span data-stu-id="20bca-159">Add a claims provider in your extension policy</span></span>

<span data-ttu-id="20bca-160">Kullanıcıların toosign Google + hesabı kullanarak isterseniz, bir talep sağlayıcısı olarak toodefine Google + hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="20bca-160">If you want users toosign in by using Google+ account, you need toodefine Google+ account as a claims provider.</span></span> <span data-ttu-id="20bca-161">Diğer bir deyişle, Azure AD B2C ile iletişim kuran bir uç nokta toospecify gerekir.</span><span class="sxs-lookup"><span data-stu-id="20bca-161">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="20bca-162">Merhaba endpoint belirli bir kullanıcı doğrulaması Azure AD B2C tooverify tarafından kullanılan talepler kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="20bca-162">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="20bca-163">Google + hesabı ekleyerek bir talep sağlayıcısı olarak tanımlamak `<ClaimsProvider>` İlkesi uzantısının düğümünde:</span><span class="sxs-lookup"><span data-stu-id="20bca-163">Define Google+ Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="20bca-164">Hello İlkesi uzantısının (TrustFrameworkExtensions.xml) çalışma dizininizi açın.</span><span class="sxs-lookup"><span data-stu-id="20bca-164">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="20bca-165">Bir XML Düzenleyici, gerekirse [Visual Studio Code deneyin](https://code.visualstudio.com/download), basit bir platformlar arası Düzenleyici.</span><span class="sxs-lookup"><span data-stu-id="20bca-165">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="20bca-166">Hello bulur `<ClaimsProviders>` bölümü</span><span class="sxs-lookup"><span data-stu-id="20bca-166">Find hello `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="20bca-167">Aşağıdaki XML parçacığını hello altında hello eklemek `ClaimsProviders` öğesi ve Değiştir `client_id` hello dosyayı kaydetmeden önce Google + hesabı uygulama istemci kimliği değeri.</span><span class="sxs-lookup"><span data-stu-id="20bca-167">Add hello following XML snippet under hello `ClaimsProviders` element and replace `client_id` value with your Google+ account application client ID before saving hello file.</span></span>  

```xml
<ClaimsProvider>
    <Domain>google.com</Domain>
    <DisplayName>Google</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Google-OAUTH">
        <DisplayName>Google</DisplayName>
        <Protocol Name="OAuth2" />
        <Metadata>
        <Item Key="ProviderName">google</Item>
        <Item Key="authorization_endpoint">https://accounts.google.com/o/oauth2/auth</Item>
        <Item Key="AccessTokenEndpoint">https://accounts.google.com/o/oauth2/token</Item>
        <Item Key="ClaimsEndpoint">https://www.googleapis.com/oauth2/v1/userinfo</Item>
        <Item Key="scope">email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Google+ application ID</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_GoogleSecret" />
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="google.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
        <ErrorHandlers>
        <ErrorHandler>
            <ErrorResponseFormat>json</ErrorResponseFormat>
            <ResponseMatch>$[?(@@.error == 'invalid_grant')]</ResponseMatch>
            <Action>Reauthenticate</Action>
            <!--In case of authorization code used error, we don't want hello user tooselect his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-google-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="20bca-168">Yukarı Hello Google + hesap talep sağlayıcısı tooSign kaydetmek veya kullanıcı gezisine oturum</span><span class="sxs-lookup"><span data-stu-id="20bca-168">Register hello Google+ account claims provider tooSign up or Sign in user journey</span></span>

<span data-ttu-id="20bca-169">Merhaba kimlik sağlayıcısı ayarlandığına.</span><span class="sxs-lookup"><span data-stu-id="20bca-169">hello identity provider has been set up.</span></span>  <span data-ttu-id="20bca-170">Ancak, hello oturumu-up/oturum açma ekranları hiçbirinde kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="20bca-170">However, it is not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="20bca-171">Merhaba Google + hesabı kimlik sağlayıcısı tooyour kullanıcı ekleme `SignUpOrSignIn` kullanıcı gezisine.</span><span class="sxs-lookup"><span data-stu-id="20bca-171">Add hello Google+ account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="20bca-172">toomake kullanılabilir, biz var olan bir şablonu kullanıcı gezisine bir kopyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="20bca-172">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="20bca-173">Daha sonra hello Google + hesabı kimlik sağlayıcısı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="20bca-173">Then we add hello Google+ account identity provider:</span></span>

>[!NOTE]
>
><span data-ttu-id="20bca-174">Merhaba kopyaladıysanız `<UserJourneys>` öğesi ilke toohello uzantısı dosyanız (TrustFrameworkExtensions.xml) temel dosyasından toothis bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20bca-174">If you copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml), you can skip toothis section.</span></span>

1.  <span data-ttu-id="20bca-175">Merhaba temel dosyanın ilkenizin (örneğin, TrustFrameworkBase.xml) açın.</span><span class="sxs-lookup"><span data-stu-id="20bca-175">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="20bca-176">Hello bulur `<UserJourneys>` öğesi ve kopyalama hello tüm içeriği `<UserJourneys>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="20bca-176">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="20bca-177">Merhaba uzantısının (örneğin, TrustFrameworkExtensions.xml) açın ve hello bulur `<UserJourneys>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="20bca-177">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="20bca-178">Merhaba öğe yoksa, ekleyin.</span><span class="sxs-lookup"><span data-stu-id="20bca-178">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="20bca-179">Merhaba tüm içeriğini yapıştırın `<UserJournesy>` hello alt sitesi olarak kopyaladığınız düğümü `<UserJourneys>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="20bca-179">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="20bca-180">Görüntü hello düğmesi</span><span class="sxs-lookup"><span data-stu-id="20bca-180">Display hello button</span></span>
<span data-ttu-id="20bca-181">Merhaba `<ClaimsProviderSelections>` öğe, Talep sağlayıcı seçme seçenekleri hello listesi ve bunların sırası tanımlar.</span><span class="sxs-lookup"><span data-stu-id="20bca-181">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="20bca-182">`<ClaimsProviderSelection>`benzer tooan kimlik sağlayıcısı düğmesi oturumu-up/oturum açma sayfasında bir öğedir.</span><span class="sxs-lookup"><span data-stu-id="20bca-182">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="20bca-183">Eklerseniz bir `<ClaimsProviderSelection>` öğesi Google + hesap için yeni bir düğme görüntülenir hello sayfasında bir kullanıcı adlandırıldığını olduğunda.</span><span class="sxs-lookup"><span data-stu-id="20bca-183">If you add a `<ClaimsProviderSelection>` element for Google+ account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="20bca-184">tooadd bu öğe:</span><span class="sxs-lookup"><span data-stu-id="20bca-184">tooadd this element:</span></span>

1.  <span data-ttu-id="20bca-185">Hello bulur `<UserJourney>` içeren düğüm `Id="SignUpOrSignIn"` kopyaladığınız hello kullanıcı gezisine içinde.</span><span class="sxs-lookup"><span data-stu-id="20bca-185">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="20bca-186">Merhaba bulun `<OrchestrationStep>` içeren düğümü`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="20bca-186">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="20bca-187">Aşağıdaki XML parçacığını altında ekleyin `<ClaimsProviderSelections>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="20bca-187">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="20bca-188">Bağlantı hello düğmesi tooan eylemi</span><span class="sxs-lookup"><span data-stu-id="20bca-188">Link hello button tooan action</span></span>
<span data-ttu-id="20bca-189">Yerinde bir düğmeye sahip olduğunuza göre toolink gerekir, tooan eylem.</span><span class="sxs-lookup"><span data-stu-id="20bca-189">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="20bca-190">Merhaba, bu durumda, Google + hesap tooreceive ile Azure AD B2C toocommunicate için bir belirteç eylemdir.</span><span class="sxs-lookup"><span data-stu-id="20bca-190">hello action, in this case, is for Azure AD B2C toocommunicate with Google+ account tooreceive a token.</span></span>

1.  <span data-ttu-id="20bca-191">Hello bulur `<OrchestrationStep>` içeren `Order="2"` hello içinde `<UserJourney>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="20bca-191">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="20bca-192">Aşağıdaki XML parçacığını altında ekleyin `<ClaimsExchanges>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="20bca-192">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * <span data-ttu-id="20bca-193">Hello sağlamak `Id` hello aynı değeri aynı olan `TargetClaimsExchangeId` bölüm önceki hello içinde</span><span class="sxs-lookup"><span data-stu-id="20bca-193">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section</span></span>
> * <span data-ttu-id="20bca-194">Olun `TechnicalProfileReferenceId` önceki (Google-OAUTH) oluşturulmuş toohello teknik profili kümesi kimliği.</span><span class="sxs-lookup"><span data-stu-id="20bca-194">Ensure `TechnicalProfileReferenceId` ID is set toohello technical profile you created earlier (Google-OAUTH).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="20bca-195">Hello İlkesi tooyour Kiracı karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="20bca-195">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="20bca-196">Merhaba, [Azure portal](https://portal.azure.com), geçiş hello [bağlamı Azure AD B2C kiracınızın](active-directory-b2c-navigate-to-b2c-context.md)ve açık hello **Azure AD B2C** dikey.</span><span class="sxs-lookup"><span data-stu-id="20bca-196">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="20bca-197">Seçin **kimlik deneyimi Framework**.</span><span class="sxs-lookup"><span data-stu-id="20bca-197">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="20bca-198">Açık hello **tüm ilkeler** dikey.</span><span class="sxs-lookup"><span data-stu-id="20bca-198">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="20bca-199">Seçin **karşıya İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="20bca-199">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="20bca-200">Denetleme **varsa hello ilkesi üzerine** kutusu.</span><span class="sxs-lookup"><span data-stu-id="20bca-200">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="20bca-201">**Karşıya yükleme** TrustFrameworkExtensions.xml ve hello doğrulama başlayabildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="20bca-201">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="20bca-202">Şimdi Çalıştır kullanarak Hello özel ilkesini test</span><span class="sxs-lookup"><span data-stu-id="20bca-202">Test hello custom policy by using Run Now</span></span>
1.  <span data-ttu-id="20bca-203">Açık **Azure AD B2C ayarlarını** ve çok Git**kimlik deneyimi Framework**.</span><span class="sxs-lookup"><span data-stu-id="20bca-203">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>

    >[!NOTE]
    >
    >    <span data-ttu-id="20bca-204">**Şimdi Çalıştır** en az bir uygulama toobe preregistered hello Kiracı'gerektirir.</span><span class="sxs-lookup"><span data-stu-id="20bca-204">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> 
    >    <span data-ttu-id="20bca-205">tooregister uygulamaları nasıl görürüm toolearn hello Azure AD B2C [başlama](active-directory-b2c-get-started.md) makale veya hello [uygulama kaydı](active-directory-b2c-app-registration.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="20bca-205">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>


2.  <span data-ttu-id="20bca-206">Açık **B2C_1A_signup_signin**, karşıya yüklediğiniz bağlı olan taraf (RP) özel ilke hello.</span><span class="sxs-lookup"><span data-stu-id="20bca-206">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="20bca-207">Seçin **Şimdi Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="20bca-207">Select **Run now**.</span></span>
3.  <span data-ttu-id="20bca-208">Google + hesabı kullanarak mümkün toosign olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="20bca-208">You should be able toosign in using Google+ account.</span></span>

## <a name="optional-register-hello-google-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="20bca-209">[İsteğe bağlı] Merhaba Google + hesap talep sağlayıcısı tooProfile düzenleme kullanıcı gezisine kaydetme</span><span class="sxs-lookup"><span data-stu-id="20bca-209">[Optional] Register hello Google+ account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="20bca-210">Tooadd hello Google + hesabı kimlik sağlayıcısı tooyour kullanıcı da isteyebilir `ProfileEdit` kullanıcı gezisine.</span><span class="sxs-lookup"><span data-stu-id="20bca-210">You may want tooadd hello Google+ account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="20bca-211">toomake, biz hello yineleyin kullanılabilir en son iki adımı:</span><span class="sxs-lookup"><span data-stu-id="20bca-211">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="20bca-212">Görüntü hello düğmesi</span><span class="sxs-lookup"><span data-stu-id="20bca-212">Display hello button</span></span>
1.  <span data-ttu-id="20bca-213">Merhaba uzantısının ilkenizin (örneğin, TrustFrameworkExtensions.xml) açın.</span><span class="sxs-lookup"><span data-stu-id="20bca-213">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="20bca-214">Hello bulur `<UserJourney>` içeren düğüm `Id="ProfileEdit"` kopyaladığınız hello kullanıcı gezisine içinde.</span><span class="sxs-lookup"><span data-stu-id="20bca-214">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="20bca-215">Merhaba bulun `<OrchestrationStep>` içeren düğümü`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="20bca-215">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="20bca-216">Aşağıdaki XML parçacığını altında ekleyin `<ClaimsProviderSelections>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="20bca-216">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="20bca-217">Bağlantı hello düğmesi tooan eylemi</span><span class="sxs-lookup"><span data-stu-id="20bca-217">Link hello button tooan action</span></span>
1.  <span data-ttu-id="20bca-218">Hello bulur `<OrchestrationStep>` içeren `Order="2"` hello içinde `<UserJourney>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="20bca-218">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="20bca-219">Aşağıdaki XML parçacığını altında ekleyin `<ClaimsExchanges>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="20bca-219">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="20bca-220">Şimdi Çalıştır kullanarak Hello özel profil Düzenleme İlkesi test</span><span class="sxs-lookup"><span data-stu-id="20bca-220">Test hello custom Profile-Edit policy by using Run Now</span></span>

1.  <span data-ttu-id="20bca-221">Açık **Azure AD B2C ayarlarını** ve çok Git**kimlik deneyimi Framework**.</span><span class="sxs-lookup"><span data-stu-id="20bca-221">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="20bca-222">Açık **B2C_1A_ProfileEdit**, karşıya yüklediğiniz bağlı olan taraf (RP) özel ilke hello.</span><span class="sxs-lookup"><span data-stu-id="20bca-222">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="20bca-223">Seçin **Şimdi Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="20bca-223">Select **Run now**.</span></span>
3.  <span data-ttu-id="20bca-224">Google + hesabı kullanarak mümkün toosign olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="20bca-224">You should be able toosign in using Google+ account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="20bca-225">Merhaba tam ilke dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="20bca-225">Download hello complete policy files</span></span>
<span data-ttu-id="20bca-226">İsteğe bağlı: Özel ilkeleri ile çalışmaya başlama size yol Bu örnek dosyalarını kullanmak yerine hello tamamladıktan sonra kendi özel ilke dosyaları kullanarak senaryonuz yapı öneririz.</span><span class="sxs-lookup"><span data-stu-id="20bca-226">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="20bca-227">Başvuru için örnek ilke dosyaları</span><span class="sxs-lookup"><span data-stu-id="20bca-227">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
