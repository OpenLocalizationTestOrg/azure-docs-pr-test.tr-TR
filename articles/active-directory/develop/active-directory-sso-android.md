---
title: "aaaHow tooenable uygulamalar arası SSO'nun ADAL kullanarak Android üzerinde | Microsoft Docs"
description: "Nasıl toouse hello özelliklerini uygulamalarınızı boyunca çoklu oturum açma ADAL SDK tooenable hello. "
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 40710225-05ab-40a3-9aec-8b4e96b6b5e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 04/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 3867e15030e5516464e4dbd92ba35894430daf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-android-using-adal"></a><span data-ttu-id="c89e1-103">Nasıl tooenable uygulamalar arası SSO'nun ADAL kullanarak Android üzerinde</span><span class="sxs-lookup"><span data-stu-id="c89e1-103">How tooenable cross-app SSO on Android using ADAL</span></span>
<span data-ttu-id="c89e1-104">Böylece kullanıcılar yalnızca tooenter kimlik bilgilerini bir kez gerekir ve bu kimlik bilgilerini otomatik olarak iş uygulamalarda çoklu oturum açma (SSO) sağlayarak müşteriler tarafından şimdi beklenir.</span><span class="sxs-lookup"><span data-stu-id="c89e1-104">Providing Single Sign-On (SSO) so that users only need tooenter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="c89e1-105">ekranda bir telefon araması veya ilerideki kodu gibi ek bir etmen (2FA) kez birlikte küçük, genellikle kullanıcı adı ve parola girme hello zorluk hızlı memnuniyetsizliği kullanıcı sonuçlarında var. toodo bu ürün için birden fazla kez</span><span class="sxs-lookup"><span data-stu-id="c89e1-105">hello difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has toodo this more than one time for your product.</span></span>

<span data-ttu-id="c89e1-106">Ayrıca, Microsoft Accounts veya Office365 iş hesabından gibi diğer uygulamaları kullanabilir bir kimlik platformu uygularsanız, müşterilerin kimlik bilgileri bu toobe kullanılabilir toouse tüm uygulamalar arasında Hayır, hello satıcı önemli bekler.</span><span class="sxs-lookup"><span data-stu-id="c89e1-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials toobe available toouse across all their applications no matter hello vendor.</span></span>

<span data-ttu-id="c89e1-107">Merhaba, Microsoft Identity SDK ile birlikte Microsoft Identity platform tüm bu sabit sizin ve SSO ya da kendi paketi uygulamaların veya olarak içinde müşterilerinizle özelliği toodelight hello verir çalışır bizim Aracısı yetenek ve Doğrulayıcı Merhaba tüm aygıt üzerinden uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="c89e1-107">hello Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you hello ability toodelight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across hello entire device.</span></span>

<span data-ttu-id="c89e1-108">Bu kılavuz size nasıl söyleyecektir tooconfigure bizim SDK, uygulama tooprovide içinde bu avantajı tooyour müşteriler.</span><span class="sxs-lookup"><span data-stu-id="c89e1-108">This walkthrough will tell you how tooconfigure our SDK within your application tooprovide this benefit tooyour customers.</span></span>

<span data-ttu-id="c89e1-109">Bu kılavuz için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="c89e1-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="c89e1-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c89e1-110">Azure Active Directory</span></span>
* <span data-ttu-id="c89e1-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="c89e1-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="c89e1-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="c89e1-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="c89e1-113">Azure Active Directory Koşullu Erişim</span><span class="sxs-lookup"><span data-stu-id="c89e1-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="c89e1-114">Merhaba belge önceki varsayar nasıl çok bildiğiniz[sağlamak hello eski portalı uygulamalarında Azure Active Directory için](active-directory-how-to-integrate.md) ve uygulamanızı hello ile tümleşik [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android) .</span><span class="sxs-lookup"><span data-stu-id="c89e1-114">hello document preceding assumes you know how too[provision applications in hello legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with hello [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span></span>

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a><span data-ttu-id="c89e1-115">Microsoft kimlik platformu hello SSO kavramlar</span><span class="sxs-lookup"><span data-stu-id="c89e1-115">SSO Concepts in hello Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="c89e1-116">Microsoft Identity aracıları</span><span class="sxs-lookup"><span data-stu-id="c89e1-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="c89e1-117">Microsoft hello kimlik bilgilerini farklı satıcılardan uygulamalar arasında köprü oluşturma için izin uygulamaları mobil her platform için sağlar ve nerede tek güvenli bir yerde gerektiren özel Gelişmiş özellikleri sağlar toovalidate kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="c89e1-117">Microsoft provides applications for every mobile platform that allow for hello bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where toovalidate credentials.</span></span> <span data-ttu-id="c89e1-118">Bunlar diyoruz **aracıların**.</span><span class="sxs-lookup"><span data-stu-id="c89e1-118">We call these **brokers**.</span></span> <span data-ttu-id="c89e1-119">İOS ve Android bunlar müşteriler bağımsız olarak yüklemek veya toohello aygıt bazılarını veya tümünü hello cihaz için kendi çalışan yöneten bir şirket tarafından gönderilen indirilebilir uygulamaları aracılığıyla sağlanır.</span><span class="sxs-lookup"><span data-stu-id="c89e1-119">On iOS and Android these are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages some or all of hello device for their employee.</span></span> <span data-ttu-id="c89e1-120">Bu aracıları yönetme güvenlik yalnızca bazı uygulamalar veya ne BT yöneticileri işlemleriniz dayalı hello tüm cihaz desteği.</span><span class="sxs-lookup"><span data-stu-id="c89e1-120">These brokers support managing security just for some applications or hello entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="c89e1-121">Windows, bu işlev toohello işletim sistemi, teknik olarak Web kimlik doğrulama Aracısı hello bilinen yerleşik bir hesabı seçicide tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="c89e1-121">In Windows, this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>

