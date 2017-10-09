Merhaba AzureRm.Resources modülü 3.0 sürümü etiketleriyle nasıl çalıştığını önemli değişiklikler dahil. Devam etmeden önce sürümünüzü kontrol edin:

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

Sonuçlarınızı sürüm 3.0 veya üstü gösteriyorsa, bu konudaki hello örnekleri ortamınız ile çalışır. 3.0 veya sonraki sürüme sahip değilseniz, bu konu başlığına devam etmeden önce PowerShell Galerisi veya Web Platform Yükleyicisi’ni kullanarak [sürümünüzü güncelleştirin](/powershell/azureps-cmdlets-docs/).

```powershell
Version
-------
3.5.0
```

toosee hello için varolan etiketleri bir *kaynak grubu*, kullanın:

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

Bu komut dosyası biçimini izleyen hello döndürür:

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

toosee hello için varolan etiketleri bir *belirtilen kaynak Kimliğine sahip kaynak*, kullanın:

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

Ya da toosee hello için varolan etiketleri bir *belirtilen ad ve kaynak grubuna sahip kaynak*, kullanın:

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

tooget *belirli bir etikete sahip kaynak gruplarını*, kullanın:

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

tooget *, belirli bir etikete sahip kaynaklar*, kullanın:

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

Etiketler tooa kaynağa veya bir kaynak grubuna uygulamak her zaman, o kaynak veya kaynak grubu hello varolan etiketleri üzerine yazın. Bu nedenle, olup hello kaynağı veya kaynak grubunu varolan etiketleri temel alarak farklı bir yaklaşım kullanmanız gerekir. 

tooadd etiketler tooa *kaynak grubu mevcut etiketleri olmadan*, kullanın:

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

tooadd etiketler tooa *varolan etiketleri olan kaynak grubuna*hello varolan etiketleri almak, hello yeni etiket eklemek ve hello etiketler yeniden uygulayın:

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

tooadd etiketler tooa *varolan etiketleri olmadan kaynak*, kullanın:

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

tooadd etiketler tooa *varolan etiketleri olan kaynağın*, kullanın:

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

tooapply tüm etiketleri bir kaynak grubu tooits kaynakları ve *hello kaynaklardaki varolan etiketleri korumuyor*, komut dosyası izleyen hello kullanın:

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

tooapply tüm etiketleri bir kaynak grubu tooits kaynakları ve *tekrarı olmayan kaynaklar varolan etiketleri korumak*, komut dosyası izleyen hello kullanın:

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    if ($g.Tags -ne $null) {
        $resources = Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName 
        foreach ($r in $resources)
        {
            $resourcetags = (Get-AzureRmResource -ResourceId $r.ResourceId).Tags
            foreach ($key in $g.Tags.Keys)
            {
                if ($resourcetags.ContainsKey($key)) { $resourcetags.Remove($key) }
            }
            $resourcetags += $g.Tags
            Set-AzureRmResource -Tag $resourcetags -ResourceId $r.ResourceId -Force
        }
    }
}
```

Tüm etiketleri tooremove boş karma tablosu geçirin:

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



