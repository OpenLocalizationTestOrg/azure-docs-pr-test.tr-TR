---
title: "Bulut için aaaContinuous teslim hizmetleri Visual Studio Online ile | Microsoft Docs"
description: "Bilgi nasıl tooset Azure için sürekli teslimini bulut uygulamaları depolama anahtar toohello hizmet yapılandırma dosyalarını tanılama kaydetmeden"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 148b2959-c5db-4e4a-a7e9-fccb252e7e8a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: dc87d049e46daf8b8a26ee4450ebd9b7910f287b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-tooazure-using-visual-studio-online"></a><span data-ttu-id="3c3be-103">Securely bulut Hizmetleri tanılama depolama anahtarı Kaydet ve Visual Studio Online kullanarak kurulum sürekli tümleştirme ve dağıtım tooAzure</span><span class="sxs-lookup"><span data-stu-id="3c3be-103">Securely Save Cloud Services Diagnostics Storage Key and Setup Continuous Integration and Deployment tooAzure using Visual Studio Online</span></span>
 <span data-ttu-id="3c3be-104">Ortak bir yöntem tooopen kaynak projeleri günümüzde olur.</span><span class="sxs-lookup"><span data-stu-id="3c3be-104">It is a common practice tooopen source projects nowadays.</span></span> <span data-ttu-id="3c3be-105">Güvenlik açıklarını Ortak kaynak denetimlerinden sızmasını gizli kullanıma sunulan gibi uygulama parolaları yapılandırma dosyaları kaydetme artık güvenli uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="3c3be-105">Saving application secrets in configuration files is no longer safe practice as security vulnerabilities are exposed from secrets being leaked from public source controls.</span></span> <span data-ttu-id="3c3be-106">Paylaşılan kaynaklar hello bulut ortamında yapı sunucuları olabileceği gerçeğidir ya da düz metin sürekli tümleştirme ardışık düzen dosyasında güvenli olmadığından gizli depolama.</span><span class="sxs-lookup"><span data-stu-id="3c3be-106">Storing secret as plaintext in a file in a Continuous Integration pipeline is not secure either since build servers could be shared resources on hello Cloud environment.</span></span> <span data-ttu-id="3c3be-107">Bu makalede nasıl Visual Studio ve Visual Studio Online azaltır hello güvenlik sorunlarının geliştirme ve sürekli tümleştirme işlemi sırasında açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3c3be-107">This article explains how Visual Studio and Visual Studio Online mitigates hello security concerns during development and Continuous Integration process.</span></span>

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a><span data-ttu-id="3c3be-108">Proje yapılandırma dosyasında tanılama depolama anahtarını gizli kaldırın</span><span class="sxs-lookup"><span data-stu-id="3c3be-108">Remove Diagnostics Storage Key Secret in Project Configuration File</span></span>
<span data-ttu-id="3c3be-109">Bulut Hizmetleri tanılama uzantısını Tanılama sonuçları kaydetmek için Azure depolama alanı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3c3be-109">Cloud Services diagnostics extension requires Azure storage for saving diagnostics results.</span></span> <span data-ttu-id="3c3be-110">Önceden hello depolama bağlantı dizesi hello bulut Hizmetleri Yapılandırma (.cscfg) dosyalarında belirtilir ve toosource denetimine iade edilemedi.</span><span class="sxs-lookup"><span data-stu-id="3c3be-110">Formerly hello storage connection string is specified in hello Cloud Services configuration (.cscfg) files and could be checked in toosource control.</span></span> <span data-ttu-id="3c3be-111">Merhaba son Azure SDK sürümündeki kısmi bir bağlantı dizesi bir belirteç tarafından değiştirilen hello anahtarla hello davranışı tooonly deposu değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="3c3be-111">In hello latest Azure SDK release we changed hello behavior tooonly store a partial connection string with hello key replaced by a token.</span></span> <span data-ttu-id="3c3be-112">Aşağıdaki adımları hello hello yeni bulut Hizmetleri Araçları nasıl çalıştığını açıklar:</span><span class="sxs-lookup"><span data-stu-id="3c3be-112">hello following steps describe how hello new Cloud Services tooling works:</span></span>

