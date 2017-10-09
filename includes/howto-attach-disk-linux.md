
Diskler hakkında daha fazla bilgi için bkz. [Sanal Makineler için Diskler ve VHD’ler hakkında](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a>Boş disk ekleme
1. Azure CLI 1.0 açın ve [tooyour Azure aboneliğine bağlanma](../articles/xplat-cli-connect.md). Azure Hizmet Yönetimi modunda olduğunuzdan emin olun (`azure config mode asm`).
2. Girin `azure vm disk attach-new` toocreate ve hello aşağıdaki örnekte gösterildiği gibi yeni bir disk ekleyin. Değiştir *myVM* , Linux sanal makineniz hello adla ve hello hello diskin boyutunu olan GB cinsinden belirtin *100GB* Bu örnekte:

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. Merhaba veri diski oluşturduktan ve bağlı sonra hello çıkışında da listelenir `azure vm disk list <virtual-machine-name>` hello aşağıdaki örnekte gösterildiği gibi:
   
    ```azurecli
    azure vm disk list TestVM
    ```

    Merhaba, benzer toohello aşağıdaki örneğine çıktı:

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a>Var olan bir diski ekleme
Var olan bir diskin eklenmesi için depolama hesabında bir .vhd olmalıdır.

1. Azure CLI 1.0 açın ve [tooyour Azure aboneliğine bağlanma](../articles/xplat-cli-connect.md). Azure Hizmet Yönetimi modunda olduğunuzdan emin olun (`azure config mode asm`).
2. Merhaba tooattach zaten istediğiniz VHD tooyour Azure aboneliği karşıya olmadığını kontrol edin:
   
    ```azurecli
    azure vm disk list
    ```

    Merhaba, benzer toohello aşağıdaki örneğine çıktı:

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. Merhaba disk bulamazsanız toouse istediğiniz, kullanarak bir yerel VHD tooyour abonelik karşıya `azure vm disk create` veya `azure vm disk upload`. Bir örneği `disk create` aşağıdaki örneğine hello olduğu gibi olacaktır:
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    Merhaba, benzer toohello aşağıdaki örneğine çıktı:

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   De kullanabilirsiniz `azure vm disk upload` tooupload bir VHD tooa belirli bir depolama hesabı. Azure sanal makine veri diski hello hakkında daha fazla komutları toomanage okuma [burada üzerinden](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

4. Eklediğiniz artık hello VHD tooyour sanal makine istenen:
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   Emin tooreplace olun *myVM* sanal makinenizin hello adla ve *myVHD* istenen VHD ile.

5. Merhaba disktir ekli toohello sanal makineyle doğrulayabilirsiniz `azure vm disk list <virtual-machine-name>`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    Merhaba, benzer toohello aşağıdaki örneğine çıktı:

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> Bir veri diski ekledikten sonra toohello sanal makineye toolog gerekir ve hello sanal makine hello disk depolama için kullanabileceğiniz şekilde hello diskini başlatmak (aşağıdaki hello nasıl toodo başlatma üzerinde hello disk daha fazla bilgi için adımlarına bakın).
> 
> 

