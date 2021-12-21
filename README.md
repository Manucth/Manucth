### 

TABLE OF CONTENT

1	Revision History	

2	Objective	

3	Scope of This Document	

4	Terms and Definitions	

Acronym	Description

3PL 	3rd Party Logistics 
CS	Customer Support
DC	Distribution center
EDI	Electronic Data Interchange
Fiori	S/4 Hana Instance
GR 	Goods Receipt 
HOI	HP Own Inventory
PGI	Post Goods Issue
PO 	Purchase Order 
PR 	Purchase Requisition 
RPA	Robotic Process Automation
S/4 	S/4 Hana (SAP system) 
SC 	Supply Chain 



5	BUSINESS PROCESS DESCRIPTION

5.1	S/4 Planning (Receiving Plant):
This process encloses the process required to create a Purchase Requisition and a Purchase Order from the beginning to the end.
The process begins with the S/4 Planning team determining the parts numbers and volumes required to support the CS business.  These part numbers and volume are calculated by the specific planning tool & process used by the relevant business.


5.2	Approval portal:
The PO may, or may not, require approval from a senior manager depending on the Buyer´s approval limit.  See below description of each case:

5.2.1	When approval is required:
5.2.1.1	If the PO request exceeds the Buyer´s approval limit, then the Buyer will need to fill out a template and upload it to the Approval portal to be reviewed by the approver.  
5.2.1.2	The approver will need to enter the approval portal to review the PO request. This will require the reviewing of parts,  volumes, price, etc., to determine if the request is valid or not, 
5.2.1.2.1	If everything is valid the PO request will be approved, and then the Buyer will receive an email alert from the approval portal informing S/4 Buying team an approved requisition template is available to process. The S4 buyer will access the portal to retrieve the request and proceed to item 5.3.
 
5.2.1.2.2	If the PO request is not approved, then the planner will be notified and will need to make the corresponding corrections to the PO template. Once the corrections are done, the PO request will need to be resent for review and approval.

5.2.2	When approval is NOT required, for example when the PO request is below the Buyer´s approval limit.
5.2.2.1	The planner simply notifies the S/4 Buying team (receiving plant) of the requirement.






5.3	S/4 Buying (Receiving Plant)
The process continues with the Buyer receiving the requirements from the PO request to execute a Purchase Requisition.  The Buyer will determine if such Purchase Requisition needs to be done by the RPA tool or if it can be submitted manually. 

5.3.1	Purchase Requisition creation:
5.3.1.1	If the Requisition is processed successfully it will get converted on the next auto-batch cycle (runs every 15 minutes) which will create the PO systematically. Or if the buyer has an urgent need they have the option to manually push the PR to get converted into a Purchase Order.
5.3.1.2	If the Purchase Requisition cannot be processed successfully, the Buyer will need to investigate the issue and try to resolve it and then reenter the Requisition once again.

5.3.2	Purchase Order creation:

5.3.2.1	If the Purchase Order is created successfully it may, or may not, have the Output Message suppressed. (For ZOCM Purchase order types, current configuration is:  the output message is always suppressed) 
5.3.2.1.1	If the Output message is suppressed it may, or may not, require a header text. (For those suppliers who require a header text code to route the order correctly on their system; please refer to addendum “XX” for instruction. For suppliers who do not need a header text code – then its an optional task )  stopped here on 16th  2021


5.3.2.1.1.1	If the PO requires a header text, the Buyer will need to input the header text and save the PO.  
5.3.2.1.1.2	If the PO does not require a header text, the Buyer will manually release the Output Message and save the PO.

5.3.2.1.2	If the Output message is not suppressed the PO will be automatically sent to the vendor via EDI 850 message (PO transmission).


5.3.2.2	If the Purchase Order cannot be created successfully, the Buyer will need to investigate the issue and try to resolve it and then reenter the PO once again. 





5.4	Vendor actions:

The vendor will receive a copy of the PO via EDI 850 and depending if there are adjustments required or not the actions are the following:
5.4.1	If there were adjustments required, the vendor needs to determine if these changes can, or cannot, be done via EDI 855.

