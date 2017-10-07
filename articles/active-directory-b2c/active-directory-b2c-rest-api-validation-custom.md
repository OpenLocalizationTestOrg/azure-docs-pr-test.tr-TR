---
title: "Azure Active Directory B2C: REST API alışverişleri doğrulama talep | Microsoft Docs"
description: "Bir konu Azure Active Directory B2C özel ilkeler hakkında"
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
ms.openlocfilehash: cec6c6e110514a8bbe0e0780f36738ff21ae2f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a>İzlenecek yol: Kullanıcı girişi doğrulama olarak Azure AD B2C kullanıcı Yolculuğunuzun REST API talep alışverişlerine tümleştirme

Hello Azure Active Directory B2C altını çizen kimlik deneyimi Framework (IEF) (Azure AD B2C) hello kimlik Geliştirici toointegrate kullanıcı gezisine bir RESTful API'si ile etkileşim sağlar.  

Bu kılavuzda Hello sonunda mümkün toocreate RESTful hizmetlerle etkileşimde bulunan bir Azure AD B2C kullanıcı gezisine olacaktır.

Merhaba IEF Taleplerde verileri gönderir ve geri Taleplerde verilerini alır. Merhaba API etkileşim Hello:

- Bir REST API talep exchange veya orchestration adım içinde olur bir doğrulama profili olarak tasarlanmış olabilir.
- Genellikle hello kullanıcıdan giriş doğrular. Merhaba kullanıcı Hello değerinden reddedilirse, hello kullanıcı tooenter hello fırsat tooreturn bir hata iletisi geçerli bir değerle yeniden deneyebilirsiniz.

Orchestration adım olarak hello etkileşim de tasarlayabilirsiniz. Daha fazla bilgi için bkz: [izlenecek yol: REST API tümleştirme talep Azure AD B2C kullanıcı Yolculuğunuzun bir orchestration adım olarak alışverişlerine](active-directory-b2c-rest-api-step-custom.md).

Merhaba doğrulama profili örneğin hello başlangıç paketi dosyasını ProfileEdit.xml hello profil düzenleme kullanıcı gezisine kullanacağız.

Hello profil hello kullanıcı tarafından düzenleme bir dışlama listesinde yer sağlanan Biz bu hello adı doğrulayabilirsiniz.

## <a name="prerequisites"></a>Ön koşullar

- Azure AD B2C Kiracı yapılandırılmış toocomplete oturumu-up/oturum açıklandığı gibi açma, yerel bir hesap [Başlarken](active-directory-b2c-get-started-custom.md).
- REST API uç noktası toointeract ile. Bu kılavuzda, biz adında bir gösteri sitesi ayarladınız [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) bir REST API hizmetiyle.

## <a name="step-1-prepare-hello-rest-api-function"></a>1. adım: hello REST API işlevi hazırlama

