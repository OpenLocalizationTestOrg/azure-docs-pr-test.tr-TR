---
title: "aaaSmooth akış Windows mağazası uygulaması Öğreticisi | Microsoft Docs"
description: "Nasıl toouse Azure Media Services toocreate XML MediaElement'i C# Windows mağazası uygulamasıyla kontrol tooplayback kesintisiz akış içeriği öğrenin."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0fa5d8c5-3d5f-4886-ae55-fb6de4f5256d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: juliako
ms.openlocfilehash: b02aa2c7f68fe22a23ea846d72fdd23bfba2b19c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobuild-a-smooth-streaming-windows-store-application"></a><span data-ttu-id="978dd-103">Nasıl tooBuild kesintisiz akış Windows mağazası uygulaması</span><span class="sxs-lookup"><span data-stu-id="978dd-103">How tooBuild a Smooth Streaming Windows Store Application</span></span>

<span data-ttu-id="978dd-104">Merhaba kesintisiz akış istemci SDK Windows 8 için isteğe bağlı ve canlı kesintisiz akış içeriği yürütebilirsiniz geliştiriciler toobuild Windows mağazası uygulamaları etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="978dd-104">hello Smooth Streaming Client SDK for Windows 8 enables developers toobuild Windows Store applications that can play on-demand and live Smooth Streaming content.</span></span> <span data-ttu-id="978dd-105">Ayrıca toohello temel içerik, hello SDK de akış kesintisiz çalınmasını Microsoft PlayReady koruma, kalite düzeyi kısıtlama, Canlı DVR, geçiş, (örneğin, kalite düzeyi değişiklikleri durum güncelleştirmeleri için dinleme ses akışı gibi zengin özellikleri sağlar ) ve hata olayları ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="978dd-105">In addition toohello basic playback of Smooth Streaming content, hello SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span></span> <span data-ttu-id="978dd-106">Merhaba desteklenen hello özellikleri daha fazla bilgi için bkz: [sürüm notları](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span><span class="sxs-lookup"><span data-stu-id="978dd-106">For more information of hello supported features, see hello [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span></span> <span data-ttu-id="978dd-107">Daha fazla bilgi için bkz: [Windows 8 için Player Framework](http://playerframework.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="978dd-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span></span> 

<span data-ttu-id="978dd-108">Bu öğretici dört dersleri içerir:</span><span class="sxs-lookup"><span data-stu-id="978dd-108">This tutorial contains four lessons:</span></span>

1. <span data-ttu-id="978dd-109">Bir temel kesintisiz akış depolama uygulaması oluştur</span><span class="sxs-lookup"><span data-stu-id="978dd-109">Create a Basic Smooth Streaming Store Application</span></span>
2. <span data-ttu-id="978dd-110">Bir kaydırma tooControl hello medya ilerleme çubuğu ekleyin</span><span class="sxs-lookup"><span data-stu-id="978dd-110">Add a Slider Bar tooControl hello Media Progress</span></span>
3. <span data-ttu-id="978dd-111">Kesintisiz akış akışları seçin</span><span class="sxs-lookup"><span data-stu-id="978dd-111">Select Smooth Streaming Streams</span></span>
4. <span data-ttu-id="978dd-112">Kesintisiz akış parçaları seçin</span><span class="sxs-lookup"><span data-stu-id="978dd-112">Select Smooth Streaming Tracks</span></span>

## <a name="prerequisites"></a><span data-ttu-id="978dd-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="978dd-113">Prerequisites</span></span>
* <span data-ttu-id="978dd-114">Windows 8 32 bit veya 64-bit.</span><span class="sxs-lookup"><span data-stu-id="978dd-114">Windows 8 32-bit or 64-bit.</span></span> <span data-ttu-id="978dd-115">Alma [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) MSDN'den.</span><span class="sxs-lookup"><span data-stu-id="978dd-115">You can get [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) from MSDN.</span></span>
* <span data-ttu-id="978dd-116">Visual Studio 2012 veya Visual Studio Express 2012 (veya sonraki bir sürümünü).</span><span class="sxs-lookup"><span data-stu-id="978dd-116">Visual Studio 2012 or Visual Studio Express 2012 (or a later version).</span></span> <span data-ttu-id="978dd-117">Merhaba deneme sürümünden alabilirsiniz [burada](http://www.microsoft.com/visualstudio/11/downloads).</span><span class="sxs-lookup"><span data-stu-id="978dd-117">You can get hello trial version from [here](http://www.microsoft.com/visualstudio/11/downloads).</span></span>
* <span data-ttu-id="978dd-118">[Microsoft Windows 8 için İstemci SDK akış kesintisiz](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span><span class="sxs-lookup"><span data-stu-id="978dd-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span></span>

<span data-ttu-id="978dd-119">Her ders tamamlandı hello çözümü MSDN Geliştirici kod örneklerini (kod Galerisi) indirilebilir:</span><span class="sxs-lookup"><span data-stu-id="978dd-119">hello completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span></span> 

* <span data-ttu-id="978dd-120">[Ders 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - Media Player, akış basit Windows 8 kesintisiz</span><span class="sxs-lookup"><span data-stu-id="978dd-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span></span> 
* <span data-ttu-id="978dd-121">[Ders 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - basit Windows 8 düzgün Media Player kaydırıcı çubuğun ile akış denetimi</span><span class="sxs-lookup"><span data-stu-id="978dd-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span></span> 
* <span data-ttu-id="978dd-122">[Ders 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - bir Windows 8 kesintisiz akış seçimi ile Media Player akış</span><span class="sxs-lookup"><span data-stu-id="978dd-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span></span>  
* <span data-ttu-id="978dd-123">[Ders 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) - Media Player izleme seçimi ile akış Windows 8 düzgün.</span><span class="sxs-lookup"><span data-stu-id="978dd-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span></span>

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a><span data-ttu-id="978dd-124">Ders 1: temel bir kesintisiz akış mağazası uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="978dd-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span></span>

<span data-ttu-id="978dd-125">Bu ders içinde bir Windows mağazası uygulaması MediaElement bir denetim tooplay kesintisiz akış ile içerik oluşturur.</span><span class="sxs-lookup"><span data-stu-id="978dd-125">In this lesson, you will create a Windows Store application with a MediaElement control tooplay Smooth Stream content.</span></span>  <span data-ttu-id="978dd-126">Merhaba çalışan uygulama şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="978dd-126">hello running application looks like:</span></span>

![Kesintisiz akış Windows mağazası uygulama örneği][PlayerApplication]

<span data-ttu-id="978dd-128">Windows mağazası uygulaması geliştirme hakkında daha fazla bilgi için bkz: [geliştirmek harika uygulamaları Windows 8 için](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span><span class="sxs-lookup"><span data-stu-id="978dd-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span></span> <span data-ttu-id="978dd-129">Bu ders hello yordamları içerir:</span><span class="sxs-lookup"><span data-stu-id="978dd-129">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="978dd-130">Bir Windows mağazası projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="978dd-130">Create a Windows Store project</span></span>
2. <span data-ttu-id="978dd-131">Tasarım hello kullanıcı arabirimi (XAML)</span><span class="sxs-lookup"><span data-stu-id="978dd-131">Design hello user interface (XAML)</span></span>
3. <span data-ttu-id="978dd-132">Dosyanın arkasındaki Hello kodunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="978dd-132">Modify hello code behind file</span></span>
4. <span data-ttu-id="978dd-133">Derleme ve hello uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="978dd-133">Compile and test hello application</span></span>

<span data-ttu-id="978dd-134">**toocreate bir Windows mağazası projesi**</span><span class="sxs-lookup"><span data-stu-id="978dd-134">**toocreate a Windows Store project**</span></span>

1. <span data-ttu-id="978dd-135">Visual Studio 2012 veya sonraki sürümünü çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="978dd-135">Run Visual Studio 2012 or later.</span></span>
2. <span data-ttu-id="978dd-136">Merhaba gelen **dosya** menüsünde tıklatın **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="978dd-136">From hello **FILE** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="978dd-137">Merhaba yeni proje iletişim kutusundan türü ya da aşağıdaki select hello değerler:</span><span class="sxs-lookup"><span data-stu-id="978dd-137">From hello New Project dialog, type or select  hello following values:</span></span>

| <span data-ttu-id="978dd-138">Ad</span><span class="sxs-lookup"><span data-stu-id="978dd-138">Name</span></span> | <span data-ttu-id="978dd-139">Değer</span><span class="sxs-lookup"><span data-stu-id="978dd-139">Value</span></span> |
| --- | --- |
| <span data-ttu-id="978dd-140">Şablon grubu</span><span class="sxs-lookup"><span data-stu-id="978dd-140">Template group</span></span> |<span data-ttu-id="978dd-141">Yüklü/Şablonlar/Visual C# / Windows Mağazası</span><span class="sxs-lookup"><span data-stu-id="978dd-141">Installed/Templates/Visual C#/Windows Store</span></span> |
| <span data-ttu-id="978dd-142">Şablon</span><span class="sxs-lookup"><span data-stu-id="978dd-142">Template</span></span> |<span data-ttu-id="978dd-143">Boş uygulama (XAML)</span><span class="sxs-lookup"><span data-stu-id="978dd-143">Blank App (XAML)</span></span> |
| <span data-ttu-id="978dd-144">Ad</span><span class="sxs-lookup"><span data-stu-id="978dd-144">Name</span></span> |<span data-ttu-id="978dd-145">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="978dd-145">SSPlayer</span></span> |
| <span data-ttu-id="978dd-146">Konum</span><span class="sxs-lookup"><span data-stu-id="978dd-146">Location</span></span> |<span data-ttu-id="978dd-147">C:\SSTutorials</span><span class="sxs-lookup"><span data-stu-id="978dd-147">C:\SSTutorials</span></span> |
| <span data-ttu-id="978dd-148">Çözüm adı</span><span class="sxs-lookup"><span data-stu-id="978dd-148">Solution Name</span></span> |<span data-ttu-id="978dd-149">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="978dd-149">SSPlayer</span></span> |
| <span data-ttu-id="978dd-150">Çözüm için dizin oluşturun</span><span class="sxs-lookup"><span data-stu-id="978dd-150">Create directory for solution</span></span> |<span data-ttu-id="978dd-151">(Seçili)</span><span class="sxs-lookup"><span data-stu-id="978dd-151">(selected)</span></span> |

1. <span data-ttu-id="978dd-152">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="978dd-152">Click **OK**.</span></span>

<span data-ttu-id="978dd-153">**tooadd başvuru toohello kesintisiz akış istemci SDK'sı**</span><span class="sxs-lookup"><span data-stu-id="978dd-153">**tooadd a reference toohello Smooth Streaming Client SDK**</span></span>

1. <span data-ttu-id="978dd-154">Çözüm Gezgini'nden sağ **SSPlayer**ve ardından **Başvuru Ekle**.</span><span class="sxs-lookup"><span data-stu-id="978dd-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span></span>
2. <span data-ttu-id="978dd-155">Değerleri aşağıdaki hello seçin veya yazın:</span><span class="sxs-lookup"><span data-stu-id="978dd-155">Type or select hello following values:</span></span>

| <span data-ttu-id="978dd-156">Ad</span><span class="sxs-lookup"><span data-stu-id="978dd-156">Name</span></span> | <span data-ttu-id="978dd-157">Değer</span><span class="sxs-lookup"><span data-stu-id="978dd-157">Value</span></span> |
| --- | --- |
| <span data-ttu-id="978dd-158">Başvuru grubu</span><span class="sxs-lookup"><span data-stu-id="978dd-158">Reference group</span></span> |<span data-ttu-id="978dd-159">Windows/uzantıları</span><span class="sxs-lookup"><span data-stu-id="978dd-159">Windows/Extensions</span></span> |
| <span data-ttu-id="978dd-160">Başvuru</span><span class="sxs-lookup"><span data-stu-id="978dd-160">Reference</span></span> |<span data-ttu-id="978dd-161">Microsoft Windows 8 ve Microsoft Visual C++ çalışma zamanı paketi için İstemci SDK akış kesintisiz seçin</span><span class="sxs-lookup"><span data-stu-id="978dd-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span></span> |

1. <span data-ttu-id="978dd-162">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="978dd-162">Click **OK**.</span></span> 

<span data-ttu-id="978dd-163">Merhaba başvuruları ekledikten sonra hedeflenen hello platform (x64 veya x86) seçmeniz gerekir, ekleyerek başvuruları için herhangi bir CPU platform yapılandırması çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="978dd-163">After adding hello references, you must select hello targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span></span>  <span data-ttu-id="978dd-164">Çözüm Gezgini'nde, sarı renkli uyarı işareti bu başvurular eklenen görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="978dd-164">In solution explorer, you will see yellow warning mark for these added references.</span></span>

<span data-ttu-id="978dd-165">**toodesign hello player kullanıcı arabirimi**</span><span class="sxs-lookup"><span data-stu-id="978dd-165">**toodesign hello player user interface**</span></span>

1. <span data-ttu-id="978dd-166">Çözüm Gezgini'nde, çift tıklayarak **MainPage.xaml** tooopen hello tasarım görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="978dd-166">From Solution Explorer, double click **MainPage.xaml** tooopen it in hello design view.</span></span>
2. <span data-ttu-id="978dd-167">Merhaba bulun  **&lt;kılavuz&gt;**  ve  **&lt;/Grid&gt;**  etiketleri hello XAML dosyası ve Yapıştır hello aşağıdaki kod hello iki etiketleri arasında:</span><span class="sxs-lookup"><span data-stu-id="978dd-167">Locate hello **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags hello XAML file, and paste hello following code between hello two tags:</span></span>

         <Grid.RowDefinitions>

            <RowDefinition Height="20"/>    <!-- spacer -->
            <RowDefinition Height="50"/>    <!-- media controls -->
            <RowDefinition Height="100*"/>  <!-- media element -->
            <RowDefinition Height="80*"/>   <!-- media stream and track selection -->
            <RowDefinition Height="50"/>    <!-- status bar -->
         </Grid.RowDefinitions>

         <StackPanel Name="spMediaControl" Grid.Row="1" Orientation="Horizontal">
            <TextBlock x:Name="tbSource" Text="Source :  " FontSize="16" FontWeight="Bold" VerticalAlignment="Center" />
            <TextBox x:Name="txtMediaSource" Text="http://ecn.channel9.msdn.com/o9/content/smf/smoothcontent/elephantsdream/Elephants_Dream_1024-h264-st-aac.ism/manifest" FontSize="10" Width="700" Margin="0,4,0,10" />
            <Button x:Name="btnSetSource" Content="Set Source" Width="111" Height="43" Click="btnSetSource_Click"/>
            <Button x:Name="btnPlay" Content="Play" Width="111" Height="43" Click="btnPlay_Click"/>
            <Button x:Name="btnPause" Content="Pause"  Width="111" Height="43" Click="btnPause_Click"/>
            <Button x:Name="btnStop" Content="Stop"  Width="111" Height="43" Click="btnStop_Click"/>
            <CheckBox x:Name="chkAutoPlay" Content="Auto Play" Height="55" Width="Auto" IsChecked="{Binding AutoPlay, ElementName=mediaElement, Mode=TwoWay}"/>
            <CheckBox x:Name="chkMute" Content="Mute" Height="55" Width="67" IsChecked="{Binding IsMuted, ElementName=mediaElement, Mode=TwoWay}"/>
         </StackPanel>

         <StackPanel Name="spMediaElement" Grid.Row="2" Height="435" Width="1072"
                    HorizontalAlignment="Center" VerticalAlignment="Center">
            <MediaElement x:Name="mediaElement" Height="356" Width="924" MinHeight="225"
                          HorizontalAlignment="Center" VerticalAlignment="Center" 
                          AudioCategory="BackgroundCapableMedia" />
            <StackPanel Orientation="Horizontal">
                <Slider x:Name="sliderProgress" Width="924" Height="44"
                        HorizontalAlignment="Center" VerticalAlignment="Center"
                        PointerPressed="sliderProgress_PointerPressed"/>
                <Slider x:Name="sliderVolume" 
                        HorizontalAlignment="Right" VerticalAlignment="Center" Orientation="Vertical" 
                        Height="79" Width="148" Minimum="0" Maximum="1" StepFrequency="0.1" 
                        Value="{Binding Volume, ElementName=mediaElement, Mode=TwoWay}" 
                        ToolTipService.ToolTip="{Binding Value, RelativeSource={RelativeSource Mode=Self}}"/>
            </StackPanel>
         </StackPanel>

         <StackPanel Name="spStatus" Grid.Row="4" Orientation="Horizontal">
            <TextBlock x:Name="tbStatus" Text="Status :  " 
               FontSize="16" FontWeight="Bold" VerticalAlignment="Center" HorizontalAlignment="Center" />
            <TextBox x:Name="txtStatus" FontSize="10" Width="700" VerticalAlignment="Center"/>
         </StackPanel>
   
   <span data-ttu-id="978dd-168">Merhaba MediaElement denetimi kullanılan tooplayback medya ' dir.</span><span class="sxs-lookup"><span data-stu-id="978dd-168">hello MediaElement control is used tooplayback media.</span></span> <span data-ttu-id="978dd-169">Merhaba kaydırıcı denetimi sliderProgress adlı hello sonraki Ders toocontrol hello medya ediyor kullanılır.</span><span class="sxs-lookup"><span data-stu-id="978dd-169">hello slider control named sliderProgress will be used in hello next lesson toocontrol hello media progress.</span></span>
3. <span data-ttu-id="978dd-170">Tuşuna **CTRL + S** toosave hello dosya.</span><span class="sxs-lookup"><span data-stu-id="978dd-170">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="978dd-171">Merhaba MediaElement denetimi kesintisiz akış içerik out-of-box desteklemez.</span><span class="sxs-lookup"><span data-stu-id="978dd-171">hello MediaElement control does not support Smooth Streaming content out-of-box.</span></span> <span data-ttu-id="978dd-172">tooenable hello desteği, kesintisiz akış, kesintisiz akış bayt akışı hello işleyici dosya adı uzantısı ve MIME türü tarafından kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="978dd-172">tooenable hello Smooth Streaming support, you must register hello Smooth Streaming byte-stream handler by file name extension and MIME type.</span></span>  <span data-ttu-id="978dd-173">tooregister, hello Windows.Media ad alanının hello MediaExtensionManager.RegisterByteStremHandler yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="978dd-173">tooregister, you use hello MediaExtensionManager.RegisterByteStremHandler method of hello Windows.Media namespace.</span></span>

<span data-ttu-id="978dd-174">Bu XAML dosyası içinde bazı olay işleyicileri hello denetimleri ile ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="978dd-174">In this XAML file, some event handlers are associated with hello controls.</span></span>  <span data-ttu-id="978dd-175">Bu olay işleyicileri tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="978dd-175">You must define those event handlers.</span></span>

<span data-ttu-id="978dd-176">**dosyanın arkasındaki toomodify hello kodu**</span><span class="sxs-lookup"><span data-stu-id="978dd-176">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="978dd-177">Çözüm Gezgini'nden sağ **MainPage.xaml**ve ardından **görünümü kodu**.</span><span class="sxs-lookup"><span data-stu-id="978dd-177">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="978dd-178">Merhaba dosya Hello üstünde hello aşağıdakileri ekleyin deyimi kullanarak:</span><span class="sxs-lookup"><span data-stu-id="978dd-178">At hello top of hello file, add hello following using statement:</span></span>
   
        using Windows.Media;
3. <span data-ttu-id="978dd-179">Merhaba hello başında **MainPage** sınıfı, veri üyenin hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-179">At hello beginning of hello **MainPage** class, add hello following data member:</span></span>
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. <span data-ttu-id="978dd-180">Merhaba hello sonunda **MainPage** oluşturucusu, hello aşağıdaki iki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-180">At hello end of hello **MainPage** constructor, add hello following two lines:</span></span>
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. <span data-ttu-id="978dd-181">Merhaba hello sonunda **MainPage** sınıfı, hello aşağıdaki kodu yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="978dd-181">At hello end of hello **MainPage** class, paste hello following code:</span></span>
   
         # region UI Button Click Events
         private void btnPlay_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Play();
         txtStatus.Text = "MediaElement is playing ...";
         }
         private void btnPause_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Pause();
         txtStatus.Text = "MediaElement is paused";
         }
         private void btnSetSource_Click(object sender, RoutedEventArgs e)
         {

         sliderProgress.Value = 0;
         mediaElement.Source = new Uri(txtMediaSource.Text);

         if (chkAutoPlay.IsChecked == true)
         {
             txtStatus.Text = "MediaElement is playing ...";
         }
         else
         {
             txtStatus.Text = "Click hello Play button tooplay hello media source.";
         }
         }
         private void btnStop_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Stop();
         txtStatus.Text = "MediaElement is stopped";
         }
         private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)
         {

         txtStatus.Text = "Seek tooposition " + sliderProgress.Value;
         mediaElement.Position = new TimeSpan(0, 0, (int)(sliderProgress.Value));
         }
         # endregion

<span data-ttu-id="978dd-182">Merhaba sliderProgress_PointerPressed olay işleyicisi burada belirtilir.</span><span class="sxs-lookup"><span data-stu-id="978dd-182">hello sliderProgress_PointerPressed event handler is defined here.</span></span>  <span data-ttu-id="978dd-183">Daha fazla works toodo tooget vardır, çalışma, hangi kapsamdaki hello sonraki Bu öğreticinin Ders.</span><span class="sxs-lookup"><span data-stu-id="978dd-183">There are more works toodo tooget it working, which will be covered in hello next lesson of this tutorial.</span></span>
6. <span data-ttu-id="978dd-184">Tuşuna **CTRL + S** toosave hello dosya.</span><span class="sxs-lookup"><span data-stu-id="978dd-184">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="978dd-185">Merhaba tamamlanmış hello kodu dosyanın arkasındaki şöyle:</span><span class="sxs-lookup"><span data-stu-id="978dd-185">hello finished hello code behind file shall look like this:</span></span>

![Visual Studio, kesintisiz akış Windows mağazası uygulamasında Codeview][CodeViewPic]

<span data-ttu-id="978dd-187">**toocompile ve test Merhaba uygulaması**</span><span class="sxs-lookup"><span data-stu-id="978dd-187">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="978dd-188">Merhaba gelen **yapı** menüsünde tıklatın **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="978dd-188">From hello **BUILD** menu, click **Configuration Manager**.</span></span>
2. <span data-ttu-id="978dd-189">Değişiklik **etkin çözüm platformu** toomatch geliştirme platformu.</span><span class="sxs-lookup"><span data-stu-id="978dd-189">Change **Active solution platform** toomatch your development platform.</span></span>
3. <span data-ttu-id="978dd-190">Tuşuna **F6** toocompile hello projesi.</span><span class="sxs-lookup"><span data-stu-id="978dd-190">Press **F6** toocompile hello project.</span></span> 
4. <span data-ttu-id="978dd-191">Tuşuna **F5** toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="978dd-191">Press **F5** toorun hello application.</span></span>
5. <span data-ttu-id="978dd-192">Merhaba uygulaması Hello üstünde hello varsayılan kesintisiz akış URL'sini kullanabilir veya farklı bir tane girin.</span><span class="sxs-lookup"><span data-stu-id="978dd-192">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
6. <span data-ttu-id="978dd-193">Tıklatın **ayarlamak kaynak**.</span><span class="sxs-lookup"><span data-stu-id="978dd-193">Click **Set Source**.</span></span> <span data-ttu-id="978dd-194">Çünkü **Otomatik Yürüt** hello medya yürütme otomatik olarak varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="978dd-194">Because **Auto Play** is enabled by default, hello media shall play automatically.</span></span>  <span data-ttu-id="978dd-195">Merhaba medya hello kullanarak denetleyebilirsiniz **Yürüt**, **duraklatma** ve **durdurmak** düğmeler.</span><span class="sxs-lookup"><span data-stu-id="978dd-195">You can control hello media using hello **Play**, **Pause** and **Stop** buttons.</span></span>  <span data-ttu-id="978dd-196">Merhaba dikey kaydırıcıyı kullanarak hello medya birimi kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="978dd-196">You can control hello media volume using hello vertical slider.</span></span>  <span data-ttu-id="978dd-197">Ancak medya ilerleme tam henüz uygulanmadı hello denetleme yatay kaydırıcı hello.</span><span class="sxs-lookup"><span data-stu-id="978dd-197">However hello horizontal slider for controlling hello media progress is not fully implemented yet.</span></span> 

<span data-ttu-id="978dd-198">Lesson1 tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="978dd-198">You have completed lesson1.</span></span>  <span data-ttu-id="978dd-199">Bu alıştırmanın ilerisinde MediaElement denetimi tooplayback kesintisiz akış içeriği kullanın.</span><span class="sxs-lookup"><span data-stu-id="978dd-199">In this lesson, you use a MediaElement control tooplayback Smooth Streaming content.</span></span>  <span data-ttu-id="978dd-200">Merhaba sonraki ders, kesintisiz akış içeriği hello kaydırıcı toocontrol hello ilerlemesini ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="978dd-200">In hello next lesson, you will add a slider toocontrol hello progress of hello Smooth Streaming content.</span></span>

## <a name="lesson-2-add-a-slider-bar-toocontrol-hello-media-progress"></a><span data-ttu-id="978dd-201">Ders 2: kaydırma tooControl hello medya ilerleme çubuğu ekleme</span><span class="sxs-lookup"><span data-stu-id="978dd-201">Lesson 2: Add a Slider Bar tooControl hello Media Progress</span></span>

<span data-ttu-id="978dd-202">Ders 1'de, bir Windows mağazası uygulaması MediaElement XAML denetim tooplayback kesintisiz akış medya içeriği ile oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="978dd-202">In lesson 1, you created a Windows Store application with a MediaElement XAML control tooplayback Smooth Streaming media content.</span></span>  <span data-ttu-id="978dd-203">Başlatma, durdurma ve duraklatma gibi bazı temel media işlevleri gelir.</span><span class="sxs-lookup"><span data-stu-id="978dd-203">It comes some basic media functions like start, stop and pause.</span></span>  <span data-ttu-id="978dd-204">Bu alıştırmanın ilerisinde kaydırıcı çubuk denetim toohello uygulaması ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="978dd-204">In this lesson, you will add a slider bar control toohello application.</span></span>

<span data-ttu-id="978dd-205">Bu öğreticide, hello geçerli hello MediaElement denetimi konumuna bağlı bir zamanlayıcı tooupdate hello kaydırıcı konumu kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="978dd-205">In this tutorial, we will use a timer tooupdate hello slider position based on hello current position of hello MediaElement control.</span></span>  <span data-ttu-id="978dd-206">Merhaba kaydırıcı başlatın ve bitiş zamanı da gerek toobe durumunda dinamik içerik güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="978dd-206">hello slider start and end time also need toobe updated in case of live content.</span></span>  <span data-ttu-id="978dd-207">Bu, daha iyi hello Uyarlamalı kaynak güncelleştirme olayda işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="978dd-207">This can be better handled in hello adaptive source update event.</span></span>

<span data-ttu-id="978dd-208">Medya kaynaklarına medya veri üreten nesneleridir.</span><span class="sxs-lookup"><span data-stu-id="978dd-208">Media sources are objects that generate media data.</span></span>  <span data-ttu-id="978dd-209">Merhaba kaynak Çözümleyici bir URL veya bayt akış alır ve bu içerik hello uygun medya kaynağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="978dd-209">hello source resolver takes a URL or byte stream and creates hello appropriate media source for that content.</span></span>  <span data-ttu-id="978dd-210">Merhaba kaynak çözümleyici hello standart hello uygulamaları toocreate medya kaynakları için yoludur.</span><span class="sxs-lookup"><span data-stu-id="978dd-210">hello source resolver is hello standard way for hello applications toocreate media sources.</span></span> 

<span data-ttu-id="978dd-211">Bu ders hello yordamları içerir:</span><span class="sxs-lookup"><span data-stu-id="978dd-211">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="978dd-212">Merhaba kesintisiz akış işleyici kaydetme</span><span class="sxs-lookup"><span data-stu-id="978dd-212">Register hello Smooth Streaming handler</span></span> 
2. <span data-ttu-id="978dd-213">Merhaba Uyarlamalı Kaynak Yöneticisi düzeyi olay işleyicileri ekleme</span><span class="sxs-lookup"><span data-stu-id="978dd-213">Add hello adaptive source manager level event handlers</span></span>
3. <span data-ttu-id="978dd-214">Merhaba Uyarlamalı kaynak düzeyi olay işleyicileri ekleme</span><span class="sxs-lookup"><span data-stu-id="978dd-214">Add hello adaptive source level event handlers</span></span>
4. <span data-ttu-id="978dd-215">MediaElement olay işleyicileri ekleme</span><span class="sxs-lookup"><span data-stu-id="978dd-215">Add MediaElement event handlers</span></span>
5. <span data-ttu-id="978dd-216">Kaydırma çubuğu ilgili kod ekleme</span><span class="sxs-lookup"><span data-stu-id="978dd-216">Add slider bar related code</span></span>
6. <span data-ttu-id="978dd-217">Derleme ve hello uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="978dd-217">Compile and test hello application</span></span>

<span data-ttu-id="978dd-218">**tooregister hello kesintisiz akış bayt akışı işleyicisi ve geçişi hello propertyset**</span><span class="sxs-lookup"><span data-stu-id="978dd-218">**tooregister hello Smooth Streaming byte-stream handler and pass hello propertyset**</span></span>

1. <span data-ttu-id="978dd-219">Çözüm Gezgini'nden sağ tıklayın **MainPage.xaml**ve ardından **görünümü kodu**.</span><span class="sxs-lookup"><span data-stu-id="978dd-219">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="978dd-220">Merhaba dosya Hello başında hello aşağıdakileri ekleyin deyimi kullanarak:</span><span class="sxs-lookup"><span data-stu-id="978dd-220">At hello beginning of hello file, add hello following using statement:</span></span>

        using Microsoft.Media.AdaptiveStreaming;
3. <span data-ttu-id="978dd-221">Merhaba MainPage sınıfı Hello başlangıcında, veri üyeleri aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-221">At hello beginning of hello MainPage class, add hello following data members:</span></span>

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. <span data-ttu-id="978dd-222">İç hello **MainPage** oluşturucusu, koddan sonra hello hello eklemek **bu. Components() başlatılamadı;**  satır ve hello önceki Ders içinde yazılmış hello kayıt kod satırı:</span><span class="sxs-lookup"><span data-stu-id="978dd-222">Inside hello **MainPage** constructor, add hello following code after hello **this.Initialize Components();** line and hello registration code lines written in hello previous lesson:</span></span>

        // Gets hello default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value tooAdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. <span data-ttu-id="978dd-223">İç hello **MainPage** oluşturucusu, hello iki RegisterByteStreamHandler yöntemleri tooadd hello İleri parametreleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="978dd-223">Inside hello **MainPage** constructor, modify hello two RegisterByteStreamHandler methods tooadd hello forth parameters:</span></span>

         // Registers Smooth Streaming byte-stream handler for ".ism" extension and, 
         // "text/xml" and "application/vnd.ms-ss" mime-types and pass hello propertyset. 
         // http://*.ism/manifest URI resources will be resolved by Byte-stream handler.
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "text/xml", 
            propertySet );
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "application/vnd.ms-sstr+xml", 
         propertySet);
6. <span data-ttu-id="978dd-224">Tuşuna **CTRL + S** toosave hello dosya.</span><span class="sxs-lookup"><span data-stu-id="978dd-224">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="978dd-225">**tooadd hello Uyarlamalı Kaynak Yöneticisi düzeyi olay işleyicisi**</span><span class="sxs-lookup"><span data-stu-id="978dd-225">**tooadd hello adaptive source manager level event handler**</span></span>

1. <span data-ttu-id="978dd-226">Çözüm Gezgini'nden sağ tıklayın **MainPage.xaml**ve ardından **görünümü kodu**.</span><span class="sxs-lookup"><span data-stu-id="978dd-226">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="978dd-227">İç hello **MainPage** sınıfı, veri üyenin hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-227">Inside hello **MainPage** class, add hello following data member:</span></span>
   
     <span data-ttu-id="978dd-228">Özel AdaptiveSource adaptiveSource = null;</span><span class="sxs-lookup"><span data-stu-id="978dd-228">private AdaptiveSource adaptiveSource = null;</span></span>
3. <span data-ttu-id="978dd-229">Merhaba hello sonunda **MainPage** sınıf, olay işleyicisi aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-229">At hello end of hello **MainPage** class, add hello following event handler:</span></span>
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. <span data-ttu-id="978dd-230">Merhaba hello sonunda **MainPage** oluşturucusu, satır toosubscribe toohello Uyarlamalı kaynak açık olay aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-230">At hello end of hello **MainPage** constructor, add hello following line toosubscribe toohello adaptive source open event:</span></span>
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. <span data-ttu-id="978dd-231">Tuşuna **CTRL + S** toosave hello dosya.</span><span class="sxs-lookup"><span data-stu-id="978dd-231">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="978dd-232">**tooadd Uyarlamalı kaynak düzeyi olay işleyicileri**</span><span class="sxs-lookup"><span data-stu-id="978dd-232">**tooadd adaptive source level event handlers**</span></span>

1. <span data-ttu-id="978dd-233">Çözüm Gezgini'nden sağ tıklayın **MainPage.xaml**ve ardından **görünümü kodu**.</span><span class="sxs-lookup"><span data-stu-id="978dd-233">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="978dd-234">İç hello **MainPage** sınıfı, veri üyenin hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-234">Inside hello **MainPage** class, add hello following data member:</span></span>
   
     <span data-ttu-id="978dd-235">Özel AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   Özel bildirim manifestObject;</span><span class="sxs-lookup"><span data-stu-id="978dd-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span></span>
3. <span data-ttu-id="978dd-236">Merhaba hello sonunda **MainPage** sınıf, olay işleyicileri aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-236">At hello end of hello **MainPage** class, add hello following event handlers:</span></span>

         # region Adaptive Source Level Events
         private void mediaElement_ManifestReady(AdaptiveSource sender, ManifestReadyEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
            manifestObject = args.AdaptiveSource.Manifest;
         }

         private void mediaElement_AdaptiveSourceStatusUpdated(AdaptiveSource sender, AdaptiveSourceStatusUpdatedEventArgs args)
         {

            adaptiveSourceStatusUpdate = args;
         }

         private void mediaElement_AdaptiveSourceFailed(AdaptiveSource sender, AdaptiveSourceFailedEventArgs args)
         {

            txtStatus.Text = "Error: " + args.HttpResponse;
         }

         # endregion Adaptive Source Level Events
4. <span data-ttu-id="978dd-237">Merhaba hello sonunda **mediaElement AdaptiveSourceOpened** yöntemi, kod toosubscribe toohello olayları aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-237">At hello end of hello **mediaElement AdaptiveSourceOpened** method, add hello following code toosubscribe toohello events:</span></span>
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. <span data-ttu-id="978dd-238">Tuşuna **CTRL + S** toosave hello dosya.</span><span class="sxs-lookup"><span data-stu-id="978dd-238">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="978dd-239">Merhaba işlevselliği ortak tooall ortam öğeleri hello uygulamasında işlemek için kullanılan Uyarlamalı kaynak yöneticisi düzeyinde de aynı olayları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="978dd-239">hello same events are available on Adaptive Source manger level as well, which can be used for handling functionality common tooall media elements in hello app.</span></span> <span data-ttu-id="978dd-240">Tüm AdaptiveSource olayları AdaptiveSourceManager altında basamaklı ve her AdaptiveSource, kendi olaylarını içerir.</span><span class="sxs-lookup"><span data-stu-id="978dd-240">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span></span>

<span data-ttu-id="978dd-241">**tooadd medya öğesi olay işleyicileri**</span><span class="sxs-lookup"><span data-stu-id="978dd-241">**tooadd Media Element event handlers**</span></span>

1. <span data-ttu-id="978dd-242">Çözüm Gezgini'nden sağ tıklayın **MainPage.xaml**ve ardından **görünümü kodu**.</span><span class="sxs-lookup"><span data-stu-id="978dd-242">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="978dd-243">Merhaba hello sonunda **MainPage** sınıf, olay işleyicileri aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-243">At hello end of hello **MainPage** class, add hello following event handlers:</span></span>

         # region Media Element Event Handlers
         private void MediaOpened(object sender, RoutedEventArgs e)
         {

            txtStatus.Text = "MediaElement opened";
         }

         private void MediaFailed(object sender, ExceptionRoutedEventArgs e)
         {

            txtStatus.Text= "MediaElement failed: " + e.ErrorMessage;
         }

         private void MediaEnded(object sender, RoutedEventArgs e)
         {

            txtStatus.Text ="MediaElement ended.";
         }

         # endregion Media Element Event Handlers
3. <span data-ttu-id="978dd-244">Merhaba hello sonunda **MainPage** oluşturucusu, kod toosubscript toohello olayları aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-244">At hello end of hello **MainPage** constructor, add hello following code toosubscript toohello events:</span></span>

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. <span data-ttu-id="978dd-245">Tuşuna **CTRL + S** toosave hello dosya.</span><span class="sxs-lookup"><span data-stu-id="978dd-245">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="978dd-246">**ilgili barkod tooadd kaydırıcı**</span><span class="sxs-lookup"><span data-stu-id="978dd-246">**tooadd slider bar related code**</span></span>

1. <span data-ttu-id="978dd-247">Çözüm Gezgini'nden sağ tıklayın **MainPage.xaml**ve ardından **görünümü kodu**.</span><span class="sxs-lookup"><span data-stu-id="978dd-247">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="978dd-248">Merhaba dosya Hello başında hello aşağıdakileri ekleyin deyimi kullanarak:</span><span class="sxs-lookup"><span data-stu-id="978dd-248">At hello beginning of hello file, add hello following using statement:</span></span>
      
        using Windows.UI.Core;
3. <span data-ttu-id="978dd-249">İç hello **MainPage** sınıfı, veri üyeleri aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-249">Inside hello **MainPage** class, add hello following data members:</span></span>
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. <span data-ttu-id="978dd-250">Merhaba hello sonunda **MainPage** oluşturucusu, hello aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-250">At hello end of hello **MainPage** constructor, add hello following code:</span></span>
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. <span data-ttu-id="978dd-251">Merhaba hello sonunda **MainPage** sınıfı, hello aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-251">At hello end of hello **MainPage** class, add hello following code:</span></span>

         # region sliderMediaPlayer
         private double SliderFrequency(TimeSpan timevalue)
         {

            long absvalue = 0;
            double stepfrequency = -1;

            if (manifestObject != null)
            {
                absvalue = manifestObject.Duration - (long)manifestObject.StartTime;
            }
            else
            {
                absvalue = mediaElement.NaturalDuration.TimeSpan.Ticks;
            }

            TimeSpan totalDVRDuration = new TimeSpan(absvalue);

            if (totalDVRDuration.TotalMinutes >= 10 && totalDVRDuration.TotalMinutes < 30)
            {
               stepfrequency = 10;
            }
            else if (totalDVRDuration.TotalMinutes >= 30 
                     && totalDVRDuration.TotalMinutes < 60)
            {
                stepfrequency = 30;
            }
            else if (totalDVRDuration.TotalHours >= 1)
            {
                stepfrequency = 60;
            }

            return stepfrequency;
         }

         void updateSliderPositionoNTicks(object sender, object e)
         {

            sliderProgress.Value = mediaElement.Position.TotalSeconds;
         }

         public void setupTimer()
         {

            sliderPositionUpdateDispatcher = new DispatcherTimer();
            sliderPositionUpdateDispatcher.Interval = new TimeSpan(0, 0, 0, 0, 300);
            startTimer();
         }

         public void startTimer()
         {

            sliderPositionUpdateDispatcher.Tick += updateSliderPositionoNTicks;
            sliderPositionUpdateDispatcher.Start();
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderStartTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.StartTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Minimum = absvalue;
            });
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderEndTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Maximum = absvalue;
            });
         }

         # endregion sliderMediaPlayer
      