<span data-ttu-id="c89e1-122">Hakkında daha fazla bilgi için bu aracıların ve nasıl müşterilerinizin bunları okuyun hello Microsoft Identity platform için kullanıcıların oturum açma akışını görebileceğiniz kullanırız.</span><span class="sxs-lookup"><span data-stu-id="c89e1-122">For more information on how we use these brokers and how your customers might see them in their login flow for hello Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="c89e1-123">Mobil cihazlarda günlüğe kaydetme için desenleri</span><span class="sxs-lookup"><span data-stu-id="c89e1-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="c89e1-124">Erişim toocredentials cihazlarda hello Microsoft Identity platformuna yönelik iki temel düzenlerden izleyin:</span><span class="sxs-lookup"><span data-stu-id="c89e1-124">Access toocredentials on devices follow two basic patterns for hello Microsoft Identity platform:</span></span>

* <span data-ttu-id="c89e1-125">Olmayan Aracısı Yardımlı oturum açmalar</span><span class="sxs-lookup"><span data-stu-id="c89e1-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="c89e1-126">Yardımlı Oturum Aracısı</span><span class="sxs-lookup"><span data-stu-id="c89e1-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="c89e1-127">Olmayan Aracısı Yardımlı oturum açmalar</span><span class="sxs-lookup"><span data-stu-id="c89e1-127">Non-broker assisted logins</span></span>
<span data-ttu-id="c89e1-128">Olmayan Aracısı Yardımlı satır içi hello uygulamayla gerçekleşir ve hello cihazda bu uygulama için hello yerel depolama kullanan oturum açma deneyimlerini oturumlardır.</span><span class="sxs-lookup"><span data-stu-id="c89e1-128">Non-broker assisted logins are login experiences that happen inline with hello application and use hello local storage on hello device for that application.</span></span> <span data-ttu-id="c89e1-129">Bu depolama uygulamalar arasında paylaşılıyor olabilir ancak sıkı şekilde bağlı toohello uygulama ya da bu kimlik bilgilerini kullanarak uygulama paketi hello kimlik bilgileridir.</span><span class="sxs-lookup"><span data-stu-id="c89e1-129">This storage may be shared across applications but hello credentials are tightly bound toohello app or suite of apps using that credential.</span></span> <span data-ttu-id="c89e1-130">Bir kullanıcı adı ve parola hello uygulamanın kendi içinde girdiğinizde, bu büyük olasılıkla birçok mobil uygulamalarda tecrübe ettiklerinize.</span><span class="sxs-lookup"><span data-stu-id="c89e1-130">You've most likely experienced this in many mobile applications when you enter a username and password within hello application itself.</span></span>

<span data-ttu-id="c89e1-131">Bu oturumlar hello aşağıdaki faydaları vardır:</span><span class="sxs-lookup"><span data-stu-id="c89e1-131">These logins have hello following benefits:</span></span>

* <span data-ttu-id="c89e1-132">Kullanıcı deneyimi tamamen hello uygulaması içinde zaten var.</span><span class="sxs-lookup"><span data-stu-id="c89e1-132">User experience exists entirely within hello application.</span></span>
* <span data-ttu-id="c89e1-133">Kimlik bilgileri, hello tarafından imzalanmış uygulamalar arasında paylaşılabilir aynı sertifika, çoklu oturum açma deneyimini tooyour suite uygulamaların sağlama.</span><span class="sxs-lookup"><span data-stu-id="c89e1-133">Credentials can be shared across applications that are signed by hello same certificate, providing a single sign-on experience tooyour suite of applications.</span></span>
* <span data-ttu-id="c89e1-134">Denetim Günlüğü'nde hello deneyimi geçici toohello uygulama önce ve sonra oturum açma sağlanır.</span><span class="sxs-lookup"><span data-stu-id="c89e1-134">Control around hello experience of logging in is provided toohello application before and after sign-in.</span></span>

