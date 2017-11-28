---
title: "Azure Active Directory B2C: özel ilkeler kullanılarak Salesforce SAML sağlayıcı ekleme | Microsoft Docs"
description: "Azure Active Directory B2C özel ilkeleri oluşturun ve yönetin hakkında bilgi edinin."
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
ms.openlocfilehash: 269cbd80fb6e861fa8588025eec70b6c6e2890d7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="ab9b6-103">Azure Active Directory B2C: SAML aracılığıyla Salesforce hesaplarını kullanarak oturum açın</span><span class="sxs-lookup"><span data-stu-id="ab9b6-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="ab9b6-104">Bu makalede nasıl kullanılacağı gösterilmektedir [özel ilkeler](active-directory-b2c-overview-custom.md) oturum açma kullanıcıların belirli bir Salesforce kuruluştan ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-104">This article shows you how to use [custom policies](active-directory-b2c-overview-custom.md) to set up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab9b6-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ab9b6-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="ab9b6-106">Azure AD B2C Kurulumu</span><span class="sxs-lookup"><span data-stu-id="ab9b6-106">Azure AD B2C setup</span></span>

<span data-ttu-id="ab9b6-107">Nasıl yapacağınızı tüm adımları tamamladığınızdan emin olmak için [özel ilkelerini kullanmaya başlama](active-directory-b2c-get-started-custom.md) Azure Active Directory B2C içinde (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="ab9b6-107">Ensure that you have completed all of the steps that show you how to [get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="ab9b6-108">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="ab9b6-108">These include:</span></span>

* <span data-ttu-id="ab9b6-109">Azure AD B2C kiracısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="ab9b6-110">Bir Azure AD B2C uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="ab9b6-111">İki ilke altyapısı uygulama kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="ab9b6-112">Anahtarları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-112">Set up keys.</span></span>
* <span data-ttu-id="ab9b6-113">Başlangıç paketi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-113">Set up the starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="ab9b6-114">Salesforce Kurulum</span><span class="sxs-lookup"><span data-stu-id="ab9b6-114">Salesforce setup</span></span>

<span data-ttu-id="ab9b6-115">Bu makalede, aşağıdaki yapmış olduğunuz olduğunu varsayın:</span><span class="sxs-lookup"><span data-stu-id="ab9b6-115">In this article, we assume that you have already done the following:</span></span>

* <span data-ttu-id="ab9b6-116">İmzalanmış Salesforce hesabınız için.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="ab9b6-117">Oturum açabileceğiniz bir [ücretsiz bir geliştirici sürümü hesap](https://developer.salesforce.com/signup).</span><span class="sxs-lookup"><span data-stu-id="ab9b6-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="ab9b6-118">[My etki alanını ayarlama](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) Salesforce kuruluşunuz için.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="ab9b6-119">Kullanıcıların devredebilir Salesforce ayarlandı</span><span class="sxs-lookup"><span data-stu-id="ab9b6-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="ab9b6-120">Azure AD B2C ile Salesforce iletişim yardımcı olmak için Salesforce meta veri URL'sini almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-120">To help Azure AD B2C communicate with Salesforce, you need to get the Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="ab9b6-121">Salesforce kimlik sağlayıcısı olarak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ab9b6-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="ab9b6-122">Bu makalede, kullanmakta olan varsayıyoruz [Salesforce Şimşek deneyimi](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span><span class="sxs-lookup"><span data-stu-id="ab9b6-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="ab9b6-123">[Salesforce oturum](https://login.salesforce.com/).</span><span class="sxs-lookup"><span data-stu-id="ab9b6-123">[Sign in to Salesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="ab9b6-124">Sol menüde altında **ayarları**, genişletin **kimlik**ve ardından **kimlik sağlayıcısı**.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-124">On the left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="ab9b6-125">Tıklatın **etkinleştirme kimlik sağlayıcısı**.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="ab9b6-126">Altında **sertifikayı seçin**, Salesforce Azure AD B2C ile iletişim kurmak için kullanmak istediğiniz sertifikayı seçin.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-126">Under **Select the certificate**, select the certificate you want Salesforce to use to communicate with Azure AD B2C.</span></span> <span data-ttu-id="ab9b6-127">(Varsayılan sertifikayı kullanabilirsiniz.) **Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-127">(You can use the default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="ab9b6-128">Salesforce'ta bağlı bir uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="ab9b6-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="ab9b6-129">Üzerinde **kimlik sağlayıcısı** sayfasında, Git **hizmet sağlayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-129">On the **Identity Provider** page, go to **Service Providers**.</span></span>
2. <span data-ttu-id="ab9b6-130">Tıklatın **hizmet sağlayıcıları bağlı uygulamalar şimdi oluşturulur. Burayı tıklatın.**</span><span class="sxs-lookup"><span data-stu-id="ab9b6-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="ab9b6-131">Altında **temel bilgileri**, bağlı uygulamanız için gerekli değerleri girin.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-131">Under **Basic Information**,  enter the required values for your connected app.</span></span>
4. <span data-ttu-id="ab9b6-132">Altında **Web uygulaması ayarları**seçin **etkinleştirmek SAML** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-132">Under **Web App Settings**, select the **Enable SAML** check box.</span></span>
5. <span data-ttu-id="ab9b6-133">İçinde **varlık kimliği** alanında, aşağıdaki URL'yi girin.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-133">In the **Entity ID** field, enter the following URL.</span></span> <span data-ttu-id="ab9b6-134">Değeri yerini olmak `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-134">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="ab9b6-135">İçinde **ACS URL** alanında, aşağıdaki URL'yi girin.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-135">In the **ACS URL** field, enter the following URL.</span></span> <span data-ttu-id="ab9b6-136">Değeri yerini olmak `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-136">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="ab9b6-137">Tüm diğer ayarlar için varsayılan değerleri bırakın.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-137">Leave the default values for all other settings.</span></span>
8. <span data-ttu-id="ab9b6-138">Listenin sonuna kaydırın ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-138">Scroll to the bottom of the list, and then click **Save**.</span></span>

### <a name="get-the-metadata-url"></a><span data-ttu-id="ab9b6-139">Meta veri URL'sini alın</span><span class="sxs-lookup"><span data-stu-id="ab9b6-139">Get the metadata URL</span></span>

1. <span data-ttu-id="ab9b6-140">Bağlı uygulamanızı genel bakış sayfasında **Yönet**.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-140">On the overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="ab9b6-141">Değeri kopyalama **meta veri bulma uç noktası**ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-141">Copy the value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="ab9b6-142">Bu makalenin sonraki bölümlerinde kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-to-federate"></a><span data-ttu-id="ab9b6-143">Salesforce kullanıcıları birleştirmek için ayarlama</span><span class="sxs-lookup"><span data-stu-id="ab9b6-143">Set up Salesforce users to federate</span></span>

1. <span data-ttu-id="ab9b6-144">Üzerinde **Yönet** sayfasında, bağlı uygulama, Git **profilleri**.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-144">On the **Manage** page of your connected app, go to **Profiles**.</span></span>
2. <span data-ttu-id="ab9b6-145">Tıklatın **profillerini yönetmek**.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="ab9b6-146">Profilleri (veya kullanıcı grupları) seçin, Azure AD B2C ile birleştirmek istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-146">Select the profiles (or groups of users) that you want to federate with Azure AD B2C.</span></span> <span data-ttu-id="ab9b6-147">Bir sistem yöneticisi olarak seçin **Sistem Yöneticisi** Salesforce hesabınıza kullanarak birleştirmek için onay kutusunu.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-147">As a system administrator, select the **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="ab9b6-148">Azure AD B2C için imzalama sertifikası oluştur</span><span class="sxs-lookup"><span data-stu-id="ab9b6-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="ab9b6-149">Salesforce gönderilen istekleri Azure AD B2C tarafından imzalanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-149">Requests sent to Salesforce need to be signed by Azure AD B2C.</span></span> <span data-ttu-id="ab9b6-150">Bir imzalama sertifikası oluşturmak için Azure PowerShell'i açın ve aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-150">To generate a signing certificate, open Azure PowerShell, and then run the following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="ab9b6-151">Kiracı adı ve parola üstteki iki satırlarındaki güncelleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-151">Make sure that you update the tenant name and password in the top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-the-saml-signing-certificate-to-azure-ad-b2c"></a><span data-ttu-id="ab9b6-152">Azure AD B2C'ye SAML imzalama sertifikası ekleme</span><span class="sxs-lookup"><span data-stu-id="ab9b6-152">Add the SAML signing certificate to Azure AD B2C</span></span>

<span data-ttu-id="ab9b6-153">İmzalama sertifikasının, Azure AD B2C kiracınızın karşıya yükle:</span><span class="sxs-lookup"><span data-stu-id="ab9b6-153">Upload the signing certificate to your Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="ab9b6-154">Azure AD B2C kiracınızın gidin.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-154">Go to your Azure AD B2C tenant.</span></span> <span data-ttu-id="ab9b6-155">Tıklatın **ayarları** > **kimlik deneyimi Framework** > **İlkesi anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="ab9b6-156">Tıklatın **+ Ekle**ve ardından:</span><span class="sxs-lookup"><span data-stu-id="ab9b6-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="ab9b6-157">Tıklatın **seçenekleri** > **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="ab9b6-158">Girin bir **adı** (örneğin, SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="ab9b6-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="ab9b6-159">Önek *B2C_1A_* anahtarınızı adına otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-159">The prefix *B2C_1A_* is automatically added to the name of your key.</span></span>
    3. <span data-ttu-id="ab9b6-160">Sertifikanızı seçmek için **dosya denetimi karşıya**.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-160">To select your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="ab9b6-161">PowerShell komut dosyasında ayarlanan sertifikanın parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-161">Enter the certificate's password that you set in the PowerShell script.</span></span>
3. <span data-ttu-id="ab9b6-162">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-162">Click **Create**.</span></span>
4. <span data-ttu-id="ab9b6-163">Bir anahtar (örneğin, B2C_1A_SAMLSigningCert) oluşturduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="ab9b6-164">Tam adını not edin (de dahil olmak üzere *B2C_1A_*).</span><span class="sxs-lookup"><span data-stu-id="ab9b6-164">Take note of the full name (including *B2C_1A_*).</span></span> <span data-ttu-id="ab9b6-165">Daha sonra ilkesinde bu anahtara başvurur.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-165">You will refer to this key later in the policy.</span></span>

## <a name="create-the-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="ab9b6-166">Temel ilkenizde Salesforce SAML Talep sağlayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ab9b6-166">Create the Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="ab9b6-167">Kullanıcıların Salesforce kullanarak oturum açabilmeniz için bir talep sağlayıcısı olarak Salesforce tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-167">You need to define Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="ab9b6-168">Diğer bir deyişle, Azure AD B2C ile iletişim kuracak uç noktası belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-168">In other words, you need to specify the endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="ab9b6-169">Uç nokta olacak *sağlamak* bir dizi *talep* , belirli bir kullanıcı kimliği doğrulanmış olduğunu doğrulamak için Azure AD B2C kullanır.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-169">The endpoint will *provide* a set of *claims* that Azure AD B2C uses to verify that a specific user has authenticated.</span></span> <span data-ttu-id="ab9b6-170">Bunu yapmak için ekleyin bir `<ClaimsProvider>` ilkenizin uzantısı dosyasında Salesforce için:</span><span class="sxs-lookup"><span data-stu-id="ab9b6-170">To do this, add a `<ClaimsProvider>` for Salesforce in the extension file of your policy:</span></span>

1. <span data-ttu-id="ab9b6-171">Uzantı dosyası (TrustFrameworkExtensions.xml) çalışma dizininizi açın.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-171">In your working directory, open the extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="ab9b6-172">Bul `<ClaimsProviders>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-172">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="ab9b6-173">Yoksa, kök düğümü altında oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-173">If it does not exist, create it under the root node.</span></span>
3. <span data-ttu-id="ab9b6-174">Yeni bir ekleme `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="ab9b6-174">Add a new `<ClaimsProvider>`:</span></span>

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

<span data-ttu-id="ab9b6-175">Altında `<ClaimsProvider>` düğümü:</span><span class="sxs-lookup"><span data-stu-id="ab9b6-175">Under the `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="ab9b6-176">Değeri değiştirme `<Domain>` ayırt eden benzersiz bir değere `<ClaimsProvider>` diğer kimlik sağlayıcılardan gelen.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-176">Change the value for `<Domain>` to a unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="ab9b6-177">Değeri güncelleştirme `<DisplayName>` talep sağlayıcısı için bir görünen ad için.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-177">Update the value for `<DisplayName>` to a display name for the claims provider.</span></span> <span data-ttu-id="ab9b6-178">Şu anda, bu değer kullanılmıyor.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-178">Currently, this value is not used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="ab9b6-179">Teknik profilini güncelleştir</span><span class="sxs-lookup"><span data-stu-id="ab9b6-179">Update the technical profile</span></span>

<span data-ttu-id="ab9b6-180">Salesforce bir SAML belirtecini almak için Azure AD B2C Azure Active Directory (Azure AD) ile iletişim kurmak için kullanacağınız protokolleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-180">To get a SAML token from Salesforce, define the protocols that Azure AD B2C will use to communicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="ab9b6-181">Bunu yapmak `<TechnicalProfile>` öğesinin `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="ab9b6-181">Do this in the `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="ab9b6-182">Kimliği güncelleştirme `<TechnicalProfile>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-182">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="ab9b6-183">Bu kimliği, bu teknik profili ilkesinin diğer bölümlerden başvurmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-183">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
2. <span data-ttu-id="ab9b6-184">Değeri güncelleştirme `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-184">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="ab9b6-185">Bu değer, oturum açma sayfasında oturum açma düğmesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-185">This value is displayed on the sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="ab9b6-186">Değeri güncelleştirme `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-186">Update the value for `<Description>`.</span></span>
4. <span data-ttu-id="ab9b6-187">Salesforce SAML 2.0 protokolü kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-187">Salesforce uses the SAML 2.0 protocol.</span></span> <span data-ttu-id="ab9b6-188">Değeri emin `<Protocol>` olan **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-188">Ensure that the value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="ab9b6-189">Güncelleştirme `<Metadata>` belirli Salesforce hesabınıza ilişkin ayarları yansıtacak şekilde önceki XML bölümünde.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-189">Update the `<Metadata>` section in the preceding XML to reflect the settings for your specific Salesforce account.</span></span> <span data-ttu-id="ab9b6-190">XML'de, meta veri değerlerini güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="ab9b6-190">In the XML, update the metadata values:</span></span>

1. <span data-ttu-id="ab9b6-191">Değerini güncelleştirmek `<Item Key="PartnerEntity">` daha önce kopyaladığınız Salesforce meta veri URL'si.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-191">Update the value of `<Item Key="PartnerEntity">` with the Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="ab9b6-192">Aşağıdaki biçime sahiptir:</span><span class="sxs-lookup"><span data-stu-id="ab9b6-192">It has the following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="ab9b6-193">İçinde `<CryptographicKeys>` bölümünde, her iki örnekleri için değeri güncelleştirin `StorageReferenceId` imzalama sertifikanızın (örneğin, B2C_1A_SAMLSigningCert) anahtar adını.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-193">In the `<CryptographicKeys>` section, update the value for both instances of `StorageReferenceId` to the name of the key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="ab9b6-194">Doğrulama için uzantı dosyasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="ab9b6-194">Upload the extension file for verification</span></span>

<span data-ttu-id="ab9b6-195">Böylece Azure AD B2C Salesforce ile iletişim kurmak bildiği ilkeniz artık yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-195">Your policy is now configured so that Azure AD B2C knows how to communicate with Salesforce.</span></span> <span data-ttu-id="ab9b6-196">Uzantı dosyası ilkenizin olmadığından sorunları kadar doğrulamak için yüklemeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-196">Try uploading the extension file of your policy, to verify that there aren't any issues so far.</span></span> <span data-ttu-id="ab9b6-197">Uzantı dosyası ilkenizin karşıya yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="ab9b6-197">To upload the extension file of your policy:</span></span>

1. <span data-ttu-id="ab9b6-198">Azure AD B2C kiracınızda Git **tüm ilkeler** dikey.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-198">In your Azure AD B2C tenant, go to the **All Policies** blade.</span></span>
2. <span data-ttu-id="ab9b6-199">Seçin **varsa ilkesi üzerine** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-199">Select the **Overwrite the policy if it exists** check box.</span></span>
3. <span data-ttu-id="ab9b6-200">Uzantı dosyası (TrustFrameworkExtensions.xml) karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-200">Upload the extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="ab9b6-201">Doğrulama başarısız olmayan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-the-salesforce-saml-claims-provider-to-a-user-journey"></a><span data-ttu-id="ab9b6-202">Bir kullanıcı gezisine Salesforce SAML talep sağlayıcısını Kaydet</span><span class="sxs-lookup"><span data-stu-id="ab9b6-202">Register the Salesforce SAML claims provider to a user journey</span></span>

<span data-ttu-id="ab9b6-203">Ardından, Salesforce SAML kimlik sağlayıcısı, kullanıcı Yolculuklar birine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-203">Next, add the Salesforce SAML identity provider to one of your user journeys.</span></span> <span data-ttu-id="ab9b6-204">Bu noktada, kimlik sağlayıcısı ayarlandı, ancak herhangi bir kullanıcı oturum açma veya kaydolma sayfalarını üzerinde kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-204">At this point, the identity provider has been set up, but it’s not available on any of the user sign-up or sign-in pages.</span></span> <span data-ttu-id="ab9b6-205">Bir oturum açma sayfasına kimlik sağlayıcısı eklemek için ilk olarak, var olan bir şablonu kullanıcı gezisine bir kopyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-205">To add the identity provider to a sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="ab9b6-206">Ardından, ayrıca Azure AD kimlik sağlayıcısı sahip olması şablon değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-206">Then, modify the template so that it also has the Azure AD identity provider.</span></span>

1. <span data-ttu-id="ab9b6-207">Temel dosya ilkenizin (örneğin, TrustFrameworkBase.xml) açın.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-207">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="ab9b6-208">Bul `<UserJourneys>` öğesini ve ardından kopyalama tüm `<UserJourney>` değeri, "SignUpOrSignIn" kimliğine dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-208">Find the `<UserJourneys>` element, and then copy the entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="ab9b6-209">Uzantı dosyası (örneğin, TrustFrameworkExtensions.xml) açın.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-209">Open the extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="ab9b6-210">Bul `<UserJourneys>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-210">Find the `<UserJourneys>` element.</span></span> <span data-ttu-id="ab9b6-211">Öğe yoksa, bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-211">If the element doesn't exist, create one.</span></span>
4. <span data-ttu-id="ab9b6-212">Kopyalanan tüm Yapıştır `<UserJourney>` bir alt öğesi olarak `<UserJourneys>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-212">Paste the entire copied `<UserJourney>` as a child of the `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="ab9b6-213">Yeni kimliği yeniden adlandırma `<UserJourney>` (örneğin, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="ab9b6-213">Rename the ID of the new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-the-identity-provider-button"></a><span data-ttu-id="ab9b6-214">Görüntü kimlik sağlayıcısı düğmesi</span><span class="sxs-lookup"><span data-stu-id="ab9b6-214">Display the identity provider button</span></span>

<span data-ttu-id="ab9b6-215">`<ClaimsProviderSelection>` Öğesidir kaydolma veya oturum açma sayfasında bir kimlik sağlayıcısı düğmesini benzer.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-215">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="ab9b6-216">Ekleyerek bir `<ClaimsProviderSelection>` öğesi Salesforce için yeni bir düğme görüntülenir bir kullanıcı bu sayfaya geçtiğinde.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes to this page.</span></span> <span data-ttu-id="ab9b6-217">Kimlik sağlayıcısı düğmesini görüntülemek için:</span><span class="sxs-lookup"><span data-stu-id="ab9b6-217">To display the identity provider button:</span></span>

1. <span data-ttu-id="ab9b6-218">İçinde `<UserJourney>` oluşturduğunuz, Bul `<OrchestrationStep>` ile `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-218">In the `<UserJourney>` that you created, find the `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="ab9b6-219">Aşağıdaki XML ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ab9b6-219">Add the following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="ab9b6-220">Ayarlama `TargetClaimsExchangeId` için mantıksal bir değer.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-220">Set `TargetClaimsExchangeId` to a logical value.</span></span> <span data-ttu-id="ab9b6-221">Aynısına başkalarının aşağıdaki öneririz (örneğin,  *\[ClaimProviderName\]Exchange*).</span><span class="sxs-lookup"><span data-stu-id="ab9b6-221">We recommend following the same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-the-identity-provider-button-to-an-action"></a><span data-ttu-id="ab9b6-222">Kimlik sağlayıcısı düğmesine bir eyleme bağlantı</span><span class="sxs-lookup"><span data-stu-id="ab9b6-222">Link the identity provider button to an action</span></span>

<span data-ttu-id="ab9b6-223">Bir kimlik sağlayıcısı düğmesi yerinde sahip olduğunuza göre bir eyleme bağlantı.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-223">Now that you have an identity provider button in place, link it to an action.</span></span> <span data-ttu-id="ab9b6-224">Bu durumda, bir SAML belirteci almak için Salesforce ile iletişim kurmak Azure AD B2C için eylemdir.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-224">In this case, the action is for Azure AD B2C to communicate with Salesforce to receive a SAML token.</span></span> <span data-ttu-id="ab9b6-225">Teknik profil için Salesforce SAML bağlayarak Talep sağlayıcı bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ab9b6-225">You can do this by linking the technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="ab9b6-226">İçinde `<UserJourney>` düğümünde, bulmak `<OrchestrationStep>` ile `Order="2"`.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-226">In the `<UserJourney>` node, find the `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="ab9b6-227">Aşağıdaki XML ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ab9b6-227">Add the following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="ab9b6-228">Güncelleştirme `Id` daha önce kullandığınız aynı değere `TargetClaimsExchangeId`.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-228">Update `Id` to the same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="ab9b6-229">Güncelleştirme `TechnicalProfileReferenceId` için `Id` teknik daha önce oluşturduğunuz (örneğin, ContosoProfile) profil.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-229">Update `TechnicalProfileReferenceId` to the `Id` of the technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="ab9b6-230">Güncelleştirilmiş uzantı dosyasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="ab9b6-230">Upload the updated extension file</span></span>

<span data-ttu-id="ab9b6-231">Tamamladığınızda uzantısının değiştirme.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-231">You are done modifying the extension file.</span></span> <span data-ttu-id="ab9b6-232">Kaydet ve bu dosyayı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-232">Save and upload this file.</span></span> <span data-ttu-id="ab9b6-233">Tüm Doğrulamalar başarıyla emin olun.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-233">Ensure that all validations succeed.</span></span>

### <a name="update-the-relying-party-file"></a><span data-ttu-id="ab9b6-234">Bağlı olan taraf dosyasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="ab9b6-234">Update the relying party file</span></span>

<span data-ttu-id="ab9b6-235">Ardından, oluşturduğunuz kullanıcı gezisine başlatır bağlı olan taraf (RP) dosyasını güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="ab9b6-235">Next, update the relying party (RP) file that initiates the user journey that you created:</span></span>

1. <span data-ttu-id="ab9b6-236">Çalışma dizininizi SignUpOrSignIn.xml kopyası.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="ab9b6-237">Sonra (örneğin, SignUpOrSignInWithAAD.xml) yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="ab9b6-238">Yeni dosya ve güncelleştirme açmak `PolicyId` için öznitelik `<TrustFrameworkPolicy>` benzersiz bir değere sahip.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-238">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="ab9b6-239">İlkeniz (örneğin, SignUpOrSignInWithAAD) adıdır.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-239">This is the name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="ab9b6-240">Değiştirme `ReferenceId` özniteliğini `<DefaultUserJourney>` eşleşecek şekilde `Id` (örneğin, SignUpOrSignUsingContoso) oluşturulan yeni kullanıcı gezisine biri.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-240">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the `Id` of the new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="ab9b6-241">Yaptığınız değişiklikleri kaydedin ve dosyayı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-241">Save your changes, and then upload the file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="ab9b6-242">Test etme ve sorun giderme</span><span class="sxs-lookup"><span data-stu-id="ab9b6-242">Test and troubleshoot</span></span>

<span data-ttu-id="ab9b6-243">Azure Portalı'nda, yeni karşıya yüklediğiniz, özel ilke sınamak için ilke dikey penceresine gidin ve ardından **Şimdi Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="ab9b6-243">To test the custom policy that you just uploaded, in the Azure portal, go to the policy blade, and then click **Run now**.</span></span> <span data-ttu-id="ab9b6-244">Başarısız olursa bkz [özel ilke sorunlarını giderme](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="ab9b6-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab9b6-245">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ab9b6-245">Next steps</span></span>

<span data-ttu-id="ab9b6-246">Geri bildirim sağlayın [ AADB2CPreview@microsoft.com ](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ab9b6-246">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
