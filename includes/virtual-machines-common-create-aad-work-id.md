
<br>

> [!NOTE]
> Bir yönetici tarafından bir kullanıcı adı ve parola verildi, zaten bir iş veya Okul kimlik şansı yoktur (bazen adlı bir *Kuruluş Kimliği*). Bu durumda, Azure hesabı tooaccess bir gerektiren Azure kaynaklarını toouse hemen başlayabilirsiniz. Bu kaynakları kullanamazsınız bulursanız, Yardım için tooreturn toothis makale gerekebilir. Daha fazla bilgi için bkz: [için kullanabileceğiniz hesaplar oturum](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) ve [nasıl bir Azure aboneliği olan ilgili tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).
> 
> 

Merhaba adımlar basittir. Toolocate, imzalı ihtiyacınız hello Klasik Azure portalı kimliğinde, varsayılan Azure Active Directory etki alanınızın bulmak ve yeni bir kullanıcı tooit Azure ortak yönetici olarak ekleyin.

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a>Varsayılan dizini hello Klasik Azure portalı bulun
Başlat toohello içinde oturum açarak [Klasik Azure portalı](https://manage.windowsazure.com) kişisel Microsoft hesabı kimliğinizi ile. Günlüğe kaydedildikten sonra hello mavi hello yan sol panelde aşağı kaydırın ve tıklayın **ACTIVE DIRECTORY**.

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

Azure'da kimlik bilgilerinizi hakkında bazı bilgiler bularak başlayalım. Merhaba ana bölmede aşağıdaki, bir varsayılan dizin olduğunu gösteren hello gibi bir şey görmeniz gerekir.

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

Daha fazla bilgi bazı şimdi öğrenin. Merhaba varsayılan dizin özelliklerini getirir hello varsayılan dizin satıra tıklayın.  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

tooview hello varsayılan etki alanı adını tıklatın **etki alanları**.

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

Burada hello Azure hesabı oluşturulduğunda, Azure Active Directory karma değeri (metin dizesinden oluşturulan bir sayı) kişisel varsayılan bir etki alanı oluşturduğunuz mümkün toosee olmalıdır bir alt etki onmicrosoft.com kullanılan, kişisel kimliği. Şimdi yeni bir kullanıcı ekleyeceksiniz hello etki alanı toowhich olmasıdır.

## <a name="creating-a-new-user-in-hello-default-domain"></a>Merhaba varsayılan etki alanında yeni bir kullanıcı oluşturma
Tıklatın **kullanıcılar** ve tek kişisel hesabınız için bakın. Hello görmelisiniz **kaynağı** bu sütun bir **Microsoft hesabı**. Kullanıcı varsayılan olarak toocreate istiyoruz. onmicrosoft.com Azure Active Directory etki alanı.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

Toofollow yapacağız [bu yönergeleri](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) , sonraki birkaç adımda Merhaba, ancak belirli bir örneği kullanın.

Merhaba sayfasının Hello altında tıklatın **+ ADD USER**. Görüntülenen hello sayfasında hello yeni bir kullanıcı adı yazın ve hello olun **kullanıcı türü** bir **kuruluşunuzdaki yeni kullanıcı**. Bu örnekte, hello yeni bir kullanıcı adı olan `ahmet`. Bulunan hello varsayılan etki alanı, daha önce ahmet kişinin e-posta adresi için hello etki alanı olarak seçin. Tamamlandığında hello İleri okuna tıklayın.

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

Daha fazla ayrıntı için Ahmet ekleyin, ama emin tooselect hello uygun hale **ROL** değeri. Kolay toouse olan **genel yönetici** toomake emin şeyler çalışıyor, ancak daha düşük bir rolü kullanabilirsiniz, iyi bir fikirdir. Bu örnek hello kullanır **kullanıcı** rol. (Hakkında daha fazla bilgi [yönetici izinleri rolüne göre](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Her oturum açma işlemi için çok faktörlü kimlik doğrulama toouse istemediğiniz sürece çok faktörlü kimlik doğrulamasını etkinleştirmeyin. İşiniz bittiğinde hello İleri okuna tıklayın.

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

Hello tıklatın **oluşturmak** düğmesini toogenerate ve geçici bir parola için Ahmet görüntüler.

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

Merhaba kullanıcı adı e-posta adresi kopyalamak veya kullanmak **parola IN e-posta Gönder**. Merhaba bilgi toolog üzerinde kısa bir süre sonra ihtiyacınız olacaktır.

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

Artık hello yeni kullanıcı görmelisiniz **Ahmet hello Geliştirici**, Azure Active Directory'den kaynaklı. Azure Active Directory ile Merhaba yeni iş veya Okul kimlik oluşturduğunuzu düşünün. Ancak, bu kimliği henüz izinleri toouse Azure sahip kaynaklar.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

Kullanırsanız **parola IN e-posta Gönder**, e-posta türünü aşağıdaki hello gönderilir.

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a>Abonelikler için Azure ortak yönetici hakları ekleme
Şimdi Hello yeni kullanıcı toohello Yönetim Portalı oturum için bir ortak, aboneliğinizi yönetici tooadd hello yeni kullanıcı gerekir. Bu, hello sol panelinde tıklatın toodo **ayarları**.

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

Merhaba Ana Ayarlar bölümünde **Yöneticiler** hello üst ve yalnızca kişisel Microsoft hesabı kimliğinizi görmeniz gerekir. Merhaba sayfasının Hello altında tıklatın **+ Ekle** toospecify bir ortak yönetici. Burada, varsayılan etki alanı dahil olmak üzere, oluşturmuştunuz hello yeni kullanıcı hello e-posta adresini girin. Hello sonraki ekran görüntüsünde gösterildiği gibi sonraki toohello kullanıcı hello varsayılan dizin için yeşil bir onay işareti görünür. Tooselect unutmayın tüm hello abonelikleri bu kullanıcı toobe mümkün tooadminister istersiniz.

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

İşiniz bittiğinde, yeni bir ortak yönetici kimlik bilgilerinizi dahil olmak üzere iki kullanıcıları artık görmelisiniz. Dışında Hello portalında oturum açın.

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a>Oturum açmayı ve hello yeni kullanıcının parolasını değiştirme
Oluşturduğunuz hello yeni bir kullanıcı olarak oturum açın.

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

Yeni bir parola istendiğinde toocreate hemen olacaktır.

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

Merhaba şuna benzeyen başarı ile ödülünü.

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a>Sonraki adımlar
Artık, yeni Azure Active Directory kimlik toouse kullanabilirsiniz [Azure kaynak grubu şablonları](../articles/xplat-cli-azure-resource-manager.md).

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
