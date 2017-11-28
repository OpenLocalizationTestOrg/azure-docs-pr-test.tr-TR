---
title: "Azure Active Directory B2C: kendi öznitelikleri toocustom ilkeleri ekleyin ve profil düzenleme kullanın | Microsoft Docs"
description: "Uzantısı özellikleri, özel öznitelikleri kullanarak ve bunları hello kullanıcı arabiriminde dahil olmak üzere bir gözden geçirme"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: 8cc9c6a38d7652797ba54a3e02078ac2bf4a693b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a><span data-ttu-id="65e9d-103">Azure Active Directory B2C: İlke oluşturma ve özel bir profilde özel öznitelikleri kullanma Düzenle</span><span class="sxs-lookup"><span data-stu-id="65e9d-103">Azure Active Directory B2C: Creating and using custom attributes in a custom profile edit policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="65e9d-104">Bu makalede, Azure AD B2C dizininizde özel bir öznitelik oluşturma ve bu yeni öznitelik özel talep hello profil düzenleme kullanıcı gezisine de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65e9d-104">In this article, you create a custom attribute in your Azure AD B2C directory and use this new attribute as a custom claim in hello profile edit user journey.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65e9d-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="65e9d-105">Prerequisites</span></span>

<span data-ttu-id="65e9d-106">Tam hello hello makaledeki adımları [özel ilkeleri ile çalışmaya başlama](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="65e9d-106">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a><span data-ttu-id="65e9d-107">Özel öznitelikler toocollect bilgileri müşterilerinizin Azure Active Directory B2C içinde özel ilkelerini kullanma hakkında kullanın</span><span class="sxs-lookup"><span data-stu-id="65e9d-107">Use custom attributes toocollect information about your customers in Azure Active Directory B2C using custom policies</span></span>
<span data-ttu-id="65e9d-108">Azure Active Directory (Azure AD) B2C dizininize yerleşik bir öznitelikler kümesi ile birlikte gelir: ad, Soyadı, şehir, posta kodu, userPrincipalName verildiğinde, vb..  Genellikle kendi öznitelikleri toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="65e9d-108">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of attributes: Given Name, Surname, City, Postal Code, userPrincipalName, etc.  You often need toocreate your own attributes.</span></span>  <span data-ttu-id="65e9d-109">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="65e9d-109">For example:</span></span>
* <span data-ttu-id="65e9d-110">Toopersist "LoyaltyNumber." gibi bir öznitelik bir müşteri dönük uygulaması gerekiyor</span><span class="sxs-lookup"><span data-stu-id="65e9d-110">A customer-facing application needs toopersist an attribute such as "LoyaltyNumber."</span></span>
* <span data-ttu-id="65e9d-111">Bir kimlik sağlayıcısı "uniqueUserGUID" gibi kaydedilmelidir benzersiz kullanıcı tanımlayıcısı var"</span><span class="sxs-lookup"><span data-stu-id="65e9d-111">An identity provider has a unique user identifier that must be saved such as "uniqueUserGUID.""</span></span>
* <span data-ttu-id="65e9d-112">Özel kullanıcı gezisine toopersist hello "migrationStatus." gibi kullanıcı durumunun gerekiyor</span><span class="sxs-lookup"><span data-stu-id="65e9d-112">A custom user journey needs toopersist hello state of user such as "migrationStatus."</span></span>

<span data-ttu-id="65e9d-113">Azure AD B2C ile her kullanıcı hesabında depolanan öznitelikler hello kümesi genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65e9d-113">With Azure AD B2C, you can extend hello set of attributes stored on each user account.</span></span> <span data-ttu-id="65e9d-114">Aynı zamanda okuma ve hello kullanarak bu öznitelikler yazma [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="65e9d-114">You can also read and write these attributes by using hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

<span data-ttu-id="65e9d-115">Uzantısı özellikleri hello Directory'deki hello kullanıcı nesnelerini hello şemasını.</span><span class="sxs-lookup"><span data-stu-id="65e9d-115">Extension properties extend hello schema of hello user objects in hello directory.</span></span>  <span data-ttu-id="65e9d-116">Hello koşulları uzantı özelliği, özel öznitelik ve özel talep aynısını bu makalede ve hello ad hello bağlamında hello bağlam (uygulama, nesne, ilke) bağlı olarak değişir toohello bakın.</span><span class="sxs-lookup"><span data-stu-id="65e9d-116">hello terms extension property, custom attribute and custom claim refer toohello same thing in hello context of this article and hello name varies depending on hello context (application, object, policy).</span></span>

<span data-ttu-id="65e9d-117">Bir kullanıcı için verileri içerebilir olsa bile uzantısı özellikleri yalnızca bir uygulama nesnesinde kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="65e9d-117">Extension properties can only be registered on an Application object even though they may contain data for a User.</span></span> <span data-ttu-id="65e9d-118">Merhaba, ekli toohello uygulama özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="65e9d-118">hello property is attached toohello application.</span></span> <span data-ttu-id="65e9d-119">Merhaba uygulama nesnesi yazma erişim izni verilsin tooregister bir uzantı özelliği olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="65e9d-119">hello Application object must be granted write access tooregister an extension property.</span></span> <span data-ttu-id="65e9d-120">(Arasında tüm türleri ve tüm uygulamalar) 100 uzantısı özellikleri tooany tek nesne yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="65e9d-120">100 Extension properties (across ALL types and ALL applications) can be written tooany single object.</span></span> <span data-ttu-id="65e9d-121">Uzantısı özellikleri toohello hedef dizin türü eklenir ve hello Azure AD B2C dizini kiracısında hemen erişilebilir hale gelir.</span><span class="sxs-lookup"><span data-stu-id="65e9d-121">Extension properties are added toohello target directory type and becomes immediately accessible in hello Azure AD B2C directory tenant.</span></span>
<span data-ttu-id="65e9d-122">Merhaba uygulaması silinirse, tüm kullanıcılar için içerdikleri herhangi bir veri yanı sıra bu uzantısı özellikleri de kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="65e9d-122">If hello application is deleted, those Extension properties along with any data contained in them for all users are also removed.</span></span> <span data-ttu-id="65e9d-123">Uzantı özelliği hello uygulama tarafından silinirse, üzerinde hello kaldırılmadan dizin nesneleri hedefleyen ve hello değerleri silindi.</span><span class="sxs-lookup"><span data-stu-id="65e9d-123">If an extension property is deleted by hello Application, it is removed on hello target directory objects, and hello values deleted.</span></span>

<span data-ttu-id="65e9d-124">Uzantısı özellikleri yalnızca hello Kiracı kayıtlı bir uygulamada Merhaba içeriğine bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="65e9d-124">Extension properties exist only in hello context of a registered  Application in hello tenant.</span></span> <span data-ttu-id="65e9d-125">Bu uygulamanın Hello nesne kimliği hello kullanmak TechnicalProfile eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="65e9d-125">hello object id of that Application must be included in hello TechnicalProfile that use it.</span></span>

>[!NOTE]
><span data-ttu-id="65e9d-126">Hello Azure AD B2C dizini genellikle adlı bir Web uygulaması içeren `b2c-extensions-app`.</span><span class="sxs-lookup"><span data-stu-id="65e9d-126">hello Azure AD B2C directory typically includes a Web App named `b2c-extensions-app`.</span></span>  <span data-ttu-id="65e9d-127">Bu uygulama, öncelikle hello Azure portal oluşturulan hello özel talepler için hello b2c yerleşik ilkeleri tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="65e9d-127">This application is primarily used by hello b2c built-in  policies for hello custom claims created via hello Azure portal.</span></span>  <span data-ttu-id="65e9d-128">Bu uygulama tooregister uzantıları için özel ilkeler b2c kullanarak yalnızca ileri düzey kullanıcıların yapması önerilir.</span><span class="sxs-lookup"><span data-stu-id="65e9d-128">Using this application tooregister extensions for b2c custom policies is recommended only for advanced users.</span></span>  <span data-ttu-id="65e9d-129">Bunun için yönergeler hello bu makalenin sonraki adımlar bölümüne dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="65e9d-129">Instructions for this are included in hello Next Steps section in this article.</span></span>


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a><span data-ttu-id="65e9d-130">Yeni bir uygulama toostore hello uzantısı özellikleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="65e9d-130">Creating a new application toostore hello extension properties</span></span>

1. <span data-ttu-id="65e9d-131">Bir tarayıcı oturumu açın ve toohello gidin [Azure Portalı hakkında](https://portal.azure.com) hello B2C tooconfigure istediğiniz dizini, yönetici kimlik bilgileriyle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="65e9d-131">Open a browsing session and navigate toohello [Azure porta](https://portal.azure.com) and sign in with administrative credentials of hello B2C Directory you wish tooconfigure.</span></span>
1. <span data-ttu-id="65e9d-132">Tıklatın **Azure Active Directory** hello sol gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="65e9d-132">Click **Azure Active Directory** on hello left navigation menu.</span></span> <span data-ttu-id="65e9d-133">Bunu seçerek daha Hizmetleri toofind gerekebilir >.</span><span class="sxs-lookup"><span data-stu-id="65e9d-133">You may need toofind it by selecting More services>.</span></span>
1. <span data-ttu-id="65e9d-134">Seçin **uygulama kayıtlar** tıklatıp **yeni uygulama kaydı**</span><span class="sxs-lookup"><span data-stu-id="65e9d-134">Select **App registrations** and click **New application registration**</span></span>
1. <span data-ttu-id="65e9d-135">Merhaba aşağıdaki girişleri önerilen sağlar:</span><span class="sxs-lookup"><span data-stu-id="65e9d-135">Provide hello following recommended entries:</span></span>
  * <span data-ttu-id="65e9d-136">Merhaba web uygulaması için bir ad belirtin: **WebApp GraphAPI DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="65e9d-136">Specify a name for hello web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
  * <span data-ttu-id="65e9d-137">Uygulama türü: Web app/API</span><span class="sxs-lookup"><span data-stu-id="65e9d-137">Application type: Web app/API</span></span>
  * <span data-ttu-id="65e9d-138">Oturum açma URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="65e9d-138">Sign-on URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span></span>
1. <span data-ttu-id="65e9d-139">Seçin ** oluşturun.</span><span class="sxs-lookup"><span data-stu-id="65e9d-139">Select **Create.</span></span> <span data-ttu-id="65e9d-140">Başarılı bir şekilde tamamlandığında görünür hello **bildirimleri**</span><span class="sxs-lookup"><span data-stu-id="65e9d-140">Successful completion appears in hello **notifications**</span></span>
1. <span data-ttu-id="65e9d-141">Yeni oluşturulan hello web uygulaması seçin: **WebApp GraphAPI DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="65e9d-141">Select hello newly created web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
1. <span data-ttu-id="65e9d-142">Select ayarları: **gerekli izinler**</span><span class="sxs-lookup"><span data-stu-id="65e9d-142">Select Settings: **Required permissions**</span></span>
1. <span data-ttu-id="65e9d-143">API seçin **Windows Active Directory**</span><span class="sxs-lookup"><span data-stu-id="65e9d-143">Select API **Windows Active Directory**</span></span>
1. <span data-ttu-id="65e9d-144">Uygulama izinleri bir onay işareti koyun: **dizin verilerini okuma ve yazma**, ve **Kaydet**</span><span class="sxs-lookup"><span data-stu-id="65e9d-144">Place a checkmark in Application Permissions: **Read and write directory data**, and **Save**</span></span>
1. <span data-ttu-id="65e9d-145">Seçin **izinleri verin** ve onaylayın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="65e9d-145">Choose **Grant permissions** and confirm **Yes**.</span></span>
1. <span data-ttu-id="65e9d-146">Tooyour panoya kopyalayın ve GraphAPI WebApp DirectoryExtensions tanımlayıcıları aşağıdaki hello kaydedin > Ayarlar > Özellikler ></span><span class="sxs-lookup"><span data-stu-id="65e9d-146">Copy tooyour clipboard and save hello following identifiers from WebApp-GraphAPI-DirectoryExtensions>Settings>Properties></span></span>
*  <span data-ttu-id="65e9d-147">**Uygulama Kimliği** .</span><span class="sxs-lookup"><span data-stu-id="65e9d-147">**Application ID** .</span></span> <span data-ttu-id="65e9d-148">Örnek:`103ee0e6-f92d-4183-b576-8c3739027780`</span><span class="sxs-lookup"><span data-stu-id="65e9d-148">Example: `103ee0e6-f92d-4183-b576-8c3739027780`</span></span>
* <span data-ttu-id="65e9d-149">**Nesne Kimliği**.</span><span class="sxs-lookup"><span data-stu-id="65e9d-149">**Object ID**.</span></span> <span data-ttu-id="65e9d-150">Örnek:`80d8296a-da0a-49ee-b6ab-fd232aa45201`</span><span class="sxs-lookup"><span data-stu-id="65e9d-150">Example: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span></span>



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a><span data-ttu-id="65e9d-151">Özel ilke tooadd hello ApplicationObjectId değiştirme</span><span class="sxs-lookup"><span data-stu-id="65e9d-151">Modifying your custom policy tooadd hello ApplicationObjectId</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item>
                <Item Key="ClientId">insert appId here</Item>
              </Metadata>
            <!-- End of changes -->
              <CryptographicKeys>
                <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
              </CryptographicKeys>
              <IncludeInSso>false</IncludeInSso>
              <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
            </TechnicalProfile>
        </ClaimsProvider>
    </ClaimsProviders>
```

>[!NOTE]
><span data-ttu-id="65e9d-152">Merhaba <TechnicalProfile Id="AAD-Common"> öğeleri dahil ve tüm hello Azure Active Directory TechnicalProfiles hello öğesini kullanarak yeniden başvurulan tooas "ortak" nedeni:`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span><span class="sxs-lookup"><span data-stu-id="65e9d-152">hello <TechnicalProfile Id="AAD-Common"> is referred tooas "common" because its elements are included in and reused in all hello Azure Active Directory TechnicalProfiles by using hello element: `<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span></span>

>[!NOTE]
><span data-ttu-id="65e9d-153">Merhaba TechnicalProfile hello ilk zaman yeni oluşturulan toohello uzantı özelliği için yazdığında, tek seferlik bir hatayla karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65e9d-153">When hello TechnicalProfile writes for hello first time toohello newly created extension property, you may experience a one-time error.</span></span>  <span data-ttu-id="65e9d-154">Merhaba uzantı özelliği ilk kez kullanıldığı hello oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="65e9d-154">hello extension property is created hello first time it is used.</span></span>  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a><span data-ttu-id="65e9d-155">Merhaba yeni uzantı özelliği kullanılarak / özel bir kullanıcı gezisine özniteliği</span><span class="sxs-lookup"><span data-stu-id="65e9d-155">Using hello new extension property / custom attribute in a user journey</span></span>


1. <span data-ttu-id="65e9d-156">Açık hello ilkeniz açıklayan bağlı olan Party(RP) dosyasının kullanıcı gezisine düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="65e9d-156">Open hello Relying Party(RP) file that describes your policy edit user journey.</span></span>  <span data-ttu-id="65e9d-157">Başlıyorsanız, önceden yapılandırılmış hello RP PolicyEdit sürümünüz dosya hello hello Azure portalında Azure B2C özel İlkesi bölümünde doğrudan önerilir toodownload olabilir.</span><span class="sxs-lookup"><span data-stu-id="65e9d-157">If you are starting out, it may be advisable toodownload your already configured version of hello RP-PolicyEdit file directly from hello Azure B2C Custom Policy section in hello Azure portal.</span></span>  <span data-ttu-id="65e9d-158">Alternatif olarak, depolama klasörünüzden XML dosyanızı açın.</span><span class="sxs-lookup"><span data-stu-id="65e9d-158">Alternatively, open your XML file from your storage folder.</span></span>
2. <span data-ttu-id="65e9d-159">Bir özel talep eklemek `loyaltyId`.</span><span class="sxs-lookup"><span data-stu-id="65e9d-159">Add a custom claim `loyaltyId`.</span></span>  <span data-ttu-id="65e9d-160">Merhaba özel dahil ederek hello talep `<RelyingParty>` öğesi, bir parametre toohello UserJourney TechnicalProfiles geçirilen ve Merhaba uygulaması için hello belirteci dahil.</span><span class="sxs-lookup"><span data-stu-id="65e9d-160">By including hello custom claim in hello `<RelyingParty>` element, it is passed as a parameter toohello UserJourney TechnicalProfiles and included in hello token for hello application.</span></span>
```xml
<RelyingParty>
   <DefaultUserJourney ReferenceId="ProfileEdit" />
   <TechnicalProfile Id="PolicyProfile">
     <DisplayName>PolicyProfile</DisplayName>
     <Protocol Name="OpenIdConnect" />
     <OutputClaims>
       <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
       <OutputClaim ClaimTypeReferenceId="city" />

       <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />

     </OutputClaims>
     <SubjectNamingInfo ClaimType="sub" />
   </TechnicalProfile>
 </RelyingParty>
 ```
3. <span data-ttu-id="65e9d-161">Bir talep tanımı toohello uzantı ilke dosyası ekleme `TrustFrameworkExtensions.xml` hello içinde `<ClaimsSchema>` gösterildiği gibi öğesi.</span><span class="sxs-lookup"><span data-stu-id="65e9d-161">Add a claim definition toohello Extension policy file  `TrustFrameworkExtensions.xml` inside hello `<ClaimsSchema>` element as shown.</span></span>
```xml
<ClaimsSchema>
        <ClaimType Id="extension_loyaltyId">
            <DisplayName>Loyalty Identification Tag</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your loyalty number from your membership card</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
</ClaimsSchema>
```
4. <span data-ttu-id="65e9d-162">Merhaba eklemek aynı tanımı toohello temel ilke dosyası talep `TrustFrameworkBase.xml`.</span><span class="sxs-lookup"><span data-stu-id="65e9d-162">Add hello same claim definition toohello Base policy file `TrustFrameworkBase.xml`.</span></span>  
><span data-ttu-id="65e9d-163">Ekleme bir `ClaimType` hello temel ve hello uzantıları dosya tanımında normalde gerekli değildir, ancak hello sonraki adımlar hello temel dosyasında hello extension_loyaltyId tooTechnicalProfiles ekleyeceksiniz beri hello İlkesi Doğrulayıcı hello karşıya yükleme reddeder temel dosyası Hello olmadan.</span><span class="sxs-lookup"><span data-stu-id="65e9d-163">Adding a `ClaimType` definition in both hello base and hello extensions file is normally not necessary, however since hello next steps will add hello extension_loyaltyId tooTechnicalProfiles in hello Base file, hello policy validator will reject hello upload of hello base file without it.</span></span>
><span data-ttu-id="65e9d-164">Merhaba TrustFrameworkBase.xml dosyasındaki "ProfileEdit" adlı hello kullanıcı gezisine yararlı tootrace hello yürütülmesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="65e9d-164">It may be useful tootrace hello execution of hello user journey named "ProfileEdit" in hello TrustFrameworkBase.xml file.</span></span>  <span data-ttu-id="65e9d-165">Merhaba kullanıcı gezisine aynı adı düzenleyicinizde ve Orchestration adım 5'hello TechnicalProfileReferenceID çağırır uyun Merhaba, Ara "SelfAsserted-ProfileUpdate" =.</span><span class="sxs-lookup"><span data-stu-id="65e9d-165">Search for hello user journey of hello same name in your editor and observe that Orchestration Step 5 invokes hello TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate".</span></span>  <span data-ttu-id="65e9d-166">Arama ve bu TechnicalProfile toofamiliarize kendiniz hello akışla inceleyin.</span><span class="sxs-lookup"><span data-stu-id="65e9d-166">Search and inspect this TechnicalProfile toofamiliarize yourself with hello flow.</span></span>
5. <span data-ttu-id="65e9d-167">Giriş ve çıkış hello TechnicalProfile "SelfAsserted-ProfileUpdate" talebi olarak loyaltyId Ekle</span><span class="sxs-lookup"><span data-stu-id="65e9d-167">Add loyaltyId as input and output claim in hello TechnicalProfile "SelfAsserted-ProfileUpdate"</span></span>
```xml
<TechnicalProfile Id="SelfAsserted-ProfileUpdate">
          <DisplayName>User ID signup</DisplayName>
          <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
          <Metadata>
            <Item Key="ContentDefinitionReferenceId">api.selfasserted.profileupdate</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>

            <InputClaim ClaimTypeReferenceId="alternativeSecurityId" />
            <InputClaim ClaimTypeReferenceId="userPrincipalName" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. <span data-ttu-id="65e9d-168">Talep TechnicalProfile "AAD-UserWriteProfileUsingObjectId" toopersist hello hello dizininde hello geçerli kullanıcı için hello uzantısı özelliğinde hello talebin değerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="65e9d-168">Add claim in TechnicalProfile "AAD-UserWriteProfileUsingObjectId" toopersist hello value of hello claim in hello extension property, for hello current user in hello directory.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteProfileUsingObjectId">
          <Metadata>
            <Item Key="Operation">Write</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">false</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
          </InputClaims>
          <PersistedClaims>
            <!-- Required claims -->
            <PersistedClaim ClaimTypeReferenceId="objectId" />

            <!-- Optional claims -->
            <PersistedClaim ClaimTypeReferenceId="givenName" />
            <PersistedClaim ClaimTypeReferenceId="surname" />
            <PersistedClaim ClaimTypeReferenceId="extension_loyaltyId" />

          </PersistedClaims>
          <IncludeTechnicalProfile ReferenceId="AAD-Common" />
        </TechnicalProfile>
```
7. <span data-ttu-id="65e9d-169">Bir kullanıcı oturum açtığında her zaman talep TechnicalProfile "AAD-UserReadUsingObjectId" tooread hello değerini hello uzantısı özniteliğinin ekleyin.</span><span class="sxs-lookup"><span data-stu-id="65e9d-169">Add claim in TechnicalProfile "AAD-UserReadUsingObjectId" tooread hello value of hello extension attribute every time a user logs in.</span></span> <span data-ttu-id="65e9d-170">Bugüne kadarki hello TechnicalProfiles değiştirilmiş yalnızca yerel hesaplar hello akışında.</span><span class="sxs-lookup"><span data-stu-id="65e9d-170">Thus far hello TechnicalProfiles have been changed in hello flow of local accounts only.</span></span>  <span data-ttu-id="65e9d-171">Merhaba yeni öznitelik bir sosyal ve Federasyon hesabı hello akışında istenirse, TechnicalProfiles farklı bir dizi değiştirilen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="65e9d-171">If hello new attribute is desired in hello flow of a social/federated account, a different set of TechnicalProfiles needs toobe changed.</span></span> <span data-ttu-id="65e9d-172">Sonraki adımlara bakın.</span><span class="sxs-lookup"><span data-stu-id="65e9d-172">See Next Steps.</span></span>

```xml
<!-- hello following technical profile is used tooread data after user authenticates. -->
     <TechnicalProfile Id="AAD-UserReadUsingObjectId">
       <Metadata>
         <Item Key="Operation">Read</Item>
         <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
       </Metadata>
       <IncludeInSso>false</IncludeInSso>
       <InputClaims>
         <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
       </InputClaims>
       <OutputClaims>
         <!-- Optional claims -->
         <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
         <OutputClaim ClaimTypeReferenceId="displayName" />
         <OutputClaim ClaimTypeReferenceId="otherMails" />
         <OutputClaim ClaimTypeReferenceId="givenName" />
         <OutputClaim ClaimTypeReferenceId="surname" />
         <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />
       </OutputClaims>
       <IncludeTechnicalProfile ReferenceId="AAD-Common" />
     </TechnicalProfile>
```


>[!IMPORTANT]
><span data-ttu-id="65e9d-173">Merhaba IncludeTechnicalProfile öğesi AAD ortak toothis TechnicalProfile tüm hello öğelerine ekler.</span><span class="sxs-lookup"><span data-stu-id="65e9d-173">hello IncludeTechnicalProfile element adds all hello elements of AAD-Common toothis TechnicalProfile.</span></span>

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="65e9d-174">"Şimdi Çalıştır" kullanarak test hello özel İlkesi</span><span class="sxs-lookup"><span data-stu-id="65e9d-174">Test hello custom policy using "Run Now"</span></span>
1. <span data-ttu-id="65e9d-175">Açık hello **Azure AD B2C dikey** ve çok gidin**kimlik deneyimi Framework > özel ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="65e9d-175">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
1. <span data-ttu-id="65e9d-176">Karşıya yüklediğiniz hello özel ilkesini seçin ve hello tıklayın **Şimdi Çalıştır** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="65e9d-176">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
1. <span data-ttu-id="65e9d-177">Bir e-posta adresi kullanarak yukarı mümkün toosign olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="65e9d-177">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="65e9d-178">Merhaba kimliği belirteci tooyour uygulama tarafından extension_loyaltyId öncesinde bir özel talep olarak hello yeni uzantı özelliği içerir geri gönderilir.</span><span class="sxs-lookup"><span data-stu-id="65e9d-178">hello  id token sent back tooyour application includes hello new extension property as a custom claim preceded by extension_loyaltyId.</span></span> <span data-ttu-id="65e9d-179">Örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="65e9d-179">See example.</span></span>

```
{
  "exp": 1493585187,
  "nbf": 1493581587,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493581587,
  "auth_time": 1493581587,
  "extension_loyaltyId": "abc",
  "city": "Redmond"
}
```

## <a name="next-steps"></a><span data-ttu-id="65e9d-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="65e9d-180">Next steps</span></span>

<span data-ttu-id="65e9d-181">Merhaba yeni talep toohello akışları sosyal hesap oturum açma TechnicalProfiles listelenen hello değiştirerek ekleyin.</span><span class="sxs-lookup"><span data-stu-id="65e9d-181">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed.</span></span> <span data-ttu-id="65e9d-182">Bu iki TechnicalProfiles sosyal ve Federasyon hesap oturumu açma toowrite tarafından kullanılan ve hello kullanıcı nesnesinin Bulucu hello gibi hello alternativeSecurityId kullanılarak hello kullanıcı verilerini okur.</span><span class="sxs-lookup"><span data-stu-id="65e9d-182">These two TechnicalProfiles are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator of hello user object.</span></span>
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

<span data-ttu-id="65e9d-183">Merhaba yerleşik ve özel ilkeleri arasında aynı uzantı öznitelikleri kullanma.</span><span class="sxs-lookup"><span data-stu-id="65e9d-183">Using hello same extension attributes between built-in and custom policies.</span></span>
<span data-ttu-id="65e9d-184">Merhaba portal deneyimi uzantı öznitelikleri (diğer adıyla özel öznitelikleri) eklediğinizde, özniteliklerle hello kullanarak kayıtlı ** b2c uzantıları-her b2c kiracınızda bulunan uygulama.</span><span class="sxs-lookup"><span data-stu-id="65e9d-184">When you add extension attributes (aka custom attributes) via hello portal experience, those attributes are registered using hello **b2c-extensions-app that exists in every b2c tenant.</span></span>  <span data-ttu-id="65e9d-185">toouse özel ilkenizde bu uzantı öznitelikleri:</span><span class="sxs-lookup"><span data-stu-id="65e9d-185">toouse these extension attributes in your custom policy:</span></span>
1. <span data-ttu-id="65e9d-186">Portal.Azure.com b2c kiracısına içinde çok gidin**Azure Active Directory** seçip **uygulama kayıtlar**</span><span class="sxs-lookup"><span data-stu-id="65e9d-186">Within your b2c tenant in portal.azure.com, navigate too**Azure Active Directory** and select **App registrations**</span></span>
2. <span data-ttu-id="65e9d-187">Bulma, **b2c uzantıları uygulaması** ve seçin</span><span class="sxs-lookup"><span data-stu-id="65e9d-187">Find your **b2c-extensions-app** and select it</span></span>
3. <span data-ttu-id="65e9d-188">'Essentials' kaydı hello altında **uygulama kimliği** ve hello **nesne kimliği**</span><span class="sxs-lookup"><span data-stu-id="65e9d-188">Under 'Essentials' record hello **Application ID** and hello **Object ID**</span></span>
4. <span data-ttu-id="65e9d-189">Bunları AAD genel teknik, profil meta verileri gibi aşağıdaki gibi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="65e9d-189">Include them in your AAD-Common Technical profile metadata like as follows:</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is hello "Object ID" from hello "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is hello "Application ID" from hello "b2c-extensions-app"-->
              </Metadata>
```

<span data-ttu-id="65e9d-190">Merhaba portal deneyim tookeep tutarlılık oluşturmanıza hello portalı kullanıcı arabirimini kullanarak bu öznitelikler *önce* , özel ilkelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="65e9d-190">tookeep consistency with hello portal experience, create these attributes using hello portal UI *before* you use them in your custom policies.</span></span>  <span data-ttu-id="65e9d-191">Bir öznitelik "ActivationStatus" Merhaba Portalı'nda oluşturduğunuzda, tooit gibi başvurması gerekir:</span><span class="sxs-lookup"><span data-stu-id="65e9d-191">When you create an attribute "ActivationStatus" in hello portal, you must refer tooit as follows:</span></span>

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a><span data-ttu-id="65e9d-192">Başvuru</span><span class="sxs-lookup"><span data-stu-id="65e9d-192">Reference</span></span>

* <span data-ttu-id="65e9d-193">A **teknik profil (TP)** , olarak düşünülebilir bir öğe türü bir *işlevi* bir uç noktanın adı, meta verilerini, protokol tanımlar ve ayrıntıları hello exchange kimlik hello talepler Deneyimi Framework gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="65e9d-193">A **Technical Profile (TP)** is an element type that can be thought of as a *function* that defines an endpoint’s name, its metadata, its protocol, and details hello exchange of claims that hello Identity Experience Framework should perform.</span></span>  <span data-ttu-id="65e9d-194">Zaman bu *işlevi* orchestration adım veya başka bir TechnicalProfile, hello InputClaims ve OutputClaims sağlanan parametre olarak hello çağıran tarafından çağrılır.</span><span class="sxs-lookup"><span data-stu-id="65e9d-194">When this *function* is called in an orchestration step or from another TechnicalProfile, hello InputClaims and OutputClaims are provided as parameters by hello caller.</span></span>


* <span data-ttu-id="65e9d-195">Uzantısı özelliklerindeki tam işleme için hello makalesine bakın [DIRECTORY şema UZANTILARI | GRAFİK API'Sİ KAVRAMLARI](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span><span class="sxs-lookup"><span data-stu-id="65e9d-195">For full treatment on extension properties, see hello article [DIRECTORY SCHEMA EXTENSIONS | GRAPH API CONCEPTS](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span></span>

>[!NOTE]
><span data-ttu-id="65e9d-196">Grafik API'si uzantı öznitelikleri hello kural kullanılarak adlandırılması `extension_ApplicationObjectID_attributename`.</span><span class="sxs-lookup"><span data-stu-id="65e9d-196">Extension attributes in Graph API are named using hello convention `extension_ApplicationObjectID_attributename`.</span></span> <span data-ttu-id="65e9d-197">Özel ilkeler, extension_attributename, böylece hello XML hello ApplicationObjectId atlama olarak tooextensions öznitelikleri bakın.</span><span class="sxs-lookup"><span data-stu-id="65e9d-197">Custom policies refer tooextensions attributes as extension_attributename, thus omitting hello ApplicationObjectId in hello XML</span></span>
