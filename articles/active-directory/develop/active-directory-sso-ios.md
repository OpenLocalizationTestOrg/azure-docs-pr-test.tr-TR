---
title: "aaaHow tooenable uygulamalar arası SSO'nun ADAL kullanarak iOS | Microsoft Docs"
description: "Nasıl toouse hello özelliklerini uygulamalarınızı boyunca çoklu oturum açma ADAL SDK tooenable hello. "
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: d042d6da-7503-4e20-bb55-06917de01fcd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 04/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: b7b4389a8dcd956211ffa1aaa431aaf21ded8961
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-ios-using-adal"></a><span data-ttu-id="b6ef6-103">Nasıl tooenable uygulamalar arası SSO'nun ADAL kullanarak iOS</span><span class="sxs-lookup"><span data-stu-id="b6ef6-103">How tooenable cross-app SSO on iOS using ADAL</span></span>
<span data-ttu-id="b6ef6-104">Böylece kullanıcılar yalnızca tooenter kimlik bilgilerini bir kez gerekir ve bu kimlik bilgilerini otomatik olarak iş uygulamalarda çoklu oturum açma (SSO) sağlayarak müşteriler tarafından şimdi beklenir.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-104">Providing Single Sign-On (SSO) so that users only need tooenter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="b6ef6-105">ekranda bir telefon araması veya ilerideki kodu gibi ek bir etmen (2FA) kez birlikte küçük, genellikle kullanıcı adı ve parola girme hello zorluk hızlı memnuniyetsizliği kullanıcı sonuçlarında var. toodo bu ürün için birden fazla kez</span><span class="sxs-lookup"><span data-stu-id="b6ef6-105">hello difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has toodo this more than one time for your product.</span></span>

<span data-ttu-id="b6ef6-106">Ayrıca, Microsoft Accounts veya Office365 iş hesabından gibi diğer uygulamaları kullanabilir bir kimlik platformu uygularsanız, müşterilerin kimlik bilgileri bu toobe kullanılabilir toouse tüm uygulamalar arasında Hayır, hello satıcı önemli bekler.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials toobe available toouse across all their applications no matter hello vendor.</span></span>

<span data-ttu-id="b6ef6-107">Merhaba, Microsoft Identity SDK ile birlikte Microsoft Identity platform tüm bu sabit sizin ve SSO ya da kendi paketi uygulamaların veya olarak içinde müşterilerinizle özelliği toodelight hello verir çalışır bizim Aracısı yetenek ve Doğrulayıcı Merhaba tüm aygıt üzerinden uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-107">hello Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you hello ability toodelight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across hello entire device.</span></span>

<span data-ttu-id="b6ef6-108">Bu kılavuz size nasıl söyleyecektir tooconfigure bizim SDK, uygulama tooprovide içinde bu avantajı tooyour müşteriler.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-108">This walkthrough will tell you how tooconfigure our SDK within your application tooprovide this benefit tooyour customers.</span></span>

<span data-ttu-id="b6ef6-109">Bu kılavuz için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="b6ef6-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="b6ef6-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b6ef6-110">Azure Active Directory</span></span>
* <span data-ttu-id="b6ef6-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="b6ef6-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="b6ef6-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="b6ef6-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="b6ef6-113">Azure Active Directory Koşullu Erişim</span><span class="sxs-lookup"><span data-stu-id="b6ef6-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="b6ef6-114">Merhaba belge önceki varsayar nasıl çok bildiğiniz[sağlamak hello eski portalı uygulamalarında Azure Active Directory için](active-directory-how-to-integrate.md) ve uygulamanızı hello ile tümleşik [Microsoft Identity iOS SDK'sı](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span><span class="sxs-lookup"><span data-stu-id="b6ef6-114">hello document preceding assumes you know how too[provision applications in hello legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with hello [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span></span>

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a><span data-ttu-id="b6ef6-115">Microsoft kimlik platformu hello SSO kavramlar</span><span class="sxs-lookup"><span data-stu-id="b6ef6-115">SSO Concepts in hello Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="b6ef6-116">Microsoft Identity aracıları</span><span class="sxs-lookup"><span data-stu-id="b6ef6-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="b6ef6-117">Microsoft hello kimlik bilgilerini farklı satıcılardan uygulamalar arasında köprü oluşturma için izin uygulamaları mobil her platform için sağlar ve nerede tek güvenli bir yerde gerektiren özel Gelişmiş özellikleri sağlar toovalidate kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-117">Microsoft provides applications for every mobile platform that allow for hello bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where toovalidate credentials.</span></span> <span data-ttu-id="b6ef6-118">Bunlar diyoruz **aracıların**.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-118">We call these **brokers**.</span></span> <span data-ttu-id="b6ef6-119">İOS ve Android cihazlarda bu aracıların müşteriler bağımsız olarak yüklemek veya toohello aygıt bazılarını veya tümünü hello cihaz için kendi çalışan yöneten bir şirket tarafından gönderilen indirilebilir uygulamaları aracılığıyla sağlanır.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-119">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages some or all of hello device for their employee.</span></span> <span data-ttu-id="b6ef6-120">Bu aracıları yönetme güvenlik yalnızca bazı uygulamalar veya ne BT yöneticileri işlemleriniz dayalı hello tüm cihaz desteği.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-120">These brokers support managing security just for some applications or hello entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="b6ef6-121">Windows, bu işlev toohello işletim sistemi, teknik olarak Web kimlik doğrulama Aracısı hello bilinen yerleşik bir hesabı seçicide tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-121">In Windows, this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>

