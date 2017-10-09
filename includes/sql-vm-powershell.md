
## <a name="start-your-powershell-session"></a>PowerShell oturumunuzu başlatma
İlk toohave hello son gereksinim [Azure PowerShell](http://msdn.microsoft.com/library/mt619274.aspx) yüklü ve çalışır. Ayrıntılı bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azureps-cmdlets-docs).

> [!NOTE]
> Merhaba bu konuda kullanılan örnekler [Azure Resource Manager dağıtım modeli](../articles/azure-resource-manager/resource-group-overview.md), hello örneklerde [Azure Resource Manager cmdlet'lerini](http://msdn.microsoft.com/library/azure/mt125356.aspx). 
> 
> 

Merhaba çalıştırmak [ **Add-AzureRmAccount** ](http://msdn.microsoft.com/library/mt619267.aspx) cmdlet'ini sunulabilir bir oturum açma ekranı tooenter ile kimlik bilgilerinizi. Kullanım hello aynı kimlik bilgilerini toosign toohello Azure portalını kullanın.

    Add-AzureRmAccount

Birden çok aboneliğiniz varsa hello kullanın [ **Set-AzureRmContext** ](http://msdn.microsoft.com/library/mt619263.aspx) cmdlet tooselect PowerShell oturumunuzun hangi aboneliği kullanın. hangi aboneliğe hello oturumu kullanarak, geçerli PowerShell toosee çalıştırmak [ **Get-AzureRmContext**](http://msdn.microsoft.com/library/mt619265.aspx). Tüm aboneliklerinizi, toosee çalıştırmak [ **Get-AzureRmSubscription**](http://msdn.microsoft.com/library/mt619284.aspx).

    Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'

