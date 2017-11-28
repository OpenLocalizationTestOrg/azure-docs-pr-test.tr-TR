---
title: "özel uygulamalar için aaaMFA Yazılım Geliştirme Seti | Microsoft Docs"
description: "Bu makalede, nasıl Azure MFA SDK tooenable iki aşamalı doğrulamayı özel uygulamalarınız için toodownload ve kullanım hello gösterir."
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
ms.openlocfilehash: 10e02e844bf3928575bfca79dbc34717a31a08b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a><span data-ttu-id="d7428-103">Yapı multi-Factor Authentication özel uygulamalar (SDK)</span><span class="sxs-lookup"><span data-stu-id="d7428-103">Building Multi-Factor Authentication into Custom Apps (SDK)</span></span>

<span data-ttu-id="d7428-104">Azure AD kiracınıza uygulamaların işlem işlemler veya oturum açma hello iki aşamalı doğrulamayı doğrudan yapı hello Azure çok faktörlü kimlik doğrulaması Yazılım Geliştirme Seti (SDK) sağlar.</span><span class="sxs-lookup"><span data-stu-id="d7428-104">hello Azure Multi-Factor Authentication Software Development Kit (SDK) lets you build two-step verification directly into hello sign-in or transaction processes of applications in your Azure AD tenant.</span></span>

<span data-ttu-id="d7428-105">Merhaba multi-Factor Authentication SDK'sı, C#, Visual Basic (.NET), Java, Perl, PHP ve Ruby için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d7428-105">hello Multi-Factor Authentication SDK is available for C#, Visual Basic (.NET), Java, Perl, PHP, and Ruby.</span></span> <span data-ttu-id="d7428-106">Merhaba SDK iki aşamalı doğrulamayı çevresinde ince bir sarmalayıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d7428-106">hello SDK provides a thin wrapper around two-step verification.</span></span> <span data-ttu-id="d7428-107">Açıklamalı kaynak kodu dosyaları, örneğin dosyaları ve ayrıntılı bir benioku dosyası da dahil olmak üzere, kodunuzu toowrite gereken her şeyi içerir.</span><span class="sxs-lookup"><span data-stu-id="d7428-107">It includes everything you need toowrite your code, including commented source code files, example files, and a detailed ReadMe file.</span></span> <span data-ttu-id="d7428-108">Her SDK ayrıca bir sertifika ve benzersiz tooyour çok faktörlü kimlik doğrulama sağlayıcısı hareketler şifreleme için özel anahtarı içerir.</span><span class="sxs-lookup"><span data-stu-id="d7428-108">Each SDK also includes a certificate and private key for encrypting transactions that are unique tooyour Multi-Factor Authentication Provider.</span></span> <span data-ttu-id="d7428-109">Bir sağlayıcı sahip olduğu sürece, gerektiği kadar çok dil ve biçimleri hello SDK indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7428-109">As long as you have a provider, you can download hello SDK in as many languages and formats as you need.</span></span>

<span data-ttu-id="d7428-110">Merhaba multi-Factor Authentication SDK'sı API'lerini hello Hello yapısını basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="d7428-110">hello structure of hello APIs in hello Multi-Factor Authentication SDK is simple.</span></span> <span data-ttu-id="d7428-111">Tek işlev hello çok faktörlü seçeneği parametreleri (gibi doğrulama modu) ve kullanıcı verilerini (Merhaba telefon numarası toocall veya gibi hello PIN numarası toovalidate) ile tooan API çağrısı yapın.</span><span class="sxs-lookup"><span data-stu-id="d7428-111">Make a single function call tooan API with hello multi-factor option parameters (like verification mode) and user data (like hello telephone number toocall or hello PIN number toovalidate).</span></span> <span data-ttu-id="d7428-112">Hello API'leri Çevir hello işlev çağrısı web hizmetleri istekleri toohello uygulamasına bulut tabanlı Azure çok faktörlü kimlik doğrulama hizmeti.</span><span class="sxs-lookup"><span data-stu-id="d7428-112">hello APIs translate hello function call into web services requests toohello cloud-based Azure Multi-Factor Authentication Service.</span></span> <span data-ttu-id="d7428-113">Tüm çağrılar her SDK'da bulunan başvuru toohello özel sertifika eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7428-113">All calls must include a reference toohello private certificate that is included in every SDK.</span></span>

