---
title: "Uygulamalar arası SSO'nun ADAL kullanarak Android üzerinde etkinleştirme | Microsoft Docs"
description: "Çoklu oturum açma, uygulamalar arasında etkinleştirmek için ADAL SDK özelliklerini kullanma "
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
ms.openlocfilehash: 9c7e959530a836fe5ddf74708363a636c39b3cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-enable-cross-app-sso-on-android-using-adal"></a><span data-ttu-id="661d8-103">Uygulamalar arası SSO'nun ADAL kullanarak Android üzerinde etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="661d8-103">How to enable cross-app SSO on Android using ADAL</span></span>
<span data-ttu-id="661d8-104">Kullanıcıların yalnızca bir kez kimlik bilgilerini girin ve bu kimlik bilgilerini otomatik olarak gerekir böylece çoklu oturum açma (SSO) iş arasında sağlayan uygulamalar artık müşteriler tarafından bekleniyordu.</span><span class="sxs-lookup"><span data-stu-id="661d8-104">Providing Single Sign-On (SSO) so that users only need to enter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="661d8-105">Ekranda bir telefon araması veya ilerideki kodu gibi ek bir etmen (2FA) kez birlikte küçük, genellikle kullanıcı adı ve parola girme zorluk hızlı memnuniyetsizliği kullanıcı sonuçlarında ürününüz için birden fazla kez bunun var.</span><span class="sxs-lookup"><span data-stu-id="661d8-105">The difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has to do this more than one time for your product.</span></span>

<span data-ttu-id="661d8-106">Ayrıca, Microsoft Accounts veya Office365 iş hesabından gibi diğer uygulamaları kullanabilir bir kimlik platformu uygularsanız, müşteriler bu kimlik bilgileri, tüm uygulamalarını satıcı olsun genelinde kullanılabilir olmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="661d8-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials to be available to use across all their applications no matter the vendor.</span></span>

<span data-ttu-id="661d8-107">Bizim Microsoft Identity SDK ile birlikte Microsoft Identity platform bu sabit iş sizin için yapar ve SSO müşterilerinizle kendi uygulama paketinin içinde ya da delight olanağı sağlar veya bizim Aracısı özellik ve tüm aygıt arasında kimlik doğrulayıcı uygulamalar ile.</span><span class="sxs-lookup"><span data-stu-id="661d8-107">The Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you the ability to delight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across the entire device.</span></span>

<span data-ttu-id="661d8-108">Bu kılavuz, müşterilerinize Bu kolaylık sağlamak için uygulamanızda bizim SDK'yı yapılandırmak nasıl söyler.</span><span class="sxs-lookup"><span data-stu-id="661d8-108">This walkthrough will tell you how to configure our SDK within your application to provide this benefit to your customers.</span></span>

<span data-ttu-id="661d8-109">Bu kılavuz için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="661d8-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="661d8-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="661d8-110">Azure Active Directory</span></span>
* <span data-ttu-id="661d8-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="661d8-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="661d8-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="661d8-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="661d8-113">Azure Active Directory Koşullu Erişim</span><span class="sxs-lookup"><span data-stu-id="661d8-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="661d8-114">Önceki belge bildiğiniz varsayar nasıl [sağlamak eski portalı uygulamalarında Azure Active Directory için](active-directory-how-to-integrate.md) ve uygulamanız ile tümleşik [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span><span class="sxs-lookup"><span data-stu-id="661d8-114">The document preceding assumes you know how to [provision applications in the legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with the [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span></span>

## <a name="sso-concepts-in-the-microsoft-identity-platform"></a><span data-ttu-id="661d8-115">Microsoft Identity platformuna SSO kavramlar</span><span class="sxs-lookup"><span data-stu-id="661d8-115">SSO Concepts in the Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="661d8-116">Microsoft Identity aracıları</span><span class="sxs-lookup"><span data-stu-id="661d8-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="661d8-117">Microsoft kimlik farklı satıcılardan uygulamalar arasında köprü oluşturma için izin uygulamaları mobil her platform için sağlar ve kimlik doğrulamaya nerede tek güvenli bir yerde gerektiren özel Gelişmiş özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="661d8-117">Microsoft provides applications for every mobile platform that allow for the bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where to validate credentials.</span></span> <span data-ttu-id="661d8-118">Bunlar diyoruz **aracıların**.</span><span class="sxs-lookup"><span data-stu-id="661d8-118">We call these **brokers**.</span></span> <span data-ttu-id="661d8-119">İOS ve Android bunlar müşteriler bağımsız olarak yüklemek veya bazı veya tüm cihaz için kendi çalışan yöneten bir şirket tarafından cihaza gönderilir indirilebilir uygulamaları aracılığıyla sağlanır.</span><span class="sxs-lookup"><span data-stu-id="661d8-119">On iOS and Android these are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages some or all of the device for their employee.</span></span> <span data-ttu-id="661d8-120">Bu aracıları yönetme güvenlik yalnızca bazı uygulamalar veya ne BT yöneticileri işlemleriniz bağlı tüm cihaz desteği.</span><span class="sxs-lookup"><span data-stu-id="661d8-120">These brokers support managing security just for some applications or the entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="661d8-121">Windows, bu işlev, Web kimlik doğrulama aracısı olarak teknik olarak bilinen işletim sistemi içinde yerleşik bir hesabı seçicide tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="661d8-121">In Windows, this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>

