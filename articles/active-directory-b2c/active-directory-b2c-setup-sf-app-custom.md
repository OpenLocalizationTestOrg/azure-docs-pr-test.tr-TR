---
title: "Azure Active Directory B2C: özel ilkeler kullanılarak Salesforce SAML sağlayıcı ekleme | Microsoft Docs"
description: "Hakkında bilgi edinin toocreate ve Azure Active Directory B2C özel ilkelerini yönetin."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d7f4143f-cd7c-4939-91a8-231a4104dc2c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/11/2017
ms.author: parakhj
ms.openlocfilehash: f14c9d96980ff124110db7cfb58bf7cd81750b7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="396ff-103">Azure Active Directory B2C: SAML aracılığıyla Salesforce hesaplarını kullanarak oturum açın</span><span class="sxs-lookup"><span data-stu-id="396ff-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="396ff-104">Bu makale size nasıl gösterir toouse [özel ilkeler](active-directory-b2c-overview-custom.md) tooset oturum açma belirli Salesforce kuruluştan kullanıcılar için ayarlama.</span><span class="sxs-lookup"><span data-stu-id="396ff-104">This article shows you how toouse [custom policies](active-directory-b2c-overview-custom.md) tooset up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="396ff-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="396ff-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="396ff-106">Azure AD B2C Kurulumu</span><span class="sxs-lookup"><span data-stu-id="396ff-106">Azure AD B2C setup</span></span>

