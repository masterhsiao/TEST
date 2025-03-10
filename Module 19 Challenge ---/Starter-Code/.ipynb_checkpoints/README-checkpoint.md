I am having trouble running step 3, my code seems correct and similar to the solved files from Module 19 but the solved files are out of date and this is a little beyond my capability.
I attached the docuementation I went through trying to fix this... thanks for undertstanding.

https://web3py.readthedocs.io/en/stable/web3.eth.html#web3.eth.Eth.default_account

https://web3py.readthedocs.io/en/stable/web3.eth.html#web3.eth.Eth.get_balance

https://web3py.readthedocs.io/en/stable/web3.eth.html#web3.eth.Eth.send_transaction

I would consider this module complete based on the circumstances Thank you very much, my pass or fail of the class depends on this.



##########################################################################################################################################################################

## Unit 19 Homework: Cryptocurrency Wallet

![An image shows a wallet with bitcoin.](Images/19-4-challenge-image.png)

### Background

You work at a startup that is building a new and disruptive platform called KryptoJobs2Go. KryptoJobs2Go is an application that its customers can use to find fintech professionals from among a list of candidates, hire them, and pay them. As KryptoJobs2Go’s lead developer, you have been tasked with integrating the Ethereum blockchain network into the application in order to enable your customers to instantly pay the fintech professionals whom they hire with cryptocurrency.

In this Challenge, you will complete the code that enables your customers to send cryptocurrency payments to fintech professionals. To develop the code and test it out, you will assume the perspective of a KryptoJobs2Go customer who is using the application to find a fintech professional and pay them for their work.

### What You're Creating

To complete this Challenge, you will use two Python files, both of which are contained in the starter folder.

The first file that you will use is called `krypto_jobs.py`. It contains the code associated with the web interface of your application. The code included in this file is compatible with the Streamlit library. You will write all of your code for this Challenge in this file.

The second file that you will use is called `crypto_wallet.py`. This file contains the Ethereum transaction functions that you have created throughout this module’s lessons. By using import statements, you will integrate the `crypto_wallet.py` Python script into the KryptoJobs2Go interface program that is found in the `krypto_jobs.py` file.

Integrating these two files will allow you to automate the tasks associated with generating a digital wallet, accessing Ethereum account balances, and signing and sending transactions via a personal Ethereum blockchain called Ganache.

Specifically, you will assume the perspective of a KryptoJobs2Go customer in order to do the following:

* Generate a new Ethereum account instance by using the mnemonic seed phrase provided by Ganache.

* Fetch and display the account balance associated with your Ethereum account address.

* Calculate the total value of an Ethereum transaction, including the gas estimate, that pays a KryptoJobs2Go candidate for their work.

* Digitally sign a transaction that pays a KryptoJobs2Go candidate, and send this transaction to the Ganache blockchain.

* Review the transaction hash code associated with the validated blockchain transaction.

Once you receive the transaction’s hash code, you will navigate to the Transactions section of Ganache to review the blockchain transaction details. To confirm that you have successfully created the transaction, you will save screenshots to the README.md file of your GitHub repository for this Challenge assignment.

### Instructions

The steps for this challenge are broken out into the following sections:

* Import Ethereum Transaction Functions into the KryptoJobs2Go Application
* Sign and Execute a Payment Transaction
* Inspect the Transaction on Ganache

#### Step 1: Import Ethereum Transaction Functions into the KryptoJobs2Go Application

In this section, you'll import several functions from the `crypto_wallet.py` script into the file `krypto_jobs.py`, which contains code for KryptoJobs2Go’s customer interface, in order to add wallet operations to the application. For this section, you will assume the perspective of a KryptoJobs2Go customer (i.e., you’ll provide your Ethereum wallet and account information to the application).

Complete the following steps:

1. Review the code contained in the `crypto_wallet.py` script file. Note that the Ethereum transaction functions that you have built throughout this module&mdash;including `wallet`, `wallet.derive_acount`, `get_balance`, `fromWei`, `estimateGas`, `sendRawTransaction`, and others&mdash;have now been incorporated into Python functions that allow you to automate the process of accessing them.

2. Add your mnemonic seed phrase (provided by Ganache) to the starter code’s `SAMPLE.env` file. When the information has been added, rename the file `.env`.

3. Open the `krypto_jobs.py` file. Toward the top of the file, after the import statements that are provided, import the following functions from the `crypto_wallet.py` file:

    * `generate_account`

    * `get_balance`

    * `send_transaction`

4. Within the Streamlit sidebar section of code, create a variable named `account`. Set this variable equal to a call on the `generate_account` function. This function will create the KryptoJobs2Go customer’s (in this case, your) HD wallet and Ethereum account.

5. Within this same section of the `krypto_jobs.py` file, define a new `st.sidebar.write` function that will display the balance of the customer’s account. Inside this function, call the `get_balance` function and pass it your Ethereum `account.address`.

#### Step 2: Sign and Execute a Payment Transaction

Next, you'll write the code that will calculate a fintech professional’s wage, in ether, based on the worker’s hourly rate and the number of hours that they work for a customer. (The fintech professionals’ hourly rates are provided in the `candidate_database` that is found in `krypto_jobs.py`.)

You will then write code that uses the calculated wage value to send a transaction that pays the worker. This code should allow the KryptoJobs2Go customer to authorize the transaction with their digital signature. For the purpose of testing out this application, you will use your own Ethereum account information as the customer account information.

To accomplish all of this, complete the following steps:

1. KryptoJobs2Go customers will select a fintech professional from the application interface’s drop-down menu, and then input the amount of time for which they’ll hire the worker. Code the application so that once a customer completes these steps, the application will calculate the amount that the worker will be paid in ether. To do so, complete the following steps:

    * Write the equation that calculates the candidate’s wage. This equation should assess the candidate’s hourly rate from the candidate database (`candidate_database[person][3]`) and then multiply this hourly rate by the value of the `hours` variable. Save this calculation’s output as a variable named `wage`.

    * Write the `wage` variable to the Streamlit sidebar by using `st.sidebar.write`.

2. Now that the application can calculate a candidate’s wage, write the code that will allow a customer (you, in this case) to send an Ethereum blockchain transaction that pays the hired candidate. To accomplish this, locate the code that reads `if st.sidebar.button("Send Transaction")`. You’ll need to add logic to this `if` statement that sends the appropriate information to the `send_transaction` function (which you imported from the `crypto_wallet` script file). Inside the `if` statement, add the following functionality:

    * Call the `send_transaction` function and pass it three parameters:

    * Your Ethereum `account` information. (Remember that this `account` instance was created when the `generate_account` function was called.) From the `account` instance, the application will be able to access the `account.address` information that is needed to populate the `from` data attribute in the raw transaction.

    * The `candidate_address` (which will be created and identified in the sidebar when a customer selects a candidate). This will populate the `to` data attribute in the raw transaction.

    * The `wage` value. This will be passed to the `toWei` function to determine the wei value of the payment in the raw transaction.

    * Save the transaction hash that the `send_transaction` function returns as a variable named `transaction_hash`, and have it display on the application’s web interface.

#### Step 3: Inspect the Transaction

Now it's time to put it all together and test the KryptoJobs2Go application with your newly integrated Ethereum wallet. You will send a test transaction by using the application’s web interface, and then look up the resulting transaction in Ganache. To do so, complete the following steps:

1. From your terminal, navigate to the project folder that contains your `.env` file and the `krypto_jobs.py` and `crypto_wallet.py` files. Be sure to activate your Conda `dev` environment if it is not already active.

2. To launch the Streamlit application, type `streamlit run krypto_jobs.py`.

3. On the resulting webpage, select a candidate that you would like to hire from the appropriate drop-down menu. Then, enter the number of hours that you would like to hire them for. (Remember, you do not have a lot of ether in your account, so you cannot hire them for long!)

4. Click the Send Transaction button to sign and send the transaction with your Ethereum account information. Navigate to the Transactions section of Ganache.

    * Take a screenshot of your address balance and history on Ganache. Save this screenshot to the README.md file of your GitHub repository for this Challenge assignment.

    * Take a screenshot of the transaction details on Ganache. Save this screenshot to the README.md file of your GitHub repository for this Challenge assignment.

5. Return to the original transaction, and click the transaction’s To address.

* Take a screenshot of the recipient’s address balance and history from your Ganache application. Save this screenshot to the README.md file of your GitHub repository for this Challenge assignment.

---

## Submission

* Upload the files for this assignment to your GitHub repository.

* Submit the link to your GitHub repo on Bootcamp Spot.

---

© 2022 edX Boot Camps LLC. Confidential and Proprietary. All Rights Reserved.
