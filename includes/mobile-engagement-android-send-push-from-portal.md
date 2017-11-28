### <a name="grant-mobile-engagement-access-to-your-gcm-api-key"></a><span data-ttu-id="1c1b7-101">GCM API Anahtarınıza Mobile Engagement erişimi verin</span><span class="sxs-lookup"><span data-stu-id="1c1b7-101">Grant Mobile Engagement access to your GCM API Key</span></span>
<span data-ttu-id="1c1b7-102">Mobile Engagement’ın sizin adınıza anında iletme bildirimleri göndermesine izin vermek için API Anahtarınıza erişim izni vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c1b7-102">To allow Mobile Engagement to send push notifications on your behalf, you need to grant it access to your API Key.</span></span> <span data-ttu-id="1c1b7-103">Bu da, anahtarınızın yapılandırıp Mobile Engagement portalına girilerek gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1c1b7-103">This is done by configuring and entering your key into the Mobile Engagement portal.</span></span>

1. <span data-ttu-id="1c1b7-104">Klasik Azure Portalı’nızdan bu proje için kullanmakta olduğunuz uygulamadan emin olun ve alttaki **Katıl** düğmesine tıklayın:</span><span class="sxs-lookup"><span data-stu-id="1c1b7-104">From your Azure Classic Portal, ensure you're in the app we're using for this project, and then click the **Engage** button at the bottom:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. <span data-ttu-id="1c1b7-105">Sonra da, GCM Anahtarınızı girmek için **Ayarlar** -> **Yerel Gönderim**’e tıklayın:</span><span class="sxs-lookup"><span data-stu-id="1c1b7-105">Then click the **Settings** -> **Native Push** section to enter your GCM Key:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. <span data-ttu-id="1c1b7-106">**GCM Ayarları** bölümünde, **API Anahtarı**’nın ön tarafındaki **Düzenle** simgesine aşağıda gösterildiği gibi tıklayın:</span><span class="sxs-lookup"><span data-stu-id="1c1b7-106">Click the **Edit** icon in front of **API Key** in the **GCM Settings** section as shown below:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. <span data-ttu-id="1c1b7-107">Açılan pencerede, daha önce aldığınız GCM Sunucu Anahtarını yapıştırın **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1c1b7-107">In the pop-up, paste the GCM Server Key you obtained before and then click **Ok**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <span data-ttu-id="1c1b7-108"><a id="send"></a>Uygulamanıza bildirim gönderme</span><span class="sxs-lookup"><span data-stu-id="1c1b7-108"><a id="send"></a>Send a notification to your app</span></span>
<span data-ttu-id="1c1b7-109">Şimdi de, uygulamamıza anında iletme bildirimi gönderen basit bir anında iletme bildirimi kampanyası oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="1c1b7-109">We will now create a simple push notification campaign that sends a push notification to our app.</span></span>

1. <span data-ttu-id="1c1b7-110">Mobile Engagement portalınızın **REACH** sekmesine gidin.</span><span class="sxs-lookup"><span data-stu-id="1c1b7-110">Navigate to the **REACH** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="1c1b7-111">Anında iletme bildirimi kampanyanızı oluşturmak için **Yeni duyuru**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1c1b7-111">Click **New announcement** to create your push notification campaign.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. <span data-ttu-id="1c1b7-112">Kampanyanızın ilk alanını şu adımlarla ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="1c1b7-112">Set up the first field of your campaign through the following steps:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    <span data-ttu-id="1c1b7-113">a.</span><span class="sxs-lookup"><span data-stu-id="1c1b7-113">a.</span></span> <span data-ttu-id="1c1b7-114">Kampanyanızı adlandırın.</span><span class="sxs-lookup"><span data-stu-id="1c1b7-114">Name your campaign.</span></span>
   
    <span data-ttu-id="1c1b7-115">b.</span><span class="sxs-lookup"><span data-stu-id="1c1b7-115">b.</span></span> <span data-ttu-id="1c1b7-116">**Teslimat türü**’nü *Sistem bildirimi -> Basit* olarak seçin: Bir başlık ve küçük bir metin satırından oluşan basit Android anında iletme bildirimi türüdür.</span><span class="sxs-lookup"><span data-stu-id="1c1b7-116">Select the **Delivery type** as *System notification -> Simple*: This is the simple Android push notification type that features a title and a small line of text.</span></span>
   
    <span data-ttu-id="1c1b7-117">c.</span><span class="sxs-lookup"><span data-stu-id="1c1b7-117">c.</span></span> <span data-ttu-id="1c1b7-118">Uygulama başlatılsın ya da başlatılmasın uygulamanın bildirim almasını sağlamak için **Teslimat zamanı**’nı *Her zaman* olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="1c1b7-118">Select **Delivery time** as *Any time* to allow the app to receive a notification whether the app is started or not.</span></span>
   
    <span data-ttu-id="1c1b7-119">d.</span><span class="sxs-lookup"><span data-stu-id="1c1b7-119">d.</span></span> <span data-ttu-id="1c1b7-120">Bildirim metnine gönderimde koyu olacak **Başlık** metnini yazın.</span><span class="sxs-lookup"><span data-stu-id="1c1b7-120">In the notification text type the **Title** which will be in bold in the push.</span></span>
   
    <span data-ttu-id="1c1b7-121">e.</span><span class="sxs-lookup"><span data-stu-id="1c1b7-121">e.</span></span> <span data-ttu-id="1c1b7-122">Ardından, **İleti**’yi yazın.</span><span class="sxs-lookup"><span data-stu-id="1c1b7-122">Then type your **Message**</span></span>
4. <span data-ttu-id="1c1b7-123">Kaydırarak aşağı gidin ve **İçerik** bölümünde **Yalnızca bildirim**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="1c1b7-123">Scroll down, and in the **Content** section, select **Notification only**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. <span data-ttu-id="1c1b7-124">Olabilecek en temel kampanya ayarını bitirdiniz.</span><span class="sxs-lookup"><span data-stu-id="1c1b7-124">You're done setting the most basic campaign possible.</span></span> <span data-ttu-id="1c1b7-125">Şimdi kaydırarak yeniden aşağı gidin ve **Oluştur** düğmesine tıklayarak kampanyanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1c1b7-125">Now scroll down again and click the **Create** button to save your campaign.</span></span>
6. <span data-ttu-id="1c1b7-126">Son adım: anında iletme bildirimlerini gönderecek kampanyanızı etkinleştirmek için **Etkinleştir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1c1b7-126">Last step: click **Activate** to activate your campaign to send push notifications.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

