### <a name="configure-a-dns-label-for-the-public-ip-address"></a><span data-ttu-id="f3284-101">Genel IP adresi için DNS etiketi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f3284-101">Configure a DNS Label for the public IP address</span></span>

<span data-ttu-id="f3284-102">SQL Server Veritabanı Altyapısına İnternet'ten bağlanmak için önce genel IP adresi için bir DNS etiketi yapılandırmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="f3284-102">To connect to the SQL Server Database Engine from the Internet, consider creating a DNS Label for your public IP address.</span></span> <span data-ttu-id="f3284-103">IP adresine göre de bağlanabilirsiniz, ancak DNS Etiketi tanımlanması daha kolay olan ve temeldeki genel IP adresini soyutlayan bir A Kaydı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f3284-103">You can connect by IP address, but the DNS Label creates an A Record that is easier to identify and abstracts the underlying public IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="f3284-104">SQL Server örneğine yalnızca aynı Sanal Ağ içinden veya yerel olarak bağlanmayı planlıyorsanız, DNS Etiketleri gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="f3284-104">DNS Labels are not required if you plan to only connect to the SQL Server instance within the same Virtual Network or only locally.</span></span>

<span data-ttu-id="f3284-105">DNS etiketi oluşturmak için önce portalda **Virtual Machines**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="f3284-105">To create a DNS Label, first select **Virtual machines** in the portal.</span></span> <span data-ttu-id="f3284-106">Özelliklerini görüntülemek için SQL Server VM’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="f3284-106">Select your SQL Server VM to bring up its properties.</span></span>

1. <span data-ttu-id="f3284-107">Sanal makineye genel bakış sayfasında **Genel IP adresi**’nizi seçin.</span><span class="sxs-lookup"><span data-stu-id="f3284-107">In the virtual machine overview, select your **Public IP address**.</span></span>

    ![genel ip adresi](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. <span data-ttu-id="f3284-109">Genel IP adresinizin özelliklerinde**Yapılandırma**’yı genişletin.</span><span class="sxs-lookup"><span data-stu-id="f3284-109">In the properties for your Public IP address, expand **Configuration**.</span></span>

1. <span data-ttu-id="f3284-110">DNS etiket adı girin.</span><span class="sxs-lookup"><span data-stu-id="f3284-110">Enter a DNS Label name.</span></span> <span data-ttu-id="f3284-111">Bu ad, SQL Server VM'nize bağlanmak için IP adresi yerine doğrudan kullanılabilen bir Kayıttır.</span><span class="sxs-lookup"><span data-stu-id="f3284-111">This name is an A Record that can be used to connect to your SQL Server VM by name instead of by IP Address directly.</span></span>

1. <span data-ttu-id="f3284-112">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f3284-112">Click the **Save** button.</span></span>

    ![dns etiketi](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-to-the-database-engine-from-another-computer"></a><span data-ttu-id="f3284-114">Başka bir bilgisayardan Veritabanı Altyapısına bağlanma</span><span class="sxs-lookup"><span data-stu-id="f3284-114">Connect to the Database Engine from another computer</span></span>

1. <span data-ttu-id="f3284-115">İnternet'e bağlı bir bilgisayarda SQL Server Management Studio’yu (SSMS) açın.</span><span class="sxs-lookup"><span data-stu-id="f3284-115">On a computer connected to the internet, open SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="f3284-116">SQL Server Management Studio’nuz yoksa [buradan](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3284-116">If you do not have SQL Server Management Studio, you can download it [here](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>

1. <span data-ttu-id="f3284-117">**Sunucuya Bağlan** veya **Veritabanı Altyapısına Bağlan** iletişim kutusunda **Sunucu adı** değerini düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="f3284-117">In the **Connect to Server** or **Connect to Database Engine** dialog box, edit the **Server name** value.</span></span> <span data-ttu-id="f3284-118">Sanal makinenin IP adresini veya tam DNS adını girin (önceki görevde saptanmıştır).</span><span class="sxs-lookup"><span data-stu-id="f3284-118">Enter the IP address or full DNS name of the virtual machine (determined in the previous task).</span></span> <span data-ttu-id="f3284-119">Ayrıca bir virgül ekleyebilir ya da SQL Server'ın TCP bağlantı noktasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3284-119">You can also add a comma and provide SQL Server's TCP port.</span></span> <span data-ttu-id="f3284-120">Örneğin, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span><span class="sxs-lookup"><span data-stu-id="f3284-120">For example, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.</span></span>

1. <span data-ttu-id="f3284-121">**Kimlik Doğrulaması** kutusunda **SQL Server Kimlik Doğrulaması**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="f3284-121">In the **Authentication** box, select **SQL Server Authentication**.</span></span>

1. <span data-ttu-id="f3284-122">**Oturum Aç** kutusuna geçerli bir SQL oturum açma adı yazın.</span><span class="sxs-lookup"><span data-stu-id="f3284-122">In the **Login** box, type the name of a valid SQL login.</span></span>

1. <span data-ttu-id="f3284-123">**Parola** kutusuna oturum açma parolasını yazın.</span><span class="sxs-lookup"><span data-stu-id="f3284-123">In the **Password** box, type the password of the login.</span></span>

1. <span data-ttu-id="f3284-124">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f3284-124">Click **Connect**.</span></span>

    ![ssms bağlanma](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)