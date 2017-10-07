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
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a>Azure Active Directory B2C: İlke oluşturma ve özel bir profilde özel öznitelikleri kullanma Düzenle

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Bu makalede, Azure AD B2C dizininizde özel bir öznitelik oluşturma ve bu yeni öznitelik özel talep hello profil düzenleme kullanıcı gezisine de kullanabilirsiniz.

## <a name="prerequisites"></a>Ön koşullar

Tam hello hello makaledeki adımları [özel ilkeleri ile çalışmaya başlama](active-directory-b2c-get-started-custom.md).

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a>Özel öznitelikler toocollect bilgileri müşterilerinizin Azure Active Directory B2C içinde özel ilkelerini kullanma hakkında kullanın
Azure Active Directory (Azure AD) B2C dizininize yerleşik bir öznitelikler kümesi ile birlikte gelir: ad, Soyadı, şehir, posta kodu, userPrincipalName verildiğinde, vb..  Genellikle kendi öznitelikleri toocreate gerekir.  Örneğin:
* Toopersist "LoyaltyNumber." gibi bir öznitelik bir müşteri dönük uygulaması gerekiyor
* Bir kimlik sağlayıcısı "uniqueUserGUID" gibi kaydedilmelidir benzersiz kullanıcı tanımlayıcısı var"
* Özel kullanıcı gezisine toopersist hello "migrationStatus." gibi kullanıcı durumunun gerekiyor

Azure AD B2C ile her kullanıcı hesabında depolanan öznitelikler hello kümesi genişletebilirsiniz. Aynı zamanda okuma ve hello kullanarak bu öznitelikler yazma [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).

Uzantısı özellikleri hello Directory'deki hello kullanıcı nesnelerini hello şemasını.  Hello koşulları uzantı özelliği, özel öznitelik ve özel talep aynısını bu makalede ve hello ad hello bağlamında hello bağlam (uygulama, nesne, ilke) bağlı olarak değişir toohello bakın.

Bir kullanıcı için verileri içerebilir olsa bile uzantısı özellikleri yalnızca bir uygulama nesnesinde kaydedilebilir. Merhaba, ekli toohello uygulama özelliğidir. Merhaba uygulama nesnesi yazma erişim izni verilsin tooregister bir uzantı özelliği olmalıdır. (Arasında tüm türleri ve tüm uygulamalar) 100 uzantısı özellikleri tooany tek nesne yazılabilir. Uzantısı özellikleri toohello hedef dizin türü eklenir ve hello Azure AD B2C dizini kiracısında hemen erişilebilir hale gelir.
Merhaba uygulaması silinirse, tüm kullanıcılar için içerdikleri herhangi bir veri yanı sıra bu uzantısı özellikleri de kaldırılır. Uzantı özelliği hello uygulama tarafından silinirse, üzerinde hello kaldırılmadan dizin nesneleri hedefleyen ve hello değerleri silindi.

Uzantısı özellikleri yalnızca hello Kiracı kayıtlı bir uygulamada Merhaba içeriğine bulunmaktadır. Bu uygulamanın Hello nesne kimliği hello kullanmak TechnicalProfile eklenmesi gerekir.

>[!NOTE]
>Hello Azure AD B2C dizini genellikle adlı bir Web uygulaması içeren `b2c-extensions-app`.  Bu uygulama, öncelikle hello Azure portal oluşturulan hello özel talepler için hello b2c yerleşik ilkeleri tarafından kullanılır.  Bu uygulama tooregister uzantıları için özel ilkeler b2c kullanarak yalnızca ileri düzey kullanıcıların yapması önerilir.  Bunun için yönergeler hello bu makalenin sonraki adımlar bölümüne dahil edilir.


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a>Yeni bir uygulama toostore hello uzantısı özellikleri oluşturma