5.4.1.1	If possible by EDI 855: The changes will be imported systematically.  
The PO will be acknowledged by the vendor and will trigger an EDI 855 to HP who will need to do an acknowledgement (refer to section 5.5 ).  The vendor will then prepare the shipment of the parts requested from the PO and do the Outbound Shipment, to finally send a pre-alert by email so HP is aware of the shipment.
5.4.1.2	If NOT possible by EDI 855: The vendor needs to inform HP about the changes needed by email. And HP will do the corresponding actions (refer to section 5.5 ).  

5.4.2	If there are no adjustments required,
The PO will be acknowledged by the vendor and will trigger an EDI 855 to HP who will need to do an acknowledgement (refer to section 5.5 ).  The vendor will then prepare the shipment of the parts requested from the PO and do the Outbound Shipment, to finally send a pre-alert by email so HP is aware of the shipment.



5.5	Adjustments and acknowledgement by S/4 Buying (Receiving Plant)

Once the Vendor has acknowledged the PO, HP will need to confirm if the PO will require changes. 

5.5.1	If the adjustments appear on the EDI 855,
This will be done automatically by the system, and here ends the process.

5.5.2	If the adjustments don´t appear on the EDI 855,

These adjustments can be manual or not.

5.5.2.1	If the changes are manual, the HP buyer must do the changes on S/4.  These changes will trigger an EDI 860 (PO change) to the vendor, which consequently will receive the PO changes and will need to send another EDI 865 (PO change ack) back to HP, and here ends the process.

5.5.2.2	If the changes are not manual, here ends the process.




5.6	3PL (Receiving Plant)
With the Outbound Shipment the 3PL will receive the four communications and be responsible of executing the actions on each of those communications described below:
•	The Invoice shipment.  The 3PL will receive an invoice from the vendor with all the relevant info about the purchase. And then the same 3PL will issue the invoice copy to the Finance team by an EDI 810 transmission.

•	An EDI 856 (shipping confirmation). The 3PL will receive this EDI systematically with all information pertain the parts ordered.

•	The manual pre-alert. The 3PL will receive this communication by email with all information pertain the parts ordered.

•	And the physical shipment.  The 3PL will receive physically the parts ordered from the PO.

5.6.1	If there is a discrepancy on the received parts, the 3PL must follow their regular receiving discrepancy protocols. 
5.6.2	If there is NO a discrepancy on the received parts, the 3PL will execute the Post Goods Receipt (PGI).


5.7	Finance accounts payable

The Accounts Payable team will receive the invoice coming from the 3PL via EDI 810 to execute their regular accounts payable processes.




















<!--
**Manucth/Manucth** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.


5.1	S/4 Planning (Receiving Plant):
This process encloses the process required to create a Purchase Requisition and a Purchase Order from the beginning to the end.
The process begins with the S/4 Planning team determining the parts numbers and volumes required to support the CS business.  These part numbers and volume are calculated by the specific planning tool & process used by the relevant business.


5.2	Approval portal:
The PO may, or may not, require approval from a senior manager depending on the Buyer´s approval limit.  See below description of each case:

5.2.1	When approval is required:
5.2.1.1	If the PO request exceeds the Buyer´s approval limit, then the Buyer will need to fill out a template and upload it to the Approval portal to be reviewed by the approver.  
5.2.1.2	The approver will need to enter the approval portal to review the PO request. This will require the reviewing of parts,  volumes, price, etc., to determine if the request is valid or not, 
5.2.1.2.1	If everything is valid the PO request will be approved, and then the Buyer will receive an email alert from the approval portal informing S/4 Buying team an approved requisition template is available to process. The S4 buyer will access the portal to retrieve the request and proceed to item 5.3.
 
5.2.1.2.2	If the PO request is not approved, then the planner will be notified and will need to make the corresponding corrections to the PO template. Once the corrections are done, the PO request will need to be resent for review and approval.

5.2.2	When approval is NOT required, for example when the PO request is below the Buyer´s approval limit.
5.2.2.1	The planner simply notifies the S/4 Buying team (receiving plant) of the requirement.






5.3	S/4 Buying (Receiving Plant)
The process continues with the Buyer receiving the requirements from the PO request to execute a Purchase Requisition.  The Buyer will determine if such Purchase Requisition needs to be done by the RPA tool or if it can be submitted manually. 

