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
ms.openlocfilehash: eb44a0d2234c9ee3801d8b3a1655d877aa2f4fef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="39675-103">İzlenecek yol: Kullanıcı girişi doğrulama olarak Azure AD B2C kullanıcı Yolculuğunuzun REST API talep alışverişlerine tümleştirme</span><span class="sxs-lookup"><span data-stu-id="39675-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="39675-104">Azure Active Directory B2C altını çizen kimlik deneyimi Framework (IEF) (Azure AD B2C) etkileşim kullanıcı gezisine bir RESTful API'si ile tümleştirmek kimlik Geliştirici sağlar.</span><span class="sxs-lookup"><span data-stu-id="39675-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="39675-105">Bu kılavuzun sonunda RESTful hizmetlerle etkileşimde bulunan bir Azure AD B2C kullanıcı gezisine oluşturmak mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="39675-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="39675-106">IEF Taleplerde verileri gönderir ve geri Taleplerde verilerini alır.</span><span class="sxs-lookup"><span data-stu-id="39675-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="39675-107">API ile etkileşim:</span><span class="sxs-lookup"><span data-stu-id="39675-107">The interaction with the API:</span></span>

- <span data-ttu-id="39675-108">Bir REST API talep exchange veya orchestration adım içinde olur bir doğrulama profili olarak tasarlanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="39675-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="39675-109">Genellikle, kullanıcıdan girdi doğrular.</span><span class="sxs-lookup"><span data-stu-id="39675-109">Typically validates input from the user.</span></span> <span data-ttu-id="39675-110">Kullanıcı değerinden reddedilirse, kullanıcı bir hata iletisi döndürmek için fırsat ile geçerli bir değer girmesini yeniden deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="39675-110">If the value from the user is rejected, the user can try again to enter a valid value with the opportunity to return an error message.</span></span>

