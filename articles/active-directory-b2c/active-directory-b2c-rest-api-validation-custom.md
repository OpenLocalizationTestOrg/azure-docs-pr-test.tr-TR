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
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="99699-103">İzlenecek yol: Kullanıcı girişi doğrulama olarak Azure AD B2C kullanıcı Yolculuğunuzun REST API talep alışverişlerine tümleştirme</span><span class="sxs-lookup"><span data-stu-id="99699-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="99699-104">Hello Azure Active Directory B2C altını çizen kimlik deneyimi Framework (IEF) (Azure AD B2C) hello kimlik Geliştirici toointegrate kullanıcı gezisine bir RESTful API'si ile etkileşim sağlar.</span><span class="sxs-lookup"><span data-stu-id="99699-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="99699-105">Bu kılavuzda Hello sonunda mümkün toocreate RESTful hizmetlerle etkileşimde bulunan bir Azure AD B2C kullanıcı gezisine olacaktır.</span><span class="sxs-lookup"><span data-stu-id="99699-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="99699-106">Merhaba IEF Taleplerde verileri gönderir ve geri Taleplerde verilerini alır.</span><span class="sxs-lookup"><span data-stu-id="99699-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="99699-107">Merhaba API etkileşim Hello:</span><span class="sxs-lookup"><span data-stu-id="99699-107">hello interaction with hello API:</span></span>

- <span data-ttu-id="99699-108">Bir REST API talep exchange veya orchestration adım içinde olur bir doğrulama profili olarak tasarlanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="99699-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="99699-109">Genellikle hello kullanıcıdan giriş doğrular.</span><span class="sxs-lookup"><span data-stu-id="99699-109">Typically validates input from hello user.</span></span> <span data-ttu-id="99699-110">Merhaba kullanıcı Hello değerinden reddedilirse, hello kullanıcı tooenter hello fırsat tooreturn bir hata iletisi geçerli bir değerle yeniden deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99699-110">If hello value from hello user is rejected, hello user can try again tooenter a valid value with hello opportunity tooreturn an error message.</span></span>

<span data-ttu-id="99699-111">Orchestration adım olarak hello etkileşim de tasarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99699-111">You can also design hello interaction as an orchestration step.</span></span> <span data-ttu-id="99699-112">Daha fazla bilgi için bkz: [izlenecek yol: REST API tümleştirme talep Azure AD B2C kullanıcı Yolculuğunuzun bir orchestration adım olarak alışverişlerine](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="99699-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="99699-113">Merhaba doğrulama profili örneğin hello başlangıç paketi dosyasını ProfileEdit.xml hello profil düzenleme kullanıcı gezisine kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="99699-113">For hello validation profile example, we will use hello profile edit user journey in hello starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="99699-114">Hello profil hello kullanıcı tarafından düzenleme bir dışlama listesinde yer sağlanan Biz bu hello adı doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99699-114">We can verify that hello name provided by hello user in hello profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99699-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="99699-115">Prerequisites</span></span>

