1. <span data-ttu-id="4d25c-101">Toohello üzerinde oturum [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="4d25c-101">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="4d25c-102">Hello sol gezinti bölmesinde hello portalı tıklatın **yeni**, ardından **Kurumsal tümleştirme**ve ardından **geçiş**.</span><span class="sxs-lookup"><span data-stu-id="4d25c-102">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Relay**.</span></span>
3. <span data-ttu-id="4d25c-103">Merhaba, **ad alanı oluşturma** iletişim kutusunda, bir ad alanı adı girin.</span><span class="sxs-lookup"><span data-stu-id="4d25c-103">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="4d25c-104">Merhaba adı olup olmadığını hello sistem hemen toosee denetler.</span><span class="sxs-lookup"><span data-stu-id="4d25c-104">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="4d25c-105">Merhaba, **abonelik** alanında, hangi toocreate hello ad alanında bir Azure aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="4d25c-105">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
5. <span data-ttu-id="4d25c-106">Merhaba,  **[kaynak grubu](../articles/azure-resource-manager/resource-group-portal.md)**  alanında, hangi hello ad alanı Canlı veya yeni bir tane oluşturmak varolan bir kaynak grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="4d25c-106">In hello **[Resource group](../articles/azure-resource-manager/resource-group-portal.md)** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
6. <span data-ttu-id="4d25c-107">İçinde **konumu**, hello ülke veya bölge içinde ad alanınızın barındırılması seçin.</span><span class="sxs-lookup"><span data-stu-id="4d25c-107">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![ad alanı oluşturma][create-namespace]
7. <span data-ttu-id="4d25c-109">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d25c-109">Click **Create**.</span></span> <span data-ttu-id="4d25c-110">Şimdi Hello sistem ad alanınızı oluşturur ve kullanıma açar.</span><span class="sxs-lookup"><span data-stu-id="4d25c-110">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="4d25c-111">Sistem, hesabınız için kaynakları sağlarken birkaç dakika sonra hello.</span><span class="sxs-lookup"><span data-stu-id="4d25c-111">After a few minutes, hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="4d25c-112">Merhaba yönetim kimlik bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="4d25c-112">Obtain hello management credentials</span></span>
1. <span data-ttu-id="4d25c-113">Ad alanları Hello listesinde yeni oluşturulan ad alanı adı hello tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d25c-113">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="4d25c-114">Merhaba ad alanı dikey penceresinde tıklayın **paylaşılan erişim ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="4d25c-114">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="4d25c-115">Merhaba, **paylaşılan erişim ilkeleri** dikey penceresinde tıklatın **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="4d25c-115">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![bağlantı bilgisi][connection-info]
4. <span data-ttu-id="4d25c-117">Merhaba, **İlkesi: RootManageSharedAccessKey** dikey penceresinde hello Kopyala düğmesini tıklatın ardından çok**bağlantı dizesi – birincil anahtarı**, daha sonra kullanmak için toocopy hello bağlantı dizesi tooyour Pano.</span><span class="sxs-lookup"><span data-stu-id="4d25c-117">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="4d25c-118">Bu değeri Not Defteri veya başka bir geçici konuma yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="4d25c-118">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![bağlantı dizesi][connection-string]

5. <span data-ttu-id="4d25c-120">Kopyalama ve yapıştırma hello değerini yineleme hello önceki adımda **birincil anahtar** tooa daha sonra kullanmak için geçici konum.</span><span class="sxs-lookup"><span data-stu-id="4d25c-120">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