<span data-ttu-id="c89e1-135">Bu oturumlar dezavantajları aşağıdaki hello vardır:</span><span class="sxs-lookup"><span data-stu-id="c89e1-135">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="c89e1-136">Kullanıcı yalnızca bu Microsoft uygulamanızı yapılandırılmış Identities arasında Microsoft Identity kullanan tüm uygulamalar boyunca çoklu oturum açma deneyimi olamaz.</span><span class="sxs-lookup"><span data-stu-id="c89e1-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="c89e1-137">Uygulamanız, koşullu erişim veya kullanımı hello Intune ürün paketi gibi daha gelişmiş iş özellikleriyle kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="c89e1-137">Your application cannot be used with more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="c89e1-138">Uygulamanızı iş kullanıcıları için sertifika tabanlı kimlik doğrulamasını destekleyemez.</span><span class="sxs-lookup"><span data-stu-id="c89e1-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="c89e1-139">Merhaba Microsoft Identity SDK'ları, uygulamaları tooenable SSO hello paylaşılan depolama ile nasıl bir temsilini şöyledir:</span><span class="sxs-lookup"><span data-stu-id="c89e1-139">Here is a representation of how hello Microsoft Identity SDKs work with hello shared storage of your applications tooenable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| Azure SDK  | | Azure SDK  |  | Azure SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="c89e1-140">Yardımlı Oturum Aracısı</span><span class="sxs-lookup"><span data-stu-id="c89e1-140">Broker assisted logins</span></span>
<span data-ttu-id="c89e1-141">Aracısı destekli hello Aracısı uygulama içinde oluşur ve hello depolama ve güvenlik hello Aracısı tooshare kimlik bilgilerinin hello Microsoft Identity platform uygulanan tüm uygulamalar için hello aygıtta kullanan oturum açma deneyimlerini oturumlardır.</span><span class="sxs-lookup"><span data-stu-id="c89e1-141">Broker-assisted logins are login experiences that occur within hello broker application and use hello storage and security of hello broker tooshare credentials across all applications on hello device that apply hello Microsoft Identity platform.</span></span> <span data-ttu-id="c89e1-142">Bu, uygulamalarınız hello Aracısı toosign kullanıcılar kullandığını anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c89e1-142">This means that your applications rely on hello broker toosign users in.</span></span> <span data-ttu-id="c89e1-143">İOS ve Android cihazlarda bu aracıların müşteriler bağımsız olarak yüklemek veya toohello aygıt hello cihaz kendi kullanıcı yöneten bir şirket tarafından gönderilen indirilebilir uygulamaları aracılığıyla sağlanır.</span><span class="sxs-lookup"><span data-stu-id="c89e1-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages hello device for their user.</span></span> <span data-ttu-id="c89e1-144">Merhaba Microsoft Authenticator uygulaması iOS bu tür bir uygulama örneğidir.</span><span class="sxs-lookup"><span data-stu-id="c89e1-144">An example of this type of application is hello Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="c89e1-145">Windows bu işlevselliği toohello işletim sistemi, teknik olarak Web kimlik doğrulama Aracısı hello bilinen yerleşik bir hesabı seçicide tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="c89e1-145">In Windows this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>
<span data-ttu-id="c89e1-146">Merhaba deneyimi platforma göre değişir ve kesintiye uğratan toousers bazen olabilir değilse doğru şekilde yönetilir.</span><span class="sxs-lookup"><span data-stu-id="c89e1-146">hello experience varies by platform and can sometimes be disruptive toousers if not managed correctly.</span></span> <span data-ttu-id="c89e1-147">Merhaba Facebook uygulamanın yüklü olması ve başka bir uygulamadan Facebook bağlanmak kullanırsanız bu deseni ile en biliyor.</span><span class="sxs-lookup"><span data-stu-id="c89e1-147">You're probably most familiar with this pattern if you have hello Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="c89e1-148">Merhaba Microsoft kimlik platformu kullandığı aynı düzeni hello.</span><span class="sxs-lookup"><span data-stu-id="c89e1-148">hello Microsoft Identity platform uses hello same pattern.</span></span>

<span data-ttu-id="c89e1-149">İOS için bu tooa "geçiş" animasyon Burada, uygulamanızın hello Microsoft Authenticator uygulamaları toohello arka toohello ön hello kullanıcı tooselect için gelen gönderilen toosign ile istediğiniz hangi hesabı doğurur.</span><span class="sxs-lookup"><span data-stu-id="c89e1-149">For iOS this leads tooa "transition" animation where your application is sent toohello background while hello Microsoft Authenticator applications comes toohello foreground for hello user tooselect which account they would like toosign in with.</span></span>  

<span data-ttu-id="c89e1-150">Android ve Windows hello hesabı seçicide daha az kesintiye uğratan toohello kullanıcı olan, uygulamanızın üzerinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c89e1-150">For Android and Windows hello account chooser is displayed on top of your application which is less disruptive toohello user.</span></span>

