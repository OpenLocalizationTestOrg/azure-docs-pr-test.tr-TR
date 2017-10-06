---
title: "Xamarin.Forms kullanarak aaaGet Mobile Apps ile başlatıldı"
description: "Xamarin.Forms geliştirme için Mobile Apps'ı kullanarak Bu öğretici toostart izleyin"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 5e692220-cc89-4548-96c8-35259722acf5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: af6b1c1ce4cf91c397552aa3d8ee40728129238c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinforms-app"></a><span data-ttu-id="54abf-103">Xamarin.Forms uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="54abf-103">Create a Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="54abf-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="54abf-104">Overview</span></span>
<span data-ttu-id="54abf-105">Bu öğretici nasıl tooadd kullanarak bulut tabanlı arka uç hizmeti tooa Xamarin.Forms mobil uygulaması hello hello arka ucu olarak Azure App Service Mobile Apps özelliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="54abf-105">This tutorial shows you how tooadd a cloud-based back-end service tooa Xamarin.Forms mobile app by using hello Mobile Apps feature of Azure App Service as hello back end.</span></span> <span data-ttu-id="54abf-106">Yeni bir Mobil Uygulama arka ucu ve uygulama verilerini Azure’da depolayan basit bir yapılacaklar listesi Xamarin.Forms uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="54abf-106">You create both a new Mobile Apps back end and a simple to-do list Xamarin.Forms app that stores app data in Azure.</span></span>

<span data-ttu-id="54abf-107">Bu öğreticiyi tamamlamak Xamarin.Forms uygulamalarına ilişkin tüm Mobile Apps öğreticileri için ön koşuldur.</span><span class="sxs-lookup"><span data-stu-id="54abf-107">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Forms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54abf-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="54abf-108">Prerequisites</span></span>
<span data-ttu-id="54abf-109">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="54abf-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="54abf-110">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="54abf-110">An active Azure account.</span></span> <span data-ttu-id="54abf-111">Bir hesabınız yoksa, bir Azure deneme sürümünü kaydolabilir ve deneme bittikten sonra dahi kullanmaya devam edebileceğiniz too10 ücretsiz mobil uygulama alın.</span><span class="sxs-lookup"><span data-stu-id="54abf-111">If you don't have an account, you can sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="54abf-112">Daha fazla bilgi için bkz. [Azure Ücretsiz Denemesi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="54abf-112">For more information, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="54abf-113">Xamarin ile Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54abf-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="54abf-114">Merhaba bilgi için bkz [ayarlamak ayarlama ve Visual Studio ve Xamarin yükleme](https://msdn.microsoft.com/library/mt613162.aspx) sayfası.</span><span class="sxs-lookup"><span data-stu-id="54abf-114">For information, see hello [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) page.</span></span>

* <span data-ttu-id="54abf-115">Xcode v7.0 veya daha sonraki sürümü ve Xamarin Studio Community yüklü bir Mac.</span><span class="sxs-lookup"><span data-stu-id="54abf-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="54abf-116">Bilgi için bkz. [Visual Studio ve Xamarin’i ayarlama ve yükleme](https://msdn.microsoft.com/library/mt613162.aspx) ve [Mac kullanıcıları için kurulum, yükleme ve doğrulamalar](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="54abf-116">For information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Set up, install, and verify for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-a-new-mobile-apps-back-end"></a><span data-ttu-id="54abf-117">Yeni bir Mobile Apps arka ucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="54abf-117">Create a new Mobile Apps back end</span></span>

<span data-ttu-id="54abf-118">geri yeni bir Mobile Apps end, toocreate hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="54abf-118">toocreate a new Mobile Apps back end, do hello following:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="54abf-119">Şimdi mobil istemci uygulamalarınızın kullanabileceği bir Mobile Apps arka ucu ayarlamış oldunuz.</span><span class="sxs-lookup"><span data-stu-id="54abf-119">You have now set up a Mobile Apps back end that your mobile client applications can use.</span></span> <span data-ttu-id="54abf-120">Ardından, bir basit bir Yapılacaklar listesi arka ucu için bir sunucu projesi indirin ve tooAzure yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="54abf-120">Next, you download a server project for a simple to-do list back end and then publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="54abf-121">Merhaba sunucu projesi yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="54abf-121">Configure hello server project</span></span>