<span data-ttu-id="661d8-122">Hakkında daha fazla bilgi için bu aracıların ve nasıl müşterilerinizin bunları okuyun Microsoft Identity platform için kullanıcıların oturum açma akışını görebileceğiniz kullanırız.</span><span class="sxs-lookup"><span data-stu-id="661d8-122">For more information on how we use these brokers and how your customers might see them in their login flow for the Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="661d8-123">Mobil cihazlarda günlüğe kaydetme için desenleri</span><span class="sxs-lookup"><span data-stu-id="661d8-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="661d8-124">Kimlik cihazlarda erişime Microsoft Identity platformuna yönelik iki temel düzenlerden izleyin:</span><span class="sxs-lookup"><span data-stu-id="661d8-124">Access to credentials on devices follow two basic patterns for the Microsoft Identity platform:</span></span>

* <span data-ttu-id="661d8-125">Olmayan Aracısı Yardımlı oturum açmalar</span><span class="sxs-lookup"><span data-stu-id="661d8-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="661d8-126">Yardımlı Oturum Aracısı</span><span class="sxs-lookup"><span data-stu-id="661d8-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="661d8-127">Olmayan Aracısı Yardımlı oturum açmalar</span><span class="sxs-lookup"><span data-stu-id="661d8-127">Non-broker assisted logins</span></span>
<span data-ttu-id="661d8-128">Olmayan Aracısı Yardımlı satır içi uygulamayla gerçekleşir ve bu uygulama için cihazda yerel depolama kullanan oturum açma deneyimlerini oturumlardır.</span><span class="sxs-lookup"><span data-stu-id="661d8-128">Non-broker assisted logins are login experiences that happen inline with the application and use the local storage on the device for that application.</span></span> <span data-ttu-id="661d8-129">Bu depolama uygulamalar arasında paylaşılıyor olabilir, ancak kimlik bilgileri uygulama veya bu kimlik bilgilerini kullanarak uygulama paketi sıkı bir şekilde bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="661d8-129">This storage may be shared across applications but the credentials are tightly bound to the app or suite of apps using that credential.</span></span> <span data-ttu-id="661d8-130">Bir kullanıcı adı ve parola uygulama içinde girdiğinizde, bu büyük olasılıkla birçok mobil uygulamalarda tecrübe ettiklerinize.</span><span class="sxs-lookup"><span data-stu-id="661d8-130">You've most likely experienced this in many mobile applications when you enter a username and password within the application itself.</span></span>

<span data-ttu-id="661d8-131">Bu oturumlar aşağıdaki avantajlara sahiptir:</span><span class="sxs-lookup"><span data-stu-id="661d8-131">These logins have the following benefits:</span></span>

* <span data-ttu-id="661d8-132">Kullanıcı deneyimi tamamen uygulaması içinde zaten var.</span><span class="sxs-lookup"><span data-stu-id="661d8-132">User experience exists entirely within the application.</span></span>
* <span data-ttu-id="661d8-133">Kimlik bilgileri, çoklu oturum açma deneyimini paketiniz uygulamaları için sağlama aynı sertifika tarafından imzalanan uygulamalar arasında paylaşılabilir.</span><span class="sxs-lookup"><span data-stu-id="661d8-133">Credentials can be shared across applications that are signed by the same certificate, providing a single sign-on experience to your suite of applications.</span></span>
* <span data-ttu-id="661d8-134">Oturum açma deneyimi geçici denetim önce ve sonra oturum açma uygulamaya sağlanır.</span><span class="sxs-lookup"><span data-stu-id="661d8-134">Control around the experience of logging in is provided to the application before and after sign-in.</span></span>

