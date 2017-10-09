## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a>Nasıl toocreate bir ağ yapılandırması kullanılarak sanal bir ağ dosya Powershell'den
Azure bir xml dosyası toodefine tüm sanal ağların kullanılabilir tooa abonelik kullanır. Bu dosya indirme, toomodify düzenleyin veya varolan sanal ağları silin ve yeni sanal ağlar oluşturun. Bu öğreticide, bu dosyayı nasıl toodownload başvurulan öğrenin tooas ağ yapılandırması (veya netcfg) dosyası ve toocreate yeni bir sanal ağ düzenleyin. toolearn hello ağ yapılandırma dosyası hakkında daha fazla bilgi görmek hello [Azure virtual network yapılandırma şeması](https://msdn.microsoft.com/library/azure/jj157100.aspx).

toocreate PowerShell, tam hello aşağıdaki adımları kullanarak bir netcfg dosyasını sahip bir sanal ağ:

1. Azure PowerShell'i hiç kullanmadıysanız, tam hello hello adımları [nasıl tooInstall ve yapılandırma Azure PowerShell](/powershell/azureps-cmdlets-docs) makalesi, ardından tooAzure oturum açın ve aboneliğinizi seçin.
2. Merhaba Hello Azure PowerShell konsolundan kullanmak **Get-AzureVnetConfig** cmdlet toodownload hello ağ yapılandırma dosyası tooa dizini hello aşağıdaki komutu çalıştırarak, bilgisayarınızdaki: 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   Beklenen çıktı:
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. Herhangi bir XML veya metin düzenleyicisi uygulama kullanarak 2. adımda kaydettiğiniz hello dosyasını açın ve Merhaba arayın  **<VirtualNetworkSites>**  öğesi. Önceden oluşturulmuş tüm ağlarınız varsa, her ağ kendi olarak görüntülenen  **<VirtualNetworkSite>**  öğesi.
4. Bu senaryoda açıklanan toocreate hello sanal ağ ekleme XML yalnızca hello altında aşağıdaki hello  **<VirtualNetworkSites>**  öğe:

   ```xml
        <VirtualNetworkSite name="TestVNet" Location="East US">
          <AddressSpace>
            <AddressPrefix>192.168.0.0/16</AddressPrefix>
          </AddressSpace>
          <Subnets>
            <Subnet name="FrontEnd">
              <AddressPrefix>192.168.1.0/24</AddressPrefix>
            </Subnet>
            <Subnet name="BackEnd">
              <AddressPrefix>192.168.2.0/24</AddressPrefix>
            </Subnet>
          </Subnets>
        </VirtualNetworkSite>
   ```
   
5. Merhaba ağ yapılandırma dosyasını kaydedin.
6. Merhaba Hello Azure PowerShell konsolundan kullanmak **kümesi AzureVnetConfig** hello aşağıdaki komutu çalıştırarak cmdlet tooupload hello ağ yapılandırma dosyası: 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   Çıkış döndürdü:
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   Varsa **OperationStatus** değil *başarılı* hello çıkış döndürülen hatalar ve tam adım 6 için hello xml dosyasını yeniden denetleyin.

7. Merhaba Hello Azure PowerShell konsolundan kullanmak **Get-AzureVnetSite** yeni ağ hello cmdlet tooverify hello aşağıdaki komutu çalıştırarak eklenmiştir: 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   Merhaba (kısaltılmış) çıkış metnini izleyen hello döndürüldü:
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
