---
title: "Kesintisiz akış Windows mağazası uygulaması Öğreticisi | Microsoft Docs"
description: "Bir C# Windows mağazası uygulaması, kesintisiz akışı kayıttan yürütme için XML MediaElement denetimi ile içerik oluşturmak için Azure Media Services kullanmayı öğrenin."
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
ms.openlocfilehash: c9bb3b1915543fea3561cb309f55c4e8a74ded6d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-build-a-smooth-streaming-windows-store-application"></a><span data-ttu-id="21eb2-103">Windows mağazası uygulama akışı düzgün oluşturma</span><span class="sxs-lookup"><span data-stu-id="21eb2-103">How to Build a Smooth Streaming Windows Store Application</span></span>

<span data-ttu-id="21eb2-104">Kesintisiz akış istemci SDK Windows 8 için isteğe bağlı ve canlı kesintisiz akış içeriği yürütmek Windows mağazası uygulamaları geliştiricilerin oluşturmalarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="21eb2-104">The Smooth Streaming Client SDK for Windows 8 enables developers to build Windows Store applications that can play on-demand and live Smooth Streaming content.</span></span> <span data-ttu-id="21eb2-105">Ek olarak temel kayıttan kesintisiz akış içeriğinin SDK Microsoft PlayReady koruma, kalite düzeyi kısıtlama, Canlı DVR, geçiş, durum güncelleştirmeleri (kalite düzeyi değişiklikleri gibi) için dinleme ses akışı gibi zengin özellikleri de sağlar ve hata olayları ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="21eb2-105">In addition to the basic playback of Smooth Streaming content, the SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span></span> <span data-ttu-id="21eb2-106">Desteklenen özellikler daha fazla bilgi için bkz: [sürüm notları](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span><span class="sxs-lookup"><span data-stu-id="21eb2-106">For more information of the supported features, see the [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span></span> <span data-ttu-id="21eb2-107">Daha fazla bilgi için bkz: [Windows 8 için Player Framework](http://playerframework.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="21eb2-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span></span> 

<span data-ttu-id="21eb2-108">Bu öğretici dört dersleri içerir:</span><span class="sxs-lookup"><span data-stu-id="21eb2-108">This tutorial contains four lessons:</span></span>

1. <span data-ttu-id="21eb2-109">Bir temel kesintisiz akış depolama uygulaması oluştur</span><span class="sxs-lookup"><span data-stu-id="21eb2-109">Create a Basic Smooth Streaming Store Application</span></span>
2. <span data-ttu-id="21eb2-110">Medya ilerleme durumunu denetlemek için bir kaydırıcı çubuğu ekleme</span><span class="sxs-lookup"><span data-stu-id="21eb2-110">Add a Slider Bar to Control the Media Progress</span></span>
3. <span data-ttu-id="21eb2-111">Kesintisiz akış akışları seçin</span><span class="sxs-lookup"><span data-stu-id="21eb2-111">Select Smooth Streaming Streams</span></span>
4. <span data-ttu-id="21eb2-112">Kesintisiz akış parçaları seçin</span><span class="sxs-lookup"><span data-stu-id="21eb2-112">Select Smooth Streaming Tracks</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21eb2-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="21eb2-113">Prerequisites</span></span>
* <span data-ttu-id="21eb2-114">Windows 8 32 bit veya 64-bit.</span><span class="sxs-lookup"><span data-stu-id="21eb2-114">Windows 8 32-bit or 64-bit.</span></span> <span data-ttu-id="21eb2-115">Alma [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) MSDN'den.</span><span class="sxs-lookup"><span data-stu-id="21eb2-115">You can get [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) from MSDN.</span></span>
* <span data-ttu-id="21eb2-116">Visual Studio 2012 veya Visual Studio Express 2012 (veya sonraki bir sürümünü).</span><span class="sxs-lookup"><span data-stu-id="21eb2-116">Visual Studio 2012 or Visual Studio Express 2012 (or a later version).</span></span> <span data-ttu-id="21eb2-117">Deneme sürümünden alabilirsiniz [burada](http://www.microsoft.com/visualstudio/11/downloads).</span><span class="sxs-lookup"><span data-stu-id="21eb2-117">You can get the trial version from [here](http://www.microsoft.com/visualstudio/11/downloads).</span></span>
* <span data-ttu-id="21eb2-118">[Microsoft Windows 8 için İstemci SDK akış kesintisiz](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span><span class="sxs-lookup"><span data-stu-id="21eb2-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span></span>

<span data-ttu-id="21eb2-119">Tamamlanan çözümü her ders için MSDN Geliştirici kod örneklerini (kod Galerisi) indirilebilir:</span><span class="sxs-lookup"><span data-stu-id="21eb2-119">The completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span></span> 

* <span data-ttu-id="21eb2-120">[Ders 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - Media Player, akış basit Windows 8 kesintisiz</span><span class="sxs-lookup"><span data-stu-id="21eb2-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span></span> 
* <span data-ttu-id="21eb2-121">[Ders 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - basit Windows 8 düzgün Media Player kaydırıcı çubuğun ile akış denetimi</span><span class="sxs-lookup"><span data-stu-id="21eb2-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span></span> 
* <span data-ttu-id="21eb2-122">[Ders 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - bir Windows 8 kesintisiz akış seçimi ile Media Player akış</span><span class="sxs-lookup"><span data-stu-id="21eb2-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span></span>  
* <span data-ttu-id="21eb2-123">[Ders 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) - Media Player izleme seçimi ile akış Windows 8 düzgün.</span><span class="sxs-lookup"><span data-stu-id="21eb2-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span></span>

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a><span data-ttu-id="21eb2-124">Ders 1: temel bir kesintisiz akış mağazası uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="21eb2-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span></span>

<span data-ttu-id="21eb2-125">Bu ders içinde bir Windows mağazası uygulaması kesintisiz akış yürütmek için MediaElement denetimi içerik oluşturur.</span><span class="sxs-lookup"><span data-stu-id="21eb2-125">In this lesson, you will create a Windows Store application with a MediaElement control to play Smooth Stream content.</span></span>  <span data-ttu-id="21eb2-126">Çalışan uygulama şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="21eb2-126">The running application looks like:</span></span>

![Kesintisiz akış Windows mağazası uygulama örneği][PlayerApplication]

<span data-ttu-id="21eb2-128">Windows mağazası uygulaması geliştirme hakkında daha fazla bilgi için bkz: [geliştirmek harika uygulamaları Windows 8 için](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span><span class="sxs-lookup"><span data-stu-id="21eb2-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span></span> <span data-ttu-id="21eb2-129">Bu ders aşağıdaki yordamları içerir:</span><span class="sxs-lookup"><span data-stu-id="21eb2-129">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="21eb2-130">Bir Windows mağazası projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="21eb2-130">Create a Windows Store project</span></span>
2. <span data-ttu-id="21eb2-131">Tasarım kullanıcı arabirimi (XAML)</span><span class="sxs-lookup"><span data-stu-id="21eb2-131">Design the user interface (XAML)</span></span>
3. <span data-ttu-id="21eb2-132">Dosyanın arkasındaki kodu değiştirin</span><span class="sxs-lookup"><span data-stu-id="21eb2-132">Modify the code behind file</span></span>
4. <span data-ttu-id="21eb2-133">Derleme ve uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="21eb2-133">Compile and test the application</span></span>

<span data-ttu-id="21eb2-134">**Bir Windows mağazası projesi oluşturmak için**</span><span class="sxs-lookup"><span data-stu-id="21eb2-134">**To create a Windows Store project**</span></span>

1. <span data-ttu-id="21eb2-135">Visual Studio 2012 veya sonraki sürümünü çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="21eb2-135">Run Visual Studio 2012 or later.</span></span>
2. <span data-ttu-id="21eb2-136">**DOSYA** menüsünde **Yeni**’ye ve sonra **Proje**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="21eb2-136">From the **FILE** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="21eb2-137">Yeni Proje iletişim kutusundan yazın veya aşağıdaki değerleri seçin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-137">From the New Project dialog, type or select  the following values:</span></span>

| <span data-ttu-id="21eb2-138">Ad</span><span class="sxs-lookup"><span data-stu-id="21eb2-138">Name</span></span> | <span data-ttu-id="21eb2-139">Değer</span><span class="sxs-lookup"><span data-stu-id="21eb2-139">Value</span></span> |
| --- | --- |
| <span data-ttu-id="21eb2-140">Şablon grubu</span><span class="sxs-lookup"><span data-stu-id="21eb2-140">Template group</span></span> |<span data-ttu-id="21eb2-141">Yüklü/Şablonlar/Visual C# / Windows Mağazası</span><span class="sxs-lookup"><span data-stu-id="21eb2-141">Installed/Templates/Visual C#/Windows Store</span></span> |
| <span data-ttu-id="21eb2-142">Şablon</span><span class="sxs-lookup"><span data-stu-id="21eb2-142">Template</span></span> |<span data-ttu-id="21eb2-143">Boş uygulama (XAML)</span><span class="sxs-lookup"><span data-stu-id="21eb2-143">Blank App (XAML)</span></span> |
| <span data-ttu-id="21eb2-144">Ad</span><span class="sxs-lookup"><span data-stu-id="21eb2-144">Name</span></span> |<span data-ttu-id="21eb2-145">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="21eb2-145">SSPlayer</span></span> |
| <span data-ttu-id="21eb2-146">Konum</span><span class="sxs-lookup"><span data-stu-id="21eb2-146">Location</span></span> |<span data-ttu-id="21eb2-147">C:\SSTutorials</span><span class="sxs-lookup"><span data-stu-id="21eb2-147">C:\SSTutorials</span></span> |
| <span data-ttu-id="21eb2-148">Çözüm adı</span><span class="sxs-lookup"><span data-stu-id="21eb2-148">Solution Name</span></span> |<span data-ttu-id="21eb2-149">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="21eb2-149">SSPlayer</span></span> |
| <span data-ttu-id="21eb2-150">Çözüm için dizin oluşturun</span><span class="sxs-lookup"><span data-stu-id="21eb2-150">Create directory for solution</span></span> |<span data-ttu-id="21eb2-151">(Seçili)</span><span class="sxs-lookup"><span data-stu-id="21eb2-151">(selected)</span></span> |

1. <span data-ttu-id="21eb2-152">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="21eb2-152">Click **OK**.</span></span>

<span data-ttu-id="21eb2-153">**Kesintisiz akış istemci SDK'sına bir başvuru eklemek için**</span><span class="sxs-lookup"><span data-stu-id="21eb2-153">**To add a reference to the Smooth Streaming Client SDK**</span></span>

1. <span data-ttu-id="21eb2-154">Çözüm Gezgini'nden sağ **SSPlayer**ve ardından **Başvuru Ekle**.</span><span class="sxs-lookup"><span data-stu-id="21eb2-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span></span>
2. <span data-ttu-id="21eb2-155">Aşağıdaki değerleri yazın veya seçin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-155">Type or select the following values:</span></span>

| <span data-ttu-id="21eb2-156">Ad</span><span class="sxs-lookup"><span data-stu-id="21eb2-156">Name</span></span> | <span data-ttu-id="21eb2-157">Değer</span><span class="sxs-lookup"><span data-stu-id="21eb2-157">Value</span></span> |
| --- | --- |
| <span data-ttu-id="21eb2-158">Başvuru grubu</span><span class="sxs-lookup"><span data-stu-id="21eb2-158">Reference group</span></span> |<span data-ttu-id="21eb2-159">Windows/uzantıları</span><span class="sxs-lookup"><span data-stu-id="21eb2-159">Windows/Extensions</span></span> |
| <span data-ttu-id="21eb2-160">Başvuru</span><span class="sxs-lookup"><span data-stu-id="21eb2-160">Reference</span></span> |<span data-ttu-id="21eb2-161">Microsoft Windows 8 ve Microsoft Visual C++ çalışma zamanı paketi için İstemci SDK akış kesintisiz seçin</span><span class="sxs-lookup"><span data-stu-id="21eb2-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span></span> |

1. <span data-ttu-id="21eb2-162">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="21eb2-162">Click **OK**.</span></span> 

<span data-ttu-id="21eb2-163">Başvuruları ekledikten sonra hedeflenen bir platform (x64 veya x86) seçmeniz gerekir, ekleyerek başvuruları için herhangi bir CPU platform yapılandırması çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="21eb2-163">After adding the references, you must select the targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span></span>  <span data-ttu-id="21eb2-164">Çözüm Gezgini'nde, sarı renkli uyarı işareti bu başvurular eklenen görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="21eb2-164">In solution explorer, you will see yellow warning mark for these added references.</span></span>

<span data-ttu-id="21eb2-165">**Tasarım player kullanıcı arabirimi**</span><span class="sxs-lookup"><span data-stu-id="21eb2-165">**To design the player user interface**</span></span>

1. <span data-ttu-id="21eb2-166">Çözüm Gezgini'nde, çift tıklayarak **MainPage.xaml** Tasarım görünümünde açın.</span><span class="sxs-lookup"><span data-stu-id="21eb2-166">From Solution Explorer, double click **MainPage.xaml** to open it in the design view.</span></span>
2. <span data-ttu-id="21eb2-167">Bulun  **&lt;kılavuz&gt;**  ve  **&lt;/Grid&gt;**  XAML dosyası etiketleri ve iki etiketleri arasına aşağıdaki kodu yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="21eb2-167">Locate the **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags the XAML file, and paste the following code between the two tags:</span></span>

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
   
   <span data-ttu-id="21eb2-168">MediaElement denetimi kayıttan yürütme ortamı için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21eb2-168">The MediaElement control is used to playback media.</span></span> <span data-ttu-id="21eb2-169">SliderProgress adlı kaydırıcı denetimi sonraki Ders medya ilerleme durumunu denetlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21eb2-169">The slider control named sliderProgress will be used in the next lesson to control the media progress.</span></span>
3. <span data-ttu-id="21eb2-170">Tuşuna **CTRL + S** dosyayı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="21eb2-170">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="21eb2-171">MediaElement denetimi kesintisiz akış içerik out-of-box desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="21eb2-171">The MediaElement control does not support Smooth Streaming content out-of-box.</span></span> <span data-ttu-id="21eb2-172">Kesintisiz akış desteğini etkinleştirmek için dosya adı uzantısı ve MIME türüne göre kesintisiz akış bayt akışı işleyici kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="21eb2-172">To enable the Smooth Streaming support, you must register the Smooth Streaming byte-stream handler by file name extension and MIME type.</span></span>  <span data-ttu-id="21eb2-173">Kaydetmek için Windows.Media ad MediaExtensionManager.RegisterByteStremHandler yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="21eb2-173">To register, you use the MediaExtensionManager.RegisterByteStremHandler method of the Windows.Media namespace.</span></span>

<span data-ttu-id="21eb2-174">Bu XAML dosyası içinde bazı olay işleyicileri denetimleri ile ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="21eb2-174">In this XAML file, some event handlers are associated with the controls.</span></span>  <span data-ttu-id="21eb2-175">Bu olay işleyicileri tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="21eb2-175">You must define those event handlers.</span></span>

<span data-ttu-id="21eb2-176">**Dosyanın arkasındaki kod değiştirmek için**</span><span class="sxs-lookup"><span data-stu-id="21eb2-176">**To modify the code behind file**</span></span>

1. <span data-ttu-id="21eb2-177">Çözüm Gezgini'nden sağ **MainPage.xaml**ve ardından **görünümü kodu**.</span><span class="sxs-lookup"><span data-stu-id="21eb2-177">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="21eb2-178">Dosyanın üst kısmında, aşağıdaki ekleme deyimini kullanarak:</span><span class="sxs-lookup"><span data-stu-id="21eb2-178">At the top of the file, add the following using statement:</span></span>
   
        using Windows.Media;
3. <span data-ttu-id="21eb2-179">Başında **MainPage** sınıfı, aşağıdaki veri üyesi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-179">At the beginning of the **MainPage** class, add the following data member:</span></span>
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. <span data-ttu-id="21eb2-180">Sonunda **MainPage** oluşturucusu, aşağıdaki iki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-180">At the end of the **MainPage** constructor, add the following two lines:</span></span>
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. <span data-ttu-id="21eb2-181">Sonunda **MainPage** sınıfında, aşağıdaki kodu yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="21eb2-181">At the end of the **MainPage** class, paste the following code:</span></span>
   
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
             txtStatus.Text = "Click the Play button to play the media source.";
         }
         }
         private void btnStop_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Stop();
         txtStatus.Text = "MediaElement is stopped";
         }
         private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)
         {

         txtStatus.Text = "Seek to position " + sliderProgress.Value;
         mediaElement.Position = new TimeSpan(0, 0, (int)(sliderProgress.Value));
         }
         # endregion

<span data-ttu-id="21eb2-182">SliderProgress_PointerPressed olay işleyicisi burada belirtilir.</span><span class="sxs-lookup"><span data-stu-id="21eb2-182">The sliderProgress_PointerPressed event handler is defined here.</span></span>  <span data-ttu-id="21eb2-183">Bu öğreticinin sonraki Ders içinde ele çalışma edinilir yapmak için daha fazla works vardır.</span><span class="sxs-lookup"><span data-stu-id="21eb2-183">There are more works to do to get it working, which will be covered in the next lesson of this tutorial.</span></span>
6. <span data-ttu-id="21eb2-184">Tuşuna **CTRL + S** dosyayı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="21eb2-184">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="21eb2-185">Tamamlanmış dosyanın arkasındaki kod şöyle:</span><span class="sxs-lookup"><span data-stu-id="21eb2-185">The finished the code behind file shall look like this:</span></span>

![Visual Studio, kesintisiz akış Windows mağazası uygulamasında Codeview][CodeViewPic]

<span data-ttu-id="21eb2-187">**Derleme ve uygulamayı test etme**</span><span class="sxs-lookup"><span data-stu-id="21eb2-187">**To compile and test the application**</span></span>

1. <span data-ttu-id="21eb2-188">Gelen **yapı** menüsünde tıklatın **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="21eb2-188">From the **BUILD** menu, click **Configuration Manager**.</span></span>
2. <span data-ttu-id="21eb2-189">Değişiklik **etkin çözüm platformu** geliştirme platformu eşleşecek şekilde.</span><span class="sxs-lookup"><span data-stu-id="21eb2-189">Change **Active solution platform** to match your development platform.</span></span>
3. <span data-ttu-id="21eb2-190">Tuşuna **F6** Projeyi derlemek için.</span><span class="sxs-lookup"><span data-stu-id="21eb2-190">Press **F6** to compile the project.</span></span> 
4. <span data-ttu-id="21eb2-191">Uygulamayı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="21eb2-191">Press **F5** to run the application.</span></span>
5. <span data-ttu-id="21eb2-192">Uygulama üst kısmında, varsayılan kesintisiz akış URL'sini kullanabilir veya farklı bir tane girin.</span><span class="sxs-lookup"><span data-stu-id="21eb2-192">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
6. <span data-ttu-id="21eb2-193">Tıklatın **ayarlamak kaynak**.</span><span class="sxs-lookup"><span data-stu-id="21eb2-193">Click **Set Source**.</span></span> <span data-ttu-id="21eb2-194">Çünkü **Otomatik Yürüt** etkin varsayılan olarak, medyayı otomatik olarak yürütmek.</span><span class="sxs-lookup"><span data-stu-id="21eb2-194">Because **Auto Play** is enabled by default, the media shall play automatically.</span></span>  <span data-ttu-id="21eb2-195">Medya kullanarak denetleyebilirsiniz **Yürüt**, **duraklatma** ve **durdurmak** düğmeler.</span><span class="sxs-lookup"><span data-stu-id="21eb2-195">You can control the media using the **Play**, **Pause** and **Stop** buttons.</span></span>  <span data-ttu-id="21eb2-196">Dikey kaydırıcıyı kullanarak medya birimi kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21eb2-196">You can control the media volume using the vertical slider.</span></span>  <span data-ttu-id="21eb2-197">Ancak medya ilerleme durumunu denetlemek için yatay kaydırıcı tam henüz uygulanmadı.</span><span class="sxs-lookup"><span data-stu-id="21eb2-197">However the horizontal slider for controlling the media progress is not fully implemented yet.</span></span> 

<span data-ttu-id="21eb2-198">Lesson1 tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="21eb2-198">You have completed lesson1.</span></span>  <span data-ttu-id="21eb2-199">Bu ders, kesintisiz akış içeriği kayıttan yürütme için MediaElement denetimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="21eb2-199">In this lesson, you use a MediaElement control to playback Smooth Streaming content.</span></span>  <span data-ttu-id="21eb2-200">Sonraki Ders kesintisiz akış içeriğinin ilerleme durumunu denetlemek için kaydırıcıyı ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="21eb2-200">In the next lesson, you will add a slider to control the progress of the Smooth Streaming content.</span></span>

## <a name="lesson-2-add-a-slider-bar-to-control-the-media-progress"></a><span data-ttu-id="21eb2-201">Ders 2: Media ilerleme durumunu denetlemek için bir kaydırıcı çubuğun ekleme</span><span class="sxs-lookup"><span data-stu-id="21eb2-201">Lesson 2: Add a Slider Bar to Control the Media Progress</span></span>

<span data-ttu-id="21eb2-202">Ders 1'de, kesintisiz akış medya içeriği kayıttan yürütme MediaElement XAML denetimine sahip bir Windows mağazası uygulaması oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="21eb2-202">In lesson 1, you created a Windows Store application with a MediaElement XAML control to playback Smooth Streaming media content.</span></span>  <span data-ttu-id="21eb2-203">Başlatma, durdurma ve duraklatma gibi bazı temel media işlevleri gelir.</span><span class="sxs-lookup"><span data-stu-id="21eb2-203">It comes some basic media functions like start, stop and pause.</span></span>  <span data-ttu-id="21eb2-204">Bu ders, uygulamaya kaydırıcı çubuğu denetimi ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="21eb2-204">In this lesson, you will add a slider bar control to the application.</span></span>

<span data-ttu-id="21eb2-205">Bu öğreticide, MediaElement denetimi geçerli konumuna bağlı kaydırıcı konumunu güncelleştirmek için bir zamanlayıcı kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="21eb2-205">In this tutorial, we will use a timer to update the slider position based on the current position of the MediaElement control.</span></span>  <span data-ttu-id="21eb2-206">Kaydırıcı başlangıç ve bitiş de canlı içerik durumunda güncelleştirilmesi gerekiyor zaman.</span><span class="sxs-lookup"><span data-stu-id="21eb2-206">The slider start and end time also need to be updated in case of live content.</span></span>  <span data-ttu-id="21eb2-207">Bu, daha iyi Uyarlamalı kaynak güncelleştirme olayda işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="21eb2-207">This can be better handled in the adaptive source update event.</span></span>

<span data-ttu-id="21eb2-208">Medya kaynaklarına medya veri üreten nesneleridir.</span><span class="sxs-lookup"><span data-stu-id="21eb2-208">Media sources are objects that generate media data.</span></span>  <span data-ttu-id="21eb2-209">Kaynak Çözümleyici bir URL veya bayt akış alır ve bu içerik için uygun medya kaynağı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="21eb2-209">The source resolver takes a URL or byte stream and creates the appropriate media source for that content.</span></span>  <span data-ttu-id="21eb2-210">Kaynak çözümleyici medya kaynaklarına oluşturmak üzere uygulamalar için standart yoludur.</span><span class="sxs-lookup"><span data-stu-id="21eb2-210">The source resolver is the standard way for the applications to create media sources.</span></span> 

<span data-ttu-id="21eb2-211">Bu ders aşağıdaki yordamları içerir:</span><span class="sxs-lookup"><span data-stu-id="21eb2-211">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="21eb2-212">Kesintisiz akış işleyici kaydetme</span><span class="sxs-lookup"><span data-stu-id="21eb2-212">Register the Smooth Streaming handler</span></span> 
2. <span data-ttu-id="21eb2-213">Uyarlamalı Kaynak Yöneticisi düzeyi olay işleyicileri ekleme</span><span class="sxs-lookup"><span data-stu-id="21eb2-213">Add the adaptive source manager level event handlers</span></span>
3. <span data-ttu-id="21eb2-214">Uyarlamalı kaynak düzeyi olay işleyicileri ekleme</span><span class="sxs-lookup"><span data-stu-id="21eb2-214">Add the adaptive source level event handlers</span></span>
4. <span data-ttu-id="21eb2-215">MediaElement olay işleyicileri ekleme</span><span class="sxs-lookup"><span data-stu-id="21eb2-215">Add MediaElement event handlers</span></span>
5. <span data-ttu-id="21eb2-216">Kaydırma çubuğu ilgili kod ekleme</span><span class="sxs-lookup"><span data-stu-id="21eb2-216">Add slider bar related code</span></span>
6. <span data-ttu-id="21eb2-217">Derleme ve uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="21eb2-217">Compile and test the application</span></span>

<span data-ttu-id="21eb2-218">**Kesintisiz akış bayt akışı işleyici kaydetmek ve propertyset geçirmek için**</span><span class="sxs-lookup"><span data-stu-id="21eb2-218">**To register the Smooth Streaming byte-stream handler and pass the propertyset**</span></span>

1. <span data-ttu-id="21eb2-219">Çözüm Gezgini'nden sağ tıklayın **MainPage.xaml**ve ardından **görünümü kodu**.</span><span class="sxs-lookup"><span data-stu-id="21eb2-219">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="21eb2-220">Dosyanın başına aşağıdaki Ekle deyimi kullanarak:</span><span class="sxs-lookup"><span data-stu-id="21eb2-220">At the beginning of the file, add the following using statement:</span></span>

        using Microsoft.Media.AdaptiveStreaming;
3. <span data-ttu-id="21eb2-221">MainPage sınıfı başına aşağıdaki veri üyeleri Ekle:</span><span class="sxs-lookup"><span data-stu-id="21eb2-221">At the beginning of the MainPage class, add the following data members:</span></span>

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. <span data-ttu-id="21eb2-222">İçinde **MainPage** oluşturucusu, sonra aşağıdaki kodu ekleyin **bu. Components() başlatılamadı;**  satır ve kayıt kod önceki Ders yazılmış satırları:</span><span class="sxs-lookup"><span data-stu-id="21eb2-222">Inside the **MainPage** constructor, add the following code after the **this.Initialize Components();** line and the registration code lines written in the previous lesson:</span></span>

        // Gets the default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value to AdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. <span data-ttu-id="21eb2-223">İçinde **MainPage** oluşturucusunu eklemek için iki RegisterByteStreamHandler yöntem Değiştir İleri parametreleri:</span><span class="sxs-lookup"><span data-stu-id="21eb2-223">Inside the **MainPage** constructor, modify the two RegisterByteStreamHandler methods to add the forth parameters:</span></span>

         // Registers Smooth Streaming byte-stream handler for ".ism" extension and, 
         // "text/xml" and "application/vnd.ms-ss" mime-types and pass the propertyset. 
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
6. <span data-ttu-id="21eb2-224">Tuşuna **CTRL + S** dosyayı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="21eb2-224">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="21eb2-225">**Uyarlamalı Kaynak Yöneticisi düzeyi olay işleyicisi eklemek için**</span><span class="sxs-lookup"><span data-stu-id="21eb2-225">**To add the adaptive source manager level event handler**</span></span>

1. <span data-ttu-id="21eb2-226">Çözüm Gezgini'nden sağ tıklayın **MainPage.xaml**ve ardından **görünümü kodu**.</span><span class="sxs-lookup"><span data-stu-id="21eb2-226">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="21eb2-227">İçinde **MainPage** sınıfı, aşağıdaki veri üyesi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-227">Inside the **MainPage** class, add the following data member:</span></span>
   
     <span data-ttu-id="21eb2-228">Özel AdaptiveSource adaptiveSource = null;</span><span class="sxs-lookup"><span data-stu-id="21eb2-228">private AdaptiveSource adaptiveSource = null;</span></span>
3. <span data-ttu-id="21eb2-229">Sonunda **MainPage** sınıfı, aşağıdaki olay işleyicisini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-229">At the end of the **MainPage** class, add the following event handler:</span></span>
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. <span data-ttu-id="21eb2-230">Sonunda **MainPage** oluşturucusu, Uyarlamalı kaynak açık olaya abone olmak için aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-230">At the end of the **MainPage** constructor, add the following line to subscribe to the adaptive source open event:</span></span>
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. <span data-ttu-id="21eb2-231">Tuşuna **CTRL + S** dosyayı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="21eb2-231">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="21eb2-232">**Uyarlamalı kaynak düzeyi olay işleyicileri eklemek için**</span><span class="sxs-lookup"><span data-stu-id="21eb2-232">**To add adaptive source level event handlers**</span></span>

1. <span data-ttu-id="21eb2-233">Çözüm Gezgini'nden sağ tıklayın **MainPage.xaml**ve ardından **görünümü kodu**.</span><span class="sxs-lookup"><span data-stu-id="21eb2-233">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="21eb2-234">İçinde **MainPage** sınıfı, aşağıdaki veri üyesi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-234">Inside the **MainPage** class, add the following data member:</span></span>
   
     <span data-ttu-id="21eb2-235">Özel AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   Özel bildirim manifestObject;</span><span class="sxs-lookup"><span data-stu-id="21eb2-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span></span>
3. <span data-ttu-id="21eb2-236">Sonunda **MainPage** sınıfı, şu olay işleyicileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-236">At the end of the **MainPage** class, add the following event handlers:</span></span>

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
4. <span data-ttu-id="21eb2-237">Sonunda **mediaElement AdaptiveSourceOpened** yöntemi, olaylara abone olmak için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-237">At the end of the **mediaElement AdaptiveSourceOpened** method, add the following code to subscribe to the events:</span></span>
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. <span data-ttu-id="21eb2-238">Tuşuna **CTRL + S** dosyayı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="21eb2-238">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="21eb2-239">Aynı olaylar, uygulamadaki tüm ortam öğeleri için ortak işlevselliği işlemek için kullanılan Uyarlamalı kaynak yöneticisi düzeyinde de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="21eb2-239">The same events are available on Adaptive Source manger level as well, which can be used for handling functionality common to all media elements in the app.</span></span> <span data-ttu-id="21eb2-240">Tüm AdaptiveSource olayları AdaptiveSourceManager altında basamaklı ve her AdaptiveSource, kendi olaylarını içerir.</span><span class="sxs-lookup"><span data-stu-id="21eb2-240">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span></span>

<span data-ttu-id="21eb2-241">**Ortam öğesi olay işleyicileri ekleme**</span><span class="sxs-lookup"><span data-stu-id="21eb2-241">**To add Media Element event handlers**</span></span>

1. <span data-ttu-id="21eb2-242">Çözüm Gezgini'nden sağ tıklayın **MainPage.xaml**ve ardından **görünümü kodu**.</span><span class="sxs-lookup"><span data-stu-id="21eb2-242">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="21eb2-243">Sonunda **MainPage** sınıfı, şu olay işleyicileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-243">At the end of the **MainPage** class, add the following event handlers:</span></span>

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
3. <span data-ttu-id="21eb2-244">Sonunda **MainPage** oluşturucusu, alt simge olayları için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-244">At the end of the **MainPage** constructor, add the following code to subscript to the events:</span></span>

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. <span data-ttu-id="21eb2-245">Tuşuna **CTRL + S** dosyayı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="21eb2-245">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="21eb2-246">**Kaydırıcı çubuğun eklemek için kodu ilgili**</span><span class="sxs-lookup"><span data-stu-id="21eb2-246">**To add slider bar related code**</span></span>

1. <span data-ttu-id="21eb2-247">Çözüm Gezgini'nden sağ tıklayın **MainPage.xaml**ve ardından **görünümü kodu**.</span><span class="sxs-lookup"><span data-stu-id="21eb2-247">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="21eb2-248">Dosyanın başına aşağıdaki Ekle deyimi kullanarak:</span><span class="sxs-lookup"><span data-stu-id="21eb2-248">At the beginning of the file, add the following using statement:</span></span>
      
        using Windows.UI.Core;
3. <span data-ttu-id="21eb2-249">İçinde **MainPage** sınıfı, aşağıdaki veri üyeleri Ekle:</span><span class="sxs-lookup"><span data-stu-id="21eb2-249">Inside the **MainPage** class, add the following data members:</span></span>
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. <span data-ttu-id="21eb2-250">Sonunda **MainPage** oluşturucusu, aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-250">At the end of the **MainPage** constructor, add the following code:</span></span>
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. <span data-ttu-id="21eb2-251">Sonunda **MainPage** sınıfında, aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-251">At the end of the **MainPage** class, add the following code:</span></span>

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
><span data-ttu-id="21eb2-252">CoreDispatcher dışı kullanıcı Arabirimi iş parçacığından için kullanıcı Arabirimi iş parçacığı değişiklik yapmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21eb2-252">CoreDispatcher is used to make changes to the UI thread from non UI Thread.</span></span> <span data-ttu-id="21eb2-253">Dağıtıcı iş parçacığı engeli durumunda, geliştirici UI klasöründe güncelleştirme amaçlayan öğesi tarafından sağlanan dağıtıcısı kullanmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21eb2-253">In case of bottleneck on dispatcher thread, developer can choose to use dispatcher provided by UI-element he/she intends to update.</span></span>  <span data-ttu-id="21eb2-254">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-254">For example:</span></span>
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. <span data-ttu-id="21eb2-255">Sonunda **mediaElement_AdaptiveSourceStatusUpdated** yöntemi, aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-255">At the end of the **mediaElement_AdaptiveSourceStatusUpdated** method, add the following code:</span></span>

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. <span data-ttu-id="21eb2-256">Sonunda **MediaOpened** yöntemi, aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-256">At the end of the **MediaOpened** method, add the following code:</span></span>

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. <span data-ttu-id="21eb2-257">Tuşuna **CTRL + S** dosyayı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="21eb2-257">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="21eb2-258">**Derleme ve uygulamayı test etme**</span><span class="sxs-lookup"><span data-stu-id="21eb2-258">**To compile and test the application**</span></span>

1. <span data-ttu-id="21eb2-259">Tuşuna **F6** Projeyi derlemek için.</span><span class="sxs-lookup"><span data-stu-id="21eb2-259">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="21eb2-260">Uygulamayı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="21eb2-260">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="21eb2-261">Uygulama üst kısmında, varsayılan kesintisiz akış URL'sini kullanabilir veya farklı bir tane girin.</span><span class="sxs-lookup"><span data-stu-id="21eb2-261">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="21eb2-262">Tıklatın **ayarlamak kaynak**.</span><span class="sxs-lookup"><span data-stu-id="21eb2-262">Click **Set Source**.</span></span> 
5. <span data-ttu-id="21eb2-263">Kaydırıcı çubuğun sınayın.</span><span class="sxs-lookup"><span data-stu-id="21eb2-263">Test the slider bar.</span></span>

<span data-ttu-id="21eb2-264">Ders 2 tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="21eb2-264">You have completed lesson 2.</span></span>  <span data-ttu-id="21eb2-265">Bu ders uygulamaya kaydırıcıyı eklendi.</span><span class="sxs-lookup"><span data-stu-id="21eb2-265">In this lesson you added a slider to application.</span></span> 

## <a name="lesson-3-select-smooth-streaming-streams"></a><span data-ttu-id="21eb2-266">Ders 3: Kesintisiz akış akışları seçin</span><span class="sxs-lookup"><span data-stu-id="21eb2-266">Lesson 3: Select Smooth Streaming Streams</span></span>
<span data-ttu-id="21eb2-267">Kesintisiz akış görüntüleyicileri tarafından seçilebilen birden çok dil ses izleri ile içerik akışı sağlamak yeteneğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="21eb2-267">Smooth Streaming is capable to stream content with multiple language audio tracks that are selectable by the viewers.</span></span>  <span data-ttu-id="21eb2-268">Bu alıştırmanın ilerisinde akışları seçmek görüntüleyiciler olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="21eb2-268">In this lesson, you will enable viewers to select streams.</span></span> <span data-ttu-id="21eb2-269">Bu ders aşağıdaki yordamları içerir:</span><span class="sxs-lookup"><span data-stu-id="21eb2-269">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="21eb2-270">XAML dosyasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="21eb2-270">Modify the XAML file</span></span>
2. <span data-ttu-id="21eb2-271">Kod behand dosyasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="21eb2-271">Modify the code behand file</span></span>
3. <span data-ttu-id="21eb2-272">Derleme ve uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="21eb2-272">Compile and test the application</span></span>

<span data-ttu-id="21eb2-273">**XAML dosyasını değiştirmek için**</span><span class="sxs-lookup"><span data-stu-id="21eb2-273">**To modify the XAML file**</span></span>

1. <span data-ttu-id="21eb2-274">Çözüm Gezgini'nden sağ **MainPage.xaml**ve ardından **Görünüm Tasarımcısı**.</span><span class="sxs-lookup"><span data-stu-id="21eb2-274">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="21eb2-275">Bulun &lt;Grid.RowDefinitions&gt;ve RowDefinitions görünür gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-275">Locate &lt;Grid.RowDefinitions&gt;, and modify the RowDefinitions so they looks like:</span></span>
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. <span data-ttu-id="21eb2-276">İçinde &lt;kılavuz&gt;&lt;/Grid&gt; etiketler, böylece kullanıcılar kullanılabilir akışları listesini görmek ve seçin akışlar bir listbox denetimini tanımlamak için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-276">Inside the &lt;Grid&gt;&lt;/Grid&gt; tags, add the following code to define a listbox control, so users can see the list of available streams, and select streams:</span></span>

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
4. <span data-ttu-id="21eb2-277">Tuşuna **CTRL + S** değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="21eb2-277">Press **CTRL+S** to save the changes.</span></span>

<span data-ttu-id="21eb2-278">**Dosyanın arkasındaki kod değiştirmek için**</span><span class="sxs-lookup"><span data-stu-id="21eb2-278">**To modify the code behind file**</span></span>

1. <span data-ttu-id="21eb2-279">Çözüm Gezgini'nden sağ **MainPage.xaml**ve ardından **görünümü kodu**.</span><span class="sxs-lookup"><span data-stu-id="21eb2-279">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="21eb2-280">SSPlayer ad alanı içinde yeni bir sınıf ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-280">Inside the SSPlayer namespace, add a new class:</span></span>
   
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
                    // mMke the video stream always checked.
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
3. <span data-ttu-id="21eb2-281">MainPage sınıfı başlangıcında, aşağıdaki değişken tanımları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-281">At the beginning of the MainPage class, add the following variable definitions:</span></span>
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. <span data-ttu-id="21eb2-282">MainPage sınıfında, aşağıdaki bölge ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-282">Inside the MainPage class, add the following region:</span></span>
   
        #region stream selection
        ///<summary>
        ///Functionality to select streams from IManifestStream available streams
        /// </summary>
   
        // This function is called from the mediaElement_ManifestReady event handler 
        // to retrieve the streams and populate them to the local data members.
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
   
                    //populate the stream lists based on the types
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
   
                    // Select the default selected streams from the manifest.
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
   
        // This function set the list box ItemSource
        private async void refreshAvailableStreamsListBoxItemSource()
        {
            try
            {
                //update the stream check box list on the UI
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
   
            // Select the frist video stream from the list if no video stream is selected
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
                    txtStatus.Text = "The audio stream is changed to " + availableAudioStreams[j].ManifestStream.Name;
                }
            }
   
            // Select the frist audio stream from the list if no audio steam is selected.
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
5. <span data-ttu-id="21eb2-283">MediaElement_ManifestReady yöntemini bulun, işlevi sonuna aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-283">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span></span>
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    <span data-ttu-id="21eb2-284">Bu nedenle MediaElement bildirimi hazır olduğunda, kod kullanılabilir akışları listesini alır ve UI liste kutusu listesi ile doldurur.</span><span class="sxs-lookup"><span data-stu-id="21eb2-284">So when MediaElement manifest is ready, the code gets a list of the available streams, and populates the UI list box with the list.</span></span>
6. <span data-ttu-id="21eb2-285">Kullanıcı arabirimini MainPage sınıfı içinde bulun düğmeleri olayları bölge'ye tıklayın ve ardından aşağıdaki işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-285">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span></span>
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of the selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on the presentation
            changeStreams(selectedStreams);
        }

<span data-ttu-id="21eb2-286">**Derleme ve uygulamayı test etme**</span><span class="sxs-lookup"><span data-stu-id="21eb2-286">**To compile and test the application**</span></span>

1. <span data-ttu-id="21eb2-287">Tuşuna **F6** Projeyi derlemek için.</span><span class="sxs-lookup"><span data-stu-id="21eb2-287">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="21eb2-288">Uygulamayı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="21eb2-288">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="21eb2-289">Uygulama üst kısmında, varsayılan kesintisiz akış URL'sini kullanabilir veya farklı bir tane girin.</span><span class="sxs-lookup"><span data-stu-id="21eb2-289">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="21eb2-290">Tıklatın **ayarlamak kaynak**.</span><span class="sxs-lookup"><span data-stu-id="21eb2-290">Click **Set Source**.</span></span> 
5. <span data-ttu-id="21eb2-291">Varsayılan audio_eng dilidir.</span><span class="sxs-lookup"><span data-stu-id="21eb2-291">The default language is audio_eng.</span></span> <span data-ttu-id="21eb2-292">Audio_es audio_eng arasında geçiş yapmak deneyin.</span><span class="sxs-lookup"><span data-stu-id="21eb2-292">Try to switch between audio_eng and audio_es.</span></span> <span data-ttu-id="21eb2-293">Her, yeni bir akış seçin, Gönder düğmesine tıklamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="21eb2-293">Everytime, you select a new stream, you must click the Submit button.</span></span>

<span data-ttu-id="21eb2-294">Ders 3 tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="21eb2-294">You have completed lesson 3.</span></span>  <span data-ttu-id="21eb2-295">Bu alıştırmanın ilerisinde akışları seçmek için işlevsellik ekleyin.</span><span class="sxs-lookup"><span data-stu-id="21eb2-295">In this lesson, you add the functionality to choose streams.</span></span>

## <a name="lesson-4-select-smooth-streaming-tracks"></a><span data-ttu-id="21eb2-296">Ders 4: Kesintisiz akış parçaları seçin</span><span class="sxs-lookup"><span data-stu-id="21eb2-296">Lesson 4: Select Smooth Streaming Tracks</span></span>
<span data-ttu-id="21eb2-297">Kesintisiz akış sunu farklı kalite düzeyleri (bit hızları) ve çözümlemeleri ile kodlanmış birden çok video dosyaları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="21eb2-297">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span></span> <span data-ttu-id="21eb2-298">Bu ders, kullanıcıların parçaları seçmesine olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="21eb2-298">In this lesson, you will enable users to select tracks.</span></span> <span data-ttu-id="21eb2-299">Bu ders aşağıdaki yordamları içerir:</span><span class="sxs-lookup"><span data-stu-id="21eb2-299">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="21eb2-300">XAML dosyasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="21eb2-300">Modify the XAML file</span></span>
2. <span data-ttu-id="21eb2-301">Kod behand dosyasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="21eb2-301">Modify the code behand file</span></span>
3. <span data-ttu-id="21eb2-302">Derleme ve uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="21eb2-302">Compile and test the application</span></span>

<span data-ttu-id="21eb2-303">**XAML dosyasını değiştirmek için**</span><span class="sxs-lookup"><span data-stu-id="21eb2-303">**To modify the XAML file**</span></span>

1. <span data-ttu-id="21eb2-304">Çözüm Gezgini'nden sağ **MainPage.xaml**ve ardından **Görünüm Tasarımcısı**.</span><span class="sxs-lookup"><span data-stu-id="21eb2-304">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="21eb2-305">Bulun &lt;kılavuz&gt; etiket adıyla **gridStreamAndBitrateSelection**, etiket sonuna aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-305">Locate the &lt;Grid&gt; tag with the name **gridStreamAndBitrateSelection**, append the following code at the end of the tag:</span></span>
   
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
3. <span data-ttu-id="21eb2-306">Tuşuna **CTRL + S** he değişiklikleri kaydetmek için</span><span class="sxs-lookup"><span data-stu-id="21eb2-306">Press **CTRL+S** to save he changes</span></span>

<span data-ttu-id="21eb2-307">**Dosyanın arkasındaki kod değiştirmek için**</span><span class="sxs-lookup"><span data-stu-id="21eb2-307">**To modify the code behind file**</span></span>

1. <span data-ttu-id="21eb2-308">Çözüm Gezgini'nden sağ **MainPage.xaml**ve ardından **görünümü kodu**.</span><span class="sxs-lookup"><span data-stu-id="21eb2-308">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="21eb2-309">SSPlayer ad alanı içinde yeni bir sınıf ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-309">Inside the SSPlayer namespace, add a new class:</span></span>
   
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
3. <span data-ttu-id="21eb2-310">MainPage sınıfı başlangıcında, aşağıdaki değişken tanımları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-310">At the beginning of the MainPage class, add the following variable definitions:</span></span>
   
        private List<Track> availableTracks;
4. <span data-ttu-id="21eb2-311">MainPage sınıfında, aşağıdaki bölge ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-311">Inside the MainPage class, add the following region:</span></span>
   
        #region track selection
        /// <summary>
        /// Functionality to select video streams
        /// </summary>
   
        /// This Function gets the tracks for the selected video stream
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
   
        // This function gets the video stream that is playing
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
   
        // This function set the UI list box control ItemSource
        private async void refreshAvailableTracksListBoxItemSource()
        {
            try
            {
                // Update the track check box list on the UI 
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableVideoTracks.ItemsSource = availableTracks; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }        
        }
   
        // This function creates a list of the selected tracks.
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
   
        // This function selects the tracks based on user selection 
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
5. <span data-ttu-id="21eb2-312">MediaElement_ManifestReady yöntemini bulun, işlevi sonuna aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-312">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span></span>
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. <span data-ttu-id="21eb2-313">Kullanıcı arabirimini MainPage sınıfı içinde bulun düğmeleri olayları bölge'ye tıklayın ve ardından aşağıdaki işlevi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="21eb2-313">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span></span>
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of the selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on the presentation
            changeStreams(selectedStreams);
         }

<span data-ttu-id="21eb2-314">**Derleme ve uygulamayı test etme**</span><span class="sxs-lookup"><span data-stu-id="21eb2-314">**To compile and test the application**</span></span>

1. <span data-ttu-id="21eb2-315">Tuşuna **F6** Projeyi derlemek için.</span><span class="sxs-lookup"><span data-stu-id="21eb2-315">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="21eb2-316">Uygulamayı çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="21eb2-316">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="21eb2-317">Uygulama üst kısmında, varsayılan kesintisiz akış URL'sini kullanabilir veya farklı bir tane girin.</span><span class="sxs-lookup"><span data-stu-id="21eb2-317">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="21eb2-318">Tıklatın **ayarlamak kaynak**.</span><span class="sxs-lookup"><span data-stu-id="21eb2-318">Click **Set Source**.</span></span> 
5. <span data-ttu-id="21eb2-319">Varsayılan olarak, tüm video akışına parçaları seçilir.</span><span class="sxs-lookup"><span data-stu-id="21eb2-319">By default, all of the tracks of the video stream are selected.</span></span> <span data-ttu-id="21eb2-320">Bit hızı değişiklikleri denemek için en düşük bit hızı seçin ve ardından kullanılabilir en yüksek bit hızı seçin.</span><span class="sxs-lookup"><span data-stu-id="21eb2-320">To experiment the bit rate changes, you can select the lowest bit rate available, and then select the highest bit rate available.</span></span> <span data-ttu-id="21eb2-321">Her bir değişiklikten sonra Gönder'i tıklatmalısınız.</span><span class="sxs-lookup"><span data-stu-id="21eb2-321">You must click Submit after each change.</span></span>  <span data-ttu-id="21eb2-322">Video kalitesini değişiklikleri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21eb2-322">You can see the video quality changes.</span></span>

<span data-ttu-id="21eb2-323">Ders 4 tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="21eb2-323">You have completed lesson 4.</span></span>  <span data-ttu-id="21eb2-324">Bu alıştırmanın ilerisinde parçaları seçmek için işlevsellik ekleyin.</span><span class="sxs-lookup"><span data-stu-id="21eb2-324">In this lesson, you add the functionality to choose tracks.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="21eb2-325">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="21eb2-325">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="21eb2-326">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="21eb2-326">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a><span data-ttu-id="21eb2-327">Diğer kaynaklar:</span><span class="sxs-lookup"><span data-stu-id="21eb2-327">Other Resources:</span></span>
* [<span data-ttu-id="21eb2-328">Gelişmiş özelliklere sahip bir kesintisiz akış Windows 8 JavaScript uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="21eb2-328">How to build a Smooth Streaming Windows 8 JavaScript application with advanced features</span></span>](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [<span data-ttu-id="21eb2-329">Kesintisiz akış teknik genel bakış</span><span class="sxs-lookup"><span data-stu-id="21eb2-329">Smooth Streaming Technical Overview</span></span>](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