<span data-ttu-id="39675-111">Orchestration adım olarak etkileşim de tasarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="39675-111">You can also design the interaction as an orchestration step.</span></span> <span data-ttu-id="39675-112">Daha fazla bilgi için bkz: [izlenecek yol: REST API tümleştirme talep Azure AD B2C kullanıcı Yolculuğunuzun bir orchestration adım olarak alışverişlerine](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="39675-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="39675-113">Doğrulama profil örneği için başlangıç paketi dosyasında ProfileEdit.xml profil düzenleme kullanıcı gezisine kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="39675-113">For the validation profile example, we will use the profile edit user journey in the starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="39675-114">Profil düzenleme kullanıcı tarafından sağlanan adı bir çıkarma listesi parçası olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="39675-114">We can verify that the name provided by the user in the profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39675-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="39675-115">Prerequisites</span></span>

- <span data-ttu-id="39675-116">Bölümünde açıklandığı gibi bir yerel hesap oturumu-up/oturum açmayı tamamlamak için yapılandırılmış bir Azure AD B2C kiracısı [Başlarken](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="39675-116">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="39675-117">Etkileşim için bir REST API uç noktası.</span><span class="sxs-lookup"><span data-stu-id="39675-117">A REST API endpoint to interact with.</span></span> <span data-ttu-id="39675-118">Bu kılavuzda, biz adında bir gösteri sitesi ayarladınız [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) bir REST API hizmetiyle.</span><span class="sxs-lookup"><span data-stu-id="39675-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="39675-119">1. adım: REST API işlevi hazırlama</span><span class="sxs-lookup"><span data-stu-id="39675-119">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="39675-120">REST API işlevleri bu makalenin kapsamı dışındadır kurulması.</span><span class="sxs-lookup"><span data-stu-id="39675-120">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="39675-121">[Azure işlevleri](https://docs.microsoft.com/azure/azure-functions/functions-reference) RESTful hizmetlerini bulutta oluşturmak için mükemmel bir araç sağlar.</span><span class="sxs-lookup"><span data-stu-id="39675-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="39675-122">Olarak bekliyor bir talep aldığında bir Azure işlevi oluşturduk `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="39675-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="39675-123">Bu talep var olup olmadığını işlevini doğrular.</span><span class="sxs-lookup"><span data-stu-id="39675-123">The function validates whether this claim exists.</span></span> <span data-ttu-id="39675-124">Tam Azure işlev kodu erişebilirsiniz [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="39675-124">You can access the complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

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
      userMessage = $"The player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

<span data-ttu-id="39675-125">IEF bekliyor `userMessage` talep, Azure işlevi döndürür.</span><span class="sxs-lookup"><span data-stu-id="39675-125">The IEF expects the `userMessage` claim that the Azure function returns.</span></span> <span data-ttu-id="39675-126">Bu talep 409 çakışma durum önceki örnekte döndürüldüğünde gibi doğrulama başarısız olursa kullanıcıya bir dize olarak sunulur.</span><span class="sxs-lookup"><span data-stu-id="39675-126">This claim will be presented as a string to the user if the validation fails, such as when a 409 conflict status is returned in the preceding example.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="39675-127">2. adım: RESTful API'si talep exchange TrustFrameworkExtensions.xml dosyanızdaki teknik bir profil olarak yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="39675-127">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="39675-128">İstenen RESTful hizmeti ile exchange tam yapılandırmasını bir teknik profilidir.</span><span class="sxs-lookup"><span data-stu-id="39675-128">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="39675-129">TrustFrameworkExtensions.xml dosyasını açın ve aşağıdaki XML parçacığını içine ekleyin `<ClaimsProviders>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="39675-129">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="39675-130">Aşağıdaki XML, RESTful sağlayıcısı `Version=1.0.0.0` protokol olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="39675-130">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="39675-131">Dış hizmetiyle etkileşime gireceğini işlevi olarak düşünün.</span><span class="sxs-lookup"><span data-stu-id="39675-131">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

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

<span data-ttu-id="39675-132">`InputClaims` Öğesi IEF REST hizmeti gönderilecek Talepleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="39675-132">The `InputClaims` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="39675-133">Bu örnekte, talep içeriğini `givenName` REST hizmeti olarak gönderilir `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="39675-133">In this example, the contents of the claim `givenName` will be sent to the REST service as `playerTag`.</span></span> <span data-ttu-id="39675-134">Bu örnekte, talep geri IEF beklemiyor.</span><span class="sxs-lookup"><span data-stu-id="39675-134">In this example, the IEF does not expect claims back.</span></span> <span data-ttu-id="39675-135">Bunun yerine, aldığı durum kodlarına dayalı davranır ve REST hizmeti yanıt bekler.</span><span class="sxs-lookup"><span data-stu-id="39675-135">Instead, it waits for a response from the REST service and acts based on the status codes that it receives.</span></span>

## <a name="step-3-include-the-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-to-validate-the-user-input"></a><span data-ttu-id="39675-136">3. adım: RESTful Hizmeti talepleri exchange kullanıcı girişi doğrulamak istediğiniz Self sürülen teknik profiline Ekle</span><span class="sxs-lookup"><span data-stu-id="39675-136">Step 3: Include the RESTful service claims exchange in self-asserted technical profile where you want to validate the user input</span></span>

<span data-ttu-id="39675-137">Doğrulama adımını en yaygın kullanımı bir kullanıcıyla etkileşim bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="39675-137">The most common use of the validation step is in the interaction with a user.</span></span> <span data-ttu-id="39675-138">Burada kullanıcının beklenmektedir giriş sağlamak için tüm etkileşimler *teknik profilleri otomatik olarak uygulanan*.</span><span class="sxs-lookup"><span data-stu-id="39675-138">All interactions where the user is expected to provide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="39675-139">Bu örnekte, kendi Asserted ProfileUpdate teknik profili doğrulama ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="39675-139">For this example, we will add the validation to the Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="39675-140">Bu teknik olduğu profilini bağlı olan taraf (RP) ilke dosyası `Profile Edit` kullanır.</span><span class="sxs-lookup"><span data-stu-id="39675-140">This is the technical profile that the relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="39675-141">Talep exchange Self sürülen teknik profiline eklemek için:</span><span class="sxs-lookup"><span data-stu-id="39675-141">To add the claims exchange to the self-asserted technical profile:</span></span>

1. <span data-ttu-id="39675-142">TrustFrameworkBase.xml dosyasını açın ve arama `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span><span class="sxs-lookup"><span data-stu-id="39675-142">Open the TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="39675-143">Bu teknik profil yapılandırmasını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="39675-143">Review the configuration of this technical profile.</span></span> <span data-ttu-id="39675-144">Kullanıcı ile exchange kullanıcısı (giriş talep) istenir talepleri ve geri Self sürülen Sağlayıcısı'ndan (çıkış talep) beklenen talepler olarak nasıl tanımlanır gözlemleyin.</span><span class="sxs-lookup"><span data-stu-id="39675-144">Observe how the exchange with the user is defined as claims that will be asked of the user (input claims) and claims that will be expected back from the self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="39675-145">Arama `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`ve bu profili orchestration 6. adım çağrılır fark `<UserJourney Id="ProfileEdit">`.</span><span class="sxs-lookup"><span data-stu-id="39675-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-the-profile-edit-rp-policy-file"></a><span data-ttu-id="39675-146">4. adım: Karşıya yükleme ve test profil düzenleme RP ilke dosyası</span><span class="sxs-lookup"><span data-stu-id="39675-146">Step 4: Upload and test the profile edit RP policy file</span></span>

1. <span data-ttu-id="39675-147">TrustFrameworkExtensions.xml dosyasının yeni sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="39675-147">Upload the new version of the TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="39675-148">Kullanım **Şimdi Çalıştır** profil düzenleme RP ilke dosyası test etmek için.</span><span class="sxs-lookup"><span data-stu-id="39675-148">Use **Run now** to test the profile edit RP policy file.</span></span>
3. <span data-ttu-id="39675-149">Doğrulama var olan adlar (örneğin, mcvinny) birini sağlayarak test **verilen ad** alan.</span><span class="sxs-lookup"><span data-stu-id="39675-149">Test the validation by providing one of the existing names (for example, mcvinny) in the **Given Name** field.</span></span> <span data-ttu-id="39675-150">Her şeyin doğru şekilde ayarlanmış olması durumunda kullanıcı player etiketi zaten kullanıldığını bildiren bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="39675-150">If everything is set up correctly, you should receive a message that notifies the user that the player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39675-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="39675-151">Next steps</span></span>

[<span data-ttu-id="39675-152">Kullanıcılardan ek bilgi toplamak için profil düzenleme ve kullanıcı kaydı değiştirin</span><span class="sxs-lookup"><span data-stu-id="39675-152">Modify the profile edit and user registration to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="39675-153">İzlenecek yol: Azure AD B2C kullanıcı Yolculuğunuzun REST API talep alışverişlerine orchestration adım olarak tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="39675-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
