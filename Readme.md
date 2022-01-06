# solana nft marketplace contract design
1. list_for_sale 
    - Params 
        ● NFT List price 
    - Accounts 
        ● “Seller Account” (Signer) 
        ● “ProductInfo Account” (PDA) 
        ● “NFT Token Account” (Seller’s) 
        ● “NFT Mint Account” (NFT Mint which seller is going to list) 
        ● “Vault NFT Token Account” (PDA token account which has same mint as “NFT Mint Account”) 
    - Logic
        ● Add infos to “ProductInfo Account” 
        ● Transfer NFT to Vault Account 
        ● Set Authority of Vault Account to PDA 
2. accept_offer
    - Params 
        ● Offer_Id - Accounts 
        ● “Seller Account” (Signer) 
        ● “Site Wallet Account” 
        ● “Wallet Authority Account” (PDA) 
        ● “ProductInfo Account” (PDA) 
        ● “Offerer NFT Token Account” 
        ● “NFT Mint Account” (NFT Mint which seller is going to list) 
        ● “Vault NFT Token Account” (PDA token account which has same mint as “NFT Mint Account”) 
        ● “Vault Authority Account” (PDA which is authority of Vault Token Account) 
    - Logic
        ● Transfer SOL from “Site Wallet Account” to “Seller Account” 
        ● Transfer NFT from “Vault NFT Token Account” to “Offerer NFT Token Account” 
        ● Close “ProductInfo Account” (PDA) 
3. make_offer 
    - Params 
        ● Offer Price 
    - Accounts 
        ● “Offerer Account” (Signer) 
        ● “Site Wallet Account” 
        ● “NFT Mint Account” 
        ● “Offerer NFT Token Account” 
        ● “ProductInfo Account” (PDA) 
    - Logic
        ● Add Offering infos to “ProductInfo Account”
        ● Transfer SOL as amount of Offer Price to “Site Wallet Account”
4. cancel_offer 
    - Params 
        ● Offer Id 
    - Accounts 
        ● “Offerer Account” (Signer) 
        ● “Site Wallet Account” 
        ● “Wallet Authority Account” (PDA) 
        ● “NFT Mint Account” 
        ● “ProductInfo Account” (PDA) 
    - Logic
        ● Remove Offering info from “ProductInfo Account” 
        ● Withdraw SOL from “Site Wallet Account” to “Offerer Account” 
5. cancel_list_for_sale 
    - Params - Accounts 
        ● “Seller Account” (Signer) 
        ● “ProductInfo Account” (PDA) 
        ● “NFT Token Account” (Seller’s) 
        ● “NFT Mint Account” (NFT Mint which seller is going to list) 
        ● “Vault Token Account” (PDA token account which has same mint as “NFT Mint Account”) 
        ● “Vault Authority Account” 
    - Logic
        ● Close “ProductInfo Account” 
        ● Transfer NFT from “Vault Token Account” to “NFT Token Account”