
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. <span data-ttu-id="9fff9-101">İçinde toohello oturum [Azure portal](https://portal.azure.com/) http://portal.azure.com/ adresindeki.</span><span class="sxs-lookup"><span data-stu-id="9fff9-101">Log in toohello [Azure portal](https://portal.azure.com/) at http://portal.azure.com/.</span></span>
2. <span data-ttu-id="9fff9-102">Merhaba sol başlığında tıklatın **TÜMÜNE Gözat**.</span><span class="sxs-lookup"><span data-stu-id="9fff9-102">In hello left banner, click **BROWSE ALL**.</span></span> <span data-ttu-id="9fff9-103">Merhaba **Gözat** dikey penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9fff9-103">hello **Browse** blade is displayed.</span></span>
3. <span data-ttu-id="9fff9-104">Kaydırın ve tıklatın **SQL sunucuları**.</span><span class="sxs-lookup"><span data-stu-id="9fff9-104">Scroll and click **SQL servers**.</span></span> <span data-ttu-id="9fff9-105">Merhaba **SQL sunucuları** dikey penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9fff9-105">hello **SQL servers** blade is displayed.</span></span>
   
    ![Azure SQL veritabanı sunucunuzun hello Portalı'nda bulunamıyor][b21-FindServerInPortal]
4. <span data-ttu-id="9fff9-107">Merhaba kolaylık sağlamak için tıklatın önceki hello denetiminde en aza **Gözat** dikey.</span><span class="sxs-lookup"><span data-stu-id="9fff9-107">For convenience, click hello minimize control on hello earlier **Browse** blade.</span></span>
5. <span data-ttu-id="9fff9-108">Merhaba filtre metin kutusuna hello sunucunuzun adını yazmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="9fff9-108">In hello filter text box, start typing hello name of your server.</span></span> <span data-ttu-id="9fff9-109">Satır görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9fff9-109">Your row is displayed.</span></span>
6. <span data-ttu-id="9fff9-110">Sunucunuz için Hello satıra tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9fff9-110">Click hello row for your server.</span></span> <span data-ttu-id="9fff9-111">Sunucunuz için bir dikey pencerede görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9fff9-111">A blade for your server is displayed.</span></span>
7. <span data-ttu-id="9fff9-112">Sunucu dikey penceresinde **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="9fff9-112">On your server blade, click **Settings**.</span></span> <span data-ttu-id="9fff9-113">Merhaba **ayarları** dikey penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9fff9-113">hello **Settings** blade is displayed.</span></span>
8. <span data-ttu-id="9fff9-114">Tıklatın **Güvenlik Duvarı**.</span><span class="sxs-lookup"><span data-stu-id="9fff9-114">Click **Firewall**.</span></span> <span data-ttu-id="9fff9-115">Merhaba **güvenlik duvarı ayarlarını** dikey penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9fff9-115">hello **Firewall Settings** blade is displayed.</span></span>
   
    ![Ayarlar > Güvenlik Duvarı][b31-SettingsFirewallNavig]
9. <span data-ttu-id="9fff9-117">Tıklatın **istemcisi ekleme IP**.</span><span class="sxs-lookup"><span data-stu-id="9fff9-117">Click **Add Client IP**.</span></span> <span data-ttu-id="9fff9-118">Merhaba ilk metin kutusuna, yeni kural için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="9fff9-118">Type in a name for your new rule into hello first text box.</span></span>
10. <span data-ttu-id="9fff9-119">Merhaba düşük ve yüksek türünde IP adresi istediğiniz hello aralığı için değerleri tooenable.</span><span class="sxs-lookup"><span data-stu-id="9fff9-119">Type in hello low and high IP address values for hello range you want tooenable.</span></span>
    
    * <span data-ttu-id="9fff9-120">Kullanışlı toohave hello düşük değer sonu olabilir **.0** ve hello ile yüksek **.255**.</span><span class="sxs-lookup"><span data-stu-id="9fff9-120">It can be handy toohave hello low value end with **.0** and hello high with **.255**.</span></span>
    
    ![Bir IP adresi aralığı tooallow Ekle][b41-AddRange]
11. <span data-ttu-id="9fff9-122">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9fff9-122">Click **Save**.</span></span>

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
