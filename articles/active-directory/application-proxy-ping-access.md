---
title: "Üstbilgi tabanlı kimlik doğrulaması ile PingAccess Azure AD uygulama proxy'si için | Microsoft Docs"
description: "Üstbilgi tabanlı kimlik doğrulamayı destekleyecek şekilde PingAccess ve uygulama proxy'si ile uygulama yayımlama."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 58034ab8830cf655199875b448948ea14dc04a70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a><span data-ttu-id="0344d-103">Uygulama proxy'si ve PingAccess ile çoklu oturum açma için üstbilgi tabanlı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="0344d-103">Header-based authentication for single sign-on with Application Proxy and PingAccess</span></span>

<span data-ttu-id="0344d-104">Azure Active Directory Uygulama proxy'si ve PingAccess Azure Active Directory müşteriler daha fazla uygulama bile erişimle sağlamak üzere birlikte ortaklık.</span><span class="sxs-lookup"><span data-stu-id="0344d-104">Azure Active Directory Application Proxy and PingAccess have partnered together to provide Azure Active Directory customers with access to even more applications.</span></span> <span data-ttu-id="0344d-105">PingAccess genişletir [varolan uygulama proxy'si teklifleri](active-directory-application-proxy-get-started.md) üstbilgileri için kimlik doğrulaması kullanan uygulamalar için çoklu oturum açma erişimini eklenecek.</span><span class="sxs-lookup"><span data-stu-id="0344d-105">PingAccess expands the [existing Application Proxy offerings](active-directory-application-proxy-get-started.md) to include single sign-on access to applications that use headers for authentication.</span></span>

## <a name="what-is-pingaccess-for-azure-ad"></a><span data-ttu-id="0344d-106">Azure AD için PingAccess nedir?</span><span class="sxs-lookup"><span data-stu-id="0344d-106">What is PingAccess for Azure AD?</span></span>

<span data-ttu-id="0344d-107">Azure Active Directory için PingAccess, üstbilgi için kimlik doğrulaması kullanan uygulamalar için kullanıcıların erişim ve çoklu oturum açma vermenizi sağlar PingAccess bir tekliftir.</span><span class="sxs-lookup"><span data-stu-id="0344d-107">PingAccess for Azure Active Directory is an offering of PingAccess that enables you to give users access and single sign-on to applications that use headers for authentication.</span></span> <span data-ttu-id="0344d-108">Uygulama proxy'si Bu uygulamaları diğer, erişimde kimlik doğrulaması için Azure AD kullanarak ve bağlayıcı hizmeti trafiğinin geçirme gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="0344d-108">Application Proxy treats these apps like any other, using Azure AD to authenticate access and then passing traffic through the connector service.</span></span> <span data-ttu-id="0344d-109">PingAccess önünde uygulamaları bulunur ve uygulamanın kimlik doğrulaması okuyamamasını biçiminde alması Azure AD erişim belirtecinden bir üstbilgisine çevirir.</span><span class="sxs-lookup"><span data-stu-id="0344d-109">PingAccess sits in front of the apps and translates the access token from Azure AD into a header so that the application receives the authentication in the format it can read.</span></span>

<span data-ttu-id="0344d-110">Kullanıcılarınızın, şirket uygulamalarınızı kullanmak oturum zaman farklı bir şey fark olmaz.</span><span class="sxs-lookup"><span data-stu-id="0344d-110">Your users won’t notice anything different when they sign in to use your corporate apps.</span></span> <span data-ttu-id="0344d-111">Bunlar hala herhangi bir yerden herhangi bir cihazda çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0344d-111">They can still work from anywhere on any device.</span></span> 

<span data-ttu-id="0344d-112">Uygulama proxy'si bağlayıcılar doğrudan kendi kimlik doğrulama türü ne olursa olsun tüm uygulamalar için Uzak trafiğe olduğundan, Yük Dengelemesi otomatik olarak da devam edeceğiz.</span><span class="sxs-lookup"><span data-stu-id="0344d-112">Since the Application Proxy connectors direct remote traffic to all apps regardless of their authentication type, they’ll continue to load balance automatically, as well.</span></span>