<span data-ttu-id="b6ef6-122">Hakkında daha fazla bilgi için bu aracıların ve nasıl müşterilerinizin bunları okuyun hello Microsoft Identity platform için kullanıcıların oturum açma akışını görebileceğiniz kullanırız.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-122">For more information on how we use these brokers and how your customers might see them in their login flow for hello Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="b6ef6-123">Mobil cihazlarda günlüğe kaydetme için desenleri</span><span class="sxs-lookup"><span data-stu-id="b6ef6-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="b6ef6-124">Erişim toocredentials cihazlarda hello Microsoft Identity platformuna yönelik iki temel düzenlerden izleyin:</span><span class="sxs-lookup"><span data-stu-id="b6ef6-124">Access toocredentials on devices follow two basic patterns for hello Microsoft Identity platform:</span></span>

* <span data-ttu-id="b6ef6-125">Olmayan Aracısı Yardımlı oturum açmalar</span><span class="sxs-lookup"><span data-stu-id="b6ef6-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="b6ef6-126">Yardımlı Oturum Aracısı</span><span class="sxs-lookup"><span data-stu-id="b6ef6-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="b6ef6-127">Olmayan Aracısı Yardımlı oturum açmalar</span><span class="sxs-lookup"><span data-stu-id="b6ef6-127">Non-broker assisted logins</span></span>
<span data-ttu-id="b6ef6-128">Olmayan Aracısı Yardımlı satır içi hello uygulamayla gerçekleşir ve hello cihazda bu uygulama için hello yerel depolama kullanan oturum açma deneyimlerini oturumlardır.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-128">Non-broker assisted logins are login experiences that happen inline with hello application and use hello local storage on hello device for that application.</span></span> <span data-ttu-id="b6ef6-129">Bu depolama uygulamalar arasında paylaşılıyor olabilir ancak sıkı şekilde bağlı toohello uygulama ya da bu kimlik bilgilerini kullanarak uygulama paketi hello kimlik bilgileridir.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-129">This storage may be shared across applications but hello credentials are tightly bound toohello app or suite of apps using that credential.</span></span> <span data-ttu-id="b6ef6-130">Bir kullanıcı adı ve parola hello uygulamanın kendi içinde girdiğinizde, bu büyük olasılıkla birçok mobil uygulamalarda tecrübe ettiklerinize.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-130">You've most likely experienced this in many mobile applications when you enter a username and password within hello application itself.</span></span>

<span data-ttu-id="b6ef6-131">Bu oturumlar hello aşağıdaki faydaları vardır:</span><span class="sxs-lookup"><span data-stu-id="b6ef6-131">These logins have hello following benefits:</span></span>

* <span data-ttu-id="b6ef6-132">Kullanıcı deneyimi tamamen hello uygulaması içinde zaten var.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-132">User experience exists entirely within hello application.</span></span>
* <span data-ttu-id="b6ef6-133">Kimlik bilgileri, hello tarafından imzalanmış uygulamalar arasında paylaşılabilir aynı sertifika, çoklu oturum açma deneyimini tooyour suite uygulamaların sağlama.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-133">Credentials can be shared across applications that are signed by hello same certificate, providing a single sign-on experience tooyour suite of applications.</span></span>
* <span data-ttu-id="b6ef6-134">Denetim Günlüğü'nde hello deneyimi geçici toohello uygulama önce ve sonra oturum açma sağlanır.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-134">Control around hello experience of logging in is provided toohello application before and after sign-in.</span></span>

