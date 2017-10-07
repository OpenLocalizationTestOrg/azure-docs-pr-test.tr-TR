---
title: "Azure Active Directory B2C: REST API alışverişleri orchestration adım olarak talep | Microsoft Docs"
description: "Konuyla ilgili bir API ile tümleştirmek Azure Active Directory B2C özel ilkeler"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/24/2017
ms.author: joroja
ms.openlocfilehash: 90a495029f48d70232ef3f99de4ea4d351395aa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a>İzlenecek yol: Azure AD B2C kullanıcı Yolculuğunuzun REST API talep alışverişlerine orchestration adım olarak tümleştirin.

Hello Azure Active Directory B2C altını çizen kimlik deneyimi Framework (IEF) (Azure AD B2C) hello kimlik Geliştirici toointegrate kullanıcı gezisine bir RESTful API'si ile etkileşim sağlar.  

Bu kılavuzda Hello sonunda mümkün toocreate RESTful hizmetlerle etkileşimde bulunan bir Azure AD B2C kullanıcı gezisine olacaktır.

Merhaba IEF Taleplerde verileri gönderir ve geri Taleplerde verilerini alır. REST API talep exchange Hello:

- Orchestration adım olarak tasarlanmış olabilir.
- Bir dış eylem tetikleyebilir. Örneğin, bir olay dış veritabanında kaydedebilirsiniz.
- Kullanılan toofetch bir değer olması ve hello kullanıcı veritabanında depolamak kullanabilirsiniz.

Alınan hello talepleri kullanan sonraki toochange hello akışını.

Bir doğrulama profili olarak hello etkileşim de tasarlayabilirsiniz. Daha fazla bilgi için bkz: [izlenecek yol: REST API tümleştirme kullanıcı girişini doğrulama olarak Azure AD B2C kullanıcı Yolculuğunuzun alışverişlerine talep](active-directory-b2c-rest-api-validation-custom.md).

Merhaba senaryo, bir kullanıcı profili Düzenle gerçekleştirdiğinde, istediğimizi şöyledir:

1. Merhaba kullanıcı bir dış sistemde arayın.
2. Bu kullanıcının, kayıtlı hello Şehir alın.
3. Bu öznitelik toohello uygulama talep olarak döndürür.

## <a name="prerequisites"></a>Ön koşullar

- Azure AD B2C Kiracı yapılandırılmış toocomplete oturumu-up/oturum açıklandığı gibi açma, yerel bir hesap [Başlarken](active-directory-b2c-get-started-custom.md).
- REST API uç noktası toointeract ile. Bu kılavuzda, bir basit Azure işlevi app Web kancası örnek olarak kullanılır.
- *Önerilen*: tam hello [REST API talep exchange izlenecek bir doğrulama adımı olarak](active-directory-b2c-rest-api-validation-custom.md).

## <a name="step-1-prepare-hello-rest-api-function"></a>1. adım: hello REST API işlevi hazırlama

