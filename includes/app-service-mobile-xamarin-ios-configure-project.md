#### <a name="configure-the-ios-project-in-xamarin-studio"></a><span data-ttu-id="fd9b7-101">Xamarin Studio'da iOS projesi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fd9b7-101">Configure the iOS project in Xamarin Studio</span></span>
1. <span data-ttu-id="fd9b7-102">Xamarin.Studio içinde açmak **Info.plist**ve güncelleştirme **paket tanımlayıcısı** yeni uygulama kimliğiniz ile daha önce oluşturduğunuz paket kimliği</span><span class="sxs-lookup"><span data-stu-id="fd9b7-102">In Xamarin.Studio, open **Info.plist**, and update the **Bundle Identifier** with the bundle ID that you created earlier with your new app ID.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. <span data-ttu-id="fd9b7-103">Ekranı aşağı kaydırarak **arka plan modları**.</span><span class="sxs-lookup"><span data-stu-id="fd9b7-103">Scroll down to **Background Modes**.</span></span> <span data-ttu-id="fd9b7-104">Seçin **arka plan modlarını etkinleştir** kutusu ve **uzak bildirimler** kutusu.</span><span class="sxs-lookup"><span data-stu-id="fd9b7-104">Select the **Enable Background Modes** box and the **Remote notifications** box.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. <span data-ttu-id="fd9b7-105">Projenizi açmak için çözüm panelinde çift **proje seçenekleri**.</span><span class="sxs-lookup"><span data-stu-id="fd9b7-105">Double-click your project in the Solution Panel to open **Project Options**.</span></span>
4. <span data-ttu-id="fd9b7-106">Altında **yapı**, seçin **iOS paket imzalama**, karşılık gelen kimliği seçin ve sağlama profili, ayarladığınız yukarı bu proje için.</span><span class="sxs-lookup"><span data-stu-id="fd9b7-106">Under **Build**, choose **iOS Bundle Signing**, and select the corresponding identity and provisioning profile you just set up for this project.</span></span>

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   <span data-ttu-id="fd9b7-107">Bu kod imzalama için proje yeni profili kullanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="fd9b7-107">This ensures that the project uses the new profile for code signing.</span></span> <span data-ttu-id="fd9b7-108">Belge sağlama resmi Xamarin aygıt için bkz: [Xamarin cihaz sağlamayı].</span><span class="sxs-lookup"><span data-stu-id="fd9b7-108">For the official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>

#### <a name="configure-the-ios-project-in-visual-studio"></a><span data-ttu-id="fd9b7-109">Visual Studio'da iOS projesi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fd9b7-109">Configure the iOS project in Visual Studio</span></span>
1. <span data-ttu-id="fd9b7-110">Visual Studio'da projeye sağ tıklayın ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="fd9b7-110">In Visual Studio, right-click the project, and then click **Properties**.</span></span>
2. <span data-ttu-id="fd9b7-111">Özellikler sayfalarında tıklatın **iOS uygulama** sekmesini tıklatın ve güncelleştirme **tanımlayıcısı** daha önce oluşturduğunuz kimliği.</span><span class="sxs-lookup"><span data-stu-id="fd9b7-111">In the properties pages, click the **iOS Application** tab, and update the **Identifier** with the ID that you created earlier.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. <span data-ttu-id="fd9b7-112">İçinde **iOS paket imzalama** sekmesinde, karşılık gelen kimliği seçin ve sağlama profili yalnızca ayarladığınız bu proje için.</span><span class="sxs-lookup"><span data-stu-id="fd9b7-112">In the **iOS Bundle Signing** tab, select the corresponding identity and provisioning profile you just set up for this project.</span></span>

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    <span data-ttu-id="fd9b7-113">Bu kod imzalama için proje yeni profili kullanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="fd9b7-113">This ensures that the project uses the new profile for code signing.</span></span> <span data-ttu-id="fd9b7-114">Belge sağlama resmi Xamarin aygıt için bkz: [Xamarin cihaz sağlamayı].</span><span class="sxs-lookup"><span data-stu-id="fd9b7-114">For the official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>
4. <span data-ttu-id="fd9b7-115">Dosyayı açın ve ardından etkinleştirmek için Info.plist çift **RemoteNotifications** altında **arka plan modları**.</span><span class="sxs-lookup"><span data-stu-id="fd9b7-115">Double-click Info.plist to open it, and then enable **RemoteNotifications** under **Background Modes**.</span></span>

<span data-ttu-id="fd9b7-116">[Xamarin cihaz sağlamayı]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/</span><span class="sxs-lookup"><span data-stu-id="fd9b7-116">[Xamarin Device Provisioning]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/</span></span>
