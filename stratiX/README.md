Instructions
=
Build docker image by the following command:<br>
```
docker image build -t [image_name] .
```
Run container and attack:<br>
```
docker container run -it [image_name]
```
 The dockerfile for this modifies stratisX source code to add regtest mode for easy demostration of vulnerability #2(which was not supported by default in stratisX)
