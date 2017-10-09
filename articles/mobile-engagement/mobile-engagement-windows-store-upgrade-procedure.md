---
title: "aaaWindows Evrensel uygulamaları SDK yükseltme yordamları"
description: "Azure Mobile Engagement için Windows Evrensel uygulamaları SDK yükseltme yordamları"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 4c898175-2cd6-43db-b350-bb408332f24d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 95aba5d55cd65d4190aad35737f872414b5ed443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a><span data-ttu-id="ec8a7-103">Windows Evrensel uygulamaları SDK yükseltme yordamları</span><span class="sxs-lookup"><span data-stu-id="ec8a7-103">Windows Universal Apps SDK Upgrade Procedures</span></span>
<span data-ttu-id="ec8a7-104">Uygulamanıza katılım daha eski bir sürümü zaten bütünleştirdiyseniz noktaları hello SDK yükseltirken aşağıdaki tooconsider hello sahip.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-104">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="ec8a7-105">Merhaba SDK çeşitli sürümleri eksik birkaç yordamları toofollow olabilir.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="ec8a7-106">0.10.1 geçirirseniz örneğin hello izleyin toofirst sahip too0.11.0 "0.9.0'dan gelen too0.10.1" yordamı sonra hello "0.10.1 gelen too0.11.0" yordamı.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-106">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

## <a name="from-330-too340"></a><span data-ttu-id="ec8a7-107">3.3.0 gelen too3.4.0</span><span class="sxs-lookup"><span data-stu-id="ec8a7-107">From 3.3.0 too3.4.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="ec8a7-108">Test günlükleri</span><span class="sxs-lookup"><span data-stu-id="ec8a7-108">Test logs</span></span>
<span data-ttu-id="ec8a7-109">Konsol günlükleri Hello SDK tarafından üretilen artık etkin/devre dışı bırakılmış/filtrelenmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-109">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="ec8a7-110">toocustomize Bu, güncelleştirme hello özellik `EngagementAgent.Instance.TestLogEnabled` tooone hello kullanılabilir hello değerinin `EngagementTestLogLevel` numaralandırma, örneğin:</span><span class="sxs-lookup"><span data-stu-id="ec8a7-110">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a><span data-ttu-id="ec8a7-111">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ec8a7-111">Resources</span></span>
<span data-ttu-id="ec8a7-112">Merhaba ulaşma katmana geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-112">hello Reach overlay has been improved.</span></span> <span data-ttu-id="ec8a7-113">Merhaba SDK NuGet paketini kaynakları parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-113">It is part of hello SDK NuGet package resources.</span></span>

<span data-ttu-id="ec8a7-114">Merhaba SDK'ın yeni sürümü toohello yükseltirken tookeep istediğinizi varolan hello dosyalarınızdan kaynaklarınızın klasör veya kaplama seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ec8a7-114">While upgrading toohello new version of hello SDK you can choose whether you want tookeep your existing files from hello overlay folder of your resources or not:</span></span>