1. Bir tarayıcı oturumu açın ve toohello gidin [Azure Portalı hakkında](https://portal.azure.com) hello B2C tooconfigure istediğiniz dizini, yönetici kimlik bilgileriyle oturum açın.
1. Tıklatın **Azure Active Directory** hello sol gezinti menüsünde. Bunu seçerek daha Hizmetleri toofind gerekebilir >.
1. Seçin **uygulama kayıtlar** tıklatıp **yeni uygulama kaydı**
1. Merhaba aşağıdaki girişleri önerilen sağlar:
  * Merhaba web uygulaması için bir ad belirtin: **WebApp GraphAPI DirectoryExtensions**
  * Uygulama türü: Web app/API
  * Oturum açma URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions
1. Seçin ** oluşturun. Başarılı bir şekilde tamamlandığında görünür hello **bildirimleri**
1. Yeni oluşturulan hello web uygulaması seçin: **WebApp GraphAPI DirectoryExtensions**
1. Select ayarları: **gerekli izinler**
1. API seçin **Windows Active Directory**
1. Uygulama izinleri bir onay işareti koyun: **dizin verilerini okuma ve yazma**, ve **Kaydet**
1. Seçin **izinleri verin** ve onaylayın **Evet**.
1. Tooyour panoya kopyalayın ve GraphAPI WebApp DirectoryExtensions tanımlayıcıları aşağıdaki hello kaydedin > Ayarlar > Özellikler >
*  **Uygulama Kimliği** . Örnek:`103ee0e6-f92d-4183-b576-8c3739027780`
* **Nesne Kimliği**. Örnek:`80d8296a-da0a-49ee-b6ab-fd232aa45201`



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a>Özel ilke tooadd hello ApplicationObjectId değiştirme

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
>Merhaba <TechnicalProfile Id="AAD-Common"> öğeleri dahil ve tüm hello Azure Active Directory TechnicalProfiles hello öğesini kullanarak yeniden başvurulan tooas "ortak" nedeni:`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`

>[!NOTE]
>Merhaba TechnicalProfile hello ilk zaman yeni oluşturulan toohello uzantı özelliği için yazdığında, tek seferlik bir hatayla karşılaşabilirsiniz.  Merhaba uzantı özelliği ilk kez kullanıldığı hello oluşturulur.  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a>Merhaba yeni uzantı özelliği kullanılarak / özel bir kullanıcı gezisine özniteliği


1. Açık hello ilkeniz açıklayan bağlı olan Party(RP) dosyasının kullanıcı gezisine düzenleyin.  Başlıyorsanız, önceden yapılandırılmış hello RP PolicyEdit sürümünüz dosya hello hello Azure portalında Azure B2C özel İlkesi bölümünde doğrudan önerilir toodownload olabilir.  Alternatif olarak, depolama klasörünüzden XML dosyanızı açın.
2. Bir özel talep eklemek `loyaltyId`.  Merhaba özel dahil ederek hello talep `<RelyingParty>` öğesi, bir parametre toohello UserJourney TechnicalProfiles geçirilen ve Merhaba uygulaması için hello belirteci dahil.
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
3. Bir talep tanımı toohello uzantı ilke dosyası ekleme `TrustFrameworkExtensions.xml` hello içinde `<ClaimsSchema>` gösterildiği gibi öğesi.
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
4. Merhaba eklemek aynı tanımı toohello temel ilke dosyası talep `TrustFrameworkBase.xml`.  
>Ekleme bir `ClaimType` hello temel ve hello uzantıları dosya tanımında normalde gerekli değildir, ancak hello sonraki adımlar hello temel dosyasında hello extension_loyaltyId tooTechnicalProfiles ekleyeceksiniz beri hello İlkesi Doğrulayıcı hello karşıya yükleme reddeder temel dosyası Hello olmadan.
>Merhaba TrustFrameworkBase.xml dosyasındaki "ProfileEdit" adlı hello kullanıcı gezisine yararlı tootrace hello yürütülmesi olabilir.  Merhaba kullanıcı gezisine aynı adı düzenleyicinizde ve Orchestration adım 5'hello TechnicalProfileReferenceID çağırır uyun Merhaba, Ara "SelfAsserted-ProfileUpdate" =.  Arama ve bu TechnicalProfile toofamiliarize kendiniz hello akışla inceleyin.
5. Giriş ve çıkış hello TechnicalProfile "SelfAsserted-ProfileUpdate" talebi olarak loyaltyId Ekle
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
6. Talep TechnicalProfile "AAD-UserWriteProfileUsingObjectId" toopersist hello hello dizininde hello geçerli kullanıcı için hello uzantısı özelliğinde hello talebin değerini ekleyin.
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
7. Bir kullanıcı oturum açtığında her zaman talep TechnicalProfile "AAD-UserReadUsingObjectId" tooread hello değerini hello uzantısı özniteliğinin ekleyin. Bugüne kadarki hello TechnicalProfiles değiştirilmiş yalnızca yerel hesaplar hello akışında.  Merhaba yeni öznitelik bir sosyal ve Federasyon hesabı hello akışında istenirse, TechnicalProfiles farklı bir dizi değiştirilen toobe gerekir. Sonraki adımlara bakın.

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
>Merhaba IncludeTechnicalProfile öğesi AAD ortak toothis TechnicalProfile tüm hello öğelerine ekler.

## <a name="test-hello-custom-policy-using-run-now"></a>"Şimdi Çalıştır" kullanarak test hello özel İlkesi
1. Açık hello **Azure AD B2C dikey** ve çok gidin**kimlik deneyimi Framework > özel ilkeleri**.
1. Karşıya yüklediğiniz hello özel ilkesini seçin ve hello tıklayın **Şimdi Çalıştır** düğmesi.
1. Bir e-posta adresi kullanarak yukarı mümkün toosign olmalıdır.

Merhaba kimliği belirteci tooyour uygulama tarafından extension_loyaltyId öncesinde bir özel talep olarak hello yeni uzantı özelliği içerir geri gönderilir. Örneğe bakın.

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

## <a name="next-steps"></a>Sonraki adımlar

Merhaba yeni talep toohello akışları sosyal hesap oturum açma TechnicalProfiles listelenen hello değiştirerek ekleyin. Bu iki TechnicalProfiles sosyal ve Federasyon hesap oturumu açma toowrite tarafından kullanılan ve hello kullanıcı nesnesinin Bulucu hello gibi hello alternativeSecurityId kullanılarak hello kullanıcı verilerini okur.
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

Merhaba yerleşik ve özel ilkeleri arasında aynı uzantı öznitelikleri kullanma.
Merhaba portal deneyimi uzantı öznitelikleri (diğer adıyla özel öznitelikleri) eklediğinizde, özniteliklerle hello kullanarak kayıtlı ** b2c uzantıları-her b2c kiracınızda bulunan uygulama.  toouse özel ilkenizde bu uzantı öznitelikleri:
1. Portal.Azure.com b2c kiracısına içinde çok gidin**Azure Active Directory** seçip **uygulama kayıtlar**
2. Bulma, **b2c uzantıları uygulaması** ve seçin
3. 'Essentials' kaydı hello altında **uygulama kimliği** ve hello **nesne kimliği**
4. Bunları AAD genel teknik, profil meta verileri gibi aşağıdaki gibi ekleyin:

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

Merhaba portal deneyim tookeep tutarlılık oluşturmanıza hello portalı kullanıcı arabirimini kullanarak bu öznitelikler *önce* , özel ilkelerini kullanın.  Bir öznitelik "ActivationStatus" Merhaba Portalı'nda oluşturduğunuzda, tooit gibi başvurması gerekir:

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a>Başvuru

* A **teknik profil (TP)** , olarak düşünülebilir bir öğe türü bir *işlevi* bir uç noktanın adı, meta verilerini, protokol tanımlar ve ayrıntıları hello exchange kimlik hello talepler Deneyimi Framework gerçekleştirmeniz gerekir.  Zaman bu *işlevi* orchestration adım veya başka bir TechnicalProfile, hello InputClaims ve OutputClaims sağlanan parametre olarak hello çağıran tarafından çağrılır.


* Uzantısı özelliklerindeki tam işleme için hello makalesine bakın [DIRECTORY şema UZANTILARI | GRAFİK API'Sİ KAVRAMLARI](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)

>[!NOTE]
>Grafik API'si uzantı öznitelikleri hello kural kullanılarak adlandırılması `extension_ApplicationObjectID_attributename`. Özel ilkeler, extension_attributename, böylece hello XML hello ApplicationObjectId atlama olarak tooextensions öznitelikleri bakın.