5.3.1	Purchase Requisition creation:
5.3.1.1	If the Requisition is processed successfully it will get converted on the next auto-batch cycle (runs every 15 minutes) which will create the PO systematically. Or if the buyer has an urgent need they have the option to manually push the PR to get converted into a Purchase Order.
5.3.1.2	If the Purchase Requisition cannot be processed successfully, the Buyer will need to investigate the issue and try to resolve it and then reenter the Requisition once again.

5.3.2	Purchase Order creation:

5.3.2.1	If the Purchase Order is created successfully it may, or may not, have the Output Message suppressed. (For ZOCM Purchase order types, current configuration is:  the output message is always suppressed) 
5.3.2.1.1	If the Output message is suppressed it may, or may not, require a header text. (For those suppliers who require a header text code to route the order correctly on their system; please refer to addendum “XX” for instruction. For suppliers who do not need a header text code – then its an optional task )  stopped here on 16th  2021


5.3.2.1.1.1	If the PO requires a header text, the Buyer will need to input the header text and save the PO.  
5.3.2.1.1.2	If the PO does not require a header text, the Buyer will manually release the Output Message and save the PO.

5.3.2.1.2	If the Output message is not suppressed the PO will be automatically sent to the vendor via EDI 850 message (PO transmission).


5.3.2.2	If the Purchase Order cannot be created successfully, the Buyer will need to investigate the issue and try to resolve it and then reenter the PO once again. 





5.4	Vendor actions:

The vendor will receive a copy of the PO via EDI 850 and depending if there are adjustments required or not the actions are the following:
5.4.1	If there were adjustments required, the vendor needs to determine if these changes can, or cannot, be done via EDI 855.

5.4.1.1	If possible by EDI 855: The changes will be imported systematically.  
The PO will be acknowledged by the vendor and will trigger an EDI 855 to HP who will need to do an acknowledgement (refer to section 5.5 ).  The vendor will then prepare the shipment of the parts requested from the PO and do the Outbound Shipment, to finally send a pre-alert by email so HP is aware of the shipment.
5.4.1.2	If NOT possible by EDI 855: The vendor needs to inform HP about the changes needed by email. And HP will do the corresponding actions (refer to section 5.5 ).  

5.4.2	If there are no adjustments required,
The PO will be acknowledged by the vendor and will trigger an EDI 855 to HP who will need to do an acknowledgement (refer to section 5.5 ).  The vendor will then prepare the shipment of the parts requested from the PO and do the Outbound Shipment, to finally send a pre-alert by email so HP is aware of the shipment.




















5.5	Adjustments and acknowledgement by S/4 Buying (Receiving Plant)

Once the Vendor has acknowledged the PO, HP will need to confirm if the PO will require changes. 

5.5.1	If the adjustments appear on the EDI 855,
This will be done automatically by the system, and here ends the process.

5.5.2	If the adjustments don´t appear on the EDI 855,

These adjustments can be manual or not.

5.5.2.1	If the changes are manual, the HP buyer must do the changes on S/4.  These changes will trigger an EDI 860 (PO change) to the vendor, which consequently will receive the PO changes and will need to send another EDI 865 (PO change ack) back to HP, and here ends the process.

5.5.2.2	If the changes are not manual, here ends the process.






















5.6	3PL (Receiving Plant)
With the Outbound Shipment the 3PL will receive the four communications and be responsible of executing the actions on each of those communications described below:
•	The Invoice shipment.  The 3PL will receive an invoice from the vendor with all the relevant info about the purchase. And then the same 3PL will issue the invoice copy to the Finance team by an EDI 810 transmission.

•	An EDI 856 (shipping confirmation). The 3PL will receive this EDI systematically with all information pertain the parts ordered.

•	The manual pre-alert. The 3PL will receive this communication by email with all information pertain the parts ordered.

•	And the physical shipment.  The 3PL will receive physically the parts ordered from the PO.

5.6.1	If there is a discrepancy on the received parts, the 3PL must follow their regular receiving discrepancy protocols. 
5.6.2	If there is NO a discrepancy on the received parts, the 3PL will execute the Post Goods Receipt (PGI).


5.7	Finance accounts payable

The Accounts Payable team will receive the invoice coming from the 3PL via EDI 810 to execute their regular accounts payable processes.


