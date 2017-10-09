### <a name="configure-a-dns-label-for-hello-public-ip-address"></a><span data-ttu-id="e0504-101">Merhaba ortak IP adresi için bir DNS etiketi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e0504-101">Configure a DNS Label for hello public IP address</span></span>

<span data-ttu-id="e0504-102">Merhaba Internet'ten gelen tooconnect toohello SQL Server veritabanı altyapısı, ortak IP adresi için bir DNS etiketi oluşturmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="e0504-102">tooconnect toohello SQL Server Database Engine from hello Internet, consider creating a DNS Label for your public IP address.</span></span> <span data-ttu-id="e0504-103">IP adresine göre bağlanabilirsiniz ancak daha kolay tooidentify bir A kaydı hello DNS etiketi oluşturur ve temel alınan genel IP adresi özetleri hello.</span><span class="sxs-lookup"><span data-stu-id="e0504-103">You can connect by IP address, but hello DNS Label creates an A Record that is easier tooidentify and abstracts hello underlying public IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="e0504-104">DNS etiketleri gerekli değildir tooonly bağlanmak toohello SQL Server planı hello içinde aynı örneği, sanal ağ veya yalnızca yerel olarak.</span><span class="sxs-lookup"><span data-stu-id="e0504-104">DNS Labels are not required if you plan tooonly connect toohello SQL Server instance within hello same Virtual Network or only locally.</span></span>

<span data-ttu-id="e0504-105">bir DNS etiketi toocreate önce seçin **sanal makineleri** hello Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="e0504-105">toocreate a DNS Label, first select **Virtual machines** in hello portal.</span></span> <span data-ttu-id="e0504-106">SQL Server VM toobring özelliklerini ayarlama seçin.</span><span class="sxs-lookup"><span data-stu-id="e0504-106">Select your SQL Server VM toobring up its properties.</span></span>

1. <span data-ttu-id="e0504-107">Merhaba sanal makineye genel bakış içinde seçin, **genel IP adresi**.</span><span class="sxs-lookup"><span data-stu-id="e0504-107">In hello virtual machine overview, select your **Public IP address**.</span></span>

    ![genel ip adresi](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. <span data-ttu-id="e0504-109">Genel IP adresinizin Hello özelliklerinde genişletin **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="e0504-109">In hello properties for your Public IP address, expand **Configuration**.</span></span>

1. <span data-ttu-id="e0504-110">DNS etiket adı girin.</span><span class="sxs-lookup"><span data-stu-id="e0504-110">Enter a DNS Label name.</span></span> <span data-ttu-id="e0504-111">Itanium tabanlı sistemler için kullanılan tooconnect tooyour SQL Server VM adı yerine IP adresine göre tarafından doğrudan olabilir bir A kaydı adıdır.</span><span class="sxs-lookup"><span data-stu-id="e0504-111">This name is an A Record that can be used tooconnect tooyour SQL Server VM by name instead of by IP Address directly.</span></span>

1. <span data-ttu-id="e0504-112">Merhaba tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e0504-112">Click hello **Save** button.</span></span>

    ![dns etiketi](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a><span data-ttu-id="e0504-114">Başka bir bilgisayardan toohello veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="e0504-114">Connect toohello Database Engine from another computer</span></span>

1. <span data-ttu-id="e0504-115">Bir bilgisayarda toohello bağlı Internet'e açık SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="e0504-115">On a computer connected toohello internet, open SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="e0504-116">SQL Server Management Studio’nuz yoksa [buradan](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0504-116">If you do not have SQL Server Management Studio, you can download it [here](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>

1. <span data-ttu-id="e0504-117">Merhaba, **tooServer bağlanmak** veya **tooDatabase altyapısı bağlanmak** iletişim kutusu, Düzen hello **sunucu adı** değeri.</span><span class="sxs-lookup"><span data-stu-id="e0504-117">In hello **Connect tooServer** or **Connect tooDatabase Engine** dialog box, edit hello **Server name** value.</span></span> <span data-ttu-id="e0504-118">Başlangıç IP adresi veya (Merhaba önceki görevde saptanmıştır) hello sanal makinenin tam DNS adını girin.</span><span class="sxs-lookup"><span data-stu-id="e0504-118">Enter hello IP address or full DNS name of hello virtual machine (determined in hello previous task).</span></span> <span data-ttu-id="e0504-119">Ayrıca bir virgül ekleyebilir ya da SQL Server'ın TCP bağlantı noktasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0504-119">You can also add a comma and provide SQL Server's TCP port.</span></span> <span data-ttu-id="e0504-120">Örneğin, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span><span class="sxs-lookup"><span data-stu-id="e0504-120">For example, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span></span>

1. <span data-ttu-id="e0504-121">Merhaba, **kimlik doğrulaması** kutusunda **SQL Server kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="e0504-121">In hello **Authentication** box, select **SQL Server Authentication**.</span></span>

1. <span data-ttu-id="e0504-122">Merhaba, **oturum açma** kutusu, geçerli SQL oturum açma türü hello adı.</span><span class="sxs-lookup"><span data-stu-id="e0504-122">In hello **Login** box, type hello name of a valid SQL login.</span></span>

1. <span data-ttu-id="e0504-123">Merhaba, **parola** kutusu, hello oturum açma hello parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="e0504-123">In hello **Password** box, type hello password of hello login.</span></span>

1. <span data-ttu-id="e0504-124">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e0504-124">Click **Connect**.</span></span>

    ![ssms bağlanma](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)