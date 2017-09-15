### <a name="grant-access-to-your-push-certificate-to-mobile-engagement"></a><span data-ttu-id="d5aae-101">Anında İletme Sertifikanıza Mobile Engagement için erişim izni verme</span><span class="sxs-lookup"><span data-stu-id="d5aae-101">Grant access to your Push Certificate to Mobile Engagement</span></span>
<span data-ttu-id="d5aae-102">Mobile Engagement’ın sizin adınıza Anında İletme Bildirimleri göndermesine izin vermek için sertifikanıza erişim izni vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d5aae-102">To allow Mobile Engagement to send Push Notifications on your behalf, you need to grant it access to your certificate.</span></span> <span data-ttu-id="d5aae-103">Bu da, sertifikanız yapılandırıp Mobile Engagement portalına girilerek gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d5aae-103">This is done by configuring and entering your certificate into the Mobile Engagement portal.</span></span> <span data-ttu-id="d5aae-104">[Apple belgeleri](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)’nde açıklandığı gibi p12 sertifikanız olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="d5aae-104">Make sure you obtain your .p12 certificate as explained in [Apple's documentation](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

1. <span data-ttu-id="d5aae-105">Mobile Engagement portalınıza gidin.</span><span class="sxs-lookup"><span data-stu-id="d5aae-105">Navigate to your Mobile Engagement portal.</span></span> <span data-ttu-id="d5aae-106">Doğru yerde olduğunuzdan emin olun ve alttaki **Katıl** düğmesine tıklayın:</span><span class="sxs-lookup"><span data-stu-id="d5aae-106">Ensure you're in the correct and then click on the **Engage** button at the bottom:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. <span data-ttu-id="d5aae-107">Engagement Portal’ınızdaki **Ayarlar** sayfasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d5aae-107">Click on the **Settings** page in your Engagement Portal.</span></span> <span data-ttu-id="d5aae-108">Buradan, p12 sertifikanızı yüklemek için **Yerel Gönderim** bölümüne tıklayın:</span><span class="sxs-lookup"><span data-stu-id="d5aae-108">From there click on the **Native Push** section to upload your p12 certificate:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. <span data-ttu-id="d5aae-109">p12 sertifikanızı seçin, bunu yükleyip parolanızı yazın:</span><span class="sxs-lookup"><span data-stu-id="d5aae-109">Select your p12, upload it and type your password:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <span data-ttu-id="d5aae-110"><a id="send"></a>Uygulamanıza bildirim gönderme</span><span class="sxs-lookup"><span data-stu-id="d5aae-110"><a id="send"></a>Send a notification to your app</span></span>
<span data-ttu-id="d5aae-111">Şimdi de, uygulamamıza Anında İletme Bildirimi gönderecek basit bir bildirim kampanyası oluşturacağız:</span><span class="sxs-lookup"><span data-stu-id="d5aae-111">We will now create a simple Push Notification campaign that will send a push to our app:</span></span>

1. <span data-ttu-id="d5aae-112">Mobile Engagement portalınızın **erişim** sekmesine gidin.</span><span class="sxs-lookup"><span data-stu-id="d5aae-112">Navigate to the **Reach** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="d5aae-113">Bildirim kampanyanızı oluşturmak için **Yeni Duyuru**’ya tıklayın</span><span class="sxs-lookup"><span data-stu-id="d5aae-113">Click **New Announcement** to create your push campaign</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. <span data-ttu-id="d5aae-114">Kampanyanızın ilk alanlarını ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="d5aae-114">Setup the first fields of your campaign:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * <span data-ttu-id="d5aae-115">Kampanyanıza bir **Ad** verin</span><span class="sxs-lookup"><span data-stu-id="d5aae-115">Provide a **Name** for your campaign</span></span> 
   * <span data-ttu-id="d5aae-116">**Teslim zamanını**, **Yalnızca uygulama dışında** olarak seçin: Bu, bazı metinleri oluşturan basit Apple anında iletilen bildirim türüdür.</span><span class="sxs-lookup"><span data-stu-id="d5aae-116">Select the **Delivery time** as **Out of app only**: this is the simple Apple push notification type that features some text.</span></span>
   * <span data-ttu-id="d5aae-117">Bildirim metninde önce ilk satır olacak **Başlık** metnini yazın.</span><span class="sxs-lookup"><span data-stu-id="d5aae-117">In the notification text, type first the **Title** which will be the first line in the push.</span></span>
   * <span data-ttu-id="d5aae-118">Sonra da ikinci satır olacak **İleti**’yi yazın</span><span class="sxs-lookup"><span data-stu-id="d5aae-118">Then type your **Message** which will be the second line</span></span>
4. <span data-ttu-id="d5aae-119">Kaydırarak aşağı gidin ve içerik bölümünde **Yalnızca bildirim**’i seçin</span><span class="sxs-lookup"><span data-stu-id="d5aae-119">Scroll down, and in the content section select **Notification only**</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. <span data-ttu-id="d5aae-120">En temel kampanya ayarını bitirdiniz.</span><span class="sxs-lookup"><span data-stu-id="d5aae-120">You're done setting the most basic campaign.</span></span> <span data-ttu-id="d5aae-121">Şimdi aşağıya kayın ve anında iletme bildirimi kampanyanızı kaydetmek için **Oluştur** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d5aae-121">Now scroll down and click on **Create** button to save your push notification campaign.</span></span> 
6. <span data-ttu-id="d5aae-122">Son olarak, anında iletme bildirimini göndermek için **Etkinleştir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d5aae-122">Finally - click on **Activate** to send push notification.</span></span> 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. <span data-ttu-id="d5aae-123">Bildirim merkezinde, iOS cihazınızdaki bildirimi aşağıdaki gibi alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d5aae-123">You will be able receive the notification on your iOS device in the notification center like the following:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. <span data-ttu-id="d5aae-124">Bu iOS cihazıyla eşleştirilmiş bir Apple Watch’unuz varsa, Apple Watch’unuzda bildirimi görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="d5aae-124">If you have an Apple Watch paired with this iOS device then you will see the notification on your Apple Watch:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

