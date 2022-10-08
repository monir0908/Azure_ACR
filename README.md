# Azure_ACR

### Step 01<hr>
Go to Azure Portal and create a container registry (e.g. registry name as: monir0908). <br>
Once the deployment is successful, it will provide us the following:<br>

<b>Login server:</b> monir0908.azurecr.io <br> 

We will need this login server later.

### Step 02<hr>
I am assuming we have `azure cli` installed. If yes, then type:<br>

```
az login
```

To login to the `acr`
```
az acr login -n monir0908
```

For example, let's say we have an image in our machine called `nginx`. And we want that image to be sent to azure `acr`. <br>
Before doing that, we need to `tag` our potential image that we want to push on to the `acr` registry. In our case, it is `nginx` image.



### Step 03<hr>
To check images stored in your machine

```
docker images
```

Now, it will display all the images stroed in our local machine. 
We have 5 images in our local machine. Let's pick `nginx` image for pushing it to the `acr`.
![Tagged Image](image_id.PNG)

We need the `IMAGE ID` of the `nginx` image. Let's copy the `IMAGE ID` of `nginx` image.
In our case it is `51086ed63d8c`.
![Tagged Image](image_id.PNG)

### Step 04<hr>
To tag a image:
```
docker tag 51086ed63d8c monir0908.azurecr.io/my-nginx:v1
```

Let's run the follwing command to see if tagging worked:
```
docker images
```

It should display our tagged version of image with other images available:

![Tagged Image](image_tagged.PNG)


























