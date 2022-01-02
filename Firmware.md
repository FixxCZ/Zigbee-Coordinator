# Flashovani firmware CC2652P a CC2538
Pro nahrani nejnovejiho FW doprucuju oficialni TI nastroj SmartRF Flash Programmer 2, po registraci zdarma na stazeni zde https://www.ti.com/tool/FLASH-PROGRAMMER  nebo muj mirror https://webshare.cz/#/file/CABRiHRXsC<br><br>
Koordinator FW pro muj CC2652P je zde (aktualne je stabilni verze 20210319):<br>
https://github.com/egony/cc2652p_E72-2G4M20S1E/tree/master/firmware/coordinator <br>
Ma podporu LED a je to overeny stabilni FW.<br><br>
Je mozne pouzit i FW od Koenkk, je funkcni jen na nem nesviti diody, pouze cervena kdyz je v rezimu parovani. Muj stick je design **Egony Stick V4 (Ebyte ver.)** takze soubor CC1352P2_CC2652P_other_*.zip (Napr. CC1352P2_CC2652P_other_coordinator_20210708.zip)<br>
https://github.com/Koenkk/Z-Stack-firmware/tree/master/coordinator/Z-Stack_3.x.0/bin

Router FW pro CC2652P neni custom a pouziva se standardni od Koenkk, tim padem neni zesilovac aktivni. Na router je lepsi pouzit CC2538.<br>
https://github.com/Koenkk/Z-Stack-firmware/tree/master/router/Z-Stack_3.x.0/bin<br>

Koordinator FW pro CC2538 zde<br>
https://github.com/jethome-ru/zigbee-firmware/tree/master/ti/coordinator/cc2538_cc2592 <br>

Router firmware pro CC2538<br>
https://github.com/jethome-ru/zigbee-firmware/tree/master/ti/router/cc2538_cc2592 <br>



### Postup
1. Stahnete si FW a otevrte SmartRF Flash Programmer 2.
2. Pripojte dongle, v Programmeru vam musi pribyt nova polozka<br>
![image](https://user-images.githubusercontent.com/46757804/116809294-88b74900-ab3d-11eb-9db1-26fa0fc103ad.png)<br>
*V pripade, ze se neobjevi, doprucuju nainstalovat CH340 driver https://sparks.gogo.co.nz/ch340.html*
3. Na donglu zmacknete a drzte tlacitko Flash a kratce stisknete tlacitko Reset, pote tlacitko Flash uvolnete.
4. Kliknete na Unknown radek u polozky USB-SERIAL CH340 a dole vyberte CC2652P a nebo CC2538xF53 podle toho jaky stick flashujete.<br>
![image](https://user-images.githubusercontent.com/46757804/116809382-08ddae80-ab3e-11eb-852a-e2017a036182.png)
5. Nastavte si Programmer podle tohoto obrazku<br>![image](https://user-images.githubusercontent.com/46757804/116809418-3a567a00-ab3e-11eb-962c-49d037e7d5fb.png)<br>
*Nikdy nezasktavejte Disable Bootloader jinak uz stick nepujde flashovat.*<br>
6. Klikente na tlacitko vypadajici jako Play<br>
7. Vysledek by mel vypadat takhle:<br>
![image](https://user-images.githubusercontent.com/46757804/116809514-afc24a80-ab3e-11eb-8eab-5678cfe881da.png)





