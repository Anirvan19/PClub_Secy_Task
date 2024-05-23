# PClub_Secy_Task
## FLAG-1
<b>pclub{path_trav3rsa1_1s_fun}</b></br>
So from the question, It is evident that our approach should be to find the file routes.txt, for that we need to understand how we are presented information on the website
Except for images and blogs everything is present there on the website and images and blogs are being extracted from the server. So from the network section in the inspect console we understand that images are being extracted through the getfile command which gets the file present on some directory on the server and presents its instance to you. So for the first flag just changing the name of the image to routes.txt worked.</br>

![image](https://github.com/Anirvan19/PClub_Secy_Task/assets/152109169/91ea82a3-71f0-4d84-8836-1484a9d2ed77)
![image](https://github.com/Anirvan19/PClub_Secy_Task/assets/152109169/a0da61ce-e399-4452-8127-63bab295a146)

## FLAG-2
<b>pclub{60:45:bd:af:3f:e5}</b></br>
Again from the question we know that for further penetration we would need to follow deep into routes.txt and the second flag might be the mac address of the eth0 which we need to find using command injection. There is a special page given in the routes.txt file and that is /ipdetails which is the most promising to find mac address so first entering the ip of the server we get all the details and if we try the ping command in linux terminal we get PING not PINGING so this is a linux based server and hence we'll try injecting linux commands. Starting from the command ip link, we get the mac address of the server.</br>

![image](https://github.com/Anirvan19/PClub_Secy_Task/assets/152109169/468a4b8e-723c-4d78-94a0-8ee285229960)

## FLAG-3
<b>pclub{01d_1s_g01d_sql1}</b></br>
Trying more commands on the /ipDetails page we find that ls command unfortunately does not work but the dir command does, this could lead us to our next flag. </br>

![image](https://github.com/Anirvan19/PClub_Secy_Task/assets/152109169/92aa8ab4-8017-45b3-b9b8-f0762e09a2f1)

we check the blogs.js file,</br>

![image](https://github.com/Anirvan19/PClub_Secy_Task/assets/152109169/2c4192d5-bc39-46d9-8265-6b17ded50eb0)

Looking at this file, it looks like the /getBlogDetail function gets the blogs data out of a SQL Table which has 4 columns the BlogIndex, BlogTitle, BlogDescription and the BlogLink.
the loop runs from the index 0 to 2 so we see only 3 blogs but if we manually change the number from the /getBlogDetail we see that there are actually 6 blogs. So the blogs table has 6 rows and 4 columns.</br>
So now our approach would be to inject SQL commands into this link to get more information on the tables present in the database, from the dir command there might also exist a users table because of users.json.</br>
We'll be using a tool called SQLmap to exploit the vulnerability present. After the analysis we get these vulnerabilities.</br>

![image](https://github.com/Anirvan19/PClub_Secy_Task/assets/152109169/cf22e000-08b8-498a-aa30-f443a09e8f6f)

We've got 3 of them - Boolean-based blind, time-based blind and Union query</br>
Now using the inbuilt --dbs command we get the databases present in the server.</br>

![image](https://github.com/Anirvan19/PClub_Secy_Task/assets/152109169/50aee17d-6f55-4ca4-867f-7b6cfee64e8b)

pclub_secy_task looks relevant to us now we will use the --tables command in this database.</br>

![image](https://github.com/Anirvan19/PClub_Secy_Task/assets/152109169/58a0942e-2dc0-41ff-b2fe-f8f961317bd2)

Now the blogs table had the same content we predicted. We now use the --dump command to retrieve information out of the table.</br>
From the Hints Table we get, </br>

![image](https://github.com/Anirvan19/PClub_Secy_Task/assets/152109169/a2950324-5c59-4ba0-b6cb-4697b3b72531)

and then the USERS Table, </br>

![image](https://github.com/Anirvan19/PClub_Secy_Task/assets/152109169/5566c419-ac46-4352-ab61-6d4873745c5c)

Now we know the user kaptaan and we use an online md5 decrypter, MD5 hash is not reversible but such online tools check their database and match it with similar hashes</br>
I am using https://md5decrypt.net/ for this. </br>
Then entering this information in the secy login page we get our flag. :D

## FLAG 4
<b>pclub{data_1s_3v3ryth1ng}</b></br>
Hints table said that 3 users have files now my social engineering knowledge predicted that the users could be amansg22 and ritvikg22 and from amansg22 we get an image ariitk.jpeg!!</br>
Now we have a stegano task at hand!!</br>
1.) Exiftool - nothing informative</br>
2.) Strings - nothing informative</br>
3.) Steghide - DAMN YESSS, we got something</br>

![image](https://github.com/Anirvan19/PClub_Secy_Task/assets/152109169/b23758de-79e2-4cf7-bb26-2db3e89d1ba6)

There is an embedded image here called qr_code.png, Scanning this QR we get</br>
<b>Y3B5aG97cW5nbl8xZl8zaTNlbGd1MWF0fQ==</b></br>
which looks like a b64 encrypted message, decrypting it back we get</br>
cpyho{qngn_1f_3i3elgu1at}, which looks like shift ciphered message and using rot13 we get our flag</br>

![image](https://github.com/Anirvan19/PClub_Secy_Task/assets/152109169/61a06380-65ee-4dc0-bdd9-c95fac297656)

## FLAG-5
<b></b></br>
From ritvikg22's user login page we get a pastebin file</br>

![image](https://github.com/Anirvan19/PClub_Secy_Task/assets/152109169/4f710ce4-2a13-40b2-a312-5a5b5a73c513)

which when connected to nc asks for username and password prompt which we need to exploit in order to get a flag.</br>
Decompiling the binary file using Ghidra
















