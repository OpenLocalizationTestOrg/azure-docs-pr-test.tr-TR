---
title: "MFA Yazılım Geliştirme Seti özel uygulamalar için | Microsoft Docs"
description: "Bu makalede karşıdan yükleme ve özel uygulamalarınız için iki aşamalı doğrulamayı etkinleştirmek için Azure MFA SDK'sını kullanma gösterilmektedir."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 281f9c61a30a20027f69808600373aa272255ef6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a><span data-ttu-id="ca570-103">Yapı multi-Factor Authentication özel uygulamalar (SDK)</span><span class="sxs-lookup"><span data-stu-id="ca570-103">Building Multi-Factor Authentication into Custom Apps (SDK)</span></span>

<span data-ttu-id="ca570-104">Azure çok faktörlü kimlik doğrulaması Yazılım Geliştirme Seti (SDK) iki aşamalı doğrulama özelliklerini doğrudan oturum açma veya işlem işlemler Azure AD kiracınıza uygulamaların oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca570-104">The Azure Multi-Factor Authentication Software Development Kit (SDK) lets you build two-step verification directly into the sign-in or transaction processes of applications in your Azure AD tenant.</span></span>

<span data-ttu-id="ca570-105">Multi-Factor Authentication SDK'sı, C#, Visual Basic (.NET), Java, Perl, PHP ve Ruby için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ca570-105">The Multi-Factor Authentication SDK is available for C#, Visual Basic (.NET), Java, Perl, PHP, and Ruby.</span></span> <span data-ttu-id="ca570-106">SDK, iki aşamalı doğrulamayı çevresinde ince bir sarmalayıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca570-106">The SDK provides a thin wrapper around two-step verification.</span></span> <span data-ttu-id="ca570-107">Açıklamalı kaynak kodu dosyaları, örneğin dosyaları ve ayrıntılı bir benioku dosyası da dahil olmak üzere, kodunuzu yazma için gereken her şeyi içerir.</span><span class="sxs-lookup"><span data-stu-id="ca570-107">It includes everything you need to write your code, including commented source code files, example files, and a detailed ReadMe file.</span></span> <span data-ttu-id="ca570-108">Her SDK ayrıca bir sertifika ve çok faktörlü kimlik doğrulama sağlayıcınızı benzersiz işlemleri şifreleme için özel anahtarı içerir.</span><span class="sxs-lookup"><span data-stu-id="ca570-108">Each SDK also includes a certificate and private key for encrypting transactions that are unique to your Multi-Factor Authentication Provider.</span></span> <span data-ttu-id="ca570-109">Bir sağlayıcı sahip olduğu sürece, gerektiği kadar çok dil ve biçimleri SDK'da indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca570-109">As long as you have a provider, you can download the SDK in as many languages and formats as you need.</span></span>

<span data-ttu-id="ca570-110">Multi-Factor Authentication SDK'sı API'lerinde yapısını basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="ca570-110">The structure of the APIs in the Multi-Factor Authentication SDK is simple.</span></span> <span data-ttu-id="ca570-111">Tek bir işlevi çok faktörlü seçeneği parametreleri (gibi doğrulama modu) ve kullanıcı verilerini (örneğin, çağırmak için telefon numarası veya doğrulamak için PIN numarası) ile bir API çağrısı yapın.</span><span class="sxs-lookup"><span data-stu-id="ca570-111">Make a single function call to an API with the multi-factor option parameters (like verification mode) and user data (like the telephone number to call or the PIN number to validate).</span></span> <span data-ttu-id="ca570-112">API web hizmetleri istekleri içine işlev çağrısı için bulut tabanlı Azure çok faktörlü kimlik doğrulama hizmeti çevir.</span><span class="sxs-lookup"><span data-stu-id="ca570-112">The APIs translate the function call into web services requests to the cloud-based Azure Multi-Factor Authentication Service.</span></span> <span data-ttu-id="ca570-113">Tüm çağrılar her SDK'da bulunan özel sertifika için bir başvuru eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca570-113">All calls must include a reference to the private certificate that is included in every SDK.</span></span>

