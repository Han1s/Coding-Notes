# CURL Basics

## GET 

- `curl https://jsonplaceholder.typicode.com/posts`

## GET with headers

- `curl -i https://jsonplaceholder.typicode.com/posts` 
  - will show headers

## Output GET into a file

- `curl -o  test.txt https://jsonplaceholder.typicode.com/posts`
  - will download the posts and ouput them to `test.txt`file 

## Make a file from GET

- `curl -O https://jsonplaceholder.typicode.com/posts`
  - will download and create `posts` file

## Download image

- `curl -O image_address`
  - will download img from the internet

## Download  but limit the speed

- `curl -O --limit-rate 1000B https://jsonplaceholder.typicode.com/posts`
  - will download it with limit

## POST

- `curl --data "title=Hello&body=Hello world" https://jsonplaceholder.typicode.com/posts`
  - makes post request with the data payload

## PUT

- `curl -X PUT -d "title=Hello&body=Hello world" https://jsonplaceholder.typicode.com/posts/3`
  - PUT request

## DELETE Request

- `curl -X DELETE https://jsonplaceholder.typicode.com/posts/3`
  - makes DELETE request

## Authentication

- `curl -u honza:12345 http://xx`
  - for authentication

## Follow redirects

- `curl http://google.com`
  - will redirect because we used `http`
  - to actually follow that we need to use: `curl -L http://google.com`

## Send a file

- `curl -u test@traversymedia.com:123456! -T hello.txt ftp://ftp.traversymedia.com`

## Download a file

- `curl -u test@traversymedia.com:123456! -O ftp://ftp.traversymedia.com/hello.txt`