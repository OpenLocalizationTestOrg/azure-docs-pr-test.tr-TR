---
title: "Azure Active Directory Raporlama: Başlarken | Microsoft Belgeleri"
description: "Azure Active Directory raporlamada kullanılabilen çeşitli raporları listeler hello"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 7ac99919-8df5-4424-9298-fc7c025ba949
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: f47875708398391dd7f3efdc56a741fdba273b76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-reporting"></a><span data-ttu-id="efe25-103">Azure Active Directory Raporlama ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="efe25-103">Getting started with Azure Active Directory Reporting</span></span>
## <a name="what-it-is"></a><span data-ttu-id="efe25-104">Nedir?</span><span class="sxs-lookup"><span data-stu-id="efe25-104">What it is</span></span>
<span data-ttu-id="efe25-105">Azure Active Directory (Azure AD), dizininize yönelik güvenlik, etkinlik ve denetim raporlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="efe25-105">Azure Active Directory (Azure AD) includes security, activity, and audit reports for your directory.</span></span> <span data-ttu-id="efe25-106">Dahil hello raporları listesi aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="efe25-106">Here's a list of hello reports included:</span></span>

### <a name="security-reports"></a><span data-ttu-id="efe25-107">Güvenlik raporları</span><span class="sxs-lookup"><span data-stu-id="efe25-107">Security reports</span></span>
* <span data-ttu-id="efe25-108">Bilinmeyen kaynaklardan gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="efe25-108">Sign-ins from unknown sources</span></span>
* <span data-ttu-id="efe25-109">Birden çok hatadan sonra gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="efe25-109">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="efe25-110">Birden çok coğrafyadan gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="efe25-110">Sign-ins from multiple geographies</span></span>
* <span data-ttu-id="efe25-111">Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="efe25-111">Sign-ins from IP addresses with suspicious activity</span></span>
* <span data-ttu-id="efe25-112">Düzensiz oturum açma etkinliği</span><span class="sxs-lookup"><span data-stu-id="efe25-112">Irregular sign-in activity</span></span>
* <span data-ttu-id="efe25-113">Muhtemelen virüs bulaşmış cihazlardan gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="efe25-113">Sign-ins from possibly infected devices</span></span>
* <span data-ttu-id="efe25-114">Anormal oturum açma etkinliği gösteren kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="efe25-114">Users with anomalous sign-in activity</span></span>

### <a name="activity-reports"></a><span data-ttu-id="efe25-115">Etkinlik raporları</span><span class="sxs-lookup"><span data-stu-id="efe25-115">Activity reports</span></span>
* <span data-ttu-id="efe25-116">Uygulama kullanımı: özet</span><span class="sxs-lookup"><span data-stu-id="efe25-116">Application usage: summary</span></span>
* <span data-ttu-id="efe25-117">Uygulama kullanımı: ayrıntılı</span><span class="sxs-lookup"><span data-stu-id="efe25-117">Application usage: detailed</span></span>
* <span data-ttu-id="efe25-118">Uygulama panosu</span><span class="sxs-lookup"><span data-stu-id="efe25-118">Application dashboard</span></span>
* <span data-ttu-id="efe25-119">Hesap hazırlama hataları</span><span class="sxs-lookup"><span data-stu-id="efe25-119">Account provisioning errors</span></span>
* <span data-ttu-id="efe25-120">Bireysel kullanıcı cihazları</span><span class="sxs-lookup"><span data-stu-id="efe25-120">Individual user devices</span></span>
* <span data-ttu-id="efe25-121">Bireysel kullanıcı Etkinliği</span><span class="sxs-lookup"><span data-stu-id="efe25-121">Individual user Activity</span></span>
* <span data-ttu-id="efe25-122">Grup etkinlik raporu</span><span class="sxs-lookup"><span data-stu-id="efe25-122">Groups activity report</span></span>
* <span data-ttu-id="efe25-123">Parola Sıfırlama Kayıt Etkinlik Raporu</span><span class="sxs-lookup"><span data-stu-id="efe25-123">Password Reset Registration Activity Report</span></span>
* <span data-ttu-id="efe25-124">Parola sıfırlama etkinliği</span><span class="sxs-lookup"><span data-stu-id="efe25-124">Password reset activity</span></span>