#### <a name="how-hello-broker-gets-invoked"></a><span data-ttu-id="c89e1-151">Merhaba Aracısı nasıl çağrılır</span><span class="sxs-lookup"><span data-stu-id="c89e1-151">How hello broker gets invoked</span></span>
<span data-ttu-id="c89e1-152">Uyumlu bir aracı hello Microsoft Authenticator uygulaması, hello Microsoft Identity SDK'ları otomatik olarak ayarlanır gibi hello aygıtta yüklüyse, bir kullanıcı herhangi bir hesabı kullanarak toolog istedikleri belirttiğinde hello broker çağırma iş hello Merhaba Microsoft Identity platform.</span><span class="sxs-lookup"><span data-stu-id="c89e1-152">If a compatible broker is installed on hello device, like hello Microsoft Authenticator application, hello Microsoft Identity SDKs will automatically do hello work of invoking hello broker for you when a user indicates they wish toolog in using any account from hello Microsoft Identity platform.</span></span> <span data-ttu-id="c89e1-153">Bu hesap, kişisel Microsoft Account, bir iş veya Okul hesabı veya bir sağladığınız hesap ve konak B2C ve B2B Ürünlerimiz kullanarak azure'da olabilir.</span><span class="sxs-lookup"><span data-stu-id="c89e1-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 
 
 #### <a name="how-we-ensure-hello-application-is-valid"></a><span data-ttu-id="c89e1-154">Biz Merhaba uygulaması nasıl emin geçerlidir</span><span class="sxs-lookup"><span data-stu-id="c89e1-154">How we ensure hello application is valid</span></span>
 
 <span data-ttu-id="c89e1-155">Merhaba gerek tooensure hello bir uygulama çağrısı hello Aracısı destekli Aracısı oturum açma bilgilerini sağladığımız önemli toohello güvenlik kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="c89e1-155">hello need tooensure hello identity of an application call hello broker is crucial toohello security we provide in broker assisted logins.</span></span> <span data-ttu-id="c89e1-156">İOS ne Android kötü amaçlı uygulamalar ve "yasal uygulamanın tanımlayıcı aldatıcı" Merhaba yasal uygulaması için amacı hello belirteçleri almak için yalnızca belirli bir uygulama için geçerli olan benzersiz tanımlayıcıları zorlar.</span><span class="sxs-lookup"><span data-stu-id="c89e1-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive hello tokens meant for hello legitimate application.</span></span> <span data-ttu-id="c89e1-157">Biz her zaman zamanında hello doğru uygulama ile iletişim kuran tooensure, biz hello Geliştirici tooprovide özel redirectURI kendi uygulama Microsoft ile kaydedilirken isteyin.</span><span class="sxs-lookup"><span data-stu-id="c89e1-157">tooensure we are always communicating with hello right application at runtime, we ask hello developer tooprovide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="c89e1-158">**Geliştiricilerin bu yeniden yönlendirme URI'si nasıl oluşturabilir aşağıda ayrıntılı olarak ele alınmıştır.**</span><span class="sxs-lookup"><span data-stu-id="c89e1-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="c89e1-159">Bu özel redirectURI ve toobe benzersiz toohello uygulama Google Play mağazası hello tarafından güvence altına hello sertifika parmak izi hello uygulamasının içerir.</span><span class="sxs-lookup"><span data-stu-id="c89e1-159">This custom redirectURI contains hello certificate thumbprint of hello application and is ensured toobe unique toohello application by hello Google Play Store.</span></span> <span data-ttu-id="c89e1-160">Bir uygulama hello Aracısı hello Android işletim sistemi tooprovide ister hello Aracısı çağırdığında hello ile sertifika parmak izi, çağrılan hello Aracısı.</span><span class="sxs-lookup"><span data-stu-id="c89e1-160">When an application calls hello broker, hello broker asks hello Android operating system tooprovide it with hello certificate thumbprint that called hello broker.</span></span> <span data-ttu-id="c89e1-161">Merhaba Aracısı bu sertifika parmak izi tooMicrosoft hello çağrısı tooour kimlik sistemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="c89e1-161">hello broker provides this certificate thumbprint tooMicrosoft in hello call tooour identity system.</span></span> <span data-ttu-id="c89e1-162">Hello sertifika parmak izi Merhaba uygulaması hello sertifika parmak iziyle eşleşmiyor kayıt sırasında toous hello geliştirici tarafından sağlanan, hello kaynak hello uygulama istenirken için size erişim toohello belirteçleri reddeder.</span><span class="sxs-lookup"><span data-stu-id="c89e1-162">If hello certificate thumbprint of hello application does not match hello certificate thumbprint provided toous by hello developer during registration, we will deny access toohello tokens for hello resource hello application is requesting.</span></span> <span data-ttu-id="c89e1-163">Bu denetim yalnızca hello geliştirici tarafından kayıtlı hello uygulama belirteçlerini almasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="c89e1-163">This check ensures that only hello application registered by hello developer receives tokens.</span></span>