## <a name="how-do-i-get-access"></a><span data-ttu-id="0344d-113">Erişim nasıl sağlarım?</span><span class="sxs-lookup"><span data-stu-id="0344d-113">How do I get access?</span></span>

<span data-ttu-id="0344d-114">Bu senaryo, Azure Active Directory PingAccess arasındaki iş ortaklığına aracılığıyla sunulur olduğundan, her iki hizmet için lisans gerekir.</span><span class="sxs-lookup"><span data-stu-id="0344d-114">Since this scenario is offered through a partnership between Azure Active Directory and PingAccess, you need licenses for both services.</span></span> <span data-ttu-id="0344d-115">Ancak, Azure Active Directory Premium aboneliği en fazla 20 uygulamalarını kapsamaktadır temel bir PingAccess lisans içerir.</span><span class="sxs-lookup"><span data-stu-id="0344d-115">However, Azure Active Directory Premium subscriptions include a basic PingAccess license that covers up to 20 applications.</span></span> <span data-ttu-id="0344d-116">20'den fazla üstbilgi tabanlı uygulamaları yayımlamak gerekiyorsa, PingAccess ek lisans satın alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0344d-116">If you need to publish more than 20 header-based applications, you can purchase an additional license from PingAccess.</span></span> 

<span data-ttu-id="0344d-117">Daha fazla bilgi için bkz. [Azure Active Directory sürümleri](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="0344d-117">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="publish-your-application-in-azure"></a><span data-ttu-id="0344d-118">Azure'da uygulamanızı yayımlama</span><span class="sxs-lookup"><span data-stu-id="0344d-118">Publish your application in Azure</span></span>

<span data-ttu-id="0344d-119">Bu makale, bir uygulamanın bu senaryo ile ilk kez yayımlama kişiler için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0344d-119">This article is intended for people who are publishing an app with this scenario for the first time.</span></span> <span data-ttu-id="0344d-120">Hem uygulama hem de PingAccess, yayımlama adımlara ek olarak çalışmaya nasıl başlayacağınız size yol göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="0344d-120">It walks through how to get started with both Application and PingAccess, in addition to the publishing steps.</span></span> <span data-ttu-id="0344d-121">Her iki hizmet zaten yapılandırdıktan ancak yayımlama adımlar Yenileyici istiyorsanız Bağlayıcısı yükleme atlayın ve üzerinde gitme [Azure AD uygulama proxy'si ile uygulamanızı eklemek](#add-your-app-to-Azure-AD-with-Application-Proxy).</span><span class="sxs-lookup"><span data-stu-id="0344d-121">If you’ve already configured both services but want a refresher on the publishing steps, you can skip the connector installation and move on to [Add your app to Azure AD with Application Proxy](#add-your-app-to-Azure-AD-with-Application-Proxy).</span></span>

>[!NOTE]
><span data-ttu-id="0344d-122">Bu senaryo Azure AD arasında ortaklık olduğundan ve PingAccess, bazı yönergeler var Ping kimlik sitesinde.</span><span class="sxs-lookup"><span data-stu-id="0344d-122">Since this scenario is a partnership between Azure AD and PingAccess, some of the instructions exist on the Ping Identity site.</span></span>

### <a name="install-an-application-proxy-connector"></a><span data-ttu-id="0344d-123">Bir uygulama ara sunucusu Bağlayıcısı'nı yüklemek</span><span class="sxs-lookup"><span data-stu-id="0344d-123">Install an Application Proxy connector</span></span>

<span data-ttu-id="0344d-124">Zaten uygulama Proxy etkin olması ve yüklü bir bağlayıcı varsa, bu bölüm atlayın ve üzerinde gitme [Azure AD uygulama proxy'si ile uygulamanızı eklemek](#add-your-app-to-azure-ad-with-application-proxy).</span><span class="sxs-lookup"><span data-stu-id="0344d-124">If you already have Application Proxy enabled, and have a connector installed, you can skip this section and move on to [Add your app to Azure AD with Application Proxy](#add-your-app-to-azure-ad-with-application-proxy).</span></span>

<span data-ttu-id="0344d-125">Uygulama Ara sunucusu Bağlayıcısı'nı uzaktan çalışanlarınızın trafiği yayımlanan uygulamalarınızı yönlendiren bir Windows Server hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="0344d-125">The Application Proxy connector is a Windows Server service that directs the traffic from your remote employees to your published apps.</span></span> <span data-ttu-id="0344d-126">Daha ayrıntılı yükleme yönergeleri için bkz: [Azure portalında uygulama ara sunucusunu etkinleştirme](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="0344d-126">For more detailed installation instructions, see [Enable Application Proxy in the Azure portal](active-directory-application-proxy-enable.md).</span></span>

1. <span data-ttu-id="0344d-127">Oturum [Azure portal](https://portal.azure.com) genel yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="0344d-127">Sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="0344d-128">Seçin **Azure Active Directory** > **uygulama proxy'si**.</span><span class="sxs-lookup"><span data-stu-id="0344d-128">Select **Azure Active Directory** > **Application proxy**.</span></span>
3. <span data-ttu-id="0344d-129">Seçin **Bağlayıcısı'nı indir** uygulama Proxy Bağlayıcısı yüklemeyi başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="0344d-129">Select **Download Connector** to start the Application Proxy connector download.</span></span> <span data-ttu-id="0344d-130">Yükleme yönergelerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="0344d-130">Follow the installation instructions.</span></span>

   ![Uygulama Ara sunucusunu etkinleştirme ve Bağlayıcısı'nı indirin](./media/application-proxy-ping-access/install-connector.png)

4. <span data-ttu-id="0344d-132">Bağlayıcı yükleme otomatik olarak etkinleştirmelisiniz uygulama proxy'si değil, seçebilirsiniz, ancak dizininiz için **uygulama ara sunucusunu etkinleştirme**.</span><span class="sxs-lookup"><span data-stu-id="0344d-132">Downloading the connector should automatically enable Application Proxy for your directory, but if not you can select **Enable Application Proxy**.</span></span>


### <a name="add-your-app-to-azure-ad-with-application-proxy"></a><span data-ttu-id="0344d-133">Azure AD uygulama proxy'si ile uygulamanızı ekleyin</span><span class="sxs-lookup"><span data-stu-id="0344d-133">Add your app to Azure AD with Application Proxy</span></span>

<span data-ttu-id="0344d-134">Azure portalında uygulamanız gereken iki eylemler vardır.</span><span class="sxs-lookup"><span data-stu-id="0344d-134">There are two actions you need to take in the Azure portal.</span></span> <span data-ttu-id="0344d-135">İlk olarak, uygulama proxy'si ile uygulamanızı yayımlamak için gerekir.</span><span class="sxs-lookup"><span data-stu-id="0344d-135">First, you need to publish your application with Application Proxy.</span></span> <span data-ttu-id="0344d-136">Ardından, PingAccess adımları sırasında kullanabilirsiniz uygulama hakkında biraz bilgi toplamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0344d-136">Then, you need to collect some information about the app that you can use during the PingAccess steps.</span></span>

<span data-ttu-id="0344d-137">Uygulamanızı yayımlamak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="0344d-137">Follow these steps to publish your app.</span></span> <span data-ttu-id="0344d-138">1-8, bkz: izlenecek adımların daha ayrıntılı için [Azure AD uygulama proxy'si ile uygulama yayımlama](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0344d-138">For a more detailed walkthrough of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

1. <span data-ttu-id="0344d-139">Son bölümde almadıysanız, oturum [Azure portal](https://portal.azure.com) genel yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="0344d-139">If you didn't in the last section, sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="0344d-140">Seçin **Azure Active Directory** > **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="0344d-140">Select **Azure Active Directory** > **Enterprise applications**.</span></span>
3. <span data-ttu-id="0344d-141">Seçin **Ekle** dikey pencerenin üstündeki.</span><span class="sxs-lookup"><span data-stu-id="0344d-141">Select **Add** at the top of the blade.</span></span>
4. <span data-ttu-id="0344d-142">Seçin **şirket içi uygulama**.</span><span class="sxs-lookup"><span data-stu-id="0344d-142">Select **On-premises application**.</span></span>
5. <span data-ttu-id="0344d-143">Yeni uygulamanızı hakkındaki bilgilerle gerekli alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="0344d-143">Fill out the required fields with information about your new app.</span></span> <span data-ttu-id="0344d-144">Ayarları için aşağıdaki yönergeleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="0344d-144">Use the following guidance for the settings:</span></span>
   - <span data-ttu-id="0344d-145">**İç URL**: normalde şirket ağında olduğunuzda, uygulamanın oturum açma sayfası götüren URL'sini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="0344d-145">**Internal URL**: Normally you provide the URL that takes you to the app’s sign in page when you’re on the corporate network.</span></span> <span data-ttu-id="0344d-146">Bu senaryo için bağlayıcı PingAccess proxy uygulama ön sayfası olarak işlemek gerekir.</span><span class="sxs-lookup"><span data-stu-id="0344d-146">For this scenario the connector needs to treat the PingAccess proxy as the front page of the app.</span></span> <span data-ttu-id="0344d-147">Şu biçimi kullanın: `https://<host name of your PA server>:<port>`.</span><span class="sxs-lookup"><span data-stu-id="0344d-147">Use this format: `https://<host name of your PA server>:<port>`.</span></span> <span data-ttu-id="0344d-148">Bağlantı noktası, varsayılan değer 3000 olmakla birlikte PingAccess yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0344d-148">The port is 3000 by default, but you can configure it in PingAccess.</span></span>
   - <span data-ttu-id="0344d-149">**Ön kimlik doğrulama yöntemi**: Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0344d-149">**Pre-authentication method**: Azure Active Directory</span></span>
   - <span data-ttu-id="0344d-150">**Üstbilgiler URL'de çevir**: Hayır</span><span class="sxs-lookup"><span data-stu-id="0344d-150">**Translate URL in Headers**: No</span></span>

   >[!NOTE]
   ><span data-ttu-id="0344d-151">Bu ilk uygulamanızı ise, bağlantı noktası 3000 başlatmak ve PingAccess yapılandırmanızı değiştirirseniz, bu ayar güncelleştirmek için geri dönün için kullanın.</span><span class="sxs-lookup"><span data-stu-id="0344d-151">If this is your first application, use port 3000 to start and come back to update this setting if you change your PingAccess configuration.</span></span> <span data-ttu-id="0344d-152">İkinci veya sonraki uygulamanız varsa bu PingAccess içinde yapılandırdığınız dinleyicisi eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0344d-152">If this is your second or later app, this will need to match the Listener you’ve configured in PingAccess.</span></span> <span data-ttu-id="0344d-153">Daha fazla bilgi edinmek [PingAccess dinleyicileri](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span><span class="sxs-lookup"><span data-stu-id="0344d-153">Learn more about [listeners in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span></span>

6. <span data-ttu-id="0344d-154">Seçin **Ekle** dikey pencerenin altındaki.</span><span class="sxs-lookup"><span data-stu-id="0344d-154">Select **Add** at the bottom of the blade.</span></span> <span data-ttu-id="0344d-155">Uygulamanızı eklenir ve Hızlı Başlat menüsü açılır.</span><span class="sxs-lookup"><span data-stu-id="0344d-155">Your application is added, and the quick start menu opens.</span></span>
7. <span data-ttu-id="0344d-156">Hızlı Başlangıç menüsünde seçin **test etmek için bir kullanıcı atamak**, ve uygulama için en az bir kullanıcı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0344d-156">In the quick start menu, select **Assign a user for testing**, and add at least one user to the application.</span></span> <span data-ttu-id="0344d-157">Bu test hesabının şirket içi uygulama erişimi olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0344d-157">Make sure this test account has access to the on-premises application.</span></span>
8. <span data-ttu-id="0344d-158">Seçin **atamak** test kullanıcı ataması kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="0344d-158">Select **Assign** to save the test user assignment.</span></span>
9. <span data-ttu-id="0344d-159">Uygulama Yönetimi dikey penceresinde, seçin **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="0344d-159">On the app management blade, select **Single sign-on**.</span></span>
10. <span data-ttu-id="0344d-160">Seçin **üstbilgi tabanlı oturum açma** açılır menüsünden.</span><span class="sxs-lookup"><span data-stu-id="0344d-160">Choose **Header-based sign-on** from the drop-down menu.</span></span> <span data-ttu-id="0344d-161">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="0344d-161">Select **Save**.</span></span>

   >[!TIP]
   ><span data-ttu-id="0344d-162">Üstbilgi tabanlı çoklu oturum açma kullanarak, ilk kez kullanıyorsanız PingAccess yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0344d-162">If this is your first time using header-based single sign-on, you need to install PingAccess.</span></span> <span data-ttu-id="0344d-163">Azure aboneliğiniz PingAccess yüklemenizle birlikte otomatik olarak ilişkili olduğundan emin olmak için PingAccess indirmek için bu tek oturum açma sayfasında bağlantıyı kullanın.</span><span class="sxs-lookup"><span data-stu-id="0344d-163">To make sure your Azure subscription is automatically associated with your PingAccess installation, use the link on this single sign-on page to download PingAccess.</span></span> <span data-ttu-id="0344d-164">Şimdi indirme sitesi açmak veya daha sonra bu sayfaya geri dönerseniz.</span><span class="sxs-lookup"><span data-stu-id="0344d-164">You can open the download site now, or come back to this page later.</span></span> 

   ![Üstbilgi tabanlı oturum açma seçin](./media/application-proxy-ping-access/sso-header.PNG)

11. <span data-ttu-id="0344d-166">Kurumsal uygulamalar dikey veya Azure Active Directory menüye dönmek için kaydırıcıyı sola kaydırma kapatın.</span><span class="sxs-lookup"><span data-stu-id="0344d-166">Close the Enterprise applications blade or scroll all the way to the left to return to the Azure Active Directory menu.</span></span>
12. <span data-ttu-id="0344d-167">Seçin **uygulama kayıtlar**.</span><span class="sxs-lookup"><span data-stu-id="0344d-167">Select **App registrations**.</span></span>

   ![Uygulama kayıtlar seçin](./media/application-proxy-ping-access/app-registrations.png)

13. <span data-ttu-id="0344d-169">Yeni eklediğiniz, ardından uygulamayı seçin **yanıt URL'leri**.</span><span class="sxs-lookup"><span data-stu-id="0344d-169">Select the app you just added, then **Reply URLs**.</span></span>

   ![Yanıt URL'leri seçin](./media/application-proxy-ping-access/reply-urls.png)

14. <span data-ttu-id="0344d-171">Dış yanıt URL'leri listesindeki uygulamanızı 5. adımda atadığınız URL olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="0344d-171">Check to see if the external URL that you assigned to your app in step 5 is in the Reply URLs list.</span></span> <span data-ttu-id="0344d-172">Değilse, şimdi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0344d-172">If it’s not, add it now.</span></span>
15. <span data-ttu-id="0344d-173">Uygulama ayarları dikey penceresinde, seçin **gerekli izinleri**.</span><span class="sxs-lookup"><span data-stu-id="0344d-173">On the app settings blade, select **Required permissions**.</span></span>

  ![Gerekli izinleri seçin](./media/application-proxy-ping-access/required-permissions.png)

16. <span data-ttu-id="0344d-175">**Add (Ekle)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="0344d-175">Select **Add**.</span></span> <span data-ttu-id="0344d-176">API için seçin **Windows Azure Active Directory**, ardından **seçin**.</span><span class="sxs-lookup"><span data-stu-id="0344d-176">For the API, choose **Windows Azure Active Directory**, then **Select**.</span></span> <span data-ttu-id="0344d-177">İzinlerini seçin **okuma ve tüm uygulamaları yazma** ve **oturum açın ve kullanıcı profilini okuma**, ardından **seçin** ve **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="0344d-177">For the permissions, choose **Read and write all applications** and **Sign in and read user profile**, then **Select** and **Done**.</span></span>  

  ![İzinleri seçin](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-the-pingaccess-steps"></a><span data-ttu-id="0344d-179">PingAccess adımlar için bilgi toplama</span><span class="sxs-lookup"><span data-stu-id="0344d-179">Collect information for the PingAccess steps</span></span>

1. <span data-ttu-id="0344d-180">Uygulama ayarları dikey üzerinde seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="0344d-180">On your app settings blade, select **Properties**.</span></span> 

  ![Özellikler'i seçin](./media/application-proxy-ping-access/properties.png)

2. <span data-ttu-id="0344d-182">Kaydet **uygulama kimliği** değeri.</span><span class="sxs-lookup"><span data-stu-id="0344d-182">Save the **Application Id** value.</span></span> <span data-ttu-id="0344d-183">PingAccess yapılandırdığınızda, bu istemci kimliği için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0344d-183">This is used for the client ID when you configure PingAccess.</span></span>
3. <span data-ttu-id="0344d-184">Uygulama ayarları dikey penceresinde, seçin **anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="0344d-184">On the app settings blade, select **Keys**.</span></span>

  ![Anahtarları seçin](./media/application-proxy-ping-access/Keys.png)

4. <span data-ttu-id="0344d-186">Bir anahtar açıklama girerek ve sona erme tarihi açılan menüden seçerek bir anahtar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0344d-186">Create a key by entering a key description and choosing an expiration date from the drop-down menu.</span></span>
5. <span data-ttu-id="0344d-187">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="0344d-187">Select **Save**.</span></span> <span data-ttu-id="0344d-188">Bir GUID görünür **değeri** alan.</span><span class="sxs-lookup"><span data-stu-id="0344d-188">A GUID appears in the **Value** field.</span></span>

  <span data-ttu-id="0344d-189">Bu değer, artık bu pencereyi kapattıktan sonra yeniden görmek açamazsınız olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0344d-189">Save this value now, as you won’t be able to see it again after you close this window.</span></span>

  ![Yeni bir anahtar oluşturun](./media/application-proxy-ping-access/create-keys.png)

6. <span data-ttu-id="0344d-191">Uygulama kayıtlar dikey veya Azure Active Directory menüye dönmek için kaydırıcıyı sola kaydırma kapatın.</span><span class="sxs-lookup"><span data-stu-id="0344d-191">Close the App registrations blade or scroll all the way to the left to return to the Azure Active Directory menu.</span></span>
7. <span data-ttu-id="0344d-192">Seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="0344d-192">Select **Properties**.</span></span>
8. <span data-ttu-id="0344d-193">Kaydet **dizin kimliği** GUID.</span><span class="sxs-lookup"><span data-stu-id="0344d-193">Save the **Directory ID** GUID.</span></span>

### <a name="optional---update-graphapi-to-send-custom-fields"></a><span data-ttu-id="0344d-194">İsteğe bağlı - güncelleştirme GraphAPI özel alanlar göndermek için</span><span class="sxs-lookup"><span data-stu-id="0344d-194">Optional - Update GraphAPI to send custom fields</span></span>

<span data-ttu-id="0344d-195">Azure AD kimlik doğrulaması için gönderir güvenlik belirteçleri listesi için bkz: [Azure AD belirteç başvurusu](./develop/active-directory-token-and-claims.md).</span><span class="sxs-lookup"><span data-stu-id="0344d-195">For a list of security tokens that Azure AD sends for authentication, see [Azure AD token reference](./develop/active-directory-token-and-claims.md).</span></span> <span data-ttu-id="0344d-196">Diğer belirteçleri gönderir bir özel talep gerekiyorsa, GraphAPI uygulaması alanı ayarlamak için kullanın *acceptMappedClaims* için **doğru**.</span><span class="sxs-lookup"><span data-stu-id="0344d-196">If you need a custom claim that sends other tokens, use GraphAPI to set the app field *acceptMappedClaims* to **True**.</span></span> <span data-ttu-id="0344d-197">Bu yapılandırma yapmak için Azure AD Graph Explorer'a veya MS Graph kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0344d-197">You can use either Azure AD Graph Explorer or MS Graph to make this configuration.</span></span> 

<span data-ttu-id="0344d-198">Bu örnek Graph Explorer'a kullanır:</span><span class="sxs-lookup"><span data-stu-id="0344d-198">This example uses Graph Explorer:</span></span>

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a><span data-ttu-id="0344d-199">PingAccess indirin ve uygulamanızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0344d-199">Download PingAccess and configure your app</span></span>

<span data-ttu-id="0344d-200">Tüm Azure Active Directory kurulum adımlarını tamamladığınıza göre size PingAccess yapılandırmaya geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0344d-200">Now that you've completed all the Azure Active Directory setup steps, you can move on to configuring PingAccess.</span></span> 

<span data-ttu-id="0344d-201">Ayrıntılı adımlar için bu senaryonun PingAccess parçası Ping kimlik belgelerinde devam [yapılandırma PingAccess Azure AD için](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span><span class="sxs-lookup"><span data-stu-id="0344d-201">The detailed steps for the PingAccess part of this scenario continue in the Ping Identity documentation, [Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span></span>

<span data-ttu-id="0344d-202">Bu adımları, zaten yoksa, PingAccess hesabı alma, PingAccess sunucusunu yükleme ve Azure portalından kopyaladığınız dizini Kimliğine sahip bir Azure AD OIDC sağlayıcı bağlantısı oluşturma işleminde size yol.</span><span class="sxs-lookup"><span data-stu-id="0344d-202">Those steps walk you through the process of getting a PingAccess account if you don't already have one, installing the PingAccess Server, and creating an Azure AD OIDC Provider connection with the Directory ID that you copied from the Azure portal.</span></span> <span data-ttu-id="0344d-203">Ardından, PingAccess üzerinde Web oturum oluşturmak için uygulama kimliği ve anahtar değerlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0344d-203">Then, you use the Application ID and Key values to create a Web Session on PingAccess.</span></span> <span data-ttu-id="0344d-204">Bundan sonra kimlik eşlemesi ayarlamanız ve bir sanal ana bilgisayar, site ve uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0344d-204">After that, you can set up identity mapping and create a virtual host, site, and application.</span></span>

### <a name="test-your-app"></a><span data-ttu-id="0344d-205">Uygulamanızı test etme</span><span class="sxs-lookup"><span data-stu-id="0344d-205">Test your app</span></span>

<span data-ttu-id="0344d-206">Tüm bu adımları tamamladıktan sonra uygulamanızı açık ve çalışıyor olması.</span><span class="sxs-lookup"><span data-stu-id="0344d-206">When you've completed all these steps, your app should be up and running.</span></span> <span data-ttu-id="0344d-207">Test etmek için bir tarayıcı açın ve uygulama Azure'da yayımlandığında oluşturduğunuz dış URL'ye gidin.</span><span class="sxs-lookup"><span data-stu-id="0344d-207">To test it, open a browser and navigate to the external URL that you created when you published the app in Azure.</span></span> <span data-ttu-id="0344d-208">Uygulamaya atanan test hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="0344d-208">Sign in with the test account that you assigned to the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0344d-209">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0344d-209">Next steps</span></span>

- [<span data-ttu-id="0344d-210">Azure AD için PingAccess yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0344d-210">Configure PingAccess for Azure AD</span></span>](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [<span data-ttu-id="0344d-211">Azure AD uygulama proxy'si nasıl çoklu oturum açma sağlar?</span><span class="sxs-lookup"><span data-stu-id="0344d-211">How does Azure AD Application Proxy provide single sign-on?</span></span>](application-proxy-sso-overview.md)
- [<span data-ttu-id="0344d-212">Uygulama proxy'si sorun giderme</span><span class="sxs-lookup"><span data-stu-id="0344d-212">Troubleshoot Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)