<span data-ttu-id="d7428-114">Azure Active Directory'de kayıtlı erişim toousers Hello API'leri sahip değil çünkü bir dosya veya veritabanı kullanıcı bilgilerini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7428-114">Because hello APIs do not have access toousers registered in Azure Active Directory, you must provide user information in a file or database.</span></span> <span data-ttu-id="d7428-115">Ayrıca, hello API'leri sağlamaz kayıt ya da kullanıcı yönetimi özellikleri, yani toobuild gerekiyor uygulamanıza bu işlemler.</span><span class="sxs-lookup"><span data-stu-id="d7428-115">Also, hello APIs do not provide enrollment or user management features, so you need toobuild these processes into your application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d7428-116">toodownload SDK Merhaba, Azure MFA, AAD Premium veya EMS lisansları olsa bile toocreate Azure multi-Factor Auth sağlayıcısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7428-116">toodownload hello SDK, you need toocreate an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span> <span data-ttu-id="d7428-117">Bu amaç için Azure multi-Factor Auth sağlayıcısı oluşturmak ve lisansları zaten varsa, emin toocreate hello sağlayıcısı hello sahip olun **etkin kullanıcı başına** modeli.</span><span class="sxs-lookup"><span data-stu-id="d7428-117">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, make sure toocreate hello Provider with hello **Per Enabled User** model.</span></span> <span data-ttu-id="d7428-118">Ardından, hello Azure MFA, Azure AD Premium veya EMS lisansları içeren hello sağlayıcısı toohello dizini bağlayın.</span><span class="sxs-lookup"><span data-stu-id="d7428-118">Then, link hello Provider toohello directory that contains hello Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="d7428-119">Bu yapılandırma hello sahip olduğunuz lisans hello sayısından SDK kullanarak daha fazla benzersiz kullanıcı varsa, yalnızca faturalandırılır olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="d7428-119">This configuration ensures that you are only billed if you have more unique users using hello SDK than hello number of licenses you own.</span></span>


## <a name="download-hello-sdk"></a><span data-ttu-id="d7428-120">Merhaba SDK yükle</span><span class="sxs-lookup"><span data-stu-id="d7428-120">Download hello SDK</span></span>
<span data-ttu-id="d7428-121">Hello Azure çok faktörlü SDK'sını indirme gerektiren bir [Azure multi-Factor Auth sağlayıcısı](multi-factor-authentication-get-started-auth-provider.md).</span><span class="sxs-lookup"><span data-stu-id="d7428-121">Downloading hello Azure Multi-Factor SDK requires an [Azure Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md).</span></span>  <span data-ttu-id="d7428-122">Azure MFA, Azure AD Premium veya Enterprise Mobility Suite lisansları ait olsa bile bu tam Azure aboneliği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d7428-122">This requires a full Azure subscription, even if Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses are owned.</span></span>  <span data-ttu-id="d7428-123">toodownload hello SDK, toohello çok faktörlü yönetim portalına gidin.</span><span class="sxs-lookup"><span data-stu-id="d7428-123">toodownload hello SDK, navigate toohello Multi-Factor Management Portal.</span></span> <span data-ttu-id="d7428-124">Merhaba portal ya da hello multi-Factor Auth sağlayıcısı doğrudan yönetme veya hello tıklatarak ulaşabilirsiniz **"Git toohello portalı"** hello MFA hizmet ayarları sayfasında bağlantı.</span><span class="sxs-lookup"><span data-stu-id="d7428-124">You can reach hello portal either by managing hello Multi-Factor Auth Provider directly, or by clicking hello **"Go toohello portal"** link on hello MFA service settings page.</span></span>