<span data-ttu-id="c89e1-164">**Microsoft Identity SDK Hello hello Aracısı çağıran veya hello aracı olmayan Yardımlı akış kullanıyorsa, hello Geliştirici hello seçimine sahiptir.**</span><span class="sxs-lookup"><span data-stu-id="c89e1-164">**hello developer has hello choice of if hello Microsoft Identity SDK calls hello broker or uses hello non-broker assisted flow.**</span></span> <span data-ttu-id="c89e1-165">Hello geliştirici değil toouse hello Aracısı destekli akış seçerse, ancak bunlar hello yararı SSO kimlik bilgilerini kullanarak bu hello kullanıcı kaybedersiniz hello aygıtta eklemiş olabilir ve kendi uygulama Microsoft iş özelliklerle kullanılmasını engeller Koşullu erişim, Intune yönetim özellikleri ve sertifika tabanlı kimlik doğrulaması gibi müşterilerinin sağlar.</span><span class="sxs-lookup"><span data-stu-id="c89e1-165">However if hello developer chooses not toouse hello broker-assisted flow they lose hello benefit of using SSO credentials that hello user may have already added on hello device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="c89e1-166">Bu oturumlar hello aşağıdaki faydaları vardır:</span><span class="sxs-lookup"><span data-stu-id="c89e1-166">These logins have hello following benefits:</span></span>

* <span data-ttu-id="c89e1-167">Kullanıcı, kendi hello satıcı olursa olsun tüm uygulamalar arasında SSO karşılaşır.</span><span class="sxs-lookup"><span data-stu-id="c89e1-167">User experiences SSO across all their applications no matter hello vendor.</span></span>
* <span data-ttu-id="c89e1-168">Uygulamanız, koşullu erişim gibi daha gelişmiş iş özellikleri kullanın veya ürün hello Intune paketi kullanın.</span><span class="sxs-lookup"><span data-stu-id="c89e1-168">Your application can use more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="c89e1-169">Uygulamanızı iş kullanıcıları için sertifika tabanlı kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="c89e1-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="c89e1-170">Çok daha güvenli oturum açma hello uygulama ve hello kullanıcı hello kimliği doğrulandı gibi ek güvenlik algoritmalarını ve şifreleme ile Merhaba Aracısı uygulaması tarafından karşılaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="c89e1-170">Much more secure sign-in experience as hello identity of hello application and hello user are verified by hello broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="c89e1-171">Bu oturumlar dezavantajları aşağıdaki hello vardır:</span><span class="sxs-lookup"><span data-stu-id="c89e1-171">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="c89e1-172">Kimlik bilgileri seçilen sırada hello kullanıcı iOS uygulamanızın deneyimi dışında geçti.</span><span class="sxs-lookup"><span data-stu-id="c89e1-172">In iOS hello user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="c89e1-173">Kayıp hello özelliği toomanage hello oturum açma deneyimi müşterilerinize uygulamanızın içinde.</span><span class="sxs-lookup"><span data-stu-id="c89e1-173">Loss of hello ability toomanage hello login experience for your customers within your application.</span></span>

<span data-ttu-id="c89e1-174">Nasıl hello Microsoft Identity SDK'ları hello çalışmak Aracısı uygulamaları tooenable SSO bir temsilini şöyledir:</span><span class="sxs-lookup"><span data-stu-id="c89e1-174">Here is a representation of how hello Microsoft Identity SDKs work with hello broker applications tooenable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
|  ADAL SDK  | |  ADAL SDK  |   |  ADAL SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+

