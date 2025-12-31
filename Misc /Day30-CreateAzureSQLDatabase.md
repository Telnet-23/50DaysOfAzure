## The Problem
The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to Azure. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. Recently, they started working on creating and configuring some database instances on Azure.

For this task, create one publicly accessible Azure SQL Database instance along with the following details:

1. The name of the Azure SQL Database must be xfusion-sqldb.

2. The server name must be xfusion-server-3015.

3. The compute + storage configuration should be Basic (For less demanding workloads).

4. The backup storage redundancy should be Locally-redundant backup storage.

5. Set the login admin username to xfusion-admin and set an appropriate password.

6. Set the database size to 2 GiB.

7. Keep the rest of the configurations as default. Finally, make sure the database is in the Ready state before submitting this task.

## The Solution
I was going to try this in the GUI but decided against it once I was unable to find any method that didnt involve a script. As that means that I would be learning absolutely nothing running a pre-made script, I opted for the GUI. 

I will say that SQL and databases in general are not a strengh of mine asnd something that I will actively take on to learn more about. So with that all said, I opened Azure and made the Database as requested. 
<img width="891" height="777" alt="image" src="https://github.com/user-attachments/assets/bb32657b-f0cb-4366-9f0e-44008ec36d22" />

And I ofcourse allowed plublic access
<img width="919" height="559" alt="image" src="https://github.com/user-attachments/assets/f3f716c4-d794-47a9-985b-b044a26d2d83" />

When I Went to create it, I kept getting a policy violation but once checking the logs, found it was due to the location. The deafault 'east us' was erroring when I initially tried to build it so I took a random stab in the dark. The logs told me the permitted locations so if you're readying this, use 'Westus'. 

## Thoughts and takeaways
Cool challenge. As mentioned, I dont do a great deal with databases so any hands on I can get with them, the better. Time for tea. 