- <span data-ttu-id="99699-116">Azure AD B2C Kiracı yapılandırılmış toocomplete oturumu-up/oturum açıklandığı gibi açma, yerel bir hesap [Başlarken](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="99699-116">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="99699-117">REST API uç noktası toointeract ile.</span><span class="sxs-lookup"><span data-stu-id="99699-117">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="99699-118">Bu kılavuzda, biz adında bir gösteri sitesi ayarladınız [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) bir REST API hizmetiyle.</span><span class="sxs-lookup"><span data-stu-id="99699-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="99699-119">1. adım: hello REST API işlevi hazırlama</span><span class="sxs-lookup"><span data-stu-id="99699-119">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="99699-120">REST API işlevleri bu makalenin kapsamı dışındadır hello kurulması.</span><span class="sxs-lookup"><span data-stu-id="99699-120">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="99699-121">[Azure işlevleri](https://docs.microsoft.com/azure/azure-functions/functions-reference) toocreate RESTful hizmetlerini hello bulutta mükemmel bir araç sağlar.</span><span class="sxs-lookup"><span data-stu-id="99699-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="99699-122">Olarak bekliyor bir talep aldığında bir Azure işlevi oluşturduk `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="99699-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="99699-123">Merhaba işlevi bu talep var olup olmadığını doğrular.</span><span class="sxs-lookup"><span data-stu-id="99699-123">hello function validates whether this claim exists.</span></span> <span data-ttu-id="99699-124">Merhaba tam Azure işlev kodu erişebilirsiniz [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="99699-124">You can access hello complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

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

<span data-ttu-id="99699-125">Merhaba IEF bekliyor hello `userMessage` talep bu hello Azure işlevi döndürür.</span><span class="sxs-lookup"><span data-stu-id="99699-125">hello IEF expects hello `userMessage` claim that hello Azure function returns.</span></span> <span data-ttu-id="99699-126">409 çakışma durumu örnek önceki hello döndürüldüğünde gibi Hello doğrulama başarısız olursa bu talebi bir dize toohello kullanıcı olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="99699-126">This claim will be presented as a string toohello user if hello validation fails, such as when a 409 conflict status is returned in hello preceding example.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="99699-127">2. adım: hello RESTful API'si talep exchange TrustFrameworkExtensions.xml dosyanızdaki teknik bir profil olarak yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="99699-127">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="99699-128">Teknik bir profili hello tam hello Exchange hello RESTful hizmeti ile istenen bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="99699-128">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="99699-129">Merhaba TrustFrameworkExtensions.xml dosyasını açın ve aşağıdaki XML parçacığını hello içinde hello ekleyin `<ClaimsProviders>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="99699-129">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="99699-130">XML, RESTful sağlayıcısı aşağıdaki hello içinde `Version=1.0.0.0` hello protokolü olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="99699-130">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="99699-131">Merhaba dış hizmetiyle etkileşime gireceğini hello işlevi olarak düşünün.</span><span class="sxs-lookup"><span data-stu-id="99699-131">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

<span data-ttu-id="99699-132">Merhaba `InputClaims` öğesi IEF toohello REST hizmeti hello gönderilecek hello talepleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="99699-132">hello `InputClaims` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="99699-133">Bu örnekte, hello hello talep içeriğini `givenName` toohello REST hizmeti olarak gönderilecek `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="99699-133">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as `playerTag`.</span></span> <span data-ttu-id="99699-134">Bu örnekte, IEF değil beklediğiniz hello geri talepleri.</span><span class="sxs-lookup"><span data-stu-id="99699-134">In this example, hello IEF does not expect claims back.</span></span> <span data-ttu-id="99699-135">Bunun yerine, hello REST hizmeti ve aldığı hello durum kodlarına dayalı davranır yanıt bekler.</span><span class="sxs-lookup"><span data-stu-id="99699-135">Instead, it waits for a response from hello REST service and acts based on hello status codes that it receives.</span></span>

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a><span data-ttu-id="99699-136">3. adım: hello RESTful Hizmeti talepleri exchange toovalidate hello kullanıcı girişi istediğiniz Self sürülen teknik profiline Ekle</span><span class="sxs-lookup"><span data-stu-id="99699-136">Step 3: Include hello RESTful service claims exchange in self-asserted technical profile where you want toovalidate hello user input</span></span>

<span data-ttu-id="99699-137">Merhaba en yaygın hello doğrulama adımı, bir kullanıcı ile Merhaba etkileşim kullanılır.</span><span class="sxs-lookup"><span data-stu-id="99699-137">hello most common use of hello validation step is in hello interaction with a user.</span></span> <span data-ttu-id="99699-138">Merhaba kullanıcı girişi beklenen tooprovide olduğu tüm etkileşimler *teknik profilleri otomatik olarak uygulanan*.</span><span class="sxs-lookup"><span data-stu-id="99699-138">All interactions where hello user is expected tooprovide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="99699-139">Bu örnekte, hello doğrulama toohello kendi Asserted ProfileUpdate teknik profili ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="99699-139">For this example, we will add hello validation toohello Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="99699-140">Bu, bağlı olan taraf (RP) ilke dosyası hello hello teknik profilidir `Profile Edit` kullanır.</span><span class="sxs-lookup"><span data-stu-id="99699-140">This is hello technical profile that hello relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="99699-141">Teknik profili otomatik olarak uygulanan tooadd hello talep exchange toohello:</span><span class="sxs-lookup"><span data-stu-id="99699-141">tooadd hello claims exchange toohello self-asserted technical profile:</span></span>

1. <span data-ttu-id="99699-142">Açık hello TrustFrameworkBase.xml dosyasını ve arama `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span><span class="sxs-lookup"><span data-stu-id="99699-142">Open hello TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="99699-143">Bu teknik profili Hello yapılandırmasını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="99699-143">Review hello configuration of this technical profile.</span></span> <span data-ttu-id="99699-144">Merhaba kullanıcısı (giriş talep) istenir talepleri ve geri hello Self sürülen Sağlayıcısı'ndan (çıkış talep) beklenen talepler olarak hello exchange hello kullanıcı ile nasıl tanımlanan gözlemleyin.</span><span class="sxs-lookup"><span data-stu-id="99699-144">Observe how hello exchange with hello user is defined as claims that will be asked of hello user (input claims) and claims that will be expected back from hello self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="99699-145">Arama `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`ve bu profili orchestration 6. adım çağrılır fark `<UserJourney Id="ProfileEdit">`.</span><span class="sxs-lookup"><span data-stu-id="99699-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a><span data-ttu-id="99699-146">4. adım: Karşıya yükleme ve test hello profil düzenleme RP ilke dosyası</span><span class="sxs-lookup"><span data-stu-id="99699-146">Step 4: Upload and test hello profile edit RP policy file</span></span>

1. <span data-ttu-id="99699-147">Merhaba hello TrustFrameworkExtensions.xml dosyasının yeni sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="99699-147">Upload hello new version of hello TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="99699-148">Kullanım **Şimdi Çalıştır** tootest hello profil RP ilke dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="99699-148">Use **Run now** tootest hello profile edit RP policy file.</span></span>
3. <span data-ttu-id="99699-149">Test hello doğrulama hello var olan adlar (örneğin, mcvinny) birini sağlayarak hello **verilen ad** alan.</span><span class="sxs-lookup"><span data-stu-id="99699-149">Test hello validation by providing one of hello existing names (for example, mcvinny) in hello **Given Name** field.</span></span> <span data-ttu-id="99699-150">Her şeyin doğru şekilde ayarlanmış olması durumunda hello kullanıcı hello player etiketi zaten kullanıldığını bildiren bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="99699-150">If everything is set up correctly, you should receive a message that notifies hello user that hello player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99699-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="99699-151">Next steps</span></span>

[<span data-ttu-id="99699-152">Hello profil düzenleme ve kullanıcı kayıt toogather ek bilgileri, kullanıcılarınızın değiştirin</span><span class="sxs-lookup"><span data-stu-id="99699-152">Modify hello profile edit and user registration toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="99699-153">İzlenecek yol: Azure AD B2C kullanıcı Yolculuğunuzun REST API talep alışverişlerine orchestration adım olarak tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="99699-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