### <a name="download-from-hello-azure-classic-portal"></a><span data-ttu-id="d7428-125">Hello Klasik Azure Portalı ' indirin</span><span class="sxs-lookup"><span data-stu-id="d7428-125">Download from hello Azure classic portal</span></span>
1. <span data-ttu-id="d7428-126">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com) yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="d7428-126">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="d7428-127">Merhaba solda seçin **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d7428-127">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="d7428-128">Merhaba Active Directory sayfasında hello üst seçin en **çok faktörlü kimlik doğrulama sağlayıcıları**</span><span class="sxs-lookup"><span data-stu-id="d7428-128">On hello Active Directory page, at hello top select **Multi-Factor Auth Providers**</span></span>
4. <span data-ttu-id="d7428-129">Merhaba altındaki seçin **Yönet**.</span><span class="sxs-lookup"><span data-stu-id="d7428-129">At hello bottom select **Manage**.</span></span> <span data-ttu-id="d7428-130">Yeni bir sayfa açılır.</span><span class="sxs-lookup"><span data-stu-id="d7428-130">A new page opens.</span></span>
5. <span data-ttu-id="d7428-131">Merhaba, hello altındaki sol tıklayın **SDK**.</span><span class="sxs-lookup"><span data-stu-id="d7428-131">On hello left, at hello bottom, click **SDK**.</span></span>
   <span data-ttu-id="d7428-132"><center>![İndirme](./media/multi-factor-authentication-sdk/download.png)</center></span><span class="sxs-lookup"><span data-stu-id="d7428-132"><center>![Download](./media/multi-factor-authentication-sdk/download.png)</center></span></span>
6. <span data-ttu-id="d7428-133">İstediğiniz bir hello ilişkili indirme bağlantıları tıklatın hello dili seçin.</span><span class="sxs-lookup"><span data-stu-id="d7428-133">Select hello language you want and click one hello associated download links.</span></span>
7. <span data-ttu-id="d7428-134">Merhaba indirmeyi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d7428-134">Save hello download.</span></span>

### <a name="download-from-hello-service-settings"></a><span data-ttu-id="d7428-135">Merhaba hizmet ayarlarını indirme</span><span class="sxs-lookup"><span data-stu-id="d7428-135">Download from hello service settings</span></span>
1. <span data-ttu-id="d7428-136">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com) yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="d7428-136">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="d7428-137">Merhaba solda seçin **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d7428-137">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="d7428-138">Azure AD örneğinize çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d7428-138">Double-click your instance of Azure AD.</span></span>
4. <span data-ttu-id="d7428-139">Merhaba üst tıklatın adresindeki **Yapılandır**</span><span class="sxs-lookup"><span data-stu-id="d7428-139">At hello top click **Configure**</span></span>
5. <span data-ttu-id="d7428-140">Çok faktörlü kimlik doğrulaması altında seçin **hizmet ayarlarını Yönet**
   ![indirin](./media/multi-factor-authentication-sdk/download2.png)</span><span class="sxs-lookup"><span data-stu-id="d7428-140">Under multi-factor authentication, select **Manage service settings**
![Download](./media/multi-factor-authentication-sdk/download2.png)</span></span>
6. <span data-ttu-id="d7428-141">Merhaba ekranında hello altında Hello Hizmetleri ayarları sayfasında, tıklatın **Git toohello portal**.</span><span class="sxs-lookup"><span data-stu-id="d7428-141">On hello services settings page, at hello bottom of hello screen click **Go toohello portal**.</span></span> <span data-ttu-id="d7428-142">Yeni bir sayfa açılır.</span><span class="sxs-lookup"><span data-stu-id="d7428-142">A new page opens.</span></span>
   <span data-ttu-id="d7428-143">![İndir](./media/multi-factor-authentication-sdk/download3a.png)</span><span class="sxs-lookup"><span data-stu-id="d7428-143">![Download](./media/multi-factor-authentication-sdk/download3a.png)</span></span>
7. <span data-ttu-id="d7428-144">Merhaba, hello altındaki sol tıklayın **SDK**.</span><span class="sxs-lookup"><span data-stu-id="d7428-144">On hello left, at hello bottom, click **SDK**.</span></span>
8. <span data-ttu-id="d7428-145">İstediğiniz bir hello ilişkili indirme bağlantıları tıklatın hello dili seçin.</span><span class="sxs-lookup"><span data-stu-id="d7428-145">Select hello language you want and click one hello associated download links.</span></span>
9. <span data-ttu-id="d7428-146">Merhaba indirmeyi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d7428-146">Save hello download.</span></span>

