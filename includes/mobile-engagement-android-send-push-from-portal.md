### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="dac64-101">GRANT Mobile Engagement erişimi tooyour GCM API anahtarı</span><span class="sxs-lookup"><span data-stu-id="dac64-101">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="dac64-102">tooallow Mobile Engagement toosend anında iletme bildirimleri sizin adınıza tooyour API anahtarı erişim toogrant gerekir.</span><span class="sxs-lookup"><span data-stu-id="dac64-102">tooallow Mobile Engagement toosend push notifications on your behalf, you need toogrant it access tooyour API Key.</span></span> <span data-ttu-id="dac64-103">Bu, yapılandırarak ve anahtarınızı hello Mobile Engagement portalına girilerek gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="dac64-103">This is done by configuring and entering your key into hello Mobile Engagement portal.</span></span>

1. <span data-ttu-id="dac64-104">Biz bu proje için kullanmakta olduğunuz ve hello ardından hello uygulamada olduğunuzdan, Azure Klasik portalından olun **Katıl** hello altındaki düğmesi:</span><span class="sxs-lookup"><span data-stu-id="dac64-104">From your Azure Classic Portal, ensure you're in hello app we're using for this project, and then click hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. <span data-ttu-id="dac64-105">Merhaba ardından **ayarları** -> **yerel gönderim** tooenter GCM anahtarınızı bölümünde:</span><span class="sxs-lookup"><span data-stu-id="dac64-105">Then click hello **Settings** -> **Native Push** section tooenter your GCM Key:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. <span data-ttu-id="dac64-106">Merhaba tıklatın **Düzenle** önüne simgesi **API anahtarı** hello içinde **GCM ayarları** bölümünde aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="dac64-106">Click hello **Edit** icon in front of **API Key** in hello **GCM Settings** section as shown below:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. <span data-ttu-id="dac64-107">Merhaba açılır hello önce aldığınız GCM Server anahtarını yapıştırın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="dac64-107">In hello pop-up, paste hello GCM Server Key you obtained before and then click **Ok**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <span data-ttu-id="dac64-108"><a id="send"></a>Bir bildirim tooyour uygulaması Gönder</span><span class="sxs-lookup"><span data-stu-id="dac64-108"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="dac64-109">Şimdi bir anında iletme bildirimi tooour uygulaması gönderir basit anında iletme bildirimi kampanyası oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="dac64-109">We will now create a simple push notification campaign that sends a push notification tooour app.</span></span>

1. <span data-ttu-id="dac64-110">Toohello gidin **ULAŞMAK** Mobile Engagement portalınıza sekmesindedir.</span><span class="sxs-lookup"><span data-stu-id="dac64-110">Navigate toohello **REACH** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="dac64-111">Tıklatın **Yeni duyuru** toocreate anında iletme bildirimi kampanyanızı.</span><span class="sxs-lookup"><span data-stu-id="dac64-111">Click **New announcement** toocreate your push notification campaign.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. <span data-ttu-id="dac64-112">Aşağıdaki adımları hello kampanyanızın ilk alan hello ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="dac64-112">Set up hello first field of your campaign through hello following steps:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    <span data-ttu-id="dac64-113">a.</span><span class="sxs-lookup"><span data-stu-id="dac64-113">a.</span></span> <span data-ttu-id="dac64-114">Kampanyanızı adlandırın.</span><span class="sxs-lookup"><span data-stu-id="dac64-114">Name your campaign.</span></span>
   
    <span data-ttu-id="dac64-115">b.</span><span class="sxs-lookup"><span data-stu-id="dac64-115">b.</span></span> <span data-ttu-id="dac64-116">Select hello **teslimat türü** olarak *sistem bildirimi -> basit*: bir başlık ve küçük bir metin satırının özellikleri hello basit Android anında iletme bildirimi türü budur.</span><span class="sxs-lookup"><span data-stu-id="dac64-116">Select hello **Delivery type** as *System notification -> Simple*: This is hello simple Android push notification type that features a title and a small line of text.</span></span>
   
    <span data-ttu-id="dac64-117">c.</span><span class="sxs-lookup"><span data-stu-id="dac64-117">c.</span></span> <span data-ttu-id="dac64-118">Seçin **teslim saati** olarak *dilediğiniz zaman* hello uygulama veya başlatılıp başlatılmadığını tooallow hello uygulama tooreceive bir bildirim.</span><span class="sxs-lookup"><span data-stu-id="dac64-118">Select **Delivery time** as *Any time* tooallow hello app tooreceive a notification whether hello app is started or not.</span></span>
   
    <span data-ttu-id="dac64-119">d.</span><span class="sxs-lookup"><span data-stu-id="dac64-119">d.</span></span> <span data-ttu-id="dac64-120">Merhaba bildirim metin türü hello içinde **başlık** olacak hello itme kalın.</span><span class="sxs-lookup"><span data-stu-id="dac64-120">In hello notification text type hello **Title** which will be in bold in hello push.</span></span>
   
    <span data-ttu-id="dac64-121">e.</span><span class="sxs-lookup"><span data-stu-id="dac64-121">e.</span></span> <span data-ttu-id="dac64-122">Ardından, **İleti**’yi yazın.</span><span class="sxs-lookup"><span data-stu-id="dac64-122">Then type your **Message**</span></span>
4. <span data-ttu-id="dac64-123">Kaydırma aşağı ve hello **içerik** bölümünde, select **yalnızca bildirim**.</span><span class="sxs-lookup"><span data-stu-id="dac64-123">Scroll down, and in hello **Content** section, select **Notification only**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. <span data-ttu-id="dac64-124">Ayar hello en temel kampanya olası bitirdiniz.</span><span class="sxs-lookup"><span data-stu-id="dac64-124">You're done setting hello most basic campaign possible.</span></span> <span data-ttu-id="dac64-125">Şimdi kaydırarak yeniden aşağı gidin ve hello tıklatın **oluşturma** toosave kampanyanızı düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dac64-125">Now scroll down again and click hello **Create** button toosave your campaign.</span></span>
6. <span data-ttu-id="dac64-126">Son adım: tıklatın **etkinleştirme** tooactivate kampanya toosend anında iletme bildirimleri.</span><span class="sxs-lookup"><span data-stu-id="dac64-126">Last step: click **Activate** tooactivate your campaign toosend push notifications.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

