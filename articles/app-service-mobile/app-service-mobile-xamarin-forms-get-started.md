---
title: "Xamarin.Forms ile Mobile Apps’i kullanmaya başlama"
description: "Xamarin.Forms geliştirme için Azure Mobile Apps kullanmaya başlamak için bu öğreticiyi izleyin."
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
ms.openlocfilehash: ee12caaad4095cff6dae3282f747ae804f93db81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-xamarinforms-app"></a><span data-ttu-id="1201c-103">Xamarin.Forms uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="1201c-103">Create a Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="1201c-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="1201c-104">Overview</span></span>
<span data-ttu-id="1201c-105">Bu öğreticide, bir Xamarin.Forms mobil uygulamasına bulut tabanlı bir arka uç hizmetini Azure Uygulama Hizmeti’nin Mobile Apps özelliğini kullanarak nasıl ekleyeceğiniz gösterilir.</span><span class="sxs-lookup"><span data-stu-id="1201c-105">This tutorial shows you how to add a cloud-based back-end service to a Xamarin.Forms mobile app by using the Mobile Apps feature of Azure App Service as the back end.</span></span> <span data-ttu-id="1201c-106">Yeni bir Mobil Uygulama arka ucu ve uygulama verilerini Azure’da depolayan basit bir yapılacaklar listesi Xamarin.Forms uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="1201c-106">You create both a new Mobile Apps back end and a simple to-do list Xamarin.Forms app that stores app data in Azure.</span></span>

<span data-ttu-id="1201c-107">Bu öğreticiyi tamamlamak Xamarin.Forms uygulamalarına ilişkin tüm Mobile Apps öğreticileri için ön koşuldur.</span><span class="sxs-lookup"><span data-stu-id="1201c-107">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Forms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1201c-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1201c-108">Prerequisites</span></span>
<span data-ttu-id="1201c-109">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="1201c-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="1201c-110">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="1201c-110">An active Azure account.</span></span> <span data-ttu-id="1201c-111">Bir hesabınız yoksa, Azure deneme sürümünü kaydolabilir ve deneme süresi bittikten sonra dahi kullanmaya devam edebileceğiniz 10 ücretsiz mobil uygulama edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1201c-111">If you don't have an account, you can sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="1201c-112">Daha fazla bilgi için bkz. [Azure Ücretsiz Denemesi](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1201c-112">For more information, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="1201c-113">Xamarin ile Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1201c-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="1201c-114">Bilgi için [Visual Studio ve Xamarin’i ayarlama ve yükleme](https://msdn.microsoft.com/library/mt613162.aspx) sayfasına bakın.</span><span class="sxs-lookup"><span data-stu-id="1201c-114">For information, see the [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) page.</span></span>

* <span data-ttu-id="1201c-115">Xcode v7.0 veya daha sonraki sürümü ve Xamarin Studio Community yüklü bir Mac.</span><span class="sxs-lookup"><span data-stu-id="1201c-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="1201c-116">Bilgi için bkz. [Visual Studio ve Xamarin’i ayarlama ve yükleme](https://msdn.microsoft.com/library/mt613162.aspx) ve [Mac kullanıcıları için kurulum, yükleme ve doğrulamalar](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="1201c-116">For information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Set up, install, and verify for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-a-new-mobile-apps-back-end"></a><span data-ttu-id="1201c-117">Yeni bir Mobile Apps arka ucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="1201c-117">Create a new Mobile Apps back end</span></span>

<span data-ttu-id="1201c-118">Yeni bir Mobile Apps arka ucu oluşturmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="1201c-118">To create a new Mobile Apps back end, do the following:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="1201c-119">Şimdi mobil istemci uygulamalarınızın kullanabileceği bir Mobile Apps arka ucu ayarlamış oldunuz.</span><span class="sxs-lookup"><span data-stu-id="1201c-119">You have now set up a Mobile Apps back end that your mobile client applications can use.</span></span> <span data-ttu-id="1201c-120">Sırada, basit bir yapılacaklar listesi arka ucu için bir sunucu projesi indirme ve Azure’a yayımlama var.</span><span class="sxs-lookup"><span data-stu-id="1201c-120">Next, you download a server project for a simple to-do list back end and then publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="1201c-121">Sunucu projesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1201c-121">Configure the server project</span></span>

