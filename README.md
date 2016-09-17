# Payment Protocol

## 1 Introduction
This protocol will enable the transfere of money from a sender to a receiver by using a Payment Cheque. This include both the operation of sending the Payment Cheque itself and the operation of validate, claim and collect the money the cheque is probising.

If the parties involved trusts each other, the process can be executed in short time, which allow for instant payment. The protocol also includes methods to communicate which other peers are trusted and mechanisms to recevie trust by exchanging a cheques at a trusted third party.

## 2 Definitions
- Payment Cheque File - This is the cheque as defined in the Payment Cheque File Specifiation. A cheque is a promis that its issuer will pay its face value to a receiver by terms as noted in the cheque.
- Payment Request File -
- Repeter Banking -

## 3 Roles
### 3.1 Cheque Issuer
The Cheque Issuer is the body issuing a Payment Cheque and making the promising that the cheque's money will be paid to the Cheque Receiver.

### 3.2 Cheque Sender
The Cheque Sender is a body that sends the Payment Cheque to a Cheque Receiver. It can be the same body as the cheque Issuer or it can be anybody else that is holding the cheque.

### 3.3 Cheque Receiver
The Cheque Receiver is the body receiveing the Payment Cheque from a Cheque Sender and which intends to claim and collect the money the cheque is promising.

### 3.4 Cheque Exchanger
A Cheque Exchanger is a body that receives a Payment Cheque and issue a new cheque of with its own promise. Hence, the a Cheque Exchanger will act both as a Cheque Recever and a Cheque Issuer. The purpose of Cheque Exchagner is to allow repeter banking.

## 4 Message flow

### 4.1 Cheque Payment
The following message diagram describes the operation of making a cheque payment and the validation of the receiver cheque.

The operation involves a Cheque Sender, Cheque Receiver and Cheque Issuer. Keep in mind that the Cheque Sender can be the same party as the Cheque Issuer.
```
 +------------+           +------------+           +------------+
 |            |           |            |           |            |
 |   Cheque   |----(A)--->|   Cheque   |           |   Cheque   |
 |   Sender   |           |  Receiver  |----(B)--->|   Issuer   |
 |            |           |            |<---(C)----|            |
 |            |<---(D)----|            |           |            |
 |            |           |            |           |            |
 +------------+           +------------+           +------------+
```
A: Cheque Sender sends a send_cheque message to Cheque Receiver containing a Payment Cheque File.

B: The Cheque Receiver receives the Payemtn Cheque File and checks that the cheque's terms meet his own payment requirement. If the receiver accepts the cheque and trusts the Cheque Issuer, he sends a claim_cheque message to the Cheque Issuer.

C: The Cheque Issuer receive the claim_cheque message. The issuer verifies the claimed cheque is a cheque that the issuer has issued and that it is unclaimed and that the claim meets the terms steded in the cheque. If the claim is valid, the issuer responds with claim_cheque_response message with result set to OK.

D: If the Cheque Receiver receives claim_cheque_response with result set to OK, the receiver can responds back to Cheque Sender with send_cheque_response message with result set to OK.

## Message definition
Overview of protocol methods:


