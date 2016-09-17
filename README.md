# Payment Protocol

## Introduction
This protocol will enable the transfere of money from a sender to a receiver by using a Payment Cheque. This include both the operation of sending the Payment Cheque itself and the operation of validate, claim and collect the money the cheque is probising.

If the parties involved trusts each other, the process can be executed in short time, which allow for instant payment. The protocol also includes methods to communicate which other peers are trusted and mechanisms to recevie trust by exchanging a cheques at a trusted third party.

## Definitions
- Payment Cheque File -
- Payment Request File -
- Repeter Banking -

## Roles
### Cheque Issuer
The Cheque Issuer is the body issuing a Payment Cheque and making the promising that the cheque's money will be paid to the Cheque Receiver.

### Cheque Sender
The Cheque Sender is a body that sends the Payment Cheque to a Cheque Receiver. It can be the same body as the cheque Issuer or it can be anybody else that is holding the cheque.

### Cheque Receiver
The Cheque Receiver is the body receiveing the Payment Cheque from a Cheque Sender and which intends to claim and collect the money the cheque is promising.

### Cheque Exchanger
A Cheque Exchanger is a body that receives a Payment Cheque and issue a new cheque of with its own promise. Hence, the a Cheque Exchanger will act both as a Cheque Recever and a Cheque Issuer. The purpose of Cheque Exchagner is to allow repeter banking.

## Message flow

### Cheque Payment
The following message diagram describes the operation of making a cheque payment and the validation of the receiver cheque.

The operation involves a Cheque Sender, Cheque Receiver and Cheque Issuer. Keep in mind that the Cheque Sender can be the same party as the Cheque Issuer.

# Header



 +---------+
 |         |
 | Cheque  |
 | Sender  |
 |         |
 +---------+


## Message definition