<span data-ttu-id="661d8-135">Bu oturumlar aşağıdaki dezavantajları vardır:</span><span class="sxs-lookup"><span data-stu-id="661d8-135">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="661d8-136">Kullanıcı yalnızca bu Microsoft uygulamanızı yapılandırılmış Identities arasında Microsoft Identity kullanan tüm uygulamalar boyunca çoklu oturum açma deneyimi olamaz.</span><span class="sxs-lookup"><span data-stu-id="661d8-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="661d8-137">Uygulamanızı koşullu erişim gibi daha gelişmiş iş özellikleriyle kullanılamaz veya ürün Intune paketi kullanın.</span><span class="sxs-lookup"><span data-stu-id="661d8-137">Your application cannot be used with more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="661d8-138">Uygulamanızı iş kullanıcıları için sertifika tabanlı kimlik doğrulamasını destekleyemez.</span><span class="sxs-lookup"><span data-stu-id="661d8-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="661d8-139">Microsoft Identity SDK'ları uygulamalarınızı SSO'yu etkinleştirmek için paylaşılan depolama ile nasıl bir temsilini şöyledir:</span><span class="sxs-lookup"><span data-stu-id="661d8-139">Here is a representation of how the Microsoft Identity SDKs work with the shared storage of your applications to enable SSO:</span></span>

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

#### <a name="broker-assisted-logins"></a><span data-ttu-id="661d8-140">Yardımlı Oturum Aracısı</span><span class="sxs-lookup"><span data-stu-id="661d8-140">Broker assisted logins</span></span>
<span data-ttu-id="661d8-141">Aracısı destekli Aracısı uygulama içinde oluşur ve kimlik bilgilerini Microsoft Identity platform uygulanan tüm uygulamalar için cihazda paylaşmak için depolama ve aracının güvenlik kullanan oturum açma deneyimlerini oturumlardır.</span><span class="sxs-lookup"><span data-stu-id="661d8-141">Broker-assisted logins are login experiences that occur within the broker application and use the storage and security of the broker to share credentials across all applications on the device that apply the Microsoft Identity platform.</span></span> <span data-ttu-id="661d8-142">Bu, uygulamalarınız kullanıcılar Oturum Aracısı kullandığını anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="661d8-142">This means that your applications rely on the broker to sign users in.</span></span> <span data-ttu-id="661d8-143">İOS ve Android cihazlarda bu aracıların müşteriler bağımsız olarak yüklemeniz veya kendi kullanıcı aygıt yöneten bir şirket tarafından cihaza gönderilir indirilebilir uygulamaları aracılığıyla sağlanır.</span><span class="sxs-lookup"><span data-stu-id="661d8-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages the device for their user.</span></span> <span data-ttu-id="661d8-144">İos'ta Microsoft Authenticator uygulama bu tür bir uygulama örneğidir.</span><span class="sxs-lookup"><span data-stu-id="661d8-144">An example of this type of application is the Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="661d8-145">Windows bu işlevsellik, Web kimlik doğrulama aracısı olarak teknik olarak bilinen işletim sistemi içinde yerleşik bir hesabı seçicide tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="661d8-145">In Windows this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>
<span data-ttu-id="661d8-146">Deneyimi platforma göre değişir ve bazen kullanıcılara işlemleri karışıklığa neden olabilir değilse doğru şekilde yönetilir.</span><span class="sxs-lookup"><span data-stu-id="661d8-146">The experience varies by platform and can sometimes be disruptive to users if not managed correctly.</span></span> <span data-ttu-id="661d8-147">Facebook uygulamanın yüklü olması ve başka bir uygulamadan Facebook bağlanmak kullanırsanız bu deseni ile en biliyor.</span><span class="sxs-lookup"><span data-stu-id="661d8-147">You're probably most familiar with this pattern if you have the Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="661d8-148">Microsoft Identity platformu aynı düzeni kullanır.</span><span class="sxs-lookup"><span data-stu-id="661d8-148">The Microsoft Identity platform uses the same pattern.</span></span>

<span data-ttu-id="661d8-149">Bu bir "geçiş" Müşteri adayları iOS için kullanıcının oturum açmak istediğiniz hangi hesabı seçmek ön Burada, uygulamanızın Microsoft Authenticator uygulamaları arka gönderilir animasyon gelir.</span><span class="sxs-lookup"><span data-stu-id="661d8-149">For iOS this leads to a "transition" animation where your application is sent to the background while the Microsoft Authenticator applications comes to the foreground for the user to select which account they would like to sign in with.</span></span>  

<span data-ttu-id="661d8-150">Android ve Windows hesabı seçicide kullanıcıya daha az kesintiye uğratan olan, uygulamanızın üzerinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="661d8-150">For Android and Windows the account chooser is displayed on top of your application which is less disruptive to the user.</span></span>

