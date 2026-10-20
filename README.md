# SQL-Injection-Burp-Suite

Burp Suite Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data

## 1. Point of the Lab

The point of this class is to learn what SQL-injection (SQLi) is, how to find and exploit different types of SQLi vulnerabilities and How to prevent them. Materials are from PortSwigger Academy and for tests I used Burp Suite Community edition.

## 2. Labs described step by step

### Lab 1: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
The point of the lab was to see if we can use SQLi to change the result we can get from the database, and get products that we are not supposed to see

#### First step: Reconnaissance
On the first page we find categories, when we click on any of them we see in URL app is sending GET-request with parameter `'category'`

<img width="1149" height="248" alt="Screenshot 2026-10-20 at 12 32 25" src="https://github.com/user-attachments/assets/335d5c95-5aec-4221-9674-c559a480cee6" />

This information is enough to make a plan of an attack

#### Second step: Theory
From gathered information we can assume how backend might look like SQL might look like:\
```SELECT * FROM products WHERE category = 'SOME_CATEGORY' AND stock = 1```
assuming that they wouldn't want customers to see products that aren't in stock

#### Third step: Testing
1) Typing in `'` in URL to see if the input string is filtered. Symbol broke the page
<img width="260" height="145" alt="Screenshot 2026-10-20 at 13 04 56" src="https://github.com/user-attachments/assets/d86d8689-7064-45fe-88dc-59bb817123f3" />

From that we gather that `'` is breaking syntax logic of SQL-query. First sing of availability for SQLi

#### Fourth step: Payload

Now our goal is to change SQL-query so that filtering by category was always `true`.
For that we'll use `OR` and a condition that is always `true` which is  `1 = 1` and so that our new query won't be interrupted by old query we'll use `--` or `#`, depending on what will work for as comment symbol in this database.
So we insert `'+or+1=1--`, in database we should get something like this\
```SELECT * FROM products WHERE category = '' OR 1=1--' AND stock = 1```
everything after a `--` is now a comment and doesn't effect new request\
<img width="409" height="52" alt="Screenshot 2026-10-20 at 13 19 54" src="https://github.com/user-attachments/assets/6a7ccf12-e858-418c-b0ed-bd7d3d6872f5" />
 And after execution on page we get:\
 <img width="1186" height="714" alt="Screenshot 2026-10-20 at 13 21 06" src="https://github.com/user-attachments/assets/babc556b-44b3-4984-a4fd-5d57f06e7e21" />
which means we got all categories and products, that we weren't able to see before



--------------------------------------------------------------------------------------------------------------------------------------
### Lab 2: SQL injection vulnerability allowing login bypass



#### First step
--------------------------------------------------------------------------------------------------------------------------------------
### Lab 3:

#### First step