> [!NOTE]
> REST API işlevleri bu makalenin kapsamı dışındadır hello kurulması. [Azure işlevleri](https://docs.microsoft.com/azure/azure-functions/functions-reference) toocreate RESTful hizmetlerini hello bulutta mükemmel bir araç sağlar.

Olarak bekliyor bir talep aldığında bir Azure işlevi oluşturduk `playerTag`. Merhaba işlevi bu talep var olup olmadığını doğrular. Merhaba tam Azure işlev kodu erişebilirsiniz [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).

```csharp
if (requestContentAsJObject.playerTag == null)
{
  return request.CreateResponse(HttpStatusCode.BadRequest);
}

var playerTag = ((string) requestContentAsJObject.playerTag).ToLower();

if (playerTag == "mcvinny" || playerTag == "msgates123" || playerTag == "revcottonmarcus")
{
  return request.CreateResponse<ResponseContent>(
    HttpStatusCode.Conflict,
    new ResponseContent
    {
      version = "1.0.0",
      status = (int) HttpStatusCode.Conflict,
      userMessage = $"hello player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

Merhaba IEF bekliyor hello `userMessage` talep bu hello Azure işlevi döndürür. 409 çakışma durumu örnek önceki hello döndürüldüğünde gibi Hello doğrulama başarısız olursa bu talebi bir dize toohello kullanıcı olarak sunulur.

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a>2. adım: hello RESTful API'si talep exchange TrustFrameworkExtensions.xml dosyanızdaki teknik bir profil olarak yapılandırın.

Teknik bir profili hello tam hello Exchange hello RESTful hizmeti ile istenen bir yapılandırmadır. Merhaba TrustFrameworkExtensions.xml dosyasını açın ve aşağıdaki XML parçacığını hello içinde hello ekleyin `<ClaimsProviders>` öğesi.

> [!NOTE]
> XML, RESTful sağlayıcısı aşağıdaki hello içinde `Version=1.0.0.0` hello protokolü olarak tanımlanır. Merhaba dış hizmetiyle etkileşime gireceğini hello işlevi olarak düşünün. <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```xml
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-CheckPlayerTagWebHook">
            <DisplayName>Check Player Tag Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/CheckPlayerTagWebHook?code=L/05YRSpojU0nECzM4Tp3LjBiA2ZGh3kTwwp1OVV7m0SelnvlRVLCg==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="playerTag" />
            </InputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
        <TechnicalProfile Id="SelfAsserted-ProfileUpdate">
            <ValidationTechnicalProfiles>
                <ValidationTechnicalProfile ReferenceId="AzureFunctions-CheckPlayerTagWebHook" />
            </ValidationTechnicalProfiles>
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

Merhaba `InputClaims` öğesi IEF toohello REST hizmeti hello gönderilecek hello talepleri tanımlar. Bu örnekte, hello hello talep içeriğini `givenName` toohello REST hizmeti olarak gönderilecek `playerTag`. Bu örnekte, IEF değil beklediğiniz hello geri talepleri. Bunun yerine, hello REST hizmeti ve aldığı hello durum kodlarına dayalı davranır yanıt bekler.

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a>3. adım: hello RESTful Hizmeti talepleri exchange toovalidate hello kullanıcı girişi istediğiniz Self sürülen teknik profiline Ekle

Merhaba en yaygın hello doğrulama adımı, bir kullanıcı ile Merhaba etkileşim kullanılır. Merhaba kullanıcı girişi beklenen tooprovide olduğu tüm etkileşimler *teknik profilleri otomatik olarak uygulanan*. Bu örnekte, hello doğrulama toohello kendi Asserted ProfileUpdate teknik profili ekleyeceğiz. Bu, bağlı olan taraf (RP) ilke dosyası hello hello teknik profilidir `Profile Edit` kullanır.

Teknik profili otomatik olarak uygulanan tooadd hello talep exchange toohello:

1. Açık hello TrustFrameworkBase.xml dosyasını ve arama `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.
2. Bu teknik profili Hello yapılandırmasını gözden geçirin. Merhaba kullanıcısı (giriş talep) istenir talepleri ve geri hello Self sürülen Sağlayıcısı'ndan (çıkış talep) beklenen talepler olarak hello exchange hello kullanıcı ile nasıl tanımlanan gözlemleyin.
3. Arama `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`ve bu profili orchestration 6. adım çağrılır fark `<UserJourney Id="ProfileEdit">`.

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a>4. adım: Karşıya yükleme ve test hello profil düzenleme RP ilke dosyası

1. Merhaba hello TrustFrameworkExtensions.xml dosyasının yeni sürümünü yükleyin.
2. Kullanım **Şimdi Çalıştır** tootest hello profil RP ilke dosyasını düzenleyin.
3. Test hello doğrulama hello var olan adlar (örneğin, mcvinny) birini sağlayarak hello **verilen ad** alan. Her şeyin doğru şekilde ayarlanmış olması durumunda hello kullanıcı hello player etiketi zaten kullanıldığını bildiren bir ileti alırsınız.

## <a name="next-steps"></a>Sonraki adımlar

[Hello profil düzenleme ve kullanıcı kayıt toogather ek bilgileri, kullanıcılarınızın değiştirin](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[İzlenecek yol: Azure AD B2C kullanıcı Yolculuğunuzun REST API talep alışverişlerine orchestration adım olarak tümleştirin.](active-directory-b2c-rest-api-step-custom.md)
