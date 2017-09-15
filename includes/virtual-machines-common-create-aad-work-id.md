
<br>

> [!NOTE]
> <span data-ttu-id="1b34f-101">Bir yönetici tarafından bir kullanıcı adı ve parola verildi, zaten bir iş veya Okul kimlik şansı yoktur (bazen adlı bir *Kuruluş Kimliği*).</span><span class="sxs-lookup"><span data-stu-id="1b34f-101">If you were given a user name and password by an administrator, there's a good chance that you already have a work or school ID (also sometimes called an *organizational ID*).</span></span> <span data-ttu-id="1b34f-102">Öyleyse, hemen bir gerektiren Azure kaynaklarına erişmek için Azure hesabınızı kullanmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b34f-102">If so, you can immediately begin to use your Azure account to access Azure resources that require one.</span></span> <span data-ttu-id="1b34f-103">Bu kaynakları kullanamazsınız bulursanız, Yardım için bu makalenin geri dönmek gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="1b34f-103">If you find that you cannot use those resources, you may need to return to this article for help.</span></span> <span data-ttu-id="1b34f-104">Daha fazla bilgi için bkz: [için kullanabileceğiniz hesaplar oturum](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) ve [nasıl bir Azure aboneliğine Azure AD ile ilgili](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span><span class="sxs-lookup"><span data-stu-id="1b34f-104">For more information, see [Accounts that you can use for sign in](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) and [How an Azure subscription is related to Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span></span>
> 
> 

<span data-ttu-id="1b34f-105">Basit adımlardır.</span><span class="sxs-lookup"><span data-stu-id="1b34f-105">The steps are simple.</span></span> <span data-ttu-id="1b34f-106">Klasik Azure portalı, kimlik, imzalı bulmak için varsayılan Azure Active Directory etki alanı bulmak ve gerekir Azure ortak yönetici olarak yeni bir kullanıcı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1b34f-106">You need to locate your signed on identity in the Azure classic portal, discover your default Azure Active Directory domain, and add a new user to it as an Azure co-administrator.</span></span>

## <a name="locate-your-default-directory-in-the-azure-classic-portal"></a><span data-ttu-id="1b34f-107">Varsayılan dizini Klasik Azure portalında bulun</span><span class="sxs-lookup"><span data-stu-id="1b34f-107">Locate your default directory in the Azure classic portal</span></span>
<span data-ttu-id="1b34f-108">Oturum açmayı Start [Klasik Azure portalı](https://manage.windowsazure.com) kişisel Microsoft hesabı kimliğinizi ile.</span><span class="sxs-lookup"><span data-stu-id="1b34f-108">Start by logging in to the [Azure classic portal](https://manage.windowsazure.com) with your personal Microsoft account identity.</span></span> <span data-ttu-id="1b34f-109">Günlüğe kaydedildikten sonra mavi bölmenin sol tarafındaki aşağı kaydırın ve tıklayın **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="1b34f-109">After you are logged in, scroll down the blue panel on the left side and click **ACTIVE DIRECTORY**.</span></span>

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

<span data-ttu-id="1b34f-111">Azure'da kimlik bilgilerinizi hakkında bazı bilgiler bularak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="1b34f-111">Let's start by finding some information about your identity in Azure.</span></span> <span data-ttu-id="1b34f-112">Bir varsayılan dizin olduğunu gösteren ana bölmede aşağıdaki gibi bir şey görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b34f-112">You should see something like the following in the main pane, showing that you have one default directory.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

<span data-ttu-id="1b34f-113">Daha fazla bilgi bazı şimdi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="1b34f-113">Let's find out some more information about it.</span></span> <span data-ttu-id="1b34f-114">Varsayılan dizin özelliklerini getirir varsayılan dizin satıra tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1b34f-114">Click the default directory row, which brings you into the default directory properties.</span></span>  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

<span data-ttu-id="1b34f-115">Varsayılan etki alanı adını görüntülemek için **etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="1b34f-115">To view the default domain name, click **DOMAINS**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

<span data-ttu-id="1b34f-116">Burada, Azure hesabı oluşturulduğunda, Azure Active Directory karma değeri (metin dizesinden oluşturulan bir sayı) kişisel varsayılan bir etki alanı oluşturduğunuz görüyor olmalısınız bir alt etki onmicrosoft.com kullanılan, kişisel kimliği.</span><span class="sxs-lookup"><span data-stu-id="1b34f-116">Here you should be able to see that when the Azure account was created, Azure Active Directory created a personal default domain that is a hash value (a number generated from a string of text) of your personal ID used as a subdomain of onmicrosoft.com.</span></span> <span data-ttu-id="1b34f-117">Bu, artık yeni bir kullanıcı ekleyeceğiniz etki alanıdır.</span><span class="sxs-lookup"><span data-stu-id="1b34f-117">That's the domain to which you will now add a new user.</span></span>

## <a name="creating-a-new-user-in-the-default-domain"></a><span data-ttu-id="1b34f-118">Varsayılan etki alanında yeni bir kullanıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1b34f-118">Creating a new user in the default domain</span></span>
<span data-ttu-id="1b34f-119">Tıklatın **kullanıcılar** ve tek kişisel hesabınız için bakın.</span><span class="sxs-lookup"><span data-stu-id="1b34f-119">Click **USERS** and look for your single personal account.</span></span> <span data-ttu-id="1b34f-120">İçinde görmelisiniz **kaynağı** bu sütun bir **Microsoft hesabı**.</span><span class="sxs-lookup"><span data-stu-id="1b34f-120">You should see in the **SOURCED FROM** column that it is a **Microsoft account**.</span></span> <span data-ttu-id="1b34f-121">Varsayılan olarak bir kullanıcı oluşturmak istiyoruz. onmicrosoft.com Azure Active Directory etki alanı.</span><span class="sxs-lookup"><span data-stu-id="1b34f-121">We want to create a user in your default .onmicrosoft.com Azure Active Directory domain.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

<span data-ttu-id="1b34f-122">İzleyin oluşturacağız [bu yönergeleri](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) sonraki birkaç adımda, ancak belirli bir örneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="1b34f-122">We're going to follow [these instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in the next few steps, but use a specific example.</span></span>

<span data-ttu-id="1b34f-123">Sayfanın alt kısmındaki tıklatın **+ ADD USER**.</span><span class="sxs-lookup"><span data-stu-id="1b34f-123">At the bottom of the page, click **+ADD USER**.</span></span> <span data-ttu-id="1b34f-124">Görüntülenen sayfasında yeni bir kullanıcı adı yazın ve olun **kullanıcı türü** bir **kuruluşunuzdaki yeni kullanıcı**.</span><span class="sxs-lookup"><span data-stu-id="1b34f-124">In the page that appears, type the new user name, and make the **Type of User** a **New user in your organization**.</span></span> <span data-ttu-id="1b34f-125">Bu örnekte, yeni kullanıcı adıdır `ahmet`.</span><span class="sxs-lookup"><span data-stu-id="1b34f-125">In this example, the new user name is `ahmet`.</span></span> <span data-ttu-id="1b34f-126">Bulunan varsayılan etki alanı daha önce etki alanı için ahmet kişinin e-posta adresi olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="1b34f-126">Select the default domain that you discovered previously as the domain for ahmet's email address.</span></span> <span data-ttu-id="1b34f-127">Bittiğinde İleri okuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1b34f-127">Click the next arrow when finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

<span data-ttu-id="1b34f-128">Daha fazla ayrıntı için Ahmet ekleyin, ancak uygun seçtiğinizden emin olun **ROL** değeri.</span><span class="sxs-lookup"><span data-stu-id="1b34f-128">Add more details for Ahmet, but make sure to select the appropriate **ROLE** value.</span></span> <span data-ttu-id="1b34f-129">Kullanımı kolay **genel yönetici** emin şeyler yapmaya çalışır, ancak daha düşük bir rolü kullanabilirsiniz, bu iyi bir fikirdir.</span><span class="sxs-lookup"><span data-stu-id="1b34f-129">It's easy to use **Global Admin** to make sure things are working, but if you can use a lesser role, that's a good idea.</span></span> <span data-ttu-id="1b34f-130">Bu örnekte **kullanıcı** rol.</span><span class="sxs-lookup"><span data-stu-id="1b34f-130">This example uses the **User** role.</span></span> <span data-ttu-id="1b34f-131">(Hakkında daha fazla bilgi [yönetici izinleri rolüne göre](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Her oturum açma işlemi için çok faktörlü kimlik doğrulamasını kullanmak istemediğiniz sürece çok faktörlü kimlik doğrulamasını etkinleştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="1b34f-131">(Find out more at [Administrator permissions by role](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Do not enable multi-factor authentication unless you want to use multifactor authentication for each log in operation.</span></span> <span data-ttu-id="1b34f-132">İşiniz bittiğinde İleri okuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1b34f-132">Click the next arrow when you're finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

<span data-ttu-id="1b34f-133">Tıklatın **oluşturma** oluşturmak ve geçici bir parola için Ahmet görüntülemek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1b34f-133">Click the **create** button to generate and display a temporary password for Ahmet.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

<span data-ttu-id="1b34f-134">Kullanıcı adı e-posta adresi kopyalamak veya kullanmak **parola IN e-posta Gönder**.</span><span class="sxs-lookup"><span data-stu-id="1b34f-134">Copy the user name email address, or use **SEND PASSWORD IN EMAIL**.</span></span> <span data-ttu-id="1b34f-135">Kısa süre içinde oturum açmak için bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b34f-135">You'll need the information to log on shortly.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

<span data-ttu-id="1b34f-136">Artık yeni kullanıcı görmelisiniz **Ahmet Geliştirici**, Azure Active Directory'den kaynaklı.</span><span class="sxs-lookup"><span data-stu-id="1b34f-136">Now you should see the new user, **Ahmet the Developer**, sourced from Azure Active Directory.</span></span> <span data-ttu-id="1b34f-137">Azure Active Directory ile yeni iş veya Okul kimlik oluşturduğunuzu düşünün.</span><span class="sxs-lookup"><span data-stu-id="1b34f-137">You've created the new work or school identity with Azure Active Directory.</span></span> <span data-ttu-id="1b34f-138">Ancak, bu kimlik henüz Azure kaynaklarını kullanmak için izinlere sahip değil.</span><span class="sxs-lookup"><span data-stu-id="1b34f-138">However, this identity does not yet have permissions to use Azure resources.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

<span data-ttu-id="1b34f-139">Kullanırsanız **parola IN e-posta Gönder**, aşağıdaki tür bir e-posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="1b34f-139">If you use **SEND PASSWORD IN EMAIL**, the following kind of email is sent.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a><span data-ttu-id="1b34f-140">Abonelikler için Azure ortak yönetici hakları ekleme</span><span class="sxs-lookup"><span data-stu-id="1b34f-140">Adding Azure co-administrator rights for subscriptions</span></span>
<span data-ttu-id="1b34f-141">Şimdi yeni kullanıcı Yönetim Portalı'na oturum açabilmeniz için yeni kullanıcı aboneliğinizin ortak yönetici eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b34f-141">Now you need to add the new user as a co-administrator of your subscription so the new user can sign in to the Management Portal.</span></span> <span data-ttu-id="1b34f-142">Bunu yapmak için sol panelinde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="1b34f-142">To do this, in the lower-left panel click **Settings**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

<span data-ttu-id="1b34f-143">Ana Ayarlar bölümünde **Yöneticiler** üst ve, yalnızca kişisel Microsoft hesabı kimliğinizi görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b34f-143">In the main settings area, click **ADMINISTRATORS** at the top and you should see only your personal Microsoft account identity.</span></span> <span data-ttu-id="1b34f-144">Sayfanın alt kısmındaki tıklatın **+ Ekle** bir ortak yönetici belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="1b34f-144">At the bottom of the page, click **+ADD** to specify a co-administrator.</span></span> <span data-ttu-id="1b34f-145">Burada, varsayılan etki alanı dahil olmak üzere, oluşturmuştunuz yeni kullanıcının e-posta adresi girin.</span><span class="sxs-lookup"><span data-stu-id="1b34f-145">Here, enter the email address of the new user you had created, including your default domain.</span></span> <span data-ttu-id="1b34f-146">Sonraki ekran görüntüsünde gösterildiği gibi kullanıcı varsayılan dizini için yanında yeşil bir onay işareti görünür.</span><span class="sxs-lookup"><span data-stu-id="1b34f-146">As shown in the next screenshot, a green check mark appears next to the user for the default directory.</span></span> <span data-ttu-id="1b34f-147">Tüm yönetmek bu kullanıcı istediğiniz abonelikleri seçin unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1b34f-147">Remember to select all of the subscriptions that you would like this user to be able to administer.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

<span data-ttu-id="1b34f-148">İşiniz bittiğinde, yeni bir ortak yönetici kimlik bilgilerinizi dahil olmak üzere iki kullanıcıları artık görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="1b34f-148">When you are done, you should now see two users, including your new co-administrator identity.</span></span> <span data-ttu-id="1b34f-149">Dışında portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1b34f-149">Log out of the portal.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-the-new-users-password"></a><span data-ttu-id="1b34f-150">Oturum açmayı ve yeni kullanıcının parolasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="1b34f-150">Logging in and changing the new user's password</span></span>
<span data-ttu-id="1b34f-151">Oluşturduğunuz yeni kullanıcı olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1b34f-151">Log in as the new user you created.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

<span data-ttu-id="1b34f-152">Hemen yeni bir parola oluşturmanız istenir.</span><span class="sxs-lookup"><span data-stu-id="1b34f-152">You will immediately be prompted to create a new password.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

<span data-ttu-id="1b34f-153">Aşağıdaki gibi görünür başarı ile ödülünü.</span><span class="sxs-lookup"><span data-stu-id="1b34f-153">You should be rewarded with success that looks like the following.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a><span data-ttu-id="1b34f-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1b34f-154">Next steps</span></span>
<span data-ttu-id="1b34f-155">Kullanmak için yeni bir Azure Active Directory kimlik bilgilerinizi şimdi kullanabilirsiniz [Azure kaynak grubu şablonları](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="1b34f-155">You can now use your new Azure Active Directory identity to use [Azure resource group templates](../articles/xplat-cli-azure-resource-manager.md).</span></span>

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how to set them up, please read http://aka.ms/Dhf67j.
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
