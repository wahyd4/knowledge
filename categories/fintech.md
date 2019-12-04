# Fintech(Financial technology)

## ISO8583 message

### A example

```
02004200040000000002161234567890123456060
9173030123456789ABC1000123456789012345678
90123456789012345678901234567890123456789
0123456789012345678901234567890123456789
```
Where:

```
  0200 - MTI (Message Type Indicator),
  4200040000000002 - primary bitmap,
  161234567890123456 - field 2, the first 2 digits: 16, is length indicator
  0609173030 - field 7,
  123456789ABC - field 22,
  012345678901234567890123456789012345678901234567890\
  1234567890123456789012345678901234567890123456789 - field 63.
```

### Definition

ISO8583 message is used in bank or financial institutes card-originated transactions. But sometime, those not card-originated transactions also use ISO8583.

### Typical Parts

Typical Fields an ISO8583 message
A typical message might include such fields:
```
MTI - Message Type Indicator.
Bit 2 - Primary Account Number (PAN)
Bit 3 - Processing Code
Bit 7 - Date and Time of transmission
Bit 11 - Audit Code
Bit 12 - Local time transaction
Bit 13 - Local transaction date
Bit 32 - Identification code of the institution of acquisition
Bit 38 - The authorization code in response
Bit 39 - Response Code
Bit 49 - Currency code of transaction
```
