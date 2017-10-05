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
ms.openlocfilehash: dc319c97e64e55861b84cc3943667418077a05d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="2a42e-103">İzlenecek yol: Azure AD B2C kullanıcı Yolculuğunuzun REST API talep alışverişlerine orchestration adım olarak tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="2a42e-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="2a42e-104">Azure Active Directory B2C altını çizen kimlik deneyimi Framework (IEF) (Azure AD B2C) etkileşim kullanıcı gezisine bir RESTful API'si ile tümleştirmek kimlik Geliştirici sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a42e-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="2a42e-105">Bu kılavuzun sonunda RESTful hizmetlerle etkileşimde bulunan bir Azure AD B2C kullanıcı gezisine oluşturmak mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="2a42e-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="2a42e-106">IEF Taleplerde verileri gönderir ve geri Taleplerde verilerini alır.</span><span class="sxs-lookup"><span data-stu-id="2a42e-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="2a42e-107">REST API exchange talepleri:</span><span class="sxs-lookup"><span data-stu-id="2a42e-107">The REST API claims exchange:</span></span>

- <span data-ttu-id="2a42e-108">Orchestration adım olarak tasarlanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="2a42e-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="2a42e-109">Bir dış eylem tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="2a42e-109">Can trigger an external action.</span></span> <span data-ttu-id="2a42e-110">Örneğin, bir olay dış veritabanında kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a42e-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="2a42e-111">Bir değer getirebilir ve kullanıcı veritabanında depolamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2a42e-111">Can be used to fetch a value and then store it in the user database.</span></span>

<span data-ttu-id="2a42e-112">Daha sonra akışını değiştirmek için alınan talep kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a42e-112">You can use the received claims later to change the flow of execution.</span></span>

<span data-ttu-id="2a42e-113">Bir doğrulama profili olarak etkileşim de tasarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a42e-113">You can also design the interaction as a validation profile.</span></span> <span data-ttu-id="2a42e-114">Daha fazla bilgi için bkz: [izlenecek yol: REST API tümleştirme kullanıcı girişini doğrulama olarak Azure AD B2C kullanıcı Yolculuğunuzun alışverişlerine talep](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="2a42e-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="2a42e-115">Bir kullanıcı profili Düzenle gerçekleştirdiğinde, istediğimizi senaryodur:</span><span class="sxs-lookup"><span data-stu-id="2a42e-115">The scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="2a42e-116">Kullanıcı bir dış sistemde arayın.</span><span class="sxs-lookup"><span data-stu-id="2a42e-116">Look up the user in an external system.</span></span>
2. <span data-ttu-id="2a42e-117">Bu kullanıcının, kayıtlı Şehir alın.</span><span class="sxs-lookup"><span data-stu-id="2a42e-117">Get the city where that user is registered.</span></span>
3. <span data-ttu-id="2a42e-118">Bu öznitelik uygulamayı bir talep olarak geri dönün.</span><span class="sxs-lookup"><span data-stu-id="2a42e-118">Return that attribute to the application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a42e-119">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2a42e-119">Prerequisites</span></span>

