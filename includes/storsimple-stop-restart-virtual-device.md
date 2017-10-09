#### <a name="toostop-and-start-a-virtual-device"></a>toostop ve başlangıç sanal cihazı
toostop sanal cihaz adına tıklayın ve ardından **kapatma**. Merhaba sanal cihaz kapatıldığı sırada durumundadır **durdurma**. Merhaba sanal cihaz kapatıldıktan sonra durumundadır **durduruldu**.

Cmdlet'leri toostop aşağıdaki hello kullanın ve sanal cihazı başlatın.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a>toorestart sanal cihazı
Sanal cihaz çalışırken ve toorestart istediğinizde, adına tıklayın ve ardından **yeniden**. Merhaba sanal cihaz yeniden başlatıldığı sırada durumundadır **yeniden**. Merhaba sanal aygıt, toouse hazır olduğunda durumundadır **çalıştıran**.

Aşağıdaki cmdlet'i toorestart sanal cihazı hello kullanın.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