```

<span data-ttu-id="c89e1-175">Bu bilgiler ile çağrılmak mümkün toobetter olmalıdır anlamanıza ve SSO hello Microsoft Identity platform ve SDK'ları kullanarak uygulamanızdaki uygulamanıza.</span><span class="sxs-lookup"><span data-stu-id="c89e1-175">Armed with this background information you should be able toobetter understand and implement SSO within your application using hello Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="c89e1-176">ADAL kullanarak uygulamalar arası SSO'nun etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c89e1-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="c89e1-177">Merhaba ADAL Android SDK burada kullandığımız için:</span><span class="sxs-lookup"><span data-stu-id="c89e1-177">Here we use hello ADAL Android SDK to:</span></span>

* <span data-ttu-id="c89e1-178">Aracı olmayan Yardımlı SSO Uygulama paketiniz için Aç</span><span class="sxs-lookup"><span data-stu-id="c89e1-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="c89e1-179">Aracısı destekli SSO desteği Aç</span><span class="sxs-lookup"><span data-stu-id="c89e1-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="c89e1-180">Aracı olmayan için SSO üzerinde kapatma SSO Destekli</span><span class="sxs-lookup"><span data-stu-id="c89e1-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="c89e1-181">Uygulamalar arasında aracı olmayan Yardımlı SSO için hello Microsoft Identity SDK'ları yönetmek SSO hello karmaşıklığını çoğunu sizin için.</span><span class="sxs-lookup"><span data-stu-id="c89e1-181">For non-broker assisted SSO across applications hello Microsoft Identity SDKs manage much of hello complexity of SSO for you.</span></span> <span data-ttu-id="c89e1-182">Bu, hello Önbelleği'nde hello doğru kullanıcı bulma ve bakımını yapma, tooquery için oturum açan kullanıcıların listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="c89e1-182">This includes finding hello right user in hello cache and maintaining a list of logged in users for you tooquery.</span></span>

<span data-ttu-id="c89e1-183">Aşağıdaki toodo hello ihtiyacınız sahip uygulamalar arasında SSO tooenable:</span><span class="sxs-lookup"><span data-stu-id="c89e1-183">tooenable SSO across applications you own you need toodo hello following:</span></span>

1. <span data-ttu-id="c89e1-184">Tüm, uygulamaların kullanıcı hello aynı istemci Kimliğini veya uygulama kimliği emin olun</span><span class="sxs-lookup"><span data-stu-id="c89e1-184">Ensure all your applications user hello same Client ID or Application ID.</span></span>
2. <span data-ttu-id="c89e1-185">Tüm uygulamalarınızın aynı SharedUserID ayarlamak hello emin olun.</span><span class="sxs-lookup"><span data-stu-id="c89e1-185">Ensure all your applications have hello same SharedUserID set.</span></span>
3. <span data-ttu-id="c89e1-186">Tüm depolama paylaştırabilirsiniz deposundan hello Google Play aynı imzalama sertifika, uygulama paylaşımı hello olun.</span><span class="sxs-lookup"><span data-stu-id="c89e1-186">Ensure that all of your applications share hello same signing certificate from hello Google Play store so that you can share storage.</span></span>

#### <a name="step-1-using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a><span data-ttu-id="c89e1-187">1. adım: Aynı istemci kimliği hello kullanarak / tüm uygulamaların paketiniz uygulamalarda hello için uygulama kimliği</span><span class="sxs-lookup"><span data-stu-id="c89e1-187">Step 1: Using hello same Client ID / Application ID for all hello applications in your suite of apps</span></span>
<span data-ttu-id="c89e1-188">Bu tooshare belirteçleri, uygulamalar arasında izin verildiğini sırayla hello Microsoft Identity platform tooknow için uygulamalarınızın her birinde aynı istemci Kimliğini veya uygulama kimliği tooshare hello gerekir</span><span class="sxs-lookup"><span data-stu-id="c89e1-188">In order for hello Microsoft Identity platform tooknow that it's allowed tooshare tokens across your applications, each of your applications will need tooshare hello same Client ID or Application ID.</span></span> <span data-ttu-id="c89e1-189">Bu ilk uygulamanızı hello Portalı'nda kayıtlı yükleyen tooyou sağlanan hello benzersiz tanımlayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="c89e1-189">This is hello unique identifier that was provided tooyou when you registered your first application in hello portal.</span></span>

<span data-ttu-id="c89e1-190">Farklı uygulamaları nasıl kullanacağını merak ediyor toohello onu kullanıyorsa, Microsoft Identity hizmet hello aynı uygulama kimliği</span><span class="sxs-lookup"><span data-stu-id="c89e1-190">You may be wondering how you will identify different apps toohello Microsoft Identity service if it uses hello same Application ID.</span></span> <span data-ttu-id="c89e1-191">Merhaba cevaptır ile Merhaba **yeniden yönlendirme URI'ler**.</span><span class="sxs-lookup"><span data-stu-id="c89e1-191">hello answer is with hello **Redirect URIs**.</span></span> <span data-ttu-id="c89e1-192">Her uygulamanın birden çok yeniden yönlendirme hello hazırlama Portalı'nda kayıtlı URI'ler olabilir.</span><span class="sxs-lookup"><span data-stu-id="c89e1-192">Each application can have multiple Redirect URIs registered in hello onboarding portal.</span></span> <span data-ttu-id="c89e1-193">Her uygulama paketiniz içinde farklı bir yeniden yönlendirme URI'sine sahip olur.</span><span class="sxs-lookup"><span data-stu-id="c89e1-193">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="c89e1-194">Bu sistem, bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="c89e1-194">An example of how this looks is below:</span></span>

<span data-ttu-id="c89e1-195">App1 yeniden yönlendirme URİ'si:`msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span><span class="sxs-lookup"><span data-stu-id="c89e1-195">App1 Redirect URI: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span></span>

<span data-ttu-id="c89e1-196">App2 yeniden yönlendirme URİ'si:`msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span><span class="sxs-lookup"><span data-stu-id="c89e1-196">App2 Redirect URI: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span></span>

<span data-ttu-id="c89e1-197">App3 yeniden yönlendirme URİ'si:`msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span><span class="sxs-lookup"><span data-stu-id="c89e1-197">App3 Redirect URI: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span></span>

<span data-ttu-id="c89e1-198">....</span><span class="sxs-lookup"><span data-stu-id="c89e1-198">....</span></span>

<span data-ttu-id="c89e1-199">Bunlar altında yuvalanmış aynı istemci kimliği hello / uygulama kimliği ve Aranan göre hello redirect URI SDK yapılandırmanızda toous döndürür.</span><span class="sxs-lookup"><span data-stu-id="c89e1-199">These are nested under hello same client ID / application ID and looked up based on hello redirect URI you return toous in your SDK configuration.</span></span>

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


