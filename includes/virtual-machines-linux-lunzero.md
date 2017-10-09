Bir diski LUN 0 mevcut değilse veri diskleri tooa Linux VM eklerken hatalarla karşılaşabilirsiniz. Hello kullanarak el ile bir disk ekliyorsanız `azure vm disk attach-new` komutu ve belirtirseniz bir LUN (`--lun`) hello izin vermek yerine, Azure platformu toodetermine uygun LUN Merhaba, dikkatli olun bir disk zaten var. / LUN 0 yer alır. 

Merhaba çıktısını parçacığıyla gösteren örnek aşağıdaki hello göz önünde bulundurun `lsscsi`:

```bash
[5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc 
[5:0:0:1]    disk    Msft     Virtual Disk     1.0   /dev/sdd 
```

Merhaba iki veri diski LUN 0 ve LUN 1 mevcut (Merhaba ilk sütunda hello `lsscsi` çıkış ayrıntıları `[host:channel:target:lun]`). Her iki diskin hello VM içinden gelen accessbile olmalıdır. El ile Merhaba LUN 1 ve ikinci bir disk hello LUN 2 konumundaki eklenen ilk disk toobe belirttiyseniz, hello disklerden doğru VM içinden göremeyebilirsiniz.

> [!NOTE]
> Hello Azure `host` değer 5 Bu örneklerde, ancak bu seçtiğiniz depolama hello türüne bağlı olarak değişebilir.
> 
> 

Bu disk davranış Azure sorun ancak hello Linux çekirdek hello SCSI belirtimleri izleyen hello yolu değil. Merhaba Linux çekirdek hello SCSI veri yoluna bağlı aygıtları için tarama yaptığında bir aygıtı LUN değerine 0 ek cihazlar için tarama hello sistem toocontinue sırada bulunması gerekir. Bu nedenle:

* Merhaba çıkışını gözden `lsscsi` bir diski LUN 0 olması bir veri diski tooverify ekledikten sonra.
* Diskinizin doğru VM içinden gösterilmez, bir diski LUN 0 mevcut doğrulayın.

