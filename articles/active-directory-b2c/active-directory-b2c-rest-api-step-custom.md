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
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="8afc3-103">İzlenecek yol: Azure AD B2C kullanıcı Yolculuğunuzun REST API talep alışverişlerine orchestration adım olarak tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="8afc3-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="8afc3-104">Hello Azure Active Directory B2C altını çizen kimlik deneyimi Framework (IEF) (Azure AD B2C) hello kimlik Geliştirici toointegrate kullanıcı gezisine bir RESTful API'si ile etkileşim sağlar.</span><span class="sxs-lookup"><span data-stu-id="8afc3-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="8afc3-105">Bu kılavuzda Hello sonunda mümkün toocreate RESTful hizmetlerle etkileşimde bulunan bir Azure AD B2C kullanıcı gezisine olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8afc3-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="8afc3-106">Merhaba IEF Taleplerde verileri gönderir ve geri Taleplerde verilerini alır.</span><span class="sxs-lookup"><span data-stu-id="8afc3-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="8afc3-107">REST API talep exchange Hello:</span><span class="sxs-lookup"><span data-stu-id="8afc3-107">hello REST API claims exchange:</span></span>

- <span data-ttu-id="8afc3-108">Orchestration adım olarak tasarlanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="8afc3-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="8afc3-109">Bir dış eylem tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="8afc3-109">Can trigger an external action.</span></span> <span data-ttu-id="8afc3-110">Örneğin, bir olay dış veritabanında kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8afc3-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="8afc3-111">Kullanılan toofetch bir değer olması ve hello kullanıcı veritabanında depolamak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8afc3-111">Can be used toofetch a value and then store it in hello user database.</span></span>

<span data-ttu-id="8afc3-112">Alınan hello talepleri kullanan sonraki toochange hello akışını.</span><span class="sxs-lookup"><span data-stu-id="8afc3-112">You can use hello received claims later toochange hello flow of execution.</span></span>

<span data-ttu-id="8afc3-113">Bir doğrulama profili olarak hello etkileşim de tasarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8afc3-113">You can also design hello interaction as a validation profile.</span></span> <span data-ttu-id="8afc3-114">Daha fazla bilgi için bkz: [izlenecek yol: REST API tümleştirme kullanıcı girişini doğrulama olarak Azure AD B2C kullanıcı Yolculuğunuzun alışverişlerine talep](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="8afc3-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="8afc3-115">Merhaba senaryo, bir kullanıcı profili Düzenle gerçekleştirdiğinde, istediğimizi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="8afc3-115">hello scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="8afc3-116">Merhaba kullanıcı bir dış sistemde arayın.</span><span class="sxs-lookup"><span data-stu-id="8afc3-116">Look up hello user in an external system.</span></span>
2. <span data-ttu-id="8afc3-117">Bu kullanıcının, kayıtlı hello Şehir alın.</span><span class="sxs-lookup"><span data-stu-id="8afc3-117">Get hello city where that user is registered.</span></span>
3. <span data-ttu-id="8afc3-118">Bu öznitelik toohello uygulama talep olarak döndürür.</span><span class="sxs-lookup"><span data-stu-id="8afc3-118">Return that attribute toohello application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8afc3-119">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8afc3-119">Prerequisites</span></span>

