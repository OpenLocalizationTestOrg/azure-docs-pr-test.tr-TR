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
# <a name="how-toobuild-a-smooth-streaming-windows-store-application"></a>Nasıl tooBuild kesintisiz akış Windows mağazası uygulaması

Merhaba kesintisiz akış istemci SDK Windows 8 için isteğe bağlı ve canlı kesintisiz akış içeriği yürütebilirsiniz geliştiriciler toobuild Windows mağazası uygulamaları etkinleştirir. Ayrıca toohello temel içerik, hello SDK de akış kesintisiz çalınmasını Microsoft PlayReady koruma, kalite düzeyi kısıtlama, Canlı DVR, geçiş, (örneğin, kalite düzeyi değişiklikleri durum güncelleştirmeleri için dinleme ses akışı gibi zengin özellikleri sağlar ) ve hata olayları ve benzeri. Merhaba desteklenen hello özellikleri daha fazla bilgi için bkz: [sürüm notları](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes). Daha fazla bilgi için bkz: [Windows 8 için Player Framework](http://playerframework.codeplex.com/). 

Bu öğretici dört dersleri içerir:

1. Bir temel kesintisiz akış depolama uygulaması oluştur
2. Bir kaydırma tooControl hello medya ilerleme çubuğu ekleyin
3. Kesintisiz akış akışları seçin
4. Kesintisiz akış parçaları seçin

## <a name="prerequisites"></a>Ön koşullar
* Windows 8 32 bit veya 64-bit. Alma [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) MSDN'den.
* Visual Studio 2012 veya Visual Studio Express 2012 (veya sonraki bir sürümünü). Merhaba deneme sürümünden alabilirsiniz [burada](http://www.microsoft.com/visualstudio/11/downloads).
* [Microsoft Windows 8 için İstemci SDK akış kesintisiz](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).

Her ders tamamlandı hello çözümü MSDN Geliştirici kod örneklerini (kod Galerisi) indirilebilir: 

* [Ders 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - Media Player, akış basit Windows 8 kesintisiz 
* [Ders 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - basit Windows 8 düzgün Media Player kaydırıcı çubuğun ile akış denetimi 
* [Ders 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - bir Windows 8 kesintisiz akış seçimi ile Media Player akış  
* [Ders 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) - Media Player izleme seçimi ile akış Windows 8 düzgün.

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a>Ders 1: temel bir kesintisiz akış mağazası uygulaması oluşturma

Bu ders içinde bir Windows mağazası uygulaması MediaElement bir denetim tooplay kesintisiz akış ile içerik oluşturur.  Merhaba çalışan uygulama şuna benzer:

![Kesintisiz akış Windows mağazası uygulama örneği][PlayerApplication]

Windows mağazası uygulaması geliştirme hakkında daha fazla bilgi için bkz: [geliştirmek harika uygulamaları Windows 8 için](http://msdn.microsoft.com/windows/apps/br229512.aspx). Bu ders hello yordamları içerir:

1. Bir Windows mağazası projesi oluşturma
2. Tasarım hello kullanıcı arabirimi (XAML)
3. Dosyanın arkasındaki Hello kodunu değiştirme
4. Derleme ve hello uygulamayı test etme

**toocreate bir Windows mağazası projesi**

1. Visual Studio 2012 veya sonraki sürümünü çalıştırın.
2. Merhaba gelen **dosya** menüsünde tıklatın **yeni**ve ardından **proje**.
3. Merhaba yeni proje iletişim kutusundan türü ya da aşağıdaki select hello değerler:

| Ad | Değer |
| --- | --- |
| Şablon grubu |Yüklü/Şablonlar/Visual C# / Windows Mağazası |
| Şablon |Boş uygulama (XAML) |
| Ad |SSPlayer |
| Konum |C:\SSTutorials |
| Çözüm adı |SSPlayer |
| Çözüm için dizin oluşturun |(Seçili) |

1. **Tamam** düğmesine tıklayın.

**tooadd başvuru toohello kesintisiz akış istemci SDK'sı**

1. Çözüm Gezgini'nden sağ **SSPlayer**ve ardından **Başvuru Ekle**.
2. Değerleri aşağıdaki hello seçin veya yazın:

| Ad | Değer |
| --- | --- |
| Başvuru grubu |Windows/uzantıları |
| Başvuru |Microsoft Windows 8 ve Microsoft Visual C++ çalışma zamanı paketi için İstemci SDK akış kesintisiz seçin |

1. **Tamam** düğmesine tıklayın. 

Merhaba başvuruları ekledikten sonra hedeflenen hello platform (x64 veya x86) seçmeniz gerekir, ekleyerek başvuruları için herhangi bir CPU platform yapılandırması çalışmaz.  Çözüm Gezgini'nde, sarı renkli uyarı işareti bu başvurular eklenen görürsünüz.

**toodesign hello player kullanıcı arabirimi**

1. Çözüm Gezgini'nde, çift tıklayarak **MainPage.xaml** tooopen hello tasarım görüntüleyin.
2. Merhaba bulun  **&lt;kılavuz&gt;**  ve  **&lt;/Grid&gt;**  etiketleri hello XAML dosyası ve Yapıştır hello aşağıdaki kod hello iki etiketleri arasında:

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
   
   Merhaba MediaElement denetimi kullanılan tooplayback medya ' dir. Merhaba kaydırıcı denetimi sliderProgress adlı hello sonraki Ders toocontrol hello medya ediyor kullanılır.
3. Tuşuna **CTRL + S** toosave hello dosya.

Merhaba MediaElement denetimi kesintisiz akış içerik out-of-box desteklemez. tooenable hello desteği, kesintisiz akış, kesintisiz akış bayt akışı hello işleyici dosya adı uzantısı ve MIME türü tarafından kaydetmeniz gerekir.  tooregister, hello Windows.Media ad alanının hello MediaExtensionManager.RegisterByteStremHandler yöntemini kullanın.

Bu XAML dosyası içinde bazı olay işleyicileri hello denetimleri ile ilişkilendirilmiş.  Bu olay işleyicileri tanımlamanız gerekir.

**dosyanın arkasındaki toomodify hello kodu**

1. Çözüm Gezgini'nden sağ **MainPage.xaml**ve ardından **görünümü kodu**.
2. Merhaba dosya Hello üstünde hello aşağıdakileri ekleyin deyimi kullanarak:
   
        using Windows.Media;
3. Merhaba hello başında **MainPage** sınıfı, veri üyenin hello ekleyin:
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. Merhaba hello sonunda **MainPage** oluşturucusu, hello aşağıdaki iki satırı ekleyin:
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. Merhaba hello sonunda **MainPage** sınıfı, hello aşağıdaki kodu yapıştırın:
   
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

Merhaba sliderProgress_PointerPressed olay işleyicisi burada belirtilir.  Daha fazla works toodo tooget vardır, çalışma, hangi kapsamdaki hello sonraki Bu öğreticinin Ders.
6. Tuşuna **CTRL + S** toosave hello dosya.

Merhaba tamamlanmış hello kodu dosyanın arkasındaki şöyle:

![Visual Studio, kesintisiz akış Windows mağazası uygulamasında Codeview][CodeViewPic]

**toocompile ve test Merhaba uygulaması**

1. Merhaba gelen **yapı** menüsünde tıklatın **Configuration Manager**.
2. Değişiklik **etkin çözüm platformu** toomatch geliştirme platformu.
3. Tuşuna **F6** toocompile hello projesi. 
4. Tuşuna **F5** toorun Merhaba uygulaması.
5. Merhaba uygulaması Hello üstünde hello varsayılan kesintisiz akış URL'sini kullanabilir veya farklı bir tane girin. 
6. Tıklatın **ayarlamak kaynak**. Çünkü **Otomatik Yürüt** hello medya yürütme otomatik olarak varsayılan olarak etkindir.  Merhaba medya hello kullanarak denetleyebilirsiniz **Yürüt**, **duraklatma** ve **durdurmak** düğmeler.  Merhaba dikey kaydırıcıyı kullanarak hello medya birimi kontrol edebilirsiniz.  Ancak medya ilerleme tam henüz uygulanmadı hello denetleme yatay kaydırıcı hello. 

Lesson1 tamamladınız.  Bu alıştırmanın ilerisinde MediaElement denetimi tooplayback kesintisiz akış içeriği kullanın.  Merhaba sonraki ders, kesintisiz akış içeriği hello kaydırıcı toocontrol hello ilerlemesini ekleyeceksiniz.

## <a name="lesson-2-add-a-slider-bar-toocontrol-hello-media-progress"></a>Ders 2: kaydırma tooControl hello medya ilerleme çubuğu ekleme

Ders 1'de, bir Windows mağazası uygulaması MediaElement XAML denetim tooplayback kesintisiz akış medya içeriği ile oluşturulmuş.  Başlatma, durdurma ve duraklatma gibi bazı temel media işlevleri gelir.  Bu alıştırmanın ilerisinde kaydırıcı çubuk denetim toohello uygulaması ekleyeceksiniz.

Bu öğreticide, hello geçerli hello MediaElement denetimi konumuna bağlı bir zamanlayıcı tooupdate hello kaydırıcı konumu kullanacağız.  Merhaba kaydırıcı başlatın ve bitiş zamanı da gerek toobe durumunda dinamik içerik güncelleştirildi.  Bu, daha iyi hello Uyarlamalı kaynak güncelleştirme olayda işlenebilir.

Medya kaynaklarına medya veri üreten nesneleridir.  Merhaba kaynak Çözümleyici bir URL veya bayt akış alır ve bu içerik hello uygun medya kaynağı oluşturur.  Merhaba kaynak çözümleyici hello standart hello uygulamaları toocreate medya kaynakları için yoludur. 

Bu ders hello yordamları içerir:

1. Merhaba kesintisiz akış işleyici kaydetme 
2. Merhaba Uyarlamalı Kaynak Yöneticisi düzeyi olay işleyicileri ekleme
3. Merhaba Uyarlamalı kaynak düzeyi olay işleyicileri ekleme
4. MediaElement olay işleyicileri ekleme
5. Kaydırma çubuğu ilgili kod ekleme
6. Derleme ve hello uygulamayı test etme

**tooregister hello kesintisiz akış bayt akışı işleyicisi ve geçişi hello propertyset**

1. Çözüm Gezgini'nden sağ tıklayın **MainPage.xaml**ve ardından **görünümü kodu**.
2. Merhaba dosya Hello başında hello aşağıdakileri ekleyin deyimi kullanarak:

        using Microsoft.Media.AdaptiveStreaming;
3. Merhaba MainPage sınıfı Hello başlangıcında, veri üyeleri aşağıdaki hello ekleyin:

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. İç hello **MainPage** oluşturucusu, koddan sonra hello hello eklemek **bu. Components() başlatılamadı;**  satır ve hello önceki Ders içinde yazılmış hello kayıt kod satırı:

        // Gets hello default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value tooAdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. İç hello **MainPage** oluşturucusu, hello iki RegisterByteStreamHandler yöntemleri tooadd hello İleri parametreleri değiştirin:

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
6. Tuşuna **CTRL + S** toosave hello dosya.

**tooadd hello Uyarlamalı Kaynak Yöneticisi düzeyi olay işleyicisi**

1. Çözüm Gezgini'nden sağ tıklayın **MainPage.xaml**ve ardından **görünümü kodu**.
2. İç hello **MainPage** sınıfı, veri üyenin hello ekleyin:
   
     Özel AdaptiveSource adaptiveSource = null;
3. Merhaba hello sonunda **MainPage** sınıf, olay işleyicisi aşağıdaki hello ekleyin:
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. Merhaba hello sonunda **MainPage** oluşturucusu, satır toosubscribe toohello Uyarlamalı kaynak açık olay aşağıdaki hello ekleyin:
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. Tuşuna **CTRL + S** toosave hello dosya.

**tooadd Uyarlamalı kaynak düzeyi olay işleyicileri**

1. Çözüm Gezgini'nden sağ tıklayın **MainPage.xaml**ve ardından **görünümü kodu**.
2. İç hello **MainPage** sınıfı, veri üyenin hello ekleyin:
   
     Özel AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   Özel bildirim manifestObject;
3. Merhaba hello sonunda **MainPage** sınıf, olay işleyicileri aşağıdaki hello ekleyin:

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
4. Merhaba hello sonunda **mediaElement AdaptiveSourceOpened** yöntemi, kod toosubscribe toohello olayları aşağıdaki hello ekleyin:
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. Tuşuna **CTRL + S** toosave hello dosya.

Merhaba işlevselliği ortak tooall ortam öğeleri hello uygulamasında işlemek için kullanılan Uyarlamalı kaynak yöneticisi düzeyinde de aynı olayları kullanılabilir. Tüm AdaptiveSource olayları AdaptiveSourceManager altında basamaklı ve her AdaptiveSource, kendi olaylarını içerir.

**tooadd medya öğesi olay işleyicileri**

1. Çözüm Gezgini'nden sağ tıklayın **MainPage.xaml**ve ardından **görünümü kodu**.
2. Merhaba hello sonunda **MainPage** sınıf, olay işleyicileri aşağıdaki hello ekleyin:

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
3. Merhaba hello sonunda **MainPage** oluşturucusu, kod toosubscript toohello olayları aşağıdaki hello ekleyin:

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. Tuşuna **CTRL + S** toosave hello dosya.

**ilgili barkod tooadd kaydırıcı**

1. Çözüm Gezgini'nden sağ tıklayın **MainPage.xaml**ve ardından **görünümü kodu**.
2. Merhaba dosya Hello başında hello aşağıdakileri ekleyin deyimi kullanarak:
      
        using Windows.UI.Core;
3. İç hello **MainPage** sınıfı, veri üyeleri aşağıdaki hello ekleyin:
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. Merhaba hello sonunda **MainPage** oluşturucusu, hello aşağıdaki kodu ekleyin:
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. Merhaba hello sonunda **MainPage** sınıfı, hello aşağıdaki kodu ekleyin:

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
>CoreDispatcher toohello UI dışı kullanıcı Arabirimi iş parçacığından iş parçacığı kullanılan toomake değişiklikler var. Dağıtıcı iş parçacığı engeli durumunda, geliştirici klasöründe tooupdate oranla toouse dağıtıcısı kullanıcı Arabirimi öğesi tarafından sağlanan seçebilirsiniz.  Örneğin:
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. Merhaba hello sonunda **mediaElement_AdaptiveSourceStatusUpdated** yöntemi, hello aşağıdaki kodu ekleyin:

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. Merhaba hello sonunda **MediaOpened** yöntemi, hello aşağıdaki kodu ekleyin:

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. Tuşuna **CTRL + S** toosave hello dosya.

**toocompile ve test Merhaba uygulaması**

1. Tuşuna **F6** toocompile hello projesi. 
2. Tuşuna **F5** toorun Merhaba uygulaması.
3. Merhaba uygulaması Hello üstünde hello varsayılan kesintisiz akış URL'sini kullanabilir veya farklı bir tane girin. 
4. Tıklatın **ayarlamak kaynak**. 
5. Test hello kaydırıcı çubuk.

Ders 2 tamamladınız.  Bu ders kaydırıcı tooapplication eklendi. 

## <a name="lesson-3-select-smooth-streaming-streams"></a>Ders 3: Kesintisiz akış akışları seçin
Kesintisiz akış, hello görüntüleyicileri tarafından seçilebilen birden çok dil ses izleri ile özellikli toostream içeriktir.  Bu alıştırmanın ilerisinde görüntüleyiciler tooselect akışları olanak sağlar. Bu ders hello yordamları içerir:

1. Merhaba XAML dosyasını değiştirme
2. Merhaba kod behand dosyasını değiştirme
3. Derleme ve hello uygulamayı test etme

**toomodify hello XAML dosyası**

1. Çözüm Gezgini'nden sağ **MainPage.xaml**ve ardından **Görünüm Tasarımcısı**.
2. Bulun &lt;Grid.RowDefinitions&gt;ve görünür gibi hello RowDefinitions değiştirin:
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. İç hello &lt;kılavuz&gt;&lt;/Grid&gt; etiketler eklemek hello kodundan aşağıdaki kodu toodefine listbox denetimi, böylece kullanıcılar kullanılabilir akışları hello listesini görmek ve akışlar seçin:

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
4. Tuşuna **CTRL + S** toosave hello değişiklikleri.

**dosyanın arkasındaki toomodify hello kodu**

1. Çözüm Gezgini'nden sağ **MainPage.xaml**ve ardından **görünümü kodu**.
2. Merhaba SSPlayer ad alanı içinde yeni bir sınıf ekleyin:
   
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
3. Merhaba MainPage sınıfı Hello başında değişken tanımları aşağıdaki hello ekleyin:
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. Merhaba MainPage sınıfı içinde bölge aşağıdaki hello ekleyin:
   
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
5. Merhaba mediaElement_ManifestReady yöntemini bulun, hello işlevi hello sonunda koddan hello Ekle:
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    Bu nedenle MediaElement bildirimi hazır olduğunda, hello kod hello kullanılabilir akışları listesini alır ve hello UI liste kutusu hello listesi ile doldurur.
6. Merhaba MainPage sınıfı içinde bulun hello UI düğmeleri olayları bölge'ye tıklayın ve ardından işlev tanımı aşağıdaki hello ekleyin:
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on hello presentation
            changeStreams(selectedStreams);
        }

**toocompile ve test Merhaba uygulaması**

1. Tuşuna **F6** toocompile hello projesi. 
2. Tuşuna **F5** toorun Merhaba uygulaması.
3. Merhaba uygulaması Hello üstünde hello varsayılan kesintisiz akış URL'sini kullanabilir veya farklı bir tane girin. 
4. Tıklatın **ayarlamak kaynak**. 
5. Merhaba varsayılan audio_eng dilidir. Tooswitch audio_eng audio_es arasındaki deneyin. Her, yeni bir akış seçin, hello gönder düğmesine tıklamanız gerekir.

Ders 3 tamamladınız.  Bu alıştırmanın ilerisinde hello işlevselliği toochoose akışlar ekleyin.

## <a name="lesson-4-select-smooth-streaming-tracks"></a>Ders 4: Kesintisiz akış parçaları seçin
Kesintisiz akış sunu farklı kalite düzeyleri (bit hızları) ve çözümlemeleri ile kodlanmış birden çok video dosyaları içerebilir. Bu ders, kullanıcıların tooselect parçaları olanak sağlar. Bu ders hello yordamları içerir:

1. Merhaba XAML dosyasını değiştirme
2. Merhaba kod behand dosyasını değiştirme
3. Derleme ve hello uygulamayı test etme

**toomodify hello XAML dosyası**

1. Çözüm Gezgini'nden sağ **MainPage.xaml**ve ardından **Görünüm Tasarımcısı**.
2. Merhaba bulun &lt;kılavuz&gt; hello adı etiketiyle **gridStreamAndBitrateSelection**, hello etiketi hello sonunda koddan hello Ekle:
   
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
3. Tuşuna **CTRL + S** toosave kendisinin değiştirir

**dosyanın arkasındaki toomodify hello kodu**

1. Çözüm Gezgini'nden sağ **MainPage.xaml**ve ardından **görünümü kodu**.
2. Merhaba SSPlayer ad alanı içinde yeni bir sınıf ekleyin:
   
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
3. Merhaba MainPage sınıfı Hello başında değişken tanımları aşağıdaki hello ekleyin:
   
        private List<Track> availableTracks;
4. Merhaba MainPage sınıfı içinde bölge aşağıdaki hello ekleyin:
   
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
5. Merhaba mediaElement_ManifestReady yöntemini bulun, hello işlevi hello sonunda koddan hello Ekle:
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. Merhaba MainPage sınıfı içinde bulun hello UI düğmeleri olayları bölge'ye tıklayın ve ardından işlev tanımı aşağıdaki hello ekleyin:
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on hello presentation
            changeStreams(selectedStreams);
         }

**toocompile ve test Merhaba uygulaması**

1. Tuşuna **F6** toocompile hello projesi. 
2. Tuşuna **F5** toorun Merhaba uygulaması.
3. Merhaba uygulaması Hello üstünde hello varsayılan kesintisiz akış URL'sini kullanabilir veya farklı bir tane girin. 
4. Tıklatın **ayarlamak kaynak**. 
5. Varsayılan olarak, tüm hello video akışına hello parçalarının seçilir. tooexperiment hello bit hızı değişiklikleri, hello düşük bit hızı kullanılabilir seçin ve ardından hello yüksek bit hızı kullanılabilir seçin. Her bir değişiklikten sonra Gönder'i tıklatmalısınız.  Merhaba video kalitesini değişiklikleri görebilirsiniz.

Ders 4 tamamladınız.  Bu alıştırmanın ilerisinde hello işlevselliği toochoose parçaları ekleyin.

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a>Diğer kaynaklar:
* [Toobuild nasıl Gelişmiş Özellikler ileri bir kesintisiz akış Windows 8 JavaScript uygulaması ile](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [Kesintisiz akış teknik genel bakış](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