<span data-ttu-id="b6ef6-135">Bu oturumlar dezavantajları aşağıdaki hello vardır:</span><span class="sxs-lookup"><span data-stu-id="b6ef6-135">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="b6ef6-136">Kullanıcı yalnızca bu Microsoft uygulamanızı yapılandırılmış Identities arasında Microsoft Identity kullanan tüm uygulamalar boyunca çoklu oturum açma deneyimi olamaz.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="b6ef6-137">Uygulamanız, koşullu erişim veya kullanımı hello Intune ürün paketi gibi daha gelişmiş iş özellikleriyle kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-137">Your application cannot be used with more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="b6ef6-138">Uygulamanızı iş kullanıcıları için sertifika tabanlı kimlik doğrulamasını destekleyemez.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="b6ef6-139">Merhaba Microsoft Identity SDK'ları, uygulamaları tooenable SSO hello paylaşılan depolama ile nasıl bir temsilini şöyledir:</span><span class="sxs-lookup"><span data-stu-id="b6ef6-139">Here is a representation of how hello Microsoft Identity SDKs work with hello shared storage of your applications tooenable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| ADAL SDK  |  |  ADAL SDK  |  |  ADAK SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="b6ef6-140">Yardımlı Oturum Aracısı</span><span class="sxs-lookup"><span data-stu-id="b6ef6-140">Broker assisted logins</span></span>
<span data-ttu-id="b6ef6-141">Aracısı destekli hello Aracısı uygulama içinde oluşur ve hello depolama ve güvenlik hello Aracısı tooshare kimlik bilgilerinin hello Microsoft Identity platform uygulanan tüm uygulamalar için hello aygıtta kullanan oturum açma deneyimlerini oturumlardır.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-141">Broker-assisted logins are login experiences that occur within hello broker application and use hello storage and security of hello broker tooshare credentials across all applications on hello device that apply hello Microsoft Identity platform.</span></span> <span data-ttu-id="b6ef6-142">Bu, uygulamalarınız hello Aracısı toosign kullanıcılar kullandığını anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-142">This means that your applications rely on hello broker toosign users in.</span></span> <span data-ttu-id="b6ef6-143">İOS ve Android cihazlarda bu aracıların müşteriler bağımsız olarak yüklemek veya toohello aygıt hello cihaz kendi kullanıcı yöneten bir şirket tarafından gönderilen indirilebilir uygulamaları aracılığıyla sağlanır.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages hello device for their user.</span></span> <span data-ttu-id="b6ef6-144">Merhaba Microsoft Authenticator uygulaması iOS bu tür bir uygulama örneğidir.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-144">An example of this type of application is hello Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="b6ef6-145">Windows bu işlevselliği toohello işletim sistemi, teknik olarak Web kimlik doğrulama Aracısı hello bilinen yerleşik bir hesabı seçicide tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-145">In Windows this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>
<span data-ttu-id="b6ef6-146">Merhaba deneyimi platforma göre değişir ve kesintiye uğratan toousers bazen olabilir değilse doğru şekilde yönetilir.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-146">hello experience varies by platform and can sometimes be disruptive toousers if not managed correctly.</span></span> <span data-ttu-id="b6ef6-147">Merhaba Facebook uygulamanın yüklü olması ve başka bir uygulamadan Facebook bağlanmak kullanırsanız bu deseni ile en biliyor.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-147">You're probably most familiar with this pattern if you have hello Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="b6ef6-148">Merhaba Microsoft kimlik platformu kullandığı aynı düzeni hello.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-148">hello Microsoft Identity platform uses hello same pattern.</span></span>

<span data-ttu-id="b6ef6-149">İOS için bu tooa "geçiş" animasyon Burada, uygulamanızın hello Microsoft Authenticator uygulamaları toohello arka toohello ön hello kullanıcı tooselect için gelen gönderilen toosign ile istediğiniz hangi hesabı doğurur.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-149">For iOS this leads tooa "transition" animation where your application is sent toohello background while hello Microsoft Authenticator applications comes toohello foreground for hello user tooselect which account they would like toosign in with.</span></span>  

<span data-ttu-id="b6ef6-150">Android ve Windows hello hesabı seçicide daha az kesintiye uğratan toohello kullanıcı olan, uygulamanızın üzerinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-150">For Android and Windows hello account chooser is displayed on top of your application which is less disruptive toohello user.</span></span>

#### <a name="how-hello-broker-gets-invoked"></a><span data-ttu-id="b6ef6-151">Merhaba Aracısı nasıl çağrılır</span><span class="sxs-lookup"><span data-stu-id="b6ef6-151">How hello broker gets invoked</span></span>
<span data-ttu-id="b6ef6-152">Uyumlu bir aracı hello Microsoft Authenticator uygulaması, hello Microsoft Identity SDK'ları otomatik olarak ayarlanır gibi hello aygıtta yüklüyse, bir kullanıcı herhangi bir hesabı kullanarak toolog istedikleri belirttiğinde hello broker çağırma iş hello Merhaba Microsoft Identity platform.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-152">If a compatible broker is installed on hello device, like hello Microsoft Authenticator application, hello Microsoft Identity SDKs will automatically do hello work of invoking hello broker for you when a user indicates they wish toolog in using any account from hello Microsoft Identity platform.</span></span> <span data-ttu-id="b6ef6-153">Bu hesap, kişisel Microsoft Account, bir iş veya Okul hesabı veya bir sağladığınız hesap ve konak B2C ve B2B Ürünlerimiz kullanarak azure'da olabilir.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 

 #### <a name="how-we-ensure-hello-application-is-valid"></a><span data-ttu-id="b6ef6-154">Biz Merhaba uygulaması nasıl emin geçerlidir</span><span class="sxs-lookup"><span data-stu-id="b6ef6-154">How we ensure hello application is valid</span></span>
 
 <span data-ttu-id="b6ef6-155">Merhaba gerek tooensure hello bir uygulama çağrısı hello Aracısı destekli Aracısı oturum açma bilgilerini sağladığımız önemli toohello güvenlik kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-155">hello need tooensure hello identity of an application call hello broker is crucial toohello security we provide in broker assisted logins.</span></span> <span data-ttu-id="b6ef6-156">İOS ne Android kötü amaçlı uygulamalar ve "yasal uygulamanın tanımlayıcı aldatıcı" Merhaba yasal uygulaması için amacı hello belirteçleri almak için yalnızca belirli bir uygulama için geçerli olan benzersiz tanımlayıcıları zorlar.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive hello tokens meant for hello legitimate application.</span></span> <span data-ttu-id="b6ef6-157">Biz her zaman zamanında hello doğru uygulama ile iletişim kuran tooensure, biz hello Geliştirici tooprovide özel redirectURI kendi uygulama Microsoft ile kaydedilirken isteyin.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-157">tooensure we are always communicating with hello right application at runtime, we ask hello developer tooprovide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="b6ef6-158">**Geliştiricilerin bu yeniden yönlendirme URI'si nasıl oluşturabilir aşağıda ayrıntılı olarak ele alınmıştır.**</span><span class="sxs-lookup"><span data-stu-id="b6ef6-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="b6ef6-159">Bu özel redirectURI ve toobe benzersiz toohello uygulama hello Apple App Store tarafından güvence altına hello hello uygulama paket Kimliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-159">This custom redirectURI contains hello Bundle ID of hello application and is ensured toobe unique toohello application by hello Apple App Store.</span></span> <span data-ttu-id="b6ef6-160">Bir uygulama çağrıları hello Aracısı hello iOS hello Aracısı sorduğunda işletim sistemi tooprovide ile Merhaba hello Aracısı adlı bir paket kimliği.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-160">When an application calls hello broker, hello broker asks hello iOS operating system tooprovide it with hello Bundle ID that called hello broker.</span></span> <span data-ttu-id="b6ef6-161">Merhaba Aracısı bu paket kimliği tooMicrosoft hello çağrısı tooour kimlik sistemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-161">hello broker provides this Bundle ID tooMicrosoft in hello call tooour identity system.</span></span> <span data-ttu-id="b6ef6-162">Merhaba hello uygulama paket Kimliğini paket kimliği kayıt sırasında toous hello geliştirici tarafından sağlanan hello eşleşmiyorsa hello kaynak hello uygulama istenirken için size erişim toohello belirteçleri reddeder.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-162">If hello Bundle ID of hello application does not match hello Bundle ID provided toous by hello developer during registration, we will deny access toohello tokens for hello resource hello application is requesting.</span></span> <span data-ttu-id="b6ef6-163">Bu denetim yalnızca hello geliştirici tarafından kayıtlı hello uygulama belirteçlerini almasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-163">This check ensures that only hello application registered by hello developer receives tokens.</span></span>