#### <a name="how-the-broker-gets-invoked"></a><span data-ttu-id="661d8-151">Aracısı'nı nasıl çağrılır</span><span class="sxs-lookup"><span data-stu-id="661d8-151">How the broker gets invoked</span></span>
<span data-ttu-id="661d8-152">Microsoft Authenticator uygulaması gibi cihaz uyumlu bir aracı yüklenmişse Microsoft Identity SDK'ları otomatik olarak bir kullanıcı Microsoft Identity platformdan herhangi bir hesabı kullanarak oturum açması istedikleri belirttiğinde, Aracısı çağırma çalışma yapın.</span><span class="sxs-lookup"><span data-stu-id="661d8-152">If a compatible broker is installed on the device, like the Microsoft Authenticator application, the Microsoft Identity SDKs will automatically do the work of invoking the broker for you when a user indicates they wish to log in using any account from the Microsoft Identity platform.</span></span> <span data-ttu-id="661d8-153">Bu hesap, kişisel Microsoft Account, bir iş veya Okul hesabı veya bir sağladığınız hesap ve konak B2C ve B2B Ürünlerimiz kullanarak azure'da olabilir.</span><span class="sxs-lookup"><span data-stu-id="661d8-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 
 
 #### <a name="how-we-ensure-the-application-is-valid"></a><span data-ttu-id="661d8-154">Biz uygulamayı nasıl emin geçerlidir</span><span class="sxs-lookup"><span data-stu-id="661d8-154">How we ensure the application is valid</span></span>
 
 <span data-ttu-id="661d8-155">Aracısı Aracısı sağladığımız güvenlik önemli bir uygulama çağrısı kimliğinden emin olmak için gereken oturumları destekli.</span><span class="sxs-lookup"><span data-stu-id="661d8-155">The need to ensure the identity of an application call the broker is crucial to the security we provide in broker assisted logins.</span></span> <span data-ttu-id="661d8-156">İOS ne Android kötü amaçlı uygulamalar "yasal uygulamanın tanımlayıcı aldatıcı" ve yasal uygulamanın amacı belirteçleri almak için yalnızca belirli bir uygulama için geçerli olan benzersiz tanımlayıcıları zorlar.</span><span class="sxs-lookup"><span data-stu-id="661d8-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive the tokens meant for the legitimate application.</span></span> <span data-ttu-id="661d8-157">Biz her zaman doğru uygulama çalışma zamanında ile iletişim kuran emin olmak için size özel redirectURI kendi uygulama Microsoft ile kaydedilirken sağlamak için geliştirici isteyin.</span><span class="sxs-lookup"><span data-stu-id="661d8-157">To ensure we are always communicating with the right application at runtime, we ask the developer to provide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="661d8-158">**Geliştiricilerin bu yeniden yönlendirme URI'si nasıl oluşturabilir aşağıda ayrıntılı olarak ele alınmıştır.**</span><span class="sxs-lookup"><span data-stu-id="661d8-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="661d8-159">Bu özel redirectURI ve Google Play mağazası tarafından uygulama için benzersiz olmasını sağlamış uygulamanın sertifika parmak izi içerir.</span><span class="sxs-lookup"><span data-stu-id="661d8-159">This custom redirectURI contains the certificate thumbprint of the application and is ensured to be unique to the application by the Google Play Store.</span></span> <span data-ttu-id="661d8-160">Bir uygulama Aracısı çağırdığında Aracısı Aracısı adlı sertifika parmak iziyle sağlamak için Android işletim sistemi sorar.</span><span class="sxs-lookup"><span data-stu-id="661d8-160">When an application calls the broker, the broker asks the Android operating system to provide it with the certificate thumbprint that called the broker.</span></span> <span data-ttu-id="661d8-161">Aracısı'nı bu sertifika parmak izi kimliğini sistemimizde çağrısında Microsoft'a sağlar.</span><span class="sxs-lookup"><span data-stu-id="661d8-161">The broker provides this certificate thumbprint to Microsoft in the call to our identity system.</span></span> <span data-ttu-id="661d8-162">Sertifika parmak izi uygulamanın bize kayıt sırasında geliştirici tarafından sağlanan sertifika parmak izi eşleşmiyorsa, biz uygulama istenirken kaynak belirteçleri için erişimi reddeder.</span><span class="sxs-lookup"><span data-stu-id="661d8-162">If the certificate thumbprint of the application does not match the certificate thumbprint provided to us by the developer during registration, we will deny access to the tokens for the resource the application is requesting.</span></span> <span data-ttu-id="661d8-163">Bu denetim yalnızca geliştirici tarafından kayıtlı uygulama belirteçlerini almasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="661d8-163">This check ensures that only the application registered by the developer receives tokens.</span></span>