### <a name="1-open-hello-role-designer"></a><span data-ttu-id="3c3be-113">1. Merhaba rol Tasarımcısı'nı açın</span><span class="sxs-lookup"><span data-stu-id="3c3be-113">1. Open hello Role designer</span></span>
* <span data-ttu-id="3c3be-114">Çift tıklatın veya bir bulut Hizmetleri rolü tooopen rol designer'ı sağ tıklatın</span><span class="sxs-lookup"><span data-stu-id="3c3be-114">Double click or right click on a Cloud Services role tooopen Role designer</span></span>

![Rolü Aç Tasarımcısı][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a><span data-ttu-id="3c3be-116">2. Tanılama bölümü altında yeni bir onay kutusu "çıkartmayın depolama anahtarı projeden gizli" eklenir</span><span class="sxs-lookup"><span data-stu-id="3c3be-116">2. Under diagnostics section, a new check box “Don’t remove storage key secret from project” is added</span></span>
* <span data-ttu-id="3c3be-117">Merhaba yerel depolama öykünücüsü kullanıyorsanız, UseDevelopmentStorage olan hello yerel bağlantı dizesi için gizli hiçbir toomanage olduğundan bu onay kutusunu devre dışı = true.</span><span class="sxs-lookup"><span data-stu-id="3c3be-117">If you are using hello local storage emulator, this checkbox is disabled because there is no secret toomanage for hello local connection string, which is UseDevelopmentStorage=true.</span></span>

![Yerel depolama öykünücüsü bağlantı dizesi gizli değil][1]

* <span data-ttu-id="3c3be-119">Yeni bir proje oluşturuyorsanız, varsayılan olarak bu onay kutusu işaretli değildir.</span><span class="sxs-lookup"><span data-stu-id="3c3be-119">If you are creating a new project, by default this checkbox is unchecked.</span></span> <span data-ttu-id="3c3be-120">Bu, seçili hello depolama bağlantı dizesi bir belirteç ile değiştirilen hello depolama anahtar bölüm sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="3c3be-120">This results in hello storage key section of hello selected storage connection string being replaced with a token.</span></span> <span data-ttu-id="3c3be-121">Merhaba hello belirteç değerini hello geçerli kullanıcının AppData gezici klasörü altında örneğin bulunacaktır: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span><span class="sxs-lookup"><span data-stu-id="3c3be-121">hello value of hello token will be found under hello current user’s AppData Roaming folder, for example: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span></span>

> <span data-ttu-id="3c3be-122">Bu hello user\AppData klasör erişim kontrol kullanıcı oturum açma tarafından ve güvenli bir yerde toostore geliştirme gizli olarak kabul edilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3c3be-122">Note that hello user\AppData folder is Access Controlled by user sign-in and is considered a secure place toostore development secrets.</span></span>
> 
> 

![Depolama anahtarı kullanıcı profili klasörü altında kaydedilir][2]

### <a name="3-select-a-diagnostics-storage-account"></a><span data-ttu-id="3c3be-124">3. Bir tanılama depolama hesabı seçin</span><span class="sxs-lookup"><span data-stu-id="3c3be-124">3. Select a diagnostics storage account</span></span>
* <span data-ttu-id="3c3be-125">"..." Merhaba tıklayarak başlatılan hello iletişim kutusundan bir depolama hesabı seçin</span><span class="sxs-lookup"><span data-stu-id="3c3be-125">Select a storage account from hello dialog launched by clicking hello “…”</span></span> <span data-ttu-id="3c3be-126">tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3c3be-126">button.</span></span> <span data-ttu-id="3c3be-127">Oluşturulan hello depolama bağlantı dizesi nasıl hello depolama hesabı anahtarı sahip olmaz dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="3c3be-127">Notice how hello storage connection string generated will not have hello storage account key.</span></span>
* <span data-ttu-id="3c3be-128">Örneğin: DefaultEndpointsProtocol = https; AccountName = contosostorage; AccountKey = $(*clouddiagstrg.key*)</span><span class="sxs-lookup"><span data-stu-id="3c3be-128">For example: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span></span>

### <a name="4----debugging-hello-project"></a><span data-ttu-id="3c3be-129">4.    Merhaba projeyi hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="3c3be-129">4.    Debugging hello project</span></span>
* <span data-ttu-id="3c3be-130">Visual Studio'da hata ayıklamayı F5 toostart.</span><span class="sxs-lookup"><span data-stu-id="3c3be-130">F5 toostart debugging in Visual Studio.</span></span> <span data-ttu-id="3c3be-131">Her şeyi hello aynı çalışmalıdır eskisi yolu.</span><span class="sxs-lookup"><span data-stu-id="3c3be-131">Everything should work in hello same way as before.</span></span>
  <span data-ttu-id="3c3be-132">![Yerel olarak hata ayıklama başlatılamıyor][3]</span><span class="sxs-lookup"><span data-stu-id="3c3be-132">![Start debugging locally][3]</span></span>

### <a name="5-publish-project-from-visual-studio"></a><span data-ttu-id="3c3be-133">5. Visual Studio'da projeyi yayımlama</span><span class="sxs-lookup"><span data-stu-id="3c3be-133">5. Publish project from Visual Studio</span></span>
* <span data-ttu-id="3c3be-134">Başlatma hello yayımlama iletişim kutusu ve oturum açma yönergeleri toopublish hello applicaion tooAzure ile devam edin.</span><span class="sxs-lookup"><span data-stu-id="3c3be-134">Launch hello publish dialog and proceed with sign-in instructions toopublish hello applicaion tooAzure.</span></span>

### <a name="6-additional-information"></a><span data-ttu-id="3c3be-135">6. Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="3c3be-135">6. Additional information</span></span>
> <span data-ttu-id="3c3be-136">Not: hello Ayarları panelini hello rol Tasarımcısı'nda şu an için olduğu gibi kalır.</span><span class="sxs-lookup"><span data-stu-id="3c3be-136">Note: hello Settings panel in hello role designer will stay as it is for now.</span></span> <span data-ttu-id="3c3be-137">Tanılama için toouse hello gizli yönetimi özelliği istiyorsanız toohello yapılandırmaları sekmesine gidin.</span><span class="sxs-lookup"><span data-stu-id="3c3be-137">If you want toouse hello secret management feature for diagnostics, go toohello Configurations tab.</span></span>
> 
> 

![Ayarları Ekle][4]

> <span data-ttu-id="3c3be-139">Not: etkinleştirilirse, hello Application Insights anahtar düz metin olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="3c3be-139">Note: If enabled, hello Application Insights key will be stored as plain text.</span></span> <span data-ttu-id="3c3be-140">hiçbir hassas verilerin güvenliğinin bozulması riskini risk altında olacak hello anahtar yalnızca karşıya yükleme içeriği için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3c3be-140">hello key is only used for upload contents so no sensitive data will be at risk being compromised.</span></span>
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a><span data-ttu-id="3c3be-141">Derleme ve bir bulut Hizmetleri'ni Visual Studio online görev şablonları kullanarak projeyi yayımlama</span><span class="sxs-lookup"><span data-stu-id="3c3be-141">Build and Publish a Cloud Services Project using Visual Studio online Task Templates</span></span>
* <span data-ttu-id="3c3be-142">Aşağıdaki adımları hello gösterilmektedir toosetup bulut Hizmetleri için sürekli tümleştirme nasıl proje Visual Studio online görevler kullanma:</span><span class="sxs-lookup"><span data-stu-id="3c3be-142">hello following steps illustrates how toosetup Continuous Integration for Cloud Services project using Visual Studio online tasks:</span></span>
  ### <a name="1----obtain-a-vso-account"></a><span data-ttu-id="3c3be-143">1.    VSO hesabı elde etme</span><span class="sxs-lookup"><span data-stu-id="3c3be-143">1.    Obtain a VSO account</span></span>
* <span data-ttu-id="3c3be-144">[Visual Studio Online hesabı oluşturma] [ Create Visual Studio Online account] zaten yoksa,</span><span class="sxs-lookup"><span data-stu-id="3c3be-144">[Create Visual Studio Online account][Create Visual Studio Online account] if you don’t have one already</span></span>
* <span data-ttu-id="3c3be-145">[Takım projesi oluşturma] [ Create team project] Visual Studio online hesabınızda</span><span class="sxs-lookup"><span data-stu-id="3c3be-145">[Create team project][Create team project] in your Visual Studio online account</span></span>

### <a name="2----setup-source-control-in-visual-studio"></a><span data-ttu-id="3c3be-146">2.    Visual Studio'da kurulum kaynak denetimi</span><span class="sxs-lookup"><span data-stu-id="3c3be-146">2.    Setup source control in Visual Studio</span></span>
* <span data-ttu-id="3c3be-147">Tooa takım projesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="3c3be-147">Connect tooa team project</span></span>

![Tooteam projesine bağlanın][5]

![Takım projesi tooconnect seçin][6]

* <span data-ttu-id="3c3be-150">Proje toosource denetim ekleme</span><span class="sxs-lookup"><span data-stu-id="3c3be-150">Add your project toosource control</span></span>

![Proje toosource denetim ekleme][7]

![Harita proje tooa kaynak denetimi klasörü][8]

* <span data-ttu-id="3c3be-153">Takım Gezgini'nden projenizdeki denetleyin</span><span class="sxs-lookup"><span data-stu-id="3c3be-153">Check in your project from Team Explorer</span></span>

![Proje toosource denetiminde denetleyin][9]

### <a name="3----configure-build-process"></a><span data-ttu-id="3c3be-155">3.    Derleme işlemi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3c3be-155">3.    Configure Build process</span></span>
* <span data-ttu-id="3c3be-156">Tooyour takım projesine göz atın ve yeni bir derleme işlem şablonları Ekle</span><span class="sxs-lookup"><span data-stu-id="3c3be-156">Browse tooyour team project and add a new build process Templates</span></span>

![Yeni bir derleme ekleyin][10]

* <span data-ttu-id="3c3be-158">Select derleme görevi</span><span class="sxs-lookup"><span data-stu-id="3c3be-158">Select build task</span></span>

![Yapı görev ekleme][11]

![Visual Studio derleme görevi şablonu seçin][12]

* <span data-ttu-id="3c3be-161">Yapı görev girişi düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="3c3be-161">Edit build task input.</span></span> <span data-ttu-id="3c3be-162">Lütfen tooyour göre parametreleri hello yapı özelleştirme</span><span class="sxs-lookup"><span data-stu-id="3c3be-162">Please customize hello build parameters according tooyour need</span></span>

![Derleme görevi yapılandırın][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* <span data-ttu-id="3c3be-164">Yapı değişkenleri yapılandırın</span><span class="sxs-lookup"><span data-stu-id="3c3be-164">Configure build variables</span></span>

![Yapı değişkenleri yapılandırın][14]

* <span data-ttu-id="3c3be-166">Bir görev tooupload derleme bırakma ekleme</span><span class="sxs-lookup"><span data-stu-id="3c3be-166">Add a task tooupload build drop</span></span>

![Seçin derleme bırakma görevi yayımlama][15]

![Yapılandırma derleme bırakma görevi yayımlama][16]

* <span data-ttu-id="3c3be-169">Merhaba yapı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="3c3be-169">Run hello build</span></span>

![Yeni yapıyı sıraya al][17]

![Yapı özetini görüntüle][18]

* <span data-ttu-id="3c3be-172">Merhaba yapı başarılı ise sonucu benzer toobelow görürsünüz</span><span class="sxs-lookup"><span data-stu-id="3c3be-172">if hello build is successful you will see a result similar toobelow</span></span>

![Sonuç derleme][19]

### <a name="4----configure-release-process"></a><span data-ttu-id="3c3be-174">4.    Yayın işlem yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3c3be-174">4.    Configure Release process</span></span>
* <span data-ttu-id="3c3be-175">Yeni bir sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="3c3be-175">Create a new release</span></span>

![Yeni sürüm oluşturma][20]

* <span data-ttu-id="3c3be-177">Hello Azure Cloud Services Dağıtımı görev seçin</span><span class="sxs-lookup"><span data-stu-id="3c3be-177">Select hello Azure Cloud Services Deployment task</span></span>

![Azure Cloud Services Dağıtımı görev seçin][21]

* <span data-ttu-id="3c3be-179">Merhaba depolama hesabı anahtarı toosource denetiminde denetlenmedi olarak toospecify hello gizli anahtarı tanılama uzantıları ayarlamak için ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="3c3be-179">As hello storage account key is not checked in toosource control, we need toospecify hello secret key for setting diagnostics extensions.</span></span> <span data-ttu-id="3c3be-180">Merhaba genişletin **yeni hizmet oluşturmak için Gelişmiş Seçenekleri** bölümünde ve hello Düzenle **tanılama depolama hesabı anahtarlarını** parametresi giriş.</span><span class="sxs-lookup"><span data-stu-id="3c3be-180">Expand hello **Advanced Options for Creating New Service** section and edit hello **Diagnostics Storage Account Keys** parameter input.</span></span> <span data-ttu-id="3c3be-181">Anahtar değer çifti hello biçiminde birden fazla satır, bu girdi alır **[RoleName]:$(StorageAccountKey)**</span><span class="sxs-lookup"><span data-stu-id="3c3be-181">This input takes in multiple lines of key value pair in hello format of **[RoleName]:$(StorageAccountKey)**</span></span>

> <span data-ttu-id="3c3be-182">Not: Merhaba bulut Hizmetleri uygulaması burada yayımlayacak olarak aynı abonelik altında depolama hesabıdır, tanılama Merhaba, hello dağıtım görev girişinde tooenter hello anahtar gerekmez; Merhaba dağıtım aboneliğinizden program aracılığıyla hello depolama bilgi edinir</span><span class="sxs-lookup"><span data-stu-id="3c3be-182">Note: if your diagnostics storage account is under hello same subscription as where you will publish hello Cloud Services application, you don't have tooenter hello key in hello deployment task input; hello deployment will programmatically obtain hello storage information from your subscription</span></span>
> 
> 

![Bulut Hizmetleri dağıtım görev yapılandırın][22]

* <span data-ttu-id="3c3be-184">Kullanım gizli depolama anahtarları değişkenleri toosave oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3c3be-184">Use secret build variables toosave storage Keys.</span></span> <span data-ttu-id="3c3be-185">bir değişken gizli olarak tıklatın hello kilit simgesini hello hello sağ tarafındaki toomask değişkenleri giriş</span><span class="sxs-lookup"><span data-stu-id="3c3be-185">toomask a variable as secret click on hello lock icon on hello right side of hello Variables input</span></span>

![Gizli derleme değişkenleri depolama anahtarları Kaydet][23]

* <span data-ttu-id="3c3be-187">Sürüm oluşturma ve proje tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="3c3be-187">Create a release and deploy your project tooAzure</span></span>

![Yeni sürüm oluşturma][24]

## <a name="next-steps"></a><span data-ttu-id="3c3be-189">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3c3be-189">Next steps</span></span>
<span data-ttu-id="3c3be-190">Azure bulut Hizmetleri için tanılama uzantıları ayarlama hakkında daha fazla toolearn lütfen bkz. [PowerShell kullanarak Azure Cloud Services tanılamayı etkinleştirme][Enable diagnostics in Azure Cloud Services using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="3c3be-190">toolearn more about setting diagnostics extensions for Azure Cloud Services, please see [Enable diagnostics in Azure Cloud Services using PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span></span>

[Create Visual Studio Online account]:https://www.visualstudio.com/team-services/
[Create team project]: https://www.visualstudio.com/it-it/docs/setup-admin/team-services/connect-to-visual-studio-team-services
[Enable diagnostics in Azure Cloud Services using PowerShell]:https://azure.microsoft.com/en-us/documentation/articles/cloud-services-diagnostics-powershell/

[0]: ./media/cloud-services-vs-ci/vs-01.png
[1]: ./media/cloud-services-vs-ci/vs-02.png
[2]: ./media/cloud-services-vs-ci/file-01.png
[3]: ./media/cloud-services-vs-ci/vs-03.png
[4]: ./media/cloud-services-vs-ci/vs-04.png
[5]: ./media/cloud-services-vs-ci/vs-05.png
[6]: ./media/cloud-services-vs-ci/vs-06.png
[7]: ./media/cloud-services-vs-ci/vs-07.png
[8]: ./media/cloud-services-vs-ci/vs-08.png
[9]: ./media/cloud-services-vs-ci/vs-09.png
[10]: ./media/cloud-services-vs-ci/vso-01.png
[11]: ./media/cloud-services-vs-ci/vso-02.png
[12]: ./media/cloud-services-vs-ci/vso-03.png
[13]: ./media/cloud-services-vs-ci/vso-04.png
[14]: ./media/cloud-services-vs-ci/vso-05.png
[15]: ./media/cloud-services-vs-ci/vso-06.png
[16]: ./media/cloud-services-vs-ci/vso-07.png
[17]: ./media/cloud-services-vs-ci/vso-08.png
[18]: ./media/cloud-services-vs-ci/vso-09.png
[19]: ./media/cloud-services-vs-ci/vso-10.png
[20]: ./media/cloud-services-vs-ci/vso-11.png
[21]: ./media/cloud-services-vs-ci/vso-12.png
[22]: ./media/cloud-services-vs-ci/vso-13.png
[23]: ./media/cloud-services-vs-ci/vso-14.png
[24]: ./media/cloud-services-vs-ci/vso-15.png