## <a name="whats-in-hello-sdk"></a><span data-ttu-id="d7428-147">Hello nedir SDK</span><span class="sxs-lookup"><span data-stu-id="d7428-147">What's in hello SDK</span></span>
<span data-ttu-id="d7428-148">Merhaba SDK hello aşağıdaki öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="d7428-148">hello SDK includes hello following items:</span></span>

* <span data-ttu-id="d7428-149">**BENİOKU**.</span><span class="sxs-lookup"><span data-stu-id="d7428-149">**README**.</span></span> <span data-ttu-id="d7428-150">Nasıl toouse Merhaba çok faktörlü kimlik doğrulaması API'leri yeni veya var olan bir uygulamada açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d7428-150">Explains how toouse hello Multi-Factor Authentication APIs in a new or existing application.</span></span>
* <span data-ttu-id="d7428-151">**Kaynak dosyaları** çok faktörlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d7428-151">**Source files** for Multi-Factor Authentication</span></span>
* <span data-ttu-id="d7428-152">**İstemci sertifikası** toocommunicate hello çok faktörlü kimlik doğrulama hizmeti ile kullanma</span><span class="sxs-lookup"><span data-stu-id="d7428-152">**Client certificate** that you use toocommunicate with hello Multi-Factor Authentication service</span></span>
* <span data-ttu-id="d7428-153">**Özel anahtarı** hello sertifika için</span><span class="sxs-lookup"><span data-stu-id="d7428-153">**Private key** for hello certificate</span></span>
* <span data-ttu-id="d7428-154">**Çağrı sonuçları.**</span><span class="sxs-lookup"><span data-stu-id="d7428-154">**Call results.**</span></span> <span data-ttu-id="d7428-155">Arama sonuç kodları listesi.</span><span class="sxs-lookup"><span data-stu-id="d7428-155">A list of call result codes.</span></span> <span data-ttu-id="d7428-156">tooopen bu dosya, bir uygulama, WordPad gibi biçimlendirme metinle kullanın.</span><span class="sxs-lookup"><span data-stu-id="d7428-156">tooopen this file, use an application with text formatting, such as WordPad.</span></span> <span data-ttu-id="d7428-157">Kullanım hello sonuç kodları tootest çağırın ve çok faktörlü kimlik doğrulaması hello uyarlamasını uygulamanızda sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="d7428-157">Use hello call result codes tootest and troubleshoot hello implementation of Multi-Factor Authentication in your application.</span></span> <span data-ttu-id="d7428-158">Kimlik doğrulama durum kodları değiller.</span><span class="sxs-lookup"><span data-stu-id="d7428-158">They are not authentication status codes.</span></span>
* <span data-ttu-id="d7428-159">**Örnekler.**</span><span class="sxs-lookup"><span data-stu-id="d7428-159">**Examples.**</span></span> <span data-ttu-id="d7428-160">Temel çalışma uygulamasını çok faktörlü kimlik doğrulaması için örnek kod.</span><span class="sxs-lookup"><span data-stu-id="d7428-160">Sample code for a basic working implementation of Multi-Factor Authentication.</span></span>

> [!WARNING]
> <span data-ttu-id="d7428-161">Merhaba istemci sertifikası, özellikle sizin için oluşturulan benzersiz bir özel sertifikasıdır.</span><span class="sxs-lookup"><span data-stu-id="d7428-161">hello client certificate is a unique private certificate that was generated especially for you.</span></span> <span data-ttu-id="d7428-162">Paylaşım değil veya bu dosyayı kaybedersiniz.</span><span class="sxs-lookup"><span data-stu-id="d7428-162">Do not share or lose this file.</span></span> <span data-ttu-id="d7428-163">Bu anahtar tooensuring hello güvenliğinizi hello multi-Factor Authentication hizmetiyle, iletişimin olur.</span><span class="sxs-lookup"><span data-stu-id="d7428-163">It’s your key tooensuring hello security of your communications with hello Multi-Factor Authentication service.</span></span>