<span data-ttu-id="b6ef6-164">**Microsoft Identity SDK Hello hello Aracısı çağıran veya hello aracı olmayan Yardımlı akış kullanıyorsa, hello Geliştirici hello seçimine sahiptir.**</span><span class="sxs-lookup"><span data-stu-id="b6ef6-164">**hello developer has hello choice of if hello Microsoft Identity SDK calls hello broker or uses hello non-broker assisted flow.**</span></span> <span data-ttu-id="b6ef6-165">Hello geliştirici değil toouse hello Aracısı destekli akış seçerse, ancak bunlar hello yararı SSO kimlik bilgilerini kullanarak bu hello kullanıcı kaybedersiniz hello aygıtta eklemiş olabilir ve kendi uygulama Microsoft iş özelliklerle kullanılmasını engeller Koşullu erişim, Intune yönetim özellikleri ve sertifika tabanlı kimlik doğrulaması gibi müşterilerinin sağlar.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-165">However if hello developer chooses not toouse hello broker-assisted flow they lose hello benefit of using SSO credentials that hello user may have already added on hello device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="b6ef6-166">Bu oturumlar hello aşağıdaki faydaları vardır:</span><span class="sxs-lookup"><span data-stu-id="b6ef6-166">These logins have hello following benefits:</span></span>

* <span data-ttu-id="b6ef6-167">Kullanıcı, kendi hello satıcı olursa olsun tüm uygulamalar arasında SSO karşılaşır.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-167">User experiences SSO across all their applications no matter hello vendor.</span></span>
* <span data-ttu-id="b6ef6-168">Uygulamanız, koşullu erişim gibi daha gelişmiş iş özellikleri kullanın veya ürün hello Intune paketi kullanın.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-168">Your application can use more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="b6ef6-169">Uygulamanızı iş kullanıcıları için sertifika tabanlı kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="b6ef6-170">Çok daha güvenli oturum açma hello uygulama ve hello kullanıcı hello kimliği doğrulandı gibi ek güvenlik algoritmalarını ve şifreleme ile Merhaba Aracısı uygulaması tarafından karşılaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-170">Much more secure sign-in experience as hello identity of hello application and hello user are verified by hello broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="b6ef6-171">Bu oturumlar dezavantajları aşağıdaki hello vardır:</span><span class="sxs-lookup"><span data-stu-id="b6ef6-171">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="b6ef6-172">Kimlik bilgileri seçilen sırada hello kullanıcı iOS uygulamanızın deneyimi dışında geçti.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-172">In iOS hello user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="b6ef6-173">Kayıp hello özelliği toomanage hello oturum açma deneyimi müşterilerinize uygulamanızın içinde.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-173">Loss of hello ability toomanage hello login experience for your customers within your application.</span></span>

<span data-ttu-id="b6ef6-174">Nasıl hello Microsoft Identity SDK'ları hello çalışmak Aracısı uygulamaları tooenable SSO bir temsilini şöyledir:</span><span class="sxs-lookup"><span data-stu-id="b6ef6-174">Here is a representation of how hello Microsoft Identity SDKs work with hello broker applications tooenable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
| Azure SDK  | | Azure SDK  |   | Azure SDK   |
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

<span data-ttu-id="b6ef6-175">Bu bilgiler ile çağrılmak mümkün toobetter olmalıdır anlamanıza ve SSO hello Microsoft Identity platform ve SDK'ları kullanarak uygulamanızdaki uygulamanıza.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-175">Armed with this background information you should be able toobetter understand and implement SSO within your application using hello Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="b6ef6-176">ADAL kullanarak uygulamalar arası SSO'nun etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="b6ef6-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="b6ef6-177">Merhaba ADAL iOS SDK'sı burada kullandığımız için:</span><span class="sxs-lookup"><span data-stu-id="b6ef6-177">Here we use hello ADAL iOS SDK to:</span></span>

