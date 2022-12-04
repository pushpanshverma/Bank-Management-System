# Bank-Management-System
It is a Python project In Which users can do some basic operations like opening  new account, Deposit Amount, Withdraw amount, Balance enquiry,  Display user Details and  Close Account.  MySql is Used to create and manage database
from distutils.util import execute
import mysql.connector
mydb=mysql.connector.connect(host='localhost', user='root', password='admin@12345', database='bank_management')
def OpenAcc():
    n=input("Enter the name:")
    ac=input("enter the account number:")
    db=input("enter the date of birth:")
    add=input("Enter the address:")
    cn=input("Enter the contact number:")
    ob=int(input("Enter the opening balance:"))
    data1=(n,ac,db,add,cn,ob)
    data2=(n,ac,ob)
    sql1=('insert into account values(%s,%s,%s,%s,%s,%s)')
    sql2=('insert into amount values()%s,%s,%s')
    x=mydb.cursor()
    x.execute(sql1,data1)
    x.execute(sql2,data2)
    mydb.commit()
    print("Data Entered successfully")


def DepoAmo():
    amount=input("enter the amount the amount you want to deposit")
    ac=input("enter the account number:")
    a='select balance from amount whereAccNo=%s'
    data=(ac,)
    x=mydb.cursor()
    x.execute(a,data)
    result=x.fetchone()
    t=result[0]+amount
    sql=('update amount set balance where AccNo=%s')
    d=(t,ac)
    x.execute(sql,d)
    mydb.commit()
    main()

def withdrawAmount():
    amount=input("enter the amount the amount you want to withdraw")
    ac=input("enter the account number:")
    a='select balance from amount whereAccNo=%s'
    data=(ac,)
    x=mydb.cursor()
    x.execute(a,data)
    result=x.fetchone()
    t=result[0]-amount
    sql=('update amount set balance where AccNo=%s')
    d=(t,ac)
    x.execute(sql,d)
    mydb.commit()
    main()

def BalEnq():
     ac=input("enter the account number:")
     a='select * from amount where AccNo=%s'
     data=(ac,)
     x=mydb.cursor()
     x.execute(a,data)
     result=x.fetchone()
     print("BAlace for account:",ac,"is",result([-1]))
     main()

def DisDetails():
     ac=input("enter the account number:")
     a='select * from amount where AccNo=%s'
     data=(ac,)
     x=mydb.cursor()
     x.execute(a,data)
     result=x.fetchone()
     for i in result:
        print(i)
        main()

def CloseAcc():
    ac=input("enter the account number:")
    sql1='delete from account where AccNo=%s'
    sql2='delete from amount where AccNo=%s'
    data=(ac,)
    x=mydb.cursor()
    x.execute(sql1,data)
    x.execute(sql2,data)
    mydb.commit()
    main()



def main():
    
    print('''
    1. OPEN NEW ACCOUNT
    2. DEPOSIT AMOUNT
    3. WITHDRAW AMOUNT
    4. BALANCE ENQUIRY
    5. DISPLAY CUSTOMER DETAILS
    6. CLOSE AN ACCOUNT
       ''')
choice=input("enter the task that you want to perform:")
if(choice=='1'):
    OpenAcc()
elif(choice=='2'):
    DepoAmo()
elif(choice=='3'):
    withdrawAmount()
elif(choice=='4'):
    BalEnq()
elif(choice=='5'):
    DisDetails()
elif(choice=='6'):
    CloseAcc()
else:
    print("Invalid Choice") 
    main()   
main()
