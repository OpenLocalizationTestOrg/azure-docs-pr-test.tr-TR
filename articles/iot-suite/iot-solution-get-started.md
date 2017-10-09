---
title: "MyDriving Azure IOT örnek: Hızlı Başlangıç | Microsoft Docs"
description: "Nasıl kapsamlı bir örnek bir uygulama ile çalışmaya başlama tooarchitect akış analizi, Machine Learning ve olay hub'ları da dahil olmak üzere Microsoft Azure kullanarak bir IOT sistemi."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: f40ea71b-5721-4a6b-a886-53c2e9dffe8f
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 03/25/2016
ms.author: harikm
ms.openlocfilehash: 411b9a992deb22b915f8291d8559e2917d976b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="mydriving-iot-system-quick-start"></a><span data-ttu-id="66d66-103">MyDriving IOT sistem: Hızlı Başlangıç</span><span class="sxs-lookup"><span data-stu-id="66d66-103">MyDriving IoT system: Quick start</span></span>
<span data-ttu-id="66d66-104">MyDriving sistemidir hello tasarımını ve uygulamasını tipik bir gösteren bir [nesnelerin interneti](iot-suite-overview.md) telemetri cihazlardan toplar (IOT) çözümü hello bulutta bu verileri işler ve machine learning uygulanır tooprovide Uyarlamalı yanıt.</span><span class="sxs-lookup"><span data-stu-id="66d66-104">MyDriving is a system that demonstrates hello design and implementation of a typical [Internet of Things](iot-suite-overview.md) (IoT) solution that gathers telemetry from devices, processes that data in hello cloud, and applies machine learning tooprovide an adaptive response.</span></span> <span data-ttu-id="66d66-105">Merhaba tanıtım cep telefonunuzu ve arabanızın denetim sisteminden bilgileri toplayan bir bağdaştırıcı verilerini kullanarak, car dönüşleri hakkındaki verileri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="66d66-105">hello demonstration logs data about your car trips, by using data from both your mobile phone and an adapter that collects information from your car’s control system.</span></span> <span data-ttu-id="66d66-106">Bu veri tooprovide geri bildirim yönlendirmeli stilinize karşılaştırma tooother kullanıcılar üzerinde kullanır.</span><span class="sxs-lookup"><span data-stu-id="66d66-106">It uses this data tooprovide feedback on your driving style in comparison tooother users.</span></span>

<span data-ttu-id="66d66-107">Merhaba gerçek MyDriving amacı kendi IOT çözümünüzü oluştururken başlattığınız tooget budur.</span><span class="sxs-lookup"><span data-stu-id="66d66-107">hello real purpose of MyDriving is tooget you started in creating your own IoT solution.</span></span> <span data-ttu-id="66d66-108">Ancak, önce şimdi uygulamayla hello MyDriving kendisini--test kullanıcı ekibimiz üyesi olarak adımıdır alın.</span><span class="sxs-lookup"><span data-stu-id="66d66-108">But before that, let’s get you going with hello MyDriving app itself--as a member of our test user team.</span></span> <span data-ttu-id="66d66-109">Merhaba mimariye inceleyin önce bu size hello uygulamanın ve bunun arkasındaki hello sistem bir tüketici olarak bir deneyim sağlar.</span><span class="sxs-lookup"><span data-stu-id="66d66-109">This gives you an experience of hello app and hello system behind it as a consumer, before you delve into hello architecture.</span></span> <span data-ttu-id="66d66-110">Bu aynı zamanda, tooHockeyApp, uygulamaları tootest kullanıcılarınızın hello alfa ve beta dağıtımlarını yönetme harika bir yol sunar.</span><span class="sxs-lookup"><span data-stu-id="66d66-110">It also introduces you tooHockeyApp, a cool way of managing hello alpha and beta distributions of your apps tootest users.</span></span>

