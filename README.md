# BLE from Ground up in STM32

# 1. Basic Knowledge
A very good reading resource is in the following link: 
[The Basics of Bluetooth Low Energy](https://www.novelbits.io/basics-bluetooth-low-energy/)
. You can also download the free ebook from the 
[website](https://novelbits-my.sharepoint.com/personal/mohammad_novelbits_io/_layouts/15/onedrive.aspx?id=%2Fpersonal%2Fmohammad%5Fnovelbits%5Fio%2FDocuments%2FIntro%20to%20BLE%20e%2Dbook%2FUpdate%2011%2D2018%2FIntro%20to%20Bluetooth%20Low%20Energy%20v1%2E1%2Epdf&parent=%2Fpersonal%2Fmohammad%5Fnovelbits%5Fio%2FDocuments%2FIntro%20to%20BLE%20e%2Dbook%2FUpdate%2011%2D2018&originalPath=aHR0cHM6Ly9ub3ZlbGJpdHMtbXkuc2hhcmVwb2ludC5jb20vOmI6L2cvcGVyc29uYWwvbW9oYW1tYWRfbm92ZWxiaXRzX2lvL0VmamZmVEgxTFZ0TWk3RWw3SGtvMDJBQmNxLTBRb2pjc2VQUktCaTl1MkJPTmc_cnRpbWU9OUNRYlhJYlAxMGc)
. Here, we only provide some essential knowledge. 
### 1.1 BLE Structure
Let's see the architecture of the BLE in the following image.
<p align="center">
<img src="/img/BLE_Structure.JPG" height="50%" width="50%"> 
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
            <td align="Left">• The transmitter uses GFSK modulation and operates at unlicensed 2.4 GHz frequency band.<br />• Using this PHY layer, BLE offers data rates of 1 Mbps (Bluetooth v4.2)/2 Mbps (Bluetooth v5.0).<br />• It uses frequency hopping transceiver.<br /> • Two modulation schemes are specified to deliver 1 Msym/s and 2 Msym/s.<br /> • Two PHY layer variants are specified viz. uncoded and coded.<br />• A Time Division Duplex (TDD) topology is employed in both of the PHY modes.</td>
        </tr>
        <tr>
            <td align="center">Link Layer</td>
            <td align="Left">It is responsible for advertising, scanning, and creating/maintaining connections. The role of BLE devices changes in peer to peer (i.e. Unicast) or broadcast modes. The common roles are Advertiser/Scanner (Initiator), Slave/Master or Broadcaster/Observer. Link layer states are defined in the figure below.<br /> <p align="center">
<img src="/img/BLE-States.jpg" height="40%" width="40%"> 
</p> </td>
        </tr>
      <tr>
            <td align="center">HCI</td>
          <td align="Left">It provides <b>communication between controller and host</b> through standard interface types. This HCI layer can be implemented either using API or by interfaces such as UART/SPI/USB. Standard HCI commands and events are defined in the bluetooth specifications.</td>
        </tr>
      <tr>
            <td align="center">L2CAP</td>
          <td align="Left">This layer offers <b>data encapsulation</b> services to upper layers. This allows logical end to end data communication.</td>
        </tr>
      <tr>
            <td align="center">SMP</td>
          <td align="Left">This security Manager layer provides methods for <b>device pairing</b> and <b>key distributions</b>. It offers services to other protocol stack layers in order to securely connect and exchange data between BLE devices.</td>
        </tr>
      <tr>
            <td align="center">GAP</td>
            <td align="Left">This layer directly interfaces with application layer and/or profiles on it. It handles <b>device discovery</b> and <b>connection related services</b> for BLE device. It also takes care of <b>initiation of security features</b>.</td>
        </tr>
      <tr>
            <td align="center">GATT</td>
            <td align="Left">This layer is service framework which specifies sub-procedures to use ATT. Data communications between two BLE devices are handled through these sub-procedures. The applications and/or profiles will use GATT directly.</td>
        </tr>
      <tr>
            <td align="center">ATT</td>
            <td align="Left">This layer allows BLE device to expose certain pieces of data or attributes.</td>
        </tr>
      <tr>
            <td align="center">Application Layer</td>
            <td align="Left">• The BLE protocol stack layers interact with applications and profiles as desired. Application interoperability in the Bluetooth system is accomplished by Bluetooth profiles.<br />• The profile defines the vertical interactions between the layers as well as the peer-to-peer interactions of specific layers between devices.<br />• A profile composed of one or more services to address particular use case. A service consists of characteristics or references to other services.<br />• Any profiles/applications run on top of GAP/GATT layers of BLE protocol stack. It handles device discovery and connection related services for the BLE device.</td>
        </tr>
    </tbody>
</table>
</p>

### 1.2 Chip Configuration
The three separate layers of the protocol and the standardized interface make it possible to implement the Host and Controller on different platforms. The following configurations are commonly used:
<p align="center">
<table>
    <thead>
        <tr>
            <th align="center">Configuration</th>
            <th align="center">Detail</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td align="center">Single-chip</td>
          <td align="Left">A single microcontroller implements all three layers and the application itself. In this case the BLE Host and the BLE Controller communicate directly through function calls and queues in RAM. The Bluetooth specification does not specify how HCI is implemented.<br /> This configuration is well suited for those applications and designs that require a small footprint and the lowest possible power consumption, since everything runs on a single IC.</td>
        </tr>
      <tr>
            <td align="center">Dual-chip</td>
          <td align="Left"><p align="center">
<img src="/img/chip-configuration.JPG" height="70%" width="70%"> </p> A. Typically used for cell phone or computer since they have powerful processor. <br />B. The chip for the application can be very samll and low power because the application doesn't need much memory or resources.</td>
        </tr>
        <tr>
            <td align="center">Three-chip</td>
          <td align="Left">Application, Host, and Controller layer are implemented on three different chip. The Host need two communication interface between Host-Application and Host-Controller. This is a very expensive configuration</td>
        </tr>
    </tbody>
</table>
</p>

### 1.3  BLE type of Device
<table>
    <thead>
        <tr>
            <th align="center">Item</th>
            <th align="center">Detail</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td align="center">Peripherals</td>
          <td align="Left">A peripheral device is a device that announces its presence by sending out advertising
packets and accepts a connection from another BLE device (the BLE central). <br /><br /> • <b>Broadcaster:</b> a device that sends out
advertising packets as well, but with one difference from a peripheral: the broadcaster does
              not allow a connection from a central device. <br /> • <b>Observer:</b> only discovers advertising devices, but does not have the capability to initiate a connection with the advertiser. </td>
        </tr>
      <tr>
            <td align="center">Centrals</td>
          <td align="Left"> a device that discovers and listens to other BLE devices that are advertising. It is also capable of establishing a connection to BLE peripherals (usually multiple at the same time).</td>
        </tr>
        <tr>
            <td align="center">Broadcaster</td>
          <td align="Left">a device that sends out advertising packets as well, but with one difference from a peripheral: the broadcaster does not allow a connection from a central device.</td>
        </tr>
        <tr>
            <td align="center">Observer</td>
          <td align="Left">Only discovers advertising devices, but does not have the capability to initiate a connection with the advertiser.</td>
        </tr>
    </tbody>
</table>
</p>

The following table is the files that we are going to use to program in BLE chip.
<p align="center">
<img src="/img/ACI_file.JPG" height="60%" width="60%"> 
</p> 

