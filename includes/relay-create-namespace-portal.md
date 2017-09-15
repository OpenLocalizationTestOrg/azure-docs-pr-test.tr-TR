1. <span data-ttu-id="23466-101">[Azure portalında][Azure portal] oturum açın.</span><span class="sxs-lookup"><span data-stu-id="23466-101">Log on to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="23466-102">Portalın sol gezinti bölmesinde **Yeni**'ye tıklayın, ardından **Enterprise Integration**'a ve **Geçiş**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="23466-102">In the left navigation pane of the portal, click **New**, then click **Enterprise Integration**, and then click **Relay**.</span></span>
3. <span data-ttu-id="23466-103">**Ad alanı oluştur** iletişim kutusunda bir ad alanı adı girin.</span><span class="sxs-lookup"><span data-stu-id="23466-103">In the **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="23466-104">Adın kullanılabilirliği sistem tarafından hemen denetlenir.</span><span class="sxs-lookup"><span data-stu-id="23466-104">The system immediately checks to see if the name is available.</span></span>
4. <span data-ttu-id="23466-105">**Abonelik** alanında, ad alanı oluşturmak için kullanmak istediğiniz bir Azure aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="23466-105">In the **Subscription** field, choose an Azure subscription in which to create the namespace.</span></span>
5. <span data-ttu-id="23466-106">**[Kaynak grubu](../articles/azure-resource-manager/resource-group-portal.md)** alanında, ad alanını barındırmak üzere var olan bir kaynak grubunu seçin veya yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="23466-106">In the **[Resource group](../articles/azure-resource-manager/resource-group-portal.md)** field, choose an existing resource group in which the namespace will live, or create a new one.</span></span>      
6. <span data-ttu-id="23466-107">**Konum** alanında, ad alanınızın barındırılması gereken ülkeyi veya bölgeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="23466-107">In **Location**, choose the country or region in which your namespace should be hosted.</span></span>
   
    ![ad alanı oluşturma][create-namespace]
7. <span data-ttu-id="23466-109">**Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="23466-109">Click **Create**.</span></span> <span data-ttu-id="23466-110">Artık sistem ad alanınızı oluşturur ve kullanıma açar.</span><span class="sxs-lookup"><span data-stu-id="23466-110">The system now creates your namespace and enables it.</span></span> <span data-ttu-id="23466-111">Birkaç dakika sonra sistem, hesabınız için kaynakları sağlar.</span><span class="sxs-lookup"><span data-stu-id="23466-111">After a few minutes, the system provisions resources for your account.</span></span>

### <a name="obtain-the-management-credentials"></a><span data-ttu-id="23466-112">Yönetim kimlik bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="23466-112">Obtain the management credentials</span></span>
1. <span data-ttu-id="23466-113">Ad alanları listesinde, yeni oluşturulan ad alanı adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="23466-113">In the list of namespaces, click the newly created namespace name.</span></span>
2. <span data-ttu-id="23466-114">Ad alanı dikey penceresinde, **Paylaşılan erişim ilkeleri**'ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="23466-114">In the namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="23466-115">**Paylaşılan erişim ilkeleri** dikey penceresinde, **RootManageSharedAccessKey** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="23466-115">In the **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![bağlantı bilgisi][connection-info]
4. <span data-ttu-id="23466-117">**İlke: RootManageSharedAccessKey** dikey penceresinde **Bağlantı dizesi–birincil anahtar** seçeneğinin yanındaki Kopyala düğmesine tıklayın ve bağlantı dizesini, daha sonra kullanmak üzere panonuza kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="23466-117">In the **Policy: RootManageSharedAccessKey** blade, click the copy button next to **Connection string–primary key**, to copy the connection string to your clipboard for later use.</span></span> <span data-ttu-id="23466-118">Bu değeri Not Defteri veya başka bir geçici konuma yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="23466-118">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![bağlantı dizesi][connection-string]

5. <span data-ttu-id="23466-120">**Birincil anahtar** değerini daha sonra kullanmak üzere geçici bir konuma kopyalayarak önceki adımı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="23466-120">Repeat the previous step, copying and pasting the value of **Primary key** to a temporary location for later use.</span></span>  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