<span data-ttu-id="396ff-107">Tüm nasıl çok Göster hello adımları tamamladığınızdan emin olun[özel ilkelerini kullanmaya başlama](active-directory-b2c-get-started-custom.md) Azure Active Directory B2C içinde (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="396ff-107">Ensure that you have completed all of hello steps that show you how too[get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="396ff-108">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="396ff-108">These include:</span></span>

* <span data-ttu-id="396ff-109">Azure AD B2C kiracısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="396ff-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="396ff-110">Bir Azure AD B2C uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="396ff-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="396ff-111">İki ilke altyapısı uygulama kaydedin.</span><span class="sxs-lookup"><span data-stu-id="396ff-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="396ff-112">Anahtarları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="396ff-112">Set up keys.</span></span>
* <span data-ttu-id="396ff-113">Merhaba başlangıç paketi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="396ff-113">Set up hello starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="396ff-114">Salesforce Kurulum</span><span class="sxs-lookup"><span data-stu-id="396ff-114">Salesforce setup</span></span>

<span data-ttu-id="396ff-115">Bu makalede, zaten hello aşağıdakileri yaptığınızdan varsayın:</span><span class="sxs-lookup"><span data-stu-id="396ff-115">In this article, we assume that you have already done hello following:</span></span>

* <span data-ttu-id="396ff-116">İmzalanmış Salesforce hesabınız için.</span><span class="sxs-lookup"><span data-stu-id="396ff-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="396ff-117">Oturum açabileceğiniz bir [ücretsiz bir geliştirici sürümü hesap](https://developer.salesforce.com/signup).</span><span class="sxs-lookup"><span data-stu-id="396ff-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="396ff-118">[My etki alanını ayarlama](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) Salesforce kuruluşunuz için.</span><span class="sxs-lookup"><span data-stu-id="396ff-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="396ff-119">Kullanıcıların devredebilir Salesforce ayarlandı</span><span class="sxs-lookup"><span data-stu-id="396ff-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="396ff-120">toohelp Azure AD B2C Salesforce ile iletişim kurmak, tooget hello Salesforce meta veri URL'sini gerekir.</span><span class="sxs-lookup"><span data-stu-id="396ff-120">toohelp Azure AD B2C communicate with Salesforce, you need tooget hello Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="396ff-121">Salesforce kimlik sağlayıcısı olarak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="396ff-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="396ff-122">Bu makalede, kullanmakta olan varsayıyoruz [Salesforce Şimşek deneyimi](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span><span class="sxs-lookup"><span data-stu-id="396ff-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="396ff-123">[İçinde tooSalesforce oturum](https://login.salesforce.com/).</span><span class="sxs-lookup"><span data-stu-id="396ff-123">[Sign in tooSalesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="396ff-124">Merhaba üzerinde menüsünde altında sol **ayarları**, genişletin **kimlik**ve ardından **kimlik sağlayıcısı**.</span><span class="sxs-lookup"><span data-stu-id="396ff-124">On hello left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="396ff-125">Tıklatın **etkinleştirme kimlik sağlayıcısı**.</span><span class="sxs-lookup"><span data-stu-id="396ff-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="396ff-126">Altında **Select hello sertifika**seçin Salesforce toouse toocommunicate Azure AD B2C ile istediğiniz hello sertifika.</span><span class="sxs-lookup"><span data-stu-id="396ff-126">Under **Select hello certificate**, select hello certificate you want Salesforce toouse toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="396ff-127">(Merhaba varsayılan sertifika kullanabilirsiniz.) **Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="396ff-127">(You can use hello default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="396ff-128">Salesforce'ta bağlı bir uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="396ff-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="396ff-129">Merhaba üzerinde **kimlik sağlayıcısı** sayfasında, çok Git**hizmet sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="396ff-129">On hello **Identity Provider** page, go too**Service Providers**.</span></span>
2. <span data-ttu-id="396ff-130">Tıklatın **hizmet sağlayıcıları bağlı uygulamalar şimdi oluşturulur. Burayı tıklatın.**</span><span class="sxs-lookup"><span data-stu-id="396ff-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="396ff-131">Altında **temel bilgileri**, bağlı uygulamanız için hello gerekli değerleri girin.</span><span class="sxs-lookup"><span data-stu-id="396ff-131">Under **Basic Information**,  enter hello required values for your connected app.</span></span>
4. <span data-ttu-id="396ff-132">Altında **Web uygulaması ayarları**seçin hello **etkinleştirmek SAML** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="396ff-132">Under **Web App Settings**, select hello **Enable SAML** check box.</span></span>
5. <span data-ttu-id="396ff-133">Merhaba, **varlık kimliği** alanında, URL aşağıdaki hello girin.</span><span class="sxs-lookup"><span data-stu-id="396ff-133">In hello **Entity ID** field, enter hello following URL.</span></span> <span data-ttu-id="396ff-134">Merhaba değeri yerini olmak `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="396ff-134">Ensure that you replace hello value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="396ff-135">Merhaba, **ACS URL** alanında, URL aşağıdaki hello girin.</span><span class="sxs-lookup"><span data-stu-id="396ff-135">In hello **ACS URL** field, enter hello following URL.</span></span> <span data-ttu-id="396ff-136">Merhaba değeri yerini olmak `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="396ff-136">Ensure that you replace hello value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="396ff-137">Merhaba tüm diğer ayarlar için varsayılan değerleri bırakın.</span><span class="sxs-lookup"><span data-stu-id="396ff-137">Leave hello default values for all other settings.</span></span>
8. <span data-ttu-id="396ff-138">Merhaba listesinin toohello altına'e gidin ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="396ff-138">Scroll toohello bottom of hello list, and then click **Save**.</span></span>

### <a name="get-hello-metadata-url"></a><span data-ttu-id="396ff-139">Merhaba meta veri URL'sini alma</span><span class="sxs-lookup"><span data-stu-id="396ff-139">Get hello metadata URL</span></span>

1. <span data-ttu-id="396ff-140">Merhaba genel bakış sayfasında, bağlı uygulamanızın tıklayın **Yönet**.</span><span class="sxs-lookup"><span data-stu-id="396ff-140">On hello overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="396ff-141">Merhaba değerini kopyalayın **meta veri bulma uç noktası**ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="396ff-141">Copy hello value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="396ff-142">Bu makalenin sonraki bölümlerinde kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="396ff-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-toofederate"></a><span data-ttu-id="396ff-143">Salesforce kullanıcılar toofederate ayarlayın</span><span class="sxs-lookup"><span data-stu-id="396ff-143">Set up Salesforce users toofederate</span></span>

1. <span data-ttu-id="396ff-144">Merhaba üzerinde **Yönet** sayfa bağlı uygulamanızı çok Git**profilleri**.</span><span class="sxs-lookup"><span data-stu-id="396ff-144">On hello **Manage** page of your connected app, go too**Profiles**.</span></span>
2. <span data-ttu-id="396ff-145">Tıklatın **profillerini yönetmek**.</span><span class="sxs-lookup"><span data-stu-id="396ff-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="396ff-146">Hello profilleri (veya kullanıcı grupları) seçin, Azure AD B2C ile toofederate istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="396ff-146">Select hello profiles (or groups of users) that you want toofederate with Azure AD B2C.</span></span> <span data-ttu-id="396ff-147">Bir sistem yöneticisi olarak hello seçin **Sistem Yöneticisi** Salesforce hesabınıza kullanarak birleştirmek için onay kutusunu.</span><span class="sxs-lookup"><span data-stu-id="396ff-147">As a system administrator, select hello **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="396ff-148">Azure AD B2C için imzalama sertifikası oluştur</span><span class="sxs-lookup"><span data-stu-id="396ff-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="396ff-149">Azure AD B2C tarafından imzalanmış tooSalesforce gerek toobe gönderdiği istekleri.</span><span class="sxs-lookup"><span data-stu-id="396ff-149">Requests sent tooSalesforce need toobe signed by Azure AD B2C.</span></span> <span data-ttu-id="396ff-150">toogenerate bir imzalama sertifikası Azure PowerShell'i açın ve ardından hello aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="396ff-150">toogenerate a signing certificate, open Azure PowerShell, and then run hello following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="396ff-151">Merhaba Kiracı adı ve parola hello üst iki satırlardaki güncelleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="396ff-151">Make sure that you update hello tenant name and password in hello top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-hello-saml-signing-certificate-tooazure-ad-b2c"></a><span data-ttu-id="396ff-152">Merhaba SAML imzalama sertifikası tooAzure AD B2C ekleme</span><span class="sxs-lookup"><span data-stu-id="396ff-152">Add hello SAML signing certificate tooAzure AD B2C</span></span>

<span data-ttu-id="396ff-153">Sertifika tooyour Azure AD B2C Kiracı imzalama hello karşıya yükle:</span><span class="sxs-lookup"><span data-stu-id="396ff-153">Upload hello signing certificate tooyour Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="396ff-154">Tooyour Azure AD B2C Kiracı gidin.</span><span class="sxs-lookup"><span data-stu-id="396ff-154">Go tooyour Azure AD B2C tenant.</span></span> <span data-ttu-id="396ff-155">Tıklatın **ayarları** > **kimlik deneyimi Framework** > **İlkesi anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="396ff-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="396ff-156">Tıklatın **+ Ekle**ve ardından:</span><span class="sxs-lookup"><span data-stu-id="396ff-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="396ff-157">Tıklatın **seçenekleri** > **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="396ff-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="396ff-158">Girin bir **adı** (örneğin, SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="396ff-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="396ff-159">Merhaba önek *B2C_1A_* anahtarınızı toohello adını otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="396ff-159">hello prefix *B2C_1A_* is automatically added toohello name of your key.</span></span>
    3. <span data-ttu-id="396ff-160">tooselect, sertifikanızı seçin **dosya denetimi karşıya**.</span><span class="sxs-lookup"><span data-stu-id="396ff-160">tooselect your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="396ff-161">Merhaba PowerShell komut dosyasında ayarlanan hello sertifikanın parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="396ff-161">Enter hello certificate's password that you set in hello PowerShell script.</span></span>
3. <span data-ttu-id="396ff-162">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="396ff-162">Click **Create**.</span></span>
4. <span data-ttu-id="396ff-163">Bir anahtar (örneğin, B2C_1A_SAMLSigningCert) oluşturduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="396ff-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="396ff-164">Merhaba tam adı not edin (de dahil olmak üzere *B2C_1A_*).</span><span class="sxs-lookup"><span data-stu-id="396ff-164">Take note of hello full name (including *B2C_1A_*).</span></span> <span data-ttu-id="396ff-165">Daha sonra hello İlkesi toothis anahtar başvurur.</span><span class="sxs-lookup"><span data-stu-id="396ff-165">You will refer toothis key later in hello policy.</span></span>

## <a name="create-hello-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="396ff-166">Temel ilkenizde Hello Salesforce SAML Talep sağlayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="396ff-166">Create hello Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="396ff-167">Kullanıcıların Salesforce kullanarak oturum açabilmeniz için bir talep sağlayıcısı olarak toodefine Salesforce gerekir.</span><span class="sxs-lookup"><span data-stu-id="396ff-167">You need toodefine Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="396ff-168">Diğer bir deyişle, Azure AD B2C ile iletişim kuracak toospecify hello uç noktası gerekir.</span><span class="sxs-lookup"><span data-stu-id="396ff-168">In other words, you need toospecify hello endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="396ff-169">Merhaba uç nokta olacak *sağlamak* bir dizi *talep* Azure AD B2C belirli bir kullanıcı doğrulaması tooverify kullanır.</span><span class="sxs-lookup"><span data-stu-id="396ff-169">hello endpoint will *provide* a set of *claims* that Azure AD B2C uses tooverify that a specific user has authenticated.</span></span> <span data-ttu-id="396ff-170">toodo bunu eklemek bir `<ClaimsProvider>` ilkenizin hello uzantısı dosyasında Salesforce için:</span><span class="sxs-lookup"><span data-stu-id="396ff-170">toodo this, add a `<ClaimsProvider>` for Salesforce in hello extension file of your policy:</span></span>

1. <span data-ttu-id="396ff-171">Çalışma dizininizi hello uzantısının (TrustFrameworkExtensions.xml) açın.</span><span class="sxs-lookup"><span data-stu-id="396ff-171">In your working directory, open hello extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="396ff-172">Hello bulur `<ClaimsProviders>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="396ff-172">Find hello `<ClaimsProviders>` section.</span></span> <span data-ttu-id="396ff-173">Yoksa, hello kök düğümü altında oluşturun.</span><span class="sxs-lookup"><span data-stu-id="396ff-173">If it does not exist, create it under hello root node.</span></span>
3. <span data-ttu-id="396ff-174">Yeni bir ekleme `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="396ff-174">Add a new `<ClaimsProvider>`:</span></span>

    ```XML
    <ClaimsProvider>
      <Domain>salesforce</Domain>
      <DisplayName>Salesforce</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="salesforce">
          <DisplayName>Salesforce</DisplayName>
          <Description>Login with your Salesforce account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="WantsSignedAssertions">false</Item>
            <Item Key="PartnerEntity">https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userId"/>
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="username"/>
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="externalIdp"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="SAMLIdp" />
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

<span data-ttu-id="396ff-175">Merhaba altında `<ClaimsProvider>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="396ff-175">Under hello `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="396ff-176">Değiştirmek için hello değer `<Domain>` ayırt eden benzersiz bir değer tooa `<ClaimsProvider>` diğer kimlik sağlayıcılardan gelen.</span><span class="sxs-lookup"><span data-stu-id="396ff-176">Change hello value for `<Domain>` tooa unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="396ff-177">Merhaba değeri güncelleştirme `<DisplayName>` hello tooa görünen adı talep sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="396ff-177">Update hello value for `<DisplayName>` tooa display name for hello claims provider.</span></span> <span data-ttu-id="396ff-178">Şu anda, bu değer kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="396ff-178">Currently, this value is not used.</span></span>

### <a name="update-hello-technical-profile"></a><span data-ttu-id="396ff-179">Merhaba teknik profilini güncelleştir</span><span class="sxs-lookup"><span data-stu-id="396ff-179">Update hello technical profile</span></span>

<span data-ttu-id="396ff-180">tooget Salesforce, bir SAML belirtecinden Azure AD B2C, Azure Active Directory (Azure AD) ile toocommunicate kullanacağını hello protokolleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="396ff-180">tooget a SAML token from Salesforce, define hello protocols that Azure AD B2C will use toocommunicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="396ff-181">Hello bunu `<TechnicalProfile>` öğesinin `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="396ff-181">Do this in hello `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="396ff-182">Merhaba Hello Kimliğini güncelleştirme `<TechnicalProfile>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="396ff-182">Update hello ID of hello `<TechnicalProfile>` node.</span></span> <span data-ttu-id="396ff-183">Bu kimliği kullanılan toorefer toothis hello İlkesi diğer kısımlarından teknik profilidir.</span><span class="sxs-lookup"><span data-stu-id="396ff-183">This ID is used toorefer toothis technical profile from other parts of hello policy.</span></span>
2. <span data-ttu-id="396ff-184">Merhaba değeri güncelleştirme `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="396ff-184">Update hello value for `<DisplayName>`.</span></span> <span data-ttu-id="396ff-185">Bu değer düğmesinde hello oturum açma, oturum açma sayfasında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="396ff-185">This value is displayed on hello sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="396ff-186">Merhaba değeri güncelleştirme `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="396ff-186">Update hello value for `<Description>`.</span></span>
4. <span data-ttu-id="396ff-187">Salesforce hello SAML 2.0 protokolünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="396ff-187">Salesforce uses hello SAML 2.0 protocol.</span></span> <span data-ttu-id="396ff-188">Bu hello değeri olun `<Protocol>` olan **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="396ff-188">Ensure that hello value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="396ff-189">Güncelleştirme hello `<Metadata>` hello belirli Salesforce hesabınızın XML tooreflect hello ayarlarını önceki bölümünde.</span><span class="sxs-lookup"><span data-stu-id="396ff-189">Update hello `<Metadata>` section in hello preceding XML tooreflect hello settings for your specific Salesforce account.</span></span> <span data-ttu-id="396ff-190">Hello XML, hello meta veri değerlerini güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="396ff-190">In hello XML, update hello metadata values:</span></span>

1. <span data-ttu-id="396ff-191">Merhaba değerini güncelleştirmek `<Item Key="PartnerEntity">` daha önce kopyaladığınız hello Salesforce meta veri URL'sine sahip.</span><span class="sxs-lookup"><span data-stu-id="396ff-191">Update hello value of `<Item Key="PartnerEntity">` with hello Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="396ff-192">Biçim aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="396ff-192">It has hello following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="396ff-193">Merhaba, `<CryptographicKeys>` bölümünde, her iki örnekleri için güncelleştirme hello değeri `StorageReferenceId` hello anahtarının imzalama sertifikanızın (örneğin, B2C_1A_SAMLSigningCert) toohello adı.</span><span class="sxs-lookup"><span data-stu-id="396ff-193">In hello `<CryptographicKeys>` section, update hello value for both instances of `StorageReferenceId` toohello name of hello key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-hello-extension-file-for-verification"></a><span data-ttu-id="396ff-194">Doğrulama Hello uzantısı dosyasını karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="396ff-194">Upload hello extension file for verification</span></span>

<span data-ttu-id="396ff-195">Böylece Azure AD B2C bilir ilkeniz yapılandırılmıştır nasıl toocommunicate Salesforce ile.</span><span class="sxs-lookup"><span data-stu-id="396ff-195">Your policy is now configured so that Azure AD B2C knows how toocommunicate with Salesforce.</span></span> <span data-ttu-id="396ff-196">Merhaba uzantısının olmadığından sorunları kadar tooverify ilkenizin karşıya yüklemeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="396ff-196">Try uploading hello extension file of your policy, tooverify that there aren't any issues so far.</span></span> <span data-ttu-id="396ff-197">tooupload hello uzantısının ilkenizin:</span><span class="sxs-lookup"><span data-stu-id="396ff-197">tooupload hello extension file of your policy:</span></span>

1. <span data-ttu-id="396ff-198">Azure AD B2C kiracınızda toohello Git **tüm ilkeler** dikey.</span><span class="sxs-lookup"><span data-stu-id="396ff-198">In your Azure AD B2C tenant, go toohello **All Policies** blade.</span></span>
2. <span data-ttu-id="396ff-199">Select hello **varsa hello ilkesi üzerine** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="396ff-199">Select hello **Overwrite hello policy if it exists** check box.</span></span>
3. <span data-ttu-id="396ff-200">Merhaba uzantısının (TrustFrameworkExtensions.xml) karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="396ff-200">Upload hello extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="396ff-201">Doğrulama başarısız olmayan emin olun.</span><span class="sxs-lookup"><span data-stu-id="396ff-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-hello-salesforce-saml-claims-provider-tooa-user-journey"></a><span data-ttu-id="396ff-202">Merhaba Salesforce SAML talep sağlayıcısı tooa kullanıcı gezisine kaydetme</span><span class="sxs-lookup"><span data-stu-id="396ff-202">Register hello Salesforce SAML claims provider tooa user journey</span></span>

<span data-ttu-id="396ff-203">Ardından, hello Salesforce SAML kimlik sağlayıcısı tooone kullanıcı Yolculuklar olarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="396ff-203">Next, add hello Salesforce SAML identity provider tooone of your user journeys.</span></span> <span data-ttu-id="396ff-204">Bu noktada, hello kimlik sağlayıcısı ayarlandı, ancak herhangi bir hello kullanıcı kaydolma veya oturum açma sayfası üzerinde kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="396ff-204">At this point, hello identity provider has been set up, but it’s not available on any of hello user sign-up or sign-in pages.</span></span> <span data-ttu-id="396ff-205">tooadd hello kimlik sağlayıcısı tooa oturum açma sayfası, ilk olarak, var olan bir şablonu kullanıcı gezisine bir kopyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="396ff-205">tooadd hello identity provider tooa sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="396ff-206">Ardından, ayrıca hello Azure AD kimlik sağlayıcısı sahip olması hello şablonu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="396ff-206">Then, modify hello template so that it also has hello Azure AD identity provider.</span></span>

1. <span data-ttu-id="396ff-207">Merhaba temel dosyanın ilkenizin (örneğin, TrustFrameworkBase.xml) açın.</span><span class="sxs-lookup"><span data-stu-id="396ff-207">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="396ff-208">Hello bulur `<UserJourneys>` öğesi ve kopyalama hello tüm `<UserJourney>` değeri, "SignUpOrSignIn" kimliğine dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="396ff-208">Find hello `<UserJourneys>` element, and then copy hello entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="396ff-209">Merhaba uzantısının (örneğin, TrustFrameworkExtensions.xml) açın.</span><span class="sxs-lookup"><span data-stu-id="396ff-209">Open hello extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="396ff-210">Hello bulur `<UserJourneys>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="396ff-210">Find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="396ff-211">Merhaba öğe yoksa, bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="396ff-211">If hello element doesn't exist, create one.</span></span>
4. <span data-ttu-id="396ff-212">Tüm kopyalanan Yapıştır hello `<UserJourney>` hello alt olarak `<UserJourneys>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="396ff-212">Paste hello entire copied `<UserJourney>` as a child of hello `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="396ff-213">Merhaba yeni Hello Kimliğini yeniden adlandırma `<UserJourney>` (örneğin, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="396ff-213">Rename hello ID of hello new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-hello-identity-provider-button"></a><span data-ttu-id="396ff-214">Görüntü hello kimlik sağlayıcısı düğmesi</span><span class="sxs-lookup"><span data-stu-id="396ff-214">Display hello identity provider button</span></span>

<span data-ttu-id="396ff-215">Merhaba `<ClaimsProviderSelection>` benzer tooan kimlik sağlayıcısı düğmesi kaydolma veya oturum açma sayfasında bir öğedir.</span><span class="sxs-lookup"><span data-stu-id="396ff-215">hello `<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="396ff-216">Ekleyerek bir `<ClaimsProviderSelection>` öğesi Salesforce için yeni bir düğme görüntülenir kullanıcı toothis sayfası çıktığında.</span><span class="sxs-lookup"><span data-stu-id="396ff-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes toothis page.</span></span> <span data-ttu-id="396ff-217">toodisplay hello kimlik sağlayıcısı düğmesi:</span><span class="sxs-lookup"><span data-stu-id="396ff-217">toodisplay hello identity provider button:</span></span>

1. <span data-ttu-id="396ff-218">Merhaba, `<UserJourney>` oluşturduğunuz, hello Bul `<OrchestrationStep>` ile `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="396ff-218">In hello `<UserJourney>` that you created, find hello `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="396ff-219">XML aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="396ff-219">Add hello following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="396ff-220">Ayarlama `TargetClaimsExchangeId` tooa mantıksal bir değer.</span><span class="sxs-lookup"><span data-stu-id="396ff-220">Set `TargetClaimsExchangeId` tooa logical value.</span></span> <span data-ttu-id="396ff-221">Aşağıdaki hello aynı öneririz kuralı başkalarının olarak (örneğin,  *\[ClaimProviderName\]Exchange*).</span><span class="sxs-lookup"><span data-stu-id="396ff-221">We recommend following hello same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-hello-identity-provider-button-tooan-action"></a><span data-ttu-id="396ff-222">Bağlantı hello kimlik sağlayıcısı düğmesi tooan eylemi</span><span class="sxs-lookup"><span data-stu-id="396ff-222">Link hello identity provider button tooan action</span></span>

<span data-ttu-id="396ff-223">Bir kimlik sağlayıcısı düğmesi yerinde sahip olduğunuza göre tooan eylem bağlantı kurun.</span><span class="sxs-lookup"><span data-stu-id="396ff-223">Now that you have an identity provider button in place, link it tooan action.</span></span> <span data-ttu-id="396ff-224">Bu durumda, Azure AD B2C toocommunicate Salesforce tooreceive SAML belirteci ile Merhaba eylem içindir.</span><span class="sxs-lookup"><span data-stu-id="396ff-224">In this case, hello action is for Azure AD B2C toocommunicate with Salesforce tooreceive a SAML token.</span></span> <span data-ttu-id="396ff-225">Merhaba teknik profil için Salesforce SAML bağlayarak Talep sağlayıcı bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="396ff-225">You can do this by linking hello technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="396ff-226">Merhaba, `<UserJourney>` düğümü, Bul hello `<OrchestrationStep>` ile `Order="2"`.</span><span class="sxs-lookup"><span data-stu-id="396ff-226">In hello `<UserJourney>` node, find hello `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="396ff-227">XML aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="396ff-227">Add hello following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="396ff-228">Güncelleştirme `Id` toohello aynı değer, sizin için daha önce kullanılan `TargetClaimsExchangeId`.</span><span class="sxs-lookup"><span data-stu-id="396ff-228">Update `Id` toohello same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="396ff-229">Güncelleştirme `TechnicalProfileReferenceId` toohello `Id` hello teknik daha önce oluşturduğunuz (örneğin, ContosoProfile) profil.</span><span class="sxs-lookup"><span data-stu-id="396ff-229">Update `TechnicalProfileReferenceId` toohello `Id` of hello technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-hello-updated-extension-file"></a><span data-ttu-id="396ff-230">Merhaba güncelleştirilmiş uzantısı dosyasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="396ff-230">Upload hello updated extension file</span></span>

<span data-ttu-id="396ff-231">Değiştirme hello uzantısının yapılır.</span><span class="sxs-lookup"><span data-stu-id="396ff-231">You are done modifying hello extension file.</span></span> <span data-ttu-id="396ff-232">Kaydet ve bu dosyayı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="396ff-232">Save and upload this file.</span></span> <span data-ttu-id="396ff-233">Tüm Doğrulamalar başarıyla emin olun.</span><span class="sxs-lookup"><span data-stu-id="396ff-233">Ensure that all validations succeed.</span></span>

### <a name="update-hello-relying-party-file"></a><span data-ttu-id="396ff-234">Merhaba bağlı olan taraf dosyasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="396ff-234">Update hello relying party file</span></span>

<span data-ttu-id="396ff-235">Ardından, oluşturduğunuz hello kullanıcı gezisine başlatan hello bağlı olan taraf (RP) dosyasını güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="396ff-235">Next, update hello relying party (RP) file that initiates hello user journey that you created:</span></span>

1. <span data-ttu-id="396ff-236">Çalışma dizininizi SignUpOrSignIn.xml kopyası.</span><span class="sxs-lookup"><span data-stu-id="396ff-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="396ff-237">Sonra (örneğin, SignUpOrSignInWithAAD.xml) yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="396ff-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="396ff-238">Açık hello yeni dosya ve güncelleştirme hello `PolicyId` için öznitelik `<TrustFrameworkPolicy>` benzersiz bir değere sahip.</span><span class="sxs-lookup"><span data-stu-id="396ff-238">Open hello new file and update hello `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="396ff-239">Bu hello ilkeniz (örneğin, SignUpOrSignInWithAAD) adıdır.</span><span class="sxs-lookup"><span data-stu-id="396ff-239">This is hello name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="396ff-240">Merhaba değiştirme `ReferenceId` özniteliğini `<DefaultUserJourney>` toomatch hello `Id` (örneğin, SignUpOrSignUsingContoso) oluşturduğunuz hello yeni kullanıcı gezisine biri.</span><span class="sxs-lookup"><span data-stu-id="396ff-240">Modify hello `ReferenceId` attribute in `<DefaultUserJourney>` toomatch hello `Id` of hello new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="396ff-241">Yaptığınız değişiklikleri kaydedin ve hello dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="396ff-241">Save your changes, and then upload hello file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="396ff-242">Test etme ve sorun giderme</span><span class="sxs-lookup"><span data-stu-id="396ff-242">Test and troubleshoot</span></span>

<span data-ttu-id="396ff-243">yalnızca, hello Azure portal, karşıya yüklediğiniz tootest hello özel ilke toohello İlkesi dikey penceresine gidin ve ardından **Şimdi Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="396ff-243">tootest hello custom policy that you just uploaded, in hello Azure portal, go toohello policy blade, and then click **Run now**.</span></span> <span data-ttu-id="396ff-244">Başarısız olursa bkz [özel ilke sorunlarını giderme](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="396ff-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="396ff-245">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="396ff-245">Next steps</span></span>

<span data-ttu-id="396ff-246">Çok görüş[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="396ff-246">Provide feedback too[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