>[!NOTE]
><span data-ttu-id="978dd-252">CoreDispatcher toohello UI dışı kullanıcı Arabirimi iş parçacığından iş parçacığı kullanılan toomake değişiklikler var.</span><span class="sxs-lookup"><span data-stu-id="978dd-252">CoreDispatcher is used toomake changes toohello UI thread from non UI Thread.</span></span> <span data-ttu-id="978dd-253">Dağıtıcı iş parçacığı engeli durumunda, geliştirici klasöründe tooupdate oranla toouse dağıtıcısı kullanıcı Arabirimi öğesi tarafından sağlanan seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="978dd-253">In case of bottleneck on dispatcher thread, developer can choose toouse dispatcher provided by UI-element he/she intends tooupdate.</span></span>  <span data-ttu-id="978dd-254">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="978dd-254">For example:</span></span>
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. <span data-ttu-id="978dd-255">Merhaba hello sonunda **mediaElement_AdaptiveSourceStatusUpdated** yöntemi, hello aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-255">At hello end of hello **mediaElement_AdaptiveSourceStatusUpdated** method, add hello following code:</span></span>

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. <span data-ttu-id="978dd-256">Merhaba hello sonunda **MediaOpened** yöntemi, hello aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-256">At hello end of hello **MediaOpened** method, add hello following code:</span></span>

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. <span data-ttu-id="978dd-257">Tuşuna **CTRL + S** toosave hello dosya.</span><span class="sxs-lookup"><span data-stu-id="978dd-257">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="978dd-258">**toocompile ve test Merhaba uygulaması**</span><span class="sxs-lookup"><span data-stu-id="978dd-258">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="978dd-259">Tuşuna **F6** toocompile hello projesi.</span><span class="sxs-lookup"><span data-stu-id="978dd-259">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="978dd-260">Tuşuna **F5** toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="978dd-260">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="978dd-261">Merhaba uygulaması Hello üstünde hello varsayılan kesintisiz akış URL'sini kullanabilir veya farklı bir tane girin.</span><span class="sxs-lookup"><span data-stu-id="978dd-261">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="978dd-262">Tıklatın **ayarlamak kaynak**.</span><span class="sxs-lookup"><span data-stu-id="978dd-262">Click **Set Source**.</span></span> 
5. <span data-ttu-id="978dd-263">Test hello kaydırıcı çubuk.</span><span class="sxs-lookup"><span data-stu-id="978dd-263">Test hello slider bar.</span></span>