## <a name="use-hello-mobile-experience"></a><span data-ttu-id="66d66-111">Merhaba mobil deneyimi kullanın</span><span class="sxs-lookup"><span data-stu-id="66d66-111">Use hello mobile experience</span></span>
<span data-ttu-id="66d66-112">Android, iOS veya Windows 10 cihaz varsa hello MyDriving uygulamasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66d66-112">You can use hello MyDriving app if you have an Android, iOS, or Windows 10 device.</span></span>

### <a name="android-and-windows-10-mobile-installation"></a><span data-ttu-id="66d66-113">Android ve Windows 10 Mobile yükleme</span><span class="sxs-lookup"><span data-stu-id="66d66-113">Android and Windows 10 Mobile installation</span></span>
<span data-ttu-id="66d66-114">Cihazınızda:</span><span class="sxs-lookup"><span data-stu-id="66d66-114">On your device:</span></span>

1. <span data-ttu-id="66d66-115">Geliştirme uygulamaları izin ver:</span><span class="sxs-lookup"><span data-stu-id="66d66-115">Allow development apps:</span></span>
   
   * <span data-ttu-id="66d66-116">Android: İçinde **ayarları** > **güvenlik**, uygulamalardan izin **bilinmeyen kaynaklardan**.</span><span class="sxs-lookup"><span data-stu-id="66d66-116">Android: In **Settings** > **Security**, allow apps from **Unknown sources**.</span></span>
   * <span data-ttu-id="66d66-117">: Windows 10 **ayarları** > **güncelleştirmeleri** > **geliştiriciler için**ayarlayın **geliştirici modunu**.</span><span class="sxs-lookup"><span data-stu-id="66d66-117">Windows 10: In **Settings** > **Updates** > **For Developers**, set **Developer mode**.</span></span>
