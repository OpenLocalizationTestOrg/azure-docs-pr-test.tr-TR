

## <a name="multi-and-single-instance-vms"></a>Birden çok ve tek örnek VM'ler
Azure sayısına kritik planlı bakım nedeniyle toohello kapalı kalma süresi--Vm'leri geçmelerini zaman bunlar zamanlayabilirsiniz çalışan pek çok müşteriniz yaklaşık 15 dakika--bu bakım sırasında oluşur. Sağlanan VM'ler planlanmış bakım aldığınızda kullanılabilirlik kümeleri toohelp denetimi kullanabilirsiniz.

Azure üzerinde çalışan sanal makineler için iki olası yapılandırmaları vardır. Sanal makineleri ya da çok örnekli veya tek örnek yapılandırılır. Sanal makineleri bir kullanılabilirlik kümesine varsa, bunlar birden çok örneği olarak yapılandırılır. Unutmayın, hatta VM'ler tek bir kullanılabilirlik kümesinde birden çok örneği olarak kabul edilir böylece dağıtılabilir. Ardından sanal makineleri bir kullanılabilirlik kümesine emin değilseniz, tek örnek yapılandırılır.  Kullanılabilirlik kümeleri hakkında daha fazla bilgi için bkz: [Yönet hello kullanılabilirlik, Windows sanal makinelerinizi](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) veya [Yönet hello kullanılabilirlik, Linux sanal makineleri](../articles/virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Planlı bakım toosingle örneğini güncelleştirir ve çok örnekli sanal makineleri ayrı ayrı gerçekleşir. (Birden çok örneği olmaları durumunda), sanal makineleri toobe Tek Örnekli yeniden yapılandırmadan veya (tek örnek varsa) toobe çok örnekli tarafından Vm'leri hello planlı bakım aldığınızda kontrol edebilirsiniz. Bkz: [planlı bakım Azure Linux sanal makineleri için](../articles/virtual-machines/linux/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [planlı bakım Azure Windows sanal makineler için](../articles/virtual-machines/windows/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Azure VM'ler için planlı bakım hakkında ayrıntılı bilgi için.

## <a name="for-multi-instance-configuration"></a>Çok örnekli yapılandırması
Bir kullanılabilirlik kümesi yapılandırmasında kullanılabilirlik kümesinden bu Vm'lere kaldırarak dağıtılan Vm'leriniz planlı bakım etkiler hello zaman seçebilirsiniz.

1. Bir e-posta tooyou hello çok örnekli yapılandırmasında bakım tooyour VM'ler planlanmış önce yedi Takvim günleri gönderilir. Abonelik kimlikleri hello ve etkilenen hello çok örnekli VM adlarını hello hello e-posta gövdesinde dahil edilir.
2. Bu yedi gün boyunca örneklerinizi hello zamanını seçebilirler çok örnekli Vm'leriniz bu bölgede kendi kullanılabilirlik kümesinden kaldırarak güncelleştirilir. Bu değişikliği yeniden başlatma, bir fiziksel ana bilgisayarından hello sanal makine taşıma yapılandırma nedenleri, hedeflenen bakım, bakım için hedeflenen değil tooanother fiziksel ana bilgisayar.
3. Kendi kullanılabilirlik hello Azure portal kümesi hello VM kaldırabilirsiniz.

   1. Merhaba Portalı'nda hello VM tooremove hello kullanılabilirlik kümesi seçin.  

   2. Altında **ayarları**, tıklatın **kullanılabilirlik kümesi**.

      ![Kullanılabilirlik kümesi seçimi](./media/virtual-machines-planned-maintenance-schedule/availabilitysetselection.png)

   3. Açılır menüsünde Hello kullanılabilirlik kümesinde, "Bölümünü bir kullanılabilirlik kümesinin." seçin

      ![Kümesinden Kaldır](./media/virtual-machines-planned-maintenance-schedule/availabilitysetwarning.png)

   4. Merhaba üstünde tıklatın **kaydetmek**. Tıklatın **Evet** Bu eylem yeniden tooacknowledge hello VM.

   >[!TIP]
   >Listelenen hello kullanılabilirlik kümeleri birini seçerek hello VM toomulti örnek daha sonra yeniden yapılandırabilirsiniz.

4. Kullanılabilirlik kümesinden kaldırıldı VM'ler taşınan tooSingle örnek konak ve hello planlı bakım tooAvailability belirlenen yapılandırmalar sırasında güncelleştirilmez.
5. Merhaba güncelleştirme tooAvailability kümesi Vm'lerine tamamlandıktan sonra (Merhaba özgün e-posta ile ana hatlarıyla tooschedule göre), hello VM'ler geri kullanılabilirlik kümeleri halinde eklemeniz gerekir. Bir kullanılabilirlik kümesinin parçası olma hello VM'ler çok örneği olarak yeniden yapılandırır ve bir önyükleme sonuçlanır. Genellikle, tüm çok örnekli güncelleştirmeleri hello tüm Azure ortamı genelinde tamamlandığında, tek örnek bakım izler.

VM bir kullanılabilirlik kümesinden kaldırılması, ayrıca Azure PowerShell kullanarak yapabiliriz:

```
Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Remove-AzureAvailabilitySet | Update-AzureVM
```

## <a name="for-single-instance-configuration"></a>Tek örnek yapılandırması
Planlı bakım, sanal makineleri tek örnek yapılandırmada kullanılabilirlik kümeleri halinde bu Vm'lere ekleyerek etkiler hello zaman seçebilirsiniz.

Adım adım

1. Bir e-posta tooyou hello planlı bakım tooVMs tek örnek yapılandırmasında önce yedi Takvim günleri gönderilir. Abonelik kimlikleri hello ve etkilenen hello Tek Örnekli VM'ler adlarını hello hello e-posta gövdesinde dahil edilir.
2. Bu yedi gün boyunca örneğinizi hello zaman seçebilirsiniz, tek örnek VM'ler tooan kullanılabilirlik ekleyerek yeniden başlatmalar o aynı bölgede ayarlayın. Bu değişikliği yeniden başlatma, bir fiziksel ana bilgisayarından hello sanal makine taşıma yapılandırma nedenleri, hedeflenen bakım, bakım için hedeflenen değil tooanother fiziksel ana bilgisayar.
3. Yönergeleri izleyerek VM'ler hello Azure portalı ve Azure PowerShell kullanarak kullanılabilirlik kümeleri halinde varolan burada tooadd. (Bkz şu adımları izler hello Azure PowerShell örnek.)
4. Bu sanal makineleri çok örnekli olarak yapılandırılır sonra hello planlı bakım hariç tutulan tooSingle örneği VM'ler.
5. Merhaba Tek Örnekli VM güncelleştirmesi tamamlandıktan sonra (Merhaba özgün e-posta tooschedule göre), kendi kullanılabilirlik kümesinden hello VM'ler kaldırarak hello VM'ler toosingle örnek döndürebilir.

VM tooan ekleme kullanılabilirlik kümesi de Azure PowerShell kullanarak yapabiliriz:

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

<!--Anchors-->



<!--Link references-->
[Virtual Machines Manage Availability]: virtual-machines-windows-tutorial.md
[Understand planned versus unplanned maintenance]: virtual-machines-manage-availability.md#Understand-planned-versus-unplanned-maintenance/