<span data-ttu-id="978dd-264">Ders 2 tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="978dd-264">You have completed lesson 2.</span></span>  <span data-ttu-id="978dd-265">Bu ders kaydırıcı tooapplication eklendi.</span><span class="sxs-lookup"><span data-stu-id="978dd-265">In this lesson you added a slider tooapplication.</span></span> 

## <a name="lesson-3-select-smooth-streaming-streams"></a><span data-ttu-id="978dd-266">Ders 3: Kesintisiz akış akışları seçin</span><span class="sxs-lookup"><span data-stu-id="978dd-266">Lesson 3: Select Smooth Streaming Streams</span></span>
<span data-ttu-id="978dd-267">Kesintisiz akış, hello görüntüleyicileri tarafından seçilebilen birden çok dil ses izleri ile özellikli toostream içeriktir.</span><span class="sxs-lookup"><span data-stu-id="978dd-267">Smooth Streaming is capable toostream content with multiple language audio tracks that are selectable by hello viewers.</span></span>  <span data-ttu-id="978dd-268">Bu alıştırmanın ilerisinde görüntüleyiciler tooselect akışları olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="978dd-268">In this lesson, you will enable viewers tooselect streams.</span></span> <span data-ttu-id="978dd-269">Bu ders hello yordamları içerir:</span><span class="sxs-lookup"><span data-stu-id="978dd-269">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="978dd-270">Merhaba XAML dosyasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="978dd-270">Modify hello XAML file</span></span>
2. <span data-ttu-id="978dd-271">Merhaba kod behand dosyasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="978dd-271">Modify hello code behand file</span></span>
3. <span data-ttu-id="978dd-272">Derleme ve hello uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="978dd-272">Compile and test hello application</span></span>

