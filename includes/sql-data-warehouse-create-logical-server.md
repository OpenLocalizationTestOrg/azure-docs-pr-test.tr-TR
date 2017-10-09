### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a><span data-ttu-id="9ccfa-101">Hello Azure portalında yeni bir mantıksal SQL sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ccfa-101">Create a new logical SQL server in hello Azure portal</span></span>

1. <span data-ttu-id="9ccfa-102">**Yeni**'ye tıklayın, **mantıksal sunucu** terimini arayın ve **ENTER**'a basın.</span><span class="sxs-lookup"><span data-stu-id="9ccfa-102">Click **New**, search **logical server**, and then hit **ENTER**.</span></span>

    ![mantıksal sunucu arama](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. <span data-ttu-id="9ccfa-104">**SQL Server (mantıksal sunucu)** girişini seçin</span><span class="sxs-lookup"><span data-stu-id="9ccfa-104">Select **SQL server (logical server)**</span></span> 

    ![mantıksal sunucu seçme](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. <span data-ttu-id="9ccfa-106">Tıklatın **oluşturma** tooopen hello yeni SQL Server (mantıksal sunucu) dikey.</span><span class="sxs-lookup"><span data-stu-id="9ccfa-106">Click **Create** tooopen hello new SQL Server (logical server) blade.</span></span>

   <span data-ttu-id="9ccfa-107"><kbd>![mantıksal sunucusu dikey penceresini açmak](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![mantıksal sunucusu dikey](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd></span><span class="sxs-lookup"><span data-stu-id="9ccfa-107"><kbd> ![open logical server blade](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd>![logical server blade](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png) </kbd></span></span>
  
3. <span data-ttu-id="9ccfa-108">Merhaba SQL Server (mantıksal sunucu) dikey'nın sunucu adı metin kutusuna, hello yeni mantıksal sunucu için geçerli bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="9ccfa-108">In hello SQL Server (logical server) blade's server name text box, provide a valid name for hello new logical server.</span></span> <span data-ttu-id="9ccfa-109">Yeşil onay işareti, geçerli bir ad sağladığınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="9ccfa-109">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![yeni sunucu adı](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > <span data-ttu-id="9ccfa-111">Merhaba, yeni sunucu için tam ad < Sunucunuzun_Adı > olacaktır. database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="9ccfa-111">hello fully qualified name for your new server will be <your_server_name>.database.windows.net.</span></span>
    >
    
4. <span data-ttu-id="9ccfa-112">Merhaba Server yönetici oturum açma metin kutusuna, bu sunucu için hello SQL kimlik doğrulaması oturum açma için kullanıcı adı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="9ccfa-112">In hello Server admin login text box, provide a user name for hello SQL authentication login for this server.</span></span> <span data-ttu-id="9ccfa-113">Bu oturum açma hello sunucu asıl oturum olarak bilinir.</span><span class="sxs-lookup"><span data-stu-id="9ccfa-113">This login is known as hello server principal login.</span></span> <span data-ttu-id="9ccfa-114">Yeşil onay işareti, geçerli bir ad sağladığınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="9ccfa-114">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![SQL yöneticisi oturum açma adı](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. <span data-ttu-id="9ccfa-116">Merhaba, **parola** ve **parolayı onayla** metin kutularında, hello sunucu asıl oturum açma hesabı için bir parola sağlayın.</span><span class="sxs-lookup"><span data-stu-id="9ccfa-116">In hello **Password** and **Confirm password** text boxes, provide a password for hello server principal login account.</span></span> <span data-ttu-id="9ccfa-117">Yeşil onay işareti, geçerli bir parola sağladığınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="9ccfa-117">A green check mark indicates that you have provided a valid password.</span></span>
    
    ![SQL yönetici parolası](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. <span data-ttu-id="9ccfa-119">İzin toocreate nesneleri sahip bir abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="9ccfa-119">Select a subscription in which you have permission toocreate objects.</span></span>

    ![aboneliği](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. <span data-ttu-id="9ccfa-121">Hello kaynak grubunun metin kutusunda **Yeni Oluştur** hello kaynak grubunun metin kutusunda, hello (da mevcut bir kaynak grubu için kendiniz bir tane önceden oluşturduğunuz halinde kullanabilirsiniz) yeni kaynak grubu için geçerli bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="9ccfa-121">In hello Resource group text box, select **Create new** and then, in hello resource group text box, provide a valid name for hello new resource group (you can also use an existing resource group if you have already created one for yourself).</span></span> <span data-ttu-id="9ccfa-122">Yeşil onay işareti, geçerli bir ad sağladığınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="9ccfa-122">A green check mark indicates that you have provided a valid name.</span></span>

    ![yeni kaynak grubu](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. <span data-ttu-id="9ccfa-124">Merhaba, **konumu** metin kutusunda bir veri merkezi - "Avustralya Doğu" gibi uygun tooyour konumu.</span><span class="sxs-lookup"><span data-stu-id="9ccfa-124">In hello **Location** text box, select a data center appropriate tooyour location - such as "Australia East".</span></span>
    
    ![sunucu konumu](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > <span data-ttu-id="9ccfa-126">onay kutusunu hello **izin azure Hizmetleri tooaccess sunucusu** bu dikey pencerede değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="9ccfa-126">hello checkbox for **Allow azure services tooaccess server** cannot be changed on this blade.</span></span> <span data-ttu-id="9ccfa-127">Merhaba sunucu güvenlik duvarı dikey penceresinde bu ayarı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ccfa-127">You can change this setting on hello server firewall blade.</span></span> <span data-ttu-id="9ccfa-128">Daha fazla bilgi için bkz. [Güvenliğe giriş](../articles/sql-database/sql-database-manage-servers-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9ccfa-128">For more information, see [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md).</span></span>
    >
    
9. <span data-ttu-id="9ccfa-129">**Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ccfa-129">Click **Create**.</span></span>

    ![oluştur düğmesi](./media/sql-data-warehouse-create-logical-server/create.png)

