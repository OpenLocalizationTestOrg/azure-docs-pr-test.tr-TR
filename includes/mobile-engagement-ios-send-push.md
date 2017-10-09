### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a><span data-ttu-id="91a3b-101">GRANT erişim tooyour anında sertifika tooMobile katılım</span><span class="sxs-lookup"><span data-stu-id="91a3b-101">Grant access tooyour Push Certificate tooMobile Engagement</span></span>
<span data-ttu-id="91a3b-102">sizin adınıza tooallow Mobile Engagement toosend anında iletme bildirimleri, tooyour sertifika erişim toogrant gerekir.</span><span class="sxs-lookup"><span data-stu-id="91a3b-102">tooallow Mobile Engagement toosend Push Notifications on your behalf, you need toogrant it access tooyour certificate.</span></span> <span data-ttu-id="91a3b-103">Bu, yapılandırarak ve sertifikanızı hello Mobile Engagement portalına girilerek gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="91a3b-103">This is done by configuring and entering your certificate into hello Mobile Engagement portal.</span></span> <span data-ttu-id="91a3b-104">[Apple belgeleri](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)’nde açıklandığı gibi p12 sertifikanız olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="91a3b-104">Make sure you obtain your .p12 certificate as explained in [Apple's documentation](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

1. <span data-ttu-id="91a3b-105">Tooyour Mobile Engagement portalına gidin.</span><span class="sxs-lookup"><span data-stu-id="91a3b-105">Navigate tooyour Mobile Engagement portal.</span></span> <span data-ttu-id="91a3b-106">Hello doğru olduğunuz ve üzerinde hello ardından olun **Katıl** hello altındaki düğmesi:</span><span class="sxs-lookup"><span data-stu-id="91a3b-106">Ensure you're in hello correct and then click on hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. <span data-ttu-id="91a3b-107">Tıklatın hello üzerinde **ayarları** Engagement portalınızın sayfası.</span><span class="sxs-lookup"><span data-stu-id="91a3b-107">Click on hello **Settings** page in your Engagement Portal.</span></span> <span data-ttu-id="91a3b-108">Merhaba orada tıklayın **yerel gönderim** tooupload p12 sertifikanızı bölümünde:</span><span class="sxs-lookup"><span data-stu-id="91a3b-108">From there click on hello **Native Push** section tooupload your p12 certificate:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. <span data-ttu-id="91a3b-109">p12 sertifikanızı seçin, bunu yükleyip parolanızı yazın:</span><span class="sxs-lookup"><span data-stu-id="91a3b-109">Select your p12, upload it and type your password:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <span data-ttu-id="91a3b-110"><a id="send"></a>Bir bildirim tooyour uygulaması Gönder</span><span class="sxs-lookup"><span data-stu-id="91a3b-110"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="91a3b-111">Şimdi bir itme tooour uygulaması gönderecek basit bir anında iletme bildirimi kampanyası oluşturacağız:</span><span class="sxs-lookup"><span data-stu-id="91a3b-111">We will now create a simple Push Notification campaign that will send a push tooour app:</span></span>

1. <span data-ttu-id="91a3b-112">Toohello gidin **ulaşmak** Mobile Engagement portalınıza sekmesindedir.</span><span class="sxs-lookup"><span data-stu-id="91a3b-112">Navigate toohello **Reach** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="91a3b-113">Tıklatın **Yeni duyuru** toocreate anında iletme kampanyanızı</span><span class="sxs-lookup"><span data-stu-id="91a3b-113">Click **New Announcement** toocreate your push campaign</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. <span data-ttu-id="91a3b-114">Kampanyanızın ilk alanlarını Hello Kurulum:</span><span class="sxs-lookup"><span data-stu-id="91a3b-114">Setup hello first fields of your campaign:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * <span data-ttu-id="91a3b-115">Kampanyanıza bir **Ad** verin</span><span class="sxs-lookup"><span data-stu-id="91a3b-115">Provide a **Name** for your campaign</span></span> 
   * <span data-ttu-id="91a3b-116">Select hello **teslim saati** olarak **yalnızca uygulama dışında**: Bu, bazı metinleri hello basit Apple anında iletilen bildirim türüdür.</span><span class="sxs-lookup"><span data-stu-id="91a3b-116">Select hello **Delivery time** as **Out of app only**: this is hello simple Apple push notification type that features some text.</span></span>
   * <span data-ttu-id="91a3b-117">İlk hello Hello bildirim metni yazın **başlık** hello itme hello ilk satırı olacak.</span><span class="sxs-lookup"><span data-stu-id="91a3b-117">In hello notification text, type first hello **Title** which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="91a3b-118">Ardından, **ileti** hello ikinci satır olacak</span><span class="sxs-lookup"><span data-stu-id="91a3b-118">Then type your **Message** which will be hello second line</span></span>
4. <span data-ttu-id="91a3b-119">Aşağı kaydırın ve içerik bölümü hello seçin **yalnızca bildirim**</span><span class="sxs-lookup"><span data-stu-id="91a3b-119">Scroll down, and in hello content section select **Notification only**</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. <span data-ttu-id="91a3b-120">Merhaba en temel kampanya ayarını bitirdiniz.</span><span class="sxs-lookup"><span data-stu-id="91a3b-120">You're done setting hello most basic campaign.</span></span> <span data-ttu-id="91a3b-121">Şimdi aşağıya kayın ve tıklayın **oluşturma** toosave anında iletme bildirimi kampanyanızı düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="91a3b-121">Now scroll down and click on **Create** button toosave your push notification campaign.</span></span> 
6. <span data-ttu-id="91a3b-122">Son olarak - tıklayın **etkinleştirme** toosend anında iletme bildirimi.</span><span class="sxs-lookup"><span data-stu-id="91a3b-122">Finally - click on **Activate** toosend push notification.</span></span> 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. <span data-ttu-id="91a3b-123">Size hello iOS Cihazınızda hello aşağıdaki gibi hello bildirim merkezi bildirimi:</span><span class="sxs-lookup"><span data-stu-id="91a3b-123">You will be able receive hello notification on your iOS device in hello notification center like hello following:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. <span data-ttu-id="91a3b-124">Bu iOS cihazıyla eşleştirilmiş bir Apple Watch varsa, Apple Watch hello bildirim görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="91a3b-124">If you have an Apple Watch paired with this iOS device then you will see hello notification on your Apple Watch:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