* <span data-ttu-id="b6ef6-178">Aracı olmayan Yardımlı SSO Uygulama paketiniz için Aç</span><span class="sxs-lookup"><span data-stu-id="b6ef6-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="b6ef6-179">Aracısı destekli SSO desteği Aç</span><span class="sxs-lookup"><span data-stu-id="b6ef6-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="b6ef6-180">Aracı olmayan için SSO üzerinde kapatma SSO Destekli</span><span class="sxs-lookup"><span data-stu-id="b6ef6-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="b6ef6-181">Uygulamalar arasında aracı olmayan Yardımlı SSO için hello Microsoft Identity SDK'ları yönetmek SSO hello karmaşıklığını çoğunu sizin için.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-181">For non-broker assisted SSO across applications hello Microsoft Identity SDKs manage much of hello complexity of SSO for you.</span></span> <span data-ttu-id="b6ef6-182">Bu, hello Önbelleği'nde hello doğru kullanıcı bulma ve bakımını yapma, tooquery için oturum açan kullanıcıların listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-182">This includes finding hello right user in hello cache and maintaining a list of logged in users for you tooquery.</span></span>

<span data-ttu-id="b6ef6-183">Aşağıdaki toodo hello ihtiyacınız sahip uygulamalar arasında SSO tooenable:</span><span class="sxs-lookup"><span data-stu-id="b6ef6-183">tooenable SSO across applications you own you need toodo hello following:</span></span>

1. <span data-ttu-id="b6ef6-184">Tüm, uygulamaların kullanıcı hello aynı istemci Kimliğini veya uygulama kimliği emin olun</span><span class="sxs-lookup"><span data-stu-id="b6ef6-184">Ensure all your applications user hello same Client ID or Application ID.</span></span>
2. <span data-ttu-id="b6ef6-185">Tüm aynı imzalama sertifikası Apple'dan anahtarlıklar paylaştırabilirsiniz, uygulama paylaşımı hello olun</span><span class="sxs-lookup"><span data-stu-id="b6ef6-185">Ensure that all of your applications share hello same signing certificate from Apple so that you can share keychains</span></span>
3. <span data-ttu-id="b6ef6-186">İstek Merhaba, uygulamaların her biri için aynı Anahtarlık yetkilerini.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-186">Request hello same keychain entitlement for each of your applications.</span></span>
4. <span data-ttu-id="b6ef6-187">Hello Microsoft Identity SDK'ları hakkında paylaşılan hello Anahtarlık toouse istediğiniz bize bildirin.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-187">Tell hello Microsoft Identity SDKs about hello shared keychain you want us toouse.</span></span>

#### <a name="using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a><span data-ttu-id="b6ef6-188">Merhaba aynı istemci kimliği kullanarak / tüm uygulamaların paketiniz uygulamalarda hello için uygulama kimliği</span><span class="sxs-lookup"><span data-stu-id="b6ef6-188">Using hello same Client ID / Application ID for all hello applications in your suite of apps</span></span>
<span data-ttu-id="b6ef6-189">Bu tooshare belirteçleri, uygulamalar arasında izin verildiğini sırayla hello Microsoft Identity platform tooknow için uygulamalarınızın her birinde aynı istemci Kimliğini veya uygulama kimliği tooshare hello gerekir</span><span class="sxs-lookup"><span data-stu-id="b6ef6-189">In order for hello Microsoft Identity platform tooknow that it's allowed tooshare tokens across your applications, each of your applications will need tooshare hello same Client ID or Application ID.</span></span> <span data-ttu-id="b6ef6-190">Bu ilk uygulamanızı hello Portalı'nda kayıtlı yükleyen tooyou sağlanan hello benzersiz tanımlayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-190">This is hello unique identifier that was provided tooyou when you registered your first application in hello portal.</span></span>

<span data-ttu-id="b6ef6-191">Farklı uygulamaları nasıl kullanacağını merak ediyor toohello onu kullanıyorsa, Microsoft Identity hizmet hello aynı uygulama kimliği</span><span class="sxs-lookup"><span data-stu-id="b6ef6-191">You may be wondering how you will identify different apps toohello Microsoft Identity service if it uses hello same Application ID.</span></span> <span data-ttu-id="b6ef6-192">Merhaba cevaptır ile Merhaba **yeniden yönlendirme URI'ler**.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-192">hello answer is with hello **Redirect URIs**.</span></span> <span data-ttu-id="b6ef6-193">Her uygulamanın birden çok yeniden yönlendirme hello hazırlama Portalı'nda kayıtlı URI'ler olabilir.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-193">Each application can have multiple Redirect URIs registered in hello onboarding portal.</span></span> <span data-ttu-id="b6ef6-194">Her uygulama paketiniz içinde farklı bir yeniden yönlendirme URI'sine sahip olur.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-194">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="b6ef6-195">Bu sistem, bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b6ef6-195">An example of how this looks is below:</span></span>

<span data-ttu-id="b6ef6-196">App1 yeniden yönlendirme URİ'si:`x-msauth-mytestiosapp://com.myapp.mytestapp`</span><span class="sxs-lookup"><span data-stu-id="b6ef6-196">App1 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span></span>

