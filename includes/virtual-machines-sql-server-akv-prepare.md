## <a name="prepare-for-akv-integration"></a>AKV tümleştirme için hazırlama
toouse Azure anahtar kasası tümleştirmeyi tooconfigure SQL Server VM'nize birkaç önkoşul vardır: 

1. [Azure PowerShell'i yükleme](#install-azure-powershell)
2. [Bir Azure Active Directory oluşturun](#create-an-azure-active-directory)
3. [Bir anahtar kasası oluşturma](#create-a-key-vault)

Merhaba aşağıdaki bölümlerde bu Önkoşullar ve toocollect çalıştırmak toolater hello PowerShell cmdlet'leri gereksinim hello bilgileri açıklanmaktadır.

### <a name="install-azure-powershell"></a>Azure PowerShell'i yükleme
Yüklediğinizden emin olun en son Azure PowerShell SDK hello. Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azureps-cmdlets-docs).

### <a name="create-an-azure-active-directory"></a>Bir Azure Active Directory oluşturun
Toohave gereken ilk olarak, bir [Azure Active Directory](https://azure.microsoft.com/trial/get-started-active-directory/) (AAD) aboneliğinizde. Birçok avantaj arasında bu, belirli kullanıcılar ve uygulamalar için toogrant izni tooyour anahtar kasasını sağlar.

Ardından, bir uygulamanın AAD ile kaydedin. Bu, VM ihtiyaç duyacağı erişim tooyour anahtar kasası olan bir hizmet sorumlusu hesabı verir. Hello Azure anahtar kasası makalede hello adımları bulabilirsiniz [bir uygulamayı Azure Active Directory ile kaydetme](../articles/key-vault/key-vault-get-started.md#register) bölüm veya hello ekran görüntüleri ile Merhaba adımları görebilirsiniz **hello uygulama için bir kimlik alma bölüm** , [bu blog gönderisine](http://blogs.technet.com/b/kv/archive/2015/01/09/azure-key-vault-step-by-step.aspx). Bu adımları gerçekleştirmeden önce aşağıdaki bilgilerle SQL VM üzerinde Azure anahtar kasası tümleştirmeyi etkinleştirdiğinizde, daha sonra gerekli bu kayıt sırasında toocollect hello gerektiğini unutmayın.

* Merhaba uygulaması eklendikten sonra hello bulur **istemci kimliği** hello üzerinde **yapılandırma** sekmesi.   ![Azure Active Directory istemci kimliği](./media/virtual-machines-sql-server-akv-prepare/aad-client-id.png)
  
    Merhaba istemci kimliği, daha sonra toohello atandığı **$spName** hello PowerShell komut dosyası tooenable Azure anahtar kasası tümleştirmeyi parametresinde (hizmet asıl adı). 
* Ayrıca, anahtarınızı oluşturduğunuzda, bu adımları sırasında hello gizli anahtarınız için hello ekran aşağıdaki gösterildiği gibi kopyalayın. Bu anahtar sırrı sonraki toohello atanan **$spSecret** hello PowerShell Betiği parametresinde (hizmet sorumlusu gizli).  
    ![Azure Active Directory parolası](./media/virtual-machines-sql-server-akv-prepare/aad-sp-secret.png)
* Aşağıdaki erişim izinleri bu yeni istemci kimliği toohave hello yetkilendirmeniz gerekir: **şifrelemek**, **şifresini**, **wrapKey**, **unwrapKey**, **oturum**, ve **doğrulayın**. Bu hello ile yapılır [kümesi AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/azure/mt603625.aspx) cmdlet'i. Daha fazla bilgi için bkz: [Authorize hello uygulama toouse hello anahtar veya gizli](../articles/key-vault/key-vault-get-started.md#authorize).

### <a name="create-a-key-vault"></a>Bir anahtar kasası oluşturma
VM ile şifreleme için kullanacağınız sipariş toouse Azure anahtar kasası toostore hello anahtarlarında erişim tooa anahtar kasası gerekir. Anahtar kasanız zaten ayarlamadıysanız hello hello adımları izleyerek oluşturun [Azure anahtar kasası ile çalışmaya başlama](../articles/key-vault/key-vault-get-started.md) konu. Bu adımları gerçekleştirmeden önce SQL VM üzerinde Azure anahtar kasası tümleştirmeyi etkinleştirdiğinizde, bu kurulum sırasında toocollect gereken bazı bilgiler daha sonra gerekli olduğuna dikkat edin.

Aldığınız toohello oluşturduğunuzda bir anahtar kasası adımı Not hello döndürülen **vaultUri** hello anahtar kasası URL'si özelliği. Bu adımda, aşağıda gösterilen sağlanan hello örnekte hello anahtar kasası adı ContosoKeyVault, bu nedenle hello anahtar kasası URL'si https://contosokeyvault.vault.azure.net/ olacaktır.

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

Merhaba anahtar kasası URL'si sonraki toohello atanan **$akvURL** hello PowerShell komut dosyası tooenable Azure anahtar kasası tümleştirmeyi parametresi.

