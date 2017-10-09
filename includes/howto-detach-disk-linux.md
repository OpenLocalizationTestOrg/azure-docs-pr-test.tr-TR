Ekli tooa sanal makine (VM) bir veri diski artık ihtiyacınız olduğunda, kolayca ayırabilirsiniz. Merhaba VM diskten ayırdığınızda hello disk değil depolama biriminden kaldırıldı. Merhaba disk üzerindeki toouse hello mevcut verileri yeniden istiyorsanız, toohello iliştirebilirsiniz aynı VM veya başka bir tane.  

> [!NOTE]
> Azure'da VM’ler işletim sistemi diski, yerel geçici disk ve isteğe bağlı veri diskleri gibi farklı tür diskler kullanır. Ayrıntılar için bkz. [Sanal Makinelerde Diskler ve VHD’ler Hakkında](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Ayrıca hello VM silmediğiniz sürece bir işletim sistemi diski ayıramazsınız.

## <a name="find-hello-disk"></a>Başlangıç diski bulun
Bir diskten VM ayırmadan önce hello hello disk toobe ayrılmış bir tanıtıcısıdır LUN numarası çıkışı toofind gerekir. Bu adımları, toodo:

1. Azure CLI'ni açın ve [tooyour Azure aboneliğine bağlanma](../articles/xplat-cli-connect.md). Azure Hizmet Yönetimi modunda olduğunuzdan emin olun (`azure config mode asm`).
2. Hangi disklerin ekli tooyour VM olduğunu bulabilirsiniz. Merhaba aşağıdaki örnek listeler hello adlı VM için diskleri `myVM`:

    ```azurecli
    azure vm disk list myVM
    ```

    Merhaba, benzer toohello aşağıdaki örneğine çıktı:

    ```azurecli
    * Fetching disk images
    * Getting virtual machines
    * Getting VM disks
      data:    Lun  Size(GB)  Blob-Name                         OS
      data:    ---  --------  --------------------------------  -----
      data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
      data:    0    30        myDataDisk.vhd
      info:    vm disk list command OK
    ```

3. Not hello LUN veya hello **mantıksal birim numarası** toodetach istediğiniz hello diski için.

## <a name="remove-operating-system-references-toohello-disk"></a>İşletim sistemi başvuruları toohello diski Kaldır
Merhaba Linux Konuk Hello diskten kullanımdan çıkarmadan önce hello diskteki tüm bölümlerin kullanımda olmadığından emin olmanız gerekir. Merhaba işletim sistemi tooremount denemez olun bir yeniden başlatma işleminden sonra onları. Büyük olasılıkla oluşturmuşsunuz ne zaman hello yapılandırma adımları geri [ekleme](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) hello disk.

1. Kullanım hello `lsscsi` komut toodiscover hello disk tanımlayıcısı. `lsscsi`, `yum install lsscsi` (Red Hat üzerinde dağıtımlarda) veya `apt-get install lsscsi` (Debian üzerinde dağıtımlarda) aracılığıyla yüklenebilir. Merhaba LUN numarası kullanarak aradığınız hello disk tanımlayıcısı bulabilirsiniz. Merhaba son hello tuple her satırda hello LUN sayısıdır. Örnekten aşağıdaki hello içinde `lsscsi`, LUN 0 eşlemeleri çok  */dev/sdc*

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. Kullanım `fdisk -l <disk>` toodiscover hello bölümleri ayrılmış hello disk toobe ile ilişkilendirilmiş. Merhaba aşağıdaki örnekte hello çıktısı için gösterilmektedir `/dev/sdc`:

    ```bash
    Disk /dev/sdc: 1098.4 GB, 1098437885952 bytes, 2145386496 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x5a1d2a1a
    
        Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1            2048  2145386495  1072692224   83  Linux
    ```

3. Merhaba disk için listelenen her bir bölümü çıkarın. Merhaba aşağıdaki örnek çıkarır `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

4. Kullanım hello `blkid` tüm bölümler için komut toodiscovery hello UUID. Merhaba, benzer toohello aşağıdaki örneğine çıktı:

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. Hello silmemelisiniz **/etc/fstab** ayrılmış hello disk toobe için tüm bölümler için hello aygıt yolları veya UUID'ler ile ilişkili dosya.  Bu örneğin girişleri şöyle olabilir:

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    or
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a>Merhaba disk ayırma
Merhaba LUN sayısını hello disk ve kaldırılan hello işletim sistemi başvuruları bulduktan sonra hazır toodetach olduğunuz bu:

1. Merhaba komutu çalıştırarak hello sanal makineden Hello seçili disk ayırma `azure vm disk detach
   <virtual-machine-name> <LUN>`. Merhaba aşağıdaki örnek ayırır LUN `0` hello adlı VM gelen `myVM`:
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. Merhaba disk çalıştırarak ayrıldı olmadığını denetleyebilirsiniz `azure vm disk list` yeniden. Aşağıdaki örnek denetimleri hello hello adlı VM `myVM`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    Merhaba, benzer toohello hello veri diski artık takılı gösteren örnek aşağıdaki çıktı:

    ```azurecli
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
     info:    vm disk list command OK
    ```

Merhaba ayrılmış disk depolama alanında kalır, ancak artık ekli tooa sanal makine değil.

