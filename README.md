# RAILWAY-RESERVATION-SYSTEM
railway_data = []
user_accounts_data = []

def menu():
    while True:
        print('1. YES')
        print('2. NO')
        ch = int(input('DO YOU WANT TO CONTINUE OR NOT: ')) 
        
        if ch != 1:
            print('THANK YOU')
            break
        
        print('WELCOME TO ONLINE RAILWAY RESERVATION SYSTEM') 
        print('1. SIGN IN')
        print('2. SIGN UP')
        print('3. DELETE ACCOUNT')
        print('4. EXIT')
        
        ch1 = int(input('ENTER YOUR CHOICE: '))
        
        if ch1 == 1:
            if checking():
                print('WELCOME')
                main()
        elif ch1 == 2:
            if checking_1():
                main()
            else:
                print('PASSWORD ALREADY EXISTS')
        elif ch1 == 3:
            if checking_2():
                print('ACCOUNT DELETED')
            else:
                print('YOUR PASSWORD OR USER_NAME IS INCORRECT')
        elif ch1 == 4:
            print('THANK YOU') 
            break
        else:
            print('ERROR 404: PAGE NOT FOUND')

def main():
    while True:
        print('1. TICKET BOOKING')
        print('2. TICKET CHECKING')
        print('3. TICKET CANCELLING')
        print('4. ACCOUNT DETAILS')
        print('5. LOG OUT')
        
        ch = int(input('ENTER YOUR CHOICE: '))
        
        if ch == 1:
            ticket_booking() 
        elif ch == 2:
            ticket_checking()
        elif ch == 3:
            ticket_cancelling()
        elif ch == 4:
            checking_3()
        elif ch == 5: 
            print('THANK YOU')
            break
        else:
            print('ERROR 404: PAGE NOT FOUND')

def ticket_booking():
    nm = input('ENTER YOUR NAME: ')
    phno = input('ENTER YOUR PHONE NUMBER: ')
    age = int(input('ENTER YOUR AGE: '))
    print('M=MALE, F=FEMALE, N=NOT TO MENTION')
    gender = input('ENTER YOUR GENDER: ')
    fr = input('ENTER YOUR STARTING POINT: ')
    to = input('ENTER YOUR DESTINATION: ')
    date = input('ENTER DATE (DD/MM/YYYY): ')
    
    gender_dict = {'M': 'MALE', 'F': 'FEMALE', 'N': 'NOT TO MENTION'}
    entry = {'name': nm, 'phno': phno, 'age': age, 'gender': gender_dict.get(gender.upper(), 'NOT TO MENTION'), 
             'from': fr, 'to': to, 'date': date}
    railway_data.append(entry)
    print('BOOKED SUCCESSFULLY')

def ticket_checking():
    phno = input('ENTER YOUR PHONE NUMBER: ')
    for data in railway_data:
        if data['phno'] == phno:
            print('TICKET DETAILS:')
            for key, value in data.items():
                print(f'{key.upper()}: {value}')
            return
    print('TICKET DOES NOT EXIST')

def ticket_cancelling():
    phno = input('ENTER YOUR PHONE NUMBER: ')
    for i, data in enumerate(railway_data):
        if data['phno'] == phno:
            del railway_data[i]
            print('TICKET CANCELLED')
            return
    print('TICKET DOES NOT EXIST')

def checking_1():
    f = input("FIRST NAME: ")
    l = input("LAST NAME: ")
    a = input('USER NAME: ')
    b = input('PASSWORD: ')
    c = input('RE-ENTER YOUR PASSWORD: ')
    ph = input("PHONE NUMBER: ")
    print('M=MALE, F=FEMALE, N=NOT TO MENTION')
    gen = input('ENTER YOUR GENDER: ')
    dob = input("ENTER YOUR DATE OF BIRTH (DD/MM/YYYY): ")
    age = input('YOUR AGE: ')
    
    gender_dict = {'m': 'MALE', 'f': 'FEMALE', 'n': 'NOT TO MENTION'}

    if b == c:
        user_entry = {'fname': f, 'lname': l, 'user_name': a, 'password': b, 'phno': ph, 'gender': gender_dict.get(gen.lower(), 'NOT TO MENTION'), 'dob': dob, 'age': age}
        user_accounts_data.append(user_entry)
        print(f'WELCOME {f} {l}')
        return True
    else:
        print('BOTH PASSWORDS ARE NOT MATCHING')
        return False

def checking():
    a = input('USER NAME: ')
    b = input('PASSWORD: ')
    for user_data in user_accounts_data:
        if user_data['user_name'] == a and user_data['password'] == b:
            print(f'HII {user_data["fname"]} {user_data["lname"]}')
            return True
    print('ACCOUNT DOES NOT EXIST')
    return False

def checking_2():
    a = input('USER NAME: ')
    b = input('PASSWORD: ')
    for i, user_data in enumerate(user_accounts_data):
        if user_data['user_name'] == a and user_data['password'] == b:
            print('IS THIS YOUR ACCOUNT?')
            for key, value in user_data.items():
                print(f'{key.upper()}: {value}')
            print('1. YES')
            print('2. NO')
            vi = int(input('ENTER YOUR CHOICE: '))
            if vi == 1:
                del user_accounts_data[i]
                return True
            elif vi == 2:
                print('SORRY, RETRY') 
    print('ACCOUNT DOES NOT EXIST')
    return False

def checking_3():
    a = input('USER NAME: ')
    b = input('PASSWORD: ')
    for user_data in user_accounts_data:
        if user_data['user_name'] == a and user_data['password'] == b:
            print('USER DETAILS:')
            for key, value in user_data.items():
                print(f'{key.upper()}: {value}')
            return
    print('ACCOUNT DOES NOT EXIST')

menu()
