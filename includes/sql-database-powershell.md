
## <a name="start-your-powershell-session"></a>PowerShell oturumunuzu başlatma
İlk olarak, size sahip hello yüklü ve çalışan en son Azure PowerShell. Ayrıntılı bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azureps-cmdlets-docs).

> [!NOTE]
> Merhaba kullanılırken SQL veritabanı'nın birçok yeni özellik yalnızca desteklenen [Azure Resource Manager dağıtım modeli](../articles/azure-resource-manager/resource-group-overview.md), hello örneklerde [Azure SQL Database PowerShell cmdlet'leri](https://msdn.microsoft.com/library/azure/mt574084\(v=azure.300\).aspx) kaynak yöneticisi için . Merhaba Hizmet Yönetimi (Klasik) dağıtım modeli [Azure SQL Veritabanı Hizmet Yönetimi cmdlet'leri](https://msdn.microsoft.com/library/azure/dn546723\(v=azure.300\).aspx) geriye dönük uyumluluk için desteklenir, ancak hello Resource Manager cmdlet'lerini kullanmanızı öneririz.
> 
> 

Merhaba çalıştırmak [ **Add-AzureRmAccount** ](https://msdn.microsoft.com/library/azure/mt619267\(v=azure.300\).aspx) cmdlet'i ve sunulabilir ile oturum açma ekranında tooenter kimlik bilgilerinizi. Kullanım hello aynı kimlik bilgilerini toosign toohello Azure portalını kullanın.

```PowerShell
Add-AzureRmAccount
```

Birden çok aboneliğiniz varsa, hello kullan [ **Set-AzureRmContext** ](https://msdn.microsoft.com/library/azure/mt619263\(v=azure.300\).aspx) cmdlet tooselect PowerShell oturumunuzun hangi aboneliği kullanın. hangi aboneliğe hello oturumu kullanarak, geçerli PowerShell toosee çalıştırmak [ **Get-AzureRmContext**](https://msdn.microsoft.com/library/azure/mt619265\(v=azure.300\).aspx). Tüm aboneliklerinizi, toosee çalıştırmak [ **Get-AzureRmSubscription**](https://msdn.microsoft.com/library/azure/mt619284\(v=azure.300\).aspx).

```PowerShell
Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'
```
