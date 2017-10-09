#### <a name="configure-hello-ios-project-in-xamarin-studio"></a><span data-ttu-id="41a78-101">Xamarin Studio'da Hello iOS projesi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="41a78-101">Configure hello iOS project in Xamarin Studio</span></span>
1. <span data-ttu-id="41a78-102">Xamarin.Studio içinde açmak **Info.plist**ve güncelleştirme hello **paket tanımlayıcısı** yeni uygulama kimliğiniz ile daha önce oluşturduğunuz kimliği ile Merhaba paketini</span><span class="sxs-lookup"><span data-stu-id="41a78-102">In Xamarin.Studio, open **Info.plist**, and update hello **Bundle Identifier** with hello bundle ID that you created earlier with your new app ID.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. <span data-ttu-id="41a78-103">Çok ilerleyin**arka plan modları**.</span><span class="sxs-lookup"><span data-stu-id="41a78-103">Scroll down too**Background Modes**.</span></span> <span data-ttu-id="41a78-104">Select hello **arka plan modlarını etkinleştir** kutusu ve hello **uzak bildirimler** kutusu.</span><span class="sxs-lookup"><span data-stu-id="41a78-104">Select hello **Enable Background Modes** box and hello **Remote notifications** box.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. <span data-ttu-id="41a78-105">Merhaba çözüm paneli tooopen projenizde çift **proje seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="41a78-105">Double-click your project in hello Solution Panel tooopen **Project Options**.</span></span>
4. <span data-ttu-id="41a78-106">Altında **yapı**, seçin **iOS paket imzalama**, select hello karşılık gelen kimliği ve sağlama profiliniz, yalnızca bu proje için ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="41a78-106">Under **Build**, choose **iOS Bundle Signing**, and select hello corresponding identity and provisioning profile you just set up for this project.</span></span>

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   <span data-ttu-id="41a78-107">Bu kod imzalama için hello proje hello yeni profili kullanan sağlar.</span><span class="sxs-lookup"><span data-stu-id="41a78-107">This ensures that hello project uses hello new profile for code signing.</span></span> <span data-ttu-id="41a78-108">Belge hello resmi Xamarin cihaz sağlama için bkz: [Xamarin cihaz sağlamayı].</span><span class="sxs-lookup"><span data-stu-id="41a78-108">For hello official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>

#### <a name="configure-hello-ios-project-in-visual-studio"></a><span data-ttu-id="41a78-109">Visual Studio'da Hello iOS projesi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="41a78-109">Configure hello iOS project in Visual Studio</span></span>
1. <span data-ttu-id="41a78-110">Visual Studio'da hello projesine sağ tıklayın ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="41a78-110">In Visual Studio, right-click hello project, and then click **Properties**.</span></span>
2. <span data-ttu-id="41a78-111">Merhaba özellikler sayfalarında hello tıklatın **iOS uygulama** sekmesi ve güncelleştirme hello **tanımlayıcısı** daha önce oluşturduğunuz hello Kimliğine sahip.</span><span class="sxs-lookup"><span data-stu-id="41a78-111">In hello properties pages, click hello **iOS Application** tab, and update hello **Identifier** with hello ID that you created earlier.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. <span data-ttu-id="41a78-112">Merhaba, **iOS paket imzalama** sekmesinde, select hello karşılık gelen kimliği ve sağlama profili, ayarladığınız yukarı bu proje için.</span><span class="sxs-lookup"><span data-stu-id="41a78-112">In hello **iOS Bundle Signing** tab, select hello corresponding identity and provisioning profile you just set up for this project.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    <span data-ttu-id="41a78-113">Bu kod imzalama için hello proje hello yeni profili kullanan sağlar.</span><span class="sxs-lookup"><span data-stu-id="41a78-113">This ensures that hello project uses hello new profile for code signing.</span></span> <span data-ttu-id="41a78-114">Belge hello resmi Xamarin cihaz sağlama için bkz: [Xamarin cihaz sağlamayı].</span><span class="sxs-lookup"><span data-stu-id="41a78-114">For hello official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>
4. <span data-ttu-id="41a78-115">Info.plist tooopen çift tıklayın ve ardından Etkinleştir **RemoteNotifications** altında **arka plan modları**.</span><span class="sxs-lookup"><span data-stu-id="41a78-115">Double-click Info.plist tooopen it, and then enable **RemoteNotifications** under **Background Modes**.</span></span>

[Xamarin cihaz sağlamayı]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/
