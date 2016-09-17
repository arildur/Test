# Payment Protocol

## 1 Introduction
This protocol will enable the transfer of money from a sender to a receiver by using a Payment Cheque. This include both the operation of sending the Payment Cheque itself and the operation of validate, claim and collect the money the cheque is promising.

If the parties involved trusts each other, the process can be executed in short time, which allow for instant payment. The protocol also includes methods to communicate which other peers are trusted and mechanisms to receive trust by exchanging a cheques at a trusted third party.

## 2 Definitions
- Payment Cheque File - This is the cheque as defined in the Payment Cheque File Specification. A cheque is a promise that its issuer will pay its face value to a receiver by terms as noted in the cheque.
- Payment Request File -
- Repeater Banking -

## 3 Roles
### 3.1 Cheque Issuer
The Cheque Issuer is the body issuing a Payment Cheque and making the promising that the cheque's money will be paid to the Cheque Receiver.

### 3.2 Cheque Sender
The Cheque Sender is a body that sends the Payment Cheque to a Cheque Receiver. It can be the same body as the cheque Issuer or it can be anybody else that is holding the cheque.

### 3.3 Cheque Receiver
The Cheque Receiver is the body receiving the Payment Cheque from a Cheque Sender and which intends to claim and collect the money the cheque is promising.

### 3.4 Cheque Exchanger
A Cheque Exchanger is a body that receives a Payment Cheque and issue a new cheque of with its own promise. Hence, the a Cheque Exchanger will act both as a Cheque Receiver and a Cheque Issuer. The purpose of Cheque Exchanger is to allow repeater banking.

## 4 Message flow

### 4.1 Overview of a complete payment operation
The following message diagram describes a complete payment operation of requesting payment, issue a cheque, transferring the cheque and the validation and collecting of the cheque's money.

Note that message (A), (B) and (C) of the operation is described in other specification and protocol documents.

Note that the Cheque Issuer body at the left and right in the diagram is the same body. It is painted twice in order to make the diagram easier to read.

The operation involves a Cheque Sender, Cheque Receiver and Cheque Issuer. In this example the Cheque Sender may be a customer and Cheque Receiver may be a merchant.

```
 +------------+           +------------+           +------------+           +------------+
 |            |           |            |<---(A)----|            |           |            |
 |            |<---(B)----|            |           |            |           |            |
 |            |----(C)--->|            |           |            |           |            |
 |  Cheque    |           |   Cheque   |----(D)--->|   Cheque   |           |   Cheque   |
 |  Issuer    |           |   Sender   |           |  Receiver  |----(E)--->|   Issuer   |
 |  (bank)    |           | (customer) |           | (merchant) |<---(F)----|   (bank)   |
 |            |           |            |<---(G)----|            |           |            |
 |            |           |            |<---(H)--->|            |           |            |
 |            |           |            |           |            |<---(I)----|            |
 +------------+           +------------+           +------------+           +------------+
```

A: Cheque Sender (customer) reads some information from the Cheque Receiver (merchant) and is requested to make a payment. Customer reads price and terms as a payment request from the merchant. (This payment request and the message is not covered by this protocol. The payment request may provided as a Payment Request as defined by the Payment Request File Specification and the message may be provided as defined in the Payment Request Protocol.)

B: Cheque Sender (customer) accepts the price and terms stated in the Payment Request and requests the Cheque Issuer (bank) to issue a cheque. (This request is not covered by this protocol, but may be sent using the Banking App Protocol.)

C: The Cheque Issuer (bank) accepts the request and issue a Payment Cheque and responds back to the customer with a Payment Cheque File. (This response is not covered by this protocol, but may be sent using the Banking App Protocol.)

D: Cheque Sender (customer) sends a send_cheque message to Cheque Receiver (merchant) containing a Payment Cheque File.

E: The Cheque Receiver (merchant) receives the Payment Cheque File from the Cheque Sender (customer). The merchant verifies that the cheque's terms meet his own payment requirements. If the merchant accepts the cheque and trusts the Cheque Issuer (bank), he can send a claim_cheque message to the bank.

F The Cheque Issuer (bank) receive the claim_cheque message. The issuer verifies the claimed cheque is a cheque that the issuer has issued and that it is unclaimed and that the claim meets the terms stated in the cheque. If the claim is valid, the issuer responds with claim_cheque_response message with result set to OK.

G: If the Cheque Receiver receives claim_cheque_response with result set to OK, the receiver can responds back to Cheque Sender with send_cheque_response message with result set to OK.

H: The payment operation between the Cheque Issuer (customer) and Cheque Receiver (merchant) is successfully completed and the customer is entitled to access whatever has been agreed from the merchant.

I: Some time later, when the Payment Cheque Escrow Time has elapsed and provided that Cheque Sender (customer) has not given complain to the Cheque Issuer (bank), the bank will make the money transfer according to the claim_cheque message. When the bank starts the money transfer, the bank will send a transfer_status message to the Cheque Receiver (merchant).

## Message definition
Overview of protocol messages:


| Method | Request message   | Response messages          | Sender        | Receiver
|--------|-------------------|----------------------------|---------------|----------
| POST   | send_cheque       | send_cheque_response       | Any           | Any with Money Address
| POST   | validate_cheque   | validate_cheque_response   | Any           | Cheque Issuer
| POST   | claim_cheque      | claim_cheque_response      | Any           | Cheque Issuer
| POST   | collect_money     | collect_money_response     | Any           | Cheque Issuer
| POST   | cheque_status     | cheque_status_response     | Cheque Issuer | Any
| POST   | get_cheque_status | get_cheque_status_response | Any           | Cheque Issuer
| POST   | exchange_cheque   | exchange_cheque_response   | Any           | Cheque Issuer
| GET    | ping              | ping_response              | Any           | Any with Money Address
| GET    | trusted_banks     | trusted_banks_response     | Any           | Any with Money Address

