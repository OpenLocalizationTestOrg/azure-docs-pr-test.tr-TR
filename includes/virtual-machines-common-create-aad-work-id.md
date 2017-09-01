
<br>

> [!NOTE]
> Bir yönetici tarafından bir kullanıcı adı ve parola verildi, zaten bir iş veya Okul kimlik şansı yoktur (bazen adlı bir *Kuruluş Kimliği*). Öyleyse, hemen bir gerektiren Azure kaynaklarına erişmek için Azure hesabınızı kullanmaya başlayabilirsiniz. Bu kaynakları kullanamazsınız bulursanız, Yardım için bu makalenin geri dönmek gerekebilir. Daha fazla bilgi için bkz: [için kullanabileceğiniz hesaplar oturum](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) ve [nasıl bir Azure aboneliğine Azure AD ile ilgili](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).
> 
> 

Basit adımlardır. Klasik Azure portalı, kimlik, imzalı bulmak için varsayılan Azure Active Directory etki alanı bulmak ve gerekir Azure ortak yönetici olarak yeni bir kullanıcı ekleyin.

## <a name="locate-your-default-directory-in-the-azure-classic-portal"></a>Varsayılan dizini Klasik Azure portalında bulun
Oturum açmayı Start [Klasik Azure portalı](https://manage.windowsazure.com) kişisel Microsoft hesabı kimliğinizi ile. Günlüğe kaydedildikten sonra mavi bölmenin sol tarafındaki aşağı kaydırın ve tıklayın **ACTIVE DIRECTORY**.

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

Azure'da kimlik bilgilerinizi hakkında bazı bilgiler bularak başlayalım. Bir varsayılan dizin olduğunu gösteren ana bölmede aşağıdaki gibi bir şey görmeniz gerekir.

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

Daha fazla bilgi bazı şimdi öğrenin. Varsayılan dizin özelliklerini getirir varsayılan dizin satıra tıklayın.  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

Varsayılan etki alanı adını görüntülemek için **etki alanları**.

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

Burada, Azure hesabı oluşturulduğunda, Azure Active Directory karma değeri (metin dizesinden oluşturulan bir sayı) kişisel varsayılan bir etki alanı oluşturduğunuz görüyor olmalısınız bir alt etki onmicrosoft.com kullanılan, kişisel kimliği. Bu, artık yeni bir kullanıcı ekleyeceğiniz etki alanıdır.

## <a name="creating-a-new-user-in-the-default-domain"></a>Varsayılan etki alanında yeni bir kullanıcı oluşturma
Tıklatın **kullanıcılar** ve tek kişisel hesabınız için bakın. İçinde görmelisiniz **kaynağı** bu sütun bir **Microsoft hesabı**. Varsayılan olarak bir kullanıcı oluşturmak istiyoruz. onmicrosoft.com Azure Active Directory etki alanı.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

İzleyin oluşturacağız [bu yönergeleri](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) sonraki birkaç adımda, ancak belirli bir örneği kullanın.

Sayfanın alt kısmındaki tıklatın **+ ADD USER**. Görüntülenen sayfasında yeni bir kullanıcı adı yazın ve olun **kullanıcı türü** bir **kuruluşunuzdaki yeni kullanıcı**. Bu örnekte, yeni kullanıcı adıdır `ahmet`. Bulunan varsayılan etki alanı daha önce etki alanı için ahmet kişinin e-posta adresi olarak seçin. Bittiğinde İleri okuna tıklayın.

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

Daha fazla ayrıntı için Ahmet ekleyin, ancak uygun seçtiğinizden emin olun **ROL** değeri. Kullanımı kolay **genel yönetici** emin şeyler yapmaya çalışır, ancak daha düşük bir rolü kullanabilirsiniz, bu iyi bir fikirdir. Bu örnekte **kullanıcı** rol. (Hakkında daha fazla bilgi [yönetici izinleri rolüne göre](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Her oturum açma işlemi için çok faktörlü kimlik doğrulamasını kullanmak istemediğiniz sürece çok faktörlü kimlik doğrulamasını etkinleştirmeyin. İşiniz bittiğinde İleri okuna tıklayın.

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

Tıklatın **oluşturma** oluşturmak ve geçici bir parola için Ahmet görüntülemek için düğmesi.

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

Kullanıcı adı e-posta adresi kopyalamak veya kullanmak **parola IN e-posta Gönder**. Kısa süre içinde oturum açmak için bilgileri gerekir.

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

Artık yeni kullanıcı görmelisiniz **Ahmet Geliştirici**, Azure Active Directory'den kaynaklı. Azure Active Directory ile yeni iş veya Okul kimlik oluşturduğunuzu düşünün. Ancak, bu kimlik henüz Azure kaynaklarını kullanmak için izinlere sahip değil.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

Kullanırsanız **parola IN e-posta Gönder**, aşağıdaki tür bir e-posta gönderilir.

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a>Abonelikler için Azure ortak yönetici hakları ekleme
Şimdi yeni kullanıcı Yönetim Portalı'na oturum açabilmeniz için yeni kullanıcı aboneliğinizin ortak yönetici eklemeniz gerekir. Bunu yapmak için sol panelinde tıklatın **ayarları**.

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

Ana Ayarlar bölümünde **Yöneticiler** üst ve, yalnızca kişisel Microsoft hesabı kimliğinizi görmeniz gerekir. Sayfanın alt kısmındaki tıklatın **+ Ekle** bir ortak yönetici belirtmek için. Burada, varsayılan etki alanı dahil olmak üzere, oluşturmuştunuz yeni kullanıcının e-posta adresi girin. Sonraki ekran görüntüsünde gösterildiği gibi kullanıcı varsayılan dizini için yanında yeşil bir onay işareti görünür. Tüm yönetmek bu kullanıcı istediğiniz abonelikleri seçin unutmayın.

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

İşiniz bittiğinde, yeni bir ortak yönetici kimlik bilgilerinizi dahil olmak üzere iki kullanıcıları artık görmelisiniz. Dışında portalında oturum açın.

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-the-new-users-password"></a>Oturum açmayı ve yeni kullanıcının parolasını değiştirme
Oluşturduğunuz yeni kullanıcı olarak oturum açın.

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

Hemen yeni bir parola oluşturmanız istenir.

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

Aşağıdaki gibi görünür başarı ile ödülünü.

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a>Sonraki adımlar
Kullanmak için yeni bir Azure Active Directory kimlik bilgilerinizi şimdi kullanabilirsiniz [Azure kaynak grubu şablonları](../articles/xplat-cli-azure-resource-manager.md).

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