<span data-ttu-id="1201c-122">Sunucu projesini Node.js veya .NET arka ucunu kullanacak şekilde yapılandırmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="1201c-122">To configure the server project to use either the Node.js or .NET back end, do the following:</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinforms-solution"></a><span data-ttu-id="1201c-123">Xamarin.Forms çözümünü indirme ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="1201c-123">Download and run the Xamarin.Forms solution</span></span>

<span data-ttu-id="1201c-124">Çözümü iki yolla indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1201c-124">You can download the solution in either of two ways.</span></span> <span data-ttu-id="1201c-125">Çözümü bir Mac’e indirebilir ve Xamarin Studio’da açabilir ya da çözümü bir Windows bilgisayara indirebilir ve ağ ile bağlı bir Mac kullanarak iOS uygulaması oluşturmak için açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1201c-125">Download it to a Mac and open it in Xamarin Studio, or download it to a Windows computer and open it in Visual Studio by using a networked Mac for building the iOS app.</span></span> <span data-ttu-id="1201c-126">Daha fazla bilgi için [Visual Studio ve Xamarin’i ayarlama ve yükleme](https://msdn.microsoft.com/library/mt613162.aspx) sayfasına bakın.</span><span class="sxs-lookup"><span data-stu-id="1201c-126">For more information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>

<span data-ttu-id="1201c-127">Bir Mac veya Windows bilgisayarda aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="1201c-127">On a Mac or Windows computer, do the following:</span></span>

1. <span data-ttu-id="1201c-128">[Azure Portal] gidin.</span><span class="sxs-lookup"><span data-stu-id="1201c-128">Go to the [Azure portal].</span></span>

2. <span data-ttu-id="1201c-129">Mobil uygulamanızın **Ayarlar** dikey penceresinde, **Mobil** başlığı altında **Kullanmaya Başlama** > **Xamarin.Forms**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="1201c-129">On the **Settings** blade for your mobile app, under **Mobile**, select **Get Started** > **Xamarin.Forms**.</span></span> <span data-ttu-id="1201c-130">**3. adım** altında **Yeni uygulama oluştur**’u ve ardından **İndir**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="1201c-130">Under **step 3**, select  **Create a new app**, and then select **Download**.</span></span>

   <span data-ttu-id="1201c-131">Bu işlem, mobil uygulamanıza bağlı olan istemci uygulaması içeren bir projeyi indirir.</span><span class="sxs-lookup"><span data-stu-id="1201c-131">This action downloads a project that contains a client application that's connected to your mobile app.</span></span> <span data-ttu-id="1201c-132">Sıkıştırılmış proje dosyasını yerel bilgisayarınıza kaydedin ve kaydettiğiniz yeri not edin.</span><span class="sxs-lookup"><span data-stu-id="1201c-132">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>

3. <span data-ttu-id="1201c-133">İndirdiğiniz projeyi çıkarın ve Xamarin Studio (Mac) veya Visual Studio'da (Windows) açın.</span><span class="sxs-lookup"><span data-stu-id="1201c-133">Extract the project that you downloaded, and then open it in Xamarin Studio (Mac) or Visual Studio (Windows).</span></span>

   ![Xamarin Studio'da ayıklanan proje][9]

   ![Visual Studio'da ayıklanan proje][8]

## <a name="optional-run-the-ios-project"></a><span data-ttu-id="1201c-136">(İsteğe bağlı) iOS projesi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="1201c-136">(Optional) Run the iOS project</span></span>
<span data-ttu-id="1201c-137">Bu bölümde iOS cihazlarda Xamarin iOS projesi çalıştırırsınız.</span><span class="sxs-lookup"><span data-stu-id="1201c-137">In this section, you run the Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="1201c-138">iOS cihazlarıyla çalışmıyorsanız, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1201c-138">You can skip this section if you are not working with iOS devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="1201c-139">Xamarin Studio’da</span><span class="sxs-lookup"><span data-stu-id="1201c-139">In Xamarin Studio</span></span>
1. <span data-ttu-id="1201c-140">iOS projesine sağ tıklayın ve ardından **Başlangıç Projesi Olarak Ayarla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="1201c-140">Right-click the iOS project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="1201c-141">**Çalıştır** menüsünde, **Hata Ayıklamayı Başlat**’a tıklayarak projeyi oluşturun ve iPhone öykünücüsünde uygulamayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="1201c-141">On the **Run** menu, select **Start Debugging** to build the project and start the app in the iPhone emulator.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="1201c-142">Visual Studio’da</span><span class="sxs-lookup"><span data-stu-id="1201c-142">In Visual Studio</span></span>
1. <span data-ttu-id="1201c-143">iOS projesine sağ tıklayın ve ardından **Başlangıç Projesi Olarak Ayarla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="1201c-143">Right-click the iOS project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="1201c-144">**Yapı** menüsünde, **Yapılandırma Yöneticisi**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="1201c-144">On the **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="1201c-145">**Yapılandırma Yöneticisi** iletişim kutusunda, iOS projesinin yanındaki **Yapı** ve **Dağıt** onay kutularını seçin.</span><span class="sxs-lookup"><span data-stu-id="1201c-145">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** check boxes next to the iOS project.</span></span>

4. <span data-ttu-id="1201c-146">Projeyi oluşturmak ve uygulamayı iPhone öykünücüsünde başlatmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="1201c-146">To build the project and start the app in the iPhone emulator, select the **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1201c-147">Projeyi oluşturma konusunda sorun yaşarsanız, NuGet paket yöneticisini çalıştırın ve Xamarin destek paketlerinin en son sürümüne güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1201c-147">If you have problems building the project, run the NuGet package manager and update to the latest version of the Xamarin support packages.</span></span> <span data-ttu-id="1201c-148">Hızlı Başlangıç projelerinin son sürümlerine güncelleştirilme işlemleri yavaş olabilir.</span><span class="sxs-lookup"><span data-stu-id="1201c-148">Quickstart projects might be slow to update to the latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="1201c-149">Uygulamada, *Xamarin öğren* gibi anlamlı bir metin yazın ve ardından artı simgesini (**+**) seçin.</span><span class="sxs-lookup"><span data-stu-id="1201c-149">In the app, type meaningful text, such as *Learn Xamarin*, and then select the plus sign (**+**).</span></span>

    ![][10]

    <span data-ttu-id="1201c-150">Bu işlem, Azure üzerinde barındırılan yeni Mobile Apps arka ucuna bir post isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="1201c-150">This action sends a post request to the new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="1201c-151">İstekten alınan veriler TodoItem tablosuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="1201c-151">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="1201c-152">Tabloda depolanan öğeler Mobile Apps arka ucu tarafından döndürülür ve veriler listede görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1201c-152">Items that are stored in the table are returned by the Mobile Apps back end, and the data is displayed in the list.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1201c-153">Çözümünüzün taşınabilir sınık kitaplık projesinin .TodoItemManager.cs C# dosyasında Mobile Apps arka ucuna erişen kodu bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="1201c-153">You'll find the code that accesses your Mobile Apps back end in the TodoItemManager.cs C# file of the portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-the-android-project"></a><span data-ttu-id="1201c-154">(İsteğe bağlı) Android projesi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="1201c-154">(Optional) Run the Android project</span></span>
<span data-ttu-id="1201c-155">Bu bölümde Android için Xamarin droid projesini çalıştırırsınız.</span><span class="sxs-lookup"><span data-stu-id="1201c-155">In this section, you run the Xamarin droid project for Android.</span></span> <span data-ttu-id="1201c-156">Android cihazlarıyla çalışmıyorsanız, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1201c-156">You can skip this section if you are not working with Android devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="1201c-157">Xamarin Studio’da</span><span class="sxs-lookup"><span data-stu-id="1201c-157">In Xamarin Studio</span></span>

1. <span data-ttu-id="1201c-158">Android projesine sağ tıklayın ve ardından **Başlangıç Projesi Olarak Ayarla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="1201c-158">Right-click the Android project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="1201c-159">Projeyi oluşturmak ve uygulamayı Android öykünücüsünde başlatmak için **Çalıştır** menüsünde, **Hata Ayıklamayı Başlat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1201c-159">To build the project and start the app in an Android emulator, on the **Run** menu, select **Start Debugging**.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="1201c-160">Visual Studio’da</span><span class="sxs-lookup"><span data-stu-id="1201c-160">In Visual Studio</span></span>

1. <span data-ttu-id="1201c-161">Android (Droid) projesine sağ tıklayın ve ardından **Başlangıç Projesi Olarak Ayarla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="1201c-161">Right-click the Android (Droid) project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="1201c-162">**Yapı** menüsünde, **Yapılandırma Yöneticisi**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="1201c-162">On the **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="1201c-163">**Yapılandırma Yöneticisi** iletişim kutusunda, Android projesinin yanındaki **Yapı** ve **Dağıt** onay kutularını seçin.</span><span class="sxs-lookup"><span data-stu-id="1201c-163">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** check boxes next to the Android project.</span></span>

4. <span data-ttu-id="1201c-164">Projeyi oluşturmak ve Android öykünücüsünde uygulamayı başlatmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="1201c-164">To build the project and start the app in an Android emulator, select the **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1201c-165">Projeyi oluşturma konusunda sorun yaşarsanız, NuGet paket yöneticisini çalıştırın ve Xamarin destek paketlerinin en son sürümüne güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1201c-165">If you have problems building the project, run the NuGet package manager and update to the latest version of the Xamarin support packages.</span></span> <span data-ttu-id="1201c-166">Hızlı Başlangıç projelerinin son sürümlerine güncelleştirilme işlemleri yavaş olabilir.</span><span class="sxs-lookup"><span data-stu-id="1201c-166">Quickstart projects might be slow to update to the latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="1201c-167">Uygulamada, *Xamarin öğren* gibi anlamlı bir metin yazın ve ardından artı simgesini (**+**) seçin.</span><span class="sxs-lookup"><span data-stu-id="1201c-167">In the app, type meaningful text, such as *Learn Xamarin*, and then select the plus sign (**+**).</span></span>

    ![][11]
    
    <span data-ttu-id="1201c-168">Bu işlem, Azure üzerinde barındırılan yeni Mobile Apps arka ucuna bir post isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="1201c-168">This action sends a post request to the new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="1201c-169">İstekten alınan veriler TodoItem tablosuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="1201c-169">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="1201c-170">Tabloda depolanan öğeler Mobile Apps arka ucu tarafından döndürülür ve veriler listede görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1201c-170">Items that are stored in the table are returned by the Mobile Apps back end, and the data is displayed in the list.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="1201c-171">Çözümünüzün taşınabilir sınık kitaplık projesinin .TodoItemManager.cs C# dosyasında Mobile Apps arka ucuna erişen kodu bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="1201c-171">You'll find the code that accesses your Mobile Apps back end in the TodoItemManager.cs C# file of the portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-the-windows-project"></a><span data-ttu-id="1201c-172">(İsteğe bağlı) Windows projesi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="1201c-172">(Optional) Run the Windows project</span></span>

<span data-ttu-id="1201c-173">Bu bölümde Windows cihazları için Xamarin WinApp projesini çalıştırırsınız.</span><span class="sxs-lookup"><span data-stu-id="1201c-173">In this section, you run the Xamarin WinApp project for Windows devices.</span></span> <span data-ttu-id="1201c-174">Windows cihazlarıyla çalışmıyorsanız, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1201c-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="1201c-175">Visual Studio’da</span><span class="sxs-lookup"><span data-stu-id="1201c-175">In Visual Studio</span></span>

1. <span data-ttu-id="1201c-176">Windows projelerinden birine sağ tıklayın ve ardından **Başlangıç Projesi Olarak Ayarla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="1201c-176">Right-click any of the Windows projects, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="1201c-177">**Yapı** menüsünde, **Yapılandırma Yöneticisi**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="1201c-177">On the **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="1201c-178">**Yapılandırma Yöneticisi** iletişim kutusunda, seçtiğiniz Windows projesinin yanındaki **Yapı** ve **Dağıt** onay kutularını seçin.</span><span class="sxs-lookup"><span data-stu-id="1201c-178">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** check boxes next to the Windows project that you chose.</span></span>

4. <span data-ttu-id="1201c-179">Projeyi oluşturmak ve uygulamayı Windows öykünücüsünde başlatmak için **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="1201c-179">To build the project and start the app in a Windows emulator, select the **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1201c-180">Projeyi oluşturma konusunda sorun yaşarsanız, NuGet paket yöneticisini çalıştırın ve Xamarin destek paketlerinin en son sürümüne güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1201c-180">If you have problems building the project, run the NuGet package manager and update to the latest version of the Xamarin support packages.</span></span> <span data-ttu-id="1201c-181">Hızlı Başlangıç projelerinin son sürümlerine güncelleştirilme işlemleri yavaş olabilir.</span><span class="sxs-lookup"><span data-stu-id="1201c-181">Quickstart projects might be slow to update to the latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="1201c-182">Uygulamada, *Xamarin öğren* gibi anlamlı bir metin yazın ve ardından artı simgesini (**+**) seçin.</span><span class="sxs-lookup"><span data-stu-id="1201c-182">In the app, type meaningful text, such as *Learn Xamarin*, and then select the plus sign (**+**).</span></span>

    <span data-ttu-id="1201c-183">Bu işlem, Azure üzerinde barındırılan yeni Mobile Apps arka ucuna bir post isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="1201c-183">This action sends a post request to the new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="1201c-184">İstekten alınan veriler TodoItem tablosuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="1201c-184">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="1201c-185">Tabloda depolanan öğeler Mobile Apps arka ucu tarafından döndürülür ve veriler listede görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1201c-185">Items that are stored in the table are returned by the Mobile Apps back end, and the data is displayed in the list.</span></span>
    
    ![][12]
    
    > [!NOTE]
    > <span data-ttu-id="1201c-186">Çözümünüzün taşınabilir sınık kitaplık projesinin .TodoItemManager.cs C# dosyasında Mobile Apps arka ucuna erişen kodu bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="1201c-186">You'll find the code that accesses your Mobile Apps back end in the TodoItemManager.cs C# file of the portable class library project of your solution.</span></span>
    >
    >

## <a name="next-steps"></a><span data-ttu-id="1201c-187">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1201c-187">Next steps</span></span>

* [<span data-ttu-id="1201c-188">Uygulamanıza kimlik doğrulaması ekleme</span><span class="sxs-lookup"><span data-stu-id="1201c-188">Add authentication to your app</span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="1201c-189">Uygulamanızdaki kullanıcıların kimliklerini bir kimlik sağlayıcısı ile nasıl doğrulayacağınızı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="1201c-189">Learn how to authenticate users of your app with an identity provider.</span></span>

* [<span data-ttu-id="1201c-190">Uygulamanıza anında iletme bildirimleri ekleme</span><span class="sxs-lookup"><span data-stu-id="1201c-190">Add push notifications to your app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)  
  <span data-ttu-id="1201c-191">Uygulamanıza anında iletme bildirimleri desteği eklemeyi ve anında iletme bildirimleri göndermek için Azure Notification Hubs’ı kullanmak üzere Mobile App arka ucunuzu yapılandırmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="1201c-191">Learn how to add push notifications support to your app and configure your Mobile Apps back end to use Azure Notification Hubs to send the push notifications.</span></span>

* [<span data-ttu-id="1201c-192">Uygulamanız için çevrimdışı eşitlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="1201c-192">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="1201c-193">Mobile Apps arka ucu kullanarak uygulamanıza çevrimdışı destek eklemeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="1201c-193">Learn how to add offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="1201c-194">Çevrimdışı eşitleme ile mobil uygulamanızın verilerini ağ bağlantısı olmasa bile görüntüleyebilir, ekleyebilir ve değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1201c-194">With offline sync, you can view, add, or modify your mobile app's data, even when there is no network connection.</span></span>

* [<span data-ttu-id="1201c-195">Mobile Apps için yönetilen istemciyi kullanma</span><span class="sxs-lookup"><span data-stu-id="1201c-195">Use the managed client for Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)  
  <span data-ttu-id="1201c-196">Xamarin uygulamanızda yönetilen istemci SDK’sıyla çalışmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="1201c-196">Learn how to work with the managed client SDK in your Xamarin app.</span></span>

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
[Azure Portal]: https://portal.azure.com/