- <span data-ttu-id="8afc3-120">Azure AD B2C Kiracı yapılandırılmış toocomplete oturumu-up/oturum açıklandığı gibi açma, yerel bir hesap [Başlarken](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="8afc3-120">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="8afc3-121">REST API uç noktası toointeract ile.</span><span class="sxs-lookup"><span data-stu-id="8afc3-121">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="8afc3-122">Bu kılavuzda, bir basit Azure işlevi app Web kancası örnek olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8afc3-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="8afc3-123">*Önerilen*: tam hello [REST API talep exchange izlenecek bir doğrulama adımı olarak](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="8afc3-123">*Recommended*: Complete hello [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="8afc3-124">1. adım: hello REST API işlevi hazırlama</span><span class="sxs-lookup"><span data-stu-id="8afc3-124">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="8afc3-125">REST API işlevleri bu makalenin kapsamı dışındadır hello kurulması.</span><span class="sxs-lookup"><span data-stu-id="8afc3-125">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="8afc3-126">[Azure işlevleri](https://docs.microsoft.com/azure/azure-functions/functions-reference) toocreate RESTful hizmetlerini hello bulutta mükemmel bir araç sağlar.</span><span class="sxs-lookup"><span data-stu-id="8afc3-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="8afc3-127">Adlı bir talep aldığında bir Azure işlevi ayarlarız `email`, ve ardından talep döndürür hello `city` , atanan hello değeriyle `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="8afc3-127">We have set up an Azure function that receives a claim called `email`, and then returns hello claim `city` with hello assigned value of `Redmond`.</span></span> <span data-ttu-id="8afc3-128">Merhaba örnek Azure işlevi açıktır [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="8afc3-128">hello sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="8afc3-129">Merhaba `userMessage` Azure işlev dönüşleri hello talep bu bağlamda isteğe bağlıdır ve hello IEF bunu yoksayacaktır.</span><span class="sxs-lookup"><span data-stu-id="8afc3-129">hello `userMessage` claim that hello Azure function returns is optional in this context, and hello IEF will ignore it.</span></span> <span data-ttu-id="8afc3-130">Bir ileti toohello uygulama geçirilen ve toohello kullanıcı daha sonra sunulan, potansiyel olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8afc3-130">You can potentially use it as a message passed toohello application and presented toohello user later.</span></span>

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

<span data-ttu-id="8afc3-131">Bir Azure işlevi uygulama hello belirli bir işlev hello tanımlayıcısını içeren kolay tooget hello işlevi URL kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="8afc3-131">An Azure function app makes it easy tooget hello function URL, which includes hello identifier of hello specific function.</span></span> <span data-ttu-id="8afc3-132">Bu durumda, hello URL'dir: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span><span class="sxs-lookup"><span data-stu-id="8afc3-132">In this case, hello URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="8afc3-133">Bunu test etmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8afc3-133">You can use it for testing.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="8afc3-134">2. adım: hello RESTful API'si talep exchange TrustFrameworExtensions.xml dosyanızdaki teknik bir profil olarak yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8afc3-134">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="8afc3-135">Teknik bir profili hello tam hello Exchange hello RESTful hizmeti ile istenen bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="8afc3-135">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="8afc3-136">Merhaba TrustFrameworkExtensions.xml dosyasını açın ve aşağıdaki XML parçacığını hello içinde hello ekleyin `<ClaimsProvider>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="8afc3-136">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="8afc3-137">XML, RESTful sağlayıcısı aşağıdaki hello içinde `Version=1.0.0.0` hello protokolü olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="8afc3-137">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="8afc3-138">Merhaba dış hizmetiyle etkileşime gireceğini hello işlevi olarak düşünün.</span><span class="sxs-lookup"><span data-stu-id="8afc3-138">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

<span data-ttu-id="8afc3-139">Merhaba `<InputClaims>` öğesi IEF toohello REST hizmeti hello gönderilecek hello talepleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8afc3-139">hello `<InputClaims>` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="8afc3-140">Bu örnekte, hello hello talep içeriğini `givenName` toohello REST hizmeti hello talep olarak gönderilecek `email`.</span><span class="sxs-lookup"><span data-stu-id="8afc3-140">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as hello claim `email`.</span></span>  

<span data-ttu-id="8afc3-141">Merhaba `<OutputClaims>` öğesi IEF hello REST hizmetinden beklediğiniz bu hello hello talepleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8afc3-141">hello `<OutputClaims>` element defines hello claims that hello IEF will expect from hello REST service.</span></span> <span data-ttu-id="8afc3-142">Alınan talep Hello sayısından bağımsız olarak, hello IEF yalnızca tanımlanan burada kullanır.</span><span class="sxs-lookup"><span data-stu-id="8afc3-142">Regardless of hello number of claims that are received, hello IEF will use only those identified here.</span></span> <span data-ttu-id="8afc3-143">Bu örnekte, olarak bir talep alınan `city` eşlenen tooan IEF talep çağrılacağı `city`.</span><span class="sxs-lookup"><span data-stu-id="8afc3-143">In this example, a claim received as `city` will be mapped tooan IEF claim called `city`.</span></span>

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="8afc3-144">3. adım: hello yeni talep ekleme `city` TrustFrameworkExtensions.xml dosyanızı toohello şeması</span><span class="sxs-lookup"><span data-stu-id="8afc3-144">Step 3: Add hello new claim `city` toohello schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="8afc3-145">Merhaba talep `city` henüz herhangi bir yere bizim şemada tanımlı değil.</span><span class="sxs-lookup"><span data-stu-id="8afc3-145">hello claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="8afc3-146">Bu nedenle, bir tanım hello öğesinin içine ekleyin `<BuildingBlocks>`.</span><span class="sxs-lookup"><span data-stu-id="8afc3-146">So, add a definition inside hello element `<BuildingBlocks>`.</span></span> <span data-ttu-id="8afc3-147">Bu öğe hello TrustFrameworkExtensions.xml dosyasının hello başında bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8afc3-147">You can find this element at hello beginning of hello TrustFrameworkExtensions.xml file.</span></span>

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

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="8afc3-148">4. adım: Profil düzenleme kullanıcı Yolculuğunuzun TrustFrameworkExtensions.xml içinde orchestration adımda olarak hello REST Hizmeti talepleri exchange Ekle</span><span class="sxs-lookup"><span data-stu-id="8afc3-148">Step 4: Include hello REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="8afc3-149">Bir adım eklemek hello kullanıcı sonra toohello profil düzenleme kullanıcı gezisine (1-4 XML aşağıdaki hello içinde düzenleme adımlarının) kimlik doğrulaması ve hello kullanıcı güncelleştirilmiş hello profil bilgilerini (5. adım) sağlanan.</span><span class="sxs-lookup"><span data-stu-id="8afc3-149">Add a step toohello profile edit user journey, after hello user has been authenticated (orchestration steps 1-4 in hello following XML) and hello user has provided hello updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="8afc3-150">Merhaba REST API çağrısı orchestration adım olarak kullanıldığı birçok kullanım örnekleri vardır.</span><span class="sxs-lookup"><span data-stu-id="8afc3-150">There are many use cases where hello REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="8afc3-151">Orchestration adım olarak, bir kullanıcı ilk kez kayıt gibi bir görevi başarıyla tamamlandıktan sonra bir güncelleştirme tooan dış sistem kullanılabilir veya bir profil olarak eşitlenen tookeep bilgilerini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8afc3-151">As an orchestration step, it can be used as an update tooan external system after a user has successfully completed a task like first-time registration, or as a profile update tookeep information synchronized.</span></span> <span data-ttu-id="8afc3-152">Bu durumda, onu hello profil düzenledikten sonra toohello uygulama sağlanan kullanılan tooaugment hello bilgilerdir.</span><span class="sxs-lookup"><span data-stu-id="8afc3-152">In this case, it's used tooaugment hello information provided toohello application after hello profile edit.</span></span>

<span data-ttu-id="8afc3-153">Kopyalama hello profil düzenleme kullanıcı gezisine XML hello TrustFrameworkBase.xml tooyour TrustFrameworkExtensions.xml dosyası hello içinde kodundan `<UserJourneys>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="8afc3-153">Copy hello profile edit user journey XML code from hello TrustFrameworkBase.xml file tooyour TrustFrameworkExtensions.xml file inside hello `<UserJourneys>` element.</span></span> <span data-ttu-id="8afc3-154">Daha sonra 6. adım altında hello değişiklik yapın.</span><span class="sxs-lookup"><span data-stu-id="8afc3-154">Then make hello modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="8afc3-155">Merhaba sipariş sürümünüzü eşleşmiyorsa hello önce hello adım olarak hello kod yerleştirdiğinizden emin olun `ClaimsExchange` türü `SendClaims`.</span><span class="sxs-lookup"><span data-stu-id="8afc3-155">If hello order does not match your version, make sure that you insert hello code as hello step before hello `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="8afc3-156">Merhaba son XML hello kullanıcı gezisine için aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="8afc3-156">hello final XML for hello user journey should look like this:</span></span>

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

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a><span data-ttu-id="8afc3-157">5. adım: hello talep ekleme `city` tooyour bağlı olan taraf İlkesi dosya hello talep tooyour uygulama gönderilir şekilde</span><span class="sxs-lookup"><span data-stu-id="8afc3-157">Step 5: Add hello claim `city` tooyour relying party policy file so hello claim is sent tooyour application</span></span>

<span data-ttu-id="8afc3-158">ProfileEdit.xml bağlı olan taraf (RP) dosyanızı düzenleyin ve hello değiştirme `<TechnicalProfile Id="PolicyProfile">` öğesi tooadd hello aşağıdaki: `<OutputClaim ClaimTypeReferenceId="city" />`.</span><span class="sxs-lookup"><span data-stu-id="8afc3-158">Edit your ProfileEdit.xml relying party (RP) file and modify hello `<TechnicalProfile Id="PolicyProfile">` element tooadd hello following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="8afc3-159">Merhaba yeni talep ekledikten sonra hello teknik profili şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="8afc3-159">After you add hello new claim, hello technical profile looks like this:</span></span>

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

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="8afc3-160">6. adım: değişikliklerinizi karşıya yüklemek ve test etme</span><span class="sxs-lookup"><span data-stu-id="8afc3-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="8afc3-161">Merhaba hello İlkesi varolan önceki sürümlerin üzerine yazın.</span><span class="sxs-lookup"><span data-stu-id="8afc3-161">Overwrite hello existing versions of hello policy.</span></span>

1.  <span data-ttu-id="8afc3-162">(İsteğe bağlı:) Devam etmeden önce hello mevcut sürümü (yükleyerek) uzantıları dosyanızın kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8afc3-162">(Optional:) Save hello existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="8afc3-163">tookeep hello ilk karmaşıklık düşük, birden fazla sürümünü hello uzantıları dosyasını karşıya yüklemeyin öneririz.</span><span class="sxs-lookup"><span data-stu-id="8afc3-163">tookeep hello initial complexity low, we recommend that you do not upload multiple versions of hello extensions file.</span></span>
2.  <span data-ttu-id="8afc3-164">(İsteğe bağlı:) Merhaba ilke kimliği hello İlkesi Düzenle dosyası için yeni sürümü Hello değiştirerek yeniden adlandırın `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="8afc3-164">(Optional:) Rename hello new version of hello policy ID for hello policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="8afc3-165">Merhaba uzantıları dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8afc3-165">Upload hello extensions file.</span></span>
4.  <span data-ttu-id="8afc3-166">Hello İlkesi Düzenle RP dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8afc3-166">Upload hello policy edit RP file.</span></span>
5.  <span data-ttu-id="8afc3-167">Kullanım **Şimdi Çalıştır** tootest hello ilkesi.</span><span class="sxs-lookup"><span data-stu-id="8afc3-167">Use **Run Now** tootest hello policy.</span></span> <span data-ttu-id="8afc3-168">IEF hello gözden geçirme hello belirteci toohello uygulama döndürür.</span><span class="sxs-lookup"><span data-stu-id="8afc3-168">Review hello token that hello IEF returns toohello application.</span></span>

<span data-ttu-id="8afc3-169">Her şeyin doğru şekilde ayarlanmış olması durumunda hello belirteci hello yeni talep içerecektir `city`, hello değerle `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="8afc3-169">If everything is set up correctly, hello token will include hello new claim `city`, with hello value `Redmond`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8afc3-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8afc3-170">Next steps</span></span>

[<span data-ttu-id="8afc3-171">Doğrulama adımı olarak REST API kullanın</span><span class="sxs-lookup"><span data-stu-id="8afc3-171">Use a REST API as a validation step</span></span>](active-directory-b2c-rest-api-validation-custom.md)

[<span data-ttu-id="8afc3-172">Hello profil düzenleme toogather ek bilgileri, kullanıcılarınızın değiştirin</span><span class="sxs-lookup"><span data-stu-id="8afc3-172">Modify hello profile edit toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
