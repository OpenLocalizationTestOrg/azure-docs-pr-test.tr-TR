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
ms.openlocfilehash: e0aaf710d230f7667fff32b50ddb64104509d740
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a><span data-ttu-id="153c3-103">Azure Active Directory B2C: Özel ilkelerini kullanma OAuth2 kimlik sağlayıcısı Google + Ekle</span><span class="sxs-lookup"><span data-stu-id="153c3-103">Azure Active Directory B2C: Add Google+ as an OAuth2 identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="153c3-104">Bu kılavuz size nasıl oturum açma hesabından Google + kullanım yoluyla kullanıcılar için etkinleştirileceğini gösterir [özel ilkeler](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="153c3-104">This guide shows you how to enable sign-in for users from Google+ account through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="153c3-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="153c3-105">Prerequisites</span></span>

<span data-ttu-id="153c3-106">Bölümündeki adımları tamamlamanız [özel ilkeleri ile çalışmaya başlama](active-directory-b2c-get-started-custom.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="153c3-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="153c3-107">Bu adımlar şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="153c3-107">These steps include:</span></span>

1.  <span data-ttu-id="153c3-108">Google + hesabı uygulaması oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="153c3-108">Creating a Google+ account application.</span></span>
2.  <span data-ttu-id="153c3-109">Azure AD B2C'ye Google + hesap uygulama anahtarı ekleme</span><span class="sxs-lookup"><span data-stu-id="153c3-109">Adding the Google+ account application key to Azure AD B2C</span></span>
3.  <span data-ttu-id="153c3-110">Bir ilke ekleme talep sağlayıcısını</span><span class="sxs-lookup"><span data-stu-id="153c3-110">Adding claims provider to a policy</span></span>
4.  <span data-ttu-id="153c3-111">Google + hesap talep sağlayıcısı için bir kullanıcı gezisine kaydediliyor</span><span class="sxs-lookup"><span data-stu-id="153c3-111">Registering the Google+ account claims provider to a user journey</span></span>
5.  <span data-ttu-id="153c3-112">İlke için bir Azure AD B2C karşıya yükleme Kiracı ve test</span><span class="sxs-lookup"><span data-stu-id="153c3-112">Uploading the policy to an Azure AD B2C tenant and test it</span></span>

## <a name="create-a-google-account-application"></a><span data-ttu-id="153c3-113">Google + hesabı uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="153c3-113">Create a Google+ account application</span></span>
<span data-ttu-id="153c3-114">Google + Azure Active Directory (Azure AD) B2C bir kimlik sağlayıcısı olarak kullanmak için bir Google + uygulaması oluşturmak ve doğru parametrelerle sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="153c3-114">To use Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Google+ application and supply it with the right parameters.</span></span> <span data-ttu-id="153c3-115">Bir Google + uygulama burada kaydedebilirsiniz: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span><span class="sxs-lookup"><span data-stu-id="153c3-115">You can register a Google+ application here: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span></span>

1.  <span data-ttu-id="153c3-116">Git [Google geliştiriciler konsol](https://console.developers.google.com/) ve Google + hesabı kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="153c3-116">Go to the [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2.  <span data-ttu-id="153c3-117">Tıklatın **proje oluştur**, girin bir **proje adı**ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="153c3-117">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>

3.  <span data-ttu-id="153c3-118">Tıklayın **projeleri menü**.</span><span class="sxs-lookup"><span data-stu-id="153c3-118">Click on the **Projects menu**.</span></span>

    ![Google + hesabı - proje'yi seçin](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  <span data-ttu-id="153c3-120">Tıklayın  **+**  düğmesi.</span><span class="sxs-lookup"><span data-stu-id="153c3-120">Click on the **+** button.</span></span>

    ![Google + hesap - yeni proje oluşturma](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  <span data-ttu-id="153c3-122">Girin bir **proje adı**ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="153c3-122">Enter a **Project name**, and then click **Create**.</span></span>

    ![Google + hesabı - yeni proje](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  <span data-ttu-id="153c3-124">Proje hazır olana kadar bekleyin ve tıklayın **projeleri menü**.</span><span class="sxs-lookup"><span data-stu-id="153c3-124">Wait until the project is ready and click on the **Projects menu**.</span></span>

    ![Google + hesabı - yeni proje kullanıma hazır olana kadar bekleyin](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  <span data-ttu-id="153c3-126">Proje adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="153c3-126">Click on your project name.</span></span>

    ![Google + hesabı - yeni proje seçin](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  <span data-ttu-id="153c3-128">Tıklatın **API Yöneticisi** ve ardından **kimlik bilgileri** sol gezinti bölmesinde.</span><span class="sxs-lookup"><span data-stu-id="153c3-128">Click **API Manager** and then click **Credentials** in the left navigation.</span></span>
9.  <span data-ttu-id="153c3-129">Tıklatın **OAuth izni ekran** üst sekmesini.</span><span class="sxs-lookup"><span data-stu-id="153c3-129">Click the **OAuth consent screen** tab at the top.</span></span>

    ![Google + hesabı - ayarlamak OAuth onay ekranı](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  <span data-ttu-id="153c3-131">Seçin veya geçerli bir belirtin **e-posta adresi**, sağlayan bir **ürün adı**, tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="153c3-131">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>

    ![Google + - uygulama kimlik bilgileri](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  <span data-ttu-id="153c3-133">Tıklatın **yeni kimlik bilgileri** ve ardından **OAuth istemci kimliği**.</span><span class="sxs-lookup"><span data-stu-id="153c3-133">Click **New credentials** and then choose **OAuth client ID**.</span></span>

    ![Google + - yeni uygulama kimlik bilgileri oluşturun](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  <span data-ttu-id="153c3-135">Altında **uygulama türü**seçin **Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="153c3-135">Under **Application type**, select **Web application**.</span></span>

    ![Google + - uygulama türünü seçme](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  <span data-ttu-id="153c3-137">Sağlayan bir **adı** uygulamanız için girin `https://login.microsoftonline.com` içinde **yetkili JavaScript çıkış** alan, ve `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` içinde **yetkili URI'ler yeniden yönlendirme** alan.</span><span class="sxs-lookup"><span data-stu-id="153c3-137">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in the **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized redirect URIs** field.</span></span> <span data-ttu-id="153c3-138">Değiştir **{tenant}** , kiracının adlı (örneğin, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="153c3-138">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="153c3-139">**{Tenant}** duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="153c3-139">The **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="153c3-140">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="153c3-140">Click **Create**.</span></span>

    ![Google + - yetkili JavaScript çıkış sağlayın ve URI'ler yeniden yönlendirme](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  <span data-ttu-id="153c3-142">Değerleri kopyalamak **istemci kimliği** ve **gizli**.</span><span class="sxs-lookup"><span data-stu-id="153c3-142">Copy the values of **Client Id** and **Client secret**.</span></span> <span data-ttu-id="153c3-143">Google + kimlik sağlayıcısı kiracınızda yapılandırmak için her ikisini de gerekir.</span><span class="sxs-lookup"><span data-stu-id="153c3-143">You need both to configure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="153c3-144">**İstemci parolası** önemli güvenlik kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="153c3-144">**Client secret** is an important security credential.</span></span>

    ![Google + - istemci kimliği ve istemci gizli anahtarı değerlerini kopyalayın](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-the-google-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="153c3-146">Azure AD B2C'ye Google + hesap uygulama anahtarı Ekle</span><span class="sxs-lookup"><span data-stu-id="153c3-146">Add the Google+ account application key to Azure AD B2C</span></span>
<span data-ttu-id="153c3-147">Google + hesaplarıyla Federasyon Google + hesabına güven Azure AD B2C uygulama adına bir istemci parolası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="153c3-147">Federation with Google+ accounts requires a client secret for Google+ account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="153c3-148">Azure AD B2C kiracısı Google + uygulama gizli anahtarı depolamak gerekir:</span><span class="sxs-lookup"><span data-stu-id="153c3-148">You need to store your Google+ application secret in Azure AD B2C tenant:</span></span>  

1.  <span data-ttu-id="153c3-149">Azure AD B2C kiracınızın gidin ve seçin **B2C ayarlarını** > **kimlik deneyimi Framework**</span><span class="sxs-lookup"><span data-stu-id="153c3-149">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="153c3-150">Seçin **İlkesi anahtarları** kiracınızda kullanılabilir tuşlarını görmek için.</span><span class="sxs-lookup"><span data-stu-id="153c3-150">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3.  <span data-ttu-id="153c3-151">Tıklatın **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="153c3-151">Click **+Add**.</span></span>
4.  <span data-ttu-id="153c3-152">İçin **seçenekleri**, kullanın **el ile**.</span><span class="sxs-lookup"><span data-stu-id="153c3-152">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="153c3-153">İçin **adı**, kullanmak `GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="153c3-153">For **Name**, use `GoogleSecret`.</span></span>  
    <span data-ttu-id="153c3-154">Önek `B2C_1A_` otomatik olarak eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="153c3-154">The prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="153c3-155">İçinde **gizli** kutusuna, https://apps.dev.microsoft.com Microsoft uygulama gizli anahtarı girin</span><span class="sxs-lookup"><span data-stu-id="153c3-155">In the **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="153c3-156">İçin **anahtar kullanımı**, kullanın **imza**.</span><span class="sxs-lookup"><span data-stu-id="153c3-156">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="153c3-157">**Oluştur**'a tıklayın</span><span class="sxs-lookup"><span data-stu-id="153c3-157">Click **Create**</span></span>
9.  <span data-ttu-id="153c3-158">Anahtar oluşturduğunuz onaylayın `B2C_1A_GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="153c3-158">Confirm that you've created the key `B2C_1A_GoogleSecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="153c3-159">Bir talep sağlayıcı uzantısı ilkenizde ekleme</span><span class="sxs-lookup"><span data-stu-id="153c3-159">Add a claims provider in your extension policy</span></span>

<span data-ttu-id="153c3-160">Google + hesabını kullanarak oturum açmalarını istiyorsanız, bir talep sağlayıcısı olarak Google + hesap tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="153c3-160">If you want users to sign in by using Google+ account, you need to define Google+ account as a claims provider.</span></span> <span data-ttu-id="153c3-161">Diğer bir deyişle, Azure AD B2C ile iletişim kuran bir uç nokta belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="153c3-161">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="153c3-162">Uç nokta Azure AD B2C tarafından belirli bir kullanıcı kimliği doğrulanmış olduğunu doğrulamak için kullanılan talep kümesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="153c3-162">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="153c3-163">Google + hesabı ekleyerek bir talep sağlayıcısı olarak tanımlamak `<ClaimsProvider>` İlkesi uzantısının düğümünde:</span><span class="sxs-lookup"><span data-stu-id="153c3-163">Define Google+ Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="153c3-164">Uzantı ilke dosyası (TrustFrameworkExtensions.xml) çalışma dizininizi açın.</span><span class="sxs-lookup"><span data-stu-id="153c3-164">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="153c3-165">Bir XML Düzenleyici, gerekirse [Visual Studio Code deneyin](https://code.visualstudio.com/download), basit bir platformlar arası Düzenleyici.</span><span class="sxs-lookup"><span data-stu-id="153c3-165">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="153c3-166">Bul `<ClaimsProviders>` bölümü</span><span class="sxs-lookup"><span data-stu-id="153c3-166">Find the `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="153c3-167">Altında aşağıdaki XML parçacığını ekleyin `ClaimsProviders` öğesi ve Değiştir `client_id` dosyayı kaydetmeden önce Google + hesabı uygulama istemci kimliği ile değer.</span><span class="sxs-lookup"><span data-stu-id="153c3-167">Add the following XML snippet under the `ClaimsProviders` element and replace `client_id` value with your Google+ account application client ID before saving the file.</span></span>  

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
            <!--In case of authorization code used error, we don't want the user to select his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-the-google-account-claims-provider-to-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="153c3-168">Kaydolun veya kullanıcı gezisine imzalamak için Google + hesap talep sağlayıcısını Kaydet</span><span class="sxs-lookup"><span data-stu-id="153c3-168">Register the Google+ account claims provider to Sign up or Sign in user journey</span></span>

<span data-ttu-id="153c3-169">Kimlik sağlayıcısı ayarlandığına.</span><span class="sxs-lookup"><span data-stu-id="153c3-169">The identity provider has been set up.</span></span>  <span data-ttu-id="153c3-170">Ancak, oturumu-up/oturum açma ekranları hiçbirinde kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="153c3-170">However, it is not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="153c3-171">Google + hesabı kimlik sağlayıcısı, kullanıcı ekleme `SignUpOrSignIn` kullanıcı gezisine.</span><span class="sxs-lookup"><span data-stu-id="153c3-171">Add the Google+ account identity provider to your user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="153c3-172">Kullanılabilir hale getirmek için var olan bir şablonu kullanıcı gezisine tekrarı oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="153c3-172">To make it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="153c3-173">Daha sonra Google + hesabı kimlik sağlayıcısı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="153c3-173">Then we add the Google+ account identity provider:</span></span>

>[!NOTE]
>
><span data-ttu-id="153c3-174">Kopyaladığınız varsa `<UserJourneys>` ilkenizin temel dosyanın bir öğeden uzantısının (TrustFrameworkExtensions.xml) için bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="153c3-174">If you copied the `<UserJourneys>` element from base file of your policy to the extension file (TrustFrameworkExtensions.xml), you can skip to this section.</span></span>

1.  <span data-ttu-id="153c3-175">Temel dosya ilkenizin (örneğin, TrustFrameworkBase.xml) açın.</span><span class="sxs-lookup"><span data-stu-id="153c3-175">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="153c3-176">Bul `<UserJourneys>` öğesi ve tüm içeriğini kopyalayın `<UserJourneys>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="153c3-176">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="153c3-177">Uzantı dosyası (örneğin, TrustFrameworkExtensions.xml) açın ve Bul `<UserJourneys>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="153c3-177">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="153c3-178">Öğe yoksa, ekleyin.</span><span class="sxs-lookup"><span data-stu-id="153c3-178">If the element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="153c3-179">Tüm içeriğini yapıştırın `<UserJournesy>` bir alt öğesi olarak kopyaladığınız düğümü `<UserJourneys>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="153c3-179">Paste the entire content of `<UserJournesy>` node that you copied as a child of the `<UserJourneys>` element.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="153c3-180">Görüntü düğmesi</span><span class="sxs-lookup"><span data-stu-id="153c3-180">Display the button</span></span>
<span data-ttu-id="153c3-181">`<ClaimsProviderSelections>` Öğesi talep sağlayıcısı seçme seçenekleri ve bunların sırası listesini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="153c3-181">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span>  <span data-ttu-id="153c3-182">`<ClaimsProviderSelection>`öğesi, bir oturumu-up/oturum açma sayfasında bir kimlik sağlayıcısı düğmesini benzerdir.</span><span class="sxs-lookup"><span data-stu-id="153c3-182">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="153c3-183">Eklerseniz bir `<ClaimsProviderSelection>` öğesi Google + hesap için yeni bir düğme görüntülenir sayfasında bir kullanıcı adlandırıldığını olduğunda.</span><span class="sxs-lookup"><span data-stu-id="153c3-183">If you add a `<ClaimsProviderSelection>` element for Google+ account, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="153c3-184">Bu öğe eklemek için:</span><span class="sxs-lookup"><span data-stu-id="153c3-184">To add this element:</span></span>

1.  <span data-ttu-id="153c3-185">Bul `<UserJourney>` içeren düğüm `Id="SignUpOrSignIn"` kopyaladığınız kullanıcı gezisine içinde.</span><span class="sxs-lookup"><span data-stu-id="153c3-185">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>
2.  <span data-ttu-id="153c3-186">Bulun `<OrchestrationStep>` içeren düğümü`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="153c3-186">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="153c3-187">Aşağıdaki XML parçacığını altında ekleyin `<ClaimsProviderSelections>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="153c3-187">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="153c3-188">Düğme için bir eylem bağlantı kurun</span><span class="sxs-lookup"><span data-stu-id="153c3-188">Link the button to an action</span></span>
<span data-ttu-id="153c3-189">Yerinde bir düğmeye sahip olduğunuza göre bir eyleme bağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="153c3-189">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="153c3-190">Eylem, bu durumda, bir belirteç almak için Google + hesabı ile iletişim kurmak Azure AD B2C içindir.</span><span class="sxs-lookup"><span data-stu-id="153c3-190">The action, in this case, is for Azure AD B2C to communicate with Google+ account to receive a token.</span></span>

1.  <span data-ttu-id="153c3-191">Bul `<OrchestrationStep>` içeren `Order="2"` içinde `<UserJourney>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="153c3-191">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="153c3-192">Aşağıdaki XML parçacığını altında ekleyin `<ClaimsExchanges>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="153c3-192">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * <span data-ttu-id="153c3-193">Olun `Id` , aynı değere sahip `TargetClaimsExchangeId` önceki bölümde</span><span class="sxs-lookup"><span data-stu-id="153c3-193">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section</span></span>
> * <span data-ttu-id="153c3-194">Olun `TechnicalProfileReferenceId` kimliği ayarlanmış teknik profiline önceki (Google-OAUTH) oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="153c3-194">Ensure `TechnicalProfileReferenceId` ID is set to the technical profile you created earlier (Google-OAUTH).</span></span>

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="153c3-195">İlke kiracınız için karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="153c3-195">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="153c3-196">İçinde [Azure portal](https://portal.azure.com), içine geçiş [bağlam Azure AD B2C kiracınızın](active-directory-b2c-navigate-to-b2c-context.md), açarak **Azure AD B2C** dikey.</span><span class="sxs-lookup"><span data-stu-id="153c3-196">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="153c3-197">Seçin **kimlik deneyimi Framework**.</span><span class="sxs-lookup"><span data-stu-id="153c3-197">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="153c3-198">Açık **tüm ilkeler** dikey.</span><span class="sxs-lookup"><span data-stu-id="153c3-198">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="153c3-199">Seçin **karşıya İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="153c3-199">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="153c3-200">Denetleme **varsa ilkesi üzerine** kutusu.</span><span class="sxs-lookup"><span data-stu-id="153c3-200">Check **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="153c3-201">**Karşıya yükleme** TrustFrameworkExtensions.xml ve doğrulama başlayabildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="153c3-201">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="153c3-202">Özel ilke Şimdi Çalıştır kullanarak test</span><span class="sxs-lookup"><span data-stu-id="153c3-202">Test the custom policy by using Run Now</span></span>
1.  <span data-ttu-id="153c3-203">Açık **Azure AD B2C ayarlarını** ve Git **kimlik deneyimi Framework**.</span><span class="sxs-lookup"><span data-stu-id="153c3-203">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>

    >[!NOTE]
    >
    >    <span data-ttu-id="153c3-204">**Şimdi Çalıştır** Kiracı'preregistered için en az bir uygulama gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="153c3-204">**Run now** requires at least one application to be preregistered on the tenant.</span></span> 
    >    <span data-ttu-id="153c3-205">Uygulamaları kaydetmek öğrenmek için Azure AD B2C bkz [başlama](active-directory-b2c-get-started.md) makale veya [uygulama kaydı](active-directory-b2c-app-registration.md) makale.</span><span class="sxs-lookup"><span data-stu-id="153c3-205">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>


2.  <span data-ttu-id="153c3-206">Açık **B2C_1A_signup_signin**, karşıya yüklediğiniz bağlı olan taraf (RP) özel ilke.</span><span class="sxs-lookup"><span data-stu-id="153c3-206">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="153c3-207">Seçin **Şimdi Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="153c3-207">Select **Run now**.</span></span>
3.  <span data-ttu-id="153c3-208">Google + hesabı kullanarak oturum olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="153c3-208">You should be able to sign in using Google+ account.</span></span>

## <a name="optional-register-the-google-account-claims-provider-to-profile-edit-user-journey"></a><span data-ttu-id="153c3-209">[İsteğe bağlı] Google + hesap talep sağlayıcısını profil düzenleme kullanıcı gezisine kaydetme</span><span class="sxs-lookup"><span data-stu-id="153c3-209">[Optional] Register the Google+ account claims provider to Profile-Edit user journey</span></span>
<span data-ttu-id="153c3-210">Google + hesabı kimlik sağlayıcısı Ayrıca, kullanıcı eklemek isteyebilirsiniz `ProfileEdit` kullanıcı gezisine.</span><span class="sxs-lookup"><span data-stu-id="153c3-210">You may want to add the Google+ account identity provider also to your user `ProfileEdit` user journey.</span></span> <span data-ttu-id="153c3-211">Kullanılabilir hale getirmek için biz son iki adımı yineleyin:</span><span class="sxs-lookup"><span data-stu-id="153c3-211">To make it available, we repeat the last two steps:</span></span>

### <a name="display-the-button"></a><span data-ttu-id="153c3-212">Görüntü düğmesi</span><span class="sxs-lookup"><span data-stu-id="153c3-212">Display the button</span></span>
1.  <span data-ttu-id="153c3-213">Uzantı dosyası ilkenizin (örneğin, TrustFrameworkExtensions.xml) açın.</span><span class="sxs-lookup"><span data-stu-id="153c3-213">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="153c3-214">Bul `<UserJourney>` içeren düğüm `Id="ProfileEdit"` kopyaladığınız kullanıcı gezisine içinde.</span><span class="sxs-lookup"><span data-stu-id="153c3-214">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span></span>
3.  <span data-ttu-id="153c3-215">Bulun `<OrchestrationStep>` içeren düğümü`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="153c3-215">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="153c3-216">Aşağıdaki XML parçacığını altında ekleyin `<ClaimsProviderSelections>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="153c3-216">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="153c3-217">Düğme için bir eylem bağlantı kurun</span><span class="sxs-lookup"><span data-stu-id="153c3-217">Link the button to an action</span></span>
1.  <span data-ttu-id="153c3-218">Bul `<OrchestrationStep>` içeren `Order="2"` içinde `<UserJourney>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="153c3-218">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="153c3-219">Aşağıdaki XML parçacığını altında ekleyin `<ClaimsExchanges>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="153c3-219">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-the-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="153c3-220">Özel Profil Düzenleme İlkesi Şimdi Çalıştır kullanarak test</span><span class="sxs-lookup"><span data-stu-id="153c3-220">Test the custom Profile-Edit policy by using Run Now</span></span>

1.  <span data-ttu-id="153c3-221">Açık **Azure AD B2C ayarlarını** ve Git **kimlik deneyimi Framework**.</span><span class="sxs-lookup"><span data-stu-id="153c3-221">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="153c3-222">Açık **B2C_1A_ProfileEdit**, karşıya yüklediğiniz bağlı olan taraf (RP) özel ilke.</span><span class="sxs-lookup"><span data-stu-id="153c3-222">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="153c3-223">Seçin **Şimdi Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="153c3-223">Select **Run now**.</span></span>
3.  <span data-ttu-id="153c3-224">Google + hesabı kullanarak oturum olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="153c3-224">You should be able to sign in using Google+ account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="153c3-225">Tam ilke dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="153c3-225">Download the complete policy files</span></span>
<span data-ttu-id="153c3-226">İsteğe bağlı: Bu örnek dosyalar yerine dosyaları ile çalışmaya başlama özel ilkeler tamamladıktan sonra size yol kendi özel İlkesi kullanarak senaryonuz yapı öneririz.</span><span class="sxs-lookup"><span data-stu-id="153c3-226">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="153c3-227">Başvuru için örnek ilke dosyaları</span><span class="sxs-lookup"><span data-stu-id="153c3-227">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
