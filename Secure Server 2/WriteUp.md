**Write Up: Secure Server 2**

Files that we were provided with the problem: 

1) capture.pcap  
2) [johndoe.py](http://johndoe.py)  
3) server.py  
   

The difference between the 1st and this second part of the problem is basically that the AES here is not commutative, so we can say that the server does not actually receive the secret as it did in the first part. So we must extract the flag in between the process itself.

We will use an approach called **MITM(Meet In The Middle)** for solving this question.

We were provided with three values– \>

1. E2(E1(flag))   
2. E4(E3(E2(E1(flag))))  
3. D2(D1(E4(E3(E2(E1(flag))))))

Here E1 means encryption with key1 and so on…   
So now we start encrypting these values for the MITM approach, first with keys 3 and 4 as follows→

* Encrypt the first value with all the possible key values.  
* The correct key encryption would return the result like **E3(E2(E1(flag)))**.  
* Decrypt the second value provided again with all possible keys. The final result obtained should be like **E3(E2(E1(flag)))**

We want these two to be equal, which indicates that we have found keys 3 and 4

Now the same stuff as above for key 1 and 2→

* Correct key output should look like **D1(E4(E3(E2(E1(flag))).**  
* With decryption of the second provided value with all possible key values, u get output as **D1(E4(E3(E2(E1(flag))))** 

Similarly here too, when they both are equal we have found keys 1 and 2\. 

The script for solving this with the above MITM approach is attached as [**solution.py**](http://solution.py) in the github repo.

**The flag – scriptCTF{s3cr37\_m3ss4g3\_1337\!\_7e4b3f8d}**