<span data-ttu-id="ca570-114">API'ler Azure Active Directory'de kayıtlı kullanıcılara erişimi olmadığı için bir dosya veya veritabanı kullanıcı bilgilerini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca570-114">Because the APIs do not have access to users registered in Azure Active Directory, you must provide user information in a file or database.</span></span> <span data-ttu-id="ca570-115">Ayrıca, bu işlemlerin uygulamanıza oluşturmak gereken şekilde API'leri kayıt ya da kullanıcı yönetimi özelliklerini sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="ca570-115">Also, the APIs do not provide enrollment or user management features, so you need to build these processes into your application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca570-116">SDK’yı indirmek için Azure MFA, AAD Premium veya EMS lisanslarınız olsa bile bir Azure Multi-Factor Auth Sağlayıcısı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca570-116">To download the SDK, you need to create an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span> <span data-ttu-id="ca570-117">Bu amaç için Azure multi-Factor Auth sağlayıcısı oluşturmak ve lisansları zaten varsa, sağlayıcı ile oluşturduğunuzdan emin olun **etkin kullanıcı başına** modeli.</span><span class="sxs-lookup"><span data-stu-id="ca570-117">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, make sure to create the Provider with the **Per Enabled User** model.</span></span> <span data-ttu-id="ca570-118">Ardından, Sağlayıcıyı Azure MFA, Azure AD Premium veya EMS lisansları içeren dizine bağlayın.</span><span class="sxs-lookup"><span data-stu-id="ca570-118">Then, link the Provider to the directory that contains the Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="ca570-119">Bu yapılandırma, sahip olduğunuz lisans sayısından SDK'sını kullanarak daha fazla benzersiz kullanıcı varsa, yalnızca faturalandırılır olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca570-119">This configuration ensures that you are only billed if you have more unique users using the SDK than the number of licenses you own.</span></span>


## <a name="download-the-sdk"></a><span data-ttu-id="ca570-120">SDK'sını indirin</span><span class="sxs-lookup"><span data-stu-id="ca570-120">Download the SDK</span></span>
<span data-ttu-id="ca570-121">Azure çok faktörlü SDK'sını indirme gerektiren bir [Azure multi-Factor Auth sağlayıcısı](multi-factor-authentication-get-started-auth-provider.md).</span><span class="sxs-lookup"><span data-stu-id="ca570-121">Downloading the Azure Multi-Factor SDK requires an [Azure Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md).</span></span>  <span data-ttu-id="ca570-122">Azure MFA, Azure AD Premium veya Enterprise Mobility Suite lisansları ait olsa bile bu tam Azure aboneliği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ca570-122">This requires a full Azure subscription, even if Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses are owned.</span></span>  <span data-ttu-id="ca570-123">SDK'yi karşıdan yüklemek için çok faktörlü Yönetim Portalı'na gidin.</span><span class="sxs-lookup"><span data-stu-id="ca570-123">To download the SDK, navigate to the Multi-Factor Management Portal.</span></span> <span data-ttu-id="ca570-124">Portal ya da multi-Factor Auth sağlayıcısı doğrudan yönetme veya tıklatarak ulaşabilirsiniz **"Portal'a Git"** MFA hizmet ayarları sayfasında bağlantı.</span><span class="sxs-lookup"><span data-stu-id="ca570-124">You can reach the portal either by managing the Multi-Factor Auth Provider directly, or by clicking the **"Go to the portal"** link on the MFA service settings page.</span></span>