<span data-ttu-id="661d8-164">**Microsoft Identity SDK Aracısı çağıran veya aracı olmayan Yardımlı akış kullanıyorsa, geliştirici seçimi vardır.**</span><span class="sxs-lookup"><span data-stu-id="661d8-164">**The developer has the choice of if the Microsoft Identity SDK calls the broker or uses the non-broker assisted flow.**</span></span> <span data-ttu-id="661d8-165">Bununla birlikte Geliştirici Aracısı destekli akışı kullanmayacak şekilde seçerse kullanıcı cihazda eklemiş olabilir ve kendi uygulama Microsoft, müşterilerinin koşullu erişim, Intune yönetim özellikleri ve sertifika tabanlı kimlik doğrulaması gibi sağlar iş özellikleriyle kullanılmasını engeller SSO kimlik bilgilerini kullanma avantajına kaybedersiniz.</span><span class="sxs-lookup"><span data-stu-id="661d8-165">However if the developer chooses not to use the broker-assisted flow they lose the benefit of using SSO credentials that the user may have already added on the device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="661d8-166">Bu oturumlar aşağıdaki avantajlara sahiptir:</span><span class="sxs-lookup"><span data-stu-id="661d8-166">These logins have the following benefits:</span></span>

* <span data-ttu-id="661d8-167">Kullanıcı, satıcı olsun tüm kullanıcıların uygulamaları üzerinden SSO karşılaşır.</span><span class="sxs-lookup"><span data-stu-id="661d8-167">User experiences SSO across all their applications no matter the vendor.</span></span>
* <span data-ttu-id="661d8-168">Uygulamanız, koşullu erişim gibi daha gelişmiş iş özellikleri kullanın veya ürün Intune paketi kullanın.</span><span class="sxs-lookup"><span data-stu-id="661d8-168">Your application can use more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="661d8-169">Uygulamanızı iş kullanıcıları için sertifika tabanlı kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="661d8-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="661d8-170">Uygulama ve kullanıcı kimliği olarak çok daha güvenli oturum açma deneyimi ek güvenlik algoritmalarını ve şifreleme ile Aracısı uygulama tarafından doğrulandı.</span><span class="sxs-lookup"><span data-stu-id="661d8-170">Much more secure sign-in experience as the identity of the application and the user are verified by the broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="661d8-171">Bu oturumlar aşağıdaki dezavantajları vardır:</span><span class="sxs-lookup"><span data-stu-id="661d8-171">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="661d8-172">Kimlik bilgileri seçilen sırada kullanıcının iOS uygulamanızın deneyimi dışında geçti.</span><span class="sxs-lookup"><span data-stu-id="661d8-172">In iOS the user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="661d8-173">Uygulamanızda müşterileriniz için oturum açma deneyimi yönetme olanağı kaybı.</span><span class="sxs-lookup"><span data-stu-id="661d8-173">Loss of the ability to manage the login experience for your customers within your application.</span></span>

<span data-ttu-id="661d8-174">Microsoft Identity SDK'ları SSO'yu etkinleştirmek için Aracısı uygulamalarla nasıl çalıştığını bir temsilini şöyledir:</span><span class="sxs-lookup"><span data-stu-id="661d8-174">Here is a representation of how the Microsoft Identity SDKs work with the broker applications to enable SSO:</span></span>

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

<span data-ttu-id="661d8-175">Daha iyi anlamanıza ve SSO Microsoft Identity platform ve SDK'ları kullanarak uygulamanızdaki uygulamanıza açabilmelisiniz bu arka plan bilgileri ile çağrılmak.</span><span class="sxs-lookup"><span data-stu-id="661d8-175">Armed with this background information you should be able to better understand and implement SSO within your application using the Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="661d8-176">ADAL kullanarak uygulamalar arası SSO'nun etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="661d8-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="661d8-177">Burada ADAL Android SDK'sı için kullanın:</span><span class="sxs-lookup"><span data-stu-id="661d8-177">Here we use the ADAL Android SDK to:</span></span>

* <span data-ttu-id="661d8-178">Aracı olmayan Yardımlı SSO Uygulama paketiniz için Aç</span><span class="sxs-lookup"><span data-stu-id="661d8-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="661d8-179">Aracısı destekli SSO desteği Aç</span><span class="sxs-lookup"><span data-stu-id="661d8-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="661d8-180">Aracı olmayan için SSO üzerinde kapatma SSO Destekli</span><span class="sxs-lookup"><span data-stu-id="661d8-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="661d8-181">Uygulamalar arasında aracı olmayan Yardımlı SSO için Microsoft Identity SDK'ları SSO karmaşıklığını çoğunu sizin için yönetin.</span><span class="sxs-lookup"><span data-stu-id="661d8-181">For non-broker assisted SSO across applications the Microsoft Identity SDKs manage much of the complexity of SSO for you.</span></span> <span data-ttu-id="661d8-182">Bu doğru kullanıcı önbellekte bulma ve bakımı, sorgu oturum açan kullanıcıların listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="661d8-182">This includes finding the right user in the cache and maintaining a list of logged in users for you to query.</span></span>