<span data-ttu-id="978dd-273">**toomodify hello XAML dosyası**</span><span class="sxs-lookup"><span data-stu-id="978dd-273">**toomodify hello XAML file**</span></span>

1. <span data-ttu-id="978dd-274">Çözüm Gezgini'nden sağ **MainPage.xaml**ve ardından **Görünüm Tasarımcısı**.</span><span class="sxs-lookup"><span data-stu-id="978dd-274">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="978dd-275">Bulun &lt;Grid.RowDefinitions&gt;ve görünür gibi hello RowDefinitions değiştirin:</span><span class="sxs-lookup"><span data-stu-id="978dd-275">Locate &lt;Grid.RowDefinitions&gt;, and modify hello RowDefinitions so they looks like:</span></span>
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. <span data-ttu-id="978dd-276">İç hello &lt;kılavuz&gt;&lt;/Grid&gt; etiketler eklemek hello kodundan aşağıdaki kodu toodefine listbox denetimi, böylece kullanıcılar kullanılabilir akışları hello listesini görmek ve akışlar seçin:</span><span class="sxs-lookup"><span data-stu-id="978dd-276">Inside hello &lt;Grid&gt;&lt;/Grid&gt; tags, add hello following code toodefine a listbox control, so users can see hello list of available streams, and select streams:</span></span>

         <Grid Name="gridStreamAndBitrateSelection" Grid.Row="3">
            <Grid.RowDefinitions>
                <RowDefinition Height="300"/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="250*"/>
                <ColumnDefinition Width="250*"/>
            </Grid.ColumnDefinitions>
            <StackPanel Name="spStreamSelection" Grid.Row="1" Grid.Column="0">
                <StackPanel Orientation="Horizontal">
                    <TextBlock Name="tbAvailableStreams" Text="Available Streams:" FontSize="16" VerticalAlignment="Center"></TextBlock>
                    <Button Name="btnChangeStreams" Content="Submit" Click="btnChangeStream_Click"/>
                </StackPanel>
                <ListBox x:Name="lbAvailableStreams" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                    ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
                    <ListBox.ItemTemplate>
                        <DataTemplate>
                            <CheckBox Content="{Binding Name}" IsChecked="{Binding isChecked, Mode=TwoWay}" />
                        </DataTemplate>
                    </ListBox.ItemTemplate>
                </ListBox>
            </StackPanel>
         </Grid>