### <a name="audit-reports"></a><span data-ttu-id="efe25-125">Denetim raporları</span><span class="sxs-lookup"><span data-stu-id="efe25-125">Audit reports</span></span>
* <span data-ttu-id="efe25-126">Dizin denetimi raporu</span><span class="sxs-lookup"><span data-stu-id="efe25-126">Directory audit report</span></span>

> [!TIP]
> <span data-ttu-id="efe25-127">Azure AD Raporlama ile ilgili daha fazla belge için [Erişim ve kullanım raporlarınızı görüntüleme](active-directory-view-access-usage-reports.md) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="efe25-127">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="how-it-works"></a><span data-ttu-id="efe25-128">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="efe25-128">How it works</span></span>
### <a name="reporting-pipeline"></a><span data-ttu-id="efe25-129">Raporlama işlem hattı</span><span class="sxs-lookup"><span data-stu-id="efe25-129">Reporting pipeline</span></span>
<span data-ttu-id="efe25-130">Merhaba raporlama işlem hattı üç ana adımdan oluşur.</span><span class="sxs-lookup"><span data-stu-id="efe25-130">hello reporting pipeline consists of three main steps.</span></span> <span data-ttu-id="efe25-131">Bir kullanıcı oturum açtığında veya bir kimlik doğrulaması yapılan her zaman, hello aşağıdakiler gerçekleşir:</span><span class="sxs-lookup"><span data-stu-id="efe25-131">Every time a user signs in, or an authentication is made, hello following happens:</span></span>

* <span data-ttu-id="efe25-132">İlk olarak, (başarıyla veya başarısız) hello kullanıcı kimlik doğrulaması ve hello sonuç hello Azure Active Directory Hizmeti veritabanlarında depolanır.</span><span class="sxs-lookup"><span data-stu-id="efe25-132">First, hello user is authenticated (successfully or unsuccessfully), and hello result is stored in hello Azure Active Directory service databases.</span></span>
* <span data-ttu-id="efe25-133">Düzenli aralıklarla, en yeni oturum açma işlemlerinin tümü işlenir.</span><span class="sxs-lookup"><span data-stu-id="efe25-133">At regular intervals, all recent sign ins are processed.</span></span> <span data-ttu-id="efe25-134">Bu noktada, güvenlik ve anormal etkinlik algoritmalarımız en yeni oturum açma işlemlerinin tümünde şüpheli etkinlik araması gerçekleştirmektedir.</span><span class="sxs-lookup"><span data-stu-id="efe25-134">At this point, our security and anomalous activity algorithms are searching all recent sign ins for suspicious activity.</span></span>
* <span data-ttu-id="efe25-135">İşlemeden sonra hello raporları yazılmış, önbelleğe alınan ve hello Klasik Azure portalına hizmet.</span><span class="sxs-lookup"><span data-stu-id="efe25-135">After processing, hello reports are written, cached, and served in hello Azure classic portal.</span></span>

### <a name="report-generation-times"></a><span data-ttu-id="efe25-136">Rapor oluşturma süreleri</span><span class="sxs-lookup"><span data-stu-id="efe25-136">Report generation times</span></span>
<span data-ttu-id="efe25-137">Toohello büyük hacimli kimlik doğrulamaları ve bileşenler Azure AD platformu hello tarafından işlenen oturum, hello en son işlenen oturum açma işlemlerini, ortalama olarak bir saat öncesine aittir.</span><span class="sxs-lookup"><span data-stu-id="efe25-137">Due toohello large volume of authentications and sign ins processed by hello Azure AD platform, hello most recent sign-ins processed are, on average, one hour old.</span></span> <span data-ttu-id="efe25-138">Nadir durumlarda too8 saatleri tooprocess hello en son oturum açma işlemleri sürebilir.</span><span class="sxs-lookup"><span data-stu-id="efe25-138">In rare cases, it may take up too8 hours tooprocess hello most recent sign-ins.</span></span>

<span data-ttu-id="efe25-139">Merhaba en son işlenen oturum açma, her rapor hello üstündeki hello Yardım metnini inceleyerek bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="efe25-139">You can find hello most recent processed sign-in by examining hello help text at hello top of each report.</span></span>

