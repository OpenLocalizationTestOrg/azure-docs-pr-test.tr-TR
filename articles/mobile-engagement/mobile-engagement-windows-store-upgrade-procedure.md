---
title: "Windows Evrensel uygulamaları SDK yükseltme yordamları"
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
ms.openlocfilehash: fe85a99a92fb39082cafe7422b356de1f20f14bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a><span data-ttu-id="8ff88-103">Windows Evrensel uygulamaları SDK yükseltme yordamları</span><span class="sxs-lookup"><span data-stu-id="8ff88-103">Windows Universal Apps SDK Upgrade Procedures</span></span>
<span data-ttu-id="8ff88-104">Uygulamanıza katılım daha eski bir sürümü zaten bütünleştirdiyseniz, SDK'yı yükseltirken aşağıdaki noktaları dikkate almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="8ff88-105">SDK çeşitli sürümleri eksik, birçok yordamı uygulamanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="8ff88-106">Örneğin, 0.10.1 önce "Kimden 0.9.0'dan 0.10.1 için" yordamını takip etmek için sahip 0.11.0 sonra "Kimden 0.10.1 0.11.0 için" yordamı geçiş ise.</span><span class="sxs-lookup"><span data-stu-id="8ff88-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

## <a name="from-330-to-340"></a><span data-ttu-id="8ff88-107">3.3.0 3.4.0 için</span><span class="sxs-lookup"><span data-stu-id="8ff88-107">From 3.3.0 to 3.4.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="8ff88-108">Test günlükleri</span><span class="sxs-lookup"><span data-stu-id="8ff88-108">Test logs</span></span>
<span data-ttu-id="8ff88-109">SDK'sı tarafından üretilen konsol günlükleri artık etkin/devre dışı bırakılmış/filtrelenmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="8ff88-110">Bu özelleştirmek için özellik güncelleştirme `EngagementAgent.Instance.TestLogEnabled` bulunan değer birine `EngagementTestLogLevel` numaralandırma, örneğin:</span><span class="sxs-lookup"><span data-stu-id="8ff88-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a><span data-ttu-id="8ff88-111">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="8ff88-111">Resources</span></span>
<span data-ttu-id="8ff88-112">Reach katmana geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-112">The Reach overlay has been improved.</span></span> <span data-ttu-id="8ff88-113">SDK'sı NuGet paketi kaynakları parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="8ff88-113">It is part of the SDK NuGet package resources.</span></span>

<span data-ttu-id="8ff88-114">SDK'sının yeni sürüme yükseltme veya varolan dosyalarınızı kaynaklarınızı katmana klasöründen tutmak isteyip istemediğinizi seçebilirsiniz ancak:</span><span class="sxs-lookup"><span data-stu-id="8ff88-114">While upgrading to the new version of the SDK you can choose whether you want to keep your existing files from the overlay folder of your resources or not:</span></span>

