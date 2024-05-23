# PClub_Secy_Task
## FLAG-1
<p>pclub{path_trav3rsa1_1s_fun}</p>
<p>So from the question, It is evident that our approach should be to find the file routes.txt, for that we need to understand how we are presented information on the website
Except for images and blogs everything is present there on the website and images and blogs are being extracted from the server. So from the network section in the inspect console we understand that images are being extracted through the getfile command which gets the file present on some directory on the server and presents its instance to you. So for the first flag just changing the name of the image to routes.txt worked.</p>
![image](https://github.com/Anirvan19/PClub_Secy_Task/assets/152109169/91ea82a3-71f0-4d84-8836-1484a9d2ed77)
![image](https://github.com/Anirvan19/PClub_Secy_Task/assets/152109169/a0da61ce-e399-4452-8127-63bab295a146)

## FLAG-2
<p>pclub{60:45:bd:af:3f:e5}</p>
<p>Again from the question we know that for further penetration we would need to follow deep into routes.txt and the second flag might be the mac address of the eth0 which we need to find using command injection. There is a special page given in the routes.txt file and that is /ipdetails which is the most promising to find </p>