## <a name="code-sample"></a><span data-ttu-id="d7428-164">Kod örneği</span><span class="sxs-lookup"><span data-stu-id="d7428-164">Code sample</span></span>
<span data-ttu-id="d7428-165">Bu kod örneği, nasıl hello Azure multi-Factor Authentication SDK'sı tooadd Standart mod sesli toouse hello API'leri çağırmak doğrulama tooyour uygulama gösterir.</span><span class="sxs-lookup"><span data-stu-id="d7428-165">This code sample shows you how toouse hello APIs in hello Azure Multi-Factor Authentication SDK tooadd standard mode voice call verification tooyour application.</span></span> <span data-ttu-id="d7428-166">Kullanıcı yanıt tooby hello # tuşuna basarak hello bir telefon çağrısı standart moddur.</span><span class="sxs-lookup"><span data-stu-id="d7428-166">Standard mode is a telephone call that hello user responds tooby pressing hello # key.</span></span>

<span data-ttu-id="d7428-167">Bu örnek, C# sunucu tarafı mantığı ile temel bir ASP.NET uygulaması hello C# .NET 2.0 multi-Factor Authentication SDK kullanır, ancak diğer dillerde hello işlemi benzer.</span><span class="sxs-lookup"><span data-stu-id="d7428-167">This example uses hello C# .NET 2.0 Multi-Factor Authentication SDK in a basic ASP.NET application with C# server-side logic, but hello process is similar in other languages.</span></span> <span data-ttu-id="d7428-168">Merhaba SDK kaynak dosyaları, değil yürütülebilir dosyaları, içerdiğinden hello dosyaları oluşturmak ve bunları başvuru veya doğrudan uygulamanızda içermiyor.</span><span class="sxs-lookup"><span data-stu-id="d7428-168">Because hello SDK includes source files, not executable files, you can build hello files and reference them or include them directly in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="d7428-169">Çok faktörlü kimlik doğrulamasını yaparken, hello ek yöntemleri (telefon araması veya kısa mesaj) ikincil veya üçüncül doğrulama toosupplement birincil kimlik doğrulama yöntemi (kullanıcı adı ve parola) kullanın.</span><span class="sxs-lookup"><span data-stu-id="d7428-169">When implementing Multi-Factor Authentication, use hello additional methods (phone call or text message) as secondary or tertiary verification toosupplement your primary authentication method (username and password).</span></span> <span data-ttu-id="d7428-170">Bu yöntemler, birincil kimlik doğrulama yöntemi olarak tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="d7428-170">These methods are not designed as primary authentication methods.</span></span>

### <a name="code-sample-overview"></a><span data-ttu-id="d7428-171">Kod örnek genel bakış</span><span class="sxs-lookup"><span data-stu-id="d7428-171">Code Sample Overview</span></span>
<span data-ttu-id="d7428-172">Bu örnek kod basit bir web demo uygulaması için bir telefon çağrısı # anahtarı yanıtı tooverify hello kullanıcı kimlik doğrulaması ile kullanır.</span><span class="sxs-lookup"><span data-stu-id="d7428-172">This sample code for a simple web demo application uses a telephone call with a # key response tooverify hello user's authentication.</span></span> <span data-ttu-id="d7428-173">Bu telefon görüşmesi faktörü çok faktörlü kimlik doğrulaması Standart modu olarak bilinir.</span><span class="sxs-lookup"><span data-stu-id="d7428-173">This telephone call factor is known in Multi-Factor Authentication as standard mode.</span></span>

<span data-ttu-id="d7428-174">Merhaba istemci-tarafı kodu tüm çok faktörlü kimlik doğrulaması özgü öğeleri içermez.</span><span class="sxs-lookup"><span data-stu-id="d7428-174">hello client-side code does not include any Multi-Factor Authentication-specific elements.</span></span> <span data-ttu-id="d7428-175">Merhaba ek kimlik doğrulama faktörleri hello birincil kimlik doğrulaması bağımsız olduğundan, oturum açma hello varolan arabirimi değiştirmeden ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7428-175">Because hello additional authentication factors are independent of hello primary authentication, you can add them without changing hello existing sign-on interface.</span></span> <span data-ttu-id="d7428-176">hello multi-Factor SDK API'leri Hello hello kullanıcı deneyimini özelleştirmesini sağlar, ancak, toochange herhangi bir şey hiç gerekmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="d7428-176">hello APIs in hello Multi-Factor SDK let you customize hello user experience, but you might not need toochange anything at all.</span></span>