<span data-ttu-id="54abf-122">tooconfigure hello sunucu projesi toouse Node.js veya .NET arka ucu Merhaba, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="54abf-122">tooconfigure hello server project toouse either hello Node.js or .NET back end, do hello following:</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinforms-solution"></a><span data-ttu-id="54abf-123">Karşıdan yükleme ve başlangıç Xamarin.Forms çözümünü çalıştırma</span><span class="sxs-lookup"><span data-stu-id="54abf-123">Download and run hello Xamarin.Forms solution</span></span>

<span data-ttu-id="54abf-124">İki yoldan biriyle hello çözümde indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54abf-124">You can download hello solution in either of two ways.</span></span> <span data-ttu-id="54abf-125">Tooa Mac indirin ve Xamarin Studio'da açın veya tooa Windows bilgisayarı yükleyebilir ve ağa bağlı bir Mac kullanarak hello iOS uygulaması oluşturmak için Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="54abf-125">Download it tooa Mac and open it in Xamarin Studio, or download it tooa Windows computer and open it in Visual Studio by using a networked Mac for building hello iOS app.</span></span> <span data-ttu-id="54abf-126">Daha fazla bilgi için [Visual Studio ve Xamarin’i ayarlama ve yükleme](https://msdn.microsoft.com/library/mt613162.aspx) sayfasına bakın.</span><span class="sxs-lookup"><span data-stu-id="54abf-126">For more information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>

<span data-ttu-id="54abf-127">Mac veya Windows bilgisayarda, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="54abf-127">On a Mac or Windows computer, do hello following:</span></span>