<span data-ttu-id="b6ef6-197">App2 yeniden yönlendirme URİ'si:`x-msauth-mytestiosapp://com.myapp.mytestapp2`</span><span class="sxs-lookup"><span data-stu-id="b6ef6-197">App2 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span></span>

<span data-ttu-id="b6ef6-198">App3 yeniden yönlendirme URİ'si:`x-msauth-mytestiosapp://com.myapp.mytestapp3`</span><span class="sxs-lookup"><span data-stu-id="b6ef6-198">App3 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span></span>

<span data-ttu-id="b6ef6-199">....</span><span class="sxs-lookup"><span data-stu-id="b6ef6-199">....</span></span>

<span data-ttu-id="b6ef6-200">Bunlar altında yuvalanmış aynı istemci kimliği hello / uygulama kimliği ve Aranan göre hello redirect URI SDK yapılandırmanızda toous döndürür.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-200">These are nested under hello same client ID / application ID and looked up based on hello redirect URI you return toous in your SDK configuration.</span></span>

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


<span data-ttu-id="b6ef6-201">*Bu yeniden yönlendirme URI biçimi hello Not aşağıda açıklanmıştır. Toosupport hello Aracısı istediğiniz sürece herhangi bir yeniden yönlendirme URI'si kullanabilir, bu durumda bunlar şunun gibi hello yukarıdaki görünmesi gerekir*</span><span class="sxs-lookup"><span data-stu-id="b6ef6-201">*Note that hello format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish toosupport hello broker, in which case they must look something like hello above*</span></span>

#### <a name="create-keychain-sharing-between-applications"></a><span data-ttu-id="b6ef6-202">Uygulamalar arasında paylaşma Anahtarlık oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6ef6-202">Create keychain sharing between applications</span></span>
<span data-ttu-id="b6ef6-203">Anahtarlık paylaşımının etkinleştirilmesi hello bu belgenin kapsamı dışındadır ve Apple'nın kendi belgede ele alınan [yetenekleri ekleme](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span><span class="sxs-lookup"><span data-stu-id="b6ef6-203">Enabling keychain sharing is beyond hello scope of this document and covered by Apple in their document [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span></span> <span data-ttu-id="b6ef6-204">Önemli olarak adlandırılan, Anahtarlık toobe istediğinize karar verin ve tüm uygulamalar için bu özelliği eklemek olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-204">What is important is that you decide what you want your keychain toobe called and add that capability across all your applications.</span></span>

<span data-ttu-id="b6ef6-205">Varsa doğru ayarladığınıza yetkilendirmeler yetkili proje dizininde bir dosyasına görmelisiniz `entitlements.plist` hello şuna benzeyen bir şey içeren:</span><span class="sxs-lookup"><span data-stu-id="b6ef6-205">When you do have entitlements set up correctly you should see a file in your project directory entitled `entitlements.plist` that contains something that looks like hello following:</span></span>

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>keychain-access-groups</key>
    <array>
        <string>$(AppIdentifierPrefix)com.myapp.mytestapp</string>
        <string>$(AppIdentifierPrefix)com.myapp.mycache</string>
    </array>