> [!NOTE]
> REST API işlevleri bu makalenin kapsamı dışındadır hello kurulması. [Azure işlevleri](https://docs.microsoft.com/azure/azure-functions/functions-reference) toocreate RESTful hizmetlerini hello bulutta mükemmel bir araç sağlar.

Adlı bir talep aldığında bir Azure işlevi ayarlarız `email`, ve ardından talep döndürür hello `city` , atanan hello değeriyle `Redmond`. Merhaba örnek Azure işlevi açıktır [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).

Merhaba `userMessage` Azure işlev dönüşleri hello talep bu bağlamda isteğe bağlıdır ve hello IEF bunu yoksayacaktır. Bir ileti toohello uygulama geçirilen ve toohello kullanıcı daha sonra sunulan, potansiyel olarak kullanabilirsiniz.

```csharp
if (requestContentAsJObject.email == null)
{
    return request.CreateResponse(HttpStatusCode.BadRequest);
}

var email = ((string) requestContentAsJObject.email).ToLower();

return request.CreateResponse<ResponseContent>(
    HttpStatusCode.OK,
    new ResponseContent
    {
        version = "1.0.0",
        status = (int) HttpStatusCode.OK,
        userMessage = "User Found",
        city = "Redmond"
    },
    new JsonMediaTypeFormatter(),
    "application/json");
```

Bir Azure işlevi uygulama hello belirli bir işlev hello tanımlayıcısını içeren kolay tooget hello işlevi URL kolaylaştırır. Bu durumda, hello URL'dir: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==. Bunu test etmek için kullanabilirsiniz.

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a>2. adım: hello RESTful API'si talep exchange TrustFrameworExtensions.xml dosyanızdaki teknik bir profil olarak yapılandırın.

Teknik bir profili hello tam hello Exchange hello RESTful hizmeti ile istenen bir yapılandırmadır. Merhaba TrustFrameworkExtensions.xml dosyasını açın ve aşağıdaki XML parçacığını hello içinde hello ekleyin `<ClaimsProvider>` öğesi.

> [!NOTE]
> XML, RESTful sağlayıcısı aşağıdaki hello içinde `Version=1.0.0.0` hello protokolü olarak tanımlanır. Merhaba dış hizmetiyle etkileşime gireceğini hello işlevi olarak düşünün. <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```XML
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-LookUpLoyaltyWebHook">
            <DisplayName>Check LookUpLoyalty Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="email" />
            </InputClaims>
            <OutputClaims>
                <OutputClaim ClaimTypeReferenceId="city" PartnerClaimType="city" />
            </OutputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

Merhaba `<InputClaims>` öğesi IEF toohello REST hizmeti hello gönderilecek hello talepleri tanımlar. Bu örnekte, hello hello talep içeriğini `givenName` toohello REST hizmeti hello talep olarak gönderilecek `email`.  

Merhaba `<OutputClaims>` öğesi IEF hello REST hizmetinden beklediğiniz bu hello hello talepleri tanımlar. Alınan talep Hello sayısından bağımsız olarak, hello IEF yalnızca tanımlanan burada kullanır. Bu örnekte, olarak bir talep alınan `city` eşlenen tooan IEF talep çağrılacağı `city`.

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a>3. adım: hello yeni talep ekleme `city` TrustFrameworkExtensions.xml dosyanızı toohello şeması

Merhaba talep `city` henüz herhangi bir yere bizim şemada tanımlı değil. Bu nedenle, bir tanım hello öğesinin içine ekleyin `<BuildingBlocks>`. Bu öğe hello TrustFrameworkExtensions.xml dosyasının hello başında bulabilirsiniz.

```XML
<BuildingBlocks>
    <!--hello claimtype city must be added toohello TrustFrameworkPolicy-->
    <!-- You can add new claims in hello BASE file Section III, or in hello extensions file-->
    <ClaimsSchema>
        <ClaimType Id="city">
            <DisplayName>City</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your city</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
    </ClaimsSchema>
</BuildingBlocks>
```

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a>4. adım: Profil düzenleme kullanıcı Yolculuğunuzun TrustFrameworkExtensions.xml içinde orchestration adımda olarak hello REST Hizmeti talepleri exchange Ekle

Bir adım eklemek hello kullanıcı sonra toohello profil düzenleme kullanıcı gezisine (1-4 XML aşağıdaki hello içinde düzenleme adımlarının) kimlik doğrulaması ve hello kullanıcı güncelleştirilmiş hello profil bilgilerini (5. adım) sağlanan.

> [!NOTE]
> Merhaba REST API çağrısı orchestration adım olarak kullanıldığı birçok kullanım örnekleri vardır. Orchestration adım olarak, bir kullanıcı ilk kez kayıt gibi bir görevi başarıyla tamamlandıktan sonra bir güncelleştirme tooan dış sistem kullanılabilir veya bir profil olarak eşitlenen tookeep bilgilerini güncelleştirin. Bu durumda, onu hello profil düzenledikten sonra toohello uygulama sağlanan kullanılan tooaugment hello bilgilerdir.

Kopyalama hello profil düzenleme kullanıcı gezisine XML hello TrustFrameworkBase.xml tooyour TrustFrameworkExtensions.xml dosyası hello içinde kodundan `<UserJourneys>` öğesi. Daha sonra 6. adım altında hello değişiklik yapın.

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> Merhaba sipariş sürümünüzü eşleşmiyorsa hello önce hello adım olarak hello kod yerleştirdiğinizden emin olun `ClaimsExchange` türü `SendClaims`.

Merhaba son XML hello kullanıcı gezisine için aşağıdaki gibi görünmelidir:

```XML
<UserJourney Id="ProfileEdit">
    <OrchestrationSteps>
        <OrchestrationStep Order="1" Type="ClaimsProviderSelection" ContentDefinitionReferenceId="api.idpselections">
            <ClaimsProviderSelections>
                <ClaimsProviderSelection TargetClaimsExchangeId="FacebookExchange" />
                <ClaimsProviderSelection TargetClaimsExchangeId="LocalAccountSigninEmailExchange" />
            </ClaimsProviderSelections>
        </OrchestrationStep>
        <OrchestrationStep Order="2" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="FacebookExchange" TechnicalProfileReferenceId="Facebook-OAUTH" />
                <ClaimsExchange Id="LocalAccountSigninEmailExchange" TechnicalProfileReferenceId="SelfAsserted-LocalAccountSignin-Email" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="3" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>localAccountAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserRead" TechnicalProfileReferenceId="AAD-UserReadUsingAlternativeSecurityId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="4" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>socialIdpAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserReadWithObjectId" TechnicalProfileReferenceId="AAD-UserReadUsingObjectId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="5" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="B2CUserProfileUpdateExchange" TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <!-- Add a step 6 toohello user journey before hello JWT token is created-->
        <OrchestrationStep Order="6" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="7" Type="SendClaims" CpimIssuerTechnicalProfileReferenceId="JwtIssuer" />
    </OrchestrationSteps>
    <ClientDefinition ReferenceId="DefaultWeb" />
</UserJourney>
```

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a>5. adım: hello talep ekleme `city` tooyour bağlı olan taraf İlkesi dosya hello talep tooyour uygulama gönderilir şekilde

ProfileEdit.xml bağlı olan taraf (RP) dosyanızı düzenleyin ve hello değiştirme `<TechnicalProfile Id="PolicyProfile">` öğesi tooadd hello aşağıdaki: `<OutputClaim ClaimTypeReferenceId="city" />`.

Merhaba yeni talep ekledikten sonra hello teknik profili şöyle görünür:

```XML
<DisplayName>PolicyProfile</DisplayName>
    <Protocol Name="OpenIdConnect" />
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <SubjectNamingInfo ClaimType="sub" />
</TechnicalProfile>
```

## <a name="step-6-upload-your-changes-and-test"></a>6. adım: değişikliklerinizi karşıya yüklemek ve test etme

Merhaba hello İlkesi varolan önceki sürümlerin üzerine yazın.

1.  (İsteğe bağlı:) Devam etmeden önce hello mevcut sürümü (yükleyerek) uzantıları dosyanızın kaydedin. tookeep hello ilk karmaşıklık düşük, birden fazla sürümünü hello uzantıları dosyasını karşıya yüklemeyin öneririz.
2.  (İsteğe bağlı:) Merhaba ilke kimliği hello İlkesi Düzenle dosyası için yeni sürümü Hello değiştirerek yeniden adlandırın `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.
3.  Merhaba uzantıları dosyasını karşıya yükleyin.
4.  Hello İlkesi Düzenle RP dosyasını karşıya yükleyin.
5.  Kullanım **Şimdi Çalıştır** tootest hello ilkesi. IEF hello gözden geçirme hello belirteci toohello uygulama döndürür.

Her şeyin doğru şekilde ayarlanmış olması durumunda hello belirteci hello yeni talep içerecektir `city`, hello değerle `Redmond`.

```JSON
{
  "exp": 1493053292,
  "nbf": 1493049692,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493049692,
  "auth_time": 1493049692,
  "city": "Redmond"
}
```

## <a name="next-steps"></a>Sonraki adımlar

[Doğrulama adımı olarak REST API kullanın](active-directory-b2c-rest-api-validation-custom.md)

[Hello profil düzenleme toogather ek bilgileri, kullanıcılarınızın değiştirin](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