* <span data-ttu-id="8ff88-115">Önceki katmana sizin yerinize çalıştığından veya tümleştirme `WebView` öğeleri el ile sonra karar mevcut dosyalarınızı korumak için bunu hala çalışır.</span><span class="sxs-lookup"><span data-stu-id="8ff88-115">If the previous overlay is working for you or you are integrating the `WebView` elements manually then you can decide to keep your exiting files, it will still work.</span></span> 
* <span data-ttu-id="8ff88-116">Yeni katmana güncelleştirmek istiyorsanız, yalnızca tam değiştirme `overlay` kaynaklarınızı klasöründen SDK paketinden yeni bir (UWP uygulamaları: yükseltmeden sonra yeni katmana klasör % USERPROFILE % alabilirsiniz\\.nuget\packages\ MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span><span class="sxs-lookup"><span data-stu-id="8ff88-116">If you want to update to the new overlay, just replace the whole `overlay` folder from your resources with the new one from the SDK package (UWP apps: after the upgrade, you can get the new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="8ff88-117">Yeni katmana kullanarak önceki bir sürümünde yapılan tüm özelleştirmeler üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="8ff88-117">Using the new overlay will overwrite any customizations made on the previous version.</span></span>
> 
> 

## <a name="from-320-to-330"></a><span data-ttu-id="8ff88-118">3.2.0 3.3.0 için</span><span class="sxs-lookup"><span data-stu-id="8ff88-118">From 3.2.0 to 3.3.0</span></span>
### <a name="resources"></a><span data-ttu-id="8ff88-119">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="8ff88-119">Resources</span></span>
<span data-ttu-id="8ff88-120">Bu adım yalnızca özelleştirilmiş kaynaklar ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-120">This step concerns customized resources only.</span></span> <span data-ttu-id="8ff88-121">Ardından (html, görüntüler, katmana) SDK tarafından sağlanan kaynakları özelleştirdiyseniz, yükseltmeden önce yedekleme ve özelleştirmeyi yükseltilmiş kaynaklardaki yeniden gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-121">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-310-to-320"></a><span data-ttu-id="8ff88-122">3.1.0 3.2.0 için</span><span class="sxs-lookup"><span data-stu-id="8ff88-122">From 3.1.0 to 3.2.0</span></span>
### <a name="resources"></a><span data-ttu-id="8ff88-123">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="8ff88-123">Resources</span></span>
<span data-ttu-id="8ff88-124">Bu adım yalnızca özelleştirilmiş kaynaklar ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-124">This step concerns customized resources only.</span></span> <span data-ttu-id="8ff88-125">Ardından (html, görüntüler, katmana) SDK tarafından sağlanan kaynakları özelleştirdiyseniz, yükseltmeden önce yedekleme ve özelleştirmeyi yükseltilmiş kaynaklardaki yeniden gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-125">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

### <a name="webview-integration"></a><span data-ttu-id="8ff88-126">Web görünümü tümleştirme</span><span class="sxs-lookup"><span data-stu-id="8ff88-126">Webview integration</span></span>
<span data-ttu-id="8ff88-127">Farklı cihaz form faktörleri eşleştirmek için bazı geliştirmeler'ın bu sürümünde sunulan.</span><span class="sxs-lookup"><span data-stu-id="8ff88-127">Some improvements to match different device form factors were introduced in this version.</span></span> <span data-ttu-id="8ff88-128">Web görünümü, tümleştirilmesi aşağıdaki eşleştiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="8ff88-128">Make sure that your integration of the webview match the following:</span></span>

<span data-ttu-id="8ff88-129">XAML sayfası () içinde:</span><span class="sxs-lookup"><span data-stu-id="8ff88-129">In your XAML page ():</span></span>

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

<span data-ttu-id="8ff88-130">Ve ilişkili .cs dosyanızda:</span><span class="sxs-lookup"><span data-stu-id="8ff88-130">And in your associated .cs file:</span></span>

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated to within a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }

              #region to implement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update the webview when the app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update the webview when the app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure to detach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are the current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements to the correct size.
              /// </summary>
              /// <param name="width">The width of your current display.</param>
              /// <param name="height">The height of your current display.</param>
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
              /// Handler that takes the Windows.Current.SizeChanged and indicates that webviews have to be resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes the ApplicationView.VisibleBoundsChanged and indicates that webviews have to be resized
              /// </summary>
              /// <param name="sender">The related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-to-300"></a><span data-ttu-id="8ff88-131">2.0.0 3.0.0 için</span><span class="sxs-lookup"><span data-stu-id="8ff88-131">From 2.0.0 to 3.0.0</span></span>
### <a name="resources"></a><span data-ttu-id="8ff88-132">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="8ff88-132">Resources</span></span>
<span data-ttu-id="8ff88-133">Bu adım yalnızca özelleştirilmiş kaynaklar ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-133">This step concerns customized resources only.</span></span> <span data-ttu-id="8ff88-134">Ardından (html, görüntüler, katmana) SDK tarafından sağlanan kaynakları özelleştirdiyseniz, yükseltmeden önce yedekleme ve özelleştirmeyi yükseltilmiş kaynaklardaki yeniden gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-134">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-111-to-200"></a><span data-ttu-id="8ff88-135">1.1.1 2.0.0 için</span><span class="sxs-lookup"><span data-stu-id="8ff88-135">From 1.1.1 to 2.0.0</span></span>
<span data-ttu-id="8ff88-136">Aşağıdaki nasıl Azure Mobile Engagement tarafından desteklenen bir uygulamaya Capptain SAS tarafından sunulan Capptain hizmetinden bir SDK tümleştirmesi geçirileceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="8ff88-136">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8ff88-137">Capptain ve Mobile Engagement aynı Hizmetleri değildir ve aşağıda verilen yordamı yalnızca istemci uygulaması geçirmek nasıl vurgular.</span><span class="sxs-lookup"><span data-stu-id="8ff88-137">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="8ff88-138">Uygulama SDK'yı geçirme verilerinizi Capptain sunucularından Mobile Engagement sunucuya geçişi YAPILMAZ</span><span class="sxs-lookup"><span data-stu-id="8ff88-138">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="8ff88-139">Önceki bir sürümünden geçiş yapıyorsanız, Lütfen 1.1.1 için önce geçirmenizi sonra aşağıdaki yordamı uygulamak için Capptain web sitesine bakın</span><span class="sxs-lookup"><span data-stu-id="8ff88-139">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="8ff88-140">Nuget paketi</span><span class="sxs-lookup"><span data-stu-id="8ff88-140">Nuget package</span></span>
<span data-ttu-id="8ff88-141">Değiştir **Capptain.WindowsPhone** tarafından **MicrosoftAzure.MobileEngagement** Nuget paketi.</span><span class="sxs-lookup"><span data-stu-id="8ff88-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="8ff88-142">Mobil katılım uygulama</span><span class="sxs-lookup"><span data-stu-id="8ff88-142">Applying Mobile Engagement</span></span>
<span data-ttu-id="8ff88-143">Terimi SDK kullanan `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="8ff88-143">The SDK uses the term `Engagement`.</span></span> <span data-ttu-id="8ff88-144">Projenizi bu değişikliği eşleşecek şekilde güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-144">You need to update your project to match this change.</span></span>

<span data-ttu-id="8ff88-145">Geçerli Capptain nuget paketini kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-145">You need to uninstall your current Capptain nuget package.</span></span> <span data-ttu-id="8ff88-146">Tüm değişikliklerinizi Capptain Kaynaklar klasörünü kaldırılacak göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="8ff88-146">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="8ff88-147">Bu dosyaları saklamak isterseniz bir kopyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8ff88-147">If you want to keep those files then make a copy of them.</span></span>

<span data-ttu-id="8ff88-148">Bundan sonra projenizde yeni Microsoft Azure katılım nuget paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8ff88-148">After that, install the new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="8ff88-149">Doğrudan [nuget sitesinde] bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ff88-149">You can find it directly on [nuget website].</span></span> <span data-ttu-id="8ff88-150">veya burada dizini.</span><span class="sxs-lookup"><span data-stu-id="8ff88-150">or here index.</span></span> <span data-ttu-id="8ff88-151">Bu eylem, katılım tarafından kullanılan tüm kaynakları dosyalarının yerini alır ve yeni katılım DLL, proje başvuruları ekler.</span><span class="sxs-lookup"><span data-stu-id="8ff88-151">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span></span>

<span data-ttu-id="8ff88-152">Proje başvuruları Capptain DLL başvurularını silerek temizlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-152">You have to clean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="8ff88-153">Bunu yapmazsanız Capptain sürümü çakışır ve hataları gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-153">If you do not make this, the version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="8ff88-154">Capptain kaynakları özelleştirdiyseniz, eski dosyaları içeriğinizi kopyalayın ve bunları yeni katılım dosyalar yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="8ff88-154">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span></span> <span data-ttu-id="8ff88-155">Xaml ve cs dosyaları güncelleştirilmesi gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8ff88-155">Please note that both xaml and cs files have to be updated.</span></span>

<span data-ttu-id="8ff88-156">Bu adımlar tamamlandığında yeni katılım başvurular tarafından eski Capptain başvuruları değiştirin yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-156">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span></span>

1. <span data-ttu-id="8ff88-157">Tüm Capptain ad alanlarını güncelleştirilmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="8ff88-157">All Capptain namespaces have to be updated.</span></span>
   
    <span data-ttu-id="8ff88-158">Geçişten önce:</span><span class="sxs-lookup"><span data-stu-id="8ff88-158">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="8ff88-159">Geçişten sonra:</span><span class="sxs-lookup"><span data-stu-id="8ff88-159">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="8ff88-160">"Capptain" içeren tüm Capptain sınıfları "Katılım" içermelidir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="8ff88-161">Geçişten önce:</span><span class="sxs-lookup"><span data-stu-id="8ff88-161">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="8ff88-162">Geçişten sonra:</span><span class="sxs-lookup"><span data-stu-id="8ff88-162">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="8ff88-163">XAML dosyaları için de Capptain ad alanı ve özniteliklerini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-163">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="8ff88-164">Geçişten önce:</span><span class="sxs-lookup"><span data-stu-id="8ff88-164">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="8ff88-165">Geçişten sonra:</span><span class="sxs-lookup"><span data-stu-id="8ff88-165">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="8ff88-166">Sayfa değiştirir</span><span class="sxs-lookup"><span data-stu-id="8ff88-166">Overlay page changes</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="8ff88-167">Ayrıca değiştirir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-167">Overlay also changes.</span></span> <span data-ttu-id="8ff88-168">Yeni ad `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="8ff88-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span></span> <span data-ttu-id="8ff88-169">Xaml ve cs dosyalarında kullanılacak sahiptir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-169">It has to be used in both xaml and cs files.</span></span> <span data-ttu-id="8ff88-170">Üstelik `CapptainGrid` adlandırılması için `EngagementGrid`, `capptain_notification_content` ve `capptain_announcement_content` adlandırıldığı `engagement_notification_content` ve `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="8ff88-170">Moreover `CapptainGrid` is to be named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span></span>
   > 
   > 
   
    <span data-ttu-id="8ff88-171">Katmana için:</span><span class="sxs-lookup"><span data-stu-id="8ff88-171">For overlay :</span></span>
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    <span data-ttu-id="8ff88-172">Bu olur:</span><span class="sxs-lookup"><span data-stu-id="8ff88-172">It becomes :</span></span>
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. <span data-ttu-id="8ff88-173">İçin diğer kaynaklar Capptain resimler ve HTML dosyaları gibi bunlar ayrıca "Katılım" kullanacak şekilde yeniden adlandırıldığı gerektiğini lütfen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8ff88-173">For the other resources like Capptain pictures and HTML files, please note that they also have been renamed to use "Engagement".</span></span>

### <a name="project-declaration"></a><span data-ttu-id="8ff88-174">Proje bildirimi</span><span class="sxs-lookup"><span data-stu-id="8ff88-174">Project declaration</span></span>
<span data-ttu-id="8ff88-175">Package.appxmanifest üzerinde `File Type Associations` gelen güncelleştirildi:</span><span class="sxs-lookup"><span data-stu-id="8ff88-175">On Package.appxmanifest `File Type Associations` has been updated from :</span></span>

* <span data-ttu-id="8ff88-176">capptain\_ulaşmak\_katılım için içerik\_ulaşmak\_içeriği</span><span class="sxs-lookup"><span data-stu-id="8ff88-176">capptain\_reach\_content to engagement\_reach\_content</span></span>
* <span data-ttu-id="8ff88-177">capptain\_günlük\_katılım dosyasına\_günlük\_dosyası</span><span class="sxs-lookup"><span data-stu-id="8ff88-177">capptain\_log\_file to engagement\_log\_file</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="8ff88-178">Uygulama Kimliği / SDK anahtarı</span><span class="sxs-lookup"><span data-stu-id="8ff88-178">Application ID / SDK Key</span></span>
<span data-ttu-id="8ff88-179">Katılım bağlantı dizesini kullanır.</span><span class="sxs-lookup"><span data-stu-id="8ff88-179">Engagement uses a connection string.</span></span> <span data-ttu-id="8ff88-180">Mobile Engagement ile bir uygulama kimliği ve bir SDK anahtarı belirtmeniz gerekmez, yalnızca bir bağlantı dizesi belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-180">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span></span> <span data-ttu-id="8ff88-181">Bunu EngagementConfiguration dosyanızı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ff88-181">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="8ff88-182">Katılım yapılandırma ayarlanabilir, `Resources\EngagementConfiguration.xml` projenizin dosya.</span><span class="sxs-lookup"><span data-stu-id="8ff88-182">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="8ff88-183">Belirtmek için bu dosyayı düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="8ff88-183">Edit this file to specify:</span></span>

* <span data-ttu-id="8ff88-184">Uygulama bağlantı dizenizi etiketleri arasına `<connectionString>` ve `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="8ff88-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="8ff88-185">Bunun yerine çalışma zamanında belirtmek istiyorsanız, katılım aracı başlatmadan önce aşağıdaki yöntemini çağırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8ff88-185">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

<span data-ttu-id="8ff88-186">Bağlantı dizesi, uygulamanız için Azure Klasik Portalı'ndaki görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8ff88-186">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="8ff88-187">Öğe adı değişikliği</span><span class="sxs-lookup"><span data-stu-id="8ff88-187">Items name change</span></span>
<span data-ttu-id="8ff88-188">Tüm öğeleri adlı *capptain* adlandırılmış *engagement*.</span><span class="sxs-lookup"><span data-stu-id="8ff88-188">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="8ff88-189">Benzer şekilde *Capptain* için *Engagement*.</span><span class="sxs-lookup"><span data-stu-id="8ff88-189">Similarly for *Capptain* to *Engagement*.</span></span>

<span data-ttu-id="8ff88-190">Yaygın olarak kullanılan Capptain öğeleri örnekleri:</span><span class="sxs-lookup"><span data-stu-id="8ff88-190">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="8ff88-191">Şimdi EngagementConfiguration adlı CapptainConfiguration</span><span class="sxs-lookup"><span data-stu-id="8ff88-191">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="8ff88-192">Şimdi EngagementAgent adlı CapptainAgent</span><span class="sxs-lookup"><span data-stu-id="8ff88-192">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="8ff88-193">Şimdi EngagementReach adlı CapptainReach</span><span class="sxs-lookup"><span data-stu-id="8ff88-193">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="8ff88-194">Şimdi EngagementHttpConfig adlı CapptainHttpConfig</span><span class="sxs-lookup"><span data-stu-id="8ff88-194">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="8ff88-195">Şimdi GetEngagementPageName adlı GetCapptainPageName</span><span class="sxs-lookup"><span data-stu-id="8ff88-195">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="8ff88-196">Ayrıca etkiler yeniden adlandırmak Not yöntemleri geçersiz kılındı.</span><span class="sxs-lookup"><span data-stu-id="8ff88-196">Note that rename also affects overridden methods.</span></span>