</dict>
</plist>
```

<span data-ttu-id="b6ef6-206">Her uygulamalarınız etkinleştirdiği hello Anahtarlık yetkilendirme varsa, ve hazır toouse SSO sonra hello Microsoft Identity SDK hakkında Anahtarlık ayarında aşağıdaki hello kullanarak söyleyin, `ADAuthenticationSettings` ayarı aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="b6ef6-206">Once you have hello keychain entitlement enabled in each of your applications, and you are ready toouse SSO, tell hello Microsoft Identity SDK about your keychain by using hello following setting in your `ADAuthenticationSettings` with hello following setting:</span></span>

```
defaultKeychainSharingGroup=@"com.myapp.mycache";
```

> [!WARNING]
> <span data-ttu-id="b6ef6-207">Uygulamalar arasında bir Anahtarlık paylaştığınızda herhangi bir uygulama kullanıcıların silin veya tüm hello belirteçleri, uygulamanızda da kötüsü silin.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-207">When you share a keychain across your applications any application can delete users or worse delete all hello tokens across your application.</span></span> <span data-ttu-id="b6ef6-208">Merhaba belirteçleri toodo arka plan çalışması üzerinde kullanan uygulamalar varsa, özellikle felaket niteliğinde budur.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-208">This is particularly disastrous if you have applications that rely on hello tokens toodo background work.</span></span> <span data-ttu-id="b6ef6-209">Bir Anahtarlık paylaşımı kaldırma işlemleri hello Microsoft Identity SDK'ları aracılığıyla içindeki tüm çok dikkatli olmalıdır anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-209">Sharing a keychain means that you must be very careful in any and all remove operations through hello Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="b6ef6-210">İşte bu kadar!</span><span class="sxs-lookup"><span data-stu-id="b6ef6-210">That's it!</span></span> <span data-ttu-id="b6ef6-211">Microsoft Identity SDK Hello şimdi tüm uygulamalar için kimlik bilgileri paylaşacaktır.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-211">hello Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="b6ef6-212">Merhaba kullanıcı listesinde de uygulama örnekleri arasında paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-212">hello user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="b6ef6-213">SSO destekli aracısı için SSO üzerinde kapatma</span><span class="sxs-lookup"><span data-stu-id="b6ef6-213">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="b6ef6-214">Merhaba hello cihazda yüklü Aracısı olduğu bir uygulama toouse yeteneği **varsayılan olarak devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-214">hello ability for an application toouse any broker that is installed on hello device is **turned off by default**.</span></span> <span data-ttu-id="b6ef6-215">İçinde uygulamanızın toouse sipariş hello Aracısı ile bazı ek yapılandırma adımları ve bazı kodu tooyour uygulama eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-215">In order toouse your application with hello broker you must do some additional configuration and add some code tooyour application.</span></span>

<span data-ttu-id="b6ef6-216">Merhaba adımları toofollow şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b6ef6-216">hello steps toofollow are:</span></span>

1. <span data-ttu-id="b6ef6-217">Uygulama kodun çağrısı toohello MS SDK Aracısı modunda etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-217">Enable broker mode in your application code's call toohello MS SDK.</span></span>
2. <span data-ttu-id="b6ef6-218">Yeni yeniden yönlendirme URI'si oluşturmak ve bu tooboth hello uygulama ve uygulama kaydınızı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-218">Establish a new redirect URI and provide that tooboth hello app and your app registration.</span></span>
3. <span data-ttu-id="b6ef6-219">URL şeması kaydediliyor.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-219">Registering a URL Scheme.</span></span>
4. <span data-ttu-id="b6ef6-220">iOS9 desteği: izni tooyour info.plist dosyası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-220">iOS9 Support: Add a permission tooyour info.plist file.</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="b6ef6-221">1. adım: uygulamanızı Aracısı modunda etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="b6ef6-221">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="b6ef6-222">hello "context" ya da kimlik doğrulama nesnenizin ilk kurulum oluşturduğunuzda, uygulama toouse hello Aracısı hello özelliği açıktır.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-222">hello ability for your application toouse hello broker is turned on when you create hello "context" or initial setup of your Authentication object.</span></span> <span data-ttu-id="b6ef6-223">Kimlik bilgileri türü kodunuzda ayarlayarak bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b6ef6-223">You do this by setting your credentials type in your code:</span></span>

```
/*! See hello ADCredentialsType enumeration definition for details */
@propertyADCredentialsType credentialsType;
```
<span data-ttu-id="b6ef6-224">Merhaba `AD_CREDENTIALS_AUTO` ayarı hello Microsoft Identity SDK tootry toocall toohello Aracısı çıkışı izin `AD_CREDENTIALS_EMBEDDED` hello Microsoft Identity SDK toohello Aracısı çağırma engeller.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-224">hello `AD_CREDENTIALS_AUTO` setting will allow hello Microsoft Identity SDK tootry toocall out toohello broker, `AD_CREDENTIALS_EMBEDDED` will prevent hello Microsoft Identity SDK from calling toohello broker.</span></span>

#### <a name="step-2-registering-a-url-scheme"></a><span data-ttu-id="b6ef6-225">2. adım: bir URL şemasını kaydetme</span><span class="sxs-lookup"><span data-stu-id="b6ef6-225">Step 2: Registering a URL Scheme</span></span>
<span data-ttu-id="b6ef6-226">Merhaba Microsoft Identity platformu URL'leri tooinvoke hello aracısı ve ardından dönüş denetim geri tooyour uygulaması kullanır.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-226">hello Microsoft Identity platform uses URLs tooinvoke hello broker and then return control back tooyour application.</span></span> <span data-ttu-id="b6ef6-227">toofinish bir URL şemasını ihtiyacınız o gidiş dönüş bu hello Microsoft Platformu hakkında bilirsiniz Identity uygulamanız için kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-227">toofinish that round trip you need a URL scheme registered for your application that hello Microsoft Identity platform will know about.</span></span> <span data-ttu-id="b6ef6-228">Bu ek olarak tooany daha önce kaydettirdiğiniz uygulamanızla diğer uygulama düzenleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-228">This can be in addition tooany other app schemes you may have previously registered with your application.</span></span>

> [!WARNING]
> <span data-ttu-id="b6ef6-229">URL şeması oldukça benzersiz toominimize hello hello kullanarak başka bir uygulama olasılığını hello yapmadan öneririz aynı URL şeması.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-229">We recommend making hello URL scheme fairly unique toominimize hello chances of another app using hello same URL scheme.</span></span> <span data-ttu-id="b6ef6-230">Apple hello uygulama Mağazası'nda kayıtlı URL şemalarını hello benzersizliğini uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-230">Apple does not enforce hello uniqueness of URL schemes that are registered in hello app store.</span></span>
> 
> 

<span data-ttu-id="b6ef6-231">Aşağıda, bu proje yapılandırmanızda görünme bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-231">Below is an example of how this appears in your project configuration.</span></span> <span data-ttu-id="b6ef6-232">Ayrıca bu Xcode'da de yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b6ef6-232">You may also do this in XCode as well:</span></span>

```
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>com.myapp.mytestapp</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>x-msauth-mytestiosapp</string>
        </array>
    </dict>