2. <span data-ttu-id="66d66-118">İle kaydolduktan ya da, oturum açma tarafından beta test ekibimiz katılma [HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="66d66-118">Join our beta test team by signing up with, or signing in to, [HockeyApp](https://rink.hockeyapp.net).</span></span> <span data-ttu-id="66d66-119">HockeyApp sürümleri kolay toodistribute erken uygulama tootest kullanıcılarınızın kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="66d66-119">HockeyApp makes it easy toodistribute early releases of your app tootest users.</span></span>
   
   <span data-ttu-id="66d66-120">Windows 10 kullanıyorsanız, hello Edge tarayıcısı kullanın.</span><span class="sxs-lookup"><span data-stu-id="66d66-120">If you’re using Windows 10, use hello Edge browser.</span></span>
   
   <span data-ttu-id="66d66-121">Build 2016 katılımcı olsaydı, oturum hello aynı oturum hello Microsoft düğmeleri birini kullanarak hello konferans için kayıtlı Microsoft hesabı e-posta.</span><span class="sxs-lookup"><span data-stu-id="66d66-121">If you were a Build 2016 attendee, sign in with hello same Microsoft account email that you registered for hello conference, by using one of hello Microsoft buttons.</span></span> <span data-ttu-id="66d66-122">HockeyApp ile zaten kaydolmuşsunuz.</span><span class="sxs-lookup"><span data-stu-id="66d66-122">You’re already signed up with HockeyApp.</span></span>
   
   ![HockeyApp oturum açma ekranı](./media/iot-solution-get-started/image1.png)
3. <span data-ttu-id="66d66-124">Merhaba uygulamasını indirip buradan yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="66d66-124">Download and install hello app from here:</span></span>
   
   * [<span data-ttu-id="66d66-125">Android</span><span class="sxs-lookup"><span data-stu-id="66d66-125">Android</span></span>](http://rink.io/spMyDrivingAndroid)
   * [<span data-ttu-id="66d66-126">Windows 10</span><span class="sxs-lookup"><span data-stu-id="66d66-126">Windows 10</span></span>](http://rink.io/spMyDrivingUWP)
   
   <span data-ttu-id="66d66-127">İki öğe yok.</span><span class="sxs-lookup"><span data-stu-id="66d66-127">There are two items.</span></span> <span data-ttu-id="66d66-128">Merhaba yüklemek **güvenilir kişiler**.</span><span class="sxs-lookup"><span data-stu-id="66d66-128">Install hello certificate in **Trusted People**.</span></span> <span data-ttu-id="66d66-129">Ardından hello uygulamasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="66d66-129">Then install hello app.</span></span>

<span data-ttu-id="66d66-130">*Tüm Windows 10 Mobile başlangıç hello uygulamasını sorunları?*</span><span class="sxs-lookup"><span data-stu-id="66d66-130">*Any issues starting hello app on Windows 10 Mobile?*</span></span> <span data-ttu-id="66d66-131">Telefonunuza bir güncelleştirme veya iki arkasında olabilir.</span><span class="sxs-lookup"><span data-stu-id="66d66-131">Your phone might be an update or two behind.</span></span> <span data-ttu-id="66d66-132">Merhaba en son güncelleştirmeleri olduğuna ya da yükleme emin olun:</span><span class="sxs-lookup"><span data-stu-id="66d66-132">Make sure you've got hello latest updates, or install:</span></span>

* [<span data-ttu-id="66d66-133">Microsoft.NET.Native.Framework.1.2.appx</span><span class="sxs-lookup"><span data-stu-id="66d66-133">Microsoft.NET.Native.Framework.1.2.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [<span data-ttu-id="66d66-134">Microsoft.NET.Native.Runtime.1.1.appx</span><span class="sxs-lookup"><span data-stu-id="66d66-134">Microsoft.NET.Native.Runtime.1.1.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [<span data-ttu-id="66d66-135">Microsoft.VCLibs.ARM.14.00.appx</span><span class="sxs-lookup"><span data-stu-id="66d66-135">Microsoft.VCLibs.ARM.14.00.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a><span data-ttu-id="66d66-136">iOS yükleme</span><span class="sxs-lookup"><span data-stu-id="66d66-136">iOS installation</span></span>
<span data-ttu-id="66d66-137">Build 2016 gittiğiniz, test ekibimiz HockeyApp üzerinde bir üyesi olarak hello uygulamasını yükleyin:</span><span class="sxs-lookup"><span data-stu-id="66d66-137">If you attended Build 2016, download hello app as a member of our test team on HockeyApp:</span></span>

1. <span data-ttu-id="66d66-138">İOS Cihazınızda çok oturum[HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="66d66-138">On your iOS device, sign in too[HockeyApp](https://rink.hockeyapp.net).</span></span>
   <span data-ttu-id="66d66-139">Bir hello Microsoft oturum açma düğmeleri ile oturum açın ve hello hello konferans kayıtlı aynı Microsoft hesabı e-posta kullanın.</span><span class="sxs-lookup"><span data-stu-id="66d66-139">Use one of hello Microsoft sign-in buttons, and sign in with hello same Microsoft account email that you registered with hello conference.</span></span> <span data-ttu-id="66d66-140">(Merhaba e-posta ve parola alanlarına kullanmayın.)</span><span class="sxs-lookup"><span data-stu-id="66d66-140">(Don’t use hello email and password fields.)</span></span>
   
   ![HockeyApp oturum açma ekranı](./media/iot-solution-get-started/image1.png)
2. <span data-ttu-id="66d66-142">Merhaba HockeyApp panosundaki MyDriving seçin ve indirin.</span><span class="sxs-lookup"><span data-stu-id="66d66-142">In hello HockeyApp dashboard, select MyDriving and download it.</span></span>
3. <span data-ttu-id="66d66-143">HockeyApp Hello beta sürümünden yetkilendirin.</span><span class="sxs-lookup"><span data-stu-id="66d66-143">Authorize hello beta release from HockeyApp:</span></span>
   
   <span data-ttu-id="66d66-144">a.</span><span class="sxs-lookup"><span data-stu-id="66d66-144">a.</span></span> <span data-ttu-id="66d66-145">Çok Git**ayarları** > **genel** > **profilleri ve aygıt yönetimi.**</span><span class="sxs-lookup"><span data-stu-id="66d66-145">Go too**Settings** > **General** > **Profiles and Device Management.**</span></span>
   
   <span data-ttu-id="66d66-146">b.</span><span class="sxs-lookup"><span data-stu-id="66d66-146">b.</span></span> <span data-ttu-id="66d66-147">Merhaba güven **Bit stadyum GmbH** sertifika.</span><span class="sxs-lookup"><span data-stu-id="66d66-147">Trust hello **Bit Stadium GmbH** certificate.</span></span>

<span data-ttu-id="66d66-148">Build 2016 gitmediğiniz, yapı ve hello uygulama kendiniz dağıtabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="66d66-148">If you didn’t attend Build 2016, you can build and deploy hello app yourself:</span></span>

1. <span data-ttu-id="66d66-149">Merhaba kodu indirme [github'dan].</span><span class="sxs-lookup"><span data-stu-id="66d66-149">Download hello code [from GitHub].</span></span>
2. <span data-ttu-id="66d66-150">Derleme ve tarafından dağıtma [Xamarin kullanarak].</span><span class="sxs-lookup"><span data-stu-id="66d66-150">Build and deploy by [using Xamarin].</span></span>

<span data-ttu-id="66d66-151">Daha fazla ayrıntı hello Bul [MyDriving Başvuru Kılavuzu](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="66d66-151">Find more details in hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="get-an-obd-adapter-optional"></a><span data-ttu-id="66d66-152">OBD bağdaştırıcıyı (isteğe bağlı) Al</span><span class="sxs-lookup"><span data-stu-id="66d66-152">Get an OBD adapter (optional)</span></span>
<span data-ttu-id="66d66-153">Bu gerçek bir nesnelerin interneti sistem yapan hello bölümüdür!</span><span class="sxs-lookup"><span data-stu-id="66d66-153">This is hello part that makes this a real Internet of Things system!</span></span> <span data-ttu-id="66d66-154">Daha fazla keyif hello gerçek bir şey olduğunu ve pahalı olmayan hello uygulama biri olmadan kullanabilirsiniz ancak.</span><span class="sxs-lookup"><span data-stu-id="66d66-154">You can use hello app without one, but it’s more fun with hello real thing, and they aren’t expensive.</span></span>

<span data-ttu-id="66d66-155">Yerleşik tanılama (OBD) hello Garaj kullanır tootune, car yukarı hello ve tek sesleri ve uyarı ampul Tanılama, car özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="66d66-155">On-board diagnostics (OBD) is hello feature of your car that hello garage uses tootune up your car and diagnose odd noises and warning lamps.</span></span> <span data-ttu-id="66d66-156">Car harika antiquity olmadıkça, genellikle bir flap hello Pano altında arkasında hello kabini yuva yerde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66d66-156">Unless your car is of great antiquity, you’ll find a socket somewhere in hello cabin, typically behind a flap under hello dashboard.</span></span> <span data-ttu-id="66d66-157">Hello sağ bağlayıcısıyla hello altyapısının performans ölçümlerini alın ve belirli ayarlamalar yapın.</span><span class="sxs-lookup"><span data-stu-id="66d66-157">With hello right connector, you can get metrics of hello engine’s performance and make certain adjustments.</span></span> <span data-ttu-id="66d66-158">Bir OBD Bağlayıcısı ailenin hello normal yerlerden satın alınabilir.</span><span class="sxs-lookup"><span data-stu-id="66d66-158">An OBD connector can be purchased cheaply from hello usual places.</span></span> <span data-ttu-id="66d66-159">Bu, telefonunuza Bluetooth veya Wi-Fi tooan uygulamasını kullanarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="66d66-159">It connects by using Bluetooth or Wi-Fi tooan app on your phone.</span></span>

<span data-ttu-id="66d66-160">Bu durumda, car toohello bulutunuzu tooconnect yapacağız.</span><span class="sxs-lookup"><span data-stu-id="66d66-160">In this case, we’re going tooconnect your car toohello cloud.</span></span> <span data-ttu-id="66d66-161">Merhaba OBD bağlantısından Hello doğrudan bağlantı tooyour telefon olmakla birlikte, uygulamamıza geçişi olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="66d66-161">hello direct connection from hello OBD is tooyour phone, but our app works as a relay.</span></span> <span data-ttu-id="66d66-162">Arabanızın telemetri düz toohello olduğu MyDriving IOT hub, yol dönüşleri toolog işlenen gönderilir ve yönlendirmeli stilinize değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="66d66-162">Your car's telemetry is sent straight toohello MyDriving IoT hub, where it's processed toolog your road trips and assess your driving style.</span></span>

<span data-ttu-id="66d66-163">tooconnect OBD aygıt:</span><span class="sxs-lookup"><span data-stu-id="66d66-163">tooconnect an OBD device:</span></span>

1. <span data-ttu-id="66d66-164">Car OBD yuva olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="66d66-164">Check that your car has an OBD socket.</span></span>
2. <span data-ttu-id="66d66-165">OBD bağdaştırıcıyı alın:</span><span class="sxs-lookup"><span data-stu-id="66d66-165">Obtain an OBD adapter:</span></span>
   
   * <span data-ttu-id="66d66-166">Bir Android veya Windows phone kullanıyorsanız, Bluetooth özellikli OBD II bağdaştırıcısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="66d66-166">If you're using an Android or Windows phone, you need a Bluetooth-enabled OBD II adapter.</span></span> <span data-ttu-id="66d66-167">Kullandık [BAFX ürünleri 34t5 Bluetooth OBDII Tarama Aracı].</span><span class="sxs-lookup"><span data-stu-id="66d66-167">We used [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span></span>
   * <span data-ttu-id="66d66-168">Bir iOS telefon kullanıyorsanız, bir Wi-Fi etkin OBD bağdaştırıcısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="66d66-168">If you're using an iOS phone, you need a Wi-Fi-enabled OBD adapter.</span></span> <span data-ttu-id="66d66-169">Kullandık [ScanTool OBDLink MX Wi-Fi: OBD bağdaştırıcısı/tanılama tarayıcı].</span><span class="sxs-lookup"><span data-stu-id="66d66-169">We used [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].</span></span>
3. <span data-ttu-id="66d66-170">İsteğe bağlı olarak, OBD bağdaştırıcısı tooconnect ile tooyour telefon gelen hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="66d66-170">Follow hello instructions that come with your OBD adapter tooconnect it tooyour phone.</span></span> <span data-ttu-id="66d66-171">Merhaba aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="66d66-171">Keep hello following in mind:</span></span>
   
   * <span data-ttu-id="66d66-172">Bluetooth bağdaştırıcısı hello telefonda hello ile eşleştirilmelidir **ayarları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="66d66-172">A Bluetooth adapter must be paired with hello phone, on hello **Settings** page.</span></span>
   * <span data-ttu-id="66d66-173">Bir Wi-Fi bağdaştırıcısı hello aralığı 192.168.xxx.xxx bir adres olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="66d66-173">A Wi-Fi adapter must have an address in hello range 192.168.xxx.xxx.</span></span>
4. <span data-ttu-id="66d66-174">Çeşitli otomobiller varsa, her (en fazla üç için) ayrı bir bağdaştırıcı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66d66-174">If you have several cars, you can get a separate adapter for each (maximum of three).</span></span>

<span data-ttu-id="66d66-175">OBD bağdaştırıcıyı yoksa, hello uygulama hala konumu ve hello telefonun GPS alıcı toohello geri hızı verileri sona erdirmek ve toosimulate bir OBD isteyip istemediğinizi sorar gönderir.</span><span class="sxs-lookup"><span data-stu-id="66d66-175">If you don’t have an OBD adapter, hello app will still send location and speed data from hello phone's GPS receiver toohello back end and will ask if you want toosimulate an OBD.</span></span>

<span data-ttu-id="66d66-176">Hello bölüm 2.1, "IOT cihazları," kendi OBD cihaz oluşturmak için seçenekler ve hello uygulama hello OBD bağdaştırıcısı verileri nasıl kullandığı hakkında daha fazla bulabilirsiniz [MyDriving Başvuru Kılavuzu](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="66d66-176">You can find out more about how hello app uses data from hello OBD adapter and about options for creating your own OBD device in section 2.1, "IoT Devices," in hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="use-hello-app"></a><span data-ttu-id="66d66-177">Merhaba uygulama kullanma</span><span class="sxs-lookup"><span data-stu-id="66d66-177">Use hello app</span></span>
<span data-ttu-id="66d66-178">Merhaba uygulaması başlatın.</span><span class="sxs-lookup"><span data-stu-id="66d66-178">Start hello app.</span></span> <span data-ttu-id="66d66-179">İlk bir hızlı başlangıç toowalk yoktur size nasıl çalışır.</span><span class="sxs-lookup"><span data-stu-id="66d66-179">There’s an initial Quickstart toowalk you through how it works.</span></span>

### <a name="track-your-trips"></a><span data-ttu-id="66d66-180">Dönüş izleme</span><span class="sxs-lookup"><span data-stu-id="66d66-180">Track your trips</span></span>
<span data-ttu-id="66d66-181">Merhaba kayıt düğmesini (Merhaba ekranında hello sonundaki büyük kırmızı daire) toostart bir seyahat ve yeniden tooend'e dokunun.</span><span class="sxs-lookup"><span data-stu-id="66d66-181">Tap hello record button (big red circle at hello bottom of hello screen) toostart a trip, and tap again tooend.</span></span>

![İzleme seyahat için hello kayıt düğmesini çizimi](./media/iot-solution-get-started/image2.png)

<span data-ttu-id="66d66-183">Hiçbir OBD aygıt ise, bir seyahat her başlattığınızda toouse hello simulator isteyip istemediğinizi istenir.</span><span class="sxs-lookup"><span data-stu-id="66d66-183">Each time you start a trip, if there’s no OBD device, you’ll be asked if you want toouse hello simulator.</span></span>

<span data-ttu-id="66d66-184">Bir seyahat Hello sonunda hello Durdur düğmesine dokunun ve özeti alın.</span><span class="sxs-lookup"><span data-stu-id="66d66-184">At hello end of a trip, tap hello stop button, and you get a summary.</span></span>

![Özet bir seyahat örneği](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a><span data-ttu-id="66d66-186">Dönüş gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="66d66-186">Review your trips</span></span>
![Geçmiş seyahat örneği](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a><span data-ttu-id="66d66-188">Profilinizi gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="66d66-188">Review your profile</span></span>
![Yürüten stili profil örneği](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a><span data-ttu-id="66d66-190">Test Geri bildirimlerinizi bize gönderin</span><span class="sxs-lookup"><span data-stu-id="66d66-190">Send us your test feedback</span></span>
<span data-ttu-id="66d66-191">Kendi IOT sistemleri MyDriving toohelp başkalarından oluşturduğumuz çünkü kesinlikle ne kadar iyi çalıştığı konusunda toohear sizden istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="66d66-191">Because we created MyDriving toohelp jumpstart your own IoT systems, we certainly want toohear from you about how well it works.</span></span> <span data-ttu-id="66d66-192">Varsa bize bildirin:</span><span class="sxs-lookup"><span data-stu-id="66d66-192">Let us know if:</span></span>

* <span data-ttu-id="66d66-193">İlgili sorunlar veya zorluklar çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="66d66-193">You run into difficulties or challenges.</span></span>
* <span data-ttu-id="66d66-194">Daha uygun tooyour senaryo yapacağı bir uzantı noktası yoktur.</span><span class="sxs-lookup"><span data-stu-id="66d66-194">There is an extension point that would make it more suitable tooyour scenario.</span></span>
* <span data-ttu-id="66d66-195">Belirli gereksinimlerini daha verimli bir şekilde tooaccomplish bulun.</span><span class="sxs-lookup"><span data-stu-id="66d66-195">You find a more efficient way tooaccomplish certain needs.</span></span>
* <span data-ttu-id="66d66-196">MyDriving veya bu belgeleri geliştirmek için diğer bir önerileri vardır.</span><span class="sxs-lookup"><span data-stu-id="66d66-196">You have any other suggestions for improving MyDriving or this documentation.</span></span>

<span data-ttu-id="66d66-197">Merhaba MyDriving app içinde kendisi hello yerleşik HockeyApp geri bildirim mekanizması kullanabilirsiniz: yalnızca iOS ve Android cihazlarda telefonunuza bir sallama verin veya hello kullan **geri bildirim** menü komutu.</span><span class="sxs-lookup"><span data-stu-id="66d66-197">Within hello MyDriving app itself, you can use hello built-in HockeyApp feedback mechanism: on iOS and Android, just give your phone a shake, or use hello **Feedback** menu command.</span></span> <span data-ttu-id="66d66-198">Biz hakkında konuşurken bilmeniz böylece bu ekran, otomatik olarak ekleyecek.</span><span class="sxs-lookup"><span data-stu-id="66d66-198">This will automatically attach a screenshot, so that we’ll know what you’re talking about.</span></span> <span data-ttu-id="66d66-199">Ve tüm talihsiz kilitlenme varsa, HockeyApp hello kilitlenme günlükleri tootell bize bunlarla ilgili toplar.</span><span class="sxs-lookup"><span data-stu-id="66d66-199">And if there are any unfortunate crashes, HockeyApp collects hello crash logs tootell us about them.</span></span> <span data-ttu-id="66d66-200">Geri bildirim hello aracılığıyla da verebilirsiniz [HockeyApp portal].</span><span class="sxs-lookup"><span data-stu-id="66d66-200">You can also give feedback through hello [HockeyApp portal].</span></span>

<span data-ttu-id="66d66-201">Ayrıca dosya bir [GitHub sorunu], veya bir yorum yazın (en-us edition).</span><span class="sxs-lookup"><span data-stu-id="66d66-201">You can also file an [issue on GitHub], or leave a comment below (en-us edition).</span></span>

<span data-ttu-id="66d66-202">Toohearing sizden umuyoruz!</span><span class="sxs-lookup"><span data-stu-id="66d66-202">We look forward toohearing from you!</span></span>

## <a name="next-steps"></a><span data-ttu-id="66d66-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="66d66-203">Next steps</span></span>
* <span data-ttu-id="66d66-204">Merhaba keşfedin [MyDriving Başvuru Kılavuzu](http://aka.ms/mydrivingdocs) nasıl artık tasarlanmış ve yerleşik toounderstand hello tüm MyDriving sistem.</span><span class="sxs-lookup"><span data-stu-id="66d66-204">Explore hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) toounderstand how we’ve designed and built hello entire MyDriving system.</span></span>
* <span data-ttu-id="66d66-205">[Bir bir sistem oluşturup](iot-solution-build-system.md) bizim Azure Resource Manager komut dosyalarını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="66d66-205">[Create and deploy a system of your own](iot-solution-build-system.md) by using our Azure Resource Manager scripts.</span></span> <span data-ttu-id="66d66-206">Merhaba [MyDriving Başvuru Kılavuzu](http://aka.ms/mydrivingdocs) Ayrıca, burada yaptığınız hello çoğu özelleştirmeleri alanlarında size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="66d66-206">hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) also guides you through areas where you’ll make hello most customizations.</span></span>

[github'dan]: https://github.com/Azure-Samples/MyDriving
[Xamarin kullanarak]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[BAFX ürünleri 34t5 Bluetooth OBDII Tarama Aracı]: http://www.amazon.com/gp/product/B005NLQAHS
[ScanTool OBDLink MX Wi-Fi: OBD bağdaştırıcısı/tanılama tarayıcı]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[HockeyApp portal]: https://rink.hockeyapp.org
[GitHub sorunu]: https://github.com/Azure-Samples/MyDriving/issues
