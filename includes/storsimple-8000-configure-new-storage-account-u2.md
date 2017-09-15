<!--author=alkohli last changed: 01/20/17-->


#### <a name="to-add-a-storage-account-credential-in-the-same-azure-subscription-as-the-storsimple-device-manager-service"></a><span data-ttu-id="71aa4-101">StorSimple Cihaz Yöneticisi hizmetiyle aynı Azure aboneliğinde depolama hesabı kimlik bilgisi eklemek için</span><span class="sxs-lookup"><span data-stu-id="71aa4-101">To add a storage account credential in the same Azure subscription as the StorSimple Device Manager service</span></span>

1. <span data-ttu-id="71aa4-102">StorSimple Cihaz Yöneticisi hizmetinize gidin.</span><span class="sxs-lookup"><span data-stu-id="71aa4-102">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="71aa4-103">**Yapılandırma** bölümünde **Depolama hesabı kimlik bilgileri**’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="71aa4-103">In the **Configuration** section, click **Storage account credentials**.</span></span>

    ![Depolama hesabı kimlik bilgileri](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct1.png)

2. <span data-ttu-id="71aa4-105">**Depolama hesabı kimlik bilgileri** dikey penceresinde **+ Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="71aa4-105">On the **Storage account credentials** blade, click **+ Add**.</span></span>

    ![Depolama hesabı kimlik bilgisi ekleyin](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct2.png)

3. <span data-ttu-id="71aa4-107">**Depolama hesabı kimlik bilgisi ekle** dikey penceresinde aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="71aa4-107">In the **Add a storage account credential** blade, do the following steps:</span></span>

    1. <span data-ttu-id="71aa4-108">Hizmetinizle aynı Azure aboneliğinde depolama kimlik bilgisi eklediğinizden, **Geçerli**’nin seçili olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="71aa4-108">As you are adding a storage account credential in the same Azure subscription as your service, ensure that **Current** is selected.</span></span>

    2. <span data-ttu-id="71aa4-109">**Depolama hesabı** açılan listesinden mevcut bir depolama hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="71aa4-109">From the **storage account** dropdown list, select an existing storage account.</span></span>

    3. <span data-ttu-id="71aa4-110">Seçilen depolama hesabına bağlı olarak **konum** görüntülenir (gri olur ve buradan değiştirilemez).</span><span class="sxs-lookup"><span data-stu-id="71aa4-110">Based on the storage account selected, the **location** will be displayed (grayed out and cannot be changed here).</span></span>

    4. <span data-ttu-id="71aa4-111">Cihazınız ve bulut arasındaki ağ iletişimi için güvenli bir kanal oluşturmak için **SSL Modunu Etkinleştir**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="71aa4-111">Select **Enable SSL Mode** to create a secure channel for network communication between your device and the cloud.</span></span> <span data-ttu-id="71aa4-112">**SSL’yi Etkinleştir** onay kutusunu yalnızca özel bulutta işlem yapıyorsanız temizleyin.</span><span class="sxs-lookup"><span data-stu-id="71aa4-112">Disable **Enable SSL** only if you are operating within a private cloud.</span></span>

        ![Depolama hesabı kimlik bilgileri ekleme dikey penceresi](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct3.png)

    5. <span data-ttu-id="71aa4-114">Depolama hesabı kimlik bilgisine yönelik iş oluşturma işlemini başlatmak için **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="71aa4-114">Click **Add** to start the job creation for the storage account credential.</span></span> <span data-ttu-id="71aa4-115">Depolama hesabı kimlik bilgisi sorunsuz bir şekilde oluşturulduğunda size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="71aa4-115">You will be notified after the storage account credential is successfully created.</span></span>

        ![Depolama hesabı kimlik bilgileri için başarı bildirimi](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct5.png)

<span data-ttu-id="71aa4-117">Yeni oluşturulan depolama hesabı kimlik bilgisi, **Depolama hesabı kimlik bilgileri** listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="71aa4-117">The newly created storage account credential will be displayed under the list of **Storage account credentials**.</span></span>

![Depolama hesabı kimlik bilgileri listesi](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct6.png)

