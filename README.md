The mn12Yji source file is dated 4/19/22 and has &HFD72 CRC value.

During the run-time, a copy of the Crystal's EEPROM value (&H025D / 605dec.) is stored at $10001F96 (1 byte) RAM location.

Additional RAM locations :   HdrRateAccum       EQU $10001F84       ;byte, holds the cumulative sum of HdrRate entries. Incremented for every error-free RF Header received.
                             RxRateAccum        EQU $10001F85       ;byte, holds the cumulative sum of RxRate entries. Incremented for every error-free RF Payload received.
                             PrmblRateAccum 		EQU $10001F86       ;byte, holds the cumulative sum of Preamble detections. Incremented for every error-free Preamble detected.

Definitions of the "Diag" line of the LexNet (RAM start address is $100018C0):
T    Pr    {}   Cr    {}    Rx    Hd    Dc    PTxed PRxed
xx   xx    xx   xx    xx    xx    xx    xx    xxxx  xxxx  

where:  T     - radio's temperature
        Pr    - counter of number of RF Preambles detected
        Cr    - radio's Crystal value read from EEPROM
        Rx    - counter of error-free RF Payloads received
        Hd    - counter of error-free RF Headers received
        Dc    - counter of the number of times the radio had to RF-disconnect from the Master
        PTxed - number of RF packets transmitted
        PRxed - number of RF packets received

To tune Slave radio's receive, send to the radio CrystalUp or CrystalDwn commands and observe Preamble Rate, Rx Rate, and Header Rate. The goal is to maximize these numbers. In the case when the Master is not transmitting RF packets with the data payloads, the Header Rate reported by the Slave will be the best indicator.

For each CrystalUp and CrystalDwn command, the radio's run-time Crystal will increment or decrement respectively. Its current value can be observed at the RAM address $10001F96, which can be viewed within the 'Data Display' LexNet's frame at the top raw labeled '$10001F90' under the seventh location labeled by "$6" on top of it.

When done tunning, please use Commtel to write the resulting Crystal value into the radio's 605(decimal) address.