![Her rapor hello üst kısmındaki Yardım metnini](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> <span data-ttu-id="efe25-141">Azure AD Raporlama ile ilgili daha fazla belge için [Erişim ve kullanım raporlarınızı görüntüleme](active-directory-view-access-usage-reports.md) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="efe25-141">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="getting-started"></a><span data-ttu-id="efe25-142">Başlarken</span><span class="sxs-lookup"><span data-stu-id="efe25-142">Getting started</span></span>
### <a name="sign-into-hello-azure-classic-portal"></a><span data-ttu-id="efe25-143">Merhaba Klasik Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="efe25-143">Sign into hello Azure classic portal</span></span>
<span data-ttu-id="efe25-144">Önce hello toosign gerekir. [Klasik Azure portalı](https://manage.windowsazure.com) genel veya uyumluluk Yöneticisi olarak.</span><span class="sxs-lookup"><span data-stu-id="efe25-144">First, you'll need toosign into hello [Azure classic portal](https://manage.windowsazure.com)  as a global or compliance administrator.</span></span> <span data-ttu-id="efe25-145">Ayrıca, bir Azure aboneliği Hizmet Yöneticisi veya ortak yöneticisi olmanız gerekir veya hello "erişim tooAzure AD" kullanarak Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="efe25-145">You must also be an Azure subscription service administrator or co-administrator, or be using hello "Access tooAzure AD" Azure subscription.</span></span>

### <a name="navigate-tooreports"></a><span data-ttu-id="efe25-146">TooReports gidin</span><span class="sxs-lookup"><span data-stu-id="efe25-146">Navigate tooReports</span></span>
<span data-ttu-id="efe25-147">tooview raporları toohello hello dizininizin üst kısmındaki Raporlar sekmesine gidin.</span><span class="sxs-lookup"><span data-stu-id="efe25-147">tooview Reports, navigate toohello Reports tab at hello top of your directory.</span></span>

<span data-ttu-id="efe25-148">Merhaba raporları görüntüleme, ilk kez kullanıyorsanız hello raporlarını görüntüleyebilmek için tooagree tooa iletişim kutusu gerekir.</span><span class="sxs-lookup"><span data-stu-id="efe25-148">If this is your first time viewing hello reports, you'll need tooagree tooa dialog box before you can view hello reports.</span></span> <span data-ttu-id="efe25-149">Bu tooensure kuruluş tooview admins için kabul edilebilir olduğundan emin olup bu veriler, bazı ülkelerde özel bilgi olarak kabul.</span><span class="sxs-lookup"><span data-stu-id="efe25-149">This is tooensure that it's acceptable for admins in your organization tooview this data, which may be considered private information in some countries.</span></span>

![İletişim kutusu](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a><span data-ttu-id="efe25-151">Raporların her birini araştırma</span><span class="sxs-lookup"><span data-stu-id="efe25-151">Explore each report</span></span>
<span data-ttu-id="efe25-152">Toplanmakta olan her rapor toosee hello veri gidin ve hello oturum açma işlemleri işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="efe25-152">Navigate into each report toosee hello data being collected and hello sign-ins processed.</span></span> <span data-ttu-id="efe25-153">Bulabileceğiniz bir [burada tüm hello raporların listesini](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="efe25-153">You can find a [list of all hello reports here](active-directory-reporting-guide.md).</span></span>

![Tüm raporlar](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-hello-reports-as-csv"></a><span data-ttu-id="efe25-155">Merhaba raporları CSV olarak indirme</span><span class="sxs-lookup"><span data-stu-id="efe25-155">Download hello reports as CSV</span></span>
<span data-ttu-id="efe25-156">Raporların her biri CSV (virgülle ayrılmış değer) dosyası olarak indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="efe25-156">Each report can be downloaded as a CSV (comma-separated value) file.</span></span> <span data-ttu-id="efe25-157">Bu dosyaları Excel, Powerbı veya üçüncü taraf analiz programları toofurther analiz verilerinizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="efe25-157">You can use these files in Excel, PowerBI or third-party analysis programs toofurther analyze your data.</span></span>

<span data-ttu-id="efe25-158">herhangi bir CSV olarak rapor toodownload toohello rapora gidin ve "Merhaba altındaki Yükle"'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="efe25-158">toodownload any report as a CSV, navigate toohello report and click "Download" at hello bottom.</span></span>

![İndir düğmesi](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> <span data-ttu-id="efe25-160">Azure AD Raporlama ile ilgili daha fazla belge için [Erişim ve kullanım raporlarınızı görüntüleme](active-directory-view-access-usage-reports.md) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="efe25-160">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="efe25-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="efe25-161">Next steps</span></span>
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a><span data-ttu-id="efe25-162">Anormal oturum açma etkinliği için uyarıları özelleştirme</span><span class="sxs-lookup"><span data-stu-id="efe25-162">Customize alerts for anomalous sign in activity</span></span>
<span data-ttu-id="efe25-163">Dizininizin toohello "Yapılandırma" sekmesine gidin.</span><span class="sxs-lookup"><span data-stu-id="efe25-163">Navigate toohello "Configure" tab of your directory.</span></span>

<span data-ttu-id="efe25-164">Toohello "Bildirimler" bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="efe25-164">Scroll toohello "Notifications" section.</span></span>

<span data-ttu-id="efe25-165">Etkinleştirmek veya devre dışı hello "Anormal oturum açma işlemlerine e-posta bildirimleri" bölümü.</span><span class="sxs-lookup"><span data-stu-id="efe25-165">Enable or disable hello "Email Notifications of Anomalous sign-ins" section.</span></span>

![Merhaba bildirimler bölümü](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-hello-azure-ad-reporting-api"></a><span data-ttu-id="efe25-167">Azure AD raporlama API'si ile Merhaba tümleştirme</span><span class="sxs-lookup"><span data-stu-id="efe25-167">Integrate with hello Azure AD Reporting API</span></span>
<span data-ttu-id="efe25-168">Bkz: [hello raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="efe25-168">See [Getting started with hello Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

### <a name="engage-multi-factor-authentication-on-users"></a><span data-ttu-id="efe25-169">Multi-Factor Authentication'ı kullanıcılar üzerinde uygulama</span><span class="sxs-lookup"><span data-stu-id="efe25-169">Engage Multi-Factor Authentication on users</span></span>
<span data-ttu-id="efe25-170">Rapordaki bir kullanıcıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="efe25-170">Select a user in a report.</span></span>

<span data-ttu-id="efe25-171">Merhaba ekranın hello Hello "MFA'yı etkinleştir" düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="efe25-171">Click hello "Enable MFA" button at hello bottom of hello screen.</span></span>

![Merhaba ekranında hello sonundaki Hello çok faktörlü kimlik doğrulaması düğmesi](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> <span data-ttu-id="efe25-173">Azure AD Raporlama ile ilgili daha fazla belge için [Erişim ve kullanım raporlarınızı görüntüleme](active-directory-view-access-usage-reports.md) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="efe25-173">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="learn-more"></a><span data-ttu-id="efe25-174">Daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="efe25-174">Learn more</span></span>
### <a name="audit-events"></a><span data-ttu-id="efe25-175">Denetim olayları</span><span class="sxs-lookup"><span data-stu-id="efe25-175">Audit events</span></span>
<span data-ttu-id="efe25-176">Hangi olayları hakkında hello dizininde denetleneceğini öğrenin [Azure Active Directory raporlama denetim olayları](active-directory-reporting-audit-events.md).</span><span class="sxs-lookup"><span data-stu-id="efe25-176">Learn about what events are audited in hello directory in [Azure Active Directory Reporting Audit Events](active-directory-reporting-audit-events.md).</span></span>

### <a name="api-integration"></a><span data-ttu-id="efe25-177">API Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="efe25-177">API Integration</span></span>
<span data-ttu-id="efe25-178">Bkz: [hello raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md) ve hello [API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt126081.aspx).</span><span class="sxs-lookup"><span data-stu-id="efe25-178">See [Getting started with hello Reporting API](active-directory-reporting-api-getting-started.md) and hello [API reference documentation](https://msdn.microsoft.com/library/azure/mt126081.aspx).</span></span>

### <a name="get-in-touch"></a><span data-ttu-id="efe25-179">İletişim</span><span class="sxs-lookup"><span data-stu-id="efe25-179">Get in touch</span></span>
<span data-ttu-id="efe25-180">Geri bildirim, yardım veya her türlü sorularınız için [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) adresine e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="efe25-180">Email [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) for feedback, help, or any questions you might have.</span></span>

> [!TIP]
> <span data-ttu-id="efe25-181">Azure AD Raporlama ile ilgili daha fazla belge için [Erişim ve kullanım raporlarınızı görüntüleme](active-directory-view-access-usage-reports.md) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="efe25-181">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

