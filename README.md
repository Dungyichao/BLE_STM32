# BLE from Ground up in STM32

# 1. Basic Knowledge
A very good reading resource is in the following link: 
[The Basics of Bluetooth Low Energy](https://www.novelbits.io/basics-bluetooth-low-energy/)
. You can also download the free ebook from the 
[website](https://novelbits-my.sharepoint.com/personal/mohammad_novelbits_io/_layouts/15/onedrive.aspx?id=%2Fpersonal%2Fmohammad%5Fnovelbits%5Fio%2FDocuments%2FIntro%20to%20BLE%20e%2Dbook%2FUpdate%2011%2D2018%2FIntro%20to%20Bluetooth%20Low%20Energy%20v1%2E1%2Epdf&parent=%2Fpersonal%2Fmohammad%5Fnovelbits%5Fio%2FDocuments%2FIntro%20to%20BLE%20e%2Dbook%2FUpdate%2011%2D2018&originalPath=aHR0cHM6Ly9ub3ZlbGJpdHMtbXkuc2hhcmVwb2ludC5jb20vOmI6L2cvcGVyc29uYWwvbW9oYW1tYWRfbm92ZWxiaXRzX2lvL0VmamZmVEgxTFZ0TWk3RWw3SGtvMDJBQmNxLTBRb2pjc2VQUktCaTl1MkJPTmc_cnRpbWU9OUNRYlhJYlAxMGc)
. Here, we only provide some essential knowledge. Let's see the architecture of the BLE in the following image.
<p align="center">
<img src="/img/BLE_Structure.JPG" height="80%" width="80%"> 
</p> 
Some simple explaination of each term can be found in the following table. (reference
[https://www.rfwireless-world.com/Terminology/BLE-Protocol-Stack-Architecture.html](https://www.rfwireless-world.com/Terminology/BLE-Protocol-Stack-Architecture.html)

)
<p align="center">
<table>
    <thead>
        <tr>
            <th align="center">Layer</th>
            <th align="center">Detail</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td align="center">Physical Layer</td>
            <td align="Left">* The transmitter uses GFSK modulation and operates at unlicensed 2.4 GHz frequency band.<br /> * Using this PHY layer, BLE offers data rates of 1 Mbps (Bluetooth v4.2)/2 Mbps (Bluetooth v5.0).<br /> * It uses frequency hopping transceiver.<br /> * Two modulation schemes are specified to deliver 1 Msym/s and 2 Msym/s.<br /> * Two PHY layer variants are specified viz. uncoded and coded.<br /> * A Time Division Duplex (TDD) topology is employed in both of the PHY modes.</td>
        </tr>
        <tr>
            <td align="center">Link Layer</td>
            <td align="Left">It is responsible for advertising, scanning, and creating/maintaining connections. The role of BLE devices changes in peer to peer (i.e. Unicast) or broadcast modes. The common roles are Advertiser/Scanner (Initiator), Slave/Master or Broadcaster/Observer. Link layer states are defined in the figure below.<br /> <p align="center">
<img src="/img/BLE-States.jpg" height="80%" width="80%"> 
</p> </td>
        </tr>
      <tr>
            <td align="center"> </td>
            <td align="Left"> </td>
        </tr>
      <tr>
            <td align="center"> </td>
            <td align="Left"> </td>
        </tr>
      <tr>
            <td align="center"> </td>
            <td align="Left"> </td>
        </tr>
      <tr>
            <td align="center"> </td>
            <td align="Left"> </td>
        </tr>
      <tr>
            <td align="center"> </td>
            <td align="Left"> </td>
        </tr>
      <tr>
            <td align="center"> </td>
            <td align="Left"> </td>
        </tr>
      <tr>
            <td align="center"> </td>
            <td align="Left"> </td>
        </tr>
    </tbody>
</table>
</p>

The three separate layers of the protocol and the standardized interface make it possible to implement the Host and Controller on different platforms. 

The following table is the files that we are going to use to program in BLE chip.
<p align="center">
<img src="/img/ACI_file.JPG" height="70%" width="70%"> 
</p> 

