<span data-ttu-id="095c6-101">Azure'da Service Bus kullanarak toobegin kuyruklar, öncelikle bir ad alanı Azure arasında benzersiz bir ad ile oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="095c6-101">toobegin using Service Bus queues in Azure, you must first create a namespace with a name that is unique across Azure.</span></span> <span data-ttu-id="095c6-102">Ad alanı, uygulamanızda bulunan Service Bus kaynaklarını adreslemek için içeriğin kapsamını belirleyen bir kapsayıcı sunar.</span><span class="sxs-lookup"><span data-stu-id="095c6-102">A namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="095c6-103">toocreate bir ad alanı:</span><span class="sxs-lookup"><span data-stu-id="095c6-103">toocreate a namespace:</span></span>

1. <span data-ttu-id="095c6-104">Toohello üzerinde oturum [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="095c6-104">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="095c6-105">Hello sol gezinti bölmesinde hello portalı tıklatın **yeni**, ardından **Kurumsal tümleştirme**ve ardından **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="095c6-105">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Service Bus**.</span></span>
3. <span data-ttu-id="095c6-106">Merhaba, **ad alanı oluşturma** iletişim kutusunda, bir ad alanı adı girin.</span><span class="sxs-lookup"><span data-stu-id="095c6-106">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="095c6-107">Merhaba adı olup olmadığını hello sistem hemen toosee denetler.</span><span class="sxs-lookup"><span data-stu-id="095c6-107">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="095c6-108">Emin hello ad alanı adı yapmadan kullanılabilir olduktan sonra fiyatlandırma Katmanı (temel, standart veya Premium) hello seçin.</span><span class="sxs-lookup"><span data-stu-id="095c6-108">After making sure hello namespace name is available, choose hello pricing tier (Basic, Standard, or Premium).</span></span>
5. <span data-ttu-id="095c6-109">Merhaba, **abonelik** alanında, hangi toocreate hello ad alanında bir Azure aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="095c6-109">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
6. <span data-ttu-id="095c6-110">Merhaba, **kaynak grubu** alanında, hangi hello ad alanı Canlı veya yeni bir tane oluşturmak varolan bir kaynak grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="095c6-110">In hello **Resource group** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
7. <span data-ttu-id="095c6-111">İçinde **konumu**, hello ülke veya bölge içinde ad alanınızın barındırılması seçin.</span><span class="sxs-lookup"><span data-stu-id="095c6-111">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![ad alanı oluşturma][create-namespace]
8. <span data-ttu-id="095c6-113">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="095c6-113">Click **Create**.</span></span> <span data-ttu-id="095c6-114">Şimdi Hello sistem ad alanınızı oluşturur ve kullanıma açar.</span><span class="sxs-lookup"><span data-stu-id="095c6-114">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="095c6-115">Hesabınız için hello sistem kaynakları sağlarken birkaç dakika toowait olabilir.</span><span class="sxs-lookup"><span data-stu-id="095c6-115">You might have toowait several minutes as hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="095c6-116">Merhaba yönetim kimlik bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="095c6-116">Obtain hello management credentials</span></span>

1. <span data-ttu-id="095c6-117">Ad alanları Hello listesinde yeni oluşturulan ad alanı adı hello tıklayın.</span><span class="sxs-lookup"><span data-stu-id="095c6-117">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="095c6-118">Merhaba ad alanı dikey penceresinde tıklayın **paylaşılan erişim ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="095c6-118">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="095c6-119">Merhaba, **paylaşılan erişim ilkeleri** dikey penceresinde tıklatın **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="095c6-119">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![bağlantı bilgisi][connection-info]
4. <span data-ttu-id="095c6-121">Merhaba, **İlkesi: RootManageSharedAccessKey** dikey penceresinde hello Kopyala düğmesini tıklatın ardından çok**bağlantı dizesi – birincil anahtarı**, daha sonra kullanmak için toocopy hello bağlantı dizesi tooyour Pano.</span><span class="sxs-lookup"><span data-stu-id="095c6-121">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="095c6-122">Bu değeri Not Defteri veya başka bir geçici konuma yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="095c6-122">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![bağlantı dizesi][connection-string]

5. <span data-ttu-id="095c6-124">Kopyalama ve yapıştırma hello değerini yineleme hello önceki adımda **birincil anahtar** tooa daha sonra kullanmak için geçici konum.</span><span class="sxs-lookup"><span data-stu-id="095c6-124">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>

<!--Image references-->

[create-namespace]: ./media/service-bus-create-namespace-portal/create-namespace.png
[connection-info]: ./media/service-bus-create-namespace-portal/connection-info.png
[connection-string]: ./media/service-bus-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
