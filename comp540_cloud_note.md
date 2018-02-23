# A Brief Note of Using Jupyter on Remote Machine and Setting up a AWS Server for GPU Computing

------

## **Running a Jupyter notebook on Clear.**
### For Linux and Mac user

 1. Open a new terminal window
 2. Type in: 
```
ssh yourNetId@ssh.clear.rice.edu
```
Then type in your password, which is the same password you use when you logging in Canvas.
 3. Install Jupyter, if you have installed, skip to next step.
```
pip install --user jupyter
```
This command will install Jupyter under user's home directory. If you do not include **--user** flag, you will encounter permission denied error.
 4. Start your Jupyter notebook
```
cd ~ 
cd ./local/bin
jupyter notebook 
```

Perhaps you would like to designate a certain port for Jupyter, if so, use:

```
jupyter notebook --port = the port you want
```
Then you can see your Jupyter notebook is running, find something like 

>  http://localhost:8889/?token=fd4bb9b48f8c71bf2b4d6c94d273ac1db57aae5db1f8658f

And copy the port token, which is ""8889" and "fd4bb9b48f8c71bf2b4d6c94d273ac1db57aae5db1f8658f", we will use it later.
5. Do not shutdown the terminal you have opened and open a new terminal.
6. Type in the command below:

```
ssh -N -f -L localhost:12345:localhost:[the port you saw/chose in step 4] yourNetId@ssh.clear.rice.edu
```

The flag -L means that the local machine forward the local port to the remote port. For more information see [here][1] 
7. Open your browser, type in **localhost:12345** in address bar.
8. Copy the token you saved in step 4 into the text field on the top of the page.

### For Windows user
1. Download Putty from [here][2]. After you get used to Putty, you may want to try XShell.
2. Open Putty Click **"Session"** on the left side of the window. Type in **netId@ssh.clear.rice.edu** under **"Host Name"**
3. Click **"ssh"** expand the tree then click **"tunnel"**.
4. Click the checkbox of **"Local ports accept..."**
5. In **"Source Port"** choose any port you like. For example: 12345
6. In **"Destination"**, type in **localhost:[the port you would like choose]**, then click **"add"**
7. Back to the **"Session"** tab, click **"Open"**.
8. Type in your password
9. Install Jupyter, if you have installed, skip to next step.
```
pip install --user jupyter
```
This command will install Jupyter under user's home directory. If you do not include **--user** flag, you will encounter permission denied error.
10. Start your Jupyter notebook
```
cd ~ 
cd ./local/bin
jupyter notebook 
```

Perhaps you would like to designate a certain port for Jupyter, if so, use:

```
jupyter notebook --port = the port you chose in Putty
```
Then you can see your Jupyter notebook is running, find something like 

>  http://localhost:8889/?token=fd4bb9b48f8c71bf2b4d6c94d273ac1db57aae5db1f8658f

And copy the port token, which is ""8889" and "fd4bb9b48f8c71bf2b4d6c94d273ac1db57aae5db1f8658f", we will use it later.
11. Open your browser, type in **localhost:12345** in address bar.
12. Copy the token you saved in step 10 into the text field on the top of the page.

## How to start a AWS EC2 GPU server machine
### Always remember to stop or terminate your AWS machine after using it!!!
### Apply credit of AWS educate program
1. Create an account on aws.amazon.com, find the account ID for step 2.
2. Go to [here][3], click **Student** and fill in the form with your @rice.edu emaill address. If you use the link in Github student pack, you will get more than \$100 credit.
3. If approved your will get \$100 credit for AWS. 

### Start a AWS EC2 GPU Server for Deep Learning
1. You have to raise the limit before you create an instance. To raise the limit, go to [AWS support page][4], create a case. For **"Regarding"**, select **"Service Limit Increase"**. For **"Limit Type"**, select **"EC2 instance"**. For **"region"**, select **"Ohio"**. For **"Primary Instance Type"**, select **"p2.xlarge"**. Note that, in p2.xlarge, there is a Tesla K80 GPU, which is suffient for personal use. If you would like to use more than one GPU at the same time, you may want to use **p2.x8large**.
2. Go back to the console, click **"Service"** then click **"EC2"**
3. Click the blue button **"create instance"**.
4. In the AMI webpage, select **"Deep Learning AMI"**.
5. Choose **p2.xlarge** on the next page, then click **"Review and Launch"**
6. Create or use exists key.
7. After some minutes, your EC2 instance is ready. Go back to the console, click **"Service"** then click **"EC2"**, then click **"Instance"** on the left side. Select the instance you created, click **"connect"**, you can find the instruction of connecting the machine.

### How to running Jupyter on AWS EC2 (using private key)
The way we run Jupyter notebook on AWS EC2 is almost the same, however, we have to use a private key to log in EC2. 

#### For Linux/Mac
Whenever you use **ssh** command, remember add **-i "youkey.pem"**. For example:
```
ssh -i "yourkey.pem" username@remoteMachineAddress
```

#### For Windows
1. Expand **"ssh"** on the left side of Putty window, and click **"Auth"**.
2. Click **"Browse"** then select your key pair file.
3. Then Click **"Open"**.

## Always remember to stop or terminate your AWS machine after using it!!!
  [1]: https://linux.die.net/man/1/ssh
  [2]: https://www.putty.org/
  [3]: https://www.awseducate.com/Registration
  [4]: https://console.aws.amazon.com/support/home