### <a name="download-from-the-azure-classic-portal"></a><span data-ttu-id="ca570-125">Azure Klasik Portalı'ndan indirin</span><span class="sxs-lookup"><span data-stu-id="ca570-125">Download from the Azure classic portal</span></span>
1. <span data-ttu-id="ca570-126">[Klasik Azure portalında](https://manage.windowsazure.com) Yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ca570-126">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="ca570-127">Sol taraftaki **Active Directory** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="ca570-127">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="ca570-128">Active Directory sayfasında, en üst seçin **çok faktörlü kimlik doğrulama sağlayıcıları**</span><span class="sxs-lookup"><span data-stu-id="ca570-128">On the Active Directory page, at the top select **Multi-Factor Auth Providers**</span></span>
4. <span data-ttu-id="ca570-129">Pencerenin alt seçin **Yönet**.</span><span class="sxs-lookup"><span data-stu-id="ca570-129">At the bottom select **Manage**.</span></span> <span data-ttu-id="ca570-130">Yeni bir sayfa açılır.</span><span class="sxs-lookup"><span data-stu-id="ca570-130">A new page opens.</span></span>
5. <span data-ttu-id="ca570-131">Alt, sol tıklayın **SDK**.</span><span class="sxs-lookup"><span data-stu-id="ca570-131">On the left, at the bottom, click **SDK**.</span></span>
   <span data-ttu-id="ca570-132"><center>![İndirme](./media/multi-factor-authentication-sdk/download.png)</center></span><span class="sxs-lookup"><span data-stu-id="ca570-132"><center>![Download](./media/multi-factor-authentication-sdk/download.png)</center></span></span>
6. <span data-ttu-id="ca570-133">İstediğiniz ve ilişkili indirme bağlantıları tıklatın dili seçin.</span><span class="sxs-lookup"><span data-stu-id="ca570-133">Select the language you want and click one the associated download links.</span></span>
7. <span data-ttu-id="ca570-134">İndirmeyi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ca570-134">Save the download.</span></span>

### <a name="download-from-the-service-settings"></a><span data-ttu-id="ca570-135">Hizmet ayarlarını indirme</span><span class="sxs-lookup"><span data-stu-id="ca570-135">Download from the service settings</span></span>
1. <span data-ttu-id="ca570-136">[Klasik Azure portalında](https://manage.windowsazure.com) Yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ca570-136">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="ca570-137">Sol taraftaki **Active Directory** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="ca570-137">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="ca570-138">Azure AD örneğinize çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca570-138">Double-click your instance of Azure AD.</span></span>
4. <span data-ttu-id="ca570-139">Üst kısımda **Yapılandır**’a tıklayın</span><span class="sxs-lookup"><span data-stu-id="ca570-139">At the top click **Configure**</span></span>
5. <span data-ttu-id="ca570-140">Çok faktörlü kimlik doğrulaması altında seçin **hizmet ayarlarını Yönet**
   ![indirin](./media/multi-factor-authentication-sdk/download2.png)</span><span class="sxs-lookup"><span data-stu-id="ca570-140">Under multi-factor authentication, select **Manage service settings**
![Download](./media/multi-factor-authentication-sdk/download2.png)</span></span>
6. <span data-ttu-id="ca570-141">Hizmetleri ayarları sayfasında, ekranın alt kısmında **Portal'a git**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca570-141">On the services settings page, at the bottom of the screen click **Go to the portal**.</span></span> <span data-ttu-id="ca570-142">Yeni bir sayfa açılır.</span><span class="sxs-lookup"><span data-stu-id="ca570-142">A new page opens.</span></span>
   <span data-ttu-id="ca570-143">![İndir](./media/multi-factor-authentication-sdk/download3a.png)</span><span class="sxs-lookup"><span data-stu-id="ca570-143">![Download](./media/multi-factor-authentication-sdk/download3a.png)</span></span>
7. <span data-ttu-id="ca570-144">Alt, sol tıklayın **SDK**.</span><span class="sxs-lookup"><span data-stu-id="ca570-144">On the left, at the bottom, click **SDK**.</span></span>
8. <span data-ttu-id="ca570-145">İstediğiniz ve ilişkili indirme bağlantıları tıklatın dili seçin.</span><span class="sxs-lookup"><span data-stu-id="ca570-145">Select the language you want and click one the associated download links.</span></span>
9. <span data-ttu-id="ca570-146">İndirmeyi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ca570-146">Save the download.</span></span>

## <a name="whats-in-the-sdk"></a><span data-ttu-id="ca570-147">SDK'ın nedir</span><span class="sxs-lookup"><span data-stu-id="ca570-147">What's in the SDK</span></span>
<span data-ttu-id="ca570-148">SDK'yı aşağıdaki öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="ca570-148">The SDK includes the following items:</span></span>

* <span data-ttu-id="ca570-149">**BENİOKU**.</span><span class="sxs-lookup"><span data-stu-id="ca570-149">**README**.</span></span> <span data-ttu-id="ca570-150">Yeni veya var olan bir uygulama içinde çok faktörlü kimlik doğrulaması API'leri kullanımı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ca570-150">Explains how to use the Multi-Factor Authentication APIs in a new or existing application.</span></span>
* <span data-ttu-id="ca570-151">**Kaynak dosyaları** çok faktörlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ca570-151">**Source files** for Multi-Factor Authentication</span></span>
* <span data-ttu-id="ca570-152">**İstemci sertifikası** multi-Factor Authentication hizmetiyle iletişim kurmak için kullandıkları</span><span class="sxs-lookup"><span data-stu-id="ca570-152">**Client certificate** that you use to communicate with the Multi-Factor Authentication service</span></span>
* <span data-ttu-id="ca570-153">**Özel anahtarı** sertifika için</span><span class="sxs-lookup"><span data-stu-id="ca570-153">**Private key** for the certificate</span></span>
* <span data-ttu-id="ca570-154">**Çağrı sonuçları.**</span><span class="sxs-lookup"><span data-stu-id="ca570-154">**Call results.**</span></span> <span data-ttu-id="ca570-155">Arama sonuç kodları listesi.</span><span class="sxs-lookup"><span data-stu-id="ca570-155">A list of call result codes.</span></span> <span data-ttu-id="ca570-156">Bu dosyayı açmak için WordPad gibi biçimlendirme metin içeren bir uygulama kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca570-156">To open this file, use an application with text formatting, such as WordPad.</span></span> <span data-ttu-id="ca570-157">Test ve uygulamanızı multi-Factor Authentication uygulamasında sorun gidermek için arama sonuç kodları kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca570-157">Use the call result codes to test and troubleshoot the implementation of Multi-Factor Authentication in your application.</span></span> <span data-ttu-id="ca570-158">Kimlik doğrulama durum kodları değiller.</span><span class="sxs-lookup"><span data-stu-id="ca570-158">They are not authentication status codes.</span></span>
* <span data-ttu-id="ca570-159">**Örnekler.**</span><span class="sxs-lookup"><span data-stu-id="ca570-159">**Examples.**</span></span> <span data-ttu-id="ca570-160">Temel çalışma uygulamasını çok faktörlü kimlik doğrulaması için örnek kod.</span><span class="sxs-lookup"><span data-stu-id="ca570-160">Sample code for a basic working implementation of Multi-Factor Authentication.</span></span>

> [!WARNING]
> <span data-ttu-id="ca570-161">İstemci sertifikası, özellikle sizin için oluşturulan benzersiz bir özel sertifikasıdır.</span><span class="sxs-lookup"><span data-stu-id="ca570-161">The client certificate is a unique private certificate that was generated especially for you.</span></span> <span data-ttu-id="ca570-162">Paylaşım değil veya bu dosyayı kaybedersiniz.</span><span class="sxs-lookup"><span data-stu-id="ca570-162">Do not share or lose this file.</span></span> <span data-ttu-id="ca570-163">Bu multi-Factor Authentication hizmetiyle, iletişimin güvenliğini sağlamak için anahtardır.</span><span class="sxs-lookup"><span data-stu-id="ca570-163">It’s your key to ensuring the security of your communications with the Multi-Factor Authentication service.</span></span>

## <a name="code-sample"></a><span data-ttu-id="ca570-164">Kod örneği</span><span class="sxs-lookup"><span data-stu-id="ca570-164">Code sample</span></span>
<span data-ttu-id="ca570-165">Bu kod örneği API'leri Azure multi-Factor Authentication SDK'sı Standart mod sesli arama doğrulama uygulamanıza eklemek için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca570-165">This code sample shows you how to use the APIs in the Azure Multi-Factor Authentication SDK to add standard mode voice call verification to your application.</span></span> <span data-ttu-id="ca570-166">Standart mod kullanıcı için # tuşuna basarak yanıt bir telefon çağrısı içindir.</span><span class="sxs-lookup"><span data-stu-id="ca570-166">Standard mode is a telephone call that the user responds to by pressing the # key.</span></span>

<span data-ttu-id="ca570-167">Bu örnek, C# sunucu tarafı mantığı ile temel bir ASP.NET uygulamasında C# .NET 2.0 çok faktörlü kimlik doğrulaması SDK kullanır, ancak diğer dillerde benzer bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="ca570-167">This example uses the C# .NET 2.0 Multi-Factor Authentication SDK in a basic ASP.NET application with C# server-side logic, but the process is similar in other languages.</span></span> <span data-ttu-id="ca570-168">SDK kaynak dosyaları, değil yürütülebilir dosyaları, içerdiğinden dosyaları oluşturmak ve bunları başvuru veya doğrudan uygulamanızda içermiyor.</span><span class="sxs-lookup"><span data-stu-id="ca570-168">Because the SDK includes source files, not executable files, you can build the files and reference them or include them directly in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="ca570-169">Çok faktörlü kimlik doğrulamasını yaparken, ek bir yöntem (telefon araması veya kısa mesaj) ikincil veya üçüncül doğrulama birincil kimlik doğrulama yöntemi (kullanıcı adı ve parola) desteklemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca570-169">When implementing Multi-Factor Authentication, use the additional methods (phone call or text message) as secondary or tertiary verification to supplement your primary authentication method (username and password).</span></span> <span data-ttu-id="ca570-170">Bu yöntemler, birincil kimlik doğrulama yöntemi olarak tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="ca570-170">These methods are not designed as primary authentication methods.</span></span>

### <a name="code-sample-overview"></a><span data-ttu-id="ca570-171">Kod örnek genel bakış</span><span class="sxs-lookup"><span data-stu-id="ca570-171">Code Sample Overview</span></span>
<span data-ttu-id="ca570-172">Bu örnek kod basit bir web demo uygulaması için bir telefon çağrısı kullanıcının kimlik doğrulamasını doğrulamak için # anahtar yanıtta kullanır.</span><span class="sxs-lookup"><span data-stu-id="ca570-172">This sample code for a simple web demo application uses a telephone call with a # key response to verify the user's authentication.</span></span> <span data-ttu-id="ca570-173">Bu telefon görüşmesi faktörü çok faktörlü kimlik doğrulaması Standart modu olarak bilinir.</span><span class="sxs-lookup"><span data-stu-id="ca570-173">This telephone call factor is known in Multi-Factor Authentication as standard mode.</span></span>

<span data-ttu-id="ca570-174">İstemci tarafı kodlar tüm çok faktörlü kimlik doğrulaması özgü öğeleri içermez.</span><span class="sxs-lookup"><span data-stu-id="ca570-174">The client-side code does not include any Multi-Factor Authentication-specific elements.</span></span> <span data-ttu-id="ca570-175">Ek kimlik doğrulama faktörleri birincil kimlik doğrulaması için bağımsız olduğundan, varolan oturum açma arabirimi değiştirmeden ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca570-175">Because the additional authentication factors are independent of the primary authentication, you can add them without changing the existing sign-on interface.</span></span> <span data-ttu-id="ca570-176">Çok faktörlü SDK API'leri, kullanıcı deneyimini özelleştirmesini sağlar, ancak hiç değişikliği gerekmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="ca570-176">The APIs in the Multi-Factor SDK let you customize the user experience, but you might not need to change anything at all.</span></span>

<span data-ttu-id="ca570-177">Sunucu tarafı kodu, adım 2'de Standart mod kimlik doğrulaması ekler.</span><span class="sxs-lookup"><span data-stu-id="ca570-177">The server-side code adds standard-mode authentication in Step 2.</span></span> <span data-ttu-id="ca570-178">Standart mod doğrulama için gerekli olan parametrelere sahip bir PfAuthParams nesnesi oluşturur: kullanıcı adı, telefon numarası ve mod ve her çağrıda gerekli olan istemci sertifikası (CertFilePath) yolu.</span><span class="sxs-lookup"><span data-stu-id="ca570-178">It creates a PfAuthParams object with the parameters that are required for standard-mode verification: username, telephone number, and mode, and the path to the client certificate (CertFilePath), which is required in each call.</span></span> <span data-ttu-id="ca570-179">PfAuthParams tüm parametreleri tanıtımı için SDK'sındaki örnek dosyasına bakın.</span><span class="sxs-lookup"><span data-stu-id="ca570-179">For a demonstration of all parameters in PfAuthParams, see the Example file in the SDK.</span></span>

<span data-ttu-id="ca570-180">Ardından, kod PfAuthParams nesnesi pf_authenticate() işleve iletir.</span><span class="sxs-lookup"><span data-stu-id="ca570-180">Next, the code passes the PfAuthParams object to the pf_authenticate() function.</span></span> <span data-ttu-id="ca570-181">Başarı veya başarısızlık kimlik doğrulamasının dönüş değerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca570-181">The return value indicates the success or failure of the authentication.</span></span> <span data-ttu-id="ca570-182">Parametreler, callStatus ve errorID ek arama sonucu bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="ca570-182">The out parameters, callStatus, and errorID, contain additional call result information.</span></span> <span data-ttu-id="ca570-183">Arama sonuç kodları SDK arama sonuçları dosyasında belgelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="ca570-183">The call result codes are documented in the call results file in the SDK.</span></span>

<span data-ttu-id="ca570-184">Bu en az uygulama birkaç satırda yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="ca570-184">This minimal implementation can be written in a few lines.</span></span> <span data-ttu-id="ca570-185">Ancak, üretim kodunda, daha gelişmiş hata işleme, ek veritabanı kodu ve geliştirilmiş bir kullanıcı deneyimi içerir.</span><span class="sxs-lookup"><span data-stu-id="ca570-185">However, in production code, you would include more sophisticated error handling, additional database code, and an enhanced user experience.</span></span>

### <a name="web-client-code"></a><span data-ttu-id="ca570-186">Web istemci kodu</span><span class="sxs-lookup"><span data-stu-id="ca570-186">Web Client Code</span></span>
<span data-ttu-id="ca570-187">Bir tanıtım sayfası için web istemci kodu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ca570-187">The following is web client code for a demo page.</span></span>

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a><span data-ttu-id="ca570-188">Sunucu Tarafında Çalışan Kod</span><span class="sxs-lookup"><span data-stu-id="ca570-188">Server-Side Code</span></span>
<span data-ttu-id="ca570-189">Aşağıdaki sunucu tarafı kodu, çok faktörlü kimlik doğrulaması yapılandırılan ve 2. adımda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ca570-189">In the following server-side code, Multi-Factor Authentication is configured and run in Step 2.</span></span> <span data-ttu-id="ca570-190">Standart mod (MODE_STANDARD) kullanıcı # tuşuna basarak yanıtının bir telefon çağrısı içindir.</span><span class="sxs-lookup"><span data-stu-id="ca570-190">Standard mode (MODE_STANDARD) is a telephone call to which the user responds by pressing the # key.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate the username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from the user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains the private key for the client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }
