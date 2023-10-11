import conf
import requests,json,time
from boltiot import Bolt,Sms
API_KEY = "" # Bolt API Key
DEVICE_ID = "" # Bolt Device ID
SID = '' # Twilio Account SID
AUTH_TOKEN = '' #Twilio Auth Token
FROM_NUMBER = '' # Twilio Trial Number
TO_NUMBER = '' #Your own mobile number
mybolt=Bolt(API_KEY,DEVICE_ID)
sms1=Sms(SID,AUTH_TOKEN,TO_NUMBER,FROM_NUMBER)
def get_crypto_price(u):
    url="http://min-api.cryptocompare.com/data/price?fsym="+u+"&tsyms=INR"
    response=requests.request("GET",url)
    response=json.loads(response.text)
    current_price=response["INR"]
    return current_price
def crypto(z):
    print("Enter the Quantity of the crypto currency,you have purchased:")
    k=float(input())
    print("Enter the Setpoint of the crypto currency,you have purchased:")
    sp=float(input())
    m=0
    while True:
        y=get_crypto_price(z)
        ss=int(y)
        print("This is the current Market Rate of "+z+" in INR")
        print(ss)
        p=(ss-sp)*(100/sp)
        p1=int(p)
        if(p1>=0):
            print("Your current Profit percent on the stock is ",p1)
        elif(p1<0):
            print("Your loss percent is",abs(p1))
        if 0<=p1<5:
            response=mybolt.digitalWrite("0","HIGH")
            print("the stock value is increased more than 1% higher than your rate:\n"+str(response))
        elif 5<=p1<10:
            response=mybolt.digitalWrite("1","HIGH")
            print("the stock value is increased more than 5% higher than your rate\n"+str(response))
        elif 10<=p1:
            response=sms1.send_sms("Cryptocurrency value is increased more than 10% kindly perform the needful exchange")
            print("the response from Twilio:\n"+str(response))
        elif p1==0 and sp<ss:
            response=mybolt.digitalWrite("0","HIGH")
            print("The stock value is just marginally higher than your rate\n",response)
        else:
            response=mybolt.digitalWrite("0","LOW")
            response=mybolt.digitalWrite("1","LOW")
            print("the prices of stock are not sufficient to exchange\n"+str(response))
        m+=1
        if m==2:
      
            print("Do you want to continue with same stock:(1/0) or to Open DATA SHEET (2)")
            s=int(input())
            if s==1:
                continue
            elif s==0:
                break
            elif s==2:
                print("Open Excel Sheet")
                import webbrowser
                webbrowser.open('https://docs.google.com/spreadsheets/d/15s0l_Zs21xVNPbXDzT7dUPd7XHfR1CVFn0lR-5khY7k/edit#gid=1362729064')
                break
            else:
                print("Kindly choose 1 for yes and 0 for No")
                continue
            
        time.sleep(10)
while True:
    try:
        print("----------------------------------------------------------------------------------------------------------------------------------------------------------------")
        print("Welcome to Crypto News Alert & Alert Engine Code:")
        print("The variety of Crypto-currency Available are:")
        print("1.Bitcoin [BTC]\n2.Ethereum [ETH]\n3.EOS [EOS]\n4.Xrp [XRP]\n5.Litecoin[LTC]\n6.Okex [OKB]\n7.Tron [TRX]\nKindly choose your Crypto from 1-7")
        ch=int(input())
        if (ch==1):
            crypto("BTC")
        elif(ch==2):
            crypto("ETH")
        elif(ch==3):
            crypto("EOS")
        elif(ch==4):
            crypto("XRP")
        elif(ch==5):
            crypto("LTC")
        elif(ch==6):
            crypto("OKB")
        elif(ch==7):
            crypto("TRX")
        else:
            print("Kindly choose a correct option, the choosen currency is invalid")
    except exceptions as e:
        print("error:",e)
