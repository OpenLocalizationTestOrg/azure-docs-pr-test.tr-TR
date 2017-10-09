<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a>StorSimple için Windows PowerShell aracılığıyla tooinstall düzenli güncelleştirmeler
1. Açık hello cihaz seri konsoluna ve seçenek 1, **oturum oturum tam erişim**. Merhaba parolayı girin. Merhaba varsayılan parola *Parola1*. 
2. Merhaba komut satırına aşağıdakini yazın:
   
     `Get-HcsUpdateAvailability`
   
    Güncelleştirmeler varsa ve kesintiye uğratan veya benzer hello güncelleştirmelerin olup olmadığını size bildirilecek.
3. Merhaba komut satırına aşağıdakini yazın:
   
     `Start-HcsUpdate`
   
    Merhaba güncelleştirme işlemi başlar.

> [!IMPORTANT]
> * Bu komut yalnızca tooregular güncelleştirmeleri uygular. Bu komut yalnızca bir denetleyicisinde çalıştırın, ancak her iki denetleyicileri güncelleştirilir. 
> * Denetleyici yük devretmesi hello güncelleştirme işlemi sırasında fark edebilirsiniz; Ancak, hello yük devretme sistem kullanılabilirliğini veya işlem etkilemez.
> 
> 

