# RestrictedLockupToken Contract Documentation

## Table of Contents

1. Overview
2. Contract Specifications
3. Constructor
4. Public Variables
5. Modifiers
6. External Functions
7. Internal Functions
8. Events
9. Setup and Configuration

---

## 1. Overview

The `RestrictedLockupToken` contract represents a token with a lockup period for each investor. The lockup period ensures that investors cannot transfer their tokens before a specified end time. Additionally, token transfers are restricted based on KYC status, accreditation status, and region.

---

## 2. Contract Specifications

- **Name**: `RestrictedLockupToken`
- **Symbol**: `RLT`
- **Decimals**: `18`

---

## 3. Constructor

The constructor initializes the token with the following parameters:

- **_admin**: Address of the admin who will have specific privileges over the contract.
- **investors**: Array of investor addresses.
- **amounts**: Array of token amounts to be distributed to each investor.
- **lockupEndTimes**: Array of lockup end timestamps for each investor.

**Note**: The length of the `investors`, `amounts`, and `lockupEndTimes` arrays must be the same.

---

## 4. Public Variables

- **admin**: Address of the admin.
- **hasPassedKYC**: Mapping to track if an address has passed the KYC process.
- **isAccreditedInvestor**: Mapping to track if an address is an accredited investor.
- **investorRegion**: Mapping to store the region of each investor.
- **lockupEndTime**: Mapping to store the lockup end timestamp for each investor.

---

## 5. Modifiers

- **onlyAdmin**: Ensures that only the admin can call a function.

---

## 6. External Functions

- **setInvestorData(investor, kycStatus, accreditedStatus, region)**:
    - Allows the admin to set KYC status, accreditation status, and region for an investor.
    - Parameters:
        - **investor**: Address of the investor.
        - **kycStatus**: Boolean indicating KYC status.
        - **accreditedStatus**: Boolean indicating accreditation status.
        - **region**: String indicating the region of the investor.

- **transfer(recipient, amount)**:
    - Allows an investor to transfer tokens to another investor.
    - Checks if the tokens are locked up and if both the sender and recipient have passed KYC, are accredited, and belong to the same region.
    - Parameters:
        - **recipient**: Address of the recipient.
        - **amount**: Amount of tokens to transfer.

- **transferFrom(sender, recipient, amount)**:
    - Allows a third party to transfer tokens on behalf of an investor, given an allowance.
    - Has the same checks as the `transfer` function.
    - Parameters:
        - **sender**: Address of the sender.
        - **recipient**: Address of the recipient.
        - **amount**: Amount of tokens to transfer.

- **balanceOf(account)**:
    - Returns the token balance of a specific address.
    - Parameter:
        - **account**: Address of the account.

- **approve(spender, amount)**:
    - Approves a third party to spend tokens on behalf of the caller.
    - Parameters:
        - **spender**: Address of the third party.
        - **amount**: Amount of tokens to approve.

- **allowance(owneraddress, spenderaddress)**:
    - Returns the amount of tokens that a third party is allowed to spend on behalf of an owner.
    - Parameters:
        - **owneraddress**: Address of the owner.
        - **spenderaddress**: Address of the spender.

---

## 7. Internal Functions

- **_transfer(sender, recipient, amount)**:
    - Handles the transfer of tokens.
    - Parameters:
        - **sender**: Address of the sender.
        - **recipient**: Address of the recipient.
        - **amount**: Amount of tokens to transfer.

- **_approve(owneraddress, spenderaddress, amount)**:
    - Handles the approval of tokens for a third party.
    - Parameters:
        - **owneraddress**: Address of the owner.
        - **spenderaddress**: Address of the spender.
        - **amount**: Amount of tokens to approve.

---

## 8. Events

- **Transfer(from, to, value)**: Emitted when tokens are transferred.
- **Approval(owner, spender, value)**: Emitted when tokens are approved for a third party.

---

## 9. Setup and Configuration

To deploy and set up the `RestrictedLockupToken` contract:

1. Prepare the list of investor addresses, their respective token amounts, and lockup end timestamps.
2. Deploy the contract with the admin's address, the list of investors, token amounts, and lockup end timestamps.
3. After deployment, the admin can use the `setInvestorData` function to set the KYC status, accreditation status, and region for each investor.
4. Investors can then transfer tokens using the `transfer` function, but only after their lockup period has ended and if they meet the KYC and accreditation requirements.

---
