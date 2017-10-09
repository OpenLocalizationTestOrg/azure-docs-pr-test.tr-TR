

VM uzantıları aşağıdakilerde size yardımcı olur:

* Hesap değerlerini sıfırlama ve kötü amaçlı yazılımdan koruma yazılımı kullanma gibi güvenlik ve kimlik özelliklerini değiştirmek
* İzleme ve tanılama başlatmak, durdurmak veya yapılandırmak
* RDP ve SSH gibi bağlantı özelliklerini sıfırlamak veya yüklemek
* VM’lerinizi tanılamak, izlemek ve yönetmek

Başka birçok özellik de vardır. Yeni VM Uzantısı özellikleri düzenli olarak kullanıma sunulur. Bu makalede için hello Azure VM Aracısı Windows ve Linux ve VM uzantısı işlevselliğini nasıl destekledikleri açıklanmaktadır. Özellik kategorisine göre VM Uzantılarının bir listesi için, bkz. [Azure VM Uzantıları ve Özellikleri](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="azure-vm-agents-for-windows-and-linux"></a>Windows ve Linux için Azure VM Aracıları
Hello Azure sanal makineleri Aracısı (VM Aracısı) yükler, yapılandırır ve VM uzantıları, Azure sanal makineleri örneklerinde kaldırır güvenli, hafif bir işlemdir. Hello VM Aracısı, Azure VM için hello güvenli yerel denetimi hizmeti olarak görev yapar. Aracı yükleri hello hello uzantıları belirli özellikler tooincrease üretkenliğinizi hello örneğini kullanarak sağlayın.

Biri Windows VM’leri için ve biri Linux VM’leri için olmak üzere iki adet Azure VM Aracısı vardır.

Bir veya daha fazla VM uzantıları bir sanal makine örneği toouse istiyorsanız hello örneği yüklü bir VM aracısı yüklü olmalıdır. Hello Azure portal ve hello görüntüden kullanılarak oluşturulan bir sanal makine görüntüsü **Market** VM Aracısı hello oluşturma işlemine otomatik olarak yükler. Bir sanal makine örneğini VM Aracısı eksikse, hello sanal makine örneği oluşturulduktan sonra hello VM Aracısı yükleyebilirsiniz. Ya da sonra karşıya özel VM görüntü hello aracısını yükleyebilirsiniz.

> [!IMPORTANT]
> Bu VM Aracıları, sanal makine örneklerinin güvenlikli yönetimini sağlayan çok hafif hizmetlerdir. Merhaba VM Aracısı istemediğiniz durumlarda olabilir. Gerekiyorsa, hello VM Aracısı'hello Azure CLI veya PowerShell kullanarak yüklü olmayan toocreate VM'ler emin olun. Merhaba VM Aracısı fiziksel olarak kaldırılabilir karşın, VM uzantıları hello davranışını hello örneği üzerinde tanımlı değil. Sonuç olarak, yüklü bir VM Aracısının kaldırılması desteklenmez.
>

Merhaba VM Aracısı durumlarda aşağıdaki hello etkinleştirilir:

* Azure portalı ve hello bir görüntüyü seçerek kullanarak bir VM örneği oluşturduğunuzda hello **Market**,
* Hello kullanarak bir VM örneği oluşturduğunuzda [New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx) veya hello [yeni AzureQuickVM](https://msdn.microsoft.com/library/azure/dn495183.aspx) cmdlet'i. VM VM Aracısı olmadan hello ekleyerek oluşturabilirsiniz **– DisableGuestAgent** parametresi toohello [Ekle AzureProvisioningConfig](https://msdn.microsoft.com/library/azure/dn495299.aspx) cmdlet'i

* Ne zaman, el ile indirme ve hello VM Aracısı mevcut VM örneği yükleme ve ayarlama hello **ProvisionGuestAgent** çok değer**doğru**. Bir PowerShell komutu veya bir REST çağrısı kullanarak Windows ve Linux aracıları için bu tekniği kullanabilirsiniz. (Merhaba ayarlamazsanız **ProvisionGuestAgent** el ile Merhaba VM Aracısı, VM aracısının düzgün algılanmadığında hello hello eklenmesi yükledikten sonra değer.) kod örnekteki nasıl aşağıdaki hello toodo bu hello burada PowerShell'i kullanma `$svc` ve `$name` bağımsız değişkenleri zaten belirlenir:

      $vm = Get-AzureVM –ServiceName $svc –Name $name
      $vm.VM.ProvisionGuestAgent = $TRUE
      Update-AzureVM –Name $name –VM $vm.VM –ServiceName $svc

* Yüklü bir VM Aracısını içeren bir VM görüntüsü oluşturduğunuzda. Merhaba VM Aracısı Hello görüntüsüyle mevcut olduğunda, görüntü tooAzure karşıya yükleyebilirsiniz. Bir Windows VM için hello karşıdan [Windows VM Aracısı .msi dosyası](http://go.microsoft.com/fwlink/?LinkID=394789) ve hello VM aracısı yükleyin. Bir Linux VM için VM Aracısı'ndan hello GitHub deposunu bulunan hello yüklemek <https://github.com/Azure/WALinuxAgent>. Merhaba nasıl tooinstall hello VM Aracısı'nı Linux üzerinde daha fazla bilgi için bkz: [Azure Linux VM Aracısı Kullanıcı Kılavuzu'na](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

> [!NOTE]
> PaaS içinde hello VM Aracısı adlandırılır **WindowsAzureGuestAgent**ve her zaman Web ve çalışan rolü, Vm'leri üzerinde kullanılabilir. (Daha fazla bilgi için bkz: [Azure rol mimarisi](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx).) hello rol VM'ler için VM Aracısı hello uzantıları toohello bulut hizmeti VM'ler şimdi ekleyebilirsiniz kalıcı sanal makineler için mevcut aynı şekilde. Merhaba VM uzantıları eklendiğinde hello büyük VM rolü'nde VM uzantıları kalıcı VMs arasındaki farktır. VM'ler daha fazla rol ile ilk toohello bulut hizmeti, sonra bu bulut hizmeti toohello dağıtımlarını uzantıları eklenir.
>
> Kullanım [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet toolist tüm kullanılabilir rol VM uzantıları.
>
>

## <a name="find-add-update-and-remove-vm-extensions"></a>VM Uzantıları Bulma, Ekleme, Güncelleştirme ve Kaldırma
Bu görevler hakkında daha fazla bilgi için, bkz: [Azure VM Uzantıları Ekleme, Bulma, Güncelleştirme ve Kaldırma](../articles/virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