4. <span data-ttu-id="978dd-277">Tuşuna **CTRL + S** toosave hello değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="978dd-277">Press **CTRL+S** toosave hello changes.</span></span>

<span data-ttu-id="978dd-278">**dosyanın arkasındaki toomodify hello kodu**</span><span class="sxs-lookup"><span data-stu-id="978dd-278">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="978dd-279">Çözüm Gezgini'nden sağ **MainPage.xaml**ve ardından **görünümü kodu**.</span><span class="sxs-lookup"><span data-stu-id="978dd-279">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="978dd-280">Merhaba SSPlayer ad alanı içinde yeni bir sınıf ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-280">Inside hello SSPlayer namespace, add a new class:</span></span>
   
        #region class Stream
   
        public class Stream
        {
            private IManifestStream stream;
            public bool isCheckedValue;
            public string name;
   
            public string Name
            {
                get { return name; }
                set { name = value; }
            }
   
            public IManifestStream ManifestStream
            {
                get { return stream; }
                set { stream = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    // mMke hello video stream always checked.
                    if (stream.Type == MediaStreamType.Video)
                    {
                        isCheckedValue = true;
                    }
                    else
                    {
                        isCheckedValue = value;
                    }
                }
            }
   
            public Stream(IManifestStream streamIn)
            {
                stream = streamIn;
                name = stream.Name;
            }
        }
        #endregion class Stream