<span data-ttu-id="c89e1-200">*Bu yeniden yönlendirme URI biçimi hello Not aşağıda açıklanmıştır. Toosupport hello Aracısı istediğiniz sürece herhangi bir yeniden yönlendirme URI'si kullanabilir, bu durumda bunlar şunun gibi hello yukarıdaki görünmesi gerekir*</span><span class="sxs-lookup"><span data-stu-id="c89e1-200">*Note that hello format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish toosupport hello broker, in which case they must look something like hello above*</span></span>

#### <a name="step-2-configuring-shared-storage-in-android"></a><span data-ttu-id="c89e1-201">2. adım: Android paylaşılan depolama ortamı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c89e1-201">Step 2: Configuring shared storage in Android</span></span>
<span data-ttu-id="c89e1-202">Ayar hello `SharedUserID` hello bu belgenin kapsamında değildir ancak hello hello Google Android belgeleri okuyarak öğrenilebilecek [bildirim](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span><span class="sxs-lookup"><span data-stu-id="c89e1-202">Setting hello `SharedUserID` is beyond hello scope of this document but can be learned by reading hello Google Android documentation on hello [Manifest](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span></span> <span data-ttu-id="c89e1-203">Önemli olan, sharedUserID çağrılacağı ve tüm uygulamalar için kullanmak istediğinize karar ' dir.</span><span class="sxs-lookup"><span data-stu-id="c89e1-203">What is important is that you decide what you want your sharedUserID will be called and use that across all your applications.</span></span>

<span data-ttu-id="c89e1-204">Merhaba olduktan sonra `SharedUserID` hazır toouse SSO olduğunuz tüm uygulamalarınızda.</span><span class="sxs-lookup"><span data-stu-id="c89e1-204">Once you have hello `SharedUserID` in all your applications you are ready toouse SSO.</span></span>

> [!WARNING]
> <span data-ttu-id="c89e1-205">Uygulamalar arasında depolama paylaştığınızda herhangi bir uygulama bu bölge kullanıcılar silin veya tüm hello belirteçleri, uygulamanızda da kötüsü silin.</span><span class="sxs-lookup"><span data-stu-id="c89e1-205">When you share storage across your applications any application can delete users, or worse delete all hello tokens across your application.</span></span> <span data-ttu-id="c89e1-206">Merhaba belirteçleri toodo arka plan çalışması üzerinde kullanan uygulamalar varsa, özellikle felaket niteliğinde budur.</span><span class="sxs-lookup"><span data-stu-id="c89e1-206">This is particularly disastrous if you have applications that rely on hello tokens toodo background work.</span></span> <span data-ttu-id="c89e1-207">Depolama paylaşımı hello Microsoft Identity SDK'ları aracılığıyla tüm kaldırma işlemleri çok dikkatli olmalıdır anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c89e1-207">Sharing storage means that you must be very careful in any and all remove operations through hello Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="c89e1-208">İşte bu kadar!</span><span class="sxs-lookup"><span data-stu-id="c89e1-208">That's it!</span></span> <span data-ttu-id="c89e1-209">Microsoft Identity SDK Hello şimdi tüm uygulamalar için kimlik bilgileri paylaşacaktır.</span><span class="sxs-lookup"><span data-stu-id="c89e1-209">hello Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="c89e1-210">Merhaba kullanıcı listesinde de uygulama örnekleri arasında paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="c89e1-210">hello user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="c89e1-211">SSO destekli aracısı için SSO üzerinde kapatma</span><span class="sxs-lookup"><span data-stu-id="c89e1-211">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="c89e1-212">Merhaba hello cihazda yüklü Aracısı olduğu bir uygulama toouse yeteneği **varsayılan olarak devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="c89e1-212">hello ability for an application toouse any broker that is installed on hello device is **turned off by default**.</span></span> <span data-ttu-id="c89e1-213">İçinde uygulamanızın toouse sipariş hello Aracısı ile bazı ek yapılandırma adımları ve bazı kodu tooyour uygulama eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c89e1-213">In order toouse your application with hello broker you must do some additional configuration and add some code tooyour application.</span></span>

<span data-ttu-id="c89e1-214">Merhaba adımları toofollow şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c89e1-214">hello steps toofollow are:</span></span>

1. <span data-ttu-id="c89e1-215">Uygulama kodun çağrısı toohello MS SDK Aracısı modunda etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c89e1-215">Enable broker mode in your application code's call toohello MS SDK</span></span>
2. <span data-ttu-id="c89e1-216">Yeni yeniden yönlendirme URI'si oluşturmak ve bu tooboth hello uygulama ve uygulama kaydınızı sağlayın</span><span class="sxs-lookup"><span data-stu-id="c89e1-216">Establish a new redirect URI and provide that tooboth hello app and your app registration</span></span>
3. <span data-ttu-id="c89e1-217">Merhaba Android bildiriminde hello doğru izinleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="c89e1-217">Setting up hello correct permissions in hello Android manifest</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="c89e1-218">1. adım: uygulamanızı Aracısı modunda etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c89e1-218">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="c89e1-219">hello "ayarlar" ya da kimlik doğrulama örneğinizi ilk kurulumu oluşturduğunuzda, uygulama toouse hello Aracısı hello özelliği açıktır.</span><span class="sxs-lookup"><span data-stu-id="c89e1-219">hello ability for your application toouse hello broker is turned on when you create hello "settings" or initial setup of your Authentication instance.</span></span> <span data-ttu-id="c89e1-220">Kodunuzda ApplicationSettings türünüz ayarlayarak bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c89e1-220">You do this by setting your ApplicationSettings type in your code:</span></span>

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="c89e1-221">2. adım: yeni yeniden yönlendirme URI'si URL şeması ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="c89e1-221">Step 2: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="c89e1-222">Her zaman hello kimlik bilgisi toohello doğru uygulama belirteçleri döndürürüz, sipariş tooensure içinde toomake geri tooyour uygulaması, Android işletim sistemi hello şekilde doğrulayabilirsiniz diyoruz emin gerekir.</span><span class="sxs-lookup"><span data-stu-id="c89e1-222">In order tooensure that we always return hello credential tokens toohello correct application, we need toomake sure we call back tooyour application in a way that hello Android operating system can verify.</span></span> <span data-ttu-id="c89e1-223">Merhaba Android işletim sistemi hello Google Play mağazasına hello hello sertifika karmasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="c89e1-223">hello Android operating system uses hello hash of hello certificate in hello Google Play store.</span></span> <span data-ttu-id="c89e1-224">Standart dışı bir uygulama tarafından sahte olamaz.</span><span class="sxs-lookup"><span data-stu-id="c89e1-224">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="c89e1-225">Bu nedenle, biz bu hello belirteçleri toohello doğru uygulama döndürüldüğünü bizim Aracısı uygulama tooensure URI'sini hello birlikte yararlanın.</span><span class="sxs-lookup"><span data-stu-id="c89e1-225">Therefore, we leverage this along with hello URI of our broker application tooensure that hello tokens are returned toohello correct application.</span></span> <span data-ttu-id="c89e1-226">Tooestablish biz bizim Geliştirici Portalı'nda tek tek bir yeniden yönlendirme URI'si bu benzersiz yeniden yönlendirme URI'si hem de uygulama ve kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c89e1-226">We require you tooestablish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="c89e1-227">Yeniden yönlendirme URI'si hello uygun biçiminde olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="c89e1-227">Your redirect URI must be in hello proper form of:</span></span>

`msauth://packagename/Base64UrlencodedSignature`

<span data-ttu-id="c89e1-228">örn: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span><span class="sxs-lookup"><span data-stu-id="c89e1-228">ex: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span></span>

<span data-ttu-id="c89e1-229">Bu yeniden yönlendirme URI'si uygulama kaydınızı hello kullanarak belirtilen toobe gereken [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c89e1-229">This Redirect URI needs toobe specified in your app registration using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="c89e1-230">Azure AD uygulama kaydı hakkında daha fazla bilgi için bkz: [Azure Active Directory ile tümleştirme](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="c89e1-230">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

#### <a name="step-3-set-up-hello-correct-permissions-in-your-application"></a><span data-ttu-id="c89e1-231">3. adım: uygulamanızda hello doğru izinleri ayarlayın</span><span class="sxs-lookup"><span data-stu-id="c89e1-231">Step 3: Set up hello correct permissions in your application</span></span>
<span data-ttu-id="c89e1-232">Aracısı uygulamamız Android uygulamalar arasında hello Hesapları Yöneticisi özelliği hello Android işletim sistemi toomanage kimlik bilgileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="c89e1-232">Our broker application in Android uses hello Accounts Manager feature of hello Android OS toomanage credentials across applications.</span></span> <span data-ttu-id="c89e1-233">Sipariş toouse hello Aracısı Android uygulama bildiriminizi izinleri toouse AccountManager hesapları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c89e1-233">In order toouse hello broker in Android your app manifest must have permissions toouse AccountManager accounts.</span></span> <span data-ttu-id="c89e1-234">Bu ayrıntılı hello olarak ele alınmıştır [Google hesabı Manager belgeleri burada](http://developer.android.com/reference/android/accounts/AccountManager.html)</span><span class="sxs-lookup"><span data-stu-id="c89e1-234">This is discussed in detail in hello [Google documentation for Account Manager here](http://developer.android.com/reference/android/accounts/AccountManager.html)</span></span>

<span data-ttu-id="c89e1-235">Özellikle, bu izinler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c89e1-235">In particular, these permissions are:</span></span>

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a><span data-ttu-id="c89e1-236">SSO yapılandırdıktan!</span><span class="sxs-lookup"><span data-stu-id="c89e1-236">You've configured SSO!</span></span>
<span data-ttu-id="c89e1-237">Şimdi hello Microsoft Identity SDK otomatik olarak hem kimlik bilgileri, uygulamalar arasında paylaşmak ve cihazlarının varsa hello Aracısı çağırma.</span><span class="sxs-lookup"><span data-stu-id="c89e1-237">Now hello Microsoft Identity SDK will automatically both share credentials across your applications and invoke hello broker if it's present on their device.</span></span>

