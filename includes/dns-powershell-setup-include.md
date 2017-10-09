## <a name="set-up-azure-powershell-for-azure-dns"></a>Azure DNS için Azure PowerShell ayarlayın

### <a name="before-you-begin"></a>Başlamadan önce

Yapılandırmanıza başlamadan önce aşağıdaki öğelerindeki hello sahip olduğunuzu doğrulayın.

* Azure aboneliği. Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.
* Tooinstall hello en son sürümünü hello Azure Resource Manager PowerShell cmdlet'lerini gerekir. Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azureps-cmdlets-docs).

### <a name="sign-in-tooyour-azure-account"></a>Azure hesabı tooyour içinde oturum

PowerShell Konsolunuzu açın ve tooyour hesap bağlanın. Daha fazla bilgi için bkz: [PowerShell kullanarak Resource Manager ile](../articles/azure-resource-manager/powershell-azure-resource-manager.md).

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a>Merhaba aboneliği seçin
 
Merhaba hesabının Hello abonelikleri kontrol edin.

```powershell
Get-AzureRmSubscription
```

Azure abonelikleri toouse hangisinin seçin.

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir. Bu konum, kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır. Ancak, tüm DNS kaynakları global olduğundan, bölgesel değil, kaynak grubu konumu hello seçimine Azure DNS üzerinde hiçbir etkisi olmaz.

Var olan bir kaynak grubunu kullanıyorsanız bu adımı atlayabilirsiniz.

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a>Kaynak sağlayıcısını kaydetme

Hello Azure DNS hizmeti hello Microsoft.Network kaynak sağlayıcısı tarafından yönetilir. Azure aboneliğinizde Azure DNS'yi kullanmadan önce bu kaynak sağlayıcısı kayıtlı toouse olmalıdır. Bu, her bir abonelik için tek seferlik bir işlemdir.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```