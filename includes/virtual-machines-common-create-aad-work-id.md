
<br>

> [!NOTE]
> <span data-ttu-id="dcb07-101">Bir yönetici tarafından bir kullanıcı adı ve parola verildi, zaten bir iş veya Okul kimlik şansı yoktur (bazen adlı bir *Kuruluş Kimliği*).</span><span class="sxs-lookup"><span data-stu-id="dcb07-101">If you were given a user name and password by an administrator, there's a good chance that you already have a work or school ID (also sometimes called an *organizational ID*).</span></span> <span data-ttu-id="dcb07-102">Bu durumda, Azure hesabı tooaccess bir gerektiren Azure kaynaklarını toouse hemen başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dcb07-102">If so, you can immediately begin toouse your Azure account tooaccess Azure resources that require one.</span></span> <span data-ttu-id="dcb07-103">Bu kaynakları kullanamazsınız bulursanız, Yardım için tooreturn toothis makale gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="dcb07-103">If you find that you cannot use those resources, you may need tooreturn toothis article for help.</span></span> <span data-ttu-id="dcb07-104">Daha fazla bilgi için bkz: [için kullanabileceğiniz hesaplar oturum](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) ve [nasıl bir Azure aboneliği olan ilgili tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span><span class="sxs-lookup"><span data-stu-id="dcb07-104">For more information, see [Accounts that you can use for sign in](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) and [How an Azure subscription is related tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span></span>
> 
> 

