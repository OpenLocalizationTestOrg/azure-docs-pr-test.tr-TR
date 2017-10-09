## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a>Azure Resource Manager istekleri tooauthenticate hazırlama
Hello kullanarak kaynakları üzerinde gerçekleştirdiğiniz tüm hello işlemleri kimlik doğrulaması yapmalıdır [Azure Resource Manager] [ lnk-authenticate-arm] ile Azure Active Directory (AD). en kolay yolu tooconfigure hello toouse PowerShell veya Azure CLI budur.

Merhaba yüklemek [Azure PowerShell cmdlet'lerini] [ lnk-powershell-install] devam etmeden önce.

adımları Göster nasıl aşağıdaki hello tooset parola kimlik doğrulaması için PowerShell kullanarak bir AD uygulamasını ayarlama. Standart bir PowerShell oturumunda aşağıdaki komutları çalıştırabilirsiniz.

1. Tooyour içinde Azure aboneliği komutu aşağıdaki hello kullanarak oturum:

    ```powershell
    Login-AzureRmAccount
    ```

1. Birden çok Azure aboneliğiniz varsa tooAzure imzalama tooall erişim verir kimlik bilgilerinizle ilişkili Azure abonelik hello. Toouse toolist hello Azure abonelikleri kullanılabilir sizin için komutu aşağıdaki hello kullan:

    ```powershell
    Get-AzureRMSubscription
    ```

    IOT hub'ınızı toomanage toouse toorun hello komutları istediğiniz komut tooselect abonelik aşağıdaki hello kullanın. Merhaba hello önceki komutunun çıktısından hello abonelik adı veya kimliği kullanabilirsiniz:

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. Not, **Tenantıd** ve **Subscriptionıd**. Daha sonra gereksinim duyarsınız.
3. Aşağıdaki komut, hello yer tutucu değiştirme hello kullanarak yeni bir Azure Active Directory uygulaması oluşturun:
   
   * **{Görünen adı}:** gibi uygulamanız için bir görünen ad **MySampleApp**
   * **{Giriş sayfası URL'si}:** , uygulamanızın hello giriş sayfasının URL'sini gibi hello **http://mysampleapp/home**. Bu URL toopoint tooa gerçek uygulama gerekmez.
   * **{Uygulama tanımlayıcısı}:** gibi benzersiz bir tanımlayıcı **http://mysampleapp**. Bu URL toopoint tooa gerçek uygulama gerekmez.
   * **{Parola}:** tooauthenticate uygulamanızla kullandığınız parola.
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. Merhaba Not **ApplicationId** oluşturduğunuz hello uygulamasının. Bu daha sonra ihtiyacınız var.
5. Aşağıdaki komut, değiştirme hello kullanarak yeni bir hizmet sorumlusu oluşturma **{MyApplicationId}** hello ile **ApplicationId** hello önceki adımdaki:
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. Aşağıdaki komut, değiştirme hello kullanarak bir rol ataması ayarlamak **{MyApplicationId}** ile **ApplicationId**.
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

Şimdi, özel C# uygulamanızdan tooauthenticate sağlar hello Azure AD uygulaması oluşturma tamamladınız. Daha sonra Bu öğreticide değerleri aşağıdaki hello gerekir:

* Tenantıd
* SubscriptionId
* ApplicationId
* Parola

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