* <span data-ttu-id="ec8a7-115">Merhaba önceki katmana sizin yerinize çalıştığından veya hello tümleştirme `WebView` öğeleri el ile mevcut dosyalarınızı tookeep karar verebilirsiniz sonra çalışmaya devam edecektir.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-115">If hello previous overlay is working for you or you are integrating hello `WebView` elements manually then you can decide tookeep your exiting files, it will still work.</span></span> 
* <span data-ttu-id="ec8a7-116">Tooupdate toohello yeni katmana, yalnızca Değiştir hello tüm istiyorsanız `overlay` kaynaklarınızla hello SDK paketinden yeni bir hello klasöründen (UWP uygulamaları: hello yükseltmeden sonra % USERPROFILE % hello yeni katmana klasör alabilirsiniz\\. nuget\ packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span><span class="sxs-lookup"><span data-stu-id="ec8a7-116">If you want tooupdate toohello new overlay, just replace hello whole `overlay` folder from your resources with hello new one from hello SDK package (UWP apps: after hello upgrade, you can get hello new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="ec8a7-117">Merhaba yeni katmana kullanarak hello önceki sürümünde yapılan tüm özelleştirmeler üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-117">Using hello new overlay will overwrite any customizations made on hello previous version.</span></span>
> 
> 

## <a name="from-320-too330"></a><span data-ttu-id="ec8a7-118">3.2.0 gelen too3.3.0</span><span class="sxs-lookup"><span data-stu-id="ec8a7-118">From 3.2.0 too3.3.0</span></span>
### <a name="resources"></a><span data-ttu-id="ec8a7-119">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ec8a7-119">Resources</span></span>
<span data-ttu-id="ec8a7-120">Bu adım yalnızca özelleştirilmiş kaynaklar ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-120">This step concerns customized resources only.</span></span> <span data-ttu-id="ec8a7-121">Toobackup sahip hello SDK (html, görüntüler, katmana) tarafından sağlanan hello kaynakları özelleştirdiyseniz, yükseltme ve yeniden Uygula önce bunları özelleştirmeyi üzerinde yükseltilmiş kaynakları.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-121">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-310-too320"></a><span data-ttu-id="ec8a7-122">3.1.0 gelen too3.2.0</span><span class="sxs-lookup"><span data-stu-id="ec8a7-122">From 3.1.0 too3.2.0</span></span>
### <a name="resources"></a><span data-ttu-id="ec8a7-123">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ec8a7-123">Resources</span></span>
<span data-ttu-id="ec8a7-124">Bu adım yalnızca özelleştirilmiş kaynaklar ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-124">This step concerns customized resources only.</span></span> <span data-ttu-id="ec8a7-125">Toobackup sahip hello SDK (html, görüntüler, katmana) tarafından sağlanan hello kaynakları özelleştirdiyseniz, yükseltme ve yeniden Uygula önce bunları özelleştirmeyi üzerinde yükseltilmiş kaynakları.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-125">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

### <a name="webview-integration"></a><span data-ttu-id="ec8a7-126">Web görünümü tümleştirme</span><span class="sxs-lookup"><span data-stu-id="ec8a7-126">Webview integration</span></span>
<span data-ttu-id="ec8a7-127">Bazı geliştirmeler toomatch farklı cihaz form faktörleri'nın bu sürümünde sunulan.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-127">Some improvements toomatch different device form factors were introduced in this version.</span></span> <span data-ttu-id="ec8a7-128">Merhaba webview, tümleştirilmesi hello aşağıdaki eşleştiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="ec8a7-128">Make sure that your integration of hello webview match hello following:</span></span>

<span data-ttu-id="ec8a7-129">XAML sayfası () içinde:</span><span class="sxs-lookup"><span data-stu-id="ec8a7-129">In your XAML page ():</span></span>

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

<span data-ttu-id="ec8a7-130">Ve ilişkili .cs dosyanızda:</span><span class="sxs-lookup"><span data-stu-id="ec8a7-130">And in your associated .cs file:</span></span>

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated toowithin a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

              #region tooimplement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update hello webview when hello app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update hello webview when hello app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure toodetach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are hello current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements toohello correct size.
              /// </summary>
              /// <param name="width">hello width of your current display.</param>
              /// <param name="height">hello height of your current display.</param>
              private void SetWebView(double width, double height)
              {
                #pragma warning disable 4014
                CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal,
                        () =>
                        {
                          this.engagement_notification_content.Width = width;
                          this.engagement_announcement_content.Width = width;
                          this.engagement_announcement_content.Height = height;
                        });
              }

              /// <summary>
              /// Handler that takes hello Windows.Current.SizeChanged and indicates that webviews have toobe resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes hello ApplicationView.VisibleBoundsChanged and indicates that webviews have toobe resized
              /// </summary>
              /// <param name="sender">hello related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-too300"></a><span data-ttu-id="ec8a7-131">2.0.0 gelen too3.0.0</span><span class="sxs-lookup"><span data-stu-id="ec8a7-131">From 2.0.0 too3.0.0</span></span>
### <a name="resources"></a><span data-ttu-id="ec8a7-132">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="ec8a7-132">Resources</span></span>
<span data-ttu-id="ec8a7-133">Bu adım yalnızca özelleştirilmiş kaynaklar ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-133">This step concerns customized resources only.</span></span> <span data-ttu-id="ec8a7-134">Toobackup sahip hello SDK (html, görüntüler, katmana) tarafından sağlanan hello kaynakları özelleştirdiyseniz, yükseltme ve yeniden Uygula önce bunları özelleştirmeyi üzerinde yükseltilmiş kaynakları.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-134">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-111-too200"></a><span data-ttu-id="ec8a7-135">1.1.1 gelen too2.0.0</span><span class="sxs-lookup"><span data-stu-id="ec8a7-135">From 1.1.1 too2.0.0</span></span>
<span data-ttu-id="ec8a7-136">Merhaba toomigrate'nın Azure Mobile Engagement tarafından desteklenen bir uygulamaya bir SDK tümleştirmesi hello Capptain hizmet gelen Capptain SAS tarafından nasıl sunulan açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-136">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ec8a7-137">Capptain ve Mobile Engagement olan değil hello aynı Hizmetleri ve yalnızca aşağıda verilen hello yordamı nasıl toomigrate hello istemci uygulamaları vurgular.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-137">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="ec8a7-138">Geçirme hello SDK hello uygulama hello Capptain sunucuları toohello Mobile Engagement sunuculardan veri geçişi YAPILMAZ</span><span class="sxs-lookup"><span data-stu-id="ec8a7-138">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="ec8a7-139">Önceki bir sürümünden geçiş yapıyorsanız, lütfen hello Capptain web sitesi toomigrate too1.1.1 ilk başvurun sonra hello aşağıdaki yordamı uygulayın</span><span class="sxs-lookup"><span data-stu-id="ec8a7-139">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.1.1 first then apply hello following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="ec8a7-140">Nuget paketi</span><span class="sxs-lookup"><span data-stu-id="ec8a7-140">Nuget package</span></span>
<span data-ttu-id="ec8a7-141">Değiştir **Capptain.WindowsPhone** tarafından **MicrosoftAzure.MobileEngagement** Nuget paketi.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="ec8a7-142">Mobil katılım uygulama</span><span class="sxs-lookup"><span data-stu-id="ec8a7-142">Applying Mobile Engagement</span></span>
<span data-ttu-id="ec8a7-143">Merhaba SDK kullanan hello terim `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-143">hello SDK uses hello term `Engagement`.</span></span> <span data-ttu-id="ec8a7-144">Proje toomatch tooupdate gereken bu değişikliği.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-144">You need tooupdate your project toomatch this change.</span></span>

<span data-ttu-id="ec8a7-145">Toouninstall, geçerli Capptain nuget paketi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-145">You need toouninstall your current Capptain nuget package.</span></span> <span data-ttu-id="ec8a7-146">Tüm değişikliklerinizi Capptain Kaynaklar klasörünü kaldırılacak göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-146">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="ec8a7-147">Tookeep istiyorsanız, bu dosyaların bir kopyasını sonra yapın.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-147">If you want tookeep those files then make a copy of them.</span></span>

<span data-ttu-id="ec8a7-148">Bundan sonra projenizde hello yeni Microsoft Azure katılım nuget paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-148">After that, install hello new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="ec8a7-149">Doğrudan [nuget sitesinde] bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-149">You can find it directly on [nuget website].</span></span> <span data-ttu-id="ec8a7-150">veya burada dizini.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-150">or here index.</span></span> <span data-ttu-id="ec8a7-151">Tüm kaynak dosyaları katılım tarafından kullanılan ve hello yeni katılım DLL tooyour ekler bu eylem değiştirir başvuruları yansıtın.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-151">This action replaces all resources files used by Engagement and adds hello new Engagement DLL tooyour project References.</span></span>

<span data-ttu-id="ec8a7-152">Proje başvuruları Capptain DLL başvurularını silerek tooclean sahip.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-152">You have tooclean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="ec8a7-153">Bunu yapmazsanız Capptain hello sürümü çakışır ve hataları gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-153">If you do not make this, hello version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="ec8a7-154">Capptain kaynakları özelleştirdiyseniz, eski dosyaları içeriğinizi kopyalayın ve bunları hello yeni katılım dosyalarında yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-154">If you have customized Capptain resources, copy your old files content and paste them in hello new Engagement files.</span></span> <span data-ttu-id="ec8a7-155">Xaml ve cs dosyaları güncelleştirilmiş toobe gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-155">Please note that both xaml and cs files have toobe updated.</span></span>

<span data-ttu-id="ec8a7-156">Bu adımlar tamamlandığında tooreplace eski Capptain başvurular hello yeni katılım başvurular tarafından yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-156">When those steps are completed you only have tooreplace old Capptain references by hello new Engagement references.</span></span>

1. <span data-ttu-id="ec8a7-157">Tüm Capptain ad güncelleştirilmiş toobe sahip.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-157">All Capptain namespaces have toobe updated.</span></span>
   
    <span data-ttu-id="ec8a7-158">Geçişten önce:</span><span class="sxs-lookup"><span data-stu-id="ec8a7-158">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="ec8a7-159">Geçişten sonra:</span><span class="sxs-lookup"><span data-stu-id="ec8a7-159">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="ec8a7-160">"Capptain" içeren tüm Capptain sınıfları "Katılım" içermelidir.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="ec8a7-161">Geçişten önce:</span><span class="sxs-lookup"><span data-stu-id="ec8a7-161">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="ec8a7-162">Geçişten sonra:</span><span class="sxs-lookup"><span data-stu-id="ec8a7-162">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="ec8a7-163">XAML dosyaları için de Capptain ad alanı ve özniteliklerini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-163">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="ec8a7-164">Geçişten önce:</span><span class="sxs-lookup"><span data-stu-id="ec8a7-164">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="ec8a7-165">Geçişten sonra:</span><span class="sxs-lookup"><span data-stu-id="ec8a7-165">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="ec8a7-166">Sayfa değiştirir</span><span class="sxs-lookup"><span data-stu-id="ec8a7-166">Overlay page changes</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="ec8a7-167">Ayrıca değiştirir.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-167">Overlay also changes.</span></span> <span data-ttu-id="ec8a7-168">Yeni ad `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span></span> <span data-ttu-id="ec8a7-169">Xaml ve cs dosyaları kullanılan toobe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-169">It has toobe used in both xaml and cs files.</span></span> <span data-ttu-id="ec8a7-170">Üstelik `CapptainGrid` toobe adlı `EngagementGrid`, `capptain_notification_content` ve `capptain_announcement_content` adlandırıldığı `engagement_notification_content` ve `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-170">Moreover `CapptainGrid` is toobe named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span></span>
   > 
   > 
   
    <span data-ttu-id="ec8a7-171">Katmana için:</span><span class="sxs-lookup"><span data-stu-id="ec8a7-171">For overlay :</span></span>
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    <span data-ttu-id="ec8a7-172">Bu olur:</span><span class="sxs-lookup"><span data-stu-id="ec8a7-172">It becomes :</span></span>
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. <span data-ttu-id="ec8a7-173">Merhaba Capptain resimler ve HTML dosyaları gibi diğer kaynaklar lütfen unutmayın. bunlar da yeniden adlandırılmış toouse "Katılım" olmuştur.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-173">For hello other resources like Capptain pictures and HTML files, please note that they also have been renamed toouse "Engagement".</span></span>

### <a name="project-declaration"></a><span data-ttu-id="ec8a7-174">Proje bildirimi</span><span class="sxs-lookup"><span data-stu-id="ec8a7-174">Project declaration</span></span>
<span data-ttu-id="ec8a7-175">Package.appxmanifest üzerinde `File Type Associations` gelen güncelleştirildi:</span><span class="sxs-lookup"><span data-stu-id="ec8a7-175">On Package.appxmanifest `File Type Associations` has been updated from :</span></span>

* <span data-ttu-id="ec8a7-176">capptain\_ulaşmak\_içerik tooengagement\_ulaşmak\_içeriği</span><span class="sxs-lookup"><span data-stu-id="ec8a7-176">capptain\_reach\_content tooengagement\_reach\_content</span></span>
* <span data-ttu-id="ec8a7-177">capptain\_günlük\_tooengagement dosya\_günlük\_dosyası</span><span class="sxs-lookup"><span data-stu-id="ec8a7-177">capptain\_log\_file tooengagement\_log\_file</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="ec8a7-178">Uygulama Kimliği / SDK anahtarı</span><span class="sxs-lookup"><span data-stu-id="ec8a7-178">Application ID / SDK Key</span></span>
<span data-ttu-id="ec8a7-179">Katılım bağlantı dizesini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-179">Engagement uses a connection string.</span></span> <span data-ttu-id="ec8a7-180">Bir uygulama kimliği ve Mobile Engagement SDK'sı anahtarla toospecify yoksa, toospecify bir bağlantı dizesi yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-180">You don't have toospecify an application ID and an SDK key with Mobile Engagement, you only have toospecify a connection string.</span></span> <span data-ttu-id="ec8a7-181">Bunu EngagementConfiguration dosyanızı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-181">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="ec8a7-182">Merhaba katılım yapılandırma ayarlanabilir, `Resources\EngagementConfiguration.xml` projenizin dosya.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-182">hello Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="ec8a7-183">Bu dosya toospecify düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="ec8a7-183">Edit this file toospecify:</span></span>

* <span data-ttu-id="ec8a7-184">Uygulama bağlantı dizenizi etiketleri arasına `<connectionString>` ve `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="ec8a7-185">Çalışma zamanında, bunun yerine, çağırabilirsiniz hello aşağıdaki toospecify istiyorsanız yöntemi hello katılım aracı başlatmadan önce:</span><span class="sxs-lookup"><span data-stu-id="ec8a7-185">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

<span data-ttu-id="ec8a7-186">Merhaba bağlantı dizesi, uygulamanız için Klasik Azure portalı hello üzerinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-186">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="ec8a7-187">Öğe adı değişikliği</span><span class="sxs-lookup"><span data-stu-id="ec8a7-187">Items name change</span></span>
<span data-ttu-id="ec8a7-188">Tüm öğeleri adlı *capptain* adlandırılmış *engagement*.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-188">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="ec8a7-189">Benzer şekilde *Capptain* çok*Engagement*.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-189">Similarly for *Capptain* too*Engagement*.</span></span>

<span data-ttu-id="ec8a7-190">Yaygın olarak kullanılan Capptain öğeleri örnekleri:</span><span class="sxs-lookup"><span data-stu-id="ec8a7-190">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="ec8a7-191">Şimdi EngagementConfiguration adlı CapptainConfiguration</span><span class="sxs-lookup"><span data-stu-id="ec8a7-191">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="ec8a7-192">Şimdi EngagementAgent adlı CapptainAgent</span><span class="sxs-lookup"><span data-stu-id="ec8a7-192">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="ec8a7-193">Şimdi EngagementReach adlı CapptainReach</span><span class="sxs-lookup"><span data-stu-id="ec8a7-193">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="ec8a7-194">Şimdi EngagementHttpConfig adlı CapptainHttpConfig</span><span class="sxs-lookup"><span data-stu-id="ec8a7-194">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="ec8a7-195">Şimdi GetEngagementPageName adlı GetCapptainPageName</span><span class="sxs-lookup"><span data-stu-id="ec8a7-195">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="ec8a7-196">Ayrıca etkiler yeniden adlandırmak Not yöntemleri geçersiz kılındı.</span><span class="sxs-lookup"><span data-stu-id="ec8a7-196">Note that rename also affects overridden methods.</span></span>