3. <span data-ttu-id="978dd-281">Merhaba MainPage sınıfı Hello başında değişken tanımları aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-281">At hello beginning of hello MainPage class, add hello following variable definitions:</span></span>
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. <span data-ttu-id="978dd-282">Merhaba MainPage sınıfı içinde bölge aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-282">Inside hello MainPage class, add hello following region:</span></span>
   
        #region stream selection
        ///<summary>
        ///Functionality tooselect streams from IManifestStream available streams
        /// </summary>
   
        // This function is called from hello mediaElement_ManifestReady event handler 
        // tooretrieve hello streams and populate them toohello local data members.
        public void getStreams(Manifest manifestObject)
        {
            availableStreams = new List<Stream>();
            availableVideoStreams = new List<Stream>();
            availableAudioStreams = new List<Stream>();
            availableTextStreams = new List<Stream>();
   
            try
            {
                for (int i = 0; i<manifestObject.AvailableStreams.Count; i++)
                {
                    Stream newStream = new Stream(manifestObject.AvailableStreams[i]);
                    newStream.isChecked = false;
   
                    //populate hello stream lists based on hello types
                    availableStreams.Add(newStream);
   
                    switch (newStream.ManifestStream.Type)
                    {
                        case MediaStreamType.Video:
                            availableVideoStreams.Add(newStream);
                            break;
                        case MediaStreamType.Audio:
                            availableAudioStreams.Add(newStream);
                            break;
                        case MediaStreamType.Text:
                            availableTextStreams.Add(newStream);
                            break;
                    }
   
                    // Select hello default selected streams from hello manifest.
                    for (int j = 0; j<manifestObject.SelectedStreams.Count; j++)
                    {
                        string selectedStreamName = manifestObject.SelectedStreams[j].Name;
                        if (selectedStreamName.Equals(newStream.Name))
                        {
                            newStream.isChecked = true;
                            break;
                        }
                    }
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function set hello list box ItemSource
        private async void refreshAvailableStreamsListBoxItemSource()
        {
            try
            {
                //update hello stream check box list on hello UI
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableStreams.ItemsSource = availableStreams; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function creates a selected streams list
        private void createSelectedStreamsList(List<IManifestStream> selectedStreams)
        {
            bool isOneVideoSelected = false;
            bool isOneAudioSelected = false;
   
            // Only one video stream can be selected
            for (int j = 0; j<availableVideoStreams.Count; j++)
            {
                if (availableVideoStreams[j].isChecked && (!isOneVideoSelected))
                {
                    selectedStreams.Add(availableVideoStreams[j].ManifestStream);
                    isOneVideoSelected = true;
                }
            }
   
            // Select hello frist video stream from hello list if no video stream is selected
            if (!isOneVideoSelected)
            {
                availableVideoStreams[0].isChecked = true;
                selectedStreams.Add(availableVideoStreams[0].ManifestStream);
            }
   
            // Only one audio stream can be selected
            for (int j = 0; j<availableAudioStreams.Count; j++)
            {
                if (availableAudioStreams[j].isChecked && (!isOneAudioSelected))
                {
                    selectedStreams.Add(availableAudioStreams[j].ManifestStream);
                    isOneAudioSelected = true;
                    txtStatus.Text = "hello audio stream is changed too" + availableAudioStreams[j].ManifestStream.Name;
                }
            }
   
            // Select hello frist audio stream from hello list if no audio steam is selected.
            if (!isOneAudioSelected)
            {
                availableAudioStreams[0].isChecked = true;
                selectedStreams.Add(availableAudioStreams[0].ManifestStream);
            }
   
            // Multiple text streams are supported.
            for (int j = 0; j < availableTextStreams.Count; j++)
            {
                if (availableTextStreams[j].isChecked)
                {
                    selectedStreams.Add(availableTextStreams[j].ManifestStream);
                }
            }
        }
   
        // Change streams on a smooth streaming presentation with multiple video streams.
        private async void changeStreams(List<IManifestStream> selectStreams)
        {
            try
            {
                IReadOnlyList<IStreamChangedResult> returnArgs =
                    await manifestObject.SelectStreamsAsync(selectStreams);
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
        #endregion stream selection
5. <span data-ttu-id="978dd-283">Merhaba mediaElement_ManifestReady yöntemini bulun, hello işlevi hello sonunda koddan hello Ekle:</span><span class="sxs-lookup"><span data-stu-id="978dd-283">Locate hello mediaElement_ManifestReady method, append hello following code at hello end of hello function:</span></span>
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    <span data-ttu-id="978dd-284">Bu nedenle MediaElement bildirimi hazır olduğunda, hello kod hello kullanılabilir akışları listesini alır ve hello UI liste kutusu hello listesi ile doldurur.</span><span class="sxs-lookup"><span data-stu-id="978dd-284">So when MediaElement manifest is ready, hello code gets a list of hello available streams, and populates hello UI list box with hello list.</span></span>
6. <span data-ttu-id="978dd-285">Merhaba MainPage sınıfı içinde bulun hello UI düğmeleri olayları bölge'ye tıklayın ve ardından işlev tanımı aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-285">Inside hello MainPage class, locate hello UI buttons click events region, and then add hello following function definition:</span></span>
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on hello presentation
            changeStreams(selectedStreams);
        }

<span data-ttu-id="978dd-286">**toocompile ve test Merhaba uygulaması**</span><span class="sxs-lookup"><span data-stu-id="978dd-286">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="978dd-287">Tuşuna **F6** toocompile hello projesi.</span><span class="sxs-lookup"><span data-stu-id="978dd-287">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="978dd-288">Tuşuna **F5** toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="978dd-288">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="978dd-289">Merhaba uygulaması Hello üstünde hello varsayılan kesintisiz akış URL'sini kullanabilir veya farklı bir tane girin.</span><span class="sxs-lookup"><span data-stu-id="978dd-289">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="978dd-290">Tıklatın **ayarlamak kaynak**.</span><span class="sxs-lookup"><span data-stu-id="978dd-290">Click **Set Source**.</span></span> 
5. <span data-ttu-id="978dd-291">Merhaba varsayılan audio_eng dilidir.</span><span class="sxs-lookup"><span data-stu-id="978dd-291">hello default language is audio_eng.</span></span> <span data-ttu-id="978dd-292">Tooswitch audio_eng audio_es arasındaki deneyin.</span><span class="sxs-lookup"><span data-stu-id="978dd-292">Try tooswitch between audio_eng and audio_es.</span></span> <span data-ttu-id="978dd-293">Her, yeni bir akış seçin, hello gönder düğmesine tıklamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="978dd-293">Everytime, you select a new stream, you must click hello Submit button.</span></span>

<span data-ttu-id="978dd-294">Ders 3 tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="978dd-294">You have completed lesson 3.</span></span>  <span data-ttu-id="978dd-295">Bu alıştırmanın ilerisinde hello işlevselliği toochoose akışlar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="978dd-295">In this lesson, you add hello functionality toochoose streams.</span></span>

## <a name="lesson-4-select-smooth-streaming-tracks"></a><span data-ttu-id="978dd-296">Ders 4: Kesintisiz akış parçaları seçin</span><span class="sxs-lookup"><span data-stu-id="978dd-296">Lesson 4: Select Smooth Streaming Tracks</span></span>
<span data-ttu-id="978dd-297">Kesintisiz akış sunu farklı kalite düzeyleri (bit hızları) ve çözümlemeleri ile kodlanmış birden çok video dosyaları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="978dd-297">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span></span> <span data-ttu-id="978dd-298">Bu ders, kullanıcıların tooselect parçaları olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="978dd-298">In this lesson, you will enable users tooselect tracks.</span></span> <span data-ttu-id="978dd-299">Bu ders hello yordamları içerir:</span><span class="sxs-lookup"><span data-stu-id="978dd-299">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="978dd-300">Merhaba XAML dosyasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="978dd-300">Modify hello XAML file</span></span>
2. <span data-ttu-id="978dd-301">Merhaba kod behand dosyasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="978dd-301">Modify hello code behand file</span></span>
3. <span data-ttu-id="978dd-302">Derleme ve hello uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="978dd-302">Compile and test hello application</span></span>

<span data-ttu-id="978dd-303">**toomodify hello XAML dosyası**</span><span class="sxs-lookup"><span data-stu-id="978dd-303">**toomodify hello XAML file**</span></span>

1. <span data-ttu-id="978dd-304">Çözüm Gezgini'nden sağ **MainPage.xaml**ve ardından **Görünüm Tasarımcısı**.</span><span class="sxs-lookup"><span data-stu-id="978dd-304">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="978dd-305">Merhaba bulun &lt;kılavuz&gt; hello adı etiketiyle **gridStreamAndBitrateSelection**, hello etiketi hello sonunda koddan hello Ekle:</span><span class="sxs-lookup"><span data-stu-id="978dd-305">Locate hello &lt;Grid&gt; tag with hello name **gridStreamAndBitrateSelection**, append hello following code at hello end of hello tag:</span></span>
   
         <StackPanel Name="spBitRateSelection" Grid.Row="1" Grid.Column="1">
         <StackPanel Orientation="Horizontal">
             <TextBlock Name="tbBitRate" Text="Available Bitrates:" FontSize="16" VerticalAlignment="Center"/>
             <Button Name="btnChangeTracks" Content="Submit" Click="btnChangeTrack_Click" />
         </StackPanel>
         <ListBox x:Name="lbAvailableVideoTracks" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                  ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
             <ListBox.ItemTemplate>
                 <DataTemplate>
                     <CheckBox Content="{Binding Bitrate}" IsChecked="{Binding isChecked, Mode=TwoWay}"/>
                 </DataTemplate>
             </ListBox.ItemTemplate>
         </ListBox>
         </StackPanel>
3. <span data-ttu-id="978dd-306">Tuşuna **CTRL + S** toosave kendisinin değiştirir</span><span class="sxs-lookup"><span data-stu-id="978dd-306">Press **CTRL+S** toosave he changes</span></span>

<span data-ttu-id="978dd-307">**dosyanın arkasındaki toomodify hello kodu**</span><span class="sxs-lookup"><span data-stu-id="978dd-307">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="978dd-308">Çözüm Gezgini'nden sağ **MainPage.xaml**ve ardından **görünümü kodu**.</span><span class="sxs-lookup"><span data-stu-id="978dd-308">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="978dd-309">Merhaba SSPlayer ad alanı içinde yeni bir sınıf ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-309">Inside hello SSPlayer namespace, add a new class:</span></span>
   
        #region class Track
        public class Track
        {
            private IManifestTrack trackInfo;
            public string _bitrate;
            public bool isCheckedValue;
   
            public IManifestTrack TrackInfo
            {
                get { return trackInfo; }
                set { trackInfo = value; }
            }
   
            public string Bitrate
            {
                get { return _bitrate; }
                set { _bitrate = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    isCheckedValue = value;
                }
            }
   
            public Track(IManifestTrack trackInfoIn)
            {
                trackInfo = trackInfoIn;
                _bitrate = trackInfoIn.Bitrate.ToString();
            }
            //public Track() { }
        }
        #endregion class Track
3. <span data-ttu-id="978dd-310">Merhaba MainPage sınıfı Hello başında değişken tanımları aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-310">At hello beginning of hello MainPage class, add hello following variable definitions:</span></span>
   
        private List<Track> availableTracks;
4. <span data-ttu-id="978dd-311">Merhaba MainPage sınıfı içinde bölge aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-311">Inside hello MainPage class, add hello following region:</span></span>
   
        #region track selection
        /// <summary>
        /// Functionality tooselect video streams
        /// </summary>
   
        /// This Function gets hello tracks for hello selected video stream
        public void getTracks(Manifest manifestObject)
        {
            availableTracks = new List<Track>();
   
            IManifestStream videoStream = getVideoStream();
            IReadOnlyList<IManifestTrack> availableTracksLocal = videoStream.AvailableTracks;
            IReadOnlyList<IManifestTrack> selectedTracksLocal = videoStream.SelectedTracks;
   
            try
            {
                for (int i = 0; i < availableTracksLocal.Count; i++)
                {
                    Track thisTrack = new Track(availableTracksLocal[i]);
                    thisTrack.isChecked = true;
   
                    for (int j = 0; j < selectedTracksLocal.Count; j++)
                    {
                        string selectedTrackName = selectedTracksLocal[j].Bitrate.ToString();
                        if (selectedTrackName.Equals(thisTrack.Bitrate))
                        {
                            thisTrack.isChecked = true;
                            break;
                        }
                    }
                    availableTracks.Add(thisTrack);
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = e.Message;
            }
        }
   
        // This function gets hello video stream that is playing
        private IManifestStream getVideoStream()
        {
            IManifestStream videoStream = null;
            for (int i = 0; i < manifestObject.SelectedStreams.Count; i++)
            {
                if (manifestObject.SelectedStreams[i].Type == MediaStreamType.Video)
                {
                    videoStream = manifestObject.SelectedStreams[i];
                    break;
                }
            }
            return videoStream;
        }
   
        // This function set hello UI list box control ItemSource
        private async void refreshAvailableTracksListBoxItemSource()
        {
            try
            {
                // Update hello track check box list on hello UI 
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableVideoTracks.ItemsSource = availableTracks; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }        
        }
   
        // This function creates a list of hello selected tracks.
        private void createSelectedTracksList(List<IManifestTrack> selectedTracks)
        {
            // Create a list of selected tracks
            for (int j = 0; j < availableTracks.Count; j++)
            {
                if (availableTracks[j].isCheckedValue == true)
                {
                    selectedTracks.Add(availableTracks[j].TrackInfo);
                }
            }
        }
   
        // This function selects hello tracks based on user selection 
        private void changeTracks(List<IManifestTrack> selectedTracks)
        {
            IManifestStream videoStream = getVideoStream();
            try
            {
                videoStream.SelectTracks(selectedTracks);
            }
            catch (Exception ex)
            {
                txtStatus.Text = ex.Message;
            }
        }
        #endregion track selection
5. <span data-ttu-id="978dd-312">Merhaba mediaElement_ManifestReady yöntemini bulun, hello işlevi hello sonunda koddan hello Ekle:</span><span class="sxs-lookup"><span data-stu-id="978dd-312">Locate hello mediaElement_ManifestReady method, append hello following code at hello end of hello function:</span></span>
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. <span data-ttu-id="978dd-313">Merhaba MainPage sınıfı içinde bulun hello UI düğmeleri olayları bölge'ye tıklayın ve ardından işlev tanımı aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="978dd-313">Inside hello MainPage class, locate hello UI buttons click events region, and then add hello following function definition:</span></span>
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on hello presentation
            changeStreams(selectedStreams);
         }

<span data-ttu-id="978dd-314">**toocompile ve test Merhaba uygulaması**</span><span class="sxs-lookup"><span data-stu-id="978dd-314">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="978dd-315">Tuşuna **F6** toocompile hello projesi.</span><span class="sxs-lookup"><span data-stu-id="978dd-315">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="978dd-316">Tuşuna **F5** toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="978dd-316">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="978dd-317">Merhaba uygulaması Hello üstünde hello varsayılan kesintisiz akış URL'sini kullanabilir veya farklı bir tane girin.</span><span class="sxs-lookup"><span data-stu-id="978dd-317">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="978dd-318">Tıklatın **ayarlamak kaynak**.</span><span class="sxs-lookup"><span data-stu-id="978dd-318">Click **Set Source**.</span></span> 
5. <span data-ttu-id="978dd-319">Varsayılan olarak, tüm hello video akışına hello parçalarının seçilir.</span><span class="sxs-lookup"><span data-stu-id="978dd-319">By default, all of hello tracks of hello video stream are selected.</span></span> <span data-ttu-id="978dd-320">tooexperiment hello bit hızı değişiklikleri, hello düşük bit hızı kullanılabilir seçin ve ardından hello yüksek bit hızı kullanılabilir seçin.</span><span class="sxs-lookup"><span data-stu-id="978dd-320">tooexperiment hello bit rate changes, you can select hello lowest bit rate available, and then select hello highest bit rate available.</span></span> <span data-ttu-id="978dd-321">Her bir değişiklikten sonra Gönder'i tıklatmalısınız.</span><span class="sxs-lookup"><span data-stu-id="978dd-321">You must click Submit after each change.</span></span>  <span data-ttu-id="978dd-322">Merhaba video kalitesini değişiklikleri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="978dd-322">You can see hello video quality changes.</span></span>

<span data-ttu-id="978dd-323">Ders 4 tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="978dd-323">You have completed lesson 4.</span></span>  <span data-ttu-id="978dd-324">Bu alıştırmanın ilerisinde hello işlevselliği toochoose parçaları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="978dd-324">In this lesson, you add hello functionality toochoose tracks.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="978dd-325">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="978dd-325">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="978dd-326">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="978dd-326">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a><span data-ttu-id="978dd-327">Diğer kaynaklar:</span><span class="sxs-lookup"><span data-stu-id="978dd-327">Other Resources:</span></span>
* [<span data-ttu-id="978dd-328">Toobuild nasıl Gelişmiş Özellikler ileri bir kesintisiz akış Windows 8 JavaScript uygulaması ile</span><span class="sxs-lookup"><span data-stu-id="978dd-328">How toobuild a Smooth Streaming Windows 8 JavaScript application with advanced features</span></span>](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [<span data-ttu-id="978dd-329">Kesintisiz akış teknik genel bakış</span><span class="sxs-lookup"><span data-stu-id="978dd-329">Smooth Streaming Technical Overview</span></span>](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