<span data-ttu-id="661d8-183">Aşağıdakileri yapmak gereken kendi uygulamalarında SSO'yu etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="661d8-183">To enable SSO across applications you own you need to do the following:</span></span>

1. <span data-ttu-id="661d8-184">Tüm uygulamalar kullanıcı aynı istemci Kimliğini veya uygulama kimliği emin olun</span><span class="sxs-lookup"><span data-stu-id="661d8-184">Ensure all your applications user the same Client ID or Application ID.</span></span>
2. <span data-ttu-id="661d8-185">Tüm uygulamalarınızın aynı SharedUserID kümesine sahip olun.</span><span class="sxs-lookup"><span data-stu-id="661d8-185">Ensure all your applications have the same SharedUserID set.</span></span>
3. <span data-ttu-id="661d8-186">Depolama paylaştırabilirsiniz tüm uygulamalar aynı imzalama sertifikası Google Play Mağazası'ndan paylaşmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="661d8-186">Ensure that all of your applications share the same signing certificate from the Google Play store so that you can share storage.</span></span>

#### <a name="step-1-using-the-same-client-id--application-id-for-all-the-applications-in-your-suite-of-apps"></a><span data-ttu-id="661d8-187">1. adım: aynı istemci Kimliğini kullanarak / uygulama kimliği paketiniz uygulamalarının tüm uygulamalar için</span><span class="sxs-lookup"><span data-stu-id="661d8-187">Step 1: Using the same Client ID / Application ID for all the applications in your suite of apps</span></span>
<span data-ttu-id="661d8-188">Belirteçleri, uygulamalar arasında paylaşmak için izin bilmeniz Microsoft Identity Platform sırayla uygulamalarınızın her birinde aynı istemci Kimliğini veya uygulama kimliği paylaşmak gerekir</span><span class="sxs-lookup"><span data-stu-id="661d8-188">In order for the Microsoft Identity platform to know that it's allowed to share tokens across your applications, each of your applications will need to share the same Client ID or Application ID.</span></span> <span data-ttu-id="661d8-189">Bu portalda ilk uygulamanızı kaydolurken, size sağlanan benzersiz bir tanımlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="661d8-189">This is the unique identifier that was provided to you when you registered your first application in the portal.</span></span>

<span data-ttu-id="661d8-190">Aynı uygulama kimliği kullanıyorsa, farklı uygulamalar Microsoft Identity hizmetine nasıl kullanacağını merak ediyor olabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="661d8-190">You may be wondering how you will identify different apps to the Microsoft Identity service if it uses the same Application ID.</span></span> <span data-ttu-id="661d8-191">Yanıt olan **yeniden yönlendirme URI'ler**.</span><span class="sxs-lookup"><span data-stu-id="661d8-191">The answer is with the **Redirect URIs**.</span></span> <span data-ttu-id="661d8-192">Her uygulamanın birden çok yeniden yönlendirme hazırlama Portalı'nda kayıtlı URI'ler olabilir.</span><span class="sxs-lookup"><span data-stu-id="661d8-192">Each application can have multiple Redirect URIs registered in the onboarding portal.</span></span> <span data-ttu-id="661d8-193">Her uygulama paketiniz içinde farklı bir yeniden yönlendirme URI'sine sahip olur.</span><span class="sxs-lookup"><span data-stu-id="661d8-193">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="661d8-194">Bu sistem, bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="661d8-194">An example of how this looks is below:</span></span>

<span data-ttu-id="661d8-195">App1 yeniden yönlendirme URİ'si:`msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span><span class="sxs-lookup"><span data-stu-id="661d8-195">App1 Redirect URI: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span></span>

<span data-ttu-id="661d8-196">App2 yeniden yönlendirme URİ'si:`msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span><span class="sxs-lookup"><span data-stu-id="661d8-196">App2 Redirect URI: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span></span>

<span data-ttu-id="661d8-197">App3 yeniden yönlendirme URİ'si:`msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span><span class="sxs-lookup"><span data-stu-id="661d8-197">App3 Redirect URI: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span></span>

<span data-ttu-id="661d8-198">....</span><span class="sxs-lookup"><span data-stu-id="661d8-198">....</span></span>

<span data-ttu-id="661d8-199">Bu durum, aynı istemci kimliği altında iç içe geçmiş / uygulama kimliği ve yeniden yönlendirme URI'si dönmek için bize SDK yapılandırmanızda dayanan Aranan.</span><span class="sxs-lookup"><span data-stu-id="661d8-199">These are nested under the same client ID / application ID and looked up based on the redirect URI you return to us in your SDK configuration.</span></span>

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