<span data-ttu-id="d7428-177">Merhaba sunucu tarafı kodu, adım 2'de Standart mod kimlik doğrulaması ekler.</span><span class="sxs-lookup"><span data-stu-id="d7428-177">hello server-side code adds standard-mode authentication in Step 2.</span></span> <span data-ttu-id="d7428-178">Standart mod doğrulama için gerekli olan hello parametrelere sahip bir PfAuthParams nesnesi oluşturur: kullanıcı adı, telefon numarası ve modu ve hello her çağrıda gereken yolu toohello istemci sertifikası (CertFilePath).</span><span class="sxs-lookup"><span data-stu-id="d7428-178">It creates a PfAuthParams object with hello parameters that are required for standard-mode verification: username, telephone number, and mode, and hello path toohello client certificate (CertFilePath), which is required in each call.</span></span> <span data-ttu-id="d7428-179">PfAuthParams tüm parametreleri tanıtımı için bkz: hello örnek hello SDK dosyasında.</span><span class="sxs-lookup"><span data-stu-id="d7428-179">For a demonstration of all parameters in PfAuthParams, see hello Example file in hello SDK.</span></span>

<span data-ttu-id="d7428-180">Ardından, hello kod hello PfAuthParams nesnesi toohello pf_authenticate() işlevi iletir.</span><span class="sxs-lookup"><span data-stu-id="d7428-180">Next, hello code passes hello PfAuthParams object toohello pf_authenticate() function.</span></span> <span data-ttu-id="d7428-181">Merhaba dönüş değeri hello başarı veya başarısızlık hello kimlik doğrulamasının gösterir.</span><span class="sxs-lookup"><span data-stu-id="d7428-181">hello return value indicates hello success or failure of hello authentication.</span></span> <span data-ttu-id="d7428-182">parametreleri, callStatus ve errorID Merhaba, ek arama sonuç bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="d7428-182">hello out parameters, callStatus, and errorID, contain additional call result information.</span></span> <span data-ttu-id="d7428-183">Merhaba arama sonuç kodları hello arama sonuçları hello SDK dosyasında belgelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="d7428-183">hello call result codes are documented in hello call results file in hello SDK.</span></span>

<span data-ttu-id="d7428-184">Bu en az uygulama birkaç satırda yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="d7428-184">This minimal implementation can be written in a few lines.</span></span> <span data-ttu-id="d7428-185">Ancak, üretim kodunda, daha gelişmiş hata işleme, ek veritabanı kodu ve geliştirilmiş bir kullanıcı deneyimi içerir.</span><span class="sxs-lookup"><span data-stu-id="d7428-185">However, in production code, you would include more sophisticated error handling, additional database code, and an enhanced user experience.</span></span>

### <a name="web-client-code"></a><span data-ttu-id="d7428-186">Web istemci kodu</span><span class="sxs-lookup"><span data-stu-id="d7428-186">Web Client Code</span></span>
<span data-ttu-id="d7428-187">Merhaba, web gösteri sayfası için istemci kodu aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="d7428-187">hello following is web client code for a demo page.</span></span>

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


### <a name="server-side-code"></a><span data-ttu-id="d7428-188">Sunucu Tarafında Çalışan Kod</span><span class="sxs-lookup"><span data-stu-id="d7428-188">Server-Side Code</span></span>
<span data-ttu-id="d7428-189">Sunucu tarafı kodu aşağıdaki hello, çok faktörlü kimlik doğrulaması yapılandırılan ve 2. adımda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d7428-189">In hello following server-side code, Multi-Factor Authentication is configured and run in Step 2.</span></span> <span data-ttu-id="d7428-190">Standart mod (MODE_STANDARD) hello # tuşuna basarak bir telefon araması toowhich hello kullanıcı yanıt içindir.</span><span class="sxs-lookup"><span data-stu-id="d7428-190">Standard mode (MODE_STANDARD) is a telephone call toowhich hello user responds by pressing hello # key.</span></span>

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
            // Step 1: Validate hello username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from hello user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains hello private key for hello client
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