</array>
```

#### <a name="step-3-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="b6ef6-233">Adım 3: yeni yeniden yönlendirme URI'si URL şeması ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6ef6-233">Step 3: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="b6ef6-234">Her zaman hello kimlik bilgisi toohello doğru uygulama belirteçleri döndürürüz, sipariş tooensure içinde toomake geri tooyour uygulaması, iOS işletim sistemi hello şekilde doğrulayabilirsiniz diyoruz emin gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-234">In order tooensure that we always return hello credential tokens toohello correct application, we need toomake sure we call back tooyour application in a way that hello iOS operating system can verify.</span></span> <span data-ttu-id="b6ef6-235">Merhaba iOS işletim sistemi raporları toohello Microsoft Aracısı uygulamaları, çağırma hello uygulama paket Kimliğini hello.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-235">hello iOS operating system reports toohello Microsoft broker applications hello Bundle ID of hello application calling it.</span></span> <span data-ttu-id="b6ef6-236">Standart dışı bir uygulama tarafından sahte olamaz.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-236">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="b6ef6-237">Bu nedenle, biz bu hello belirteçleri toohello doğru uygulama döndürüldüğünü bizim Aracısı uygulama tooensure URI'sini hello birlikte yararlanın.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-237">Therefore, we leverage this along with hello URI of our broker application tooensure that hello tokens are returned toohello correct application.</span></span> <span data-ttu-id="b6ef6-238">Tooestablish biz bizim Geliştirici Portalı'nda tek tek bir yeniden yönlendirme URI'si bu benzersiz yeniden yönlendirme URI'si hem de uygulama ve kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-238">We require you tooestablish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="b6ef6-239">Yeniden yönlendirme URI'si hello uygun biçiminde olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="b6ef6-239">Your redirect URI must be in hello proper form of:</span></span>

`<app-scheme>://<your.bundle.id>`

<span data-ttu-id="b6ef6-240">örn: *x msauth mytestiosapp://com.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="b6ef6-240">ex: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span></span>

<span data-ttu-id="b6ef6-241">Bu yeniden yönlendirme URI'si uygulama kaydınızı hello kullanarak belirtilen toobe gereken [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b6ef6-241">This Redirect URI needs toobe specified in your app registration using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="b6ef6-242">Azure AD uygulama kaydı hakkında daha fazla bilgi için bkz: [Azure Active Directory ile tümleştirme](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="b6ef6-242">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

##### <a name="step-3a-add-a-redirect-uri-in-your-app-and-dev-portal-toosupport-certificate-based-authentication"></a><span data-ttu-id="b6ef6-243">Adım 3a: yeniden yönlendirme URI'si, uygulama ve Geliştirici Portalı toosupport sertifika tabanlı kimlik doğrulaması ekleme</span><span class="sxs-lookup"><span data-stu-id="b6ef6-243">Step 3a: Add a redirect URI in your app and dev portal toosupport certificate based authentication</span></span>
<span data-ttu-id="b6ef6-244">toosupport sertifikası tabanlı kimlik doğrulaması ikinci "msauth" gerekiyor, uygulama ve hello kayıtlı toobe [Azure portal](https://portal.azure.com/) tooadd istiyorsanız toohandle sertifika kimlik doğrulamasını destekleyen uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-244">toosupport cert based authentication a second "msauth"  needs toobe registered in your application and hello [Azure portal](https://portal.azure.com/) toohandle certificate authentication if you wish tooadd that support in your application.</span></span>

`msauth://code/<broker-redirect-uri-in-url-encoded-form>`

<span data-ttu-id="b6ef6-245">örn: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span><span class="sxs-lookup"><span data-stu-id="b6ef6-245">ex: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span></span>

#### <a name="step-4-ios9-add-a-configuration-parameter-tooyour-app"></a><span data-ttu-id="b6ef6-246">4. adım: iOS9: bir yapılandırma parametresi tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="b6ef6-246">Step 4: iOS9: Add a configuration parameter tooyour app</span></span>
<span data-ttu-id="b6ef6-247">ADAL kullanan – canOpenURL: hello Aracısı hello cihazda yüklü değilse toocheck.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-247">ADAL uses –canOpenURL: toocheck if hello broker is installed on hello device.</span></span> <span data-ttu-id="b6ef6-248">İOS 9 Apple ne uygulama düzenleri sorgulayabilir aşağı kilitli.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-248">In iOS 9 Apple locked down what schemes an application can query for.</span></span> <span data-ttu-id="b6ef6-249">Tooadd "msauth" toohello LSApplicationQueriesSchemes bölümünü gerekir, `info.plist file`.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-249">You will need tooadd “msauth” toohello LSApplicationQueriesSchemes section of your `info.plist file`.</span></span>

<span data-ttu-id="b6ef6-250"><key>LSApplicationQueriesSchemes</key></span><span class="sxs-lookup"><span data-stu-id="b6ef6-250"><key>LSApplicationQueriesSchemes</key></span></span>

<span data-ttu-id="b6ef6-251"><array><string>msauth</string>
</array></span><span class="sxs-lookup"><span data-stu-id="b6ef6-251"><array> <string>msauth</string>
</array></span></span>

### <a name="youve-configured-sso"></a><span data-ttu-id="b6ef6-252">SSO yapılandırdıktan!</span><span class="sxs-lookup"><span data-stu-id="b6ef6-252">You've configured SSO!</span></span>
<span data-ttu-id="b6ef6-253">Şimdi hello Microsoft Identity SDK otomatik olarak hem kimlik bilgileri, uygulamalar arasında paylaşmak ve cihazlarının varsa hello Aracısı çağırma.</span><span class="sxs-lookup"><span data-stu-id="b6ef6-253">Now hello Microsoft Identity SDK will automatically both share credentials across your applications and invoke hello broker if it's present on their device.</span></span>

