Since Vistara-SHG pools real money between members and pays out a winner, treat the profile-verification step as actual KYC, not just a profile form. Here's what to collect:

**Identity**
- Full name (as per government ID)
- Date of birth
- Gender
- Father's/spouse's name
- Aadhaar number (masked in DB, store only last 4 digits + hashed reference)
- PAN number — important once yearly contributions cross reporting thresholds
- A live selfie for face-match against the ID photo (basic liveness check, not just an upload)

**Address**
- Current address
- Permanent address (if different)
- Proof document type + upload (Aadhaar, utility bill, or bank statement)

**Contact (verify both, don't just collect)**
- Mobile number — OTP verified
- Email — verification link

**Bank details (needed for payouts to the winner)**
- Account holder name
- Account number
- IFSC code
- Bank name/branch
- Proof: cancelled cheque or passbook first page

**Financial profile**
- Occupation
- Annual income bracket
- Source of funds (declaration — standard for pooled-money products)

**Documents to store**
- Aadhaar front + back
- PAN card
- Bank proof
- Selfie/liveness capture

**Consent**
- Terms & KYC consent checkbox with timestamp
- Explicit consent to be part of a pooled-money scheme

One thing worth flagging before you go further: a bhishi is structurally a chit fund / ROSCA. In India, chit funds are regulated under the **Chit Funds Act, 1982** and generally need registration with the state Registrar of Chits, plus PMLA-style KYC obligations once you're pooling and disbursing member money. That's a legal/compliance question, not an engineering one — worth a quick check with a lawyer or CA before you launch this for real money, even if v1 is just for a closed friends-and-family group. I'm not able to give legal advice here, just flagging it so it doesn't bite you later.

For your schema, I'd put verification fields in a separate `kyc_details` table (not on the main `users` table) with a `status` enum (`pending/approved/rejected`), `reviewed_by`, `reviewed_at`, and `rejection_reason` — makes the admin approval audit trail clean and keeps sensitive documents out of your main user queries.