- <span data-ttu-id="2a42e-120">Bölümünde açıklandığı gibi bir yerel hesap oturumu-up/oturum açmayı tamamlamak için yapılandırılmış bir Azure AD B2C kiracısı [Başlarken](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="2a42e-120">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="2a42e-121">Etkileşim için bir REST API uç noktası.</span><span class="sxs-lookup"><span data-stu-id="2a42e-121">A REST API endpoint to interact with.</span></span> <span data-ttu-id="2a42e-122">Bu kılavuzda, bir basit Azure işlevi app Web kancası örnek olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2a42e-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="2a42e-123">*Önerilen*: tamamlamak [REST API talep exchange izlenecek bir doğrulama adımı olarak](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="2a42e-123">*Recommended*: Complete the [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="2a42e-124">1. adım: REST API işlevi hazırlama</span><span class="sxs-lookup"><span data-stu-id="2a42e-124">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="2a42e-125">REST API işlevleri bu makalenin kapsamı dışındadır kurulması.</span><span class="sxs-lookup"><span data-stu-id="2a42e-125">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="2a42e-126">[Azure işlevleri](https://docs.microsoft.com/azure/azure-functions/functions-reference) RESTful hizmetlerini bulutta oluşturmak için mükemmel bir araç sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a42e-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="2a42e-127">Adlı bir talep aldığında bir Azure işlevi ayarlarız `email`ve ardından talep döndürür `city` atanan değeriyle `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="2a42e-127">We have set up an Azure function that receives a claim called `email`, and then returns the claim `city` with the assigned value of `Redmond`.</span></span> <span data-ttu-id="2a42e-128">Azure işlevi örnek açıktır [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="2a42e-128">The sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="2a42e-129">`userMessage` Azure işlevi döndürür talep bu bağlamda isteğe bağlıdır ve IEF bunu göz ardı eder.</span><span class="sxs-lookup"><span data-stu-id="2a42e-129">The `userMessage` claim that the Azure function returns is optional in this context, and the IEF will ignore it.</span></span> <span data-ttu-id="2a42e-130">Potansiyel olarak uygulamaya geçirilen ve daha sonra kullanıcıya bir ileti kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a42e-130">You can potentially use it as a message passed to the application and presented to the user later.</span></span>

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

<span data-ttu-id="2a42e-131">Bir Azure işlevi uygulama belirli bir işlev tanımlayıcısını içeren işlevi URL'sini alma kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="2a42e-131">An Azure function app makes it easy to get the function URL, which includes the identifier of the specific function.</span></span> <span data-ttu-id="2a42e-132">Bu durumda, URL'si şöyledir: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span><span class="sxs-lookup"><span data-stu-id="2a42e-132">In this case, the URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="2a42e-133">Bunu test etmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a42e-133">You can use it for testing.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="2a42e-134">2. adım: RESTful API'si talep exchange TrustFrameworExtensions.xml dosyanızdaki teknik bir profil olarak yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2a42e-134">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="2a42e-135">İstenen RESTful hizmeti ile exchange tam yapılandırmasını bir teknik profilidir.</span><span class="sxs-lookup"><span data-stu-id="2a42e-135">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="2a42e-136">TrustFrameworkExtensions.xml dosyasını açın ve aşağıdaki XML parçacığını içine ekleyin `<ClaimsProvider>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="2a42e-136">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="2a42e-137">Aşağıdaki XML, RESTful sağlayıcısı `Version=1.0.0.0` protokol olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2a42e-137">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="2a42e-138">Dış hizmetiyle etkileşime gireceğini işlevi olarak düşünün.</span><span class="sxs-lookup"><span data-stu-id="2a42e-138">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

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

<span data-ttu-id="2a42e-139">`<InputClaims>` Öğesi IEF REST hizmeti gönderilecek Talepleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2a42e-139">The `<InputClaims>` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="2a42e-140">Bu örnekte, talep içeriğini `givenName` REST hizmeti talep olarak gönderileceği `email`.</span><span class="sxs-lookup"><span data-stu-id="2a42e-140">In this example, the contents of the claim `givenName` will be sent to the REST service as the claim `email`.</span></span>  

<span data-ttu-id="2a42e-141">`<OutputClaims>` Öğesi IEF REST hizmetinden beklediği talepleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2a42e-141">The `<OutputClaims>` element defines the claims that the IEF will expect from the REST service.</span></span> <span data-ttu-id="2a42e-142">Alınan talep sayısından bağımsız olarak, IEF yalnızca tanımlanan burada kullanır.</span><span class="sxs-lookup"><span data-stu-id="2a42e-142">Regardless of the number of claims that are received, the IEF will use only those identified here.</span></span> <span data-ttu-id="2a42e-143">Bu örnekte, olarak bir talep alınan `city` bir IEF eşlenecek adlı talep `city`.</span><span class="sxs-lookup"><span data-stu-id="2a42e-143">In this example, a claim received as `city` will be mapped to an IEF claim called `city`.</span></span>

## <a name="step-3-add-the-new-claim-city-to-the-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="2a42e-144">3. adım: yeni talep ekleme `city` TrustFrameworkExtensions.xml dosyanızın şemaya</span><span class="sxs-lookup"><span data-stu-id="2a42e-144">Step 3: Add the new claim `city` to the schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="2a42e-145">Talep `city` henüz herhangi bir yere bizim şemada tanımlı değil.</span><span class="sxs-lookup"><span data-stu-id="2a42e-145">The claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="2a42e-146">Bu nedenle, öğe içindeki bir tanım ekleyin `<BuildingBlocks>`.</span><span class="sxs-lookup"><span data-stu-id="2a42e-146">So, add a definition inside the element `<BuildingBlocks>`.</span></span> <span data-ttu-id="2a42e-147">Bu öğe TrustFrameworkExtensions.xml dosyasının başında bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a42e-147">You can find this element at the beginning of the TrustFrameworkExtensions.xml file.</span></span>

```XML
<BuildingBlocks>
    <!--The claimtype city must be added to the TrustFrameworkPolicy-->
    <!-- You can add new claims in the BASE file Section III, or in the extensions file-->
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

## <a name="step-4-include-the-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="2a42e-148">4. adım: Profil düzenleme kullanıcı Yolculuğunuzun TrustFrameworkExtensions.xml içinde bir orchestration adım gibi REST Hizmeti talepleri exchange içerir</span><span class="sxs-lookup"><span data-stu-id="2a42e-148">Step 4: Include the REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="2a42e-149">Kullanıcı sonra Profil düzenleme kullanıcı gezisine adıma (1-4 Aşağıdaki XML düzenleme adımlarının) kimlik doğrulaması ve kullanıcının güncelleştirilmiş profil bilgilerini (5. adım) sağlamıştır ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2a42e-149">Add a step to the profile edit user journey, after the user has been authenticated (orchestration steps 1-4 in the following XML) and the user has provided the updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="2a42e-150">REST API çağrısı orchestration adım olarak kullanıldığı birçok kullanım örnekleri vardır.</span><span class="sxs-lookup"><span data-stu-id="2a42e-150">There are many use cases where the REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="2a42e-151">Orchestration adım olarak, bu profili güncelleştirme olarak veya bir kullanıcı ilk kez kayıt gibi bir görevi başarıyla tamamlandıktan sonra bir dış sistem için bir güncelleştirme olarak bilgilerin eşitlenmiş tutmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2a42e-151">As an orchestration step, it can be used as an update to an external system after a user has successfully completed a task like first-time registration, or as a profile update to keep information synchronized.</span></span> <span data-ttu-id="2a42e-152">Bu durumda, bu profili düzenledikten sonra uygulamaya sağlanan bilgileri artırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2a42e-152">In this case, it's used to augment the information provided to the application after the profile edit.</span></span>

<span data-ttu-id="2a42e-153">Kopya profil düzenleme Itanium tabanlı sistemler için kullanıcı gezisine XML kodu TrustFrameworkBase.xml dosyasından TrustFrameworkExtensions.xml dosyanıza içinde `<UserJourneys>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="2a42e-153">Copy the profile edit user journey XML code from the TrustFrameworkBase.xml file to your TrustFrameworkExtensions.xml file inside the `<UserJourneys>` element.</span></span> <span data-ttu-id="2a42e-154">Ardından 6. adım altında değişiklik yapın.</span><span class="sxs-lookup"><span data-stu-id="2a42e-154">Then make the modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="2a42e-155">Sipariş sürümünüzü eşleşmiyorsa, önce adım olarak kod ekleme emin olun `ClaimsExchange` türü `SendClaims`.</span><span class="sxs-lookup"><span data-stu-id="2a42e-155">If the order does not match your version, make sure that you insert the code as the step before the `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="2a42e-156">Kullanıcı gezisine için son XML aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="2a42e-156">The final XML for the user journey should look like this:</span></span>

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
        <!-- Add a step 6 to the user journey before the JWT token is created-->
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

## <a name="step-5-add-the-claim-city-to-your-relying-party-policy-file-so-the-claim-is-sent-to-your-application"></a><span data-ttu-id="2a42e-157">5. adım: talep ekleme `city` bağlı olan taraf için ilke dosya talep uygulamanıza gönderilir şekilde</span><span class="sxs-lookup"><span data-stu-id="2a42e-157">Step 5: Add the claim `city` to your relying party policy file so the claim is sent to your application</span></span>

<span data-ttu-id="2a42e-158">ProfileEdit.xml bağlı olan taraf (RP) dosyanızı düzenleyin ve değiştirme `<TechnicalProfile Id="PolicyProfile">` öğesi aşağıdakileri ekleyin: `<OutputClaim ClaimTypeReferenceId="city" />`.</span><span class="sxs-lookup"><span data-stu-id="2a42e-158">Edit your ProfileEdit.xml relying party (RP) file and modify the `<TechnicalProfile Id="PolicyProfile">` element to add the following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="2a42e-159">Yeni Talep ekledikten sonra teknik profili şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="2a42e-159">After you add the new claim, the technical profile looks like this:</span></span>

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

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="2a42e-160">6. adım: değişikliklerinizi karşıya yüklemek ve test etme</span><span class="sxs-lookup"><span data-stu-id="2a42e-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="2a42e-161">İlkenin mevcut sürümlerin üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="2a42e-161">Overwrite the existing versions of the policy.</span></span>

1.  <span data-ttu-id="2a42e-162">(İsteğe bağlı:) Devam etmeden önce mevcut sürümü (yükleyerek) uzantıları dosyanızın kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2a42e-162">(Optional:) Save the existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="2a42e-163">İlk karmaşıklık düşük tutmak için birden fazla sürümünü uzantıları dosya karşıya yüklemeyin öneririz.</span><span class="sxs-lookup"><span data-stu-id="2a42e-163">To keep the initial complexity low, we recommend that you do not upload multiple versions of the extensions file.</span></span>
2.  <span data-ttu-id="2a42e-164">(İsteğe bağlı:) İlke Kimliği İlkesi Düzenle dosyası için yeni sürümü değiştirerek yeniden adlandırın `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="2a42e-164">(Optional:) Rename the new version of the policy ID for the policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="2a42e-165">Uzantıları dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2a42e-165">Upload the extensions file.</span></span>
4.  <span data-ttu-id="2a42e-166">İlkeyi Düzenle RP dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2a42e-166">Upload the policy edit RP file.</span></span>
5.  <span data-ttu-id="2a42e-167">Kullanım **Şimdi Çalıştır** ilkesini test etmek.</span><span class="sxs-lookup"><span data-stu-id="2a42e-167">Use **Run Now** to test the policy.</span></span> <span data-ttu-id="2a42e-168">Uygulamaya IEF döndüren belirteci gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="2a42e-168">Review the token that the IEF returns to the application.</span></span>

<span data-ttu-id="2a42e-169">Her şeyin doğru şekilde ayarlanmış olması durumunda, yeni talep belirteci içerecektir `city`, değerle `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="2a42e-169">If everything is set up correctly, the token will include the new claim `city`, with the value `Redmond`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2a42e-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2a42e-170">Next steps</span></span>

[<span data-ttu-id="2a42e-171">Doğrulama adımı olarak REST API kullanın</span><span class="sxs-lookup"><span data-stu-id="2a42e-171">Use a REST API as a validation step</span></span>](active-directory-b2c-rest-api-validation-custom.md)

[<span data-ttu-id="2a42e-172">Kullanıcılardan ek bilgi toplamak için profil düzenleme değiştirme</span><span class="sxs-lookup"><span data-stu-id="2a42e-172">Modify the profile edit to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