1. <span data-ttu-id="54abf-128">Toohello Git [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="54abf-128">Go toohello [Azure portal].</span></span>

2. <span data-ttu-id="54abf-129">Merhaba üzerinde **ayarları** mobil uygulamanızın dikey altında **mobil**seçin **Get Started** > **Xamarin.Forms**.</span><span class="sxs-lookup"><span data-stu-id="54abf-129">On hello **Settings** blade for your mobile app, under **Mobile**, select **Get Started** > **Xamarin.Forms**.</span></span> <span data-ttu-id="54abf-130">**3. adım** altında **Yeni uygulama oluştur**’u ve ardından **İndir**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="54abf-130">Under **step 3**, select  **Create a new app**, and then select **Download**.</span></span>

   <span data-ttu-id="54abf-131">Bu eylem bağlı tooyour mobil uygulama olan istemci uygulaması içeren bir projeyi indirir.</span><span class="sxs-lookup"><span data-stu-id="54abf-131">This action downloads a project that contains a client application that's connected tooyour mobile app.</span></span> <span data-ttu-id="54abf-132">Merhaba sıkıştırılmış proje dosyasını tooyour yerel bilgisayara kaydedin ve kaydettiğiniz yeri not edin.</span><span class="sxs-lookup"><span data-stu-id="54abf-132">Save hello compressed project file tooyour local computer, and make a note of where you save it.</span></span>

3. <span data-ttu-id="54abf-133">İndirdiğiniz Merhaba projeyi çıkarın ve Xamarin Studio (Mac) veya Visual Studio'da (Windows) açın.</span><span class="sxs-lookup"><span data-stu-id="54abf-133">Extract hello project that you downloaded, and then open it in Xamarin Studio (Mac) or Visual Studio (Windows).</span></span>

   ![Xamarin Studio'da ayıklanan proje][9]

   ![Visual Studio'da ayıklanan proje][8]

## <a name="optional-run-hello-ios-project"></a><span data-ttu-id="54abf-136">(İsteğe bağlı) Merhaba iOS projesi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="54abf-136">(Optional) Run hello iOS project</span></span>
<span data-ttu-id="54abf-137">Bu bölümde, iOS cihazları için hello Xamarin iOS projesi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="54abf-137">In this section, you run hello Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="54abf-138">iOS cihazlarıyla çalışmıyorsanız, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54abf-138">You can skip this section if you are not working with iOS devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="54abf-139">Xamarin Studio’da</span><span class="sxs-lookup"><span data-stu-id="54abf-139">In Xamarin Studio</span></span>
1. <span data-ttu-id="54abf-140">Merhaba iOS projesine sağ tıklayın ve ardından **başlangıç projesi olarak ayarla**.</span><span class="sxs-lookup"><span data-stu-id="54abf-140">Right-click hello iOS project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="54abf-141">Merhaba üzerinde **çalıştırmak** menüsünde, select **hata ayıklamayı Başlat** toobuild hello proje ve hello uygulamayı hello iPhone öykünücüsünde başlatın.</span><span class="sxs-lookup"><span data-stu-id="54abf-141">On hello **Run** menu, select **Start Debugging** toobuild hello project and start hello app in hello iPhone emulator.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="54abf-142">Visual Studio’da</span><span class="sxs-lookup"><span data-stu-id="54abf-142">In Visual Studio</span></span>
1. <span data-ttu-id="54abf-143">Merhaba iOS projesine sağ tıklayın ve ardından **başlangıç projesi olarak ayarla**.</span><span class="sxs-lookup"><span data-stu-id="54abf-143">Right-click hello iOS project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="54abf-144">Merhaba üzerinde **yapı** menüsünde, select **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="54abf-144">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="54abf-145">Merhaba, **Configuration Manager** iletişim kutusu, select hello **yapı** ve **dağıtma** onay kutularını sonraki toohello iOS projesi.</span><span class="sxs-lookup"><span data-stu-id="54abf-145">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello iOS project.</span></span>

4. <span data-ttu-id="54abf-146">toobuild hello proje ve hello uygulamayı hello iPhone öykünücüsünde, select hello başlatın **F5** anahtarı.</span><span class="sxs-lookup"><span data-stu-id="54abf-146">toobuild hello project and start hello app in hello iPhone emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="54abf-147">Başlangıç projesi oluşturma sorunları varsa hello NuGet Paket Yöneticisi ve güncelleştirme toohello en son sürümünü hello Xamarin destek paketlerinin çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="54abf-147">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="54abf-148">Hızlı Başlangıç projeleri yavaş tooupdate toohello en son sürümleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="54abf-148">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="54abf-149">Merhaba uygulamada gibi anlamlı bir metin yazın *Xamarin öğren*, ve ardından artı işaretini seçin hello (**+**).</span><span class="sxs-lookup"><span data-stu-id="54abf-149">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    ![][10]

    <span data-ttu-id="54abf-150">Bu eylem, yeni mobil uygulama arka Azure üzerinde barındırılan uç bir post isteği toohello gönderir.</span><span class="sxs-lookup"><span data-stu-id="54abf-150">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="54abf-151">Veriler hello istek hello Todoıtem tablosuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="54abf-151">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="54abf-152">Hello tabloda depolanan öğeler veri hello listesinde görüntülenen Mobile Apps sonlandırmak ve hello hello tarafından döndürülür.</span><span class="sxs-lookup"><span data-stu-id="54abf-152">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>

    > [!NOTE]
    > <span data-ttu-id="54abf-153">Mobile Apps arka uç hello Todoıtemmanager.cs C# çözümünüzün hello taşınabilir sınıf kitaplığı proje dosyası içinde erişen hello kodu bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="54abf-153">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-hello-android-project"></a><span data-ttu-id="54abf-154">(İsteğe bağlı) Merhaba Android projesi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="54abf-154">(Optional) Run hello Android project</span></span>
<span data-ttu-id="54abf-155">Bu bölümde, hello Xamarin Android projesi Android için çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="54abf-155">In this section, you run hello Xamarin droid project for Android.</span></span> <span data-ttu-id="54abf-156">Android cihazlarıyla çalışmıyorsanız, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54abf-156">You can skip this section if you are not working with Android devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="54abf-157">Xamarin Studio’da</span><span class="sxs-lookup"><span data-stu-id="54abf-157">In Xamarin Studio</span></span>

1. <span data-ttu-id="54abf-158">Merhaba Android projesine sağ tıklayın ve ardından **başlangıç projesi olarak ayarla**.</span><span class="sxs-lookup"><span data-stu-id="54abf-158">Right-click hello Android project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="54abf-159">toobuild hello proje ve hello uygulama hello bir Android öykünücüsünde başlatın **çalıştırmak** menüsünde, select **hata ayıklamayı Başlat**.</span><span class="sxs-lookup"><span data-stu-id="54abf-159">toobuild hello project and start hello app in an Android emulator, on hello **Run** menu, select **Start Debugging**.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="54abf-160">Visual Studio’da</span><span class="sxs-lookup"><span data-stu-id="54abf-160">In Visual Studio</span></span>

1. <span data-ttu-id="54abf-161">Merhaba Android (Droid) projesine sağ tıklayın ve ardından **başlangıç projesi olarak ayarla**.</span><span class="sxs-lookup"><span data-stu-id="54abf-161">Right-click hello Android (Droid) project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="54abf-162">Merhaba üzerinde **yapı** menüsünde, select **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="54abf-162">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="54abf-163">Merhaba, **Configuration Manager** iletişim kutusu, select hello **yapı** ve **dağıtma** onay kutularını sonraki toohello Android projesi.</span><span class="sxs-lookup"><span data-stu-id="54abf-163">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello Android project.</span></span>

4. <span data-ttu-id="54abf-164">toobuild hello proje ve hello uygulamayı Android öykünücüsünde, select hello başlatın **F5** anahtarı.</span><span class="sxs-lookup"><span data-stu-id="54abf-164">toobuild hello project and start hello app in an Android emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="54abf-165">Başlangıç projesi oluşturma sorunları varsa hello NuGet Paket Yöneticisi ve güncelleştirme toohello en son sürümünü hello Xamarin destek paketlerinin çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="54abf-165">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="54abf-166">Hızlı Başlangıç projeleri yavaş tooupdate toohello en son sürümleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="54abf-166">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="54abf-167">Merhaba uygulamada gibi anlamlı bir metin yazın *Xamarin öğren*, ve ardından artı işaretini seçin hello (**+**).</span><span class="sxs-lookup"><span data-stu-id="54abf-167">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    ![][11]
    
    <span data-ttu-id="54abf-168">Bu eylem, yeni mobil uygulama arka Azure üzerinde barındırılan uç bir post isteği toohello gönderir.</span><span class="sxs-lookup"><span data-stu-id="54abf-168">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="54abf-169">Veriler hello istek hello Todoıtem tablosuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="54abf-169">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="54abf-170">Hello tabloda depolanan öğeler veri hello listesinde görüntülenen Mobile Apps sonlandırmak ve hello hello tarafından döndürülür.</span><span class="sxs-lookup"><span data-stu-id="54abf-170">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="54abf-171">Mobile Apps arka uç hello Todoıtemmanager.cs C# çözümünüzün hello taşınabilir sınıf kitaplığı proje dosyası içinde erişen hello kodu bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="54abf-171">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-hello-windows-project"></a><span data-ttu-id="54abf-172">(İsteğe bağlı) Merhaba Windows projesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="54abf-172">(Optional) Run hello Windows project</span></span>

<span data-ttu-id="54abf-173">Bu bölümde, Windows cihazları için Xamarin WinApp projesi hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="54abf-173">In this section, you run hello Xamarin WinApp project for Windows devices.</span></span> <span data-ttu-id="54abf-174">Windows cihazlarıyla çalışmıyorsanız, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54abf-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="54abf-175">Visual Studio’da</span><span class="sxs-lookup"><span data-stu-id="54abf-175">In Visual Studio</span></span>

1. <span data-ttu-id="54abf-176">Merhaba Windows projeleri hiçbirini sağ tıklayın ve ardından **başlangıç projesi olarak ayarla**.</span><span class="sxs-lookup"><span data-stu-id="54abf-176">Right-click any of hello Windows projects, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="54abf-177">Merhaba üzerinde **yapı** menüsünde, select **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="54abf-177">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="54abf-178">Merhaba, **Configuration Manager** iletişim kutusu, select hello **yapı** ve **dağıtma** seçtiğiniz onay kutularını sonraki toohello Windows projesi.</span><span class="sxs-lookup"><span data-stu-id="54abf-178">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello Windows project that you chose.</span></span>

4. <span data-ttu-id="54abf-179">toobuild hello proje ve hello uygulamayı Windows öykünücüsünde, select hello başlatın **F5** anahtarı.</span><span class="sxs-lookup"><span data-stu-id="54abf-179">toobuild hello project and start hello app in a Windows emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="54abf-180">Başlangıç projesi oluşturma sorunları varsa hello NuGet Paket Yöneticisi ve güncelleştirme toohello en son sürümünü hello Xamarin destek paketlerinin çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="54abf-180">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="54abf-181">Hızlı Başlangıç projeleri yavaş tooupdate toohello en son sürümleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="54abf-181">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="54abf-182">Merhaba uygulamada gibi anlamlı bir metin yazın *Xamarin öğren*, ve ardından artı işaretini seçin hello (**+**).</span><span class="sxs-lookup"><span data-stu-id="54abf-182">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    <span data-ttu-id="54abf-183">Bu eylem, yeni mobil uygulama arka Azure üzerinde barındırılan uç bir post isteği toohello gönderir.</span><span class="sxs-lookup"><span data-stu-id="54abf-183">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="54abf-184">Veriler hello istek hello Todoıtem tablosuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="54abf-184">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="54abf-185">Hello tabloda depolanan öğeler veri hello listesinde görüntülenen Mobile Apps sonlandırmak ve hello hello tarafından döndürülür.</span><span class="sxs-lookup"><span data-stu-id="54abf-185">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>
    
    ![][12]
    
    > [!NOTE]
    > <span data-ttu-id="54abf-186">Mobile Apps arka uç hello Todoıtemmanager.cs C# çözümünüzün hello taşınabilir sınıf kitaplığı proje dosyası içinde erişen hello kodu bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="54abf-186">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="next-steps"></a><span data-ttu-id="54abf-187">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="54abf-187">Next steps</span></span>

* [<span data-ttu-id="54abf-188">Kimlik doğrulama tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="54abf-188">Add authentication tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="54abf-189">Bilgi nasıl bir kimlik sağlayıcısı ile uygulamanızın tooauthenticate kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="54abf-189">Learn how tooauthenticate users of your app with an identity provider.</span></span>

* [<span data-ttu-id="54abf-190">Anında iletme bildirimleri tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="54abf-190">Add push notifications tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)  
  <span data-ttu-id="54abf-191">Mobile Apps arka uç toouse Azure Notification Hubs toosend hello anında iletme bildirimlerini yapılandırmak ve tooadd anında iletme bildirimleri tooyour uygulama'ı nasıl desteklediğini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="54abf-191">Learn how tooadd push notifications support tooyour app and configure your Mobile Apps back end toouse Azure Notification Hubs toosend hello push notifications.</span></span>

* [<span data-ttu-id="54abf-192">Uygulamanız için çevrimdışı eşitlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="54abf-192">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="54abf-193">Bilgi nasıl tooadd çevrimdışı destek Mobile Apps kullanarak uygulamanız için yedekleme son.</span><span class="sxs-lookup"><span data-stu-id="54abf-193">Learn how tooadd offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="54abf-194">Çevrimdışı eşitleme ile mobil uygulamanızın verilerini ağ bağlantısı olmasa bile görüntüleyebilir, ekleyebilir ve değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54abf-194">With offline sync, you can view, add, or modify your mobile app's data, even when there is no network connection.</span></span>

* [<span data-ttu-id="54abf-195">Mobile Apps için Hello yönetilen istemci kullanma</span><span class="sxs-lookup"><span data-stu-id="54abf-195">Use hello managed client for Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)  
  <span data-ttu-id="54abf-196">İstemci SDK'sı, Xamarin uygulamanızda toowork hello ile nasıl yönetileceğini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="54abf-196">Learn how toowork with hello managed client SDK in your Xamarin app.</span></span>

<!-- Anchors. -->
[Get started with Mobile Apps back ends]:#getting-started
[Create a new Mobile Apps back end]:#create-new-service
[Next steps]:#next-steps


<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