<span data-ttu-id="661d8-200">*Bu yeniden yönlendirme URI biçimi açıklanmıştır aşağıda olduğunu unutmayın. Aracısı desteklemek istediğiniz sürece, bu durumda yukarıdaki şöyle benzemelidir herhangi yeniden yönlendirme URI'si kullanabilir*</span><span class="sxs-lookup"><span data-stu-id="661d8-200">*Note that the format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish to support the broker, in which case they must look something like the above*</span></span>

#### <a name="step-2-configuring-shared-storage-in-android"></a><span data-ttu-id="661d8-201">2. adım: Android paylaşılan depolama ortamı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="661d8-201">Step 2: Configuring shared storage in Android</span></span>
<span data-ttu-id="661d8-202">Ayarı `SharedUserID` bu belgenin kapsamı dışındadır, ancak üzerinde Google Android belgeleri okuyarak öğrenilebilecek [bildirim](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span><span class="sxs-lookup"><span data-stu-id="661d8-202">Setting the `SharedUserID` is beyond the scope of this document but can be learned by reading the Google Android documentation on the [Manifest](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span></span> <span data-ttu-id="661d8-203">Önemli olan, sharedUserID çağrılacağı ve tüm uygulamalar için kullanmak istediğinize karar ' dir.</span><span class="sxs-lookup"><span data-stu-id="661d8-203">What is important is that you decide what you want your sharedUserID will be called and use that across all your applications.</span></span>

<span data-ttu-id="661d8-204">Bulduktan sonra `SharedUserID` tüm uygulamalarınızda SSO kullanmaya hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="661d8-204">Once you have the `SharedUserID` in all your applications you are ready to use SSO.</span></span>

> [!WARNING]
> <span data-ttu-id="661d8-205">Uygulamalar arasında depolama paylaştığınızda herhangi bir uygulama bu bölge kullanıcılar silin veya tüm belirteçleri, uygulamanızda da kötüsü silin.</span><span class="sxs-lookup"><span data-stu-id="661d8-205">When you share storage across your applications any application can delete users, or worse delete all the tokens across your application.</span></span> <span data-ttu-id="661d8-206">Bu iş arka plan için belirteçleri kullanan uygulamalar varsa, özellikle felaket niteliğinde değildir.</span><span class="sxs-lookup"><span data-stu-id="661d8-206">This is particularly disastrous if you have applications that rely on the tokens to do background work.</span></span> <span data-ttu-id="661d8-207">Depolama paylaşımı Microsoft Identity SDK'ları aracılığıyla tüm kaldırma işlemleri çok dikkatli olmalıdır anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="661d8-207">Sharing storage means that you must be very careful in any and all remove operations through the Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="661d8-208">İşte bu kadar!</span><span class="sxs-lookup"><span data-stu-id="661d8-208">That's it!</span></span> <span data-ttu-id="661d8-209">Microsoft Identity SDK'sı, artık tüm uygulamalar için kimlik bilgileri paylaşacaktır.</span><span class="sxs-lookup"><span data-stu-id="661d8-209">The Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="661d8-210">Kullanıcı listesini, ayrıca uygulama örnekleri arasında paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="661d8-210">The user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="661d8-211">SSO destekli aracısı için SSO üzerinde kapatma</span><span class="sxs-lookup"><span data-stu-id="661d8-211">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="661d8-212">Bir uygulama cihazda yüklü herhangi bir aracı kullanmak için özelliği **varsayılan olarak devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="661d8-212">The ability for an application to use any broker that is installed on the device is **turned off by default**.</span></span> <span data-ttu-id="661d8-213">Uygulamanızı Aracısı ile kullanmak için bazı ek yapılandırma adımları ve uygulamanız için bazı kod eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="661d8-213">In order to use your application with the broker you must do some additional configuration and add some code to your application.</span></span>

<span data-ttu-id="661d8-214">İzlemeniz gereken adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="661d8-214">The steps to follow are:</span></span>

1. <span data-ttu-id="661d8-215">MS SDK, uygulama kodun çağrıda Aracısı modunu etkinleştir</span><span class="sxs-lookup"><span data-stu-id="661d8-215">Enable broker mode in your application code's call to the MS SDK</span></span>
2. <span data-ttu-id="661d8-216">Yeni bir yeniden yönlendirme URI'sine kurmak ve hem uygulama hem de uygulama kaydınızı sağlayın</span><span class="sxs-lookup"><span data-stu-id="661d8-216">Establish a new redirect URI and provide that to both the app and your app registration</span></span>
3. <span data-ttu-id="661d8-217">Android bildirimindeki doğru izinleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="661d8-217">Setting up the correct permissions in the Android manifest</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="661d8-218">1. adım: uygulamanızı Aracısı modunda etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="661d8-218">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="661d8-219">"Ayarlar" ya da kimlik doğrulama örneğinizi ilk kurulumu oluşturduğunuzda özelliği Aracısı'nı kullanmak, uygulamanız için etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="661d8-219">The ability for your application to use the broker is turned on when you create the "settings" or initial setup of your Authentication instance.</span></span> <span data-ttu-id="661d8-220">Kodunuzda ApplicationSettings türünüz ayarlayarak bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="661d8-220">You do this by setting your ApplicationSettings type in your code:</span></span>

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="661d8-221">2. adım: yeni yeniden yönlendirme URI'si URL şeması ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="661d8-221">Step 2: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="661d8-222">Her zaman doğru uygulamaya kimlik bilgisi belirteçleri biz dönmek emin olmak için size geri Android işletim sistemi doğrulayabilirsiniz şekilde uygulamanıza diyoruz emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="661d8-222">In order to ensure that we always return the credential tokens to the correct application, we need to make sure we call back to your application in a way that the Android operating system can verify.</span></span> <span data-ttu-id="661d8-223">Android işletim sistemi Google Play Mağazası'nda sertifika karmasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="661d8-223">The Android operating system uses the hash of the certificate in the Google Play store.</span></span> <span data-ttu-id="661d8-224">Standart dışı bir uygulama tarafından sahte olamaz.</span><span class="sxs-lookup"><span data-stu-id="661d8-224">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="661d8-225">Bu nedenle, biz bu belirteçleri doğru uygulama döndürüldüğünden emin olmak için Aracısı uygulamamız URI'sini birlikte yararlanın.</span><span class="sxs-lookup"><span data-stu-id="661d8-225">Therefore, we leverage this along with the URI of our broker application to ensure that the tokens are returned to the correct application.</span></span> <span data-ttu-id="661d8-226">Bizim Geliştirici Portalı'nda bir yeniden yönlendirme URI'si olarak ayarlayın ve bu benzersiz yeniden yönlendirme URI'si hem uygulamanızda kurmak isteriz.</span><span class="sxs-lookup"><span data-stu-id="661d8-226">We require you to establish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="661d8-227">Yeniden yönlendirme URI'si uygun biçiminde olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="661d8-227">Your redirect URI must be in the proper form of:</span></span>

`msauth://packagename/Base64UrlencodedSignature`

<span data-ttu-id="661d8-228">örn: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span><span class="sxs-lookup"><span data-stu-id="661d8-228">ex: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span></span>

<span data-ttu-id="661d8-229">Bu yeniden yönlendirme URI'sini kullanarak, uygulama kaydı belirtilmesi gerekiyor [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="661d8-229">This Redirect URI needs to be specified in your app registration using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="661d8-230">Azure AD uygulama kaydı hakkında daha fazla bilgi için bkz: [Azure Active Directory ile tümleştirme](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="661d8-230">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

#### <a name="step-3-set-up-the-correct-permissions-in-your-application"></a><span data-ttu-id="661d8-231">3. adım: uygulamanızın doğru izinleri ayarlayın</span><span class="sxs-lookup"><span data-stu-id="661d8-231">Step 3: Set up the correct permissions in your application</span></span>
<span data-ttu-id="661d8-232">Aracısı uygulamamız Android uygulamalar arasında kimlik bilgilerini yönetmek için Android işletim sistemi Hesap Yöneticisi özelliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="661d8-232">Our broker application in Android uses the Accounts Manager feature of the Android OS to manage credentials across applications.</span></span> <span data-ttu-id="661d8-233">Android Aracısı'nı kullanmak için uygulama bildiriminizi AccountManager hesaplarını kullanmak için izinleri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="661d8-233">In order to use the broker in Android your app manifest must have permissions to use AccountManager accounts.</span></span> <span data-ttu-id="661d8-234">Bu ayrıntılı olarak ele alınmıştır [Google hesabı Manager belgeleri burada](http://developer.android.com/reference/android/accounts/AccountManager.html)</span><span class="sxs-lookup"><span data-stu-id="661d8-234">This is discussed in detail in the [Google documentation for Account Manager here](http://developer.android.com/reference/android/accounts/AccountManager.html)</span></span>

<span data-ttu-id="661d8-235">Özellikle, bu izinler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="661d8-235">In particular, these permissions are:</span></span>

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a><span data-ttu-id="661d8-236">SSO yapılandırdıktan!</span><span class="sxs-lookup"><span data-stu-id="661d8-236">You've configured SSO!</span></span>
<span data-ttu-id="661d8-237">Şimdi Microsoft Identity SDK otomatik olarak hem kimlik bilgileri, uygulamalar arasında paylaşmak ve cihazlarında varsa, aracı çağırma.</span><span class="sxs-lookup"><span data-stu-id="661d8-237">Now the Microsoft Identity SDK will automatically both share credentials across your applications and invoke the broker if it's present on their device.</span></span>

