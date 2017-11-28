---
title: "MyDriving Azure IOT örnek: Hızlı Başlangıç | Microsoft Docs"
description: "Akış analizi, Machine Learning ve olay hub'ları da dahil olmak üzere Microsoft Azure kullanarak bir IOT sistemi mimari konusunda kapsamlı bir örnek bir uygulama kullanmaya başlayın."
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
ms.openlocfilehash: 031b492df1f186087e7b91102cbb44f552999293
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="mydriving-iot-system-quick-start"></a><span data-ttu-id="47666-103">MyDriving IOT sistem: Hızlı Başlangıç</span><span class="sxs-lookup"><span data-stu-id="47666-103">MyDriving IoT system: Quick start</span></span>
<span data-ttu-id="47666-104">MyDriving sistemidir tasarımını ve uygulamasını tipik bir gösteren bir [nesnelerin interneti](iot-suite-overview.md) telemetri cihazlardan toplar (IOT) çözümü bu verileri bulutta işler ve makine sağlamak öğrenme geçerlidir bir Uyarlamalı yanıt.</span><span class="sxs-lookup"><span data-stu-id="47666-104">MyDriving is a system that demonstrates the design and implementation of a typical [Internet of Things](iot-suite-overview.md) (IoT) solution that gathers telemetry from devices, processes that data in the cloud, and applies machine learning to provide an adaptive response.</span></span> <span data-ttu-id="47666-105">Tanıtım cep telefonunuzu ve arabanızın denetim sisteminden bilgileri toplayan bir bağdaştırıcı verilerini kullanarak, car dönüşleri hakkındaki verileri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="47666-105">The demonstration logs data about your car trips, by using data from both your mobile phone and an adapter that collects information from your car’s control system.</span></span> <span data-ttu-id="47666-106">Diğer kullanıcıların kıyasla yönlendirmeli stilinize hakkında geri bildirim sağlamak için bu verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="47666-106">It uses this data to provide feedback on your driving style in comparison to other users.</span></span>

<span data-ttu-id="47666-107">MyDriving gerçek amacı, kendi IOT çözümünüzü oluştururken başlamanıza yardımcı olmaktır.</span><span class="sxs-lookup"><span data-stu-id="47666-107">The real purpose of MyDriving is to get you started in creating your own IoT solution.</span></span> <span data-ttu-id="47666-108">Ancak, önce şimdi, uygulamayla MyDriving kendisini--test kullanıcı ekibimiz üyesi olarak yapmalarını.</span><span class="sxs-lookup"><span data-stu-id="47666-108">But before that, let’s get you going with the MyDriving app itself--as a member of our test user team.</span></span> <span data-ttu-id="47666-109">Mimariye inceleyin önce bu uygulamanın ve bunun arkasındaki sistem bir tüketici olarak bir deneyim sağlar.</span><span class="sxs-lookup"><span data-stu-id="47666-109">This gives you an experience of the app and the system behind it as a consumer, before you delve into the architecture.</span></span> <span data-ttu-id="47666-110">Bu aynı zamanda, HockeyApp, kullanıcılar test uygulamalarınızın alfa, beta dağıtımları yönetme cool olanağı sunar.</span><span class="sxs-lookup"><span data-stu-id="47666-110">It also introduces you to HockeyApp, a cool way of managing the alpha and beta distributions of your apps to test users.</span></span>

## <a name="use-the-mobile-experience"></a><span data-ttu-id="47666-111">Mobil deneyimi kullanın</span><span class="sxs-lookup"><span data-stu-id="47666-111">Use the mobile experience</span></span>
<span data-ttu-id="47666-112">Android, iOS veya Windows 10 cihaz varsa MyDriving uygulamasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47666-112">You can use the MyDriving app if you have an Android, iOS, or Windows 10 device.</span></span>

