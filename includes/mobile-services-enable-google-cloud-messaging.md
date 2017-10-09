
1. <span data-ttu-id="7e602-101">Toohello gidin [Google Cloud Console](https://console.developers.google.com/project), Google hesabı kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7e602-101">Navigate toohello [Google Cloud Console](https://console.developers.google.com/project), sign in with your Google account credentials.</span></span> 
2. <span data-ttu-id="7e602-102">**Proje Oluştur**’a tıklayıp bir proje adı yazın ve sonra **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7e602-102">Click **Create Project**, type a project name, then click **Create**.</span></span> <span data-ttu-id="7e602-103">İstenirse, SMS doğrulamasını hello taşımak ve tıklatın **oluşturma** yeniden.</span><span class="sxs-lookup"><span data-stu-id="7e602-103">If requested, carry out hello SMS Verification, and click **Create** again.</span></span>
   
    ![Yeni proje oluşturma](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     <span data-ttu-id="7e602-105">Yeni **Proje adı**’nızı yazıp **Proje oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7e602-105">Type in your new **Project name** and click **Create project**.</span></span>
3. <span data-ttu-id="7e602-106">Merhaba tıklatın **yardımcı programlar ve diğerleri** düğmesine tıklayın ve ardından **proje bilgileri**.</span><span class="sxs-lookup"><span data-stu-id="7e602-106">Click hello **Utilities and More** button and then click **Project Information**.</span></span> <span data-ttu-id="7e602-107">Merhaba Not **proje numarası**.</span><span class="sxs-lookup"><span data-stu-id="7e602-107">Make a note of hello **Project Number**.</span></span> <span data-ttu-id="7e602-108">Bu değer hello olarak tooset gerekir `SenderId` hello istemci uygulamasında değişken.</span><span class="sxs-lookup"><span data-stu-id="7e602-108">You will need tooset this value as hello `SenderId` variable in hello client app.</span></span>
   
    ![Yardımcı programlar ve daha fazlası](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. <span data-ttu-id="7e602-110">Hello panoyu altında proje **mobil API'leri**, tıklatın **Google Cloud Messaging**, hello sonraki sayfada'ye tıklayın **API etkinleştir** ve hizmet hello koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="7e602-110">In hello project dashboard, under **Mobile APIs**, click **Google Cloud Messaging**, then on hello next page click **Enable API** and accept hello terms of service.</span></span> 
   
    ![GCM etkinleştirme](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![GCM etkinleştirme](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. <span data-ttu-id="7e602-113">Merhaba proje panosunda tıklatın **kimlik bilgileri** > **kimlik bilgisi Oluştur** > **API anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="7e602-113">In hello project dashboard, Click **Credentials** > **Create Credential** > **API Key**.</span></span> 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. <span data-ttu-id="7e602-114">**Yeni anahtar oluştur**’da **Sunucu anahtarı**’na tıklayın, anahtarınız için bir ad yazın ve **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7e602-114">In **Create a new key**, click **Server key**, type a name for your key, then click **Create**.</span></span>
7. <span data-ttu-id="7e602-115">Merhaba Not **API anahtarı** değeri.</span><span class="sxs-lookup"><span data-stu-id="7e602-115">Make a note of hello **API KEY** value.</span></span>
   
    <span data-ttu-id="7e602-116">Bu API anahtar değeri tooenable Azure tooauthenticate GCM ile birlikte kullanabilir ve uygulamanız adına anında iletme bildirimleri göndermek.</span><span class="sxs-lookup"><span data-stu-id="7e602-116">You will use this API key value tooenable Azure tooauthenticate with GCM and send push notifications on behalf of your app.</span></span>

