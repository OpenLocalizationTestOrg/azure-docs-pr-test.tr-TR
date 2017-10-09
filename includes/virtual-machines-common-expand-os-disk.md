## <a name="overview"></a>Genel Bakış
Oluşturduğunuzda, yeni bir sanal makine (VM) bir kaynak grubunda bir görüntüden dağıtarak [Azure Marketi](https://azure.microsoft.com/marketplace/), hello varsayılan işletim sistemi sürücüsü olan 127 GB. Olası tooadd veri diskleri toohello (kaç bağlı olarak SKU hello sırasında seçtiğiniz) VM, ayrıca önerilen tooinstall uygulamaları ve CPU yoğun iş yükleri bu eki disklerdeki ise rağmen müşterilerin tooexpand hello OS görmemeleri gerekir aşağıdaki gibi belirli senaryolar toosupport sürücü:

1. İşletim sistemi sürücüsüne bileşen yükleyen eski uygulamaları destekleme.
2. Fiziksel bir bilgisayarı veya sanal makineyi daha büyük bir işletim sistemi sürücüsüne sahip şirket içi kaynaktan geçirme.

> [!IMPORTANT]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır: Resource Manager ve Klasik. Bu makalede, hello Resource Manager modelini kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.
> 
> 

## <a name="resize-hello-os-drive"></a>Merhaba işletim sistemi sürücüsü yeniden boyutlandırma
Bu makalede biz hello işletim sistemi sürücüsü resource manager modüllerini kullanarak yeniden boyutlandırma, hello görevi [Azure Powershell](/powershell/azureps-cmdlets-docs). Yönetici modunda Powershell ISE veya Powershell penceresi açın ve aşağıdaki hello adımları izleyin:

1. Oturum açma tooyour Microsoft Azure kaynak yönetimi modunda hesabınızı ve aboneliğinizi aşağıdaki gibi seçin:
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. Aşağıdakileri yaparak kaynak grubunuzun adını ve VM adını ayarlayın:
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. Başvuru tooyour VM aşağıdaki gibi alın:
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. Merhaba VM hello disk aşağıdaki gibi yeniden boyutlandırma önce durdurun:
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. Ve biz beklediğinden hello şu anda İşte! Merhaba işletim sistemi disk istenen toohello değeri Hello boyutunu ayarlayın ve hello VM şu şekilde güncelleştirin:
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > Merhaba yeni boyutu hello mevcut disk boyutundan daha büyük olmalıdır. Merhaba izin verilen en fazla 1023 GB'tır.
   > 
   > 
6. Güncelleştirme hello VM birkaç saniye sürebilir. Hello VM Hello komutu yürütme tamamlandıktan sonra aşağıdaki gibi yeniden başlatın:
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

Hepsi bu! Şimdi hello VM RDP'ye Bilgisayar Yönetimi (veya Disk Yönetimi) açın ve yeni ayrılmış alanı hello kullanarak hello sürücüyü genişletin.

## <a name="summary"></a>Özet
Bu makalede, Azure Resource Manager modüllerini Powershell tooexpand hello bir Iaas sanal makinenin işletim sistemi sürücüsü kullandık. Aşağıda çoğaltılamaz hello daha sonra başvurmak üzere tam komut dosyası vardır:

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a>Sonraki Adımlar
Bu makalede, biz öncelikle hello VM hello işletim sistemi diski genişletme üzerinde odaklanmış olsa hello geliştirilmiş komut dosyası ayrıca tek satırlık bir kod değiştirerek hello veri diskleri ekli toohello VM genişletmek için kullanılabilir. Örneğin, tooexpand hello ilk veri diski ekli toohello VM, hello yerine ```OSDisk``` nesnesinin ```StorageProfile``` ile ```DataDisks``` dizi ve sayısal dizin tooobtain bir başvuru toofirst ekli veri diski aşağıda gösterildiği gibi kullanın:

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
Benzer şekilde, diğer veri diskleri ekli toohello VM, yukarıda gösterildiği gibi bir dizin kullanarak ya da başvuru veya hello ```Name``` aşağıda gösterildiği gibi hello disk özelliği:

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

Nasıl tooattach tooan Azure Resource Manager VM diskleri çıkışı toofind istiyorsanız, bunu işaretleyin [makale](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

