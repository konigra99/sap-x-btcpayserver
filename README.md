# sap-x-btcpayserver
How to receive and invoice in bitcoin in your SAP S4/HANA on premise system

Please visit my blogpost in the SAP Community, to read my thoughts around this integration.
Leave a comment in the discussion and if you like it - please leave a like to make me happy!

https://community.sap.com/t5/technology-blogs-by-members/how-to-receive-and-invoice-bitcoin-in-sap-proof-of-concept/ba-p/13640808

![image](https://github.com/konigra99/sap-x-btcpayserver/assets/164070213/bd4933e4-48a9-4000-a29e-94eedb16fd9b)

![image](https://github.com/konigra99/sap-x-btcpayserver/assets/164070213/0b00f371-eb24-4a46-8358-21138a737b76)

![image](https://github.com/konigra99/sap-x-btcpayserver/assets/164070213/bc132039-750e-43df-a2cf-8be2dce1f1a9)


Do you like what you see?
If you want to achieve the same level of integration of btcpayserver into your S4HANA Development system, you need to follow these steps:

1. Setup a btcpayserver instance (https://btcpayserver.org/) This is a free and open source payment processor software - no third party involved!
   - btcpayserver comes with a bitcoin fullnode, a lightning node and a Store

2. Configure your btcpayserver and make it reachable via the internet.
   Configure the following list:
   - a Store on your btcpayserver (this is important for the API calls)
   - a bitcoin wallet
   - a lightning wallet / node
   - bitcoin and fiat exchange rate source (in my case, Kraken)
   - the checkout appearance (in my case, in the look of SAP)
   - an admin user and a API key (you can setup a dedicated "read only" and "create invoice"-only technical user with an API key for extra security)
   - depending on your setup:
      - give it an URL via your DNS provider (important for the Destination settings in SAP environment)
      - a certificate for secure https connection (important for the transaction STRUST in your SAP environment)
      - take care of your firewall within SAP (create an exception rule for your btcpayserver, so the SAP connection can be established)

5. Within your SAP environment, take the following steps:
   - create a Destination to your btcpayserver in t-code SM59
   - import your ssl-certificates into t-code STRUST and distribute it with t-code SMICM
   - create a package in SE80
   - create two database tables with the following fields
     Name: YTABINVOICE
     <img width="886" alt="image" src="https://github.com/konigra99/sap-x-btcpayserver/assets/164070213/c648ed3b-3b29-4970-b302-990547e1254a">
     Name:ZTABINV
     <img width="889" alt="image" src="https://github.com/konigra99/sap-x-btcpayserver/assets/164070213/7ad118d5-e69c-467c-bc7f-73a8c20bea0a">

   - Import the program main code Z_BITCOIN (insert your individual information where needed (Destination in t-code SM59, the URL, and StoreIDs))
   - Import the function module for the price Z_GET_PRICE (Destination in t-code SM59, the URL, and StoreIDs)
   - take care of the naming of the fields

6. Test it!

If you need further help, please reach out to me.
If you have any feedback, please let me know.

If a video tutorial would help, let me know and I will create one in due time for you.
