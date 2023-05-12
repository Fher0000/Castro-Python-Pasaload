# Castro-Python-Pasaload
Python program (Pasaload acitivity)
import threading
import multiprocessing
import time

bal = multiprocessing.Value('i', 10000)  
lock = threading.Lock()  

def PassALoad(amt, phonenum):
    global bal
    with lock:
        if bal.value >= amt:
            print("Please wait, processing pasaload to", phonenum, "...")
            time.sleep(2)  
            bal.value -= amt
            print("Congrats! The pasaload is successful! Your current balance is:", bal.value)
        else:
            print(" Oh no! Insufficient balance for pasaload.")

if __name__ == '__main__':
    amt = int(input("Good Day User! Please enter the amount you preferred for pasaload: "))
    phonenum = input("Please enter the contact number here: ")

   
    threads = []
    for _ in range(5):
        t = threading.Thread(target=PassALoad, args=(amt, phonenum))
        threads.append(t)
        t.start()

   
    for t in threads:
        t.join()