### <a name="android-and-windows-10-mobile-installation"></a><span data-ttu-id="47666-113">Android ve Windows 10 Mobile yükleme</span><span class="sxs-lookup"><span data-stu-id="47666-113">Android and Windows 10 Mobile installation</span></span>
<span data-ttu-id="47666-114">Cihazınızda:</span><span class="sxs-lookup"><span data-stu-id="47666-114">On your device:</span></span>

1. <span data-ttu-id="47666-115">Geliştirme uygulamaları izin ver:</span><span class="sxs-lookup"><span data-stu-id="47666-115">Allow development apps:</span></span>
   
   * <span data-ttu-id="47666-116">Android: İçinde **ayarları** > **güvenlik**, uygulamalardan izin **bilinmeyen kaynaklardan**.</span><span class="sxs-lookup"><span data-stu-id="47666-116">Android: In **Settings** > **Security**, allow apps from **Unknown sources**.</span></span>
   * <span data-ttu-id="47666-117">: Windows 10 **ayarları** > **güncelleştirmeleri** > **geliştiriciler için**ayarlayın **geliştirici modunu**.</span><span class="sxs-lookup"><span data-stu-id="47666-117">Windows 10: In **Settings** > **Updates** > **For Developers**, set **Developer mode**.</span></span>
2. <span data-ttu-id="47666-118">İle kaydolduktan ya da, oturum açma tarafından beta test ekibimiz katılma [HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="47666-118">Join our beta test team by signing up with, or signing in to, [HockeyApp](https://rink.hockeyapp.net).</span></span> <span data-ttu-id="47666-119">HockeyApp kullanıcılar test etmek için uygulamanızın sürümleri erken dağıtmak kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="47666-119">HockeyApp makes it easy to distribute early releases of your app to test users.</span></span>
   
   <span data-ttu-id="47666-120">Windows 10 kullanıyorsanız, Edge tarayıcısını kullanın.</span><span class="sxs-lookup"><span data-stu-id="47666-120">If you’re using Windows 10, use the Edge browser.</span></span>
   
   <span data-ttu-id="47666-121">Build 2016 katılımcı olsaydı, Microsoft'un düğmeler birini kullanarak konferans için kayıtlı aynı Microsoft hesabı e-posta oturum açın.</span><span class="sxs-lookup"><span data-stu-id="47666-121">If you were a Build 2016 attendee, sign in with the same Microsoft account email that you registered for the conference, by using one of the Microsoft buttons.</span></span> <span data-ttu-id="47666-122">HockeyApp ile zaten kaydolmuşsunuz.</span><span class="sxs-lookup"><span data-stu-id="47666-122">You’re already signed up with HockeyApp.</span></span>
   
   ![HockeyApp oturum açma ekranı](./media/iot-solution-get-started/image1.png)
3. <span data-ttu-id="47666-124">Karşıdan yükleme ve uygulamayı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="47666-124">Download and install the app from here:</span></span>
   
   * [<span data-ttu-id="47666-125">Android</span><span class="sxs-lookup"><span data-stu-id="47666-125">Android</span></span>](http://rink.io/spMyDrivingAndroid)
   * [<span data-ttu-id="47666-126">Windows 10</span><span class="sxs-lookup"><span data-stu-id="47666-126">Windows 10</span></span>](http://rink.io/spMyDrivingUWP)
   
   <span data-ttu-id="47666-127">İki öğe yok.</span><span class="sxs-lookup"><span data-stu-id="47666-127">There are two items.</span></span> <span data-ttu-id="47666-128">Yüklemek **güvenilir kişiler**.</span><span class="sxs-lookup"><span data-stu-id="47666-128">Install the certificate in **Trusted People**.</span></span> <span data-ttu-id="47666-129">Daha sonra uygulamayı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="47666-129">Then install the app.</span></span>

<span data-ttu-id="47666-130">*Windows 10 Mobile uygulama başlatma sorunları?*</span><span class="sxs-lookup"><span data-stu-id="47666-130">*Any issues starting the app on Windows 10 Mobile?*</span></span> <span data-ttu-id="47666-131">Telefonunuza bir güncelleştirme veya iki arkasında olabilir.</span><span class="sxs-lookup"><span data-stu-id="47666-131">Your phone might be an update or two behind.</span></span> <span data-ttu-id="47666-132">En son güncelleştirmeleri olduğuna emin olun veya yükleyin:</span><span class="sxs-lookup"><span data-stu-id="47666-132">Make sure you've got the latest updates, or install:</span></span>

* [<span data-ttu-id="47666-133">Microsoft.NET.Native.Framework.1.2.appx</span><span class="sxs-lookup"><span data-stu-id="47666-133">Microsoft.NET.Native.Framework.1.2.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [<span data-ttu-id="47666-134">Microsoft.NET.Native.Runtime.1.1.appx</span><span class="sxs-lookup"><span data-stu-id="47666-134">Microsoft.NET.Native.Runtime.1.1.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [<span data-ttu-id="47666-135">Microsoft.VCLibs.ARM.14.00.appx</span><span class="sxs-lookup"><span data-stu-id="47666-135">Microsoft.VCLibs.ARM.14.00.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a><span data-ttu-id="47666-136">iOS yükleme</span><span class="sxs-lookup"><span data-stu-id="47666-136">iOS installation</span></span>
<span data-ttu-id="47666-137">Build 2016 gittiğiniz, uygulamayı test ekibimiz HockeyApp üzerinde bir üyesi olarak karşıdan yükleyin:</span><span class="sxs-lookup"><span data-stu-id="47666-137">If you attended Build 2016, download the app as a member of our test team on HockeyApp:</span></span>

1. <span data-ttu-id="47666-138">İOS Cihazınızda oturum [HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="47666-138">On your iOS device, sign in to [HockeyApp](https://rink.hockeyapp.net).</span></span>
   <span data-ttu-id="47666-139">Microsoft'un oturum açma düğmeler ve konferans kayıtlı aynı Microsoft hesabı e-posta ile oturum birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="47666-139">Use one of the Microsoft sign-in buttons, and sign in with the same Microsoft account email that you registered with the conference.</span></span> <span data-ttu-id="47666-140">(E-posta ve parola alanlarına kullanmayın.)</span><span class="sxs-lookup"><span data-stu-id="47666-140">(Don’t use the email and password fields.)</span></span>
   
   ![HockeyApp oturum açma ekranı](./media/iot-solution-get-started/image1.png)
2. <span data-ttu-id="47666-142">HockeyApp panosunda MyDriving seçin ve indirin.</span><span class="sxs-lookup"><span data-stu-id="47666-142">In the HockeyApp dashboard, select MyDriving and download it.</span></span>
3. <span data-ttu-id="47666-143">HockeyApp beta sürümünden yetkilendirin.</span><span class="sxs-lookup"><span data-stu-id="47666-143">Authorize the beta release from HockeyApp:</span></span>
   
   <span data-ttu-id="47666-144">a.</span><span class="sxs-lookup"><span data-stu-id="47666-144">a.</span></span> <span data-ttu-id="47666-145">Git **ayarları** > **genel** > **profilleri ve aygıt yönetimi.**</span><span class="sxs-lookup"><span data-stu-id="47666-145">Go to **Settings** > **General** > **Profiles and Device Management.**</span></span>
   
   <span data-ttu-id="47666-146">b.</span><span class="sxs-lookup"><span data-stu-id="47666-146">b.</span></span> <span data-ttu-id="47666-147">Güven **Bit stadyum GmbH** sertifika.</span><span class="sxs-lookup"><span data-stu-id="47666-147">Trust the **Bit Stadium GmbH** certificate.</span></span>

<span data-ttu-id="47666-148">Build 2016 gitmediğiniz, derleme ve uygulamayı kendiniz dağıtın:</span><span class="sxs-lookup"><span data-stu-id="47666-148">If you didn’t attend Build 2016, you can build and deploy the app yourself:</span></span>

1. <span data-ttu-id="47666-149">Kodu indirme [github'dan].</span><span class="sxs-lookup"><span data-stu-id="47666-149">Download the code [from GitHub].</span></span>
2. <span data-ttu-id="47666-150">Derleme ve tarafından dağıtma [Xamarin kullanarak].</span><span class="sxs-lookup"><span data-stu-id="47666-150">Build and deploy by [using Xamarin].</span></span>

<span data-ttu-id="47666-151">Daha ayrıntılı olarak Bul [MyDriving Başvuru Kılavuzu](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="47666-151">Find more details in the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="get-an-obd-adapter-optional"></a><span data-ttu-id="47666-152">OBD bağdaştırıcıyı (isteğe bağlı) Al</span><span class="sxs-lookup"><span data-stu-id="47666-152">Get an OBD adapter (optional)</span></span>
<span data-ttu-id="47666-153">Bu gerçek bir nesnelerin interneti sistem yapan bölümüdür!</span><span class="sxs-lookup"><span data-stu-id="47666-153">This is the part that makes this a real Internet of Things system!</span></span> <span data-ttu-id="47666-154">Uygulama, olmadan kullanabilirsiniz ancak daha fazla keyif gerçek bir şey olduğunu ve pahalı olmayan.</span><span class="sxs-lookup"><span data-stu-id="47666-154">You can use the app without one, but it’s more fun with the real thing, and they aren’t expensive.</span></span>

<span data-ttu-id="47666-155">Yerleşik tanılama (OBD), car ayarlamak ve tek sesleri ve uyarı ampul tanılamak için Garaj kullanır, car özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="47666-155">On-board diagnostics (OBD) is the feature of your car that the garage uses to tune up your car and diagnose odd noises and warning lamps.</span></span> <span data-ttu-id="47666-156">Car harika antiquity olmadıkça, genellikle bir flap Pano altında arkasında kabini yuva yere bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47666-156">Unless your car is of great antiquity, you’ll find a socket somewhere in the cabin, typically behind a flap under the dashboard.</span></span> <span data-ttu-id="47666-157">Sağ bağlayıcısıyla altyapının performans ölçümlerini alın ve belirli ayarlamalar yapın.</span><span class="sxs-lookup"><span data-stu-id="47666-157">With the right connector, you can get metrics of the engine’s performance and make certain adjustments.</span></span> <span data-ttu-id="47666-158">Bir OBD Bağlayıcısı ailenin normal yerlerden satın alınabilir.</span><span class="sxs-lookup"><span data-stu-id="47666-158">An OBD connector can be purchased cheaply from the usual places.</span></span> <span data-ttu-id="47666-159">Bu, Bluetooth veya Wi-Fi telefonunuzda bir uygulama kullanarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="47666-159">It connects by using Bluetooth or Wi-Fi to an app on your phone.</span></span>

<span data-ttu-id="47666-160">Bu durumda, car bulutunun bağlanacağı yapacağız.</span><span class="sxs-lookup"><span data-stu-id="47666-160">In this case, we’re going to connect your car to the cloud.</span></span> <span data-ttu-id="47666-161">OBD doğrudan bağlantı için telefonunuza olsa da, uygulamamıza geçişi olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="47666-161">The direct connection from the OBD is to your phone, but our app works as a relay.</span></span> <span data-ttu-id="47666-162">Arabanızın telemetri düz MyDriving IOT hub'ına yol dönüşleri oturum ve yönlendirmeli stilinize değerlendirmek için işleneceği gönderilir.</span><span class="sxs-lookup"><span data-stu-id="47666-162">Your car's telemetry is sent straight to the MyDriving IoT hub, where it's processed to log your road trips and assess your driving style.</span></span>

<span data-ttu-id="47666-163">Bir OBD aygıtı bağlamak için:</span><span class="sxs-lookup"><span data-stu-id="47666-163">To connect an OBD device:</span></span>

1. <span data-ttu-id="47666-164">Car OBD yuva olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="47666-164">Check that your car has an OBD socket.</span></span>
2. <span data-ttu-id="47666-165">OBD bağdaştırıcıyı alın:</span><span class="sxs-lookup"><span data-stu-id="47666-165">Obtain an OBD adapter:</span></span>
   
   * <span data-ttu-id="47666-166">Bir Android veya Windows phone kullanıyorsanız, Bluetooth özellikli OBD II bağdaştırıcısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="47666-166">If you're using an Android or Windows phone, you need a Bluetooth-enabled OBD II adapter.</span></span> <span data-ttu-id="47666-167">Kullandık [BAFX ürünleri 34t5 Bluetooth OBDII Tarama Aracı].</span><span class="sxs-lookup"><span data-stu-id="47666-167">We used [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span></span>
   * <span data-ttu-id="47666-168">Bir iOS telefon kullanıyorsanız, bir Wi-Fi etkin OBD bağdaştırıcısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="47666-168">If you're using an iOS phone, you need a Wi-Fi-enabled OBD adapter.</span></span> <span data-ttu-id="47666-169">Kullandık [ScanTool OBDLink MX Wi-Fi: OBD bağdaştırıcısı/tanılama tarayıcı].</span><span class="sxs-lookup"><span data-stu-id="47666-169">We used [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].</span></span>
3. <span data-ttu-id="47666-170">Telefonunuza bağlanmak için OBD bağdaştırıcınızı birlikte gelen yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="47666-170">Follow the instructions that come with your OBD adapter to connect it to your phone.</span></span> <span data-ttu-id="47666-171">Aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="47666-171">Keep the following in mind:</span></span>
   
   * <span data-ttu-id="47666-172">Üzerinde telefon ile eşleştirilmelidir Bluetooth bağdaştırıcısı **ayarları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="47666-172">A Bluetooth adapter must be paired with the phone, on the **Settings** page.</span></span>
   * <span data-ttu-id="47666-173">Bir Wi-Fi bağdaştırıcısı adres aralığı 192.168.xxx.xxx olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="47666-173">A Wi-Fi adapter must have an address in the range 192.168.xxx.xxx.</span></span>
4. <span data-ttu-id="47666-174">Çeşitli otomobiller varsa, her (en fazla üç için) ayrı bir bağdaştırıcı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47666-174">If you have several cars, you can get a separate adapter for each (maximum of three).</span></span>

<span data-ttu-id="47666-175">OBD bağdaştırıcıyı sahip değilseniz, uygulama konumu ve hız veri arka ucuna telefonun GPS alıcısından hala gönderir ve bir OBD benzetimini yapmak isteyip istemediğinizi sorar.</span><span class="sxs-lookup"><span data-stu-id="47666-175">If you don’t have an OBD adapter, the app will still send location and speed data from the phone's GPS receiver to the back end and will ask if you want to simulate an OBD.</span></span>

<span data-ttu-id="47666-176">Bölüm 2.1, "IOT cihazları," kendi OBD cihaz oluşturmak için seçenekler ve uygulama OBD bağdaştırıcısı verileri nasıl kullandığı hakkında daha fazla bulabilirsiniz [MyDriving Başvuru Kılavuzu](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="47666-176">You can find out more about how the app uses data from the OBD adapter and about options for creating your own OBD device in section 2.1, "IoT Devices," in the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="use-the-app"></a><span data-ttu-id="47666-177">Uygulamasını kullanma</span><span class="sxs-lookup"><span data-stu-id="47666-177">Use the app</span></span>
<span data-ttu-id="47666-178">Uygulamayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="47666-178">Start the app.</span></span> <span data-ttu-id="47666-179">Bir başlangıç hızlı başlangıç nasıl çalıştığını aracılığıyla yol yoktur.</span><span class="sxs-lookup"><span data-stu-id="47666-179">There’s an initial Quickstart to walk you through how it works.</span></span>

### <a name="track-your-trips"></a><span data-ttu-id="47666-180">Dönüş izleme</span><span class="sxs-lookup"><span data-stu-id="47666-180">Track your trips</span></span>
<span data-ttu-id="47666-181">Bir seyahat başlatmak için (ekranın en büyük kırmızı daire) kaydı düğmesine dokunun ve sonuna yeniden dokunun.</span><span class="sxs-lookup"><span data-stu-id="47666-181">Tap the record button (big red circle at the bottom of the screen) to start a trip, and tap again to end.</span></span>

![İzleme seyahat için Kaydet düğmesine çizimi](./media/iot-solution-get-started/image2.png)

<span data-ttu-id="47666-183">Hiçbir OBD aygıt ise, bir seyahat her başlattığınızda, simulator kullanmak isteyip istemediğinizi istenir.</span><span class="sxs-lookup"><span data-stu-id="47666-183">Each time you start a trip, if there’s no OBD device, you’ll be asked if you want to use the simulator.</span></span>

<span data-ttu-id="47666-184">Bir seyahat sonunda durdur düğmesine dokunun ve özeti alın.</span><span class="sxs-lookup"><span data-stu-id="47666-184">At the end of a trip, tap the stop button, and you get a summary.</span></span>

![Özet bir seyahat örneği](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a><span data-ttu-id="47666-186">Dönüş gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="47666-186">Review your trips</span></span>
![Geçmiş seyahat örneği](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a><span data-ttu-id="47666-188">Profilinizi gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="47666-188">Review your profile</span></span>
![Yürüten stili profil örneği](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a><span data-ttu-id="47666-190">Test Geri bildirimlerinizi bize gönderin</span><span class="sxs-lookup"><span data-stu-id="47666-190">Send us your test feedback</span></span>
<span data-ttu-id="47666-191">Azure'daki yardımcı olmak için MyDriving kendi IOT sistemleri oluşturduğundan kesinlikle ne kadar iyi çalıştığı hakkında görüşlerinizi istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="47666-191">Because we created MyDriving to help jumpstart your own IoT systems, we certainly want to hear from you about how well it works.</span></span> <span data-ttu-id="47666-192">Varsa bize bildirin:</span><span class="sxs-lookup"><span data-stu-id="47666-192">Let us know if:</span></span>

* <span data-ttu-id="47666-193">İlgili sorunlar veya zorluklar çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="47666-193">You run into difficulties or challenges.</span></span>
* <span data-ttu-id="47666-194">Senaryonuz için daha uygun hale bir uzantı noktası yoktur.</span><span class="sxs-lookup"><span data-stu-id="47666-194">There is an extension point that would make it more suitable to your scenario.</span></span>
* <span data-ttu-id="47666-195">Belirli gereksinimleri gerçekleştirmek için daha verimli bir şekilde bulur.</span><span class="sxs-lookup"><span data-stu-id="47666-195">You find a more efficient way to accomplish certain needs.</span></span>
* <span data-ttu-id="47666-196">MyDriving veya bu belgeleri geliştirmek için diğer bir önerileri vardır.</span><span class="sxs-lookup"><span data-stu-id="47666-196">You have any other suggestions for improving MyDriving or this documentation.</span></span>

<span data-ttu-id="47666-197">MyDriving uygulama içinde yerleşik HockeyApp geri bildirim mekanizması kullanabilirsiniz: yalnızca iOS ve Android cihazlarda telefonunuza bir sallama verin veya kullanmak **geri bildirim** menü komutu.</span><span class="sxs-lookup"><span data-stu-id="47666-197">Within the MyDriving app itself, you can use the built-in HockeyApp feedback mechanism: on iOS and Android, just give your phone a shake, or use the **Feedback** menu command.</span></span> <span data-ttu-id="47666-198">Biz hakkında konuşurken bilmeniz böylece bu ekran, otomatik olarak ekleyecek.</span><span class="sxs-lookup"><span data-stu-id="47666-198">This will automatically attach a screenshot, so that we’ll know what you’re talking about.</span></span> <span data-ttu-id="47666-199">Ve tüm talihsiz kilitlenme varsa, bunları hakkında bize iletmek için kilitlenme günlükleri HockeyApp toplar.</span><span class="sxs-lookup"><span data-stu-id="47666-199">And if there are any unfortunate crashes, HockeyApp collects the crash logs to tell us about them.</span></span> <span data-ttu-id="47666-200">Geri bildirim aracılığıyla da verebilirsiniz [HockeyApp portal].</span><span class="sxs-lookup"><span data-stu-id="47666-200">You can also give feedback through the [HockeyApp portal].</span></span>

<span data-ttu-id="47666-201">Ayrıca dosya bir [GitHub sorunu], veya bir yorum yazın (en-us edition).</span><span class="sxs-lookup"><span data-stu-id="47666-201">You can also file an [issue on GitHub], or leave a comment below (en-us edition).</span></span>

<span data-ttu-id="47666-202">İşitme için sizden umuyoruz!</span><span class="sxs-lookup"><span data-stu-id="47666-202">We look forward to hearing from you!</span></span>

## <a name="next-steps"></a><span data-ttu-id="47666-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="47666-203">Next steps</span></span>
* <span data-ttu-id="47666-204">Araştır [MyDriving Başvuru Kılavuzu](http://aka.ms/mydrivingdocs) nasıl artık tasarlanmış ve tüm MyDriving sistem yerleşik anlamak için.</span><span class="sxs-lookup"><span data-stu-id="47666-204">Explore the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) to understand how we’ve designed and built the entire MyDriving system.</span></span>
* <span data-ttu-id="47666-205">[Bir bir sistem oluşturup](iot-solution-build-system.md) bizim Azure Resource Manager komut dosyalarını kullanarak.</span><span class="sxs-lookup"><span data-stu-id="47666-205">[Create and deploy a system of your own](iot-solution-build-system.md) by using our Azure Resource Manager scripts.</span></span> <span data-ttu-id="47666-206">[MyDriving Başvuru Kılavuzu](http://aka.ms/mydrivingdocs) ayrıca yapacağınız en özelleştirmeleri alanlarında sırasında size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="47666-206">The [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) also guides you through areas where you’ll make the most customizations.</span></span>

<span data-ttu-id="47666-207">[github'dan]: https://github.com/Azure-Samples/MyDriving</span><span class="sxs-lookup"><span data-stu-id="47666-207">[from GitHub]: https://github.com/Azure-Samples/MyDriving</span></span>
<span data-ttu-id="47666-208">[Xamarin kullanarak]: https://developer.xamarin.com/guides/ios/getting_started/installation/</span><span class="sxs-lookup"><span data-stu-id="47666-208">[using Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/</span></span>
<span data-ttu-id="47666-209">[BAFX ürünleri 34t5 Bluetooth OBDII Tarama Aracı]: http://www.amazon.com/gp/product/B005NLQAHS</span><span class="sxs-lookup"><span data-stu-id="47666-209">[BAFX Products 34t5 Bluetooth OBDII Scan Tool]: http://www.amazon.com/gp/product/B005NLQAHS</span></span>
<span data-ttu-id="47666-210">[ScanTool OBDLink MX Wi-Fi: OBD bağdaştırıcısı/tanılama tarayıcı]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP</span><span class="sxs-lookup"><span data-stu-id="47666-210">[ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP</span></span>
<span data-ttu-id="47666-211">[HockeyApp portal]: https://rink.hockeyapp.org</span><span class="sxs-lookup"><span data-stu-id="47666-211">[HockeyApp portal]: https://rink.hockeyapp.org</span></span>
<span data-ttu-id="47666-212">[GitHub sorunu]: https://github.com/Azure-Samples/MyDriving/issues</span><span class="sxs-lookup"><span data-stu-id="47666-212">[issue on GitHub]: https://github.com/Azure-Samples/MyDriving/issues</span></span>
