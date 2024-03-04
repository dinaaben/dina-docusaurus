---
sidebar_label: 'Hi!'
sidebar_position: 3
---

# Hello Hello!

This is my **first Docusaurus document**!
I am adding a sentence.


# Hello Hello!

This is my **first Docusaurus document**!
I am adding another sentence.
And another sentence

```mermaid
sequenceDiagram
    participant IMSClient
    participant P_CSCF
    participant I_CSCF
    participant S_CSCF
    participant HSS
    participant UE

    IMSClient->>P_CSCF: REGISTER
    P_CSCF->>I_CSCF: Forward REGISTER
    I_CSCF->>HSS: Poll for S-CSCF data
    HSS-->>I_CSCF: S-CSCF decision data
    I_CSCF->>S_CSCF: Forward REGISTER
    S_CSCF->>P_CSCF: 401 - UNAUTHORIZED, Challenge
    P_CSCF->>UE: Forward 401 - UNAUTHORIZED, Challenge
    UE->>UE: Hash SSD + Nonce
    UE->>P_CSCF: REGISTER with hashed values
    P_CSCF->>I_CSCF: Forward new REGISTER
    I_CSCF->>S_CSCF: Forward new REGISTER
    S_CSCF->>HSS: Poll for SSD
    HSS-->>S_CSCF: SSD
    S_CSCF->>S_CSCF: Hash SSD + Nonce, Check Match
    S_CSCF-->>P_CSCF: 200 - OK
    P_CSCF-->>UE: Forward 200 - OK
    ```