<span data-ttu-id="dcb07-105">Merhaba adımlar basittir.</span><span class="sxs-lookup"><span data-stu-id="dcb07-105">hello steps are simple.</span></span> <span data-ttu-id="dcb07-106">Toolocate, imzalı ihtiyacınız hello Klasik Azure portalı kimliğinde, varsayılan Azure Active Directory etki alanınızın bulmak ve yeni bir kullanıcı tooit Azure ortak yönetici olarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="dcb07-106">You need toolocate your signed on identity in hello Azure classic portal, discover your default Azure Active Directory domain, and add a new user tooit as an Azure co-administrator.</span></span>

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a><span data-ttu-id="dcb07-107">Varsayılan dizini hello Klasik Azure portalı bulun</span><span class="sxs-lookup"><span data-stu-id="dcb07-107">Locate your default directory in hello Azure classic portal</span></span>
<span data-ttu-id="dcb07-108">Başlat toohello içinde oturum açarak [Klasik Azure portalı](https://manage.windowsazure.com) kişisel Microsoft hesabı kimliğinizi ile.</span><span class="sxs-lookup"><span data-stu-id="dcb07-108">Start by logging in toohello [Azure classic portal](https://manage.windowsazure.com) with your personal Microsoft account identity.</span></span> <span data-ttu-id="dcb07-109">Günlüğe kaydedildikten sonra hello mavi hello yan sol panelde aşağı kaydırın ve tıklayın **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="dcb07-109">After you are logged in, scroll down hello blue panel on hello left side and click **ACTIVE DIRECTORY**.</span></span>

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

<span data-ttu-id="dcb07-111">Azure'da kimlik bilgilerinizi hakkında bazı bilgiler bularak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="dcb07-111">Let's start by finding some information about your identity in Azure.</span></span> <span data-ttu-id="dcb07-112">Merhaba ana bölmede aşağıdaki, bir varsayılan dizin olduğunu gösteren hello gibi bir şey görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="dcb07-112">You should see something like hello following in hello main pane, showing that you have one default directory.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

<span data-ttu-id="dcb07-113">Daha fazla bilgi bazı şimdi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="dcb07-113">Let's find out some more information about it.</span></span> <span data-ttu-id="dcb07-114">Merhaba varsayılan dizin özelliklerini getirir hello varsayılan dizin satıra tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dcb07-114">Click hello default directory row, which brings you into hello default directory properties.</span></span>  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

<span data-ttu-id="dcb07-115">tooview hello varsayılan etki alanı adını tıklatın **etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="dcb07-115">tooview hello default domain name, click **DOMAINS**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

<span data-ttu-id="dcb07-116">Burada hello Azure hesabı oluşturulduğunda, Azure Active Directory karma değeri (metin dizesinden oluşturulan bir sayı) kişisel varsayılan bir etki alanı oluşturduğunuz mümkün toosee olmalıdır bir alt etki onmicrosoft.com kullanılan, kişisel kimliği. Şimdi yeni bir kullanıcı ekleyeceksiniz hello etki alanı toowhich olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="dcb07-116">Here you should be able toosee that when hello Azure account was created, Azure Active Directory created a personal default domain that is a hash value (a number generated from a string of text) of your personal ID used as a subdomain of onmicrosoft.com. That's hello domain toowhich you will now add a new user.</span></span>

## <a name="creating-a-new-user-in-hello-default-domain"></a><span data-ttu-id="dcb07-117">Merhaba varsayılan etki alanında yeni bir kullanıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dcb07-117">Creating a new user in hello default domain</span></span>
<span data-ttu-id="dcb07-118">Tıklatın **kullanıcılar** ve tek kişisel hesabınız için bakın.</span><span class="sxs-lookup"><span data-stu-id="dcb07-118">Click **USERS** and look for your single personal account.</span></span> <span data-ttu-id="dcb07-119">Hello görmelisiniz **kaynağı** bu sütun bir **Microsoft hesabı**.</span><span class="sxs-lookup"><span data-stu-id="dcb07-119">You should see in hello **SOURCED FROM** column that it is a **Microsoft account**.</span></span> <span data-ttu-id="dcb07-120">Kullanıcı varsayılan olarak toocreate istiyoruz. onmicrosoft.com Azure Active Directory etki alanı.</span><span class="sxs-lookup"><span data-stu-id="dcb07-120">We want toocreate a user in your default .onmicrosoft.com Azure Active Directory domain.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

<span data-ttu-id="dcb07-121">Toofollow yapacağız [bu yönergeleri](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) , sonraki birkaç adımda Merhaba, ancak belirli bir örneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="dcb07-121">We're going toofollow [these instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in hello next few steps, but use a specific example.</span></span>

<span data-ttu-id="dcb07-122">Merhaba sayfasının Hello altında tıklatın **+ ADD USER**.</span><span class="sxs-lookup"><span data-stu-id="dcb07-122">At hello bottom of hello page, click **+ADD USER**.</span></span> <span data-ttu-id="dcb07-123">Görüntülenen hello sayfasında hello yeni bir kullanıcı adı yazın ve hello olun **kullanıcı türü** bir **kuruluşunuzdaki yeni kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="dcb07-123">In hello page that appears, type hello new user name, and make hello **Type of User** a **New user in your organization**.</span></span> <span data-ttu-id="dcb07-124">Bu örnekte, hello yeni bir kullanıcı adı olan `ahmet`.</span><span class="sxs-lookup"><span data-stu-id="dcb07-124">In this example, hello new user name is `ahmet`.</span></span> <span data-ttu-id="dcb07-125">Bulunan hello varsayılan etki alanı, daha önce ahmet kişinin e-posta adresi için hello etki alanı olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="dcb07-125">Select hello default domain that you discovered previously as hello domain for ahmet's email address.</span></span> <span data-ttu-id="dcb07-126">Tamamlandığında hello İleri okuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dcb07-126">Click hello next arrow when finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

<span data-ttu-id="dcb07-127">Daha fazla ayrıntı için Ahmet ekleyin, ama emin tooselect hello uygun hale **ROL** değeri.</span><span class="sxs-lookup"><span data-stu-id="dcb07-127">Add more details for Ahmet, but make sure tooselect hello appropriate **ROLE** value.</span></span> <span data-ttu-id="dcb07-128">Kolay toouse olan **genel yönetici** toomake emin şeyler çalışıyor, ancak daha düşük bir rolü kullanabilirsiniz, iyi bir fikirdir.</span><span class="sxs-lookup"><span data-stu-id="dcb07-128">It's easy toouse **Global Admin** toomake sure things are working, but if you can use a lesser role, that's a good idea.</span></span> <span data-ttu-id="dcb07-129">Bu örnek hello kullanır **kullanıcı** rol.</span><span class="sxs-lookup"><span data-stu-id="dcb07-129">This example uses hello **User** role.</span></span> <span data-ttu-id="dcb07-130">(Hakkında daha fazla bilgi [yönetici izinleri rolüne göre](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Her oturum açma işlemi için çok faktörlü kimlik doğrulama toouse istemediğiniz sürece çok faktörlü kimlik doğrulamasını etkinleştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="dcb07-130">(Find out more at [Administrator permissions by role](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Do not enable multi-factor authentication unless you want toouse multifactor authentication for each log in operation.</span></span> <span data-ttu-id="dcb07-131">İşiniz bittiğinde hello İleri okuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dcb07-131">Click hello next arrow when you're finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

<span data-ttu-id="dcb07-132">Hello tıklatın **oluşturmak** düğmesini toogenerate ve geçici bir parola için Ahmet görüntüler.</span><span class="sxs-lookup"><span data-stu-id="dcb07-132">Click hello **create** button toogenerate and display a temporary password for Ahmet.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

<span data-ttu-id="dcb07-133">Merhaba kullanıcı adı e-posta adresi kopyalamak veya kullanmak **parola IN e-posta Gönder**.</span><span class="sxs-lookup"><span data-stu-id="dcb07-133">Copy hello user name email address, or use **SEND PASSWORD IN EMAIL**.</span></span> <span data-ttu-id="dcb07-134">Merhaba bilgi toolog üzerinde kısa bir süre sonra ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="dcb07-134">You'll need hello information toolog on shortly.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

<span data-ttu-id="dcb07-135">Artık hello yeni kullanıcı görmelisiniz **Ahmet hello Geliştirici**, Azure Active Directory'den kaynaklı.</span><span class="sxs-lookup"><span data-stu-id="dcb07-135">Now you should see hello new user, **Ahmet hello Developer**, sourced from Azure Active Directory.</span></span> <span data-ttu-id="dcb07-136">Azure Active Directory ile Merhaba yeni iş veya Okul kimlik oluşturduğunuzu düşünün.</span><span class="sxs-lookup"><span data-stu-id="dcb07-136">You've created hello new work or school identity with Azure Active Directory.</span></span> <span data-ttu-id="dcb07-137">Ancak, bu kimliği henüz izinleri toouse Azure sahip kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="dcb07-137">However, this identity does not yet have permissions toouse Azure resources.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

<span data-ttu-id="dcb07-138">Kullanırsanız **parola IN e-posta Gönder**, e-posta türünü aşağıdaki hello gönderilir.</span><span class="sxs-lookup"><span data-stu-id="dcb07-138">If you use **SEND PASSWORD IN EMAIL**, hello following kind of email is sent.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a><span data-ttu-id="dcb07-139">Abonelikler için Azure ortak yönetici hakları ekleme</span><span class="sxs-lookup"><span data-stu-id="dcb07-139">Adding Azure co-administrator rights for subscriptions</span></span>
<span data-ttu-id="dcb07-140">Şimdi Hello yeni kullanıcı toohello Yönetim Portalı oturum için bir ortak, aboneliğinizi yönetici tooadd hello yeni kullanıcı gerekir.</span><span class="sxs-lookup"><span data-stu-id="dcb07-140">Now you need tooadd hello new user as a co-administrator of your subscription so hello new user can sign in toohello Management Portal.</span></span> <span data-ttu-id="dcb07-141">Bu, hello sol panelinde tıklatın toodo **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="dcb07-141">toodo this, in hello lower-left panel click **Settings**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

<span data-ttu-id="dcb07-142">Merhaba Ana Ayarlar bölümünde **Yöneticiler** hello üst ve yalnızca kişisel Microsoft hesabı kimliğinizi görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="dcb07-142">In hello main settings area, click **ADMINISTRATORS** at hello top and you should see only your personal Microsoft account identity.</span></span> <span data-ttu-id="dcb07-143">Merhaba sayfasının Hello altında tıklatın **+ Ekle** toospecify bir ortak yönetici.</span><span class="sxs-lookup"><span data-stu-id="dcb07-143">At hello bottom of hello page, click **+ADD** toospecify a co-administrator.</span></span> <span data-ttu-id="dcb07-144">Burada, varsayılan etki alanı dahil olmak üzere, oluşturmuştunuz hello yeni kullanıcı hello e-posta adresini girin.</span><span class="sxs-lookup"><span data-stu-id="dcb07-144">Here, enter hello email address of hello new user you had created, including your default domain.</span></span> <span data-ttu-id="dcb07-145">Hello sonraki ekran görüntüsünde gösterildiği gibi sonraki toohello kullanıcı hello varsayılan dizin için yeşil bir onay işareti görünür.</span><span class="sxs-lookup"><span data-stu-id="dcb07-145">As shown in hello next screenshot, a green check mark appears next toohello user for hello default directory.</span></span> <span data-ttu-id="dcb07-146">Tooselect unutmayın tüm hello abonelikleri bu kullanıcı toobe mümkün tooadminister istersiniz.</span><span class="sxs-lookup"><span data-stu-id="dcb07-146">Remember tooselect all of hello subscriptions that you would like this user toobe able tooadminister.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

<span data-ttu-id="dcb07-147">İşiniz bittiğinde, yeni bir ortak yönetici kimlik bilgilerinizi dahil olmak üzere iki kullanıcıları artık görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="dcb07-147">When you are done, you should now see two users, including your new co-administrator identity.</span></span> <span data-ttu-id="dcb07-148">Dışında Hello portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="dcb07-148">Log out of hello portal.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a><span data-ttu-id="dcb07-149">Oturum açmayı ve hello yeni kullanıcının parolasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="dcb07-149">Logging in and changing hello new user's password</span></span>
<span data-ttu-id="dcb07-150">Oluşturduğunuz hello yeni bir kullanıcı olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="dcb07-150">Log in as hello new user you created.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

<span data-ttu-id="dcb07-151">Yeni bir parola istendiğinde toocreate hemen olacaktır.</span><span class="sxs-lookup"><span data-stu-id="dcb07-151">You will immediately be prompted toocreate a new password.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

<span data-ttu-id="dcb07-152">Merhaba şuna benzeyen başarı ile ödülünü.</span><span class="sxs-lookup"><span data-stu-id="dcb07-152">You should be rewarded with success that looks like hello following.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a><span data-ttu-id="dcb07-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dcb07-153">Next steps</span></span>
<span data-ttu-id="dcb07-154">Artık, yeni Azure Active Directory kimlik toouse kullanabilirsiniz [Azure kaynak grubu şablonları](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="dcb07-154">You can now use your new Azure Active Directory identity toouse [Azure resource group templates](../articles/xplat-cli-azure-resource-manager.md).</span></span>

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how tooset them up, please read http://aka.ms/Dhf67j.
    Username: ahmet@aztrainpassxxxxxoutlook.onmicrosoft.com
    Password: *********
    /info:    Added subscription Azure Pass
    info:    Setting subscription Azure Pass as default
    +
    info:    login command OK
    ralph@local:~$ azure config mode arm
    info:    New mode is arm
    ralph@local:~$ azure group list
    info:    Executing command group list
    + Listing resource groups
    info:    No matched resource groups were found
    info:    group list command OK
    ralph@local:~$ azure group create newgroup westus
    info:    Executing command group create
    + Getting resource group newgroup
    + Creating resource group newgroup
    info:    Created resource group newgroup
    data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/newgroup
    data:    Name:                newgroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags:
    data:
    info:    group create command OK